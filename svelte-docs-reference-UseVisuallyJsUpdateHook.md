# useVisuallyJsUpdate()

This hook provides a means for you to dynamically respond to changes in the underlying model - an example of its usage from VisuallyJs's own starter apps is in the [Network Infrastructure](https://visuallyjs.com/demonstrations/network-infrastructure) starter app, where we display a `Monthly Spend`, which is calculated dynamically as the model is updated.

This hook will only return a value if your component is a descendant inside a [SurfaceProvider](/svelte/docs/reference/SurfaceProvider.md) or [SurfaceComponent](/svelte/docs/reference/SurfaceComponent.md).

## Usage[​](#usage "Direct link to Usage")

You can compute anything you like in the callback you pass to the hook. Here we compute the sum of the `monthlyPrice` of each of the nodes in the dataset.

```html
<script>
    import { useVisuallyJsUpdate } from "@visuallyjs/browser-ui-svelte"
	let total = $state(0)

	useVisuallyJsUpdate((model) => {
		// compute total by summing the `monthlyPrice` of each of our nodes
		const t = model.getNodes().map(n => n.data).reduce((acc, current) => acc + current.monthlyPrice, 0)
		total = t
	})

</script>
<div>Monthly Total: ${total.toFixed(2)}</div>


```

You then need to ensure that you use this component inside a `SurfaceProvider`:

```html
<script setup>
import { SurfaceComponent, SurfaceProvider } from "@visuallyjs/browser-ui-svelte"
import MonthlySpend from './MonthlySpend.svelte'
</script>
<SurfaceProvider>
	<SurfaceComponent data={...} viewOptions={...}/>
		<MonthlySpend/>
</SurfaceProvider>

```

although you can also nest it inside a `SurfaceComponent`:

```html
<script setup>
import { SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
import MonthlySpend from './MonthlySpend.svelte'
</script>
<SurfaceComponent data={...} viewOptions={...}>
	<MonthlySpend/>
</SurfaceComponent>

```
