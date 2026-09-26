# \<PaperProvider/>

This is a context provider that enables you to use various other components alongside a [PaperComponent](/vue/docs/reference/PaperComponent.md) without having to explicitly connect them up.

## Usage[​](#usage "Direct link to Usage")

```html
<script setup>
  const data = { ... }
</script>
<template>
  <PaperProvider>
    <PaperComponent data={...}/>
    <ControlsComponent/>
    <MiniviewComponent/>
  </PaperProvider>
</template>

```

The list of components that are paper context aware is:

* [MiniviewComponent](/vue/docs/reference/MiniviewComponent.md)
* [ControlsComponent](/vue/docs/reference/ControlsComponent.md)
* [ExportControlsComponent](/vue/docs/reference/ExportControlsComponent.md)
* [PaletteComponent](/vue/docs/reference/PaletteComponent.md)
* [ShapePalette](/vue/docs/reference/ShapePaletteComponent.md)
* [InspectorComponent](/vue/docs/reference/InspectorComponent.md)
* [ShapeComponent](/vue/docs/reference/ShapeComponent.md)
