ControlsComponentProps

| Name           | Type                         | Description                                                                                     |
| -------------- | ---------------------------- | ----------------------------------------------------------------------------------------------- |
| buttons?       | [ControlsComponentButtons]() | Optional extra buttons to add to the controls component.                                        |
| className?     | string                       | Optional class name to set on the control component's container                                 |
| clear?         | boolean                      | Whether or not to show the clear button, defaults to true.                                      |
| clearMessage?  | string                       | Optional message to show the user when prompting them to confirm they want to clear the dataset |
| orientation?   | "row" \| "column"            | Optional orientation for the controls. Defaults to 'row'.                                       |
| undoRedo?      | boolean                      | Whether or not to show undo/redo buttons, defaults to true                                      |
| zoomButtons?   | boolean                      | Whether or not to show the zoom in/zoom out buttons, defaults to false                          |
| zoomToExtents? | boolean                      | Whether or not to show the zoom to extents button, defaults to true                             |
