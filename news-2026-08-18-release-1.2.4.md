# Release 1.2.4

August 18, 2026 ·

<!-- -->

One min read

Release 1.2.4 is now available. In this release:

### General[​](#general "Direct link to General")

* Added new `Bowtie` layout - a two sided hierarchy, such as you might use in a Mindmap.
* Added support for `autoArm` and `armTimeout` to the lasso plugin - the plugin switches on after a long press on the canvas, without the user needing to switch the surface to select mode.
* Our Mindmap starter apps were updated to use the new Bowtie layout instead of the custom layout they were previously using.
* Ported JsPlumb's "neighbourhood views" starter app to VisuallyJs - an app that shows how you can provide several different views of the same dataset on a single page

### Vue[​](#vue "Direct link to Vue")

* The renderer was updated to ensure that the `vertex` passed to Surface/Paper vertex components is marked raw, and not converted to a Proxy by Vue.
* Added support for optional `dataType` prop on the Surface/Paper components

### React[​](#react "Direct link to React")

* Added support for optional `dataType` prop on the Surface/Paper components

### Svelte[​](#svelte "Direct link to Svelte")

* Added support for optional `dataType` prop on the Surface/Paper components

### Angular[​](#angular "Direct link to Angular")

* Added support for optional `dataType` prop on the Surface/Paper components
