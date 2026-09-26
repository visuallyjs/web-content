# Dragging Nodes and Groups

By default, all node/group elements rendered by the UI will be made draggable, and the default behaviour of a draggable element is that it can be dragged to anywhere on the canvas. No special treatment is needed for touch devices - VisuallyJs abstracts that away.

## Drag options[​](#drag-options "Direct link to Drag options")

You can provide `dragOptions` when you render a UI. The most common reason for doing this is that you want to restrict the areas of your elements that your users can use to drag the element, for which you can provide a `cssFilter`:

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  dragOptions: {
    cssFilter: ".someClass, .someClass *, .someOtherClass *"
  }
};
}

```

This instructs VisuallyJs to not allow dragging to start when the mousedown/touchstart event occurs on an element that matches the given selector.

The full list of options is:

DragOptions

Options for element drag

| Name                   | Type                                                                                         | Description                                                                                                                                                                                                                                                                                                                   |
| ---------------------- | -------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| autoPan?               | boolean                                                                                      | Defaults to true, meaning the canvas will pan automatically to track elements that have been dragged out of the visible area.                                                                                                                                                                                                 |
| autoPanBoundsStrategy? | [AutoPanBoundsStrategy]()                                                                    | When auto-panning, this flag instructs the auto pan how to determine if an element is inside the root bounds or not. A value of "contained" (the default), means the whole element has to be inside the root bounds. A value of "intersecting" means that the element needs to just intersect the root bounds by some amount. |
| autoPanDelta?          | number                                                                                       | When auto-panning, this is the number of pixels that the canvas repositions itself on each tick. Defaults to 5.                                                                                                                                                                                                               |
| autoPanRepeat?         | number                                                                                       | When auto-panning, this is the speed (in milliseconds) at which the canvas repositions itself. Defaults to 15ms.                                                                                                                                                                                                              |
| canDrop?               | (candidate:[Node]() \| [Group](), target:[Node]() \| [Group](), onCanvas:boolean) => boolean | Optional function that is invoked at the start of a drag, and which identifies allowed drop targets. Each target - the canvas, nodes and groups - is passed in turn to this method; returning false indicates that the given target is not valid for that drag.                                                               |
| constrainFunction?     | [DragConstrainFunction\<E>]()                                                                | Optional function to use to constrain element dragging.                                                                                                                                                                                                                                                                       |
| cssFilter?             | string                                                                                       | Optional CSS3 selector identifying parts of nodes/groups that should not cause a drag to start.                                                                                                                                                                                                                               |
| filter?                | [VertexDragFilter\<E>]()                                                                     | Optional function to invoke prior to a drag starting.                                                                                                                                                                                                                                                                         |

## Preventing dragging[​](#preventing-dragging "Direct link to Preventing dragging")

Dragging can be switched off in a few ways.

### All elements[​](#all-elements "Direct link to All elements")

If you wish to switch off dragging for all elements you can set that in your render options:

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  elementsDraggable: false
};
}

```

### Per element[​](#per-element "Direct link to Per element")

You can also control element dragging by writing a `data-vjs-not-draggable` attribute onto your node/group DOM element:

```html
<div data-vjs-not-draggable="true">
    This vertex is not draggable.
</div>

```

### CSS filter[​](#css-filter "Direct link to CSS filter")

`cssFilter` allows you to provide a CSS selector identifying elements that should be excluded from dragging:

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  dragOptions: {
    cssFilter: ".some-selector, [data-some-attribute]"
  }
};
}

```

### Filter function[​](#filter-function "Direct link to Filter function")

`filter` is a function that can be used to programmatically determine if a drag should start:

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  dragOptions: {
    filter: (p:{el:BrowserElement, vertex:Node|Group, e:MouseEvent}) => {
  return vertex.objectType !== Group.objectType
}
  }
};
}

```

### Programmatically[​](#programmatically "Direct link to Programmatically")

