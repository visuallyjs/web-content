ZoomOptions

Options to control how a user manages zoom on the canvas.

| Name                  | Type          | Description                                                                                                                                                                                                                                          |
| --------------------- | ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| fixedTransformOrigin? | [PointXY]()   | Optional fixed transform origin for the canvas. Defaults to null.When this is supplied the zoom function does not change the transform origin You can still zoom and pan but the zoom/pan is applied relative to the top/left corner of the content. |
| initialValue?         | number        | Initial zoom value. Defaults to 1.                                                                                                                                                                                                                   |
| range?                | [ZoomRange]() | Zoom range to support. The default is \[0.05, 3]                                                                                                                                                                                                     |
| step?                 | number        | When zooming by step, this defines the change in zoom for each step. Defaults to 0.25.                                                                                                                                                               |
| wheel?                | boolean       | When true - which is the default - the wheel will be used for zoom.                                                                                                                                                                                  |
