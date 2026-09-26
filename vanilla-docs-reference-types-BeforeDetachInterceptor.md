BeforeDetachInterceptor

A function to run before the given edge is detached from the given source vertex. If this method returns false, the detach will be aborted.

`(source:Vertex, target:Vertex, edge:Edge) => boolean`
