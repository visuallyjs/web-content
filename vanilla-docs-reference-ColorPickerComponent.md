# ColorPicker

A helper component that offers the ability to change color and keep a history of selected colors, for use with an [Inspector](/vanilla/docs/reference/InspectorComponent.md).

## Usage[​](#usage "Direct link to Usage")

If you haven't yet read the docs for [Inspector](/vanilla/docs/reference/InspectorComponent.md) we'd recommend it. This component is used in the template for an inspector, using the HTML element `vjs-color`. Here we adapt the example shown on the inspector page to replace the standard color input with one of our color pickers:

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
            return `<div>
Edge Type:
    <label><input type="radio" vjs-att="edgeType" value="type1"/>Type 1</label>
    <label><input type="radio" vjs-att="edgeType" value="type2"/>Type 2</label>
</div>` 
        }
    }
})

```
