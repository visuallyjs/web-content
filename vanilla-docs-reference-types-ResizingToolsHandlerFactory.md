ResizingToolsHandlerFactory

A factory that can return handlers for resize, given a vertex to resize and a resize direction (as well as the default resize function for the given direction). When a resize begins, the factory is called with the ui, current vertex, resize direction, and default handler. It returns a ResizeFunction that is invoked each time a discrete resize event then occurs, until the mouse/pointer is released. Each time the resize function is invoked, it is expected to return an object containing a new x, y, width and height for the vertex being resized, as well as, optionally, an object containing required updates to other model objects. This object is keyed by vertex ID, and its values are individual updates to apply to the vertex with that ID.

`(ui:Surface, vertex:Node | Group, resizeDirection:ResizeDirection, defaultHandler:ResizeFunction) => ResizeFunction`
