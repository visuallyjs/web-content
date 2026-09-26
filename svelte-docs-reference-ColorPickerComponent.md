# \<ColorPickerComponent/>

A helper component that offers the ability to change color and keep a history of selected colors, for use with an [InspectorComponent](/svelte/docs/reference/InspectorComponent.md).

## Usage[​](#usage "Direct link to Usage")

If you haven't yet read the docs for [InspectorComponent](/svelte/docs/reference/InspectorComponent.md) we'd recommend it.

This component is used in the template for an inspector. You need to pass in the name of the property to manage.

```html
<script lang="ts">

import { InspectorComponent, ColorPickerComponent } from "@visuallyjs/browser-ui-svelte"
import {Base} from "@visuallyjs/browser-ui";

let current = $state<Base|null>(null)
    
</script>

<InspectorComponent bind:current={current}>

	<ColorPickerComponent propertyName="bgColor"/>

</InspectorComponent>

```

ColorPickerComponentProps

Props for the ColorPicker inspector component.

| Name         | Type   | Description                                                      |
| ------------ | ------ | ---------------------------------------------------------------- |
| maxColors?   | number | Maximum color swatches to show. Defaults to 10.                  |
| propertyName | string | Property name in the data that this picker represents. Required. |
