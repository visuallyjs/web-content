# Unattached edges

In a diagram, by default, edges may have a `source` and/or `target` vertex, or their source/target may be located in whitespace. We refer to this as an `unattached edge`.

## Configuration[​](#configuration "Direct link to Configuration")

Unattached edges are switched on by default. To turn them off, set `allowUnattached:false` in your render options:

```typescript

import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular";
import {Component} from "@angular/core";

@Component({
    template:`<div style="width:100%;height:500px">
<vjs-diagram [data]="data" [options]="options"/>
</div>`
export class MyComponent {
    data = ...
    
    options = {
  edges: {
    allowUnattached: false
  }
}
}

```
