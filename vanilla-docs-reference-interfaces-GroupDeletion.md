GroupDeletion

The result of a group deletion.

| Name         | Type                         | Description                                                                                                                                                                                                                                       |
| ------------ | ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| children     | Array<[Node]() \| [Group]()> | List all nodes and groups that were deleted. Always present; may be empty.                                                                                                                                                                        |
| edges        | Array<[Edge]()>              | List of edges that were deleted. Always present but may be empty.                                                                                                                                                                                 |
| group        | [Group]()                    | The group that was deleted                                                                                                                                                                                                                        |
| nestedGroups | Array<[GroupDeletion]()>     | List of group's child groups that were also deleted as a result of this group's deletion. This array is always present but may be empty: the group may have been empty, or the user may have instructed the model not to delete its child groups. |
| nodes        | Array<[NodeDeletion]()>      | List of group's child nodes that were also deleted as a result of this group's deletion. This array is always present but may be empty: the group may have been empty, or the user may have instructed the model not to delete its child nodes.   |
| parentGroup? | [Group]()                    | Optional, provided if the deleted object was the child of a group.                                                                                                                                                                                |
