# \<ShapePropertiesInspector/>

## Usage[​](#usage "Direct link to Usage")

If you haven't yet read the docs for [InspectorComponent](/react/docs/reference/InspectorComponent.md) we'd recommend it.

This component renders the properties defined by the selected shape in the active shape library. Use it inside an inspector and pass it the vertex being inspected.

```jsx
import { InspectorComponent, ShapePropertiesInspector } from "@visuallyjs/browser-ui-react"
import { Vertex } from "@visuallyjs/browser-ui"

export default function MyInspectorComponent() {
    return <InspectorComponent>
        {(current) => {
            if (current.objectType === Vertex.objectType) {
                return <ShapePropertiesInspector vertex={current} />
            }
            return null
        }}
    </InspectorComponent>
}

```

## Props[​](#props "Direct link to Props")

ShapePropertiesInspectorProps

Props for the ShapePropertiesInspector

| Name       | Type       | Description                                                                                                        |
| ---------- | ---------- | ------------------------------------------------------------------------------------------------------------------ |
| maxRadios? | number     | The maximum number of radio buttons to show for a value list before switching to a select dropdown. Defaults to 7. |
| vertex     | [Vertex]() | vertex to inspector                                                                                                |

`maxRadios` controls how many choices are displayed as radio buttons before the inspector uses a dropdown.
