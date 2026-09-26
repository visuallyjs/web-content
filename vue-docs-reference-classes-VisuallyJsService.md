### VisuallyJsService

Provides access to Surface/Diagram/Paper ui components, as well as models. This service is provided in the root as an application-wide instance, but each of the providers also creates and provides an instance of this service.

### Class Members[​](#class-members "Direct link to Class Members")

| Name    | Type                           | Description                                                |
| ------- | ------------------------------ | ---------------------------------------------------------- |
| diagram | ShallowRef<>                   | The current diagram in scope. May be null.                 |
| model   | ShallowRef<[BrowserUIModel]()> | The current model in scope. May be null.                   |
| paper   | ShallowRef<>                   | The current paper in scope. May be null.                   |
| surface | ShallowRef<>                   | The current surface in scope. May be null.                 |
| ui      | ShallowRef<>                   | The current ui (a surface or paper) in scope. May be null. |
