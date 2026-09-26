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
