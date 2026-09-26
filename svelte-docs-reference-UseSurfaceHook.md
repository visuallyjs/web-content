# useSurface()

If you decide to write your own component that needs to access the underlying `Surface`, this hook will be of use.

## Usage[​](#usage "Direct link to Usage")

```html
<script>
	import { useSurface } from "@visuallyjs/browser-ui-svelte"
	const surface = useSurface()
</script>
{#if surface != null}
The surface currently has {surface.model.getNodes().length} nodes
{/if}
{#if surface == null}Loading...{/if}


```

This hook will only return a value if your component is a descendant inside a [SurfaceProvider](/svelte/docs/reference/SurfaceProvider.md) or [SurfaceComponent](/svelte/docs/reference/SurfaceComponent.md), for instance:

```html
<script>
	import MyComponent from "MyComponent.svelte"
	import { SurfaceProvider, SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
</script>
<SurfaceProvider>
	<SurfaceComponent data={...} options={...}/>
		<MyComponent/>
</SurfaceProvider>

```