If you want to enable/disable dragging for some specific element on an ad-hoc basis you can use the `setDraggable` method:

```javascript

surface.setDraggable("1", false)          // mark node "1" as not draggable, using its id


```

`setDraggable` takes as argument either a vertex id, a vertex object, or a DOM element.

## Dragging on a grid[​](#dragging-on-a-grid "Direct link to Dragging on a grid")

You can impose a grid on the elements in a surface:

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  grid: {
    size: {
      width: 50,
      height: 50
    }
  }
};
}

```

The full list of options supported by grid are defined in the [GridOptions]() interface:

GridOptions

Options for a grid in the UI

| Name             | Type     | Description                                                                                                                               |
| ---------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| fitGroupsToGrid? | boolean  | Whether or not to ensure calculated group sizes (from auto sized groups) are a multiple of the grid size in each axis. Defaults to false. |
| size?            | [Grid]() | Width/height of the grid cells                                                                                                            |
| snap?            | boolean  | Whether or not to snap elements to the grid when dragging. Defaults to false.                                                             |

## Magnetizing[​](#magnetizing "Direct link to Magnetizing")

VisuallyJs has a built in "magnetizer", which provides a means to nudge elements around in your UI so that things don't overlap. There are a few different ways to use the magnetizer, and it is covered in full [on this page](/angular/docs/apps/magnetizer.md). In the canvas below we're using the magnetizer in `constant` mode, so that as you drag a vertex the other vertices are moved aside. We've also switched on `trackback`, which causes vertices to try to move back to their original position wherever possible.

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  magnetizer: {
    constant: true,
    trackback: true
  }
};
}

```

**********

## Drag events[​](#drag-events "Direct link to Drag events")

The UI posts a few events to which you can subscribe in order to track the movement of vertices on your canvas. These events can be subscribed to either when creating the surface:

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';
import { EVENT_NODE_MOVE_END } from "@visuallyjs/browser-ui"


@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  dragOptions: {
    events: {
      $[EVENT_NODE_MOVE_END]: (params) => {
      // a node was moved
  }
    }
  }
};
}

```

or you can bind to them after creating the surface:

```javascript

surface.bind(EVENT_NODE_MOVE_END, (params) => {
    // a node was moved
})

```

The full list of events you can map to is:

| Name                      | Value                              | Payload                   | Description                                                             |
| ------------------------- | ---------------------------------- | ------------------------- | ----------------------------------------------------------------------- |
| EVENT\_GROUP\_MOVE        | "group<!-- -->:move<!-- -->"       | [VertexMoveParams]()      | Fired each time the mouse/pointer moves while a group is being dragged. |
| EVENT\_GROUP\_MOVE\_END   | "group:move<!-- -->:end<!-- -->"   | [VertexMoveEndParams]()   | Fired at the end of a group drag                                        |
| EVENT\_GROUP\_MOVE\_START | "group:move<!-- -->:start<!-- -->" | [VertexMoveStartParams]() | Fired as the user starts to drag a group                                |
| EVENT\_NODE\_MOVE         | "node<!-- -->:move<!-- -->"        | [VertexMoveParams]()      | Fired each time the mouse/pointer moves while a node is being dragged.  |
| EVENT\_NODE\_MOVE\_ABORT  | "node:move<!-- -->:abort<!-- -->"  | [VertexMoveStartParams]() | Fired if a node drag is aborted                                         |
| EVENT\_NODE\_MOVE\_END    | "node:move<!-- -->:end<!-- -->"    | [VertexMoveEndParams]()   | Fired at the end of a node drag                                         |
| EVENT\_NODE\_MOVE\_START  | "node:move<!-- -->:start<!-- -->"  | [VertexMoveStartParams]() | Fired as the user starts to drag a node                                 |

## Auto pan[​](#auto-pan "Direct link to Auto pan")

VisuallyJs will auto pan a canvas when a node/group is dragged outside of the visible bounds. This can be controlled with a few flags set inside the `dragOptions`:

* **autoPan** Set to false if you wish to switch off auto panning.
* **autoPanDelta** Defaults to 5 pixels. This is the amount by which the canvas will pan on each tick of the timer.
* **autoPanRepeat** The time in milliseconds between each tick of the auto pan timer. Defaults to 10 milliseconds.

### Switching off auto pan[​](#switching-off-auto-pan "Direct link to Switching off auto pan")

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  dragOptions: {
    autoPan: false
  }
};
}

```

