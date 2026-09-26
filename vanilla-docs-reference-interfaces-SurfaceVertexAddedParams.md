SurfaceVertexAddedParams

Payload for a `node:added` or `group:added` event from the Surface.

| Name   | Type                  | Description                                |
| ------ | --------------------- | ------------------------------------------ |
| el     | [BrowserElement]()    | DOM element representing the vertex        |
| id     | string                | ID of the vertex that was added            |
| pos?   | [PointXY]()           | Optional position the vertex was added at. |
| size?  | [Size]()              | can be set if not currently bulk loading.  |
| vertex | [Node]() \| [Group]() | Vertex that was added                      |
