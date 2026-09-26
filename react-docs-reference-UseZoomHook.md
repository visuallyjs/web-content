# useZoom()

`useZoom` provides access to the current zoom level for the UI in scope. It can be used both to selectively render content based on the current zoom, and also simply to show the user what the current zoom level is.

info

This hook can be used both when you're building a [node-based app](/react/docs/apps.md) or a [diagram](/react/docs/diagrams.md)

## Usage[​](#usage "Direct link to Usage")

### Selectively rendering content[​](#selectively-rendering-content "Direct link to Selectively rendering content")

In this example, we have a component that renders a node, and always shows the node's title. If the zoom is larger than 1, the node also shows the node's description.

```tsx
import { useZoom, JsxWrapperProps } from "@visuallyjs/browser-ui-react"

export default function MyNodeComponent(ctx:JsxWrapperProps) {
    
    const zoom = useZoom(ctx.ui)
    
    return <div>
        <h3>{ctx.data.title}</h3>
        {zoom > 1 && <p>{ctx.data.description}</p>}
    </div>
}


```

### Stand alone component[​](#stand-alone-component "Direct link to Stand alone component")

You can also use this hook to build a component that displays the current zoom level.

```tsx
import { useZoom } from "@visuallyjs/browser-ui-react"

export default function CurrentZoom() {
    
    const zoom = useZoom()
    
    return <div>Zoom: {zoom.toFixed(2)}</div>
}


```

Here, we need to ensure that the `CurrentZoom` component is declared inside a `SurfaceProvider` or `SurfaceComponent`, in order for it to be able to resolve the surface:

```jsx
import { useVisuallyJsUpdate, SurfaceComponent } from "@visuallyjs/browser-ui-react"
import CurrentZoom from './CurrentZoom'

export default function MyApp() {
    
    return <SurfaceProvider>
            <SurfaceComponent data={...} viewOptions={...}/>
            <CurrentZoom/>
        </SurfaceProvider>
}


```
