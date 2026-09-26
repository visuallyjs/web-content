# Rendering Nodes

<!-- -->

<!-- -->

In VisuallyJs, you render your nodes using Angular components, which you map to node types via a set of [AngularNodeMapping]() objects in `viewOptions` prop on a `SurfaceComponent`. You can map components like this:

## Mapping components[​](#mapping-components "Direct link to Mapping components")

```typescript
import { DEFAULT } from "@visuallyjs/browser-ui"
import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular"
import { MyNodeComponent } from "./my-node.component"
import { Type1NodeComponent } from "./type1-node.component"

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [VisuallyJsModule],
  template: `<vjs-surface [viewOptions]="viewOptions"/>`
})
export class MyAppComponent {
  viewOptions = {
    nodes: {
      [DEFAULT]: {
        component: MyNodeComponent
      },
      "type1": {
        component: Type1NodeComponent
      }
    }
  }
}

```

Here, nodes of type `type1` are mapped to `Type1NodeComponent`. Any other node type is mapped to the "default" mapping, which uses `MyNodeComponent`.

## Creating a component[​](#creating-a-component "Direct link to Creating a component")

Every component used to render a node must extend `BaseNodeComponent` from `@visuallyjs/browser-ui-angular`. This base class exposes a `data` member and a `$data` signal, which provide access to the underlying node data.

A typical node component looks like this:

**my-node.component.ts**

```typescript
import { Component } from "@angular/core"
import { BaseNodeComponent } from "@visuallyjs/browser-ui-angular"

@Component({
  templateUrl: './my-node.component.html'
})
export class MyNodeComponent extends BaseNodeComponent {
  // Your component logic here
}

```

**my-node.component.html**

```html
<div class="aNode">
  {{ data.id }}
</div>

```

For instance, this is the component for the mockup workflow node in the node/group overview page:

**intro-node.component.ts**

```typescript
import { Component } from "@angular/core"
import { BaseNodeComponent } from "@visuallyjs/browser-ui-angular"

@Component({
  templateUrl: './intro-node.component.html'
})
export class IntroNodeComponent extends BaseNodeComponent { }

```

**intro-node.component.html**

```html
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
            {{ $data().label || "New Task" }}
        </div>
    </div>

    <div class="node-port"></div>
</div>

```

...which - with a dash of CSS - looks like this:

**********

and which we mapped like this:

```typescript
import { DEFAULT } from "@visuallyjs/browser-ui"
import { IntroNodeComponent } from "./intro-node.component"

const viewOptions = {
  nodes: {
    [DEFAULT]: {
      component: IntroNodeComponent
    }
  }
}

```

You can encapsulate as much behaviour as you like inside the components you use to render your nodes.

## Accessing the context[​](#accessing-the-context "Direct link to Accessing the context")

You can access the underlying model, vertex and UI from inside your component. The `BaseNodeComponent` provides access to the model instance and the surface instance, among other things:

**context-node.component.ts**

```typescript
import { Component } from "@angular/core"
import { BaseNodeComponent } from "@visuallyjs/browser-ui-angular"

@Component({
  template: `
    <div>
        <button (click)="countNodes()">Click me</button>
    </div>
  `
})
export class ContextNodeComponent extends BaseNodeComponent {
    countNodes() {
        alert(`There are ${this.model.getNodes().length} nodes in the dataset. My ID is ${this.data.id}.`)
    }
}

```

**********

***

## Rendering content based on zoom[​](#rendering-content-based-on-zoom "Direct link to Rendering content based on zoom")

You might want to show more detail when zoomed in and less detail when zoomed out. VisuallyJs exposes a signal called `zoom()` on `BaseVertexComponent` to assist you with this.

```html
@if (zoom() > 1.5) {
  <div class="details">
    <!-- Detailed information shown only when zoomed in -->
    <p>{{ data.description }}</p>
  </div>
}

```

You can also use it within your component class for computed properties or effects:

```typescript
import { Component, computed } from '@angular/core';
import { BaseNodeComponent } from '@visuallyjs/browser-ui-angular';

@Component({ ... })
export class MyCustomNode extends BaseNodeComponent {
  isZoomedIn = computed(() => this.zoom() > 2);
}

```

<!-- -->

***

## Node helper methods[​](#node-helper-methods "Direct link to Node helper methods")

`BaseNodeComponent` exposes a number of helper methods you can use to manipulate the model from inside your component:

### Class Members[​](#class-members "Direct link to Class Members")

