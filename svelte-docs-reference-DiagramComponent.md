# \<DiagramComponent/>

Provides an SVG diagram component. This is a wrapper around a Surface or Paper, with a few flags set:

* We use an SVG container element
* Every cell is drawn as an SVG element from a ShapeLibrary
* Cell sizes and positions are stored inside the model

A Diagram is a pure SVG UI.

## Usage[​](#usage "Direct link to Usage")

```html
<script lang="ts">
	import {DiagramComponent, DiagramComponentOptions} from "@visuallyjs/browser-ui-svelte"
	import {FLOWCHART_SHAPES} from "@visuallyjs/browser-ui";

	const options: DiagramComponentOptions = {
		shapes: {
			sets: {FLOWCHART_SHAPES}
		}
	}
	const data = {
		...
	}
</script>
<DiagramComponent options={options} data={data}/>

```

## Props[​](#props "Direct link to Props")

DiagramComponentProps

| Name          | Type               | Description                                                                                                                              |
| ------------- | ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------- |
| className?    | string             | Optional class name to set on the diagram component's container                                                                          |
| data?         | any                | Optional data to load after the component has been mounted.                                                                              |
| modelOptions? | [ModelOptions]()   | Options for the model used by the diagram. Only required for<br />certain advanced use cases.                                            |
| options?      | [DiagramOptions]() | Options for the diagram.                                                                                                                 |
| url?          | string             | Optional url from which to load data after the component has been mounted. If you provide this and also data, this will take precedence. |
