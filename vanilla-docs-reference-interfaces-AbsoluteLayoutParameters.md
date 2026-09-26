AbsoluteLayoutParameters

Constructor parameters for an AbsoluteLayout.

| Name              | Type                 | Description                                                                                                    |
| ----------------- | -------------------- | -------------------------------------------------------------------------------------------------------------- |
| absoluteBacked?   | boolean              | Defaults to false. If true, then the layout will use any position values found in the data for a given vertex. |
| height?           | number               | Optional fixed height for the layout.                                                                          |
| locationFunction? | [LocationFunction]() | Optional function that, given some vertex, can provide the x/y location of the vertex on the canvas            |
| padding?          | [PointXY]()          | Optional padding to put around the elements.                                                                   |
| width?            | number               | Optional fixed width for the layout.                                                                           |
