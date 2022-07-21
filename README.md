# quary
Micro-library for writing vanilla web components

* [Introduction](https://github.com/schrotie/quary/tree/master/documentation/introduction)
* [Motivation](https://github.com/schrotie/quary/tree/master/documentation/motivation)
* [API reference](https://github.com/schrotie/quary/tree/master/documentation/api)
* [Tutorial](https://github.com/schrotie/quary/tree/master/demo)


Quary is a tiny (2k uglified gzip, some 350 lines of code without comments and new lines as of this writing) utility library to help develop high performance vanilla web components. Some of its API syntax is reminiscent of web dev warhorse jQuery, but it's also a JavaScript array, hence the name.

It fascilitates selecting and monitoring/manipulating elements while constraining its scope to the most important features to remain highly maintainable. Most notably it unifies monitoring of events, attribute, property, and text changes and allows easy and traceable insertion into the DOM using arrays to initialize nodes and conditional rendering.

__Tiny__: demo/dbmonster.html is a selfcontained HTML app _below 10K_ (load without server into your Chrome or Firefox, for other browsers you may need to add more polyfills).

__High Performance__: quary dbmonster is among the fastest dbmonsters out there, one of the lowest memory footprints.

... _and all that at 100 lines of nicely structured code plus templates_

```html
<!DOCTYPE html>
<html>
	<head><script type="module">
		import $ from '../quary.mjs';

		const template = `
			<style>:host {
				cursor: pointer;
				font-family: sans-serif;
			}</style>
			<h3><slot></slot></h3>
			<ul></ul>
		`;

		window.customElements.define('hello-framework', class extends HTMLElement {
			constructor() {
				super();
				$(this).on('click', () => alert('Quary loves you!'));
			}
			connectedCallback() {
				$(this).shadow(template);
				$(this, 'ul').append({
					array   : $(this, ':host').attr('greet').split(' '),
					template: '<li> </li>',
					update  : (li, item) => li.text(`Hello ${item}!`),
				});
			}
		});
	</script></head>
	<body>
		<hello-framework greet="Angular React Vue">Greetings!</hello-framework>
	</body>
</html>
```
This works as is in Chrome, for other browsers you may need to load polyfills until they fully support the standard. Everything that starts with `$` above is Quary, the rest ist standart tech. The result of the above is:
### Greetings!
* Hello Angular!
* Hello React!
* Hello Vue!

... and that example renders so fast, it's hard to find the 3ms time for rendering between the other stuff Chrome does on page start up.

# Installation
```sh
npm i -s 'quary'
```

# Status

I used Quary in several projects over some years, among that several tens of thousands of professional production code lines. I weeded out bugs and stabalized the API. Quary comes with a test suite that covers 100% of the lines of code. Use at you own risk, but personally I consider it good to go.

# Intended Audience

If you're the ~~Visual Basic~~ Angular/React kind of dev, Quary is not for you. It does not hold your hand, it does not structure your project. Quary is for you, if you like to be in control, if you know what you're doing. It has zero magic, no surprises … actually, one thing did surprise me: you really need very little utility to empower you to write vanilly web components and make full use of the platform.
