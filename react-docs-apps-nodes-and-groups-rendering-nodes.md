# Rendering Nodes

<!-- -->

<!-- -->

In VisuallyJs, you render your nodes using React components, which you map to node types via a set of [ReactNodeMapping]() objects in `viewOptions` prop on a `SurfaceComponent`. You can map JSX directly inside the view like this:

## Rendering with JSX[​](#rendering-with-jsx "Direct link to Rendering with JSX")

```jsx

import { DEFAULT } from "@visuallyjs/browser-ui"
import { SurfaceComponent, JsxWrapperProps } from "@visuallyjs/browser-ui-react"

export default function MyAppComponent() {
  const viewOptions = {
    nodes:{
      [DEFAULT]:{
        jsx:(ctx:JsxWrapperProps) => <div className="aNode">{ctx.data.id}</div>
       }
      },
      "type1":{
        jsx:(ctx:JsxWrapperProps) => <div className="aNode">
          <h1>TYPE 1</h1>
          <p>{ctx.data.id}</p>
        </div>
     }
    }
  }
    
    return <div><SurfaceComponent viewOptions={viewOptions}/></div>
}


```

Here, nodes of type `type1` have their own mapping to a specific piece of JSX. Any other node type is mapped to the "default" mapping, which declares some other JSX. Any valid JSX is supported.

## Rendering with React components[​](#rendering-with-react-components "Direct link to Rendering with React components")

You do not need to use inline JSX as shown in the example above; in fact a more modular approach is to define JSX components separately and then map those. For instance, this is the JSX for the mockup workflow node in the node/group overview page:

```jsx

export function IntroNode({ctx}) {
    return <div className="workflow-node">
        <div className="node-header">
            <span className="node-type">TASK</span>
            <div className="node-status-dot"></div>
        </div>
        
        <div className="node-body">
            <div className="node-icon">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2">
                    <path d="M12 2v20M2 12h20" />
                </svg>
            </div>
            <div className="node-label">
                {ctx.data.label || "New Task"}
            </div>
        </div>

        <div className="node-port"></div>
    </div>
}

```

...which - with a dash of CSS - looks like this:

**********

and which we mapped like this:

```jsx

import { DEFAULT } from "@visuallyjs/browser-ui"
import { SurfaceComponent, JsxWrapperProps } from "@visuallyjs/browser-ui-react"
import IntroNode from "./IntroNode"

export default function MyAppComponent() {
  const viewOptions = {
    nodes:{
      [DEFAULT]:{
        jsx:(ctx:JsxWrapperProps) => <IntroNode ctx={ctx}/>
       }
      }
    }
  }
    
    return <div><SurfaceComponent viewOptions={viewOptions}/></div>
}

```

You can encapsulate as much behaviour as you like inside the components you use to render your nodes.

## Accessing the context[​](#accessing-the-context "Direct link to Accessing the context")

You can access the underlying model, vertex and UI from inside your JSX via the `ctx`. This is an object of type [VisuallyJsModel]()

```jsx

import { DEFAULT } from "@visuallyjs/browser-ui"
import { SurfaceComponent, JsxWrapperProps } from "@visuallyjs/browser-ui-react"
import IntroNode from "./IntroNode"

export default function MyAppComponent() {
    
  function countNodes(ctx) {
    alert(`There are ${ctx.model.getNodes().length} nodes in the dataset. My ID is ${ctx.data.id}.`)
  }
    
  const viewOptions = {
    nodes:{
      [DEFAULT]:{
        jsx:(ctx):JsxWrapperProps => <div>
            <button onClick={() => countNodes(ctx)}>Click me</button>
        </div>
       }
      }
    }
  }
    
    return <div><SurfaceComponent viewOptions={viewOptions}/></div>
}

```

**********

The `ctx` member passed in to your jsx is of type `JsxWrapperProps`:

JsxWrapperProps

These are the props that are passed to the `jsx` you provide to map a node, group or overlay component in the `viewOptions` of a SurfaceComponent or PaperComponent. VisuallyJs passes in the UI, the model (which you can get from the UI anyway), the object being rendered, the object's data, and any `childProps` that have been configured.

