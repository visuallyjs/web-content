ClonedSet

The return value from a paste. Contains a list of nodes, groups and edges that were pasted, as well as a map of previous edge/vertex ids to their new ids, the computed origin of the copied vertices, and the amount by which the set of objects was translated for the paste (so the paste location is origin + transform).

| Name      | Type                      | Description                                                        |
| --------- | ------------------------- | ------------------------------------------------------------------ |
| edgeMap   | Map\<string,string>       | Map of edges that were pasted, keyed by id                         |
| edges     | Array<[AddEdgeOptions]()> | List of edges that were pasted.                                    |
| groups    | Array<[ObjectData]()>     | List of groups that were pasted.                                   |
| nodes     | Array<[ObjectData]()>     | List of nodes that were pasted.                                    |
| origin    | [PointXY]()               | The computed origin of the set of pasted objects, prior to pasting |
| transform | [PointXY]()               | The transformation applied to the content origin when pasting.     |
| vertexMap | Map\<string,string>       | Map of nodes/groups that were pasted, keyed by id                  |
