ConstrainFunction\<EL,E>

Type Parameters

|    |   |   |
| -- | - | - |
| EL |   |   |
| E  |   |   |

Definition of a function that can be used to constrain the movement of an element that is being dragged. The function is given the "desiredLoc", which is the location the element would be moved to if not constrained, and it is expected to return either some other value, meaning place the element at that position, or null, meaning for the given desired location there is no preferred position and the element should not be moved.

`(desiredLoc:PointXY, dragEl:EL, constrainRect:Size, size:Size, currentPos:PointXY, e:E) => PointXY`