| Name   | Type               | Description                                                                                           |
| ------ | ------------------ | ----------------------------------------------------------------------------------------------------- |
| data   | [ObjectData]()     | The object's backing data                                                                             |
| model  | [BrowserUIModel]() | Underlying model. Can also be accessed via `ui.model`.                                                |
| obj    | T                  | The object to be rendered - a Node, Group or Edge.                                                    |
| props  | any                | Any extra props configured by the view to present to this JSX.                                        |
| ui     | [BrowserUI]()      | The UI that is rendering this object.                                                                 |
| vertex | T                  | The object to be rendered - a Node, Group or Edge. Use this in preference to `obj` from 1.2.0 onwards |

## Rendering content based on zoom[​](#rendering-content-based-on-zoom "Direct link to Rendering content based on zoom")

You might want to show more detail when zoomed in and less detail when zoomed out. VisuallyJs provides a `useZoom` hook to assist you with this.

```tsx
import { useZoom } from '@visuallyjs/browser-ui-react';

export default function ZoomDisplay({ ui, obj, model }) {
  const zoom = useZoom(ui);

  return (
    <div style={{ position: 'absolute', top: 10, left: 10, background: 'white', padding: '5px' }}>
      Current Zoom: {(zoom * 100).toFixed(0)}%
      {zoom > 1.5 && <p>High magnification active</p>}
      {zoom < 0.5 && <p>Low magnification active</p>}
    </div>
  );
}

```

## Managing element size[​](#managing-element-size "Direct link to Managing element size")

The default behaviour of VisuallyJs is to render a <!-- -->node<!-- --> using whatever HTML is provided, and then after the element has been rendered, read back the size of the element from the DOM. For many types of applications this approach is really useful - you can draw whatever you like for your <!-- -->node<!-- -->s and VisuallyJs will figure out where any connected edges need to be placed, based on the size of the elements, which has been determined by their content and the CSS in your page.

In some applications, though, you'll want to give your users control over the size of <!-- -->node<!-- -->s, and VisuallyJs supports that too via the `useModelForSizes` rendering option.

### useModelForSizes[​](#usemodelforsizes "Direct link to useModelForSizes")

You can instruct VisuallyJs to extract `width` and `height` from your <!-- -->node<!-- --> data and to set the DOM element to these values, via the `useModelForSizes` flag:

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

export default function MyComponent() {

  const renderOptions = {
  useModelForSizes: true
}
  return <SurfaceComponent renderOptions={renderOptions}/>
}

```

VisuallyJs will now set the width and height of rendered DOM elements from the `width` and `height` properties in their data. When either of those values are updated, VisuallyJs will update the size of the DOM element accordingly.

### Default size[​](#default-size "Direct link to Default size")

If a given <!-- -->node<!-- --> does not have width or height values in its data, VisuallyJs will use a default value, which you can specify in one of two places - either the `defaults` section of some render options:

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

export default function MyComponent() {

  const renderOptions = {
  useModelForSizes: true,
  defaults: {
    nodeSize: {
      width: 150,
      height: 100
    }
  }
}
  return <SurfaceComponent renderOptions={renderOptions}/>
}

```

<!-- -->

or inside a <!-- -->node<!-- --> definition in the view:

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

import { DEFAULT } from "@visuallyjs/browser-ui"

export default function MyComponent() {

  const renderOptions = {
  useModelForSizes: true,
  defaults: {
    nodeSize: {
      width: 150,
      height: 100
    }
  }
}

  const viewOptions = {
  nodes: {
    [DEFAULT]: {
      defaultSize: {
        width: 150,
        height: 100
      }
    },
    type1: {}
  }
}
  return <SurfaceComponent renderOptions={renderOptions} viewOptions={viewOptions}/>
}

```

<!-- -->

You can in fact provide values in both places - as shown above - and VisuallyJs will use the values from a <!-- -->node<!-- --> definition first. <!-- -->In the above example we see that `type1` has no default size set, so VisuallyJs will use `nodeSize` from the defaults block.<!-- -->

In the absence of any default values, VisuallyJs will <!-- -->render nodes with width 100 pixels and height 80 pixels<!-- -->.
