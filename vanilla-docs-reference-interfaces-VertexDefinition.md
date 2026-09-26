VertexDefinition

Base class for node, group and port definitions. This interface is shared by the model and the view.

| Name                 | Type    | Description                                                                                   |
| -------------------- | ------- | --------------------------------------------------------------------------------------------- |
| allowLoopback?       | boolean | Whether or not to allow edges from this vertex back to itself. Defaults to false.             |
| allowVertexLoopback? | boolean | Whether or not to allow edges from a port back to the vertex it belongs to. Defaults to true. |
| maxConnections?      | number  | Optional connection limit. Defaults to 1. A value of -1 means there is no limit.              |
