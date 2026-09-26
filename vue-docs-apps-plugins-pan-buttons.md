# Pan Buttons

Provides buttons around the perimeter of the Surface canvas that allow the user to nudge the pan. Users can click and hold to auto pan.

**********

## Setup[​](#setup "Direct link to Setup")

```html
<script setup>

import { PanButtonsPlugin } from "@visuallyjs/browser-ui"

const renderOptions = {
  plugins: [
    PanButtonsPlugin.type
  ]
}


</script>
<template>
  <SurfaceComponent :renderOptions="renderOptions" />
</template>

```

## CSS Classes[​](#css-classes "Direct link to CSS Classes")

There are a number of classes added to the elements this plugin creates, allowing you to style the buttons as you like:

| Class                    | Description                                                             |
| ------------------------ | ----------------------------------------------------------------------- |
| `vjs-surface-pan`        | Assigned to each of the pan buttons added around the surface.           |
| `vjs-surface-pan-active` | Assigned when the user is pressing a pan button and a pan is in motion. |
| `vjs-surface-pan-bottom` | Assigned to the pan button on the bottom edge of the surface.           |
| `vjs-surface-pan-left`   | Assigned to the pan button added on the left edge of the surface.       |
| `vjs-surface-pan-right`  | Assigned to the pan button on the right edge of the surface.            |
| `vjs-surface-pan-top`    | Assigned by to the pan button on the top edge of the surface.           |

## Options[​](#options "Direct link to Options")

PanButtonsPluginOptions

Options for the pan buttons plugin.

| Name               | Type   | Description                                                                                             |
| ------------------ | ------ | ------------------------------------------------------------------------------------------------------- |
| panDistance?       | number | Amount in pixels to pan the surface by when one of the buttons is pressed and released. Defaults to 50. |
| panRepeatDistance? | number | Amount in pixels to adjust pan by each time the timer fires. Defaults to 10.                            |
| panRepeatInterval? | number | Time in milliseconds between successive adjustment to the pan. Defaults to 60.                          |
| startPanTimeout?   | number | Time in milliseconds after the mouse button is pressed before panning should start. Defaults to 150.    |
