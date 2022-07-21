<a name="module_quary"></a>

## quary
Quary module.


* [quary](#module_quary)
    * [.Quary](#module_quary.Quary)
        * [new exports.Quary(node, [selector])](#new_module_quary.Quary_new)
        * [.access(key, [value])](#module_quary.Quary+access) ⇒ <code>any</code>
        * [.addClass(className)](#module_quary.Quary+addClass) ⇒ <code>Quary</code>
        * [.after(nodes)](#module_quary.Quary+after) ⇒ <code>Quary</code>
        * [.append(nodes)](#module_quary.Quary+append) ⇒ <code>Quary</code>
        * [.attr(name, [value])](#module_quary.Quary+attr) ⇒ <code>Quary</code> \| <code>string</code>
        * [.before(nodes)](#module_quary.Quary+before) ⇒ <code>Quary</code>
        * [.call(method, ...args)](#module_quary.Quary+call) ⇒ <code>Array</code>
        * [.ccall(method, ...args)](#module_quary.Quary+ccall) ⇒ <code>Quary</code>
        * [.emit(event, [customEventInit])](#module_quary.Quary+emit) ⇒ <code>Quary</code>
        * [.hasClass(className)](#module_quary.Quary+hasClass) ⇒ <code>bool</code>
        * [.off(evt, callback)](#module_quary.Quary+off) ⇒ <code>Quary</code>
        * [.on(evt, noSelfOrCallback, [callback])](#module_quary.Quary+on) ⇒ <code>Quary</code>
        * [.once(evt, callback)](#module_quary.Quary+once) ⇒ <code>Quary</code>
        * [.prepend(nodes)](#module_quary.Quary+prepend) ⇒ <code>Quary</code>
        * [.prop(name, [value])](#module_quary.Quary+prop) ⇒ <code>Quary</code> \| <code>any</code>
        * [.query(selector)](#module_quary.Quary+query) ⇒ <code>Quary</code>
        * [.removeClass(className)](#module_quary.Quary+removeClass) ⇒ <code>Quary</code>
        * [.shadow([template], [options])](#module_quary.Quary+shadow) ⇒ <code>Quary</code>
        * [.text([t])](#module_quary.Quary+text) ⇒ <code>Quary</code> \| <code>string</code>
        * [.toggleClass(className, [state])](#module_quary.Quary+toggleClass) ⇒ <code>Quary</code>
        * [.when(evt)](#module_quary.Quary+when) ⇒ <code>Promise</code>
    * [.quary(node, [selector])](#module_quary.quary) ⇒ <code>Quary</code>
    * [.template(template)](#module_quary.template) ⇒ <code>DocumentFragment</code> \| <code>dynTemplate</code>


* * *

<a name="module_quary.Quary"></a>

### quary.Quary
Quary Class. It extends Array, the elements being the nodes
selected or passed on initialization.
It is exported so that you can extend it or manipulate the prototype
or do whatever you like to it.

**Kind**: static class of [<code>quary</code>](#module_quary)  

* [.Quary](#module_quary.Quary)
    * [new exports.Quary(node, [selector])](#new_module_quary.Quary_new)
    * [.access(key, [value])](#module_quary.Quary+access) ⇒ <code>any</code>
    * [.addClass(className)](#module_quary.Quary+addClass) ⇒ <code>Quary</code>
    * [.after(nodes)](#module_quary.Quary+after) ⇒ <code>Quary</code>
    * [.append(nodes)](#module_quary.Quary+append) ⇒ <code>Quary</code>
    * [.attr(name, [value])](#module_quary.Quary+attr) ⇒ <code>Quary</code> \| <code>string</code>
    * [.before(nodes)](#module_quary.Quary+before) ⇒ <code>Quary</code>
    * [.call(method, ...args)](#module_quary.Quary+call) ⇒ <code>Array</code>
    * [.ccall(method, ...args)](#module_quary.Quary+ccall) ⇒ <code>Quary</code>
    * [.emit(event, [customEventInit])](#module_quary.Quary+emit) ⇒ <code>Quary</code>
    * [.hasClass(className)](#module_quary.Quary+hasClass) ⇒ <code>bool</code>
    * [.off(evt, callback)](#module_quary.Quary+off) ⇒ <code>Quary</code>
    * [.on(evt, noSelfOrCallback, [callback])](#module_quary.Quary+on) ⇒ <code>Quary</code>
    * [.once(evt, callback)](#module_quary.Quary+once) ⇒ <code>Quary</code>
    * [.prepend(nodes)](#module_quary.Quary+prepend) ⇒ <code>Quary</code>
    * [.prop(name, [value])](#module_quary.Quary+prop) ⇒ <code>Quary</code> \| <code>any</code>
    * [.query(selector)](#module_quary.Quary+query) ⇒ <code>Quary</code>
    * [.removeClass(className)](#module_quary.Quary+removeClass) ⇒ <code>Quary</code>
    * [.shadow([template], [options])](#module_quary.Quary+shadow) ⇒ <code>Quary</code>
    * [.text([t])](#module_quary.Quary+text) ⇒ <code>Quary</code> \| <code>string</code>
    * [.toggleClass(className, [state])](#module_quary.Quary+toggleClass) ⇒ <code>Quary</code>
    * [.when(evt)](#module_quary.Quary+when) ⇒ <code>Promise</code>


* * *

<a name="new_module_quary.Quary_new"></a>

#### new exports.Quary(node, [selector])
Instantiate a Quary object.
Will create an Array (Quary is an Array!) of nodes from node
parameter.
If selector is passed, will query all nodes passed as node and the
node-array will be the concatenated result of the queries.
Note that for the node parameter, it selects node.shadowRoot by default,
if available. If you want the node and not its shadowRoot, pass ':host'
as selector.


| Param | Type | Description |
| --- | --- | --- |
| node | <code>Node</code> \| <code>Array.&lt;Node&gt;</code> \| <code>NodeList</code> \| <code>Quary</code> \| <code>String</code> | the initial node(s) |
| [selector] | <code>String</code> | if passed will query node(s) with selector |


* * *

<a name="module_quary.Quary+access"></a>

#### quary.access(key, [value]) ⇒ <code>any</code>
access the selected nodes' attributes, properties or text depending on
the leading character of the "key" parameter. This matches the syntax of
event handler methods!

**Kind**: instance method of [<code>Quary</code>](#module_quary.Quary)  
**Returns**: <code>any</code> - if you pass a value will return this for chaining,
otherwise will return an array with the retrieved values. NOTE: this
differs from the attr, prop, and text methods which will return the
value of the first matched element!  

| Param | Type | Description |
| --- | --- | --- |
| key | <code>String</code> | MUST be @key, .key, or § to access attr, prop, or text (see respective methods). |
| [value] | <code>any</code> | if you pass a value will call setters |


* * *

<a name="module_quary.Quary+addClass"></a>

#### quary.addClass(className) ⇒ <code>Quary</code>
add a CSS-class to all selected nodes; uses classList.add

**Kind**: instance method of [<code>Quary</code>](#module_quary.Quary)  
**Returns**: <code>Quary</code> - this for chaining calls  

| Param | Type | Description |
| --- | --- | --- |
| className | <code>string</code> | the class to add |


* * *

<a name="module_quary.Quary+after"></a>

#### quary.after(nodes) ⇒ <code>Quary</code>
Insert DOM after all selected nodes

**Kind**: instance method of [<code>Quary</code>](#module_quary.Quary)  
**Returns**: <code>Quary</code> - this for chaining calls  

| Param | Type | Description |
| --- | --- | --- |
| nodes | <code>Node</code> \| <code>Array.&lt;Node&gt;</code> \| <code>Quary</code> \| <code>String</code> \| <code>$.template</code> | DOM to insert; String will be transformed by calling $.template $.template is the result of a call to [$.template](#module_quary.template) |


* * *

<a name="module_quary.Quary+append"></a>

#### quary.append(nodes) ⇒ <code>Quary</code>
Append DOM to all selected nodes

**Kind**: instance method of [<code>Quary</code>](#module_quary.Quary)  
**Returns**: <code>Quary</code> - this for chaining calls  

| Param | Type | Description |
| --- | --- | --- |
| nodes | <code>Node</code> \| <code>Array.&lt;Node&gt;</code> \| <code>Quary</code> \| <code>String</code> \| <code>$.template</code> | DOM to insert; String will be transformed by calling $.template $.template is the result of a call to [$.template](#module_quary.template) |


* * *

<a name="module_quary.Quary+attr"></a>

#### quary.attr(name, [value]) ⇒ <code>Quary</code> \| <code>string</code>
get or set attribute values. If called with one parameters, will return
the respective attribute value of the first selected element. If called
with two parameters, will set the respective attribute for all selected
elements and return this for chaining.

**Kind**: instance method of [<code>Quary</code>](#module_quary.Quary)  
**Returns**: <code>Quary</code> \| <code>string</code> - this for chaining or attribute value  

| Param | Type | Description |
| --- | --- | --- |
| name | <code>string</code> | attribute name |
| [value] | <code>string</code> | value to set for attribute[name] on all elements; if undefined or false will call removeAttribute! |

**Example**  
```js
document.registerElement('hello-world', class extends HTMLElement {
	constructor() {super();}
	connectedCallback() {
		console.log($(this, ':host').attr('hello')); // -> “world?”
		$(this, ':host').attr('hello', 'world!');
		console.log($(this, ':host').attr('hello')); // -> “world!”
	}
});
<hello-world hello="world?"></hello-world>
```

* * *

<a name="module_quary.Quary+before"></a>

#### quary.before(nodes) ⇒ <code>Quary</code>
Insert DOM before all selected nodes

**Kind**: instance method of [<code>Quary</code>](#module_quary.Quary)  
**Returns**: <code>Quary</code> - this for chaining calls  

| Param | Type | Description |
| --- | --- | --- |
| nodes | <code>Node</code> \| <code>Array.&lt;Node&gt;</code> \| <code>Quary</code> \| <code>String</code> \| <code>$.template</code> | DOM to insert; String will be transformed by calling $.template $.template is the result of a call to [$.template](#module_quary.template) |


* * *

<a name="module_quary.Quary+call"></a>

#### quary.call(method, ...args) ⇒ <code>Array</code>
calls the designated method on each selected element and returns an array
and return an array of the results.

**Kind**: instance method of [<code>Quary</code>](#module_quary.Quary)  

| Param | Type | Description |
| --- | --- | --- |
| method | <code>String</code> | method name |
| ...args | <code>any</code> | arguments passed to the method |


* * *

<a name="module_quary.Quary+ccall"></a>

#### quary.ccall(method, ...args) ⇒ <code>Quary</code>
"Chainable Call", same as call but returns "this"

**Kind**: instance method of [<code>Quary</code>](#module_quary.Quary)  

| Param | Type | Description |
| --- | --- | --- |
| method | <code>String</code> | method name |
| ...args | <code>any</code> | arguments passed to the method |


* * *

<a name="module_quary.Quary+emit"></a>

#### quary.emit(event, [customEventInit]) ⇒ <code>Quary</code>
calls dispatchEvent selected element

**Kind**: instance method of [<code>Quary</code>](#module_quary.Quary)  

| Param | Type | Description |
| --- | --- | --- |
| event | <code>Event</code> \| <code>String</code> | if String will emit CustomEvent, optionally with customEventInit, otherwise emits event as passed |
| [customEventInit] | <code>Object</code> | use to initialize CustomEvent, only if event is String |


* * *

<a name="module_quary.Quary+hasClass"></a>

#### quary.hasClass(className) ⇒ <code>bool</code>
check if a selected element has the designated CSS-class ;
uses classList.contains

**Kind**: instance method of [<code>Quary</code>](#module_quary.Quary)  
**Returns**: <code>bool</code> - true if found, else undefined  

| Param | Type | Description |
| --- | --- | --- |
| className | <code>string</code> | the class to check |


* * *

<a name="module_quary.Quary+off"></a>

#### quary.off(evt, callback) ⇒ <code>Quary</code>
unregister an event handler on all selected nodes; support attribute
value, property- and text change events (see
[Quary.on](#module_quary.Quary+on));

**Kind**: instance method of [<code>Quary</code>](#module_quary.Quary)  
**Returns**: <code>Quary</code> - this for chaining  

| Param | Type | Description |
| --- | --- | --- |
| evt | <code>String</code> | event name to pass to removeEventListener. To stop listening to attribute changes do `attr:name`, for properties `prop:name`, for text use `text:` |
| callback | <code>function</code> | function to unregister |


* * *

<a name="module_quary.Quary+on"></a>

#### quary.on(evt, noSelfOrCallback, [callback]) ⇒ <code>Quary</code>
register an event handler on all selected nodes

This is a very powerful utility: you can register standard event handlers.
In this case it's just a shorthand for

```js
node.addEventListener(evt, callback)
```

However, you can thus also manage attribute-, property- and text event
handlers. Attribute and text event handlers are implemented as
MutationObservers. Property event handlers add getter and setter
methods to the object instance. It is done on the instance and not on the
prototype in order to less likely interfere with getters and setters
implemented in the class. Quary should - but currently doesn't -
handle those. I recommend not using property event handlers on components
that you do not own yourself. Properties are the most efficient way of
data binding, but they don't support it well. Attribute- and text event
handlers are no problem and should be the preferred way of interacting
with third party components. If an independent or third party component
does use properties to interact with its surrounding - which is perfectly
reasonable - it _should_ emit standart events in order notify client code
of changes.

Another peculiarity with property event handlers:
When your web component has custom properties, it will usually want to
react to changes of the properties. To this end you implement setter
methods. Now it can happen that something instantiates your element and
sets a property _before_ your element is registered. In these cases the
property will be written as an instance property _over_ the setter method
(which comes later!). This is a trivial problem but easy to miss and
somewhat tedious to work around. If you use `$(this).on('myProperty')`,
Quary will take care of this for you. However: don't implement
getters and/or setters for you properties, Quary will do that!
Just register your event handlers with it!

Quite often an event handler changes something and directly or indirectly
triggers the event, that it handles. The noSelf option helps break this
recursion. noSelf works with all types of event handlers.

**Kind**: instance method of [<code>Quary</code>](#module_quary.Quary)  
**Returns**: <code>Quary</code> - this for chaining  

| Param | Type | Description |
| --- | --- | --- |
| evt | <code>String</code> | event name to pass to addEventListener. To listen to attribute changes do 'attr:name'. This will create a MutationObserver for changes of the attribute called 'name'. For properties `prop:name`, for text use `text:` |
| noSelfOrCallback | <code>String</code> \| <code>function</code> | if you want to catch recursive events pass 'noSelf', otherwise put callback here |
| [callback] | <code>function</code> | function to call on event |

**Example**  
```js
$(this, 'button').on(
	'click',
	this._onButtonClick.bind(this)
);
$(this, 'button').on(
	'click',
	'noSelf',
	this._onButtonClick.bind(this)
);
$(this, ':host').on(
	'attr:hello',
	this._onHelloAtributeChange.bind(this)
);
// shorthand:
$(this, ':host').on('@hello', this._onHelloAtributeChange.bind(this));
$(this, ':host').on(
	'prop:hello',
	this._onHelloPropertyChange.bind(this)
);
// shorthand:
$(this, ':host').on('.hello', this._onHelloPropertyChange.bind(this));
$(this, 'label').on(
	'text:',
	this._onLabelTextChange.bind(this)
);
// shorthand:
$(this, 'label').on('§',      this._onLabelTextChange.bind(this));
```

* * *

<a name="module_quary.Quary+once"></a>

#### quary.once(evt, callback) ⇒ <code>Quary</code>
register an event handler on all selected nodes; support attribute
value, property- and text change events (see
[Quary.on](#module_quary.Quary+on));
callback will be called at most once; Note:
this is called "one" in jQuery. For _once_ I deviate from jQuery since
the name is IMHO a bad choice. Instead I use the better name established
in node.js

**Kind**: instance method of [<code>Quary</code>](#module_quary.Quary)  
**Returns**: <code>Quary</code> - this for chaining  

| Param | Type | Description |
| --- | --- | --- |
| evt | <code>String</code> | event name to pass to addEventListener. To listen to attribute changes do 'attr:name'. This will create a MutationObserver for changes of the attribute called 'name'. For properties `prop:name`, for text use `text:` |
| callback | <code>function</code> | function to call on event |


* * *

<a name="module_quary.Quary+prepend"></a>

#### quary.prepend(nodes) ⇒ <code>Quary</code>
Insert DOM as first content of all selected nodes

**Kind**: instance method of [<code>Quary</code>](#module_quary.Quary)  
**Returns**: <code>Quary</code> - this for chaining calls  

| Param | Type | Description |
| --- | --- | --- |
| nodes | <code>Node</code> \| <code>Array.&lt;Node&gt;</code> \| <code>Quary</code> \| <code>String</code> \| <code>$.template</code> | DOM to insert; String will be transformed by calling $.template getTemplate is the result of a call to this.getTemplate (see [$.template](#module_quary.template)) |


* * *

<a name="module_quary.Quary+prop"></a>

#### quary.prop(name, [value]) ⇒ <code>Quary</code> \| <code>any</code>
get or set property values. If called with one parameters, will return
the respective property value of the first selected element. If called
with two parameters, will set the respective property for all selected
elements and return this for chaining.

**Kind**: instance method of [<code>Quary</code>](#module_quary.Quary)  
**Returns**: <code>Quary</code> \| <code>any</code> - this for chaining or property value  

| Param | Type | Description |
| --- | --- | --- |
| name | <code>string</code> | property name |
| [value] | <code>string</code> | value to set for node[name] on all elements |

**Example**  
```js
document.registerElement('hello-world', class extends HTMLElement {
	constructor() {
		super();
		this.hello = 'world?'
	}
	connectedCallback() {
		console.log($(this, ':host').prop('hello')); // -> “world?”
		$(this, ':host').prop('hello', 'world!');
		console.log($(this, ':host').prop('hello')); // -> “world!”
	}
});
```

* * *

<a name="module_quary.Quary+query"></a>

#### quary.query(selector) ⇒ <code>Quary</code>
calls querySelector on all selected nodes and return new Quary
with the concatenated result. Note that this is analogous to jQuery's
find method. But since Quary is an Array, this would overwrite
Array.find. Thus I renamed the method to 'query.

**Kind**: instance method of [<code>Quary</code>](#module_quary.Quary)  
**Returns**: <code>Quary</code> - new Quary object with the query-result  

| Param | Type | Description |
| --- | --- | --- |
| selector | <code>String</code> | CSS-selector to query |


* * *

<a name="module_quary.Quary+removeClass"></a>

#### quary.removeClass(className) ⇒ <code>Quary</code>
remove a CSS-class from all selected nodes; uses classList.remove

**Kind**: instance method of [<code>Quary</code>](#module_quary.Quary)  
**Returns**: <code>Quary</code> - this for chaining calls  

| Param | Type | Description |
| --- | --- | --- |
| className | <code>string</code> | the class to remove |


* * *

<a name="module_quary.Quary+shadow"></a>

#### quary.shadow([template], [options]) ⇒ <code>Quary</code>
`$(this).shadow(template)` is just a shorthand for
```js
this.attachShadow(options).appendChild(template)
```
You will likely do something like this in the majority of your web
component's connectedCallbacks.

**Kind**: instance method of [<code>Quary</code>](#module_quary.Quary)  
**Returns**: <code>Quary</code> - this for chaining  

| Param | Type | Description |
| --- | --- | --- |
| [template] | <code>String</code> | passed to [$.template](#module_quary.template) |
| [options] | <code>Object</code> | passed to attachShadow |

**Example**  
```js
connectedCallback() {$(this).shadow('Hello world!');}
```

* * *

<a name="module_quary.Quary+text"></a>

#### quary.text([t]) ⇒ <code>Quary</code> \| <code>string</code>
get or set textNode values. If called without parameters, will return
the respective textNode value of the first selected element. If called
with one parameters, will set the respective textNode value for all
selected elements and return this for chaining.

**Kind**: instance method of [<code>Quary</code>](#module_quary.Quary)  
**Returns**: <code>Quary</code> \| <code>string</code> - this for chaining or text value  

| Param | Type | Description |
| --- | --- | --- |
| [t] | <code>String</code> | string to set on nodeValue |

**Example**  
```js
document.registerElement('hello-world', class extends HTMLElement {
	constructor() {super();}
	connectedCallback() {
		console.log($(this, ':host').text()); // -> “Hello world?”
		$(this, ':host').text('Hello world!');
		console.log($(this, ':host').text()); // -> “Hello world!”
	}
});
<hello-world>Hello world?></hello-world>
```

* * *

<a name="module_quary.Quary+toggleClass"></a>

#### quary.toggleClass(className, [state]) ⇒ <code>Quary</code>
toggle a CSS-class on all selected nodes; uses classList.toggle

**Kind**: instance method of [<code>Quary</code>](#module_quary.Quary)  
**Returns**: <code>Quary</code> - this for chaining calls  

| Param | Type | Description |
| --- | --- | --- |
| className | <code>string</code> | the class to toggle |
| [state] | <code>bool</code> | if true [addClass](#module_quary.Quary+addClass), if false [removeClass](#module_quary.Quary+removeClass) |


* * *

<a name="module_quary.Quary+when"></a>

#### quary.when(evt) ⇒ <code>Promise</code>
Alternative to
[Quary.once](#module_quary.Quary+once)
for promise based programming . Same syntax as once, but does not accept
callback, instead returns a promise (not "this" as most other messages!)
that resolves when the event occurs.

**Kind**: instance method of [<code>Quary</code>](#module_quary.Quary)  

| Param | Type |
| --- | --- |
| evt | <code>Event</code> | 


* * *

<a name="module_quary.quary"></a>

### quary.quary(node, [selector]) ⇒ <code>Quary</code>
Instantiate a Quary object. See [Quary](#module_quary.Quary)

**Kind**: static method of [<code>quary</code>](#module_quary)  
**Returns**: <code>Quary</code> - instance  

| Param | Type | Description |
| --- | --- | --- |
| node | <code>Node</code> \| <code>Array.&lt;Node&gt;</code> \| <code>NodeList</code> \| <code>Quary</code> | the initial node |
| [selector] | <code>String</code> | if passed will query node(s) with selector |


* * *

<a name="module_quary.template"></a>

### quary.template(template) ⇒ <code>DocumentFragment</code> \| <code>dynTemplate</code>
`$.template` creates an HTMLTemplateElement, initializes it with the passed
template string, stores it in its template library, and returns a clone
of the content. On subsequent calls, the existing template is efficiently
cloned.

Instead of template string you can also pass an object in order to generate
a dynamic template.
Dynamic templates can render arrays and render conditionally. Using
dynamic templates together with the Quary DOM helper insertion
functions like `append` allows you to easily manage nodes based on dynamic
conditions. Note that when a condition changes to false or an array shrinks,
Quary DOM helper _insertion_ methods will actually _remove_ content
instead of _insert_ it. See parameter description for details.

**Kind**: static method of [<code>quary</code>](#module_quary)  
**Returns**: <code>DocumentFragment</code> \| <code>dynTemplate</code> - cloned from the created
template, or the processor of a DynTemplate if passed an object for a
dynamic template.  

| Param | Type | Description |
| --- | --- | --- |
| template | <code>String</code> \| <code>Object</code> | the template string, use Object to define dynamic template |
| [template.array] | <code>Array</code> | array or function that returns an Array of items to render. If you don't want to use `template.update` you could also just return `{length: 5}` to render 5 nodes; if you just want conditional, you can also skip this; if you want to use the `update` callback with a conditional, you may pass `[item]` so that update gets that item |
| [template.chunks] | <code>Number</code> | if passed renders `chunks` elements and then calls `setTimeout` before continuing |
| [template.condition] | <code>Bool</code> | if false will render nothing |
| [template.done] | <code>function</code> | called when finished; optionally use together with `template.chunks`; `template.done` will never be called, if another dyn-template is rendered before this finished |
| template.template | <code>String</code> | template string for the rendered content |
| [template.update] | <code>function</code> | called for each element of the array with two parameters: `template.update(renderedContent, template.array[i])` Note that update may be called asynchronously when using `template.chunks` |
| [template.id] | <code>String</code> | key to identify rendered content; only required if you want multiple dynTemplates under the same parent |

**Example**  
```js
connectedCallback() {
	$(this).shadow('<ul></ul>');
	$(this, 'ul').append({
		array: () => $(this, ':host').attr('greet').split(),
		template: '<li></li>',
	});
}
```

* * *