### Changing auto pan repeat time[​](#changing-auto-pan-repeat-time "Direct link to Changing auto pan repeat time")

Here we tell VisuallyJs to pan the canvas every 5ms instead of the default:

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  dragOptions: {
    autoPanRepeat: 5
  }
};
}

```

### Changing auto pan delta[​](#changing-auto-pan-delta "Direct link to Changing auto pan delta")

Here we tell VisuallyJs to move 15 pixels on each step instead of the default:

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  dragOptions: {
    autoPanDelta: 15
  }
};
}

```

## Identifying drop targets[​](#identifying-drop-targets "Direct link to Identifying drop targets")

By default, an element can be dragged to any position on the canvas, and into any group. You can use the `canDrop` option of `dragOptions` to restrict where an element can be dropped:

```javascript
dragOptions:{
  canDrop:(candidate, target, onCanvas) => {
    // return true if the candidate can be dropped on the target
  }
}

```

The arguments passed to `canDrop` are:

* **candidate** The node or group being dragged.
* **target** The node, group, or canvas that is a potential drop target.
* **onCanvas** A boolean indicating if the target is the canvas.

VisuallyJs calls this function for every possible drop target when a drag starts. If you return `false` for a given target, VisuallyJs will not allow the candidate to be dropped there.

## Drag groups[​](#drag-groups "Direct link to Drag groups")

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

## CSS Classes[​](#css-classes "Direct link to CSS Classes")

There are a number of CSS classes assigned to various parts of the UI during a node/group drag. These can be used to easily add visual cues for your users, and also to manage z-index for the best user experience.

| Class                              | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `vjs-drag-active`                  | Assigned to any element that is a candidate drop target for an edge that is being dragged                                                                                                                                                                                                                                                                                                                                                                                 |
| `vjs-drag-hover`                   | Assigned to any element that is the current drop target for an edge that is being dragged                                                                                                                                                                                                                                                                                                                                                                                 |
| `vjs-drag-hover-cannot-drop`       | Assigned to a vertex or the canvas when an element that is being dragged on the canvas is hovering over it but drop is not allowed.                                                                                                                                                                                                                                                                                                                                       |
| `vjs-drag-original-group`          | Assigned to a group element when one of its children is being dragged. This can be useful to help manage z-index: we recommend using this class to set a z-index for the drag parent group above that of the other groups, which will ensure that the element you are dragging will appear on top of other groups.                                                                                                                                                        |
| `vjs-element-dragging`             | Assigned by the Surface to a vertex element that is being dragged                                                                                                                                                                                                                                                                                                                                                                                                         |
| `vjs-group-child-element-dragging` | Assigned by the Surface to the group parent of a vertex element that is being dragged, if applicable. You can use this class for a couple of things - to show that a child element is being dragged, of course, but also a good idea is to use this class to bump the z-index for any group that has it assigned, to put that group above other groups. This ensures that as you drag a child vertex over to some other group, it appears on top of that group in the UI. |
| `vjs-most-recently-dragged`        | Assigned by the Surface to the vertex element(s) that was/were the most recently dragged elements.                                                                                                                                                                                                                                                                                                                                                                        |
| `vjs-surface-element-dragging`     | Assigned by the Surface to its container when a node or group is being dragged                                                                                                                                                                                                                                                                                                                                                                                            |
