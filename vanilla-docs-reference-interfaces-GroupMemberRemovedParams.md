GroupMemberRemovedParams

Payload for a group member removed event in the model

| Name              | Type                  | Description                                                                    |
| ----------------- | --------------------- | ------------------------------------------------------------------------------ |
| group             | [Group]()             | Group the vertex was removed from                                              |
| newPosition?      | [PointXY]()           | Optional new position for the vertex.                                          |
| originalPosition? | [PointXY]()           | Optional original position for the vertex.                                     |
| targetGroup?      | [Group]()             | If the vertex is being moved to some other group, that group is provided here. |
| vertex            | [Node]() \| [Group]() | Vertex that was removed from the group                                         |
