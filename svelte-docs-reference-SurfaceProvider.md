# \<SurfaceProvider/>

This is a context provider that enables you to use various other components alongside a [SurfaceComponent](/svelte/docs/reference/SurfaceComponent.md) without having to explicitly connect them up.

## Usage[​](#usage "Direct link to Usage")

```html
<script>
const data = { ... }
const viewOptions = {
    ...
}
</script>

<template>
  <SurfaceProvider>
    <SurfaceComponent data={...}/>
    <ControlsComponent/>
    <MiniviewComponent/>
  </SurfaceProvider>
</template>

```

The list of components that are surface context aware is:

* [MiniviewComponent](/svelte/docs/reference/MiniviewComponent.md)
* [ControlsComponent](/svelte/docs/reference/ControlsComponent.md)
* [ExportControlsComponent](/svelte/docs/reference/ExportControlsComponent.md)
* [PaletteComponent](/svelte/docs/reference/PaletteComponent.md)
* [ShapePalette](/svelte/docs/reference/ShapePaletteComponent.md)
* [InspectorComponent](/svelte/docs/reference/InspectorComponent.md)
* [ShapeComponent](/svelte/docs/reference/ShapeComponent.md)
