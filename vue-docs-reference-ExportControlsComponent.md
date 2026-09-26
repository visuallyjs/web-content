# \<ExportControlsComponent/>

Provides a set of buttons allowing your users to export a given canvas as SVG, PNG or JPG.

info

This component only works when your surface is using a `ShapeLibrary` to render elements, or if you are using a `Diagram`.

## Usage[​](#usage "Direct link to Usage")

This component is context aware and will discover the Surface to attach itself to if there is a single surface in your app. Alternatively you can wrap your surface and export controls inside a [SurfaceProvider](/vue/docs/reference/SurfaceProvider.md), or you can declare the export controls component as a child of a surface.

```html
<script>
import { defineComponent } from "vue"
  
export default defineComponent({
  name:"my-app",
  data:() => {
    return {
      ...
    }
  }
})
    
</script>
<template>
    <SurfaceComponent .../>
    <ExportControlsComponent/>
</template>


```

## Props[​](#props "Direct link to Props")

ExportControlsComponentProps

Props for the ExportControlsComponent

| Name            | Type                     | Description                                                                                                                     |
| --------------- | ------------------------ | ------------------------------------------------------------------------------------------------------------------------------- |
| allowJpgExport? | boolean                  | Defaults to true.                                                                                                               |
| allowPngExport? | boolean                  | Defaults to true.                                                                                                               |
| allowSvgExport? | boolean                  | Defaults to true.                                                                                                               |
| imageOptions?   | [ImageExportUIOptions]() | Options for image exports.                                                                                                      |
| label?          | string                   | What to show in the label, if visible. Defaults to "Export:".                                                                   |
| labelProperty?  | string                   | The name of the property that holds the label for a vertex                                                                      |
| margins?        | [PointXY]()              | Optional margins to apply to both SVG and image exports. Will not override any margins specified in svgOptions or imageOptions. |
| showLabel?      | boolean                  | Whether or not to show a label in front of the buttons. Defaults to true.                                                       |
| surfaceId?      | string                   | Optional ID of the surface to attach to. It is better to nest this component inside a SurfaceComponent or SurfaceProvider.      |
| svgOptions?     | [SvgExportUIOptions]()   | Options for SVG exports.                                                                                                        |
