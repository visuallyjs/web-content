# Magnetizer

The magnetizer is a useful piece of VisuallyJs's UI functionality, providing a means to nudge elements around in your UI so that things don't overlap. There are a few different ways to use the magnetizer - you can instruct your layout to apply the magnetizer after the layout is run, or you can use it to manage element dragging. You can also call it programmatically on an ad-hoc basis.

## Layout magnetization[​](#layout-magnetization "Direct link to Layout magnetization")

All layouts support the option of switching on magnetization, which is invoked after the layout runs. For some layouts this ability is theoretically of no use, for instance the [Force directed layout](/vue/docs/apps/layouts/force-directed.md), because in that layout the elements in your UI have already been moved apart by the layout itself. But if you're using, for instance, the [Absolute layout](/vue/docs/apps/layouts/absolute.md), then there is a chance one or more elements are overlapping.

You can switch on magnetization in a layout by setting it as a layout option:

```html
<script setup>

import { AbsoluteLayout } from "@visuallyjs/browser-ui"

const renderOptions = {
  layout: {
    type: AbsoluteLayout.type,
    options: {
      magnetizer: true
    }
  }
}


</script>
<template>
  <SurfaceComponent :renderOptions="renderOptions" />
</template>

```

Each time the layout runs, the magnetizer will be run afterwards.

## Magnetizing after dragging[​](#magnetizing-after-dragging "Direct link to Magnetizing after dragging")

You can instruct the magnetizer to run after some vertex has been dragged:

```html
<script setup>

const renderOptions = {
  magnetizer: {
    afterDrag: true
  }
}


</script>
<template>
  <SurfaceComponent :renderOptions="renderOptions" />
</template>

```

Try dragging one element on top of another element in the canvas below. At the end of the drag the magnetizer will run. The element you just dragged will be the "focus", and will not move from where you placed it:

**********

#### Repositioning the dragged element[​](#repositioning-the-dragged-element "Direct link to Repositioning the dragged element")

As mentioned above, the dragged element will remain stationary if the magnetize is run after a drag. You can change that behaviour, though:

```html
<script setup>

const renderOptions = {
  magnetizer: {
    afterDrag: true,
    repositionDraggedElement: true
  }
}


</script>
<template>
  <SurfaceComponent :renderOptions="renderOptions" />
</template>

```

Try dragging one element on top of another element in the canvas below. At the end of the drag the magnetizer will run, but this time the dragged element will be the one that is moved if there is any overlap:

**********

## Magnetizing while dragging[​](#magnetizing-while-dragging "Direct link to Magnetizing while dragging")

You can run the magnetizer while dragging an element by using the `constant` flag:

```html
<script setup>

const renderOptions = {
  magnetizer: {
    constant: true
  }
}


</script>
<template>
  <SurfaceComponent :renderOptions="renderOptions" />
</template>

```

Try dragging node 1 through the gap between nodes 2 and 3 in this canvas - they'll move out of the way as node 1 moves through, and then spring back. Once you release the mouse button, the position of each node is fixed.

**********

