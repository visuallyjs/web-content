LayoutParameters

Base interface for layout parameters. All layout parameter interfaces extend this.

| Name              | Type                 | Description                                                                                         |
| ----------------- | -------------------- | --------------------------------------------------------------------------------------------------- |
| height?           | number               | Optional fixed height for the layout.                                                               |
| locationFunction? | [LocationFunction]() | Optional function that, given some vertex, can provide the x/y location of the vertex on the canvas |
| padding?          | [PointXY]()          | Optional padding to put around the elements.                                                        |
| width?            | number               | Optional fixed width for the layout.                                                                |
