# useVisuallyJsUpdate()

This hook provides a means for you to dynamically respond to changes in the underlying model - an example of its usage from VisuallyJs's own starter apps is in the [Network Infrastructure](https://visuallyjs.com/demonstrations/network-infrastructure) starter app, where we display a `Monthly Spend`, which is calculated dynamically as the model is updated.

This hook will only return a value if your component is a descendant in the JSX of a [SurfaceProvider](/react/docs/reference/SurfaceProvider.md) or [SurfaceComponent](/react/docs/reference/SurfaceComponent.md).

## Usage[​](#usage "Direct link to Usage")

You can compute anything you like in the callback you pass to the hook. Here we compute the sum of the `monthlyPrice` of each of the nodes in the dataset.

```jsx
import { useVisuallyJsUpdate } from "@visuallyjs/browser-ui-react"

export default function MonthlySpend() {
    
    const [total, setTotal] = useState(0)

    useVisuallyJsUpdate((model) => {
        // compute total by summing the `monthlyPrice` of each of our nodes
        const t = model.getNodes().map(n => n.data).reduce((acc, current) => acc + current.monthlyPrice, 0)
        setTotal(t)
    })
    
    return <div>Monthly Total: ${total}</div>
}


```

You then need to ensure that you use this component inside a `SurfaceProvider`:

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"
import MonthlySpend from './MonthlySpend'

export default function MyApp() {
    
    return <SurfaceProvider>
            <SurfaceComponent data={...} viewOptions={...}/>
            <MonthlySpend/>
        </SurfaceProvider>
}


```

although you can also nest it inside a `SurfaceComponent`:

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"
import MonthlySpend from './MonthlySpend'

export default function MyApp() {
    
    return <SurfaceComponent data={...} viewOptions={...}>
            <MonthlySpend/>
        </SurfaceComponent>
}


```
