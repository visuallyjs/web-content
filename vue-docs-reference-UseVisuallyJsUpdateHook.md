# useVisuallyJsUpdate()

This hook provides a means for you to dynamically respond to changes in the underlying model - an example of its usage from VisuallyJs's own starter apps is in the [Network Infrastructure](https://visuallyjs.com/demonstrations/network-infrastructure) starter app, where we display a `Monthly Spend`, which is calculated dynamically as the model is updated.

This hook will only return a value if your component is a descendant inside a [SurfaceProvider](/vue/docs/reference/SurfaceProvider.md) or [SurfaceComponent](/vue/docs/reference/SurfaceComponent.md).

## Usage[​](#usage "Direct link to Usage")

You can compute anything you like in the callback you pass to the hook. Here we compute the sum of the `monthlyPrice` of each of the nodes in the dataset.

```html
<script setup>
    import { useVisuallyJsUpdate } from "@visuallyjs/browser-ui-vue"
	let total = ref(0)

	useVisuallyJsUpdate((model) => {
		// compute total by summing the `monthlyPrice` of each of our nodes
		const t = model.getNodes().map(n => n.data).reduce((acc, current) => acc + current.monthlyPrice, 0)
		total.value = t
	})

</script>
<template>
    <div>Monthly Total: ${{total.toFixed(2)}}</div>
</template>


```

You then need to ensure that you use this component inside a `SurfaceProvider`:

```html
<script setup>
import { SurfaceComponent, SurfaceProvider } from "@visuallyjs/browser-ui-vue"
import MonthlySpend from './MonthlySpend.vue'
</script>
<template>
	<SurfaceProvider>
		<SurfaceComponent data={...} viewOptions={...}/>
        <MonthlySpend/>
	</SurfaceProvider>
</template>

```

although you can also nest it inside a `SurfaceComponent`:

```html
<script setup>
import { SurfaceComponent } from "@visuallyjs/browser-ui-vue"
import MonthlySpend from './MonthlySpend.vue'
</script>
<template>
	<SurfaceComponent data={...} viewOptions={...}>
		<MonthlySpend/>
    </SurfaceComponent>
</template>

```
