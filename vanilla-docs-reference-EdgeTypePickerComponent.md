# EdgeTypePicker

This component provides the means for a user to pick an edge type from a visual rendering of the available options. It reads the current list of edge property mappings from the surface its inspector is attached to, and draws a sample of each one in a list for the user to select from. It is designed for use inside of an Inspector.

## Usage[​](#usage "Direct link to Usage")

If you haven't yet read the docs for [Inspector](/vanilla/docs/reference/InspectorComponent.md) we'd recommend it. This component is used in the template for an inspector, using the HTML element `vjs-edge-type`. Here, we adapt the example from the inspectors page to replace the radio buttons used to select edge type with an edge type picker:

```typescript
import { createSurface, VanillaInspector, 
        Node, Base, Edge } from "@visuallyjs/browser-ui"

const renderOptions = {... }

const surface = createSurface(document.getElementById("myContainer"), renderOptions)

new VanillaInspector(document.getElementById("myInspector"), surface, {
    templateResolver:(obj:Base):string => {
        if (obj.objectType === Node.objectType) {
            return  `<div>
  <label>Label:<input vjs-att="label" vjs-focus/></label>
  <label>Background:<vjs-color vjs-att="bg"/></label>
</div>`
        } else if (obj.objectType === Edge.objectType) {
            return `<div>Edge Type:<vjs-edge-type vjs-att="edgeType"/></div>` 
        }
    }
})

```

## Edge Mappings[​](#edge-mappings "Direct link to Edge Mappings")

This component expects that you have some edge mappings declared on your surface - it is these that the component displays for the user to select from.

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
