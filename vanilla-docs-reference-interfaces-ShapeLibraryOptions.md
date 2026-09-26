ShapeLibraryOptions

Options for a shape library.

| Name                 | Type                                  | Description                                                                                                                                                                                            |
| -------------------- | ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| categoryParameter?   | string                                | The property to use to map an object's category (ie which shape set to use). Defaults to "category".                                                                                                   |
| defaultFillColor?    | string                                | Optional default for fill color. If not provided, fill is set to #FFFFFF.                                                                                                                              |
| defaultOutlineColor? | string                                | Optional default for outline color. If not provided, outline is set to #000000.                                                                                                                        |
| labelBackground?     | boolean \| [LabelBackgroundOptions]() | Options for label background. Use `true` for defaults, or supply your own values (which will be merged on top of the defaults)                                                                         |
| labelFillRatio?      | number                                | How much of the width of a shape a multiline label will take up before wrapping. Defaults to 0.8. You can set this to a number greater than 1, if you like, but that will allow the label to overflow. |
| labelPosition?       | LabelPosition                         | Default position for labels (will be overridden by a shape that defines its own position. Defaults to "center"                                                                                         |
| multilineLabels?     | boolean                               | Defaults to true - labels are split across multiple lines to fit inside their shape. Set this to false if you want labels to always be a single line.                                                  |
| typeParameter?       | string                                | The property to use to map an object's type. Defaults to "type".                                                                                                                                       |
