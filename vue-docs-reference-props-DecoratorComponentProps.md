DecoratorComponentProps

Props for the Decorator component.

| Name         | Type                        | Description                                                                                                                                                                                                        |
| ------------ | --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| constraints? | [FixedElementConstraints]() | Optional constraints when using fixed placement: you can instruct the UI to restrict movement in one or both axes.                                                                                                 |
| placement?   | "fixed" \| "floating"       | Whether to float the element over the UI, so that it does not move with the content (floating), or to place the element onto the canvas, so that it moves/zooms with the content (fixed). Floating is the default. |
| position?    | [PointXY]()                 | For floating placement, this is a point relative to the viewport origin. for fixed placement, this is a point relative to the canvas origin. Defaults to 0,0.                                                      |
