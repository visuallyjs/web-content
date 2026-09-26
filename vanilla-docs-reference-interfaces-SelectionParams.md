SelectionParams

Defines the payload for a selection event.

| Name      | Type                    | Description                                                                                           |
| --------- | ----------------------- | ----------------------------------------------------------------------------------------------------- |
| obj       | [Base]()                | The subject of the selection event                                                                    |
| reason?   | string                  | Optional reason for the selection event, which can be passed to the model when selecting some object. |
| selection | [VisuallyJsSelection]() | Selection this event pertains to                                                                      |
