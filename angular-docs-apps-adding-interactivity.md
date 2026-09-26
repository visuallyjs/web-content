# Adding Interactivity

In the [Building an App](/angular/docs/apps/building-an-app.md) page we ran through the steps involved in creating a basic app and having it display some nodes and edges. On this page we're going to talk you through how to go about adding interactivity to the app - such things as the ability to drag new edges, respond to events, and more.

## Dragging edges[​](#dragging-edges "Direct link to Dragging edges")

To add support for dragging edges between vertices, we need to update the components we use to draw our nodes with some markup containing specific VisuallyJs attributes. We'll add a little red circle to the corner of each node to use an edge drag source, and we'll make the entire node element a drag target:

##### Node component[​](#node-component "Direct link to Node component")

```typescript
import { Component } from "@angular/core"
import { BaseNodeComponent } from '@visuallyjs/browser-ui-angular'

@Component({
    template:`<div data-vjs-target="true" class="my-node">
            <span>{{data.label}} {{data.id}}</span>
            <div class="edge-source" data-vjs-source="true"/>
        </div>`
})
export class MyNodeComponent extends BaseNodeComponent { } 

```

##### Group component[​](#group-component "Direct link to Group component")

```typescript
import { Component } from "@angular/core"
import { BaseGroupComponent } from '@visuallyjs/browser-ui-angular'

@Component({
    template:`<div data-vjs-target="true" class="my-group">
        <strong>{{data.label}} {{data.id}}</strong>
        <div data-vjs-group-content="true"/>
        <div class="edge-source" data-vjs-source="true"/>
    </div>`
})
export class MyGroupComponent extends BaseGroupComponent { } 

```

**********

We've used some CSS to style the `.edge-source` elements. The key points to note are the **data-vjs-target** attribute on the node's root element, and the **data-vjs-source** attribute on the connect elements - respectively, they inform VisuallyJs that the entire element is an edge target, and that the red circles are edge sources. You can use any markup you like to setup this mechanism, you just need to use those attributes.

Edges created with this setup will be of type `default`, but there are a number of attributes you can use to control what type of edge is created - we refer you to the [Edges](/angular/docs/apps/edges/overview.md) documentation.

## Events[​](#events "Direct link to Events")

VisuallyJs has a powerful event binding mechanism that allows you to map handlers to operations on the objects in your model. For example, let's map a `tap` event to our various mappings:

```typescript

import { Component } from "@angular/core"
import { VisuallyJsModule } from '@visuallyjs/browser-ui-angular'
import { EVENT_TAP,
    NodeEventCallbackPayload,
    GroupEventCallbackPayload,
    EdgeEventCallbackPayload} from "@visuallyjs/browser-ui"


@Component({
    template:`<div style="width:600px;height:500px">
        <vjs-surface [data]="data" [viewOptions]="viewOptions">
            <vjs-controls/>
            <vjs-miniview/>
        </vjs-surface>
    </div>`,
    imports:[VisuallyJsModule]
})
export class MyApp {

    data = { ... }

    viewOptions = {
        nodes:{
            default:{
                component:MyNodeComponent,
                events:{
                    [EVENT_TAP]:(p:NodeEventCallbackPayload)  => {
                        alert(`You clicked on node ${p.obj.id}`)
                    }
                }
            }
        },
        groups: {
            default: {
                constrain:true,
                component:MyGroupComponent,
                events:{
                    [EVENT_TAP]:(p:GroupEventCallbackPayload)  => {
                        alert(`You clicked on group ${p.obj.id}`)
                    }
                }
            }
        },
        edges:{
            default:{
                overlays:[{
                    type:ArrowOverlay.type,
                    options:{
                        location:1
                    }
                }],
                events:{
                    [EVENT_TAP]:(p:EdgeEventCallbackPayload)  => {
                        if(confirm(`You clicked on edge ${p.obj.id}. Do you want to delete it?`)) {
                            p.model.removeEdge(p.obj)
                        }
                    }
                }
            }
        }
    }
}

```

Try clicking on a node, group or edge - for nodes and groups you'll see a popup displaying their id, but for edges we ask you if you want to delete the edge. This demonstrates a powerful common thread throughout VisuallyJs - programmatically, you operate on your app at the data model level, and VisuallyJs takes care of what that means for the UI.

**********

Notice in the event mappings above the various types for the callback payloads:

* Node event listeners are invoked with an object of type [NodeEventCallbackPayload]()
* Group event listeners are invoked with an object of type [GroupEventCallbackPayload]()
* Edge event listeners are invoked with an object of type [EdgeEventCallbackPayload]()

info

A `tap` event is an event captured by VisuallyJs, which consists of a `mousedown` event on some element, followed by a `mouseup` event on the same element, where the pointer has not moved between the two events. We recommend you use these events in preference to `click` events throughout your code, unless you have a specific reason to bind to a `click`. Browsers will fire a click event when you drag an element; they do not check that the pointer is in the same location on mouseup as it was on mousedown.

## Next Steps[​](#next-steps "Direct link to Next Steps")

[Layouts](layouts/overview)

[Read about the available layouts in VisuallyJs](layouts/overview)

[Edges](edges/overview)

[Read about everything you can do with edges](edges/overview)
