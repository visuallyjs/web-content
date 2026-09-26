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
