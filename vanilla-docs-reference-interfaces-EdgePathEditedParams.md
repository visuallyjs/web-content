EdgePathEditedParams

Payload for an edge path edited event.

| Name             | Type                     | Description                            |
| ---------------- | ------------------------ | -------------------------------------- |
| edge             | [Edge]()                 | The edge that was edited               |
| geometry         | any                      | The edge's new geometry                |
| originalGeometry | any                      | The edge's original geometry           |
| ui               | VisuallyJsRenderer\<any> | The UI the user is editing the path on |
