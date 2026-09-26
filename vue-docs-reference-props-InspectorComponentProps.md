InspectorComponentProps

Props for the InspectorComponent

| Name                 | Type                    | Description                                                                                                                                                  |
| -------------------- | ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| afterUpdate?         | (s:[Surface]()) => void | Optional function to invoke after an update.                                                                                                                 |
| autoCommit?          | boolean                 | Whether or not to auto commit on enter keypress/blur. Defaults to true.                                                                                      |
| className?           | string                  | Optional extra css classes to set on the root element                                                                                                        |
| filter?              | (b:[Base]()) => boolean | Optional filter you can use to instruct the inspector to ignore certain items.                                                                               |
| modelValue?          | Object                  | A model value that this component will apply 2-way binding to. You do not actually supply a prop named `modelValue`; you supply this as `v-model="someRef"`. |
| multipleSelections?  | boolean                 | Whether or not to support multiple selections. Defaults to true.                                                                                             |
| refresh              | (obj:[Base]()) => void  | Callback invoked when a new object has started to be edited.                                                                                                 |
| renderEmptyContainer | () => void              | Callback invoked when the inspector is cleared.                                                                                                              |
| showCloseButton?     | boolean                 | Whether or not to show a close button. Defaults to false.                                                                                                    |
| surfaceId?           | string                  | Optional ID of the surface to attach to. It is better to nest this component inside a SurfaceComponent or SurfaceProvider.                                   |
