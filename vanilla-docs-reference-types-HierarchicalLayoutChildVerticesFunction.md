HierarchicalLayoutChildVerticesFunction\<T>

Type Parameters

|   |           |                                                                                                                 |
| - | --------- | --------------------------------------------------------------------------------------------------------------- |
| T | [HasId]() | Defines the type of the object from which child vertices will be retrieved, and the type of the child vertices. |

Defines the function used to find child edges in some HierarchicalLayout. This function can be used to implement layouts that only show a certain subset of the entire dataset, or to implement a collapse/expand scheme.

`(node:T, layer:number, dataSource:DataSource) => Array<T>`
