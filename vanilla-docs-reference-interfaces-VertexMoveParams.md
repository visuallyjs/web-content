VertexMoveParams

Payload for the node

<!-- -->

:move

<!-- -->

event that is fired when a node/group has just begun to be moved.

| Name      | Type                                                                                                                                            | Description                                                                                                                                                                                                                                                                                            |
| --------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| dragGroup | Array<{<br />  element:ViewportElement\<E>,<br />  originalPos:[PointXY](),<br />  pos:[PointXY](),<br />  vertex:[Node]() \| [Group]()<br />}> | The list of vertices that were dragged. This array will always contain at the very least information about a vertex that was dragged. If the vertex was in a drag group then all of the members of that drag group will be in this array too.                                                          |
| positions | Record\<string,[PointXY]()>                                                                                                                     | This object contains a record of the final position of every vertex that was moved as a result of this vertex drag - the vertex itself, any members of a drag group for which the vertex was an active member, plus any elements that may have been moved via the magnetizer during or after the drag. |
