ControlsComponentProps

Props for the ControlsComponent

| Name           | Type              | Description                                                                                       |
| -------------- | ----------------- | ------------------------------------------------------------------------------------------------- |
| className?     | string            | Optional class name(s) to attach to the component's container element.                            |
| clear?         | boolean           | Defaults to true. Whether or not to show the 'clear dataset' button.                              |
| clearMessage?  | string            | Optional message to use when the user presses the clear button. Defaults to 'Clear dataset?'.     |
| onMaybeClear?  | Function          | A function to use instead of the browser's default prompt when the user presses the clear button. |
| orientation    | "row" \| "column" | Defaults to 'row' - whether to show buttons in a row or a column                                  |
| surfaceId?     | string            | ID of the surface to attach to. Optional, a default will be used if not provided.                 |
| undoRedo?      | boolean           | Defaults to true, meaning show the undo/redo buttons.                                             |
| zoomButtons?   | boolean           | Defaults to false, meaning the zoom in/zoom out buttons are not shown by default.                 |
| zoomToExtents? | boolean           | Defaults to true, meaning the 'zoom to extents' button will be shown.                             |
