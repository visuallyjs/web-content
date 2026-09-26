SvgExportUIOptions

Options for the SvgExportUI

| Name                 | Type                          | Description                                                                                                                                              |
| -------------------- | ----------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| downloadButtonLabel? | string                        | Optional label to use on the download button. Defaults to "Download".                                                                                    |
| filename?            | string                        | Optional filename to use - defaults to `visuallyjs-export`. You do not need to provide the extension.                                                    |
| height?              | number                        | Optional height to set on the SVG output. Defaults to unset, meaning the SVG will adapt to whatever its container's height is.                           |
| margins?             | [PointXY]()                   | Optional margin to set around the content. Defaults to 50px in x and y                                                                                   |
| showGrid?            | boolean                       | Whether or not to show the grid in the export (the UI itself has to be showing a grid for the export to have one). Defaults to true.                     |
| style?               | string \| Record\<string,any> | Optional style to set in a `style` element in the SVG header. You can provide the CSS for the style element as a string, or you can provide a JS object. |
| width?               | number                        | Optional width to set on the SVG output. Defaults to unset, meaning the SVG will adapt to whatever its container's width is.                             |
