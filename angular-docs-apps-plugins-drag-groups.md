# Drag Groups

A `DragGroup` models a group of vertices that should be dragged together. You can have any number of drag groups in your canvas. When you assign a vertex to a drag group you indicate to VisuallyJs whether that vertex should be an `active` member - meaning that when it is dragged all of the other vertices in the drag group are also dragged - or that it should be a `passive` member - meaning that when it is dragged no other members should be dragged, but that it should be dragged whenever an `active` member is dragged.

### Assigning drag groups[​](#assigning-drag-groups "Direct link to Assigning drag groups")

To assign vertices to drag groups you need to include the `DragGroupsPlugin`:

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';
import { DragGroupsPlugin } from "@visuallyjs/browser-ui"


@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  plugins: [
    {
      type: DragGroupsPlugin.type,
      options: {
        assignDragGroup: (v) => {
          return { id:'dragGroup', active:v.type === 'main' }
        }
      }
    }
  ]
};
}

```

The key piece to note is the `assignDragGroup` function that you provide. In the above example our `assignDragGroup` function instructs VisuallyJs to add every vertex to a group called `"dragGroup"`, but that the vertex should only be an `active` member if it has a `type` of `"main"`.

Consider this dataset:

```javascript
{
  nodes:[
    {"id":"1","left":50,"top":50,"type":"main"},
    {"id":"2","left":250,"top":160},
    {"id":"3","left":350,"top":100},
]

```

We have one `"main"` vertex and two other vertices. In the canvas below, try dragging the large green box around. You'll see the two red boxes drag along with it. Now try dragging one of the red boxes - nothing else moves. This is because all of the nodes are inside a drag group, but the large green node is marked `active` and the red nodes are marked `passive`, due to the `assignDragGroup` function shown above:

**********

The key is the `assignDragGroup` function that we provide. In the implementation above we do two things:

* all vertices are assigned to a drag group called `"dragGroup"`
* The vertex whose `type` is `"main"` is marked `active:true`; the others are marked `active:false`

### Multiple drag groups[​](#multiple-drag-groups "Direct link to Multiple drag groups")

Our example above just used a single drag group, but we can have as many of these as we want. For instance, here's a canvas in which all the red elements are dragged in a single group, and all the green elements are dragged in a different group:

**********

This was an even simpler setup - we just use each node's `type` to specify its drag group:

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';
import { DragGroupsPlugin } from "@visuallyjs/browser-ui"


@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  plugins: [
    {
      type: DragGroupsPlugin.type,
      options: {
        assignDragGroup: (v) => {
          return v.type
        }
      }
    }
  ]
};
}

```

Every element in this example is marked `active` because that's the default if you do not specify it. All we had to do in this example is return the name of a drag group and VisuallyJs adds the vertex as an active participant to that group.

Our dataset in this example is:

```javascript
{
  nodes:[
    {"id":"1","left":50,"top":50,"type":"green"},
    {"id":"2","left":150,"top":160,"type":"red"},
    {"id":"3","left":200,"top":30,"type":"red"},
    {"id":"4","left":250,"top":100,"type":"green"},
]

```

### Example - annotating objects[​](#example---annotating-objects "Direct link to Example - annotating objects")

A good example of how this functionality is useful is the concept of annotating objects in a diagram - explanatory notes for some given vertex that you want to place near the vertex, but whose positioning you want to adjust in each case to suit the diagram. When you drag a vertex that has annotations you want the annotations to move with the vertex, but you want to be able to position the annotations without moving the vertex itself.

Consider this dataset:

```javascript
{
  nodes:[
    {"id":"1","type":"main","left":50,"top":50},
    {"id":"2","type":"main","left":300,"top":50},
    {"id":"3","type":"annotation","text":"I belong to node 1","ref":"1","left":70,"top":-40},
    {"id":"4","type":"annotation","text":"I belong to node 1","ref":"1","left":-90,"top":120},
    {"id":"5","type":"annotation","text":"I belong to node 2","ref":"2","left":380,"top":160},
]

```

We've got two nodes of type `main`, and three nodes of type `annotation`, each of which have a `ref` member, which points to a `main` node. We want to be able to drag our `main` nodes around and have the `annotation` nodes follow, but we also want to be able to position the `annotation` nodes around the `main` nodes where we please. This is easily achieved:

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';
import { DragGroupsPlugin } from "@visuallyjs/browser-ui"


@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  plugins: [
    {
      type: DragGroupsPlugin.type,
      options: {
        assignDragGroup: (v) => {
          return v.type === 'main' ? v.id : {id:v.data.ref, active:false}
        }
      }
    }
  ]
};
}

```

* For nodes of type `main`, we just return the node's id: `v.id`
* For nodes of type `annotation`, we return the `ref` as the drag group id, and mark the vertex passive: `{id:v.data.ref, active:false}`.

Which gives us this arrangement:

**********

And there you have it! Annotated objects using just a few lines of configuration.

#### Cleaning up annotations[​](#cleaning-up-annotations "Direct link to Cleaning up annotations")

One thing to keep in mind is that the annotations and the edges that connect them to their reference nodes will not automatically be removed by VisuallyJs if the reference node is removed from the dataset. To handle this we can use another of VisuallyJs's capabilities you won't find in other libraries in this space - [Transactions](/angular/docs/apps/model/undo-redo.md#transactions) - to cleanup the annotations, but in an undo/redo friendly way.

Try clicking one of the red circle buttons below. We'll remove the node the button belongs to, and we'll also remove any annotations that are attached to it (code follows below) :

**********

To remove a node and its annotations in an undo-friendly way, we find everything we want to delete and then perform all the removals inside a transaction. An example function, into which you'd pass the model and the ID of the node to cleanup, is:

```typescript
function removeNode(model:VisuallyJsModel, nodeId:string) {
    
    // find all annotation nodes that reference this node
    const annotations = model.getNodes().filter(n => n.data.ref === nodeId)

    // in a transaction, remove all the annotation nodes and then the focus node. Edges will be cleaned up automatically, and if the user clicks undo, the entire transaction is rolled back as one.
    model.transaction(() => {
      annotations.forEach(a => model.removeNode(a))
      model.removeNode(nodeId)
    })
}

```

<br />

We declare a node component that extends `BaseNodeComponent`, from which we can access `model` for the underlying model, and `getNode()` to get the vertex that the component represents:

```javascript
import { BaseNodeComponent } from "@visuallyjs/browser-ui-angular"
import {Component} from "@angular/core"

@Component({
  template:`<div>
    <div data-vjs-delete="true" (click)="removeNodeAndAnnotations()"></div>  
  </div>`
})
export class MainNodeComponent extends BaseNodeComponent {
    removeNodeAndAnnotations() {
        const node = this.getNode()
        const annotations = this.model.getNodes().filter(n => n.data.ref === node.id)            
        this.model.transaction(() => {
          annotations.forEach(a => this.model.removeNode(a))
          this.model.removeNode(node.id)
        })
    }
}

```
