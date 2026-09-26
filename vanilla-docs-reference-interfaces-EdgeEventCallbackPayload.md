EdgeEventCallbackPayload

The payload passed to an EdgeEventCallback

| Name       | Type                 | Description                          |
| ---------- | -------------------- | ------------------------------------ |
| connection | [Connection\<any>]() | The connection rendered by the UI    |
| e          | MouseEvent           | The event that invoked this callback |
| model      | [VisuallyJsModel]()  | The underlying model                 |
| obj        | [Edge]()             | The edge that the event occurred on  |
| ui         | UICore\<any>         | The UI that drew this edge           |
