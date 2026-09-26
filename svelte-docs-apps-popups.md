# Popups

Popups, new in 1.2.1, offer a means for you to declaratively attach some component to act as a popup on a vertex, and as the user pans, zooms or drags the vertex, VisuallyJs will ensure that the popup remains in place relative to the element.

![Popups](https://static.visuallyjs.com/img/blog/1.2.1/popups.png)

## Configuration[​](#configuration "Direct link to Configuration")

### Declare Component[​](#declare-component "Direct link to Declare Component")

<!-- -->

<!-- -->

<!-- -->

<!-- -->

To configure a popup in Svelte you need to define a component that will take a `vertex`, `model` and `ui` as props (and, optionally, a `hide` function that your component can use to tell the popup to hide). This example (shown above) is from our [AI Agent Builder demonstration](/demonstrations/ai-agent-builder.md):

```html

<script>
import {BrowserUI, Node, VisuallyJsModel} from "@visuallyjs/browser-ui";

const {vertex, model, ui, hide} = $props()
</script>
<div>
{#if vertex != null}
  {vertex.data.label}
  {model.getNodes().length}
{/if}
</div>

```

Your component has access to:

* the vertex the popup is attached to
* the data model
* the UI that rendered this popup
* a function you can invoke to instruct the popup to hide

### Configure Popup[​](#configure-popup "Direct link to Configure Popup")

<!-- -->

<!-- -->

<!-- -->

<!-- -->

Then to declare that you want to use this component as a popup, you need to declare a `SurfacePopup` in your component's template, and specify the selector that the popup should listen for:

```html

<SurfacePopup selector=".vjs-next-step-picker">
  {#snippet popup(vertex, model, ui, hide)}
      <PopupComponent {vertex} {model} {ui} {hide}/>
  {/snippet}
</SurfacePopup>

```

### Add Popup Launcher[​](#add-popup-launcher "Direct link to Add Popup Launcher")

<!-- -->

<!-- -->

<!-- -->

<!-- -->

Lastly, you can now include a launcher for this popup anywhere inside a component you're using to render a vertex:

```html

<script>
import { defineProps } from "vue";

const {data, vertex, ui} = defineProps()
</script>
<div>
<h1>{{data.label}}</h1>
<button class="vjs-next-step-picker">Launch popup</button>
</div>


```
