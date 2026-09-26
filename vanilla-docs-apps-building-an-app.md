# Building an App

On this page we'll run through how to build a basic app with VisuallyJs - we'll be creating the app from the [Overview](/vanilla/docs/apps.md) page, from the initial setup of the app with a couple of helper components, to the addition of nodes and groups and edges, and then we'll provide some suggestions for where you may wish to go next.

Note that in this example we're providing you the basics of how to render groups, but not every app needs groups of course.

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

## Creating the app[​](#creating-the-app "Direct link to Creating the app")

### 1. Import components and CSS[​](#1-import-components-and-css "Direct link to 1. Import components and CSS")

The first step is to import `SurfaceComponent`, `ControlsComponent`, `MiniviewComponent` and the VisuallyJs default stylesheet:

```jsx
import { SurfaceComponent, ControlsComponent, MiniviewComponent } from "@visuallyjs/browser-ui-react"
import "@visuallyjs/browser-ui/css/visuallyjs.css"

```

### 2. Create your component[​](#2-create-your-component "Direct link to 2. Create your component")

```jsx
export default function MyApp() {
    return <div style={{width:"600px", height:"500px"}}>
        <SurfaceComponent>
            <ControlsComponent/>
            <MiniviewComponent/>
        </SurfaceComponent>
    </div>
}

```

This is the result - a blank canvas:

**********

### 3. Add nodes and group[​](#3-add-nodes-and-group "Direct link to 3. Add nodes and group")

Now we'll add the nodes and the group. Notice how the node `3` declares that it belongs to group `g1`.

```jsx
export default function MyApp() {
    
    const data = {
        nodes:[
            { id:"1", label:"Node", left:50, top:30 },
            { id:"2", label:"Node", left:50, top:200 },
            { id:"3", label:"Node", left:50, top:30, group:"g1" }
        ],
        groups:[
            { id:"g1", left:280, top:30, label:"Group" }
        ]
    }
    
    return <div style={{width:"600px", height:"500px"}}>
        <SurfaceComponent data={data}>
            <ControlsComponent/>
            <MiniviewComponent/>
        </SurfaceComponent>
    </div>
}

```

**********

info

Our nodes/groups have a `left` and `top` property, which defines their position. This is the default setup, in which VisuallyJs uses an [Absolute layout](/vanilla/docs/apps/layouts/absolute.md). But VisuallyJs ships with a number of different layouts you can use to automatically position your elements - you can read about them in the [layouts docs](/vanilla/docs/apps/layouts/overview.md). For node `3`, the left and top values define the node's position with respect to its parent group.

### 4. Customise nodes and group[​](#4-customise-nodes-and-group "Direct link to 4. Customise nodes and group")

So far we've got a basic surface up and running and we're rendering our nodes and groups using some default JSX. But the real power of VisuallyJs apps comes when you supply the JSX to render nodes/groups yourself. To do that, we're going to declare a `viewOptions` object, into which we're going to set a mapping for nodes of type "default". The mapping provides the JSX to use to render the node:

```jsx
import {SurfaceComponent, ControlsComponent, MiniviewComponent} from "@visuallyjs/browser-ui-react";

export default function MyApp() {

    const data = {...}

    const viewOptions = {
        nodes: {
            default: {
                jsx: (ctx: JsxWrapperProps) => <div className="my-node">
                    <span>{ctx.data.label} {ctx.data.id}</span>
                </div>
            }
        },
        groups: {
            default: {
                constrain:true,
                jsx: (ctx: JsxWrapperProps) => <div className="my-group">
                    <strong>{ctx.data.label} {ctx.data.id}</strong>
                    <div data-vjs-group-content={true}/>
                </div>
            }
        }
    }

    return <div style={{width: "600px", height: "500px"}}>
        <SurfaceComponent data={data}>
            <ControlsComponent/>
            <MiniviewComponent/>
        </SurfaceComponent>
    </div>
}

```

**********

The key piece to note here is the `ctx` object which is passed in to the JSX you provide - it contains information about the vertex that is being rendered, as well as the UI rendering it, and the underlying model. This object is of type [JsxWrapperProps]().

#### Notes about styling[​](#notes-about-styling "Direct link to Notes about styling")

In our code snippet above we do not show the specific styles used for the nodes/group - they are set by the underlying CSS, and can be anything at all. VisuallyJs will automatically adapt to whatever dimensions the objects in your UI end up having.

#### Notes about the group[​](#notes-about-the-group "Direct link to Notes about the group")

There are a couple of things to take note of regarding the group mapping in the above code snippet:

* We declared `constrain:true` on the group mapping. This instructs VisuallyJs that children of the group cannot be dragged outside of the group. There are a number of related flags controlling child content - see the [groups](/vanilla/docs/apps/nodes-and-groups/groups.md) page for a thorough discussion.
* Inside our group's markup we declared a `div` that has `data-vjs-group-content="true"` set on it. This is an optional mechanism you can use to tell VisuallyJs what part of your group nodes should act as the container for child nodes/groups. It allows you great flexibility in creating the UI representing groups in your data model.

### 5. Add edges[​](#5-add-edges "Direct link to 5. Add edges")

To add edges to our app, we add them in to the `data` object we created above:

```jsx
const data = {
    nodes:[ ... ],
    edges:[
        { source:"1", target:"2" }
    ]
}

```

**********

### 6. Customise edges[​](#6-customise-edges "Direct link to 6. Customise edges")

Our new edge uses the default settings - it's a straight line, it's anchored on each node on the face that is closest to the other node, and it has no overlays. We can update the `viewOptions` to include an edge definition:

```jsx
const viewOptions = {
  nodes:{ ... }, 
  edges:{
      default:{
          overlays:[
              { 
                  type:ArrowOverlay.type,
                  options:{
                      location:1
                  }
              }
          ]
      }
  }
}

```

**********

Here, we've added an `Arrow` overlay, but there are many configuration options for edges - we'd recommend taking a look through the [edge documentation](/vanilla/docs/apps/edges/overview.md) for a thorough discussion.

## Next Steps[​](#next-steps "Direct link to Next Steps")

[Adding Interactivity](adding-interactivity)

[Add support for dragging edges, responding to events, and more](adding-interactivity)

[Layouts](layouts/overview)

[Read about the available layouts in VisuallyJs](layouts/overview)

[Nodes](nodes)

[Read about everything you can do with nodes](nodes)

[Groups](groups)

[Read about everything you can do with groups](groups)

[Edges](edges/overview)

[Read about everything you can do with edges](edges/overview)
