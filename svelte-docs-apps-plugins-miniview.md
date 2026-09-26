# Miniview

Provides a miniaturized view of a surface, showing the nodes/groups in the surface canvas. Users can pan/zoom the surface via pointer/touch events on the miniview, and click on specific vertices to have the surface center itself on the clicked vertex.

## Usage[​](#usage "Direct link to Usage")

This component is context aware and will discover the Surface to attach itself to if it is a child of a [SurfaceProvider](/svelte/docs/reference/SurfaceProvider.md):

```html
<SurfaceComponent renderOptions={...} data={...}>
    <MiniviewComponent />
</SurfaceComponent>

```

or if it is a descendant of a [SurfaceProvider](/svelte/docs/reference/SurfaceProvider.md):

```html
<SurfaceProvider>
    <SurfaceComponent renderOptions={...} data={...}/>
    <div class="someContainer">
        <MiniviewComponent/>
    </div>
</SurfaceProvider>

```

## Lasso[​](#lasso "Direct link to Lasso")

By default, as a user drags the lasso on the main canvas to select elements, a corresponding lasso will appear in the miniview, showing the selection area in context of the overall diagram.

We've selected the lasso tool in this canvas - drag it around and you'll see the miniview displaying the lasso also.

**********

To disable this feature and prevent the lasso from being shown in the miniview, you can set `showLasso` to `false` in the miniview component's props:

```html
<SurfaceProvider>
  <SurfaceComponent {renderOptions} {data}/>
  <div class="someContainer">
    <MiniviewComponent showLasso={false}/>
  </div>
</SurfaceProvider>

```

## Selected vertices[​](#selected-vertices "Direct link to Selected vertices")

The miniview highlights vertices that are part of the current selection on the main canvas, by assigning the CSS class `.vjs-miniview-selected` to the elements representing these vertices in the miniview.

In this canvas, two nodes are initially selected, and are shown as highlighted in the miniview. Tap a node to set it as the current selection.

Being able to see the selected elements inside the miniview is particularly useful with large datasets, where one or more selected vertices may not currently be in the viewport. When someone lassos a large area and the canvas has been panned, it's helpful for them to be able to see everything that is currently selected.

This option defaults to `true`, meaning selection tracking is active by default. However, you can explicitly set `trackSelection` to `false` in the miniview's options if you wish to disable this behavior.

```html
<SurfaceProvider>
    <SurfaceComponent {renderOptions} {data}/>
    <div class="someContainer">
      <MiniviewComponent trackSelection={false}/>
    </div>
</SurfaceProvider>

```

## Props[​](#props "Direct link to Props")

MiniviewComponentProps

| Name              | Type                                | Description                                                                                                                                                                                                   |
| ----------------- | ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| activeTracking?   | boolean                             | Defaults to true, meaning the miniview actively updates as nodes/groups are dragged on the related surface. If this is set to false, the miniview only updates after mouseup.                                 |
| className?        | string                              | Optional class name to set on the miniview component's container                                                                                                                                              |
| clickToCenter?    | boolean                             | Defaults to true, meaning a click on a node/group in the miniview will cause that node/group to be centered in the related surface.                                                                           |
| collapsible?      | boolean                             | Defaults to true, determines whether or not the miniview can be collapsed.                                                                                                                                    |
| elementFilter?    | (v:[Vertex]()) => boolean           | Optional filter for elements to display. Defaults to undefined - all elements displayed.                                                                                                                      |
| enableWheelZoom?  | boolean                             | Defaults to true, Whether or not to enable the wheel zoom.                                                                                                                                                    |
| showLasso?        | boolean                             | Defaults to true - the miniview will display a lasso as the user is using the lasso in the canvas                                                                                                             |
| trackSelection?   | boolean                             | Defaults to true - the miniview will add a CSS class to elements whose model object is in the current selection.                                                                                              |
| typeFunction?     | (v:[Node]() \| [Group]()) => string | Optional function to use to derive a type for each rendered node/group. This is written onto the corresponding element as the value of the `data-vjs-miniview-type` attribute, and can be useful for styling. |
| visible?          | boolean                             | Defaults to true. Whether or not the miniview is initially visible.                                                                                                                                           |
| wheelReverse?     | boolean                             | Defaults to false. Whether or not to reverse the zoom direction in response to a wheel event.                                                                                                                 |
| wheelSensitivity? | number                              | Optional override for how sensitive the wheel zoom should be.                                                                                                                                                 |
