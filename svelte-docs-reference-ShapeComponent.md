# \<ShapeComponent/>

A component that renders an SVG shape from a `ShapeLibrary`. This component can be used inside your own Svelte components if you've got a `ShapeLibrary` setup on your Surface - see the documentation for a discussion of this.

If you're building an SVG diagram in which the shapes are the entire node contents, you may want to look at the [DiagramComponent](/svelte/docs/reference/DiagramComponent.md).

## Usage[​](#usage "Direct link to Usage")

This component is used inside the component that represents some node (or group) in your app. For example, we might create a component to render our nodes like this:

```html
<script>
  import { ShapeComponent } from "@visuallyjs/browser-ui-svelte"
  
  const { data } = $props()
    
</script>

<div class="my-node">
	<h3>{{data.label}}</h3>
	<ShapeComponent data={data}/>
</div>

```

`data` is the backing data for the vertex being rendered, and is injected by the surface component. The Shape component will extract the vertex's `type` (and optionally `category`) values, and will use them to resolve an appropriate shape to draw from the ShapeLibrary the surface is using.

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

| Name             | Type           | Description                                                                                                                                                                           |
| ---------------- | -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| data             | [ObjectData]() | Backing data for the vertex. Required. This is passed in as a prop to a component used to render a node/group, so you can pass it straight through from the parent to this component. |
| font?            | [FontSpec]()   | Optional font size/style.                                                                                                                                                             |
| labelPosition?   | LabelPosition  | Defaults to "center". Use "top" or "bottom" to set the label above or below the shape.                                                                                                |
| labelProperty?   | string         | The name of the property containing each vertex's label. Defaults to `label`.                                                                                                         |
| labelStrokeWidth | string         | Stroke width to use on the text element rendering a label. Defaults to "0.25px".                                                                                                      |
| showLabels?      | boolean        | Whether or not to show labels on each shape. Defaults to false.                                                                                                                       |
