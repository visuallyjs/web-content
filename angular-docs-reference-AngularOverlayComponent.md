# AngularOverlayComponent

You can use Angular components as edge overlays in VisuallyJs - any component is allowed, with the one caveat that it must implement this interface.

AngularOverlayComponent

Definition of an angular component that will act as an overlay. This interface exists largely for convenience; the code will write the members of this interface onto any component it creates.

| Name | Type     | Description                             |
| ---- | -------- | --------------------------------------- |
| edge | [Edge]() | The edge that this overlay is drawn on. |

## Usage[​](#usage "Direct link to Usage")

Create a component and declare that it implements this interface:

```typescript
import {Component} from "@angular/core"
import { Edge, VisuallyJsModel, Surface, ObjectData } from "@visuallyjs/browser-ui"
import {AngularOverlayComponent} from "@visuallyjs/browser-ui-angular"

@Component({
    template:`<div class="my-overlay">
  This is edge {{edge.id}} with some value {{edge.data.someValue}}
</div>`
})
export class MyOverlay implements AngularOverlayComponent {
    edge!:Edge
    model!: VisuallyJsModel;
    surface!: Surface;
    data!: ObjectData;
}

```

then map that component in your view options:

```typescript
import {Component} from "@angular/core"
import { MyOverlay } from "./my.overlay.ts"
import {VisuallyJsModule, AngularComponentOverlayType} from "@visuallyjs/browser-ui-angular"

@Component({
    template:`<vjs-surface [viewOptions]="view" [data]="data"/>`
})
export class MyApp {
    data = {
        nodes:[ {id:"1", label:"1", left:50, top:50}, {id:"2", label:"2", left:250, top:250}],
        edges:[
            { source:"1", target:"2", data:{someValue:"hello"}}
        ]
    }
    
    view = {
      edges: {
          default: {
              overlays: [{
                  type: AngularComponentOverlayType,
                  options: {
                      component: MyOverlay
                  }
              }]
          }
      }  
    }
}

```

## BaseAngularOverlayComponent[​](#baseangularoverlaycomponent "Direct link to BaseAngularOverlayComponent")

`BaseAngularOverlayComponent` is an abstract implementation of `AngularComponentOverlay`, which provides a few class members and methods that can be useful.

We could update our code from above to use one like this:

```typescript
import {Component} from "@angular/core"
import { Edge } from "@visuallyjs/browser-ui"
import {BaseAngularOverlayComponent} from "@visuallyjs/browser-ui-angular"

@Component({
    template:`<div class="my-overlay">
  This is edge {{edge.id}} with some value {{obj.someValue}}
</div>`
})
export class MyOverlay extends BaseAngularOverlayComponent { }

```

Notice two things:

* We no longer needed to declare `edge` on the component, as the superclass does that
* We could replace `edge.data` with `data`, to access the underlying data.

### Class Members[​](#class-members "Direct link to Class Members")

| Name                               | Type                | Description                                                                                                            |
| ---------------------------------- | ------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| data                               | [ObjectData]()      | Backing data for the edge this overlay is attached to                                                                  |
| edge                               | [Edge]()            | Underlying Edge model object this overlay is attached to                                                               |
| model                              | [VisuallyJsModel]() | The underlying model                                                                                                   |
| ui                                 | T                   | The UI that this overlay is rendered by                                                                                |
| removeEdge()                       | void                | Remove the underlying edge. This will unload the edge and its visual representation, including this overlay component. |
| updateEdge(updates:[ObjectData]()) | void                | Update the underlying edge with the given data.                                                                        |
