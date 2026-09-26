# Snaplines

Snaplines provide visual cues to allow your users to fine-tune their layouts. When two edges are in proximity a snapline is shown, or when the center of some vertex is in proximity with the edge(s) of some other vertex/vertices. When the two objects are aligned exactly, an additional class is written to the snapline, allowing you to provide your users with a visual cue.

**********

## Instantiation[​](#instantiation "Direct link to Instantiation")

Snaplines can be specified in the `plugins` of the render options for some surface:

```html
<script setup>

import { SnaplinesPlugin } from "@visuallyjs/browser-ui"

const renderOptions = {
  plugins: [
    {
      type: "snaplines",
      options: {}
    }
  ]
}


</script>
<template>
  <SurfaceComponent :renderOptions="renderOptions" />
</template>

```

## Configuration[​](#configuration "Direct link to Configuration")

SnaplinesPluginOptions

Options for the SnaplinesPlugin

| Name         | Type    | Description                                                                                                                                                |
| ------------ | ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| enabled?     | boolean | Defaults to true. If false, you can start the plugin in disabled mode.                                                                                     |
| showCenters? | boolean | Whether or not to show center snaplines. Defaults to true.                                                                                                 |
| showEdges?   | boolean | Whether or not to show edge snaplines. Defaults to true.                                                                                                   |
| tolerance?   | number  | The tolerance either side of a snapline inside which an element must be before the snapline is activated. Defaults to 10 pixels (either side of the line). |

## Enable/disable[​](#enabledisable "Direct link to Enable/disable")

You can switch the snaplines plugin on and off via its `setEnabled(..)` method. To do this, you need to get a reference to the plugin and then call the method:

```javascript
const snaplinesPlugin = surface.getPlugin(SnaplinesPlugin.type)
snaplinesPlugin.setEnabled(false)

```

## CSS Classes[​](#css-classes "Direct link to CSS Classes")

Snaplines are drawn as DIV elements, and several CSS classes are exposed to allow you to control their appearance.

| Class                       | Description                                                                                                                      |
| --------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| `vjs-snapline`              | Assigned to both horizontal and vertical snaplines when active                                                                   |
| `vjs-snapline-active`       | Assigned to an element attached to an active snapline                                                                            |
| `vjs-snapline-active-exact` | Assigned to an element attached to an active snapline and the elements on the snapline are exactly aligned (parsed to integers). |
| `vjs-snapline-exact`        | Assigned to both horizontal and vertical snaplines when the elements are exactly aligned                                         |
| `vjs-snapline-horizontal`   | Assigned to horizontal snaplines when active                                                                                     |
| `vjs-snapline-vertical`     | Assigned to vertical snaplines when active                                                                                       |

## Options[​](#options "Direct link to Options")

SnaplinesPluginOptions

Options for the SnaplinesPlugin

| Name         | Type    | Description                                                                                                                                                |
| ------------ | ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| enabled?     | boolean | Defaults to true. If false, you can start the plugin in disabled mode.                                                                                     |
| showCenters? | boolean | Whether or not to show center snaplines. Defaults to true.                                                                                                 |
| showEdges?   | boolean | Whether or not to show edge snaplines. Defaults to true.                                                                                                   |
| tolerance?   | number  | The tolerance either side of a snapline inside which an element must be before the snapline is activated. Defaults to 10 pixels (either side of the line). |
