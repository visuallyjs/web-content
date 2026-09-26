EdgeSourceChangedParams

Payload for the event fired when an edge source is changed.

| Name    | Type                      | Description                                                                                                            |
| ------- | ------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| edge    | [Edge]()                  | Edge that was updated                                                                                                  |
| new?    | [PointXY]() \| [Vertex]() | Current source/target                                                                                                  |
| old?    | [PointXY]() \| [Vertex]() | Previous source/target/position                                                                                        |
| source? | VisuallyJsRenderer\<any>  | The UI in which this operation occurred. Not set if the operation was as a result of a programmatic call to the model. |
| success | boolean                   | Whether or not the operation was successful                                                                            |
