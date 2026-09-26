InspectorComponentProps

| Name                | Type                      | Description                                                                                                                                                                            |
| ------------------- | ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| autoCommit?         | boolean                   | Whether or not to auto commit changes on blur or enter keypress. Defaults to true.                                                                                                     |
| className?          | string                    | Optional class name to set on the component's root element.                                                                                                                            |
| current?            | [Base]() \| null          | A $state ref that the inspector will apply 2-way binding to. Since 1.2.0 this is the preferred way to use an inspector, as it reduces the amount of boilerplate you need to configure. |
| filter?             | (obj:[Base]()) => boolean | Optional filter function that you can supply if you want to ignore certain objects in your dataset.                                                                                    |
| multipleSelections? | boolean                   | Whether or not to allow multiple objects to be selected and edited at once.<br />Defaults to false.                                                                                    |
| refresh?            | (obj:[Base]()) => void    | Callback invoked when a new object has started to be edited.                                                                                                                           |
| style?              | string                    | Optional style to set on the component's root element.                                                                                                                                 |
