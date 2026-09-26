# ShapeComponent

This is a custom tag that renders an SVG shape from a `ShapeLibrary`. You can use this inside the markup for your nodes/groups if you've got a `ShapeLibrary` setup.

If you're building an SVG diagram in which the shapes are the entire node contents, you may want to look at the [DiagramComponent](/vanilla/docs/reference/DiagramComponent.md).

## Usage[​](#usage "Direct link to Usage")

This component is used inside the component that represents some node (or group) in your app. For example, we might create markup to render our nodes like this:

```typescript
const surface = createSurface(someElement, {
  view:{
    nodes:{
      default:{
        template:`<svg:svg class="my-node-type" width="{{width}}" height="{{height}}">
  <vjs-shape/>
</svg:svg>`
      } 
    }
  }
})

```

The shape tag will extract the vertex's `type` (and optionally `category`) values, and will use them to resolve an appropriate shape to draw from the ShapeLibrary the Surface is using.

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
