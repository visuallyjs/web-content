# useInspector()

This hook is for use by components that are children of an [InspectorComponent](/react/docs/reference/InspectorComponent.md). It provides access to the underlying `Inspector`. You won't need to use this hook unless you're writing your own custom components for an inspector.

## Usage[​](#usage "Direct link to Usage")

```jsx
import { useInspector } from "@visuallyjs/browser-ui-react"

export default function MyEditorComponent(props) {
    const inspector = useInspector()
    
    // you can call inspector.setValue(key, value) to set values
    
}


```
