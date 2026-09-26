# useVisuallyJsModel()

This hook provides access to the underlying model. It's not something you'll necessarily need often, but if you're writing your own components that want to manipulate the model, this is the hook for you.

## Usage[​](#usage "Direct link to Usage")

```jsx
import { useVisuallyJsModel } from "@visuallyjs/browser-ui-react"

export default function MyComponent() {

    const model = useVisuallyJsModel()
    
    return <div>
        {model && <>The model currently has {model.getNodes().length} nodes.</>}
        {!model && <>Loading...</>}
    </div>
}


```
