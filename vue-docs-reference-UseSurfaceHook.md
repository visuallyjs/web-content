# useSurface()

If you decide to write your own component that needs to access the underlying `Surface`, this hook will be of use.

## Usage[​](#usage "Direct link to Usage")

```html
<script setup>
	import { useSurface } from "@visuallyjs/browser-ui-vue"
	const surface = useSurface()
    
</script>
<template>
	<div v-if="surface != null">The surface currently has {surface.model.getNodes().length} nodes</div>
    <div v-if="surface == null">Loading...</div>
</template>


```

This hook will only return a value if your component is a descendant in the JSX of a [SurfaceProvider](/vue/docs/reference/DiagramProvider.md) or [SurfaceComponent](/vue/docs/reference/DiagramComponent.md), for instance:

```html
<script setup>
	import MyComponent from "MyComponent.vue"
	import { SurfaceProvider, SurfaceComponent } from "@visuallyjs/browser-ui-vue"    
</script>
<template>
	<SurfaceProvider>
		<SurfaceComponent data={...} options={...}/>
		<MyComponent/>
	</SurfaceProvider>
</template>

```
