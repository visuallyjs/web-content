TooltipOptions

Options for a tooltip

| Name          | Type         | Description                                                                                                                                    |
| ------------- | ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| cornerRadius? | number       | Corner radius for the tooltip. Defaults to 3px.                                                                                                |
| fill?         | string       | Fill color. Defaults to white.                                                                                                                 |
| font?         | [FontSpec]() | Optional font for the tooltip.                                                                                                                 |
| format        | string       | The text to display. You can use template syntax to access a few context specific variables - see the docs for a discussion.                   |
| outline?      | string       | Outline color. Defaults to "#999999"                                                                                                           |
| outlineWidth? | number       | Outline width. Defaults to 1.                                                                                                                  |
| textColor?    | string       | Color for text. Defaults to system default.                                                                                                    |
| timeout?      | number       | Time to display the tooltip, in milliseconds, before hiding it. Defaults to 2500. Set this to -1 to have the Tooltip never hide automatically. |
| valueSuffix?  | string       | Optional string to append to values                                                                                                            |
