# Drag and Drop

* [The future of drag and drop APIs](https://medium.com/@dan_abramov/the-future-of-drag-and-drop-apis-249dfea7a15f)
* [react-dnd](https://github.com/gaearon/react-dnd)
* [dnd-core](https://github.com/gaearon/dnd-core)
* [Sortable](http://rubaxa.github.io/Sortable/)
* [The HTML5 drag and drop disaster](http://www.quirksmode.org/blog/archives/2009/09/the_html5_drag.html)

DnD needs `mousedown`, `mousemove`, and `mouseup` for selecting the element, dragging it, and releasing it.

Most libraries handle `mousemove` and not a lot using HTML5 Drag and Drop API.

HTML5 API has:

* `dragstart`
* `dragend`
* `dragenter`
* `dragleave`
* `dragover`
* `drag`
* `drop`

