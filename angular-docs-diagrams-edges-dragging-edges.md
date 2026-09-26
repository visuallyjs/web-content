# Dragging edges

By default, shapes in a diagram are configured as edge drag targets, and, when selected, as edge drag sources, via the arrow icon in the bottom right corner of the selection frame. In the diagram below we have programmatically selected a cell via the `selectCell` method of the diagram - try dragging an edge from the arrow in the bottom right corner of the "Drag from me" shape and dropping it anywhere on the "Drag to me" shape:

**********

## Visual cues[​](#visual-cues "Direct link to Visual cues")

### While dragging[​](#while-dragging "Direct link to While dragging")

There are two main CSS classes you can use to provide visual cues to your users about the state of an edge drag:

* `vjs-drag-active` When an edge is being dragged, this class is assigned to all elements onto which the edge could be dropped

* `vjs-drag-hover` When an edge is being dragged and the mouse is hovering over a possible target, this class is assigned to that element

In the canvas below we have these style rules:

```css
.vjs-node {
    outline:1px solid;
}
  
.vjs-drag-active {
    outline:2px solid forestgreen;
}

.vjs-drag-hover {
  outline:4px solid orangered;
}

```

Try dragging an edge - you'll see the `.vjs-drag-active` class applied to each of the nodes initially. When you drag the edge over one of the nodes you'll see the `.vjs-drag-hover` class applied:

**********

### Connected elements[​](#connected-elements "Direct link to Connected elements")

When some element has one or more edges attached to it, VisuallyJs adds the CSS class `vjs-connected` to the element in the DOM. In the canvas below we have this style rule declared:

```css
.vjs-connected g {
    fill:#0a58ca;
}

```

Nodes 1 and 2 are connected in our initial dataset and are, accordingly, painted with a blue background, via the CSS rule. If you drag a new edge (from one of the red circles) to node 3 you'll see it update to have a blue background, as the `vjs-connected` class will be assigned when the edge is established.

**********

***

## Specifying source/target elements[​](#specifying-sourcetarget-elements "Direct link to Specifying source/target elements")

As mentioned above, the default behaviour of a diagram is to attach a drag source element to the selection rectangle when a shape is selected. If you want more fine-grained control over which parts of your element as used as the source/target for edge dragging, you can add `data-vjs-source` and/or `data-vjs-target` attributes to specific elements. For example, this is a shape that has a blue circle in its top right corner, and that circle can be used to drag source edges:

```html
<svg width="{{width}}" height="{{height}}" viewBox="0 0 100 100" overflow="visible">
  <rect x="0" y="0" width="100" height="100" stroke="midnightblue" stroke-width="3"/>
  <circle cx="90" cy="10" r="5" stroke="none" fill="blue" data-vjs-source="true"/>
</svg>

```

We added this to a simple shape library:

```javascript
const SIMPLE_SHAPE_LIB = {
  id:"demo-source",
  shapes:[
    {
      type:"shape",
      template:`...template from above...`
    }
  ]
}

```

and then loaded it into a diagram:

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
  shapes: [SIMPLE_SHABE_LIB]
}
}

```

Now you can drag edges from the small blue circles:

**********

This is a good start, but there are a few caveats to consider with the above example:

* We're still relying on the fact that whole elements are targets by default - we cannot drag to a specific location on the target
* When we select a node, it still shows the drag source element in the selection frame;
* Our edge shows as being connected to the shape's main element, rather than the blue circle.

We'll address each of these.

### Default target[​](#default-target "Direct link to Default target")

We can tell VisuallyJs not to make a shape a target by default via the `defaultTarget` property in a shape type:

```javascript
const SIMPLE_SHAPE_LIB = {
  id:"demo-source",
  shapes:[
    {
      type:"shape",
      defaultTarget:false,
      template:`...template from above...`
    }
  ]
}

```

### Hide source handle[​](#hide-source-handle "Direct link to Hide source handle")

To suppress the edge source handle, we can use a `mediator` (discussed in detail [on this page](/angular/docs/diagrams/controlling-diagram-actions.md)):

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
  shapes: [SIMPLE_SHABE_LIB],
  mediator: {
    canLink: () => false
  }
}
}

```

This is a simple mediator which does not consider the context at all, it just disables link for all shapes. `canLink` is given the vertex that has been selected as an argument, and so you can perform more sophisticated checks than what we have here - check the linked page for details.

At this point we have suppressed the default source edge handle, and instructed VisuallyJs that our shape should not be treated as a target - but now we're not going to be able to drag any edges! So let's update the shape template with a target element:

```html
<svg width="{{width}}" height="{{height}}" viewBox="0 0 100 100" overflow="visible">
  <rect x="0" y="0" width="100" height="100" stroke="midnightblue" stroke-width="3"/>
  <circle cx="90" cy="10" r="5" stroke="none" fill="blue" data-vjs-source="true"/>
  <circle cx="10" cy="10" r="5" stroke="none" fill="orangered" data-vjs-target="true"/>
</svg>

```

Now you can drag from the blue circle to the red circle:

**********

...but we still have the issue that the edge is connected to the main element and not the circles. If you wanted to setup a connection between the circles, you'd need to introduce `ports` to your UI: addressable elements that are children of the main shape. We'll update our template with a `data-vjs-port` attribute on the source and target:

```html
<svg width="{{width}}" height="{{height}}" viewBox="0 0 100 100" overflow="visible">
  <rect x="0" y="0" width="100" height="100" stroke="midnightblue" stroke-width="3"/>
  <circle cx="90" cy="10" r="5" stroke="none" fill="blue" 
          data-vjs-source="true" data-vjs-port="source"/>
  <circle cx="10" cy="10" r="5" stroke="none" fill="orangered" 
          data-vjs-target="true" data-vjs-port="target"/>
</svg>

```

