# ExportControls

Provides a set of buttons allowing your users to export a given canvas as SVG, PNG or JPG.

info

This component only works when your surface is using a `ShapeLibrary` to render elements, or if you are using a `Diagram`.

## Usage[​](#usage "Direct link to Usage")

```typescript
import { FLOWCHART_SHAPES } from "@visuallyjs/browser-ui"
import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular"

@Component({
    template:`<div>
        <vjs-surface [renderOptions]="renderOptions" [data]="data"/>
        <vjs-export-controls />
        </div>`
})
export class MyApp {
    renderOptions = { 
        shapes:{
            sets:[ FLOWCHART_SHAPES ]
        }
    }
    data = { ... }
}


```

## Definition[​](#definition "Direct link to Definition")

### Inputs[​](#inputs "Direct link to Inputs")

| Name            | Type                     | Description                                                                                                                     |
| --------------- | ------------------------ | ------------------------------------------------------------------------------------------------------------------------------- |
| allowJpgExport? | boolean                  | Defaults to true - whether or not to show a JPG export button.                                                                  |
| allowPngExport? | boolean                  | Defaults to true - whether or not to show a PNG export button.                                                                  |
| allowSvgExport? | boolean                  | Defaults to true - whether or not to show an SVG export button.                                                                 |
| imageOptions?   | [ImageExportUIOptions]() | Options for image exports.                                                                                                      |
| label?          | string                   | What to show in the label, if visible. Defaults to "Export:".                                                                   |
| margins?        | [PointXY]()              | Optional margins to apply to both SVG and image exports. Will not override any margins specified in svgOptions or imageOptions. |
| showLabel?      | boolean                  | Whether or not to show a label in front of the buttons. Defaults to true.                                                       |
| svgOptions?     | [SvgExportUIOptions]()   | Options for SVG exports.                                                                                                        |
