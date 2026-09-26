# \<SurfaceProvider/>

This is a context provider that enables you to use various other components alongside a [SurfaceComponent](/vue/docs/reference/SurfaceComponent.md) without having to explicitly connect them up.

## Usage[​](#usage "Direct link to Usage")

```html
<script setup>
  const data = { ... }
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

* [MiniviewComponent](/vue/docs/reference/MiniviewComponent.md)
* [ControlsComponent](/vue/docs/reference/ControlsComponent.md)
* [ExportControlsComponent](/vue/docs/reference/ExportControlsComponent.md)
* [PaletteComponent](/vue/docs/reference/PaletteComponent.md)
* [ShapePalette](/vue/docs/reference/ShapePaletteComponent.md)
* [InspectorComponent](/vue/docs/reference/InspectorComponent.md)
* [ShapeComponent](/vue/docs/reference/ShapeComponent.md)
