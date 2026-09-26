ZoomToFitOptions

Options for the zoomToFit method.

| Name                | Type                   | Description                                                                                                                                                                                                            |
| ------------------- | ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| alignX?             | [CanvasAlignmentX]()   | How to align the content in the X axis - left, right or center                                                                                                                                                         |
| alignY?             | [CanvasAlignmentY]()   | How to align the content in the Y axis - top, bottom or center                                                                                                                                                         |
| doNotAnimate?       | boolean                | If true, don't animate while centering. Defaults to false, ie. the operation will be animated.                                                                                                                         |
| doNotZoomIfVisible? | boolean                | If the content is all already visible, do not make any changes to zoom.                                                                                                                                                |
| fill?               | number                 | A decimal between 0 and 1, which indicates how much of the viewport size the content will take up. This value is applied as a ratio of the width or height of the viewport - whichever is smaller. The default is 0.9. |
| onComplete?         | (p:[PointXY]()) => any | Optional function to call on operation complete.                                                                                                                                                                       |
| padding?            | number                 | Blank space to leave around the content                                                                                                                                                                                |
