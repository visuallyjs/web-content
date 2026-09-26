VertexMoveEndParams

Payload for the node:move

<!-- -->

:end

<!-- -->

event that is fired when a node/group has just been moved.

| Name      | Type                                                                                                                                                         | Description                                                                                                                                                                                                                                   |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| dragGroup | Array<{<br />  el:E,<br />  element:ViewportElement\<E>,<br />  originalPos:[PointXY](),<br />  pos:[PointXY](),<br />  vertex:[Node]() \| [Group]()<br />}> | The list of vertices that were dragged. This array will always contain at the very least information about a vertex that was dragged. If the vertex was in a drag group then all of the members of that drag group will be in this array too. |
