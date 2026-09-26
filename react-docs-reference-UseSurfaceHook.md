# useSurface()

If you decide to write your own component that needs to access the underlying `Surface`, this hook will be of use.

## Usage[​](#usage "Direct link to Usage")

```jsx
import { useSurface } from "@visuallyjs/browser-ui-react"

export default function MyComponent() {
    
    const surface = useSurface()
    
    return <div>
        {surface && <>The Surface currently has {surface.model.getNodes().length} nodes.</>}
        {!surface && <>Loading...</>}
    </div>
}


```

This hook will only return a value if your component is a descendant in the JSX of a [SurfaceProvider](/react/docs/reference/SurfaceProvider.md) or [SurfaceComponent](/react/docs/reference/SurfaceComponent.md), for instance:

```jsx

import MyComponent from "./my-component"
import { SurfaceProvider, SurfaceComponent } from "@visuallyjs/browser-ui-react"

export default function MyApp() {
    
    return <SurfaceProvider>
        <SurfaceComponent data={{nodes:[{id:"1"}, {id:"2"}]}}/>
        <MyComponent/>
    </SurfaceProvider>
}


```
