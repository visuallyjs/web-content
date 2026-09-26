# \<ExportControlsComponent/>

Provides a set of buttons allowing your users to export a given canvas as SVG, PNG or JPG.

info

This component only works when your surface is using a `ShapeLibrary` to render elements, or if you are using a `Diagram`.

## Usage[​](#usage "Direct link to Usage")

This component is context aware and will discover the Surface to attach itself to if it is a child of a `SurfaceComponent`:

```jsx
import { FLOWCHART_SHAPES } from "@visuallyjs/browser-ui"
import { SurfaceComponent, ExportControlsComponent} from "@visuallyjs/browser-ui-react"

export default function() {
    const renderOptions = {
        shapes:{
            sets:[FLOWCHART_SHAPES]
        }
    }
    return <SurfaceComponent renderOptions={renderOptions} data={...}>
        <ExportControlsComponent />
    </SurfaceComponent>    
}

```

or if it is a descendant of a `SurfaceProvider`:

```jsx
import { FLOWCHART_SHAPES } from "@visuallyjs/browser-ui"
import { SurfaceComponent, ExportControlsComponent, SurfaceProvider} from "@visuallyjs/browser-ui-react"

export default function() {
    const renderOptions = {
        shapes:{
            sets:[FLOWCHART_SHAPES]
        }
    }
    return <SurfaceProvider> 
        <SurfaceComponent renderOptions={renderOptions} data={...}/>
        <ExportControlsComponent />
    </SurfaceProvider>
}

```

## Props[​](#props "Direct link to Props")

ExportControlsComponentProps

Options for the ExportControlsComponent

| Name            | Type                     | Description                                                                                                                                                                                                                                           |
| --------------- | ------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| allowJpgExport? | boolean                  | Defaults to true.                                                                                                                                                                                                                                     |
| allowPngExport? | boolean                  | Defaults to true.                                                                                                                                                                                                                                     |
| allowSvgExport? | boolean                  | Defaults to true.                                                                                                                                                                                                                                     |
| imageOptions?   | [ImageExportUIOptions]() | Options for image exports.                                                                                                                                                                                                                            |
| label?          | string                   | What to show in the label, if visible. Defaults to "Export:".                                                                                                                                                                                         |
| margins?        | [PointXY]()              | Optional margins to apply to both SVG and image exports. Will not override any margins specified in svgOptions or imageOptions.                                                                                                                       |
| showLabel?      | boolean                  | Whether or not to show a label in front of the buttons. Defaults to true.                                                                                                                                                                             |
| surfaceId?      | string                   | The ID of surface to attach to. Optional, and likely to be deprecated in a future release. The component is context aware and will try to resolve the Surface/Paper to attach to from an ancestor SurfaceProvider SurfaceComponent or PaperComponent. |
| svgOptions?     | [SvgExportUIOptions]()   | Options for SVG exports.                                                                                                                                                                                                                              |
