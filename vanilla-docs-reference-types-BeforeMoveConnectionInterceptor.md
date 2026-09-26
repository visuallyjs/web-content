BeforeMoveConnectionInterceptor

A function to run before an edge of the given type is relocated from its current source or target to a new source or target. Returning false from this method will abort the move.

`(source:Vertex, target:Vertex, edge:Edge) => any`
