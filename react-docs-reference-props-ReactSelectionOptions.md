ReactSelectionOptions

Options for declaring a selection that this component will manage.

| Name            | Type                   | Description                                                                                                    |
| --------------- | ---------------------- | -------------------------------------------------------------------------------------------------------------- |
| autoFill?       | boolean                | Optional. If true, the selection will automatically reload when nodes/groups are added to the main model.      |
| generator       | [SelectionGenerator]() | Required. A function that will populate the selection.                                                         |
| onBeforeReload? | Function               | Optional. Called before the selection is cleared at the beginning of a reload, when a `generator` is supplied. |
| onReload?       | Function               | Optional. Called after a reload when a `generator` was supplied.                                               |
