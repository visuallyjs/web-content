NodeDeletion

The result of a node deletion.

| Name         | Type            | Description                                                        |
| ------------ | --------------- | ------------------------------------------------------------------ |
| edges        | Array<[Edge]()> | List of edges that were deleted. Always present but may be empty.  |
| node         | [Node]()        | The node that was deleted.                                         |
| parentGroup? | [Group]()       | Optional, provided if the deleted object was the child of a group. |
