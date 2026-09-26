# Miniview

Provides a miniaturized view of a surface, showing the nodes/groups in the surface canvas. Users can pan/zoom the surface via pointer/touch events on the miniview, and click on specific vertices to have the surface center itself on the clicked vertex.

## Usage[​](#usage "Direct link to Usage")

This component is context aware and will discover the Surface to attach itself to if it is a child of a [SurfaceComponent](/react/docs/reference/SurfaceComponent.md):

```jsx
<SurfaceComponent renderOptions={...} data={...}>
    <MiniviewComponent />
</SurfaceComponent>

```

or if it is a descendant of a [SurfaceProvider](/react/docs/reference/SurfaceProvider.md):

```jsx
<SurfaceProvider>
    <SurfaceComponent renderOptions={...} data={...}/>
    <div className="someContainer">
        <MiniviewComponent/>
    </div>
</SurfaceProvider>

```

## Lasso[​](#lasso "Direct link to Lasso")

By default, as a user drags the lasso on the main canvas to select elements, a corresponding lasso will appear in the miniview, showing the selection area in context of the overall diagram.

We've selected the lasso tool in this canvas - drag it around and you'll see the miniview displaying the lasso also.

**********

To disable this feature and prevent the lasso from being shown in the miniview, you can set `showLasso` to `false` in the miniview component's props:

```jsx
<SurfaceProvider>
    <SurfaceComponent renderOptions={...} data={...}/>
    <div className="someContainer">
        <MiniviewComponent showLasso={false}/>
    </div>
</SurfaceProvider>

```

## Selected vertices[​](#selected-vertices "Direct link to Selected vertices")

The miniview highlights vertices that are part of the current selection on the main canvas, by assigning the CSS class `.vjs-miniview-selected` to the elements representing these vertices in the miniview.

In this canvas, two nodes are initially selected, and are shown as highlighted in the miniview. Tap a node to set it as the current selection.

Being able to see the selected elements inside the miniview is particularly useful with large datasets, where one or more selected vertices may not currently be in the viewport. When someone lassos a large area and the canvas has been panned, it's helpful for them to be able to see everything that is currently selected.

This option defaults to `true`, meaning selection tracking is active by default. However, you can explicitly set `trackSelection` to `false` in the miniview's options if you wish to disable this behavior.

```jsx
<SurfaceProvider>
    <SurfaceComponent {renderOptions} {data}/>
    <div className="someContainer">
        <MiniviewComponent trackSelection={false}/>
    </div>
</SurfaceProvider>

```

## Props[​](#props "Direct link to Props")

MiniviewComponentProps

Props for the MiniviewComponent.

| Name            | Type                                   | Description                                                                                                                         |
| --------------- | -------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| activeTracking? | boolean                                | Whether or not to move miniview elements at the same time as their related surface element is being dragged. Defaults to true.      |
| className?      | string                                 | Optional class name to append to the root element's class list.                                                                     |
| clickToCenter?  | boolean                                | Defaults to true, meaning a click on a node/group in the miniview will cause that node/group to be centered in the related surface. |
| elementFilter?  | (obj:[Group]() \| [Node]()) => boolean | Optional filter to decide which elements to show in the miniview.                                                                   |
| showLasso?      | boolean                                | Defaults to true - the miniview will display a lasso as the user is using the lasso in the canvas                                   |
| trackSelection? | boolean                                | Defaults to true - the miniview will add a CSS class to elements whose model object is in the current selection.                    |
| typeFunction?   | (obj:[Group]() \| [Node]()) => string  | Optional function to use to decorate miniview elements with a `vjs-miniview-type` attribute. Can be used for simple styling.        |
