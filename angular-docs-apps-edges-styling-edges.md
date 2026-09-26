# Styling edges

There are a few approaches you can take when it comes to styling your edges - VisuallyJs provides an out of the box mapping from edge data to basic properties such as edge width, color etc, via the concept of [Simple edge styles](#simple-edge-styles). You can also [use CSS](#styling-with-css), or you can map a `PaintStyle` to your edges via a [view](#styling-with-paintstyles) or [in the UI defaults](#styling-with-ui-defaults). That's a lot of choice, so here we present a quick pros and cons for each option:

| Method                                    | Pros                                                                                                                                                             | Cons                                                                                                                                                            |
| ----------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [CSS](#styling-with-css)                  | Clean separation of presentation from code. Allows usage of various SVG CSS effects. Allows styling all edges of some type uniformly.                            | Does not support export to SVG, PNG or JPG. Does not support styling each edge individually. Does not support path outlines.                                    |
| [Paint styles](#styling-with-paintstyles) | Allows styling all edges of some **type** uniformly. Supports export to SVG. Supports path outlines.                                                             | Does not support styling each edge individually.                                                                                                                |
| [Simple edge styles](#simple-edge-styles) | Minimal setup. Allows each edge to be styled individually. Seamlessly integrated with update and undo/redo. Supports path outlines. Supports export to SVG.      | Each edge needs its own styles declared in the backing data. Limited set of configurable properties.                                                            |
| [UI Defaults](#styling-with-ui-defaults)  | Allows configuration of default styles value which will apply, in the absence of some other value, to all edges. Supports export to SVG. Supports path outlines. | Does not support styling each edge individually. Applies to all types (but you can override on a per-type basis via [Paint styles](#styling-with-paintstyles)). |

### Styling with CSS[​](#styling-with-css "Direct link to Styling with CSS")

Since VisuallyJs uses SVG to render edges, you can target the artifacts that VisuallyJs adds to the DOM via CSS. VisuallyJs uses a class of `vjs-connector` on the SVG element it uses for each edge, and the edge itself is written as one or more `path` elements inside of that, which each have a class according to their function:

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

### Styling with PaintStyles[​](#styling-with-paintstyles "Direct link to Styling with PaintStyles")

A `PaintStyle` is an object containing various properties to apply to a given type of edge. The definition is:

PaintStyle

Basic style definition for an edge

| Name           | Type                     | Description                                                               |
| -------------- | ------------------------ | ------------------------------------------------------------------------- |
| dashArray?     | string                   | Definition for stroke pattern                                             |
| fill?          | string                   | Fill color for the edge.                                                  |
| gradient?      | Array<\[number, string]> | Definition of a linear gradient to apply. Each entry is \[offset, color]. |
| outlineStroke? | string                   | Color for the outline path                                                |
| outlineWidth?  | number                   | Width of the outline path                                                 |
| stroke?        | string                   | Stroke color for the edge                                                 |
| strokeWidth?   | number                   | Width of the stroke                                                       |

All properties are optional; VisuallyJs will use an default value where properties are not specified. To setup an outline path, you must provide both `outlineStroke` *and* `outlineWidth`.

#### Mapping a PaintStyle in a view[​](#mapping-a-paintstyle-in-a-view "Direct link to Mapping a PaintStyle in a view")

You can map a `PaintStyle` to some specific edge type inside a view:

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [viewOptions]="viewOptions"></vjs-surface> `
})
export class AppComponent {
  viewOptions = {
  edges: {
    redWithOutline: {
      paintStyle: {
        stroke: "red",
        strokeWidth: 3
      }
    }
  }
};
}

```

#### Mapping a PaintStyle in the UI defaults[​](#mapping-a-paintstyle-in-the-ui-defaults "Direct link to Mapping a PaintStyle in the UI defaults")

You can also set a default paint style via the `defaults` for some surface:

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  defaults: {
    paintStyle: {
      stroke: "red",
      strokeWidth: 3
    }
  }
};
}

```

#### Controlling the hit zone[​](#controlling-the-hit-zone "Direct link to Controlling the hit zone")

By default, VisuallyJs paints a single `path` element for each edge. If you want your users to be able to interact with your edges but your edges have a stroke width of only a couple of pixels, this can be difficult. To manage this with a `paintStyles` we recommend using the `outlineWidth` and `outlineStroke` paint style properties to setup a hit zone:

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  defaults: {
    paintStyle: {
      stroke: "red",
      strokeWidth: 3,
      outlineStroke: "transparent",
      outlineWidth: 2
    }
  }
};
}

```

Calculating the outline width

When you provide `outlineWidth` and `outlineStroke` properties in a `PaintStyle`, the visible width of the outline is computed as:

`w = strokeWidth + (2 * outlineWidth)`

which is to say that the `outlineWidth` value you provide is applied to each side of the connector's path.

In this example we've used `"transparent"` for the outline color, which gives us the expanded hit zone without altering the appearance of each edge. You can, of course, use any color you like.

#### Hover styles[​](#hover-styles-1 "Direct link to Hover styles")

You can also provide a `hoverPaintStyle` property in your view, which VisuallyJs will use to paint the edge when the mouse is hovering over it:

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [viewOptions]="viewOptions"></vjs-surface> `
})
export class AppComponent {
  viewOptions = {
  edges: {
    redWithOutline: {
      paintStyle: {
        stroke: "red",
        strokeWidth: 3,
        outlineStroke: "orangered",
        outlineWidth: 2
      },
      hoverPaintStyle: {
        stroke: "green",
        strokeWidth: 3,
        outlineStroke: "yellowgreen",
        outlineWidth: 4
      }
    }
  }
};
}

```

### Simple edge styles[​](#simple-edge-styles "Direct link to Simple edge styles")

Simple edge styles allow you to map values from an edge's backing data to its appearance. The `LineStyle` interface defines the supported properties:

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

None of these properties are mandatory. VisuallyJs will fall back to its defaults for these via the `paintStyle` mechanism if your edge data does not contain any of these properties.

#### Example[​](#example "Direct link to Example")

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface #surfaceComponent></vjs-surface> `
})
export class AppComponent {
  @ViewChild('surfaceComponent') surfaceComponent: SurfaceComponent;

  ngAfterViewInit() {
    const surface = this.surfaceComponent.surface
    const model = surface.model
    
   model.load({
   type:"json",
   data:{
       nodes:[
           { id:"1" }, { id:"2" }
       ],
       edges:[
           {
               source:"1",
               target:"2",
               data:{
                   color:"cadetblue",
                   lineWidth:3,
                   outlineColor:"pink",
                   outlineWidth:5
               }
           }
       ]
   }
   })
  }
}

```

In this example the edge in our dataset will have a color of "cadetblue" and a stroke width of 3 pixels. It will also have an outline of 5 pixels each side, and the color of the outline will be pink. I think we can all agree it will look pretty fetching indeed.

We'll render an edge with this backing data:

```javascript
{
    color:"cadetblue",
    lineWidth:3,
    outlineColor:"pink",
    outlineWidth:5,
    id:"edge"  
}

```

(we gave it an `id` because we want to access it when you press a button in a moment; id is not a mandatory property).

If you now click this button, we'll set these new values, and you'll see the edge update:

```javascript

model.updateEdge("edge", {
    color:"black", 
    outlineColor:"yellow",
    lineWidth:2,
    outlineWidth:3,
    label:"New label"
})        
        

```

note

Simple edge styles are switched on by default. If you do not want this behaviour in your app, you can save yourself some CPU cycles by setting `simpleEdgeStyles:false` in your render options.

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

### Styling with UI Defaults[​](#styling-with-ui-defaults "Direct link to Styling with UI Defaults")

The UI `defaults` supports two keys that allow you to configure default paint styles for your edges:

#### Supported properties[​](#supported-properties "Direct link to Supported properties")

| Key               | Constant                        | Description                                                                                                                                                                                                      |
| ----------------- | ------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `paintStyle`      | `DEFAULT_KEY_PAINT_STYLE`       | A `PaintStyle` object as discussed above, whose values will be used for all edges unless a more specific type mapping is found in the view. Defaults to a stroke width of 2 pixels and a stroke color of `#456`. |
| `hoverPaintStyle` | `DEFAULT_KEY_HOVER_PAINT_STYLE` | A `PaintStyle` object as discussed above, whose values will be used for all edges when the mouse is hovering over it unless a more specific type mapping is found in the view. Defaults to null.                 |

#### Example[​](#example "Direct link to Example")

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  defaults: {
    paintStyle: {
      stroke: "red",
      strokeWidth: 3
    },
    hoverPaintStyle: {
      stroke: "orangered",
      strokeWidth: 5
    }
  }
};
}

```

#### Controlling the hit zone[​](#controlling-the-hit-zone-1 "Direct link to Controlling the hit zone")

VisuallyJs paints a single `path` element for each edge. It also paints an outline element behind each path, which, by default, extends to 10 pixels either side of the edge path, and has a transparent stroke. You can switch this mechanism off if you wish:

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  edges: {
    paintOutline: false
  }
};
}

```

You can also set the outline width and color:

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  edges: {
    outlineWidth: 20,
    outlineColor: "cadetblue"
  }
};
}

```

**********
