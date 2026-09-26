SurfaceEdgeAddedParams

Payload for an edge

<!-- -->

:added

<!-- -->

event from a surface.

| Name         | Type                               | Description                                                                                 |
| ------------ | ---------------------------------- | ------------------------------------------------------------------------------------------- |
| addedByMouse | boolean                            | True if the edge was added via the mouse (or touch events), false if added programmatically |
| connection   | [Connection<]()[BrowserElement]()> | Connection representing the edge in the UI                                                  |
| edge         | [Edge]()                           | The edge that was added                                                                     |
| geometry     | [Geometry]()                       | Associated geometry, may be null                                                            |
| source       | [Vertex]()                         | Source vertex for the new edge                                                              |
| target       | [Vertex]()                         | Target vertex for the new edge                                                              |
