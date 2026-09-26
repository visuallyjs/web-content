VertexRemovedParams

Base payload for a vertex removed event in the model

| Name                      | Type            | Description                                                                                                                   |
| ------------------------- | --------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| edges                     | Array<[Edge]()> | List of edges that are being removed as a result of this vertex's removal.                                                    |
| parentGroup?              | [Group]()       | If the vertex was a member of some other group, that group is provided here                                                   |
| parentGroupIsBeingRemoved | boolean         | Indicates that the vertex is being removed because some parent group is being removed and is forcing removal of its children. |
