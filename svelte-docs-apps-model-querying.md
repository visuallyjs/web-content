# Querying the model

The VisuallyJs model offers several methods to query the hierarchy of nodes and groups.

## Groups[​](#groups "Direct link to Groups")

When you have a hierarchical model where nodes or groups can be nested within other groups, you can use these methods to navigate the hierarchy.

### Ancestor groups[​](#ancestor-groups "Direct link to Ancestor groups")

#### getAncestors[​](#getancestors "Direct link to getAncestors")

Gets a list of groups that are ancestors of the given node/group (or port, for which we first resolve the node/group it resides on). The list of ancestors is ordered in terms of their proximity to the focus, ie. the first entry is the focus vertex's immediate parent.

Signature

getAncestors(vertex:[Vertex]())

Parameters

|        |            |   |
| ------ | ---------- | - |
| vertex | [Vertex]() |   |

Return value

Array<[Group]()>

### Descendants of a group[​](#descendants-of-a-group "Direct link to Descendants of a group")

#### getDescendants[​](#getdescendants "Direct link to getDescendants")

Gets a list of nodes/groups that are descendants of the given group.

Signature

getDescendants(vertex:[Group]())

Parameters

|        |           |   |
| ------ | --------- | - |
| vertex | [Group]() |   |

Return value

Array<[Node]() | [Group]()>

### Testing for ancestor[​](#testing-for-ancestor "Direct link to Testing for ancestor")

#### isAncestor[​](#isancestor "Direct link to isAncestor")

Returns whether or not `possibleAncestor` is in fact an ancestor of the given focus node/group

Signature

isAncestor(focus:[Vertex](), possibleAncestor:[Group]())

Parameters

|                  |            |                                           |
| ---------------- | ---------- | ----------------------------------------- |
| focus            | [Vertex]() | Vertex to test                            |
| possibleAncestor | [Group]()  | Group which may be an ancestor of `focus` |

Return value

boolean

### Testing for descendant[​](#testing-for-descendant "Direct link to Testing for descendant")

#### isDescendantGroup[​](#isdescendantgroup "Direct link to isDescendantGroup")

Determine whether `possibleDescendant` is in fact a descendant of the `ancestor` group

Signature

isDescendantGroup(possibleDescendant:[Group](), ancestor:[Group]())

Parameters

|                    |           |                |
| ------------------ | --------- | -------------- |
| possibleDescendant | [Group]() | Group to test  |
| ancestor           | [Group]() | Ancestor group |

Return value

boolean

### Selecting descendants[​](#selecting-descendants "Direct link to Selecting descendants")

While the methods above return arrays of objects, you may sometimes want to perform selection-based operations on a hierarchy.

#### selectDescendants[​](#selectdescendants "Direct link to selectDescendants")

Selects all descendants of some Node or Group, and, optionally, the Node/Group itself.

Signature

selectDescendants(obj:string | [Node]() | [Group](), includeFocus:boolean, includeEdges:boolean)

Parameters

|              |                                 |                                                                                            |
| ------------ | ------------------------------- | ------------------------------------------------------------------------------------------ |
| obj          | string \| [Node]() \| [Group]() | Node/Group, or ID of Node/Group, to select                                                 |
| includeFocus | boolean                         | Whether or not to include the focus node/group in the returned dataset. Defaults to false. |
| includeEdges | boolean                         | Whether or not to include edges in the returned dataset. Defaults to false.                |

Return value

[VisuallyJsSelection]()
