VertexDrawingPluginTypeGenerator

Defines a function used by the vertex drawing plugin to generate an `objectType` (Group/Node) and `type` (app-specific) for a vertex that is about to be drawn.

`(origin:PointXY, e:MouseEvent) => {
  data:ObjectData,
  objectType:Node.objectType | Group.objectType,
  type:string
}`
