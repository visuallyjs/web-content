EdgeData

The default type that represents an edge in a dataset to load or a saved dataset. Edges differ slightly from nodes and groups in that there are fields which are mandatory: `source` and `data`. Edges also differ from nodes and groups in that any backing data for an edge (including its `id` and/or `type`) need to be provided in the `data` member of the edge, not in the root as with nodes and groups.

| Name      | Type                                                                            | Description                                                                                                                                   |
| --------- | ------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| anchors?  | {<br />  source:[ObjectAnchorSpec](),<br />  target:[ObjectAnchorSpec]()<br />} | Optional anchors for the edge.                                                                                                                |
| cost?     | number                                                                          | Cost to associate with the edge. Defaults to 1. This value can be used when computing shortest paths.                                         |
| data?     | [ObjectData]()                                                                  | Optional data to associate with the edge                                                                                                      |
| directed? | boolean                                                                         | Whether or not the given edge is directed, ie. when computing a path the edge can only be traversed from source to target. Defaults to false. |
| geometry? | [Geometry]()                                                                    | Optional geometry that defines the edge's path                                                                                                |
| source    | string \| [PointXY]()                                                           | Either the ID of the source vertex or a canvas location.                                                                                      |
| target    | string \| [PointXY]()                                                           | Either the ID of the target vertex or a canvas location.                                                                                      |
