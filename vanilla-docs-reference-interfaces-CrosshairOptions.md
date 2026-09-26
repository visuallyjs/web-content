CrosshairOptions

Options for the crosshair display on an axis.

| Name              | Type                       | Description                                                                                                                                                                     |
| ----------------- | -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| color?            | string                     | Color of the crosshair line.                                                                                                                                                    |
| cssClass?         | string                     | Optional CSS class to write to the crosshair element.                                                                                                                           |
| labelColor?       | string                     | Color for the label text. Defaults to the same color as the line.                                                                                                               |
| labelFont?        | [FontSpec]()               | Font for the label.                                                                                                                                                             |
| labelFormat?      | string                     | Formatter for the label.                                                                                                                                                        |
| labelPosition?    | "end" \| "start"           | Position of the label on the crosshair. For a horizontal line, 'start' means 'left' and 'end' means 'right'. For a vertical line, 'start' means 'bottom' and 'end' means 'top'. |
| labelValueFormat? | number \| "float" \| "int" | Standard number format for the value (e.g. 'int', 'float', or a number for decimal places).                                                                                     |
| showLabel?        | boolean                    | Whether or not to show the current value on the crosshair. Defaults to true.                                                                                                    |
| width?            | number                     | Width of the crosshair line. Defaults to 1.                                                                                                                                     |
