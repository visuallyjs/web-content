## [Release 1.1.4](/news/2026/06/29/release-1.1.4.md)

June 29, 2026 ·

<!-- -->

One min read

sporritt

Release 1.1.4 of VisuallyJs is now available, containing several nice updates to the canvas and its plugins.

### Miniview[​](#miniview "Direct link to Miniview")

* Lasso is shown on miniview while it is being used (can be switched off)

![Miniview lasso](https://static.visuallyjs.com/img/blog/miniview-lasso-1.1.4.png)

* Miniview now highlights vertices that are selected in the canvas

![Miniview lasso](https://static.visuallyjs.com/img/blog/miniview-selected-element-1.1.4.png)

### Lasso[​](#lasso "Direct link to Lasso")

* Added support for the lasso inside of groups

### Autopan[​](#autopan "Direct link to Autopan")

* Added support for automatically panning the surface when the user lassos outside of the visible area.
* Added support for auto pan of the canvas when a user is dragging a new edge or relocating an existing edge.

### Miscellaneous[​](#miscellaneous "Direct link to Miscellaneous")

* UI fires `EVENT_EDGE_DRAG_START`, `EVENT_EDGE_DRAG`, `EVENT_EDGE_DRAG_END`, `EVENT_EDGE_DRAG_ABORT` events during edge drag lifecycle now
* Added `addVertexDragFilter(f:VertexDragFilter<BrowserElement>)` method to `Surface`
* Diagrams do not, by default, draw a border around a selected edge now. Use `edges.highlightSelected:true` in your Diagram options to enable this behaviour.
* Improved the way drag handles for edges are drawn to make it easier for users to locate them.

[**Read more**](/news/2026/06/29/release-1.1.4.md)
