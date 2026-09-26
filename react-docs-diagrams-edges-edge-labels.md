# Edge Labels

You can extract the value of each edge's `label` from the edge's backing data:

```jsx

import { DiagramComponent } from "@visuallyjs/browser-ui-react"
import "@visuallyjs/browser-ui/css/visuallyjs.css";

export default function App() {
    
  const data = {
  nodes:[
    {id:"1",x:50,y:50,type:"diamond"},
     {id:"2",x:250,y:50,type:"rectangle"}
  ],
  edges:[
    {source:"1",target:"2",data:{label:"A Label"}}
  ]
}
    
  const options = {
  edges: {
    showLabels: true
  }
}
    
  return <div style={{width:"100%", height:"500px"}}>
    <DiagramComponent data={data} options={options}/>
  </div>    
}

```

**********

## Rotated labels[​](#rotated-labels "Direct link to Rotated labels")

By default, edge labels will be drawn so that the text reads horizontally. You can instruct VisuallyJs to rotate edge labels to match the slope of the connector line via the `labelsRotatable` edge option:

```jsx

import { DiagramComponent } from "@visuallyjs/browser-ui-react"
import "@visuallyjs/browser-ui/css/visuallyjs.css";

export default function App() {
    
  const data = {
  nodes:[
    {id:"1",x:250,y:50,type:"ellipse"},
     {id:"2",x:50,y:100,type:"rectangle"}
  ],
  edges:[
    {source:"1",target:"2",data:{label:"A Label"}}
  ]
}
    
  const options = {
  edges: {
    showLabels: true,
    labelsRotatable: true,
    targetMarker: "Arrow"
  }
}
    
  return <div style={{width:"100%", height:"500px"}}>
    <DiagramComponent data={data} options={options}/>
  </div>    
}

```

**********

### Strict rotation[​](#strict-rotation "Direct link to Strict rotation")

In the above example, the edge's source is to the right of the target, and so, strictly speaking, if the label were rotated to match the slope of the connector, it would be flipped. Since this is not easy to read for a user, by default we rotate labels in `"legible"` mode - when the angle of rotation lies between 90 and 270 degrees, we flip it.

If you want VisuallyJs to strictly honour the slope of the connector, you can set `strict` for `labelsRotatable`:

```jsx

import { DiagramComponent } from "@visuallyjs/browser-ui-react"
import "@visuallyjs/browser-ui/css/visuallyjs.css";

export default function App() {
    
  const data = {
  nodes:[
    {id:"1",x:250,y:50,type:"ellipse"},
     {id:"2",x:50,y:100,type:"rectangle"}
  ],
  edges:[
    {source:"1",target:"2",data:{label:"A Label"}}
  ]
}
    
  const options = {
  edges: {
    showLabels: true,
    labelsRotatable: "strict",
    targetMarker: "Arrow"
  }
}
    
  return <div style={{width:"100%", height:"500px"}}>
    <DiagramComponent data={data} options={options}/>
  </div>    
}

```

**********

## Label location[​](#label-location "Direct link to Label location")

By default, an edge label will be assigned a location of `0.5` - meaning it will be halfway along the edge path. You can change this by providing a `labelLocation`:

```jsx

import { DiagramComponent } from "@visuallyjs/browser-ui-react"
import "@visuallyjs/browser-ui/css/visuallyjs.css";

export default function App() {
    
  const data = {
  nodes:[
    {id:"1",x:50,y:50,type:"diamond"},
     {id:"2",x:250,y:50,type:"rectangle"}
  ],
  edges:[
    {source:"1",target:"2",data:{label:"A Label"}}
  ]
}
    
  const options = {
  edges: {
    showLabels: true,
    labelLocation: 0.25
  }
}
    
  return <div style={{width:"100%", height:"500px"}}>
    <DiagramComponent data={data} options={options}/>
  </div>    
}

```

**********

You can also control this via a `labelLocation` value in your edge's backing data. For example, this edge:

```javascript
{
    source:"someNode",
    target:"someOtherNode",
    data:{
        labelLocation:0.25
    }
}

```

would instruct VisuallyJs to put the label at 0.25, and you would not need to set `labelLocation` in the edge options.
