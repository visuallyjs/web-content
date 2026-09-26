ResizeFunction

Function invoked each time a resize event occurs that a ResizingToolsHandlerFactory is controlling. This function is expected to return an object containing a new x, y, width and height for the vertex being resized, as well as, optionally, an object containing required updates to other model objects, keyed by the other model object's IDs.

`(dx:number, dy:number) => {
  height:number,
  updates:Record<string,ObjectData>,
  width:number,
  x:number,
  y:number
}`
