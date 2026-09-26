# \<EdgePropertyMappingsInspector/>

This component automatically renders a form for editing edge properties based on the edge property mappings defined on the surface. It is designed for use inside of an Inspector and provides an easy way to allow users to customize edge appearance and behavior.

## Usage[​](#usage "Direct link to Usage")

If you haven't yet read the docs for [InspectorComponent](/vue/docs/reference/InspectorComponent.md) we'd recommend it.

This component is used inside an inspector. It automatically reads the current edge property mappings from the surface and displays the controls for the selected edge.

```html

<script setup>
	import { ref } from "vue"

	const current = ref(null)

</script>
<template>
  <InspectorComponent v-model="current">
    <div v-if="current?.objectType === 'Edge'" class="edge-inspector">
      <EdgePropertyMappingsInspector />
    </div>
  </InspectorComponent>
</template>

```

## Props[​](#props "Direct link to Props")

EdgePropertyMappingsInspectorProps

| Name             | Type                                                | Description                                                                                                                            |
| ---------------- | --------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| className?       | string                                              | Optional class name to use on the wrapper div. Defaults to `vjs-inspector-section`.                                                    |
| getPropertyName? | (pm:[PropertyMapping<]()[EdgeMapping]()>) => string | Optional, you can implement this method to return your own names to use for properties in the inspector.                               |
| mappings?        | [EdgePropertyMappings]()                            | Optional property mappings to render a form for. The default behaviour is to retrieve the property mappings from the inspector context |
| showName?        | boolean                                             | Optional, whether or not to show property names. Defaults to true.                                                                     |

## Edge Mappings[​](#edge-mappings "Direct link to Edge Mappings")

This component expects that you have some edge mappings declared on your surface - it is these that the component uses to build the form.

Edge mappings allows you to match specific values for a given property to a set of config options for an edge.

An edge mapping declares a `property`, which is the name of some property an edge's backing data that VisuallyJs will attempt to match. In the code snippet below we're matching the property `lineStyle`. Then there is a `mappings` section, which is an object whose keys are the values we're matching.

In this example we see four possible matches - `"source"`, `"target"`, `"plain"` and `"dashed"`. Each match then declares a set of zero or more configuration options for the edge.

The `name` property is optional; it is used in the edge property mapper inspector as the default label to show for the section pertaining to the property mapping. If omitted, the value of `property` will be used as the section label.

```json
{
    "property": "lineStyle",
    "name": "Line Style",
    "mappings": {
      "source": {
        "overlays": [
          {
            "type": "Arrow",
            "options": {
              "location": 0,
              "direction": -1,
              "width": 5,
              "length": 10
            }
          }
        ]
      },
      "target": {
        "overlays": [
          {
            "type": "Arrow",
            "options": {
              "location": 1,
              "width": 5,
              "length": 10
            }
          }
        ]
      },
      "plain": {},
      "dashed": {
        "cssClass": "some-css-class"
      }
    }
}

```
