# \<ShapePropertiesInspector/>

## Usage[​](#usage "Direct link to Usage")

If you haven't yet read the docs for [InspectorComponent](/vue/docs/reference/InspectorComponent.md) we'd recommend it.

This component renders the properties defined by the selected shape in the active shape library. Use it inside an inspector and pass it the vertex being inspected.

```html
<script setup>
import { ShapePropertiesInspectorComponent } from "@visuallyjs/browser-ui-vue"
import { isNode } from "@visuallyjs/browser-ui"
import { ref } from "vue"

const current = ref(null)
</script>

<template>
  <InspectorComponent v-model="current">
    <ShapePropertiesInspectorComponent
      v-if="current != null && isNode(current)"
      :vertex="current"
    />
  </InspectorComponent>
</template>

```

## Props[​](#props "Direct link to Props")

ShapePropertiesInspectorProps

| Name       | Type       | Description                                                                                                        |
| ---------- | ---------- | ------------------------------------------------------------------------------------------------------------------ |
| maxRadios? | number     | The maximum number of radio buttons to show for a value list before switching to a select dropdown. Defaults to 7. |
| vertex     | [Vertex]() | vertex to inspect                                                                                                  |

`maxRadios` controls how many choices are displayed as radio buttons before the inspector uses a dropdown.
