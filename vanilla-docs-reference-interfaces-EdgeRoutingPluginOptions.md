EdgeRoutingPluginOptions

Options for the edge routing plugin.

| Name               | Type                      | Description                                                                                                                                                                                                                             |
| ------------------ | ------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| mode               | [EdgeRoutingPluginMode]() | Mode to use to draw edges. 'orthogonal' is like the orthogonal connector - segments that are either vertical or horizontal.<br />`direct` draws straight lines through regions. Both modes assign a separate anchor point to each edge. |
| orthogonalMode?    | [OrthogonalRouterMode]()  | When mode is 'orthogonal' this instructs VisuallyJs whether to group edges in buses, or to route each edge separately.                                                                                                                  |
| orthogonalPadding? | number                    | How much space to leave between stacked orthogonal edges. Defaults to 10 pixels.                                                                                                                                                        |
