# \<MiniviewComponent/>

Provides a miniaturized view of a surface, showing the nodes/groups in the surface canvas. Users can pan/zoom the surface via pointer/touch events on the miniview, and click on specific vertices to have the surface center itself on the clicked vertex.

## Usage[​](#usage "Direct link to Usage")

You need to have a `SurfaceComponent` in your app for `MiniviewComponent` to work. The miniview component will resolve the surface to attach to automatically, if your app has only a single surface in it (which is most apps). If your app has more than one surface, you will need to assign a `surfaceId` to each surface and miniview component.

```html
<SurfaceComponent ... />
<MiniviewComponent/>

```

## Lasso[​](#lasso "Direct link to Lasso")

By default, as a user drags the lasso on the main canvas to select elements, a corresponding lasso will appear in the miniview, showing the selection area in context of the overall diagram.

We've selected the lasso tool in this canvas - drag it around and you'll see the miniview displaying the lasso also.

**********

To disable this feature and prevent the lasso from being shown in the miniview, you can set `showLasso` to `false` in the miniview component's props:

```html
<SurfaceComponent ... />
<MiniviewComponent :showLasso="false"/>

```

## Selected vertices[​](#selected-vertices "Direct link to Selected vertices")

The miniview highlights vertices that are part of the current selection on the main canvas, by assigning the CSS class `.vjs-miniview-selected` to the elements representing these vertices in the miniview.

In this canvas, two nodes are initially selected, and are shown as highlighted in the miniview. Tap a node to set it as the current selection.

Being able to see the selected elements inside the miniview is particularly useful with large datasets, where one or more selected vertices may not currently be in the viewport. When someone lassos a large area and the canvas has been panned, it's helpful for them to be able to see everything that is currently selected.

This option defaults to `true`, meaning selection tracking is active by default. However, you can explicitly set `trackSelection` to `false` in the miniview's options if you wish to disable this behavior.

```html
<SurfaceComponent ... />
<MiniviewComponent :trackSelection="false"/>

```

## Props[​](#props "Direct link to Props")

MiniviewComponentProps

Supported props for the MiniviewComponent.

| Name            | Type    | Description                                                                                                                                                                                              |
| --------------- | ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| activeTracking? | boolean | Defaults to true, meaning the miniview will automatically track element dragging.                                                                                                                        |
| className?      | string  | Optional CSS to add to the container element for the miniview.                                                                                                                                           |
| clickToCenter?  | boolean | Defaults to true - a click on an element in the miniview will center the related element in the surface the<br />miniview is attached to.                                                                |
| showLasso?      | boolean | Defaults to true - the miniview will display a lasso as the user is using the lasso in the canvas                                                                                                        |
| surfaceId?      | string  | ID of the surface to attach to. This is optional; Visually JS will use the default surface ID if you do not<br />provide this. For apps where there's only one surface there is no need to provide this. |
| trackSelection? | boolean | Defaults to true - the miniview will add a CSS class to elements whose model object is in the current selection.                                                                                         |
