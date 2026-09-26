ShapeSet

Defines a set of shapes. This is the interface you should extend if you wish to supply custom shape sets to the widget.

| Name          | Type                               | Description                                                                                                                                                   |
| ------------- | ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| labelPadding? | number                             | Optional label padding when labels are top/bottom to use as a default for all shapes. Individual shapes can set their own values. This defaults to 10 pixels. |
| properties?   | Array<[ShapePropertyDefinition]()> | A list of configurable properties exposed by shapes in this set.                                                                                              |
