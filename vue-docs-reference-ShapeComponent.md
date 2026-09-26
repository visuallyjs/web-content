# \<ShapeComponent/>

A component that renders an SVG shape from a `ShapeLibrary`. This component can be used inside your own Vue components if you've got a `ShapeLibrary` setup on your Surface - see the documentation for a discussion of this.

If you're building an SVG diagram in which the shapes are the entire node contents, you may want to look at the [DiagramComponent](/vue/docs/reference/DiagramComponent.md).

## Usage[​](#usage "Direct link to Usage")

This component is used inside the component that represents some node (or group) in your app. For example, we might create a component to render our nodes like this:

```html
<script>
import { defineComponent} from "vue"
import { BaseNodeComponent } from "@visuallyjs/browser-ui-vue" 

export default defineComponent({
    mixins:[BaseNodeComponent]
})
</script>
<template>
    <div class="my-node">
        <h3>{{data.label}}</h3>
        <Shape :data="data"/>
    </div>
</template>

```

`data` is exposed by `BaseNodeComponent`, and is the backing data for the vertex being rendered. The Shape component will extract the vertex's `type` (and optionally `category`) values, and will use them to resolve an appropriate shape to draw from the ShapeLibrary the Surface is using.

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

## Props[​](#props "Direct link to Props")

ShapeComponentProps

Props for the `ShapeComponent`.

| Name              | Type           | Description                                                                |
| ----------------- | -------------- | -------------------------------------------------------------------------- |
| labelColor?       | string         | Color for the label. Defaults to #000000.                                  |
| labelFillRatio?   | number         | When using a multiline label, defines the maximum width of any given line. |
| labelProperty?    | string         | Name of the property containing the object's label. Defaults to "label".   |
| labelStrokeWidth? | number         | Stroke width for the label text.                                           |
| multilineLabels?  | boolean        | Defaults to true - the label will be drawn across multiple lines.          |
| obj               | [ObjectData]() | Backing data for the vertex                                                |
| showLabels?       | boolean        | Whether or not to show labels Defaults to false.                           |
