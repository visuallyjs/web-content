# Popups

Popups, new in 1.2.1, offer a means for you to declaratively attach some component to act as a popup on a vertex, and as the user pans, zooms or drags the vertex, VisuallyJs will ensure that the popup remains in place relative to the element.

![Popups](https://static.visuallyjs.com/img/blog/1.2.1/popups.png)

## Configuration[​](#configuration "Direct link to Configuration")

### Declare Component[​](#declare-component "Direct link to Declare Component")

<!-- -->

<!-- -->

To configure a popup in Angular you need to define a component that will take a `vertex`, `model` and `ui` as props (and, optionally, a `hide` function that your component can use to tell the popup to hide). This example (shown above) is from our [AI Agent Builder demonstration](/demonstrations/ai-agent-builder.md):

```typescript

import {BrowserUIModel, Node, Surface} from '@visuallyjs/browser-ui';
import {Component, Input} from '@angular/core';

@Component({
selector:"app-popup",
template:"<div><h3>{{vertex.data.label}}</h3><button (click)="update()">UPDATE</button></div>"
})
export class PopupComponent {
@Input() vertex!:Node
@Input() model!:BrowserUIModel
@Input() ui!:Surface
@Input() hide?:Function

update() {
  this.model.updateNode(this.vertex, {label:"CHANGED"})
}
}

```

<!-- -->

<!-- -->

Your component has access to:

* the vertex the popup is attached to
* the data model
* the UI that rendered this popup
* a function you can invoke to instruct the popup to hide

### Configure Popup[​](#configure-popup "Direct link to Configure Popup")

<!-- -->

<!-- -->

Then to declare that you want to use this component as a popup, you need to declare a `vjs-surface-popup` in your component's template, and specify the selector that the popup should listen for:

```html

<vjs-surface [data]="data" [viewOptions]="view" [renderOptions]="renderOptions">
    <vjs-surface-popup selector=".vjs-next-step-picker">
      <ng-template let-vertex="vertex" let-model="model" let-ui="ui">
        <app-popup [vertex]="vertex" [model]="model" [ui]="ui"/>
      </ng-template>
    </vjs-surface-popup>
  </vjs-surface>

```

<!-- -->

<!-- -->

### Add Popup Launcher[​](#add-popup-launcher "Direct link to Add Popup Launcher")

<!-- -->

<!-- -->

Lastly, you can now include a launcher for this popup anywhere inside a component you're using to render a vertex:

```typescript

@Component({
selector:"app-component",
template:`<div>
      <h1>{{$data().label}}</h1>
      <button class="vjs-next-step-picker">Launch popup</button>
  </div>`
})
export class MyVertexComponent extends BaseNodeComponent() {}

```

<!-- -->
