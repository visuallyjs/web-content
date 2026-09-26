ControlsComponentOptions

Options for the controls component.

| Name           | Type                         | Description                                                                                                                                                         |
| -------------- | ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| buttons?       | [ControlsComponentButtons]() | Optional extra buttons to add to the controls component.                                                                                                            |
| clear?         | boolean                      | Whether or not to show the clear button, defaults to true.                                                                                                          |
| clearMessage?  | string                       | Optional message to show the user when prompting them to confirm they want to clear the dataset                                                                     |
| orientation?   | "row" \| "column"            | Optional orientation for the controls. Defaults to 'row'.                                                                                                           |
| undoRedo?      | boolean                      | Whether or not to show undo/redo buttons, defaults to true                                                                                                          |
| zoom?          | boolean                      | Whether or not to show zoom in/zoom out buttons. Defaults to false when the UI's zoom method is "wheel", and defaults to true when the UI's zoom method is "click". |
| zoomToExtents? | boolean                      | Whether or not to show the zoom to extents button, defaults to true                                                                                                 |
