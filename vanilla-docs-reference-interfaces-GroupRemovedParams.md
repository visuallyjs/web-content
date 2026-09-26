GroupRemovedParams

Payload for a group added event in the model

| Name                      | Type                         | Description                                                                                                                   |
| ------------------------- | ---------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| children                  | Array<[Node]() \| [Group]()> | If children were removed, this is the list of them                                                                            |
| edges                     | Array<[Edge]()>              | List of edges that are being removed as a result of this vertex's removal.                                                    |
| group                     | [Group]()                    | Group that was removed                                                                                                        |
| parentGroup?              | [Group]()                    | If the vertex was a member of some other group, that group is provided here                                                   |
| parentGroupIsBeingRemoved | boolean                      | Indicates that the vertex is being removed because some parent group is being removed and is forcing removal of its children. |
| removeChildren?           | boolean                      | If true, indicates the group's children were also removed                                                                     |
