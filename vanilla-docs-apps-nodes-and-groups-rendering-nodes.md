# Rendering Nodes

<!-- -->

<!-- -->

In VisuallyJs, you render your nodes using HTML templates, which you map to node types via a set of [VanillaNodeMapping]() objects in `viewOptions` property on a `Surface`. You can map templates like this:

## Rendering with templates[​](#rendering-with-templates "Direct link to Rendering with templates")

```javascript
import { DEFAULT } from "@visuallyjs/browser-ui"

const viewOptions = {
  nodes:{
    [DEFAULT]:{
      view:'<div class="aNode">{{id}}</div>'
     },
    "type1":{
      view:`<div class="aNode">
        <h1>TYPE 1</h1>
        <p>{{id}}</p>
      </div>`
   }
  }
}

```

Here, nodes of type `type1` have their own mapping to a specific HTML template. Any other node type is mapped to the "default" mapping.

## Modular templates[​](#modular-templates "Direct link to Modular templates")

You do not need to use inline templates as shown in the example above; in fact a more modular approach is to define your HTML templates as strings separately and then map those. For instance, this is the HTML for the mockup workflow node in the node/group overview page:

```javascript
const introNodeTemplate = `
    <div class="workflow-node">
        <div class="node-header">
            <span class="node-type">TASK</span>
            <div class="node-status-dot"></div>
        </div>
        
        <div class="node-body">
            <div class="node-icon">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <path d="M12 2v20M2 12h20" />
                </svg>
            </div>
            <div class="node-label">
                {{label}}
            </div>
        </div>

        <div class="node-port"></div>
    </div>
`

```

and which we mapped like this:

```javascript
import { DEFAULT } from "@visuallyjs/browser-ui"

const viewOptions = {
  nodes:{
    [DEFAULT]:{
      view: introNodeTemplate
     }
    }
}

```

You can encapsulate as much behaviour as you like inside the templates you use to render your nodes.

## Accessing the context[​](#accessing-the-context "Direct link to Accessing the context")

You can access the underlying model, vertex and UI from inside your templates. For more complex logic, you can use the `onRender` callback:

```javascript
import { DEFAULT } from "@visuallyjs/browser-ui"

const viewOptions = {
    nodes:{
        [DEFAULT]:{
            view:'<div class="aNode"><button class="count-btn">Click me</button></div>',
            onRender:(ctx) => {
                ctx.el.querySelector('.count-btn').addEventListener('click', () => {
                     alert(`There are ${ctx.model.getNodes().length} nodes in the dataset. My ID is ${ctx.data.id}.`)
                })
            }
        }
    }
}

```

**********

The `ctx` member passed in to your `onRender` callback is of type `VanillaWrapperProps`:

Sorry - we could not find this document.

## Managing element size[​](#managing-element-size "Direct link to Managing element size")

The default behaviour of VisuallyJs is to render a <!-- -->node<!-- --> using whatever HTML is provided, and then after the element has been rendered, read back the size of the element from the DOM. For many types of applications this approach is really useful - you can draw whatever you like for your <!-- -->node<!-- -->s and VisuallyJs will figure out where any connected edges need to be placed, based on the size of the elements, which has been determined by their content and the CSS in your page.

In some applications, though, you'll want to give your users control over the size of <!-- -->node<!-- -->s, and VisuallyJs supports that too via the `useModelForSizes` rendering option.

### useModelForSizes[​](#usemodelforsizes "Direct link to useModelForSizes")

You can instruct VisuallyJs to extract `width` and `height` from your <!-- -->node<!-- --> data and to set the DOM element to these values, via the `useModelForSizes` flag:

```javascript
import { newInstance } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  useModelForSizes: true
})

```

VisuallyJs will now set the width and height of rendered DOM elements from the `width` and `height` properties in their data. When either of those values are updated, VisuallyJs will update the size of the DOM element accordingly.

### Default size[​](#default-size "Direct link to Default size")

If a given <!-- -->node<!-- --> does not have width or height values in its data, VisuallyJs will use a default value, which you can specify in one of two places - either the `defaults` section of some render options:

```javascript
import { newInstance } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  useModelForSizes: true,
  defaults: {
    nodeSize: {
      width: 150,
      height: 100
    }
  }
})

```

<!-- -->

or inside a <!-- -->node<!-- --> definition in the view:

```javascript
import { newInstance, DEFAULT } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  useModelForSizes: true,
  defaults: {
    nodeSize: {
      width: 150,
      height: 100
    }
  },
  view: {
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
})

```

<!-- -->

You can in fact provide values in both places - as shown above - and VisuallyJs will use the values from a <!-- -->node<!-- --> definition first. <!-- -->In the above example we see that `type1` has no default size set, so VisuallyJs will use `nodeSize` from the defaults block.<!-- -->

In the absence of any default values, VisuallyJs will <!-- -->render nodes with width 100 pixels and height 80 pixels<!-- -->.
