LocationFunction

Used by layouts. This type defines a function that, given some vertex, can provide the x/y location of the vertex on the canvas. During a group layout, the second argument will contain the group that is being laid out, but when running the layout for the main canvas, `parentGroup` will not be provided.

`(n:Vertex, parentGroup:Group) => PointXY`
