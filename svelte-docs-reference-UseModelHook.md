# useVisuallyJsModel()

This hook provides access to the underlying model. It's not something you'll necessarily need often, but if you're writing your own components that want to manipulate the model, this is the hook for you.

## Usage[​](#usage "Direct link to Usage")

This is an asynchronous hook that returns a Promise, which resolves to the current model in use. Your component should use it as shown in the code below.

```tsx
<script lang="ts">
import { useVisuallyJsModel, BrowserUISvelteModel } from "@visuallyjs/browser-ui-svelte"

let model = $state<BrowserUISvelteModel>()
useVisuallyJsModel().then((s:BrowserUISvelteModel) => model = s)
</script>

<div class="my-component">
    {#if model}
    The model currently has {model.getNodes().length} nodes
    {:else}
    Loading...
    {/if}
</div>


```
