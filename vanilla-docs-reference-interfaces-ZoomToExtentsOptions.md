ZoomToExtentsOptions

Options for the zoomToExtents method

| Name                | Type                                      | Description                                                                                                                                                                                                                  |
| ------------------- | ----------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| doNotAnimate?       | boolean                                   | If true, don't animate while centering. Defaults to false, ie. the operation will be animated.                                                                                                                               |
| doNotZoomIfVisible? | boolean                                   | If the given extents is all already visible, do not make any changes to zoom.                                                                                                                                                |
| extents             | [RectangleXY]() \| Array<[RectangleXY]()> | Extents to zoom to. Can be a single box or an array of boxes; in the latter case VisuallyJs will calculate a minimum bounding box for all the boxes provided.                                                                |
| fill?               | number                                    | A decimal between 0 and 1, which indicates how much of the viewport size the given extents will take up. This value is applied as a ratio of the width or height of the viewport - whichever is smaller. The default is 0.9. |
| onComplete?         | (p:[PointXY]()) => any                    | Optional function to call on operation complete.                                                                                                                                                                             |
