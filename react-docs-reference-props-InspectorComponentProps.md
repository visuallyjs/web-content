InspectorComponentProps

Props for the InspectorComponent

| Name                | Type                      | Description                                                                                                                                                                                           |
| ------------------- | ------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| afterUpdate?        | (s:[BrowserUI]()) => void | Optional function to invoke after an update.                                                                                                                                                          |
| autoCommit?         | boolean                   | Whether or not to auto commit on enter keypress/blur. Defaults to true.                                                                                                                               |
| className?          | string                    | Optional extra css classes to set on the root element                                                                                                                                                 |
| filter?             | (b:[Base]()) => boolean   | Optional filter you can use to instruct the inspector to ignore certain items.                                                                                                                        |
| multipleSelections? | boolean                   | Whether or not to support multiple selections. Defaults to true.                                                                                                                                      |
| refresh?            | (obj:[Base]()) => void    | Callback invoked when a new object has started to be edited. You need to provide this if the child content you provide to the Inspector is not a function.                                            |
| renderEmptyContent? | () => any                 | Optional function that returns JSX to use when nothing is selected                                                                                                                                    |
| showCloseButton?    | boolean                   | Whether or not to show a close button. Defaults to false.                                                                                                                                             |
| surface?            | [Surface]()               | Surface to attach to. It is not mandatory that you supply this - the component is context aware and can try to resolve a surface from an ancestor SurfaceProvider SurfaceComponent or PaperComponent. |
