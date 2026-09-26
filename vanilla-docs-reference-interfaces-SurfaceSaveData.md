SurfaceSaveData

Definition of the payload returned from the Surface's `save` method.

| Name            | Type        | Description                                             |
| --------------- | ----------- | ------------------------------------------------------- |
| data            | any         | Data exported from the model                            |
| pan             | [PointXY]() | The current pan position of the surface canvas          |
| transformOrigin | [PointXY]() | The current position of the surface's transform origin. |
| zoom            | number      | The current zoom level                                  |
