VertexDragFilter\<E>

Type Parameters

|   |   |   |
| - | - | - |
| E |   |   |

Defines a function that will be invoked prior to a vertex being dragged. Returning false from this function will abort the vertex drag.

`(p:{
  e:MouseEvent,
  el:E,
  vertex:Node | Group
}) => boolean`
