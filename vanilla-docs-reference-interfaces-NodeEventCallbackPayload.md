NodeEventCallbackPayload

The payload passed to a NodeEventCallback

| Name  | Type                | Description                                                   |
| ----- | ------------------- | ------------------------------------------------------------- |
| e     | MouseEvent          | The pointer event that caused the event handler to be invoked |
| el    | EL                  | Element that represents the vertex in the UI                  |
| model | [VisuallyJsModel]() | The underlying VisuallyJs model                               |
| obj   | [Node]()            | The model object for the vertex                               |
| ui    | UICore\<EL>         | The UI that rendered this vertex                              |
