# useDiagram()

If you decide to write your own component that needs to access the underlying `Diagram`, this hook will be of use.

## Usage[​](#usage "Direct link to Usage")

```html
<script>
	import { useDiagram } from "@visuallyjs/browser-ui-svelte"
	const diagram = useDiagram()
</script>
{#if diagram != null}
The diagram currently has {diagram.model.getNodes().length} nodes
{/if}
{#if diagram == null}Loading...{/if}


```

This hook will only return a value if your component is a descendant in the JSX of a [DiagramProvider](/svelte/docs/reference/DiagramProvider.md) or [DiagramComponent](/svelte/docs/reference/DiagramComponent.md), for instance:

```html
<script>
	import MyComponent from "MyComponent.svelte"
	import { DiagramProvider, DiagramComponent } from "@visuallyjs/browser-ui-svelte"    
</script>
<DiagramProvider>
	<DiagramComponent data={...} options={...}/>
		<MyComponent/>
</DiagramProvider>

```
