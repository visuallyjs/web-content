# \<ColorPickerComponent/>

A helper component that offers the ability to change color and keep a history of selected colors, for use with an [InspectorComponent](/vue/docs/reference/InspectorComponent.md).

## Usage[​](#usage "Direct link to Usage")

If you haven't yet read the docs for [InspectorComponent](/vue/docs/reference/InspectorComponent.md) we'd recommend it.

This component is used in the template for an inspector. You need to pass in the name of the property to manage.

```html

<script setup>
	import { ref } from "vue"

	const current = ref(null)

</script>
<template>
  <InspectorComponent v-model="current">
	  <ColorPickerComponent propertyName="bgColor"/>
  </InspectorComponent>
</template>

```

## Inputs[​](#inputs "Direct link to Inputs")

ColorPickerComponentProps

| Name         | Type   | Description                                              |
| ------------ | ------ | -------------------------------------------------------- |
| maxColors?   | number | Maximum number of color swatches to show, defaults to 10 |
| propertyName | string | The name of the property to bind to.                     |
