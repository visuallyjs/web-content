# useDiagram()

If you decide to write your own component that needs to access the underlying `Diagram`, this hook will be of use.

## Usage[​](#usage "Direct link to Usage")

```jsx
import { useDiagram } from "@visuallyjs/browser-ui-react"

export default function MyComponent() {
    
    const diagram = useDiagram()
    
    return <div>
        {diagram && <>The diagram currently has {diagram.model.getNodes().length} nodes.</>}
        {!diagram && <>Loading...</>}
    </div>
}


```

This hook will only return a value if your component is a descendant in the JSX of a [DiagramProvider](/react/docs/reference/DiagramProvider.md) or [DiagramComponent](/react/docs/reference/DiagramComponent.md), for instance:

```jsx

import MyComponent from "./my-component"
import { DiagramProvider, DiagramComponent } from "@visuallyjs/browser-ui-react"

export default function MyApp() {
    
    return <DiagramProvider>
        <DiagramComponent data={...} options={...}/>
        <MyComponent/>
    </DiagramProvider>
}


```