The vertices spring back to their original position in the canvas above because when you switch on `constant` mode, the UI automatically also switches on `trackback`. You can switch off trackback if you wish - see the section [below](#trackback).

tip

If you have `trackback` switched on, your users can switch if off temporarily while dragging by holding down the `shift` key.

## Trackback[​](#trackback "Direct link to Trackback")

To switch off trackback:

```html
<script setup>

const renderOptions = {
  magnetizer: {
    constant: true,
    trackback: false
  }
}


</script>
<template>
  <SurfaceComponent :renderOptions="renderOptions" />
</template>

```

Try dragging node 1 through the gap between nodes 2 and 3 in this canvas - they'll move out of the way as node 1 moves through, but this time they won't spring back:

**********

tip

If you have switched off `trackback` your users can still switch it on temporarily, by holding down the `shift` key while dragging.

## Adhoc magnetization[​](#adhoc-magnetization "Direct link to Adhoc magnetization")

You can instruct the Surface widget to run the magnetizer over the entire contents of the UI at any time via the `magnetize` method:

#### magnetize[​](#magnetize "Direct link to magnetize")

Magnetize the elements in the display. If `focus` is provided it will be used as the origin for magnetization,

<br />

and not moved (unless `repositionFocus` is true). If no `focus` is provided, the computed center of all the

<br />

elements will be used as the origin.

Signature

magnetize(focus:string | [Vertex](), repositionFocus:boolean)

Parameters

|                 |                      |   |
| --------------- | -------------------- | - |
| focus           | string \| [Vertex]() |   |
| repositionFocus | boolean              |   |

Return value

void

By default, the magnetizer will use the computed center of all the elements as its origin, and all elements will be pushed away from that point, as in this call:

```javascript
surface.magnetize()

```

An alternative, though, is to supply a vertex that you wish to act as the origin, and which you do not wish to move:

```javascript
surface.magnetize("nodeId")

```

Here we passed the ID of some node, but we could also have passed the node itself. The signature of the `magnetize` method is:

```text
magnetize(focus?:string|Vertex):void

```

## Setting a vertex position and magnetizing[​](#setting-a-vertex-position-and-magnetizing "Direct link to Setting a vertex position and magnetizing")

Another feature the Surface offers is the ability to set the position of some element and to immediately magnetize the UI after setting the element's position, using that element as the focus:

```javascript
setMagnetizedPosition(element:string|Vertex, x:number, y:number):void

```

This is effectively the same as:

```javascript
surface.setPosition(element, x, y)
surface.magnetize(element)

```

This operation is wrapped in a transaction on the model so if undo is called then every element affected by the magnetize is relocated to its original position.

## Gathering Elements[​](#gathering-elements "Direct link to Gathering Elements")

The magnetizer can also gather elements to bring them closer together around some origin. Internally this works by pulling each affected element in on its radial from the origin to the element's center, and then running the magnetizer to nudge everything back out so that nothing overlaps.

```text
gather(focus?:string|Vertex):void

```

To gather all the elements in the UI around their computed center, don't supply a focus element:

```text
surface.gather()

```

To gather all the elements in the UI around some focus element:

```text
surface.gather(idOrVertex)

```

This code sets up a surface so that when you click on one of the nodes, the other nodes in the surface are gathered around it:

```html
<script setup>

const renderOptions = {
  zoomToFit: true
}
function viewOptions() {
  return {
  nodes: {
    default: {
      events: {
        tap: (p) => {
            p.ui.gather(p.obj)
        }
      }
    }
  }
}
    }

</script>
<template>
  <SurfaceComponent :renderOptions="renderOptions"  :viewOptions="viewOptions()" />
</template>

```

Try clicking one of the nodes in the canvas below. You'll see the other two nodes are gathered in to it. Note that nodes are gathered along a path from the current location to the focus node, and so other nodes may still obstruct their travel. A good example of that is if you click node 1: node 2 is pulled in close to node 1, but node 3 can only travel until it is blocked by node 2.

**********

## All options[​](#all-options "Direct link to All options")

The Surface offers many options for configuring the magnetizer. The full list is:

MagnetizeOptions

Options for the magnetize functionality of the UI.

| Name                      | Type        | Description                                                                                                                                                                                                                                                                                                                                                    |
| ------------------------- | ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| afterDrag?                | boolean     | If true, magnetizer will be run after a vertex is dragged. Defaults to false.                                                                                                                                                                                                                                                                                  |
| afterGroupCollapse?       | boolean     | Defaults to false. Indicates the UI should gather nodes around a newly collapsed group                                                                                                                                                                                                                                                                         |
| afterGroupExpand?         | boolean     | Defaults to false. Indicates the UI should magnetize nodes around a newly expanded group                                                                                                                                                                                                                                                                       |
| afterGroupGrow?           | boolean     | Defaults to false. Indicates the UI should magnetize/gather nodes around a newly resized group if the group size was enlarged.                                                                                                                                                                                                                                 |
| afterGroupResize?         | boolean     | Defaults to false. Indicates the surface should magnetize/gather nodes around a newly resized group, regardless of whether the group size grew or if it shrunk. This flag is the same as setting `afterGroupShrink` and `afterGroupGrow`                                                                                                                       |
| afterGroupShrink?         | boolean     | Defaults to false. Indicates the UI should magnetize/gather nodes around a newly resized group if the group size was reduced.                                                                                                                                                                                                                                  |
| afterLayout?              | boolean     | If true, magnetizer will be run after the layout is run.                                                                                                                                                                                                                                                                                                       |
| constant?                 | boolean     | If true, magnetizer will be run constantly as a vertex is being dragged, pushing other vertices out of the way of the vertex that is being dragged. Defaults to false. By default, `constant` magnetize will also set `trackback:true`, but you can disable that behaviour by setting `trackback:false`.                                                       |
| constrainToViewport?      | boolean     | If true, vertices moved by the magnetizer will be constrained to move within the visible viewport, which is a function of the current zoom/pan of the UI. Otherwise, vertices will be able to be pushed out of the visible viewport.                                                                                                                           |
| padding?                  | [PointXY]() | How much padding to leave between elements. Defaults to 100 pixels in each axis.                                                                                                                                                                                                                                                                               |
| repositionDraggedElement? | boolean     | If true, and `afterDrag` is true, when the magnetizer is run after a drag it will be the recently dragged element that moves in precedence to the other elements. By default, the recently dragged element is *not* moved by the magnetize operation - it stays where you dragged it.                                                                          |
| trackback?                | boolean     | Used in conjunction with `constant`: attempts to track any moved elements to their original positions (or as close as possible) once the path is clear, each time the magnetizer runs a sweep. Defaults to true (when `constant` is true).                                                                                                                     |
| trackbackThreshold?       | number      | When in `constant` mode and `trackback` is set, this value specifies a threshold for elements that have been pushed from their original position. Beyond this threshold, the magnetizer will no longer attempt to track an element back. This can be useful in certain situations where the user does want to move an element by pushing it via the magnetizer |
