AlignContentOptions

Options for aligning content in the UI.

| Name               | Type                   | Description                                                                                    |
| ------------------ | ---------------------- | ---------------------------------------------------------------------------------------------- |
| alignX?            | [CanvasAlignmentX]()   | How to align the content in the X axis - left, right or center                                 |
| alignY?            | [CanvasAlignmentY]()   | How to align the content in the Y axis - top, bottom or center                                 |
| animationDuration? | number                 | How long, in milliseconds, the animation should take to run.                                   |
| doNotAnimate?      | boolean                | If true, don't animate while centering. Defaults to false, ie. the operation will be animated. |
| onComplete?        | (p:[PointXY]()) => any | Optional function to call on operation complete.                                               |
| padding?           | number                 | How much padding to leave around the content.                                                  |
| zoom?              | number                 | Zoom to set prior to alignment                                                                 |
