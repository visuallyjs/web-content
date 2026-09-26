# \<ExportControlsComponent/>

Provides a set of buttons allowing your users to export a given canvas as SVG, PNG or JPG.

info

This component only works when your surface is using a `ShapeLibrary` to render elements, or if you are using a `Diagram`.

## Usage[​](#usage "Direct link to Usage")

This component is context aware and will discover the Surface to attach itself to if it is either a child element of a [SurfaceComponent](/svelte/docs/reference/SurfaceComponent.md). Alternatively you can wrap your surface and controls inside a [SurfaceProvider](/svelte/docs/reference/SurfaceProvider.md). In the code below we've shown the controls as a child of the surface.

info

The SVG/image exporter will only work if you're using a shape library in your app to render your nodes as SVG.

```html

<script>
	import {SurfaceComponent, ExportControlsComponent} from "@visuallyjs/browser-ui-svelte"
	import {FLOWCHART_SHAPES} from "@visuallyjs/browser-ui";

	const renderOptions = {
		shapes: {
			sets: [FLOWCHART_SHAPES]
		}
	}
	const viewOptions = {...}
</script>

<SurfaceComponent renderOptions={renderOptions} viewOptions={viewOptions}>
	<ExportControlsComponent/>
</SurfaceComponent>

```

## Props[​](#props "Direct link to Props")

ExportControlsComponentProps

| Name            | Type                     | Description                                                               |
| --------------- | ------------------------ | ------------------------------------------------------------------------- |
| allowJpgExport? | boolean                  | Defaults to true.                                                         |
| allowPngExport? | boolean                  | Defaults to true.                                                         |
| allowSvgExport? | boolean                  | Defaults to true.                                                         |
| className?      | string                   | Optional class name to set on the element.                                |
| imageOptions?   | [ImageExportUIOptions]() | Options for image exports.                                                |
| label?          | string                   | What to show in the label, if visible. Defaults to "Export:".             |
| showLabel?      | boolean                  | Whether or not to show a label in front of the buttons. Defaults to true. |
| svgOptions?     | [SvgExportUIOptions]()   | Options for SVG exports.                                                  |
