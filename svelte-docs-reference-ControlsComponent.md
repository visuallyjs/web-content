# \<ControlsComponent/>

This component provides a set of controls for a surface - such operations as zoom to extents, undo/redo, clear, etc. The operations that are available can be specified on the controls element, and you can also add your own buttons.

## Usage[​](#usage "Direct link to Usage")

This component is context aware and will discover the Surface to attach itself to if it is either a child element of a [SurfaceComponent](/svelte/docs/reference/SurfaceComponent.md). Alternatively you can wrap your surface and controls inside a [SurfaceProvider](/svelte/docs/reference/SurfaceProvider.md). In the code below we've shown the controls as a child of the surface.

```html
<script>
	import {SurfaceComponent, ControlsComponent} from "@visuallyjs/browser-ui-svelte"
    const renderOptions = {... }
    const viewOptions = { ... }
</script>

<SurfaceComponent renderOptions={renderOptions} viewOptions={viewOptions}>
	<ControlsComponent/>
</SurfaceComponent>

```

## Props[​](#props "Direct link to Props")

ControlsComponentProps

| Name           | Type                         | Description                                                                                     |
| -------------- | ---------------------------- | ----------------------------------------------------------------------------------------------- |
| buttons?       | [ControlsComponentButtons]() | Optional extra buttons to add to the controls component.                                        |
| className?     | string                       | Optional class name to set on the control component's container                                 |
| clear?         | boolean                      | Whether or not to show the clear button, defaults to true.                                      |
| clearMessage?  | string                       | Optional message to show the user when prompting them to confirm they want to clear the dataset |
| orientation?   | "row" \| "column"            | Optional orientation for the controls. Defaults to 'row'.                                       |
| undoRedo?      | boolean                      | Whether or not to show undo/redo buttons, defaults to true                                      |
| zoomButtons?   | boolean                      | Whether or not to show the zoom in/zoom out buttons, defaults to false                          |
| zoomToExtents? | boolean                      | Whether or not to show the zoom to extents button, defaults to true                             |
