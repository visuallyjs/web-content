# Building a diagram

On this page we'll run through how to build a basic diagram with VisuallyJs - we'll be creating the diagram from the [Overview](/vanilla/docs/diagrams.md) page, from the initial setup of the diagram with a couple of helper components, to the addition of shapes and edges, and then we'll provide some suggestions for where you may wish to go next.

## Installation[​](#installation "Direct link to Installation")

You'll need to ensure you've imported VisuallyJs:

* npm
* pnpm
* yarn
* bun

```bash
npm install @visuallyjs/browser-ui

```

```bash
pnpm add @visuallyjs/browser-ui

```

```bash
yarn add @visuallyjs/browser-ui

```

```bash
bun add @visuallyjs/browser-ui

```

## Creating the diagram[​](#creating-the-diagram "Direct link to Creating the diagram")

### 1. Import components and CSS[​](#1-import-components-and-css "Direct link to 1. Import components and CSS")

The first step is to import `DiagramComponent`, `ControlsComponent`, `MiniviewComponent` and the VisuallyJs default stylesheet:

```jsx
import { DiagramComponent, ControlsComponent, MiniviewComponent } from "@visuallyjs/browser-ui-react"
import "@visuallyjs/browser-ui/css/visuallyjs.css"

```

### 2. Create your diagram[​](#2-create-your-diagram "Direct link to 2. Create your diagram")

At the minimum, we need to tell our `DiagramComponent` which shape sets you want to use:

```jsx
export default function MyApp() {
    return <div style={{width:"600px", height:"500px"}}>
        <DiagramComponent options={{
            shapes:[FLOWCHART_SHAPES]
        }}>
            <ControlsComponent/>
            <MiniviewComponent/>
        </DiagramComponent>
    </div>
}

```

This is the result - a blank canvas:

**********

### 3. Add shapes[​](#3-add-shapes "Direct link to 3. Add shapes")

Now we'll add some shapes. Note we also set `zoomToFit` so that after the data has been loaded the entire dataset is visible.

```jsx
export default function MyApp() {
    
  const data = {
    nodes:[
      { id:"1", label:"Start", x:100, y:50, type:"terminus", width:80, height:80, outline:"#000000", fill:"#ffffff"}, 
      { id:"2", label:"Decide", x:40, y:200, type:"decision", width:100, height:100, outline:"#000000", fill:"#ffffff"},
      { id:"3", label:"Yes Path", x:-150, y:250, type:"decision", width:100, height:100, outline:"#000000", fill:"#ffffff"}, 
      { id:"4", label:"No Path", x:150, y:450, type:"decision", width:100, height:100, outline:"#000000", fill:"#ffffff"},
    ],
    edges:[
      { source:"1", target:"2"}, 
      { source:"2", target:"3", data:{label:"Yes"}},
      { source:"2", target:"4", data:{label:"No"}}
    ]
  }

    return <div style={{width:"600px", height:"500px"}}>
        <DiagramComponent data={data} options={{
            shapes:[FLOWCHART_SHAPES],
            zoomToFit:true
        }}>
            <ControlsComponent/>
            <MiniviewComponent/>
        </DiagramComponent>
    </div>
}

```

This is the result. It's not bad, but those connector lines don't quite suit this type of diagram:

**********

### 4. Customise edges[​](#4-customise-edges "Direct link to 4. Customise edges")

Let's make a few updates to the edges in our diagram:

* We'll update the connectors to use an `Orthogonal` connector instead - consisting of horizontal and vertical line segments, and we'll tell VisuallyJs to use a `cornerRadius` on the connector, to make the corners rounded
* We'll set an `Arrow` as the target marker for our edges
* We'll instruct VisuallyJs to show a label on edges (which requires that the edge data has a `label` declared)

```jsx
<div style={{width:"600px", height:"500px"}}>
  <DiagramComponent data={data} options={{
    shapes:[FLOWCHART_SHAPES], 
    zoomToFit:true,
    edges:{
      connector: {
          type: "Orthogonal",
          options: {
              cornerRadius: 7
          }
      },
      targetMarker:"Arrow",
        showLabels:true  
    }
  }}>
    <ControlsComponent/>
    <MiniviewComponent/>
  </DiagramComponent>
</div>

```

**********

### 5. Resize/rotate[​](#5-resizerotate "Direct link to 5. Resize/rotate")

By default, a diagram is editable - try clicking on a shape in the canvas below. VisuallyJs attaches tools to the shape that allow you to resize, rotate, clone or delete a shape.

**********

You can switch off editing altogether via the `editable:false` option, or you can switch off rotation via `rotatable:false`.

### 6. Add a palette[​](#6-add-a-palette "Direct link to 6. Add a palette")

We'll add a palette from which users can drag new shapes onto the canvas. To do this we'll introduce a `DiagramProvider`, which is a context object that allows component to access a Diagram in scope, and then we'll use a `DiagramPaletteComponent`.

```jsx
<div style={{width:"600px", height:"500px", display:"flex"}}>
    <DiagramProvider>
      <DiagramPaletteComponent style={{ flex:"0 0 20%" }}/>
      <DiagramComponent style={{ flex:"0 0 80%" }} data={data} options={{
        shapes:[FLOWCHART_SHAPES], 
        zoomToFit:true,
        edges:{
          connector: {
            type: "Orthogonal",
            options: {
              cornerRadius: 7
            }
         },
         targetMarker:"Arrow",
         showLabels:true  
       }
      }}>
        <ControlsComponent/>
        <MiniviewComponent/>
      </DiagramComponent>
    </DiagramProvider>     
</div>

```

**********

## Next Steps[​](#next-steps "Direct link to Next Steps")

[Shapes](./shapes/overview)

[Read an in depth discussion of how to work with shapes in a diagram](./shapes/overview)

[Controlling diagram actions](./controlling-diagram-actions)

[Read about mediators, a simple but powerful means of controlling various diagram actions](./controlling-diagram-actions)
