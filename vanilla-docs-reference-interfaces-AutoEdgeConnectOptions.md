AutoEdgeConnectOptions

Options for auto edge connect.

| Name         | Type                  | Description                                                                                                                                                                                                                                        |
| ------------ | --------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| activeClass? | string                | Class to set on the UI canvas when drag starts and auto edge connect is active                                                                                                                                                                     |
| connectMode? | "eager" \| "onDemand" | The mode to run the auto connect functionality in. "onDemand" is the default, meaning the user has to press the Meta key in order to activate the edge auto connect. In "eager" mode, the edge auto connect is switched on as soon as drag starts. |
| enabled      | boolean               | Whether or not auto edge connect is enabled.                                                                                                                                                                                                       |
| key?         | string                | The key to listen for to switch from primed to active when connect mode is `onDemand`                                                                                                                                                              |
| lineStyle?   | [LineStyle]()         | Style to use for an automatically created edge (while the user is still dragging the new element). Defaults to a gray dashed line.                                                                                                                 |
