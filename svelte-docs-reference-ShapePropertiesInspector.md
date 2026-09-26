# \<ShapePropertiesInspector/>

## Usage[​](#usage "Direct link to Usage")

If you haven't yet read the docs for [InspectorComponent](/svelte/docs/reference/InspectorComponent.md) we'd recommend it.

This component renders the properties defined by the selected shape in the active shape library. Use it inside an inspector and pass it the vertex being inspected.

```html
<script lang="ts">
import { InspectorComponent, ShapePropertiesInspector } from "@visuallyjs/browser-ui-svelte"
import { isNode } from "@visuallyjs/browser-ui"
import type { Base } from "@visuallyjs/browser-ui"

let current = $state<Base | null>(null)
</script>

<InspectorComponent bind:current={current}>
  {#if current != null && isNode(current)}
    <ShapePropertiesInspector vertex={current} />
  {/if}
</InspectorComponent>

```

## Props[​](#props "Direct link to Props")

ShapePropertiesInspectorProps

Props for ShapePropertiesInspector

| Name       | Type       | Description                                                                                                        |
| ---------- | ---------- | ------------------------------------------------------------------------------------------------------------------ |
| maxRadios? | number     | The maximum number of radio buttons to show for a value list before switching to a select dropdown. Defaults to 7. |
| vertex     | [Vertex]() | vertex to inspector                                                                                                |

`maxRadios` controls how many choices are displayed as radio buttons before the inspector uses a dropdown.
