# \<DiagramProvider/>

This is a context provider that enables you to use various other components alongside a [DiagramComponent](/svelte/docs/reference/DiagramComponent.md) without having to explicitly connect them up.

## Usage[​](#usage "Direct link to Usage")

```html
<script lang="ts">
	import {DiagramComponent, DiagramComponentOptions, DiagramProvider, DiagramPaletteComponent} from "@visuallyjs/browser-ui-svelte"
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
<DiagramProvider>
	<DiagramComponent options={options} data={data}/>
    <div>
		<DiagramPaletteComponent/>
    </div>
</DiagramProvider>


```

The list of components that are diagram context aware is:

* [DiagramPaletteComponent](/svelte/docs/reference/DiagramPaletteComponent.md)
* [ControlsComponent](/svelte/docs/reference/ControlsComponent.md)
* [ExportControlsComponent](/svelte/docs/reference/ExportControlsComponent.md)
