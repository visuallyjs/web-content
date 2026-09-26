# Styling edges

There are a few approaches you can take when it comes to styling your edges - VisuallyJs provides an out of the box mapping from edge data to basic properties such as edge width, color etc, via the concept of [Simple edge styles](#simple-edge-styles). You can also [use CSS](#styling-with-css), or you can map a `PaintStyle` to your edges via a [view](#styling-with-paintstyles) or [in the UI defaults](#styling-with-ui-defaults). That's a lot of choice, so here we present a quick pros and cons for each option:

| Method                                | Pros                                                                                                                                                             | Cons                                                                                                                                              |
| ------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Diagram defaults](#diagram-defaults) | Allows configuration of default styles value which will apply, in the absence of some other value, to all edges. Supports export to SVG. Supports path outlines. | Does not support styling each edge individually. Applies to all types (but you can override on a per-type basis via [Edge styles](#edge-styles)). |
| [Edge styles](#edge-styles)           | Minimal setup. Allows each edge to be styled individually. Seamlessly integrated with update and undo/redo. Supports path outlines. Supports export to SVG.      | Each edge needs its own styles declared in the backing data. Limited set of configurable properties.                                              |
| [CSS](#styling-with-css)              | Clean separation of presentation from code. Allows usage of various SVG CSS effects. Supports path outlines. Allows styling all edges of some type uniformly.    | Does not support export to SVG, PNG or JPG. Does not support styling each edge individually.                                                      |

### Diagram Defaults[​](#diagram-defaults "Direct link to Diagram Defaults")

To provide default values for edges, you can provide a `lineStyle` property in the `edges` section of your diagram config:

```html
<script>

import { DiagramComponent } from "@visuallyjs/browser-ui-svelte"
    
const data = ...
    
const options = {
  edges: {
    lineStyle: {
      color: "#0000FF",
      lineWidth: 5
    }
  }
}
    
</script>    

<div class="my-container">
    <DiagramComponent data={data} options={options}/>
</div>

```

**********

This `lineStyle` is expected to conform to the `LineStyle` interface:

LineStyle

Defines the simple properties for an edge style.

| Name           | Type                     | Description                                                                                                  |
| -------------- | ------------------------ | ------------------------------------------------------------------------------------------------------------ |
| color?         | string                   | Color to paint the edge's path                                                                               |
| dashArray?     | string                   | Definition of dash pattern to use to draw the edge path                                                      |
| fontFamily?    | string                   | Font size to use; defaults to whatever the browser decides given the context                                 |
| fontSize?      | number                   | Font size to use; defaults to whatever the browser decides given the context                                 |
| fontStyle?     | [FontStyle]()            | Font style to use; defaults to whatever the browser decides given the context                                |
| gradient?      | Array<\[number, string]> | An array of color stops to use as a linear gradient for the edge path. When this is set, `color` is ignored. |
| label?         | string                   | Label to show on the edge                                                                                    |
| labelLocation? | number                   | Location for the label, defaults to 0.5                                                                      |
| lineWidth?     | number                   | Width of the edge path                                                                                       |
| outlineColor?  | string                   | Color to paint the edge's outline path                                                                       |
| outlineWidth?  | number                   | Width to draw the edge's outline path                                                                        |

#### Controlling the hit zone[​](#controlling-the-hit-zone "Direct link to Controlling the hit zone")

For each edge, VisuallyJs paints an SVG path to represent the edge itself, and another path behind it, with a wider stroke width and a transparent stroke. This background path facilitates selection of an edge via a pointer device. If you wish to change the width/color of the outline path, you can do so in the `lineStyle`:

```html
<script>

import { DiagramComponent } from "@visuallyjs/browser-ui-svelte"
    
const data = ...
    
const options = {
  edges: {
    lineStyle: {
      color: "#0000FF",
      outlineColor: "#FF0000",
      outlineWidth: 20
    }
  }
}
    
</script>    

<div class="my-container">
    <DiagramComponent data={data} options={options}/>
</div>

```

Calculating the outline width

When you provide `outlineWidth` and `outlineColor` value, the visible width of the outline is computed as:

`w = lineWidth + (2 * outlineWidth)`

which is to say that the `outlineWidth` value you provide is applied to each side of the connector's path.

**********

### Edge styles[​](#edge-styles "Direct link to Edge styles")

Edge styles allow you to map values from an edge's backing data to its appearance. As with the diagram defaults discussed above, the [LineStyle]() interface defines the supported properties.

None of these properties are mandatory. VisuallyJs will fall back to its defaults if your edge data does not contain any of these properties.

#### Example[​](#example "Direct link to Example")

We setup a diagram with just the defaults:

```html
<script>

import { DiagramComponent } from "@visuallyjs/browser-ui-svelte"
    
const data = ...
    
const options = {}
    
</script>    

<div class="my-container">
    <DiagramComponent data={data} options={options}/>
</div>

```

In this example the edge in our dataset will have a color of "cadetblue" and a stroke width of 3 pixels. It will also have an outline of 5 pixels each side, and the color of the outline will be pink. I think we can all agree it will look pretty fetching indeed.

We'll render an edge with this backing data:

```javascript
{
    color:"cadetblue",
    lineWidth:3,
    outlineColor:"pink",
    outlineWidth:5,
    label:"Initial label",
    labelLocation:0.25,
    fontSize:25,
}

```

If you now click this button, we'll set these new values, and you'll see the edge update:

```javascript

diagram.model.updateEdge("edge", {
    color:"black", 
    outlineColor:"yellow",
    lineWidth:2,
    outlineWidth:3,
    label:"New label"
})        
        

```

#### Gradient Example[​](#gradient-example "Direct link to Gradient Example")

<!-- -->

In this example the edge in our dataset will have a stroke width of 5 pixels, and will be painted with a linear gradient from "lightblue" to "forestgreen".

Let's render that example from above. We'll render an edge with this backing data:

```javascript
{
    gradient:[[0,"lightblue"],[100, "forestgreen"]],
    lineWidth:5
}

```

**********

### Styling with CSS[​](#styling-with-css "Direct link to Styling with CSS")

Since VisuallyJs uses SVG to render edges, you can target the artifacts that VisuallyJs adds to the DOM via CSS. VisuallyJs uses a class of `vjs-connector` on the SVG element it uses for each edge, and the edge itself is written as one or more `path` elements inside of that, which each have a class according to their function.

caution

Edges styled with CSS will not look the same in SVG/PNG/JPG output as they do in the browser. If you are offering export, you should restrict the use of CSS to style edges in a diagram to "runtime" concerns - things that are transient to the operation of the UI (such as hover states). If you are not offering your users the export to SVG/PNG/JPG functionality, then this is probably not a concern for you.

```html
<svg class="vjs-connector">
  <path d="..." class="vjs-connector-outline"></path>
  <path d="..." class="vjs-connector-path"></path>
</svg>

```

#### Targeting the edge's SVG element[​](#targeting-the-edges-svg-element "Direct link to Targeting the edge's SVG element")

To target the parent element for some path, for instance to assign `z-index`, you need a rule like this:

```css
.vjs-connector {
    z-index:50;
}

```

#### Targeting the SVG path[​](#targeting-the-svg-path "Direct link to Targeting the SVG path")

To target the element used to render the path, you need a rule like this:

```css
.vjs-connector-path {
    stroke-width:2;
    stroke:cadetblue;
    stroke-dasharray: 2;
}

```

#### Hover styles[​](#hover-styles "Direct link to Hover styles")

To change the appearance of an edge on hover, use the `:hover` css meta class:

```css
.vjs-connector-path:hover {
    stroke:orangered;
}

```

Note that the above example targets the path element on hover, but you can also target the parent SVG element of course:

```css
.vjs-connector:hover {
    outline:1px solid orangered;
}

```

#### Marching ants effect[​](#marching-ants-effect "Direct link to Marching ants effect")

It's simple to get this 'marching ants' effect via CSS with VisuallyJs:

##### 1. Define the CSS animation[​](#1-define-the-css-animation "Direct link to 1. Define the CSS animation")

Define a CSS animation with a single keyframe that sets the dash offset:

```css
@keyframes dashdraw {
    0% {
        stroke-dashoffset:10;
    }
}

```

##### 2. Map the animation to a CSS rule[​](#2-map-the-animation-to-a-css-rule "Direct link to 2. Map the animation to a CSS rule")

```css
.animated-edge {
    stroke-dasharray:5;
    animation: dashdraw .5s linear infinite;
}

```

##### 3. Use the cssClass property in an edge definition to map to this class (optional)[​](#3-use-the-cssclass-property-in-an-edge-definition-to-map-to-this-class-optional "Direct link to 3. Use the cssClass property in an edge definition to map to this class (optional)")

<!-- -->

We said that (3) is optional because if you just want to apply it to every edge in your dataset you can change the CSS rule shown in (2) to target every edge:

```css
.vjs-connector-path {
    stroke-dasharray:5;
    animation: dashdraw .5s linear infinite;
}

```

#### Selected edges[​](#selected-edges "Direct link to Selected edges")

When an edge is in the model's current selection, it has the CSS class `vjs-selected-connection` applied to it. You can target this class to change the appearance of either the connector's parent element:

```css
.vjs-selected-connection {
    outline:2px solid orangered;
}

```

or the path element representing the edge:

```css
.vjs-selected-connection .vjs-connector-path {
    stroke:orangered;
}

```

#### Controlling the hit zone[​](#controlling-the-hit-zone-1 "Direct link to Controlling the hit zone")

By default, VisuallyJs paints a single `path` element for each edge. If you want your users to be able to interact with your edges but your edges have a stroke width of only a couple of pixels, this can be difficult. To manage this with a `paintStyles` we recommend using the `outlineWidth` and `outlineStroke` paint style properties to setup a hit zone:

```html
<script>
  import { SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
  const renderOptions = {
  defaults: {
    paintStyle: {
      stroke: "red",
      strokeWidth: 3,
      outlineStroke: "transparent",
      outlineWidth: 2
    }
  }
}
</script>

<SurfaceComponent {renderOptions}/>

```

In this example we've used `"transparent"` for the outline color, which gives us the expanded hit zone without altering the appearance of each edge. You can, of course, use any color you like.
