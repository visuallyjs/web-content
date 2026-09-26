# Unattached edges

In a diagram, by default, edges may have a `source` and/or `target` vertex, or their source/target may be located in whitespace. We refer to this as an `unattached edge`.

## Configuration[​](#configuration "Direct link to Configuration")

Unattached edges are switched on by default. To turn them off, set `allowUnattached:false` in your render options:

```jsx

import { DiagramComponent } from "@visuallyjs/browser-ui-react"
import "@visuallyjs/browser-ui/css/visuallyjs.css";

export default function App() {
    
  const data = ...
    
  const options = {
  edges: {
    allowUnattached: false
  }
}
    
  return <div style={{width:"100%", height:"500px"}}>
    <DiagramComponent data={data} options={options}/>
  </div>    
}

```
