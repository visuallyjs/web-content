ZoomToElementsOptions

Options for the zoomToElements method.

| Name                | Type                   | Description                                                                                                                                                                                                            |
| ------------------- | ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| doNotAnimate?       | boolean                | If true, don't animate while zooming. Defaults to false, ie. the operation will be animated.                                                                                                                           |
| doNotZoomIfVisible? | boolean                | If the content is all already visible, do not make any changes to zoom.                                                                                                                                                |
| elements            | Array\<EL>             | Array of elements to zoom to                                                                                                                                                                                           |
| fill?               | number                 | A decimal between 0 and 1, which indicates how much of the viewport size the content will take up. This value is applied as a ratio of the width or height of the viewport - whichever is smaller. The default is 0.9. |
| onComplete?         | (p:[PointXY]()) => any | Optional function to call on operation complete.                                                                                                                                                                       |
