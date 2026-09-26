IntersectingVerticesOptions

Options for a find intersecting vertices call

| Name                          | Type                                 | Description                                                                    |
| ----------------------------- | ------------------------------------ | ------------------------------------------------------------------------------ |
| dimensions                    | [Size]()                             | Size of the search rectangle, in canvas coordinates                            |
| dontIncludeGroups?            | boolean                              | If true, ignore groups in the canvas root                                      |
| dontIncludeNestedGroups?      | boolean                              | If true, ignore groups that are children of groups                             |
| dontIncludeNodes?             | boolean                              | If true, ignore nodes in the canvas root                                       |
| dontIncludeNodesInsideGroups? | boolean                              | If true, ignore nodes that are children of groups                              |
| enclosed?                     | boolean                              | If true, only vertices fully enclosed by the search rectangle will be returned |
| filter?                       | (n:[Node]() \| [Group]()) => boolean | Optional final filter to apply to the discovered list                          |
| origin                        | [PointXY]()                          | Origin of the search rectangle, in canvas coordinates                          |
