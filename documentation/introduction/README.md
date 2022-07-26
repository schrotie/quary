# Hello world!

## Vanilla Web Component

```js
window.customElements.define('vanilla-hello-world', class extends HTMLElement {
	constructor() {
   	super();
		this.attachShadow({mode: 'open'}).innerHTML = 'Hello world!';
	}
});
```
## Quary
```js
import $ from '../quary.mjs';
window.customElements.define('sq-hello-world', class extends HTMLElement {
	constructor() {
   	super();
 		$(this).shadow('Hello world!');
  }
});
```

The difference is that Quary takes the template, creates an HTMLTemplateElement only once regardless of how many instances of hello-world are created and provides a native clone of that template. This is a lot more efficient than setting `innerHTML`.

# API

See [API reference](https://github.com/schrotie/quary/tree/master/documentation/api))

The Quary module has two exports. The first is `Quary`. You should only use it, if you want to modify/extend quary. The other export '`quary`' is also the default export. Thus `import {quary} ...` and `import quary ...` both work. I usually do `import $ ...` for brevity's sake.

So lets assume you did `import $ from '../quary.mjs';`. Now `$` is a function that takes one or two arguments and returns a `new Quary`.
jQuery works on the document, Quary is for web components which work on document-fragments. Thus the first arguments is always an entry node (or several). The second is an optional selector. If you pass the selector the result will be that of querying the entry nodes for the selector, otherwise the result is the entry node(s). Anyway, what you get is an Array (Quary extends Array!) of nodes augmented with a couple of methods to simplify your web component developer life.

The whole DOM API has 5 types of methods:
* __query__  
`constructor`, `query`
* __className__  
`addClass`, `removeClass`, `hasClass`
* __node insertion__  
`append`, `prepend`, `before`, `after`, `shadow`
* __value accessors__  
`attr`, `prop`, `text`
* __event management__  
`on`, `off`, `once`

Node insertion supports templates, and templates support conditional- and array-nodes. Whenever you pass a string to an insertion method, Quary will create a HTMLTemplateElement, if it does not find it in its library, and furtheron generates clones from that template.

Event management and accessors are symmetric: besides "normal" events you can register attribute, property, and text-events. Quary value accessors and event management combined provide a complete toolkit for two-way data binding. I do not recommend that, though, for anything but the smallest applications. Usually you should use something like Redux and its one way binding philosophy. However, many generic components will need to react to _their_ attribute and/or property changes and Quary has everything you need for this.

## Text Values and Chaining

So far didn't look like jQuery at all, I know. We're getting there:

```js
// First define the template. Quary never does anything to it, it's all vanilla:
const template = `
<style>
	span.checked {background: green;}
</style>
<span>Hello world?</span>`;

document.registerElement('hello-world', class extends HTMLElement {
	constructor() {super();}
	connectedCallback() {
		// should always do this, nodes can be connected several times!
		if(this.shadowRoot) return;
		$(this).shadow(template);
		$(this, 'span').text('Hello world!').toggleClass('checked');
	}
});
```

`$(this).shadow(template)` is just a shorthand for
```js
this.attachShadow({mode: open}).appendChild($.template(template))
```
Not much, but since it's used in most components ...

The `$` method always expects a node as first argument and an optional selector as its second. It calls `(node.shadowRoot || node).querySelectorAll(selector)` and returns its DOM swiss army knife that let's you do various stuff on the result similar to jQuery. In fact, if you are familiar with jQuery you should feel pretty much at home. Be aware, though, that Quary is a tiny subset of jQuery. The former was a compatibility layer as much as a utility and it filled many holes in the platform that the platform has meanwhile caught up upon ... and Quary aims to be minimal and _only_ address the most common web component use cases.

The example calls two methods in a chain: first `text` for each selected node calls `node.childNodes[0].nodeValue = text`, `text` being "Hello world!" in the example. Note that it brutally calls `childNodes[0]` if you call `text`. What it does is by far the best performing approach to change character-data in the DOM. This only works, if there already is a textNode there. In this case there is: "Hello world?" in the template. Usually I just leave an empty space where I want to manipulate nodeValues later, like so:

```html
<span> </span> <!-- works,  can   call text on span -->
<span></span>  <!-- breaks, can't call text on span -->
```

You may also use zero-width-space: `&#8203;`. This is an important point: if you want to put text into your template/shadowDOM, you have to create a textNode for it. Quary doesn't do that for you. It's just a space, but it is significant. Quary is just a collection of shorthand methods and no nanny. jQuery is a lot more powerful there, doing all kinds of magic. I want Quary to be my bare metal web component utility workbench, not more - and no surprises, no strings attached (pun intended).

So the example first calls `text`, which like all the DOM utilities returns a chainable reference to itself in most cases. If you call `text` without arguments, it will return the text of the first matched element (like jQuery). Here we manipulate, though, and get a chainable result on which (i.e. on the same `span` element in this case) on which `toggleClass` is called. `toggleClass` is like jQuerie's `toggleClass`, but it is just a shorthand for `node.classList.toggle`. If your browser does not support `classList` (_you know who ..._) you're screwed. Well, actually you're not screwed but required to load the respective polyfill. But you know, no nanny and blah ...


## Component Attributes

In many cases web components interface with their surroundings through attributes. Quary helps with that:

```js
document.registerElement('hello-world', class extends HTMLElement {
	constructor() {
		super();
		 // Creates an attribute mutation observer.
		$(this).on('attr:hello', this._onHello.bind(this));
	}
	_onHello() {
		console.log($(this, ':host').attr('hello')); // -> “world?”
		$(this, ':host').attr('hello', 'world!');
		console.log($(this, ':host').attr('hello')); // -> “world!”
	}
});
```
```html
<hello-world hello="world?"></hello-world>
```
There's a gotcha here: When you pass a node to `$` Quary selects its `shadowRoot` by default. In most cases, that's what you want, register event handlers on shadow DOM, traverse and manipulate it. In the cases where you don't want that, i.e. when you want to work with the host node, you have to explicitly select it using the `:host` selector. Note that in the constructor this is not necessary, since that is always called before the `shadowRoot` is attached.


## Arrays

This is somewhat of an acid test for code dealing with web components: every once in a while you need to render data that comes in an array and now you need to somehow iterate it and create DOM from it. If you used `innerHTML = template`, this is where you break, because a scrolled view will jump to the top if you do this. Here's Quary's take on the matter. This is also a slightly more involved example that brings together several features of Quary:
```js
window.customElements.define('hello-framework', class extends HTMLElement {
	constructor() {super();}
	connectedCallback() {
		$(this).shadow('<ul></ul>');
		$(this, 'ul').append({
			array   : $(this, ':host').attr('greet').split(' '),
			template: '<li> </li>',
			update  : (li, item) => li.text(`Hello ${item}!`),
		});
	}
});
```
```html
<hello-framework greet="Angular React Vue"></hello-framework>
```
Result:
- Hello Angular!
- Hello React!
- Hello Vue!

# More

Dynamic templates can do a bit more, chunked and/or conditional rendering for example. For this and a more helpers/features please refer to the [API reference](https://github.com/schrotie/quary/tree/master/documentation/api).
Also checkout the [demo directory](https://github.com/schrotie/quary/tree/master/demo). It contains a few examples on how to use Quary. Most notably, demo/todoRedux/ contains a [tutorial](https://blog.roggendorf.pro/2018/11/19/native-web-application-tutorial/) on how to develop modern native web applications.
