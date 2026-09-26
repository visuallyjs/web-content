# Edge Labels

You can extract the value of each edge's `label` from the edge's backing data:

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
    showLabels: true
  }
}
}

```

**********

## Rotated labels[​](#rotated-labels "Direct link to Rotated labels")

By default, edge labels will be drawn so that the text reads horizontally. You can instruct VisuallyJs to rotate edge labels to match the slope of the connector line via the `labelsRotatable` edge option:

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
    showLabels: true,
    labelsRotatable: true,
    targetMarker: "Arrow"
  }
}
}

```

**********

### Strict rotation[​](#strict-rotation "Direct link to Strict rotation")

In the above example, the edge's source is to the right of the target, and so, strictly speaking, if the label were rotated to match the slope of the connector, it would be flipped. Since this is not easy to read for a user, by default we rotate labels in `"legible"` mode - when the angle of rotation lies between 90 and 270 degrees, we flip it.

If you want VisuallyJs to strictly honour the slope of the connector, you can set `strict` for `labelsRotatable`:

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
    showLabels: true,
    labelsRotatable: "strict",
    targetMarker: "Arrow"
  }
}
}

```

**********

## Label location[​](#label-location "Direct link to Label location")

By default, an edge label will be assigned a location of `0.5` - meaning it will be halfway along the edge path. You can change this by providing a `labelLocation`:

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
    showLabels: true,
    labelLocation: 0.25
  }
}
}

```

**********

You can also control this via a `labelLocation` value in your edge's backing data. For example, this edge:

```javascript
{
    source:"someNode",
    target:"someOtherNode",
    data:{
        labelLocation:0.25
    }
}

```

would instruct VisuallyJs to put the label at 0.25, and you would not need to set `labelLocation` in the edge options.
