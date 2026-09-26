# Miniview

HTML Tag

**vjs-miniview**

Provides a miniaturized view of a surface, showing the nodes/groups in the surface canvas. Users can pan/zoom the surface via pointer/touch events on the miniview, and click on specific vertices to have the surface center itself on the clicked vertex.

## Usage[​](#usage "Direct link to Usage")

This component has the underlying `VisuallyJsService` injected, and in applications that contain only a single surface component (which is most), the miniview component can automatically resolve the surface component to attach to, regardless of their relationship in the DOM. You must, of course, have declared a surface component in your template in order for the miniview component to work.

```typescript

import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular"

@Component({
    template:`<div>
        <vjs-surface [renderOptions]="renderOptions" [data]="data"/>
        <vjs-miniview />
        </div>`
})
export class MyApp {
    renderOptions = { ... }
    data = { ... }
}


```

## Lasso[​](#lasso "Direct link to Lasso")

By default, as a user drags the lasso on the main canvas to select elements, a corresponding lasso will appear in the miniview, showing the selection area in context of the overall diagram.

We've selected the lasso tool in this canvas - drag it around and you'll see the miniview displaying the lasso also.

**********

To disable this feature and prevent the lasso from being shown in the miniview, you can set `showLasso` to `false` in the miniview component's inputs:

```typescript

import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular"

@Component({
    template:`<div>
        <vjs-surface [renderOptions]="renderOptions" [data]="data"/>
        <vjs-miniview [showLasso]="false"/>
        </div>`
})
export class MyApp {
    renderOptions = { ... }
    data = { ... }
}


```

## Selected vertices[​](#selected-vertices "Direct link to Selected vertices")

The miniview highlights vertices that are part of the current selection on the main canvas, by assigning the CSS class `.vjs-miniview-selected` to the elements representing these vertices in the miniview.

In this canvas, two nodes are initially selected, and are shown as highlighted in the miniview. Tap a node to set it as the current selection.

Being able to see the selected elements inside the miniview is particularly useful with large datasets, where one or more selected vertices may not currently be in the viewport. When someone lassos a large area and the canvas has been panned, it's helpful for them to be able to see everything that is currently selected.

This option defaults to `true`, meaning selection tracking is active by default. However, you can explicitly set `trackSelection` to `false` in the miniview's options if you wish to disable this behavior.

```typescript

import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular"

@Component({
    template:`<div>
        <vjs-surface [renderOptions]="renderOptions" [data]="data"/>
        <vjs-miniview [trackSelection]="false"/>
        </div>`
})
export class MyApp {
    renderOptions = { ... }
    data = { ... }
}


```

## Definition[​](#definition "Direct link to Definition")

### Inputs[​](#inputs "Direct link to Inputs")

| Name            | Type                                  | Description                                                                                                                                                  |
| --------------- | ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| activeTracking? | boolean                               | Whether or not to move miniview elements at the same time as their related surface element is being dragged. Defaults to true.                               |
| clickToCenter?  | boolean                               | Defaults to true, meaning a click on a node/group in the miniview will cause that node/group to be centered in the related surface.                          |
| elementFilter?  | (obj:[Vertex]()) => boolean           | Optional filter to determine whether or not include a given vertex in the miniview                                                                           |
| showLasso?      | boolean                               | Defaults to true - the miniview will display a lasso as the user is using the lasso in the canvas                                                            |
| trackSelection? | boolean                               | Defaults to true - the miniview will add a CSS class to elements whose model object is in the current selection.                                             |
| typeFunction?   | (obj:[Node]() \| [Group]()) => string | Optional function to determine a `type` for each vertex, which is then written as an attribute onto the DOM element representing the vertex in the miniview. |
