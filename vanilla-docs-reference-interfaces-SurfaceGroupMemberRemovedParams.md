SurfaceGroupMemberRemovedParams

Payload for a `group:member:removed` event from the Surface.

| Name              | Type                  | Description                                                                    |
| ----------------- | --------------------- | ------------------------------------------------------------------------------ |
| el                | Element               | DOM element representing the member that was added to the group                |
| group             | [Group]()             | Group the vertex was removed from                                              |
| groupEl           | Element               | DOM element representing the group                                             |
| newPosition?      | [PointXY]()           | Optional new position for the vertex.                                          |
| originalPosition? | [PointXY]()           | Optional original position for the vertex.                                     |
| pos               | [PointXY]()           | Position the member that was removed was located at.                           |
| targetGroup?      | [Group]()             | If the vertex is being moved to some other group, that group is provided here. |
| vertex            | [Node]() \| [Group]() | Vertex that was removed from the group                                         |
