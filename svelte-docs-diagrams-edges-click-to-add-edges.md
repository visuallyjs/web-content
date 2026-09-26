# Click to add edges

This is an input method for edges whereby your users click a shape to select it, and then click a target shape. With pointer devices the user can see the edge that is being created as the pointer moves to the target, but with touch devices this is not the case, so take that into account if you're considering using this.

## Configuration[​](#configuration "Direct link to Configuration")

To setup click to add edges, you specify a flag in your render options:

```html
<script>

import { DiagramComponent } from "@visuallyjs/browser-ui-svelte"
    
const data = ...
    
const options = {
  edges: {
    inputMethod: "click"
  }
}
    
</script>    

<div class="my-container">
    <DiagramComponent data={data} options={options}/>
</div>

```

Shapes are automatically configured as edge targets in a diagram.

## Cancelling edge input[​](#cancelling-edge-input "Direct link to Cancelling edge input")

If you've clicked a source vertex but you wish to abort, you have one of two choices:

* Press the **ESCAPE** key
* Right-click somewhere in the canvas whitespace

caution

If you have set `consumeRightClick:false` in your render options, right click will *not* work to cancel edge input.

## Unattached edges[​](#unattached-edges "Direct link to Unattached edges")

The click to add functionality cannot currently be used to establish an edge whose target is initially unattached.

## Relocating edges[​](#relocating-edges "Direct link to Relocating edges")

Edges that were added via click-to-add can only be relocated by dragging.

## CSS Classes[​](#css-classes "Direct link to CSS Classes")

| Class                         | Description                                                                                        |
| ----------------------------- | -------------------------------------------------------------------------------------------------- |
| `vjs-edge-click-entry-method` | Added to the document body when in click mode for edges, and the user has clicked/tapped a source. |
