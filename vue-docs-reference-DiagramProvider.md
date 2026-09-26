# \<DiagramProvider/>

This is a context provider that enables you to use various other components alongside a [DiagramComponent](/vue/docs/reference/DiagramComponent.md) without having to explicitly connect them up.

## Usage[​](#usage "Direct link to Usage")

```html
<script setup>
  const data = { ... }
</script>
<template>
  <DiagramProvider>
    <DiagramComponent data={...}/>
    <ControlsComponent/>
    <MiniviewComponent/>
  </DiagramProvider>
</template>

```

The list of components that are surface context aware is:

* [MiniviewComponent](/vue/docs/reference/MiniviewComponent.md)
* [ControlsComponent](/vue/docs/reference/ControlsComponent.md)
* [ExportControlsComponent](/vue/docs/reference/ExportControlsComponent.md)
* [DiagramPaletteComponent](/vue/docs/reference/DiagramPaletteComponent.md)
* [InspectorComponent](/vue/docs/reference/InspectorComponent.md)
