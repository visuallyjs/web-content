RectangleXY

Defines a rectangle in 2d space - its x/y location, width and height, and optionally the computed center, but that can of course be calculated from the other values. Internally there are times when the code has this to hand so we include it here.

| Name    | Type        | Description                                                                                                                                                         |
| ------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| center? | [PointXY]() | Center of the box. In some cases the code has this information to hand<br />and populates it, but if it is absent you can figure it out from the<br />other values. |
| height  | number      | element height                                                                                                                                                      |
| width   | number      | Element width                                                                                                                                                       |
| x       | number      | X location                                                                                                                                                          |
| y       | number      | Y location                                                                                                                                                          |
