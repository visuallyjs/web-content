AbstractEdgeTerminus

This is the base interface for objects in a Graph that can act as the terminus for an Edge.

| Name           | Type   | Description                                                                                                                                                                                                                        |
| -------------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| data           | any    | Object's backing data                                                                                                                                                                                                              |
| id             | string | Object's ID, unique to some scope. All edges must have a unique ID, but an edge may have the same ID as some vertex. No two nodes and groups may have the same ID. Ports must have a unique ID on the vertex on which they reside. |
| objectType     | string | The kind of the object.                                                                                                                                                                                                            |
| getAllEdges    |        | no description                                                                                                                                                                                                                     |
| getFullId      |        | no description                                                                                                                                                                                                                     |
| getSourceEdges |        | no description                                                                                                                                                                                                                     |
| getTargetEdges |        | no description                                                                                                                                                                                                                     |
