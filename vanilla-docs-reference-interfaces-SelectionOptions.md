SelectionOptions

Options for the behaviour of a selection.

| Name            | Type                   | Description                                                                                                                                                                                                       |
| --------------- | ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| autoFill?       | boolean                | Defaults to false. If true, and a `generator` is supplied,                                                                                                                                                        |
| generator?      | [SelectionGenerator]() | Optional function that can be called to fill the selection. You'd use this when you are rendering individual selections and you need to be able to refresh the whole view based on some change in the data model. |
| lazy?           | boolean                | If true, the selection will not populate itself as soon as it is constructed. Otherwise, and this is the default behaviour, it will.                                                                              |
| mode?           | [SelectionMode]()      | Defaults to SelectionModes.mixed, meaning any combination of nodes, groups and edges may be present in the selection at a given point in time.                                                                    |
| onBeforeReload? | Function               | Optional. called before the selection is cleared at the beginning of a reload, when a `generator` is supplied.                                                                                                    |
| onClear?        | Function               | Optional function to call when the selection is cleared.                                                                                                                                                          |
| onReload?       | Function               | Optional. called after a reload when a `generator` was supplied.                                                                                                                                                  |
