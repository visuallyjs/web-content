ResizingToolsModelUpdater

Defines a function that is invoked each time the resizing tools writes a size update to the model. The vertex that was resized, plus its new position and size, are passed to this function, and the function return a record of other updates it wishes to make to the model, keyed by object id. These updates are written and included as part of the transaction, and will be undone if the resize operation is subsequently undone.

`(v:Node, pos:PointXY, size:Size) => Record<string,ObjectData>`
