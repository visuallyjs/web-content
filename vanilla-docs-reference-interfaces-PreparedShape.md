PreparedShape

Defines a wrapper around a shape with some `type` and `category` that adds properties (to be used to define the shape's appearance) and, optionally, the shape's initial size.

| Name       | Type           | Description                                                                             |
| ---------- | -------------- | --------------------------------------------------------------------------------------- |
| category   | string         | The shape set the underlying shape is sourced from                                      |
| label      | string         | Label to show for the prepared shape in a palette                                       |
| properties | [ObjectData]() | Properties with which to configure the shape when it is created.                        |
| shapeId    | string         | The ID for this prepared shape. Used internally, but ensure you provide a unique value. |
| size?      | [Size]()       | Optional initial size to use for the shape                                              |
| type       | string         | The type of the underlying shape                                                        |
