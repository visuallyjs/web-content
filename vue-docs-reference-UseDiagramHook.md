# useDiagram()

If you decide to write your own component that needs to access the underlying `Diagram`, this hook will be of use.

## Usage[​](#usage "Direct link to Usage")

```html
<script setup>
	import { useDiagram } from "@visuallyjs/browser-ui-vue"
	const diagram = useDiagram()
    
</script>
<template>
	<div v-if="diagram != null">The diagram currently has {diagram.model.getNodes().length} nodes</div>
    <div v-if="diagram == null">Loading...</div>
</template>


```

This hook will only return a value if your component is a descendant in the JSX of a [DiagramProvider](/vue/docs/reference/DiagramProvider.md) or [DiagramComponent](/vue/docs/reference/DiagramComponent.md), for instance:

```html
<script setup>
	import MyComponent from "MyComponent.vue"
	import { DiagramProvider, DiagramComponent } from "@visuallyjs/browser-ui-vue"    
</script>
<template>
	<DiagramProvider>
		<DiagramComponent data={...} options={...}/>
			<MyComponent/>
	</DiagramProvider>
</template>

```
