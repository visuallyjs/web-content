# useZoom()

`useZoom` provides access to the current zoom level for the UI in scope. It can be used both to selectively render content based on the current zoom, and also simply to show the user what the current zoom level is.

info

This hook can be used both when you're building a [node-based app](/vue/docs/apps.md) or a [diagram](/vue/docs/diagrams.md)

## Usage[​](#usage "Direct link to Usage")

### Selectively rendering content[​](#selectively-rendering-content "Direct link to Selectively rendering content")

In this example, we have a component that renders a node, and always shows the node's title. If the zoom is larger than 1, the component also shows the node's description.

```html
<script setup lang="ts">
    import { useZoom, VueWrapperProps } from "@visuallyjs/browser-ui-vue"
    
    const {ui, data} = defineProps<VueWrapperProps>() 
    
    const zoom = useZoom()
</script>
<template>
	<div>
		<h3>{{data.title}}</h3>
		<v-if="zoom > 1">
		    <p>{{data.description}}</p>
        </v-if>
	</div>
</template>

```

### Stand alone component[​](#stand-alone-component "Direct link to Stand alone component")

You can also use this hook to build a component that displays the current zoom level.

```html
<script setup>
    import { useZoom } from "@visuallyjs/browser-ui-vue"
    const zoom = useZoom()
</script>
<template>
	<div>Zoom: {{zoom.toFixed(2)}}</div>
</template>

```

Here, we need to ensure that the `CurrentZoom` component is declared inside a `SurfaceProvider` or `SurfaceComponent`, in order for it to be able to resolve the surface:

```html
<script setup>
    import { SurfaceProvider, SurfaceComponent } from "@visuallyjs/browser-ui-vue"
    import CurrentZoom from './CurrentZoom.vue'
</script>
<template>
	<SurfaceProvider>
		<SurfaceComponent :data="..." :viewOptions="..."/>
        <CurrentZoom/>
	</SurfaceProvider>
</template>



```
