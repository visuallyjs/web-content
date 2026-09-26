# Unattached edges

In a diagram, by default, edges may have a `source` and/or `target` vertex, or their source/target may be located in whitespace. We refer to this as an `unattached edge`.

## Configuration[​](#configuration "Direct link to Configuration")

Unattached edges are switched on by default. To turn them off, set `allowUnattached:false` in your render options:

```html
<script>

import { DiagramComponent } from "@visuallyjs/browser-ui-svelte"
    
const data = ...
    
const options = {
  edges: {
    allowUnattached: false
  }
}
    
</script>    

<div class="my-container">
    <DiagramComponent data={data} options={options}/>
</div>

```
