SvgExportComponentOptions

Options for the SvgExportComponent

| Name            | Type                     | Description                                                                                                                     |
| --------------- | ------------------------ | ------------------------------------------------------------------------------------------------------------------------------- |
| allowJpgExport? | boolean                  | Defaults to true.                                                                                                               |
| allowPngExport? | boolean                  | Defaults to true.                                                                                                               |
| allowSvgExport? | boolean                  | Defaults to true.                                                                                                               |
| imageOptions?   | [ImageExportUIOptions]() | Options for image exports.                                                                                                      |
| label?          | string                   | What to show in the label, if visible. Defaults to "Export:".                                                                   |
| margins?        | [PointXY]()              | Optional margins to apply to both SVG and image exports. Will not override any margins specified in svgOptions or imageOptions. |
| showLabel?      | boolean                  | Whether or not to show a label in front of the buttons. Defaults to true.                                                       |
| svgOptions?     | [SvgExportUIOptions]()   | Options for SVG exports.                                                                                                        |
