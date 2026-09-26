# Overlays

Overlays are adornments to connections. There are two types - simple overlays, which are such things as arrows at the end of a line, or a label, etc, and component overlays, in which you can provide a component to use for the overlay.

<!-- -->

In this canvas we have an edge with 6 [simple overlays](#simple-overlays) - a [Rectangle](#rectangle), a [PlainArrow](#plainarrow), a [Label](#label), a [Diamond](#diamond), a [Dot](#dot), and an [Arrow](#arrow):

**********

info

## Location[​](#location "Direct link to Location")

A key concept with overlays is that of their **location**. It refers to some point along the path inscribed by the edge, and it can be specified in one of three ways:

* as a decimal in the range \[0..1], which indicates some proportional amount of travel along the path inscribed by the edge. The default value of 0.5 is in this form, and it means the default location of an overlay on an edge is a point halfway along the path.
* as an integer greater than 1, which indicates some absolute number of pixels to travel along the edge from the start point
* as an integer less than zero, which indicates some absolute number of pixels to travel backwards along the edge from the end point.

The default location for an overlay is halfway along the path traveled by the connector - `location` is `0.5`. If you specify `location:1`, then the overlay will be at the end of the path; `location:0` puts the overlay at the start.

## Simple Overlays[​](#simple-overlays "Direct link to Simple Overlays")

VisuallyJs ships with several types of simple overlays:

* **Arrow** - a configurable arrow that is painted at some point along the connector. You can control the length and width of the Arrow, the 'foldback' point - a point the tail points fold back into, and the direction (allowed values are 1 and -1; 1 is the default and means point in the direction of the connection)
* **Label** - a configurable label that is painted at some point along the connector, either as an SVG element or an HTML element
* **PlainArrow** - an Arrow shaped as a triangle, with no foldback.
* **Diamond** - A diamond shaped overlay.
* **Dot** A circle overlay, with configurable radius
* **Rectangle** A rectangle overlay, with configurable width and height
* **Custom** - allows you to create the overlay yourself - your overlay may be any DOM element you like.

`PlainArrow` and `Diamond` are actually just configured instances of the generic `Arrow` overlay (see examples).

### Arrow[​](#arrow "Direct link to Arrow")

An arrow with a configurable `foldback` point, which is specified as a fraction of the arrow's length. The default value is 0.62.

```javascript
{
  "type": "Arrow",
  "options": {
    "location": 1
  }
}

```

**********

ArrowOverlayOptions

Options for an Arrow overlay.

| Name        | Type                                                    | Description                                                                                                    |
| ----------- | ------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| attributes? | Record\<string,string>                                  | Optional custom attributes to write to the overlay's element.                                                  |
| cssClass?   | string                                                  | Optional CSS class(es) to add to the overlay's element.                                                        |
| direction?  | number                                                  | 1 to point forwards (the default), -1 to point backwards. Only taken into consideration in some overlay types. |
| events?     | Record<[OverlayEvents](),(value:any, event:any) => any> | Optional event handlers to attach to the overlay.                                                              |
| foldback?   | number                                                  | How far, as a decimal, along the line from head to baseline to fold back into. Defaults to 0.623.              |
| hollow?     | boolean                                                 | Defaults to false. When true, the arrow is stroked but not filled.                                             |
| id?         | string                                                  | Optional ID for the overlay. Can be used to retrieve the overlay from a connection.                            |
| length?     | number                                                  | Length from the head to the baseline. Defaults to 20.                                                          |
| location?   | number                                                  | Defaults to 0.5. See docs.                                                                                     |
| paintStyle? | [PaintStyle]()                                          | Optional paint style to use.                                                                                   |
| visibility? | [OverlayVisibility]()                                   | Whether the overlay is always visible, or only on hover. Defaults to OVERLAY\_VISIBILITY\_ALWAYS.              |
| width?      | number                                                  | Width of the arrow's baseline. Defaults to 20.                                                                 |

#### Arrow direction[​](#arrow-direction "Direct link to Arrow direction")

A point to note is that `location:0` for arrow overlays will not reverse the direction in which the arrow is pointing. To have the arrow point backwards along the path you have to provide a value for `direction`:

```javascript
overlays:[    
    {
        type:"Arrow",
        options:{
            width:10,
            length:15,
            location:0,
            direction:-1
        }
    }   
]

```

The `direction:-1` here instructs VisuallyJs to draw the arrow painting backwards. There are only two valid values for `direction` - `1` and `-1`. If you provide any other value - or no value - then VisuallyJs will use a value of 1, meaning the arrow points forwards.

### PlainArrow[​](#plainarrow "Direct link to PlainArrow")

This overlay is an extension of `Arrow` with the `foldback` parameter's value fixed to `1`. This results in an arrow with a flat back.

```javascript
{
  "type": "PlainArrow",
  "options": {
    "location": 0.25
  }
}

```

**********

### Diamond[​](#diamond "Direct link to Diamond")

This overlay is an extension of `Arrow` with the `foldback` parameter's value fixed to `2`. This results in an arrow shaped like a diamond.

```javascript
{
  "type": "Diamond",
  "options": {
    "location": 0.75
  }
}

```

**********

### Dot[​](#dot "Direct link to Dot")

This is a circle, with configurable radius.

```javascript
{
  "type": "Dot",
  "options": {
    "location": 0.85
  }
}

```

**********

DotOverlayOptions

Options for a Dot overlay

| Name        | Type                                                    | Description                                                                                                                                                                                                                                                                                                                     |
| ----------- | ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| align?      | "center" \| "flush"                                     | When the overlay is at position 1 or 0 (or is being used a source/target marker), this determines how the dot intersects the vertex. A value of 'flush', which is the default, means a point on the circumference of the dot touches the vertex boundary. A value of 'center' means the dot's center is on the vertex boundary. |
| attributes? | Record\<string,string>                                  | Optional custom attributes to write to the overlay's element.                                                                                                                                                                                                                                                                   |
| cssClass?   | string                                                  | Optional CSS class(es) to add to the overlay's element.                                                                                                                                                                                                                                                                         |
| direction?  | number                                                  | 1 to point forwards (the default), -1 to point backwards. Only taken into consideration in some overlay types.                                                                                                                                                                                                                  |
| events?     | Record<[OverlayEvents](),(value:any, event:any) => any> | Optional event handlers to attach to the overlay.                                                                                                                                                                                                                                                                               |
| hollow?     | boolean                                                 | Defaults to false. When true, the arrow is stroked but not filled.                                                                                                                                                                                                                                                              |
| id?         | string                                                  | Optional ID for the overlay. Can be used to retrieve the overlay from a connection.                                                                                                                                                                                                                                             |
| location?   | number                                                  | Defaults to 0.5. See docs.                                                                                                                                                                                                                                                                                                      |
| paintStyle? | [PaintStyle]()                                          | Optional paint style to use.                                                                                                                                                                                                                                                                                                    |
| radius?     | number                                                  | Radius of the dot. Defaults to 5.                                                                                                                                                                                                                                                                                               |
| visibility? | [OverlayVisibility]()                                   | Whether the overlay is always visible, or only on hover. Defaults to OVERLAY\_VISIBILITY\_ALWAYS.                                                                                                                                                                                                                               |

### Rectangle[​](#rectangle "Direct link to Rectangle")

This is a rectangle, with configurable width and height.

```javascript
{
  "type": "Rectangle",
  "options": {
    "location": 0.15
  }
}

```

**********

RectangleOverlayOptions

Options for a Rectangle overlay

| Name        | Type                                                    | Description                                                                                                                                                                                                                                                                                                                                  |
| ----------- | ------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| align?      | "center" \| "flush"                                     | When the overlay is at position 1 or 0 (or is being used a source/target marker), this determines how the rectangle intersects the vertex. A value of 'flush', which is the default, means a point on the boundary of the rectangle touches the vertex boundary. A value of 'center' means the rectangle's center is on the vertex boundary. |
| attributes? | Record\<string,string>                                  | Optional custom attributes to write to the overlay's element.                                                                                                                                                                                                                                                                                |
| cssClass?   | string                                                  | Optional CSS class(es) to add to the overlay's element.                                                                                                                                                                                                                                                                                      |
| direction?  | number                                                  | 1 to point forwards (the default), -1 to point backwards. Only taken into consideration in some overlay types.                                                                                                                                                                                                                               |
| events?     | Record<[OverlayEvents](),(value:any, event:any) => any> | Optional event handlers to attach to the overlay.                                                                                                                                                                                                                                                                                            |
| height?     | number                                                  | Height of the rectangle. Defaults to 10.                                                                                                                                                                                                                                                                                                     |
| hollow?     | boolean                                                 | Defaults to false. When true, the arrow is stroked but not filled.                                                                                                                                                                                                                                                                           |
| id?         | string                                                  | Optional ID for the overlay. Can be used to retrieve the overlay from a connection.                                                                                                                                                                                                                                                          |
| location?   | number                                                  | Defaults to 0.5. See docs.                                                                                                                                                                                                                                                                                                                   |
| paintStyle? | [PaintStyle]()                                          | Optional paint style to use.                                                                                                                                                                                                                                                                                                                 |
| rotate?     | boolean                                                 | Whether or not to rotate the rectangle so that it is always perpendicular to the connector path. Defaults to false.                                                                                                                                                                                                                          |
| visibility? | [OverlayVisibility]()                                   | Whether the overlay is always visible, or only on hover. Defaults to OVERLAY\_VISIBILITY\_ALWAYS.                                                                                                                                                                                                                                            |
| width?      | number                                                  | Width of the rectangle. Defaults to 10.                                                                                                                                                                                                                                                                                                      |

### Label[​](#label "Direct link to Label")

```javascript
{
  "type": "Label",
  "options": {
    "label": "Label"
  }
}

```

**********

By default, label overlays will be drawn horizontally, and they wont track the slope of the connector. You can mark a label as `rotatable` if you want it to track the slope of the connector:

```javascript
{
  "type": "Label",
  "options": {
    "label": "Label",
    "rotatable": true
  }
}

```

**********

LabelOverlayOptions

Options for a label overlay

| Name                    | Type                                                    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ----------------------- | ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| attributes?             | Record\<string,string>                                  | Optional custom attributes to write to the overlay's element.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| backgroundStyle?        | [LabelBackgroundStyle]()                                | Optional style for the label's background.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| cssClass?               | string                                                  | Optional CSS class(es) to add to the overlay's element.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| direction?              | number                                                  | 1 to point forwards (the default), -1 to point backwards. Only taken into consideration in some overlay types.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| events?                 | Record<[OverlayEvents](),(value:any, event:any) => any> | Optional event handlers to attach to the overlay.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| font?                   | [FontSpec]()                                            | Optional spec for the font to use on this label.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| id?                     | string                                                  | Optional ID for the overlay. Can be used to retrieve the overlay from a connection.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| label                   | string \| Function                                      | String, or a function returning a string, for the label.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| labelLocationAttribute? | string                                                  | Optional name of the attribute that identifies this overlay's location on the path. Defaults to `location`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| location?               | number                                                  | Defaults to 0.5. See docs.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| rotatable?              | boolean \| "strict" \| "legible"                        | Sets whether the label can be rotated to match the gradient of the connector at that location at which it is positioned. If you supply boolean true here, the label will be made rotatable, in "legible" mode - in which VisuallyJs ensures that the label is legible by avoiding rotating the text so that it is upside down or otherwise awkward to read. You can set "strict" mode, which will rotate the label to the appropriate angle regardless of whether or not it will make the label difficult to read. If you supply boolean false, the label will not be rotatable in any situation. |
| useHTMLElement?         | boolean                                                 | Whether or not to use an HTML element. Defaults to false (uses an SVG element)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| visibility?             | [OverlayVisibility]()                                   | Whether the overlay is always visible, or only on hover. Defaults to OVERLAY\_VISIBILITY\_ALWAYS.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |

The `label` for a label overlay can be a string or a function, but in practice with VisuallyJs you'll generally be defining labels as strings, as the values presented to the renderer are extracted from the JSON backing data for each edge.

#### SVG vs HTML elements[​](#svg-vs-html-elements "Direct link to SVG vs HTML elements")

By default, regardless of whether or not the container is an SVG element, a label overlay will be rendered as an SVG element. This is the most memory efficient and also allows a label to be printed by an SVG exporter. You can instruct VisuallyJs to use an HTML element via the `useHTMLElement` option for the label.

### Custom[​](#custom "Direct link to Custom")

The custom overlay allows you to create your own overlays, which VisuallyJs will position for you. You need to implement the `create` method, which is passed the connection on which the overlay is located as an argument, as well as its associated edge, the ui instance, and the underlying model, and which returns a DOM element:

```javascript

  overlays:[
    {
        type:"Custom",
        options:{
          create:(connection:Connection, edge:Edge, ui:BrowserUI, model:VisuallyJsModel) => {
              const d = document.createElement("select")
              d.innerHTML = "<option value='foo'>foo</option><option value='bar'>bar</option>"
              return d
          },
          location:0.7
        }
    }
  ]

```

Here we have created a select box with a couple of values, assigned to it the id of 'customOverlay' and placed it at location 0.7.

**********

#### Interacting with the model[​](#interacting-with-the-model "Direct link to Interacting with the model")

Since the `create` method is passed in the full context in which the edge is being rendered, you can respond to events in your overlay and update the model accordingly. Lets create a factory method to generate custom overlays, which takes a `vertex` and `location` as argument:

```typescript
function customFactory(vertex:"source"|"target", location:number) {
    return {
        create:(c:Connection, edge:Edge, ui:BrowserUI, model:VisuallyJsModel) => {
            const d = document.createElement("select")
            d.innerHTML = "<option value='#452385'>#452385</option><option value='#2387F5'>#2387F5</option>"
            d.addEventListener("change", (e) => {
                const value = d.options[d.selectedIndex].value
                model.updateNode(edge[vertex], {bg:value})
            })
            return d
        },
        location
    }
}

```

This overlay provides a select with a list of colors. We'll use this twice in our edge mapping:

```javascript
overlays:[
    {
        type:"Custom",
        options:customFactory("source", 0.3)
    },
    {
        type:"Custom",
        options:customFactory("target", 0.7)
    }
]

```

And we get this. Our `create` method adds a change event listener to the select box, which updates the appropriate vertex in the model when you select a new color<!-- -->:s

**********

#### Rotating custom overlays[​](#rotating-custom-overlays "Direct link to Rotating custom overlays")

As with label overlays, custom overlays will, by default, be drawn in their normal orientation, without taking account the slope of the connector line at the position at which they are located. You can set the `rotatable` flag on the custom overlay options to change that:

**********

tip

A custom overlay is a plain HTML element, and although you can attach model interactivity, as shown above, you may wish to consider using a component overlay instead.

## Showing/hiding on hover[​](#showinghiding-on-hover "Direct link to Showing/hiding on hover")

It is possible to mark some overlay as being only visible when the mouse is hovering over the edge to which it belongs:

<!-- -->

```html
<script setup>
import { OVERLAY_VISIBILITY_HOVER } from "@visuallyjs/browser-ui"

const options = {
  edges: {
    overlays: [
      {
        type: "Label",
        options: {
          label: "Hello!",
          visibility: OVERLAY_VISIBILITY_HOVER
        }
      }
    ],
    paintOutline: true,
    outlineWidth: 30
  }
}
const data = ...
</script>
<template>
  <div class="my-container">
    <DiagramComponent :data="data" :options="options"></DiagramComponent>
  </div>        
</template>

```

Try hovering the mouse over the edge path in this example:

**********

<!-- -->

info

In this example we made it easy to hover over the edge by instructing VisuallyJs to paint a 30 pixel transparent connector outline, via the `outlineWidth:30` config.

## Vue component overlays[​](#vue-component-overlays "Direct link to Vue component overlays")

VisuallyJs supports using Vue components as overlays - you need to create a component that takes props of type `VueWrapperProps<Edge>`, and then you have access - reactively - to the edge, and its source and target. You also have access to the underlying `model` and `ui`:

### VueComponentOverlay.vue[​](#vuecomponentoverlayvue "Direct link to VueComponentOverlay.vue")

```html
<script setup lang="ts">
import { Edge } from "@visuallyjs/browser-ui";
import { VueWrapperProps } from "@visuallyjs/browser-ui-vue";
import { defineProps} from "vue";

const {edge, overlay, model, ui} = defineProps<VueWrapperProps<Edge>();
</script>

<template>
  <div style="background: white; border: 1px solid #ccc; padding: 2px 5px; border-radius: 4px; font-size: 10px; pointer-events: all;">
    Vue Overlay from {{edge.source.id}}
  </div>
</template>


```

#### AppComponent.vue[​](#appcomponentvue "Direct link to AppComponent.vue")

```html
<script setup>

function viewOptions() {
  return {
  edges: {
    default: {
      overlays: [
        {
          component: VueComponentOverlay,
          options: {
            location: 0.5
          }
        }
      ]
    }
  }
}
    }

</script>
<template>
  <SurfaceComponent :viewOptions="viewOptions()" />
</template>

```

VueWrapperProps

The props that are passed in to a component used to render a node/group by a surface or paper component.

| Name   | Type               | Description                                       |
| ------ | ------------------ | ------------------------------------------------- |
| data   | [ObjectData]()     | Data that backs the object. Reactive.             |
| def    | any                | Definition for this node/group type               |
| el     | [BrowserElement]() | The underlying DOM element                        |
| model  | [BrowserUIModel]() | Underlying model.                                 |
| obj    | T                  | The vertex (node or group) that is being rendered |
| ui     | [BrowserUI]()      | Underlying UI                                     |
| vertex | T                  | The vertex (node or group) that is being rendered |
