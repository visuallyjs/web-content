AlignContentToFaceOptions

Options for aligning content to a specific position in the UI.

| Name               | Type                   | Description                                                                                    |
| ------------------ | ---------------------- | ---------------------------------------------------------------------------------------------- |
| animationDuration? | number                 | How long, in milliseconds, the animation should take to run.                                   |
| doNotAnimate?      | boolean                | If true, don't animate while centering. Defaults to false, ie. the operation will be animated. |
| onComplete?        | (p:[PointXY]()) => any | Optional function to call on operation complete.                                               |
| zoom?              | number                 | Zoom level to set during the alignment                                                         |
