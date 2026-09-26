ElementDraggerOptions

Options for an ElementDragger

| Name                | Type                                                 | Description                                                                                                                              |
| ------------------- | ---------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| constrain?          | [ConstrainFunction<]()[BrowserElement](),MouseEvent> | Function to constrain movement of the elements.                                                                                          |
| containment?        | [ContainmentType]()                                  | Shortcut for some basic constrain scenarios - constrain to parent, constrain entirely to parent, dont allow movement into negative axes. |
| containmentPadding? | number                                               | If `containment` is set, you can provide a value for padding here. Currently the default is 5 pixels.                                    |
| filter?             | string                                               | CSS3 filter identifying parts of the elements that should not allow drag                                                                 |