Now when you drag an edge between the circles, it remains on the circles:

**********

## Specifying anchors[​](#specifying-anchors "Direct link to Specifying anchors")

If you've got a setup like we discussed in the previous section - with your own source/target elements declared - you can also instruct VisuallyJs what anchor to use when connecting to some element. Anchors can be defined on multiple levels in VisuallyJs; many times it suffices to not specify them at all and just use the default `Continuous` anchor. But there are use cases where the placement and behaviour of the anchor is intrinsic to the shape. Being able to declare anchor types right inside the template can be very useful.

Let's define a new shape that is a circle within a circle. The outer ring will be our edge source, and the inner circle will be the target:

```html
<svg width="{{width}}" height="{{height}}" viewBox="0 0 100 100" overflow="visible">
  <circle cx="50" cy="50" r="40" stroke="none" fill="midnightblue" data-vjs-source="true"/>
  <circle cx="50" cy="50" fill="blue" r="25" data-vjs-target="true" />
</svg>

```

Drag and edge from one to the other - you'll see that it uses the default anchor, `Continuous`. You can drag another edge and you'll see the edges stack up on each shape:

**********

In this UI, though, I want to emphasise the circular nature of the shapes. I want to use a `Center` anchor for each one - and I can do that directly in the template:

```html
<svg width="{{width}}" height="{{height}}" viewBox="0 0 100 100" overflow="visible">
  <circle cx="50" cy="50" r="40" stroke="none" fill="midnightblue" data-vjs-source="true" 
          data-vjs-anchor="Center"/>
  <circle cx="50" cy="50" fill="blue" r="25" data-vjs-target="true" 
          data-vjs-anchor="Center" />
</svg>

```

**********

#### Anchor syntax[​](#anchor-syntax "Direct link to Anchor syntax")

Anchors in VisuallyJs all boil down to 4 essential pieces of information:

* `x` Where, as a proportion of width, the anchor is located on the x-axis
* `y` Where, as a proportion of height, the anchor is located on the y-axis
* `ox` In which x direction should a connection naturally travel from this anchor. Valid values are 1 (to the right), 0 (dont care) or -1 (to the left)
* `oy` In which y direction should a connection naturally travel from this anchor. Valid values are 1 (downwards), 0 (dont care) or -1 (upwards)

You can use [any named anchor](/angular/docs/diagrams/edges/anchors.md), but you can also specify custom values for `x`, `y`, `ox` and `oy`, via a comma-delimited string:

```html
<circle data-vjs-anchor="0,0.5,-1,0" data-vjs-source="true"/>

```

In this example, we have indicated our anchor is on the left edge, halfway down, and points to the left. This is in fact the same as saying `Left`. But with this syntax you can do things that aren't covered by one of the named anchors, for instance an anchor that sits in the center of some element but points to the left:

```html
<circle data-vjs-anchor="0.5,0.5,-1,0" data-vjs-source="true"/>

```

## Snapping to drag targets[​](#snapping-to-drag-targets "Direct link to Snapping to drag targets")

You can instruct VisuallyJs to snap to target shapes when dragging edges:

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
    snap: {
      enabled: true
    }
  }
}
}

```

Which you can see in operation here - try dragging an edge from one of the shapes. As it gets within proximity of one of the other nodes, the edge is snapped:

**********

### Adjusting sensitivity[​](#adjusting-sensitivity "Direct link to Adjusting sensitivity")

By default the snapping mechanism will kick in at a distance of 50 pixels from the target. You can change this:

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
    snap: {
      enabled: true,
      threshold: 20
    }
  }
}
}

```

Which you can see in operation here - try dragging an edge from one of the shapes. As it gets within 20px of one of the other nodes, the edge is snapped:

**********

## Constraining connectivity[​](#constraining-connectivity "Direct link to Constraining connectivity")

You can control whether or not a shape will display a link icon via the `canLink` mediator action:

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
  canLink: (vertex: Vertex, shape: Shape, el: HTMLElement) => {
      return vertex.type !== \pool\" && vertex.type !== \"lane\"
}"
}
}

```

Mediators are discussed in detail [on this page](/angular/docs/diagrams/controlling-diagram-actions.md#canlink)

## CSS Classes[​](#css-classes "Direct link to CSS Classes")

There are a number of CSS classes assigned to various parts of the UI during an edge drag. These can be used to easily add visual cues for your users, and also to manage z-index for the best user experience.

| Class                          | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `vjs-connector-source-drag`    | The class assigned to the SVG element with which a user can drag to reposition the source of some edge.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `vjs-connector-target-drag`    | The class assigned to the SVG element with which a user can drag to reposition the target of some edge.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `vjs-connector-transient-drag` | Assigned to the temporary DOM element used when relocating an existing edge via the mouse/touch events.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `vjs-edge-relocating`          | Assigned by the Surface to the DOM element representing an edge that is being dragged to relocate its source or target. This class is only added when the edge input handler is in drag mode. It is assigned to the connector element once the mouse starts to move, and removed on mouseup.                                                                                                                                                                                                                                                                                                |
| `vjs-edge-will-relocate`       | Assigned by the Surface to the DOM element representing an edge that is about to be relocated. When the edge input mode is dragging, this class is assigned on mousedown on one of the drag handles, before the mouse moves, and removed when the mouse begins to move (or on mouseup if the user does not move the mouse). When the edge input mode is tap, this class is assigned when the user has tapped on one of the relocate handles, and is removed either when the user clicks on whitespace, cancelling the relocation, or clicks on an active target and effects the relocation. |
| `vjs-surface-edge-dragging`    | Assigned by the Surface to its root element when an edge is being dragged. This is not assigned to the edge element itself.                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
