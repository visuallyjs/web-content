BeforeStartDetachInterceptor

A function to run before the given edge is detached from the given source vertex. If this method returns false, the detach will be aborted. The difference between this and `beforeDetach` is that this method is fired as soon as a user tries to detach an edge in the UI, whereas `beforeDetach` allows a user to detach the edge in the UI.

`(source:Vertex, edge:Edge) => Record<string,any> | boolean`
