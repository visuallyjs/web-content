BeforeStartConnectInterceptor

A function to run before an edge of the given type is dragged from the given source. Returning false from this method will abort the connection.

`(source:Vertex, type:string) => boolean | Record<string,any>`
