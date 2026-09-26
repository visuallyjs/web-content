ImageExportOptions

Options for an ImageExporter

| Name      | Type                          | Description                                                                                                                                                                                                                                |
| --------- | ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| height?   | number                        | Optional height for the export. The exported image's aspect ratio will always be honoured so if you provide both this and `width`, this will be ignored. If you don't provide this the natural height of the underlying SVG will be used.  |
| margins?  | [PointXY]()                   | Optional margin to set around the content. Defaults to 50px in x and y                                                                                                                                                                     |
| quality?  | number                        | Optional quality of the resulting image - only used for jpeg. Defaults to 1.0.                                                                                                                                                             |
| showGrid? | boolean                       | Whether or not to show the grid in the export (the UI itself has to be showing a grid for the export to have one). Defaults to true.                                                                                                       |
| style?    | string \| Record\<string,any> | Optional style to set in a `style` element in the SVG header. You can provide the CSS for the style element as a string, or you can provide a JS object.                                                                                   |
| type?     | string                        | Content type for the export. Defaults to `image/png`. Most modern browsers also support `image/jpeg`.                                                                                                                                      |
| width?    | number                        | Optional width for the export. The exported image's aspect ratio will always be honoured so if you provide both this and `height`, height will be ignored. If you don't provide this the natural width of the underlying SVG will be used. |
