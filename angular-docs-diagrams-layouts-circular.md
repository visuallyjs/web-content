# Circular Layout

Arranges all the nodes/groups in the model into a circle, with a radius sufficiently large that no two nodes/groups overlap.

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';
import { CircularLayout } from "@visuallyjs/browser-ui"


@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  layout: {
    type: CircularLayout.type
  }
};
}

```

***

### Parameters[​](#parameters "Direct link to Parameters")

CircularLayoutParameters

Parameters for the circular layout.

| Name              | Type                 | Description                                                                                                                                                                                                                                                               |
| ----------------- | -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| centerContent?    | boolean              | Whether or not to shift the layout so that the origin is \[width/2, height/2] and not \[0,0]. This is useful in situations such as groups, where elements cannot be placed in a negative position in either axis (due to there being no facility to pan the group canvas) |
| centerRoot?       | boolean              | If true, the first node in the data set will be placed in the center of the circle. Defaults to false.                                                                                                                                                                    |
| height?           | number               | Optional fixed height for the layout.                                                                                                                                                                                                                                     |
| locationFunction? | [LocationFunction]() | Optional function that, given some vertex, can provide the x/y location of the vertex on the canvas                                                                                                                                                                       |
| padding?          | [PointXY]()          | Optional padding to put around the elements.                                                                                                                                                                                                                              |
| width?            | number               | Optional fixed width for the layout.                                                                                                                                                                                                                                      |

***

### Centering the root node[​](#centering-the-root-node "Direct link to Centering the root node")

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';
import { CircularLayout } from "@visuallyjs/browser-ui"


@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  layout: {
    type: CircularLayout.type,
    options: {
      centerRoot: true
    }
  }
};
}

```