| Name                                               | Type                           | Description                                                                                                                                                                                      |
| -------------------------------------------------- | ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| $data                                              | WritableSignal<[ObjectData]()> | This signal represents the underlying data for the vertex this component represents.                                                                                                             |
| data                                               | [ObjectData]()                 | Data object for the vertex                                                                                                                                                                       |
| zoom                                               | WritableSignal\<number>        | This is a signal that provides the current zoom for the canvas the component is in. You can use this to selectively hide/show content based upon the zoom level.                                 |
| addNewPort(type:string, data:[ObjectData]())       | void                           | Instructs the model to add a new port with the given data to the vertex this component represents. This will call the model's `portFactory`.                                                     |
| addPort(data:[ObjectData]())                       | [Port]()                       | Adds a port with the given data to the vertex this component represents.                                                                                                                         |
| addToSelection()                                   | void                           | Adds the vertex this component represents to the current selection in the model.                                                                                                                 |
| cloneNode(options:[SurfaceVertexCloneOptions]())   | void                           | Instructs the model to clone this node - a new node which is a copy of this one will be added to the UI, with a position shifted slightly in X and Y from the cloned node.                       |
| cloneVertex(options:[SurfaceVertexCloneOptions]()) | void                           | Clones this vertex, optionally setting to a given position, or offsetting from the original, and optionally magnetizing the new vertex's position, and flashing it to show the user where it is. |
| flashNode(duration:number, animName:string)        | void                           | Flash this Node                                                                                                                                                                                  |
| getNode()                                          | [Node]()                       | Gets the node that this component represents.                                                                                                                                                    |
| getPort(portId:string)                             | [Port]()                       | Gets the port with the given ID                                                                                                                                                                  |
| getVertex()                                        | [Node]()                       | Gets the vertex that this component represents. Subclasses have getters that return more specific subclasses of Vertex.                                                                          |
| removeFromSelection()                              | void                           | Removes the vertex this component represents from the current selection in the model.                                                                                                            |
| removeNode()                                       | void                           | Shortcut method to remove the node (and therefore this whole component)                                                                                                                          |
| removePort(portId:string)                          | void                           | Removes the port with the given id.                                                                                                                                                              |
| removeVertex()                                     | void                           | Removes the vertex this component represents from the data model, which will cause this component to be cleaned up.                                                                              |
| setAsSelection()                                   | void                           | Sets the vertex this component represents as the current selection in the model.                                                                                                                 |
| updateNode(data:[ObjectData]())                    | void                           | Shortcut method to update the current data backing this node, for convenience.                                                                                                                   |
| updateVertex(data:[ObjectData]())                  | void                           | Shortcut method to update the current data backing this vertex, for convenience.                                                                                                                 |

***

## Managing element size[​](#managing-element-size "Direct link to Managing element size")

The default behaviour of VisuallyJs is to render a <!-- -->node<!-- --> using whatever HTML is provided, and then after the element has been rendered, read back the size of the element from the DOM. For many types of applications this approach is really useful - you can draw whatever you like for your <!-- -->node<!-- -->s and VisuallyJs will figure out where any connected edges need to be placed, based on the size of the elements, which has been determined by their content and the CSS in your page.

In some applications, though, you'll want to give your users control over the size of <!-- -->node<!-- -->s, and VisuallyJs supports that too via the `useModelForSizes` rendering option.

### useModelForSizes[​](#usemodelforsizes "Direct link to useModelForSizes")

You can instruct VisuallyJs to extract `width` and `height` from your <!-- -->node<!-- --> data and to set the DOM element to these values, via the `useModelForSizes` flag:

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  useModelForSizes: true
};
}

```

VisuallyJs will now set the width and height of rendered DOM elements from the `width` and `height` properties in their data. When either of those values are updated, VisuallyJs will update the size of the DOM element accordingly.

### Default size[​](#default-size "Direct link to Default size")

If a given <!-- -->node<!-- --> does not have width or height values in its data, VisuallyJs will use a default value, which you can specify in one of two places - either the `defaults` section of some render options:

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  useModelForSizes: true,
  defaults: {
    nodeSize: {
      width: 150,
      height: 100
    }
  }
};
}

```

<!-- -->

or inside a <!-- -->node<!-- --> definition in the view:

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';
import { DEFAULT } from "@visuallyjs/browser-ui"


@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions" [viewOptions]="viewOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  useModelForSizes: true,
  defaults: {
    nodeSize: {
      width: 150,
      height: 100
    }
  }
};
  viewOptions = {
  nodes: {
    [DEFAULT]: {
      defaultSize: {
        width: 150,
        height: 100
      }
    },
    type1: {}
  }
};
}

```

<!-- -->

You can in fact provide values in both places - as shown above - and VisuallyJs will use the values from a <!-- -->node<!-- --> definition first. <!-- -->In the above example we see that `type1` has no default size set, so VisuallyJs will use `nodeSize` from the defaults block.<!-- -->

In the absence of any default values, VisuallyJs will <!-- -->render nodes with width 100 pixels and height 80 pixels<!-- -->.
