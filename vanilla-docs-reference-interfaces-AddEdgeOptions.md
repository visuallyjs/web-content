AddEdgeOptions

Options for the `addEdge` method in the VisuallyJsModel class.

| Name      | Type                                                                            | Description                                                                                 |
| --------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| anchors?  | {<br />  source:[SingleAnchorSpec](),<br />  target:[SingleAnchorSpec]()<br />} | Optional anchors for the edge.                                                              |
| cost?     | number                                                                          | Optional edge cost. Defaults to 1.                                                          |
| data?     | undefined                                                                       | Optional backing data for the edge.                                                         |
| directed? | boolean                                                                         | By default edges are not directed. This is used only when computing paths between vertices. |
| geometry? | any                                                                             | Optional edge geometry.                                                                     |
| source    | string \| [PointXY]() \| [Vertex]()                                             | Source for the edge - a vertex, vertex id, or canvas location.                              |
| target    | string \| [PointXY]() \| [Vertex]()                                             | Target for the edge - a vertex, vertex id, or canvas location.                              |
