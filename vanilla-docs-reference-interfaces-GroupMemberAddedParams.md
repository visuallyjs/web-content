GroupMemberAddedParams

Payload for a group member added event in the model.

| Name              | Type                  | Description                                                                                                   |
| ----------------- | --------------------- | ------------------------------------------------------------------------------------------------------------- |
| group             | [Group]()             | Group the vertex was added to                                                                                 |
| originalPosition? | [PointXY]()           | Optional original location for the vertex that was added                                                      |
| pos?              | [PointXY]()           | Optional new location for the vertex that was added                                                           |
| sourceGroup?      | [Group]()             | If a vertex being added to some group is currently a member of some other group, that group is provided here. |
| vertex            | [Node]() \| [Group]() | Vertex that was added to the group                                                                            |
| vertexIsNew?      | boolean               | Set to true if the vertex is also brand new, not copied from elsewhere in the dataset.                        |
