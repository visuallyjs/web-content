# useZoom()

`useZoom` provides access to the current zoom level for the UI in scope. It can be used both to selectively render content based on the current zoom, and also simply to show the user what the current zoom level is.

info

This hook can be used both when you're building a [node-based app](/svelte/docs/apps.md) or a [diagram](/svelte/docs/diagrams.md)

## Usage[​](#usage "Direct link to Usage")

### Selectively rendering content[​](#selectively-rendering-content "Direct link to Selectively rendering content")

In this example, we have a component that renders a node, and always shows the node's title. If the zoom is larger than 1, the component also shows the node's description.

```html
<script lang="ts">
    import { useZoom, SvelteWrapperProps } from "@visuallyjs/browser-ui-svelte"

	let { model, vertex, data }:SvelteWrapperProps = $props();
    
    const zoom = useZoom()
</script>
<div>
	<h3>{{data.title}}</h3>
	{
	{#if zoom > 1}
	<p>{{data.description}}</p>
	{/if}
</div>

```

### Stand alone component[​](#stand-alone-component "Direct link to Stand alone component")

You can also use this hook to build a component that displays the current zoom level.

```html
<script>
    import { useZoom } from "@visuallyjs/browser-ui-svelte"
    const zoom = useZoom()
</script>
<div>Zoom: {zoom.toFixed(2)}</div>

```

Here, we need to ensure that the `CurrentZoom` component is declared inside a `SurfaceProvider` or `SurfaceComponent`, in order for it to be able to resolve the surface:

```html
<script setup>
    import { SurfaceProvider, SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
    import CurrentZoom from './CurrentZoom.svelte'
</script>
<SurfaceProvider>
	<SurfaceComponent :data="..." :viewOptions="..."/>
	<CurrentZoom/>
</SurfaceProvider>


```
