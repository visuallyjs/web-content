# SVG Shape

This component renders an SVG shape from a `ShapeLibrary`. It can be used inside your own Angular components if you've configured your surface to use SVG shapes.

If you're building an SVG diagram in which the shapes are the entire node contents, you may want to look at the [DiagramComponent](/angular/docs/reference/DiagramComponent.md).

## Usage[​](#usage "Direct link to Usage")

This component is used inside a component that represents some node (or group) in your app. For example, here we use one in the template for a component we're using to render each node, which we pass in to a `SurfaceComponent`:

```typescript
import { Component } from "@angular/core"
import { BaseNodeComponent } from "@visuallyjs/browser-ui-angular"

@Component({
   template:`<div>
  <strong>{{data.label}}</strong>
  <vjs-shape [data]="data" [width]="data.width" [height]="data.height"/>
</div>` 
})
export class MyNodeComponent extends BaseNodeComponent { }  

```

You need to pass `data` in as an input to the SVG shape component (`data` is a class member of `BaseNodeComponent` and `BaseGroupComponent`), as well as map the `width` and `height` inputs. This might seem unnecessary but if you do not bind width and height Angular's change detection will not propagate changes in those values to the template rendering the shape.

The SVG shape component will use `type` (and optionally `category`) from `data` to resolve an appropriate shape to draw from the ShapeLibrary the Surface is using.

## Supported Properties[​](#supported-properties "Direct link to Supported Properties")

An svg shape supports these properties:

* **type** Identifies the shape to be drawn. Required.
* **category** Identifies the shape set that the shape belongs to. Not required if you have only one shape set, but recommended.
* **fill** The color to use for the SVG's background - equivalent to the SVG attribute `fill`.
* **outline** The color to use for the outline of the shape - equivalent to the SVG attribute `stroke`.
* **outlineWidth** The `stroke-width` to use in the shape's outline.
* **label** Label to display for the shape.

An example payload might be:

```json
{
    "type": "process",
    "category": "flowchart",
    "fill":"#FFFFFF",
    "outline":"#000000",
    "outlineWidth":2,
    "label":"My Node" 
}

```

## Definition[​](#definition "Direct link to Definition")

### Inputs[​](#inputs "Direct link to Inputs")

| Name              | Type           | Description                                                                                                                                                                                                                                            |
| ----------------- | -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| height            | number         | Current height. See notes for `width`.                                                                                                                                                                                                                 |
| label?            | string         | Optional label to use. It is better to use this than to rely on the component extracting the<br />label from the object data, as there are some scenarios where the change detection is not invoked<br />when relying on the `labelProperty` approach. |
| labelFillRatio    | number         | For multiline labels, the proportion of the width of the shape that the longest line can take up.                                                                                                                                                      |
| labelProperty?    | string         | Defaults to `label`. The name of the property inside each vertex that contains its label.                                                                                                                                                              |
| labelStrokeWidth? | string         | The stroke width to use for labels. Optional. Defaults to Visually JS's default.                                                                                                                                                                       |
| multilineLabels?  | boolean        | Defaults to true. Set to false if you do not want multi line labels.                                                                                                                                                                                   |
| obj               | [ObjectData]() | The data for the vertex to render. Required.                                                                                                                                                                                                           |
| showLabels?       | boolean        | Whether or not to show labels.                                                                                                                                                                                                                         |
| width             | number         | Current width for the shape. Although it may seem counterintuitive, this is required - you'll need to set it to `[width]="obj.width"`. Angular's change detection will not pick up changes to this otherwise.                                          |
