[ ![Codeship Status for lexoyo/stage](https://codeship.com/projects/3bbb51a0-ea08-0133-a1fa-5a99213623df/status?branch=master)](https://codeship.com/projects/147777)
[![Code Climate](https://codeclimate.com/github/lexoyo/stage/badges/gpa.svg)](https://codeclimate.com/github/lexoyo/stage)
[![Démo stage wysiwyg drag and drop](https://monitoshi.lexoyo.me/badge/1555368788372-6479)](https://lexoyo.me/stage/pub/)

## About this project

This "stage" component enables the user select elements, drag and drop them, resize them.

A component like this will be useful to the developer building any tool which includes a WYSIWYG.

This project is maintained, has very few dependencies and is used in [Silex website builder](https://www.silex.me)

[Here is a very simple example](https://lexoyo.me/stage/pub/).

## Features

* [x] move and resize elements
* [x] supports absolute position as well as elements in the flow
* [x] multi selection
* [x] shift + resize will keep proportions
* [x] drawing mode, which let the user select multiple elements easily or draw a new element on the stage
* [x] hooks give you full control over what is selectable, draggable, droppable, resizeable, a drop zone
* [x] events to be notified of every action of the user
* [x] scroll when the user moves near the border of the stage, or to show a specific element
* [x] handle the events outside the iframe (the user can drag an element and release the mouse outside the iframe)
* [ ] [vote and submit feature requests](https://github.com/lexoyo/stage/issues?q=is%3Aissue+is%3Aopen+label%3Aenhancement)

Here is a [list of features](https://github.com/lexoyo/stage/issues?q=is%3Aissue+is%3Aopen+label%3Aenhancement) which is the current road map (please vote with :+1:s).

## Use

See [the online demo](https://lexoyo.me/stage/pub/) and its sources: [html here](https://github.com/lexoyo/stage/blob/master/src/jade/index.jade) and [js here](https://github.com/lexoyo/stage/blob/master/src/ts/demo.js).

The component can be initialized like this, which will make it possible to select, move and resize all the elements marked with the `.selectable` css class.

```javascript
// All the div in the iframe
const iframe = document.querySelector('#iframe')
const stage = new Stage(iframe, iframe.contentDocument.querySelectorAll('div'))
```

The iframe is where you add elements with the `.selectable`, `.draggable`, `.resizeable`, `.droppable` css classes, which can then be moved and resized.

Your application can catch events and store the new style of the elements after a drop.

```
stage.on('drop', e => {
	console.log('elements have been moved or resized, store their new styles if you wish', e.elements);
});
```

By default the elements which can be dragged or moved are those with the CSS classes `.selectable`,`.draggable`, `.resizeable` but you can override this as follow. The `.droppable` CSS class can be overrided too:

```javascript
const stage = new Stage(iframe, {
	isSelectable: (el) => el.classList.contains('selectable'),
	isDroppable: (el, selection) => el.classList.contains('droppable'),
})
```

## Build

The build requires nodejs and npm, and it produces these files:
* `pub/stage.js`, which you need to include in your project
* `pub/stage.css`, which will be included in the iframe to draw the UI
* `pub/demo.html`, which is a demo page for you to test the component

Run `npm install` and `npm run build` to build these files.

## Dependencies

This component only depenency is [the redux library](https://www.npmjs.com/package/redux).

It uses [Typescript](https://www.typescriptlang.org/) to compile to Javscript and [less](http://lesscss.org/) to compile to CSS. Also the unit tests are written with [Jest](https://jestjs.io/).

## Contribute

Please [vote for the features which matter to you here](https://github.com/lexoyo/stage/labels/enhancement).

If you want to contribute code, [read this readme for an introduction to the source code](./src/ts/). And then you can help fixing the [issues found in the code by Code Climat](https://codeclimate.com/github/lexoyo/stage/issues) or find things to do [in these issues which need to be done](https://github.com/lexoyo/stage/labels/ready).

The source code is written in ES2015 with less and jade.
