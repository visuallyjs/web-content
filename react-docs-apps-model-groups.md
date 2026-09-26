# Groups

## Model object[​](#model-object "Direct link to Model object")

### Group

A group is an extension of node that can contain other nodes and groups.

### Class Members[​](#class-members "Direct link to Class Members")

| Name    | Type            | Description                                                                                |
| ------- | --------------- | ------------------------------------------------------------------------------------------ |
| group   | [Group]()       | Group the node is a member of, if any. This property should never be written by your code. |
| id      | string          | The vertex's id. Must be a string.                                                         |
| members | Array<[Node]()> | Members of the group. Do not write to, or manipulate in any way, this array.               |
| type    | string          | Object's type.                                                                             |

### Class Methods[​](#class-methods "Direct link to Class Methods")

#### getAllDirectEdges[​](#getalldirectedges "Direct link to getAllDirectEdges")

Gets all the edges connecting to this group and any ports on the group.

Signature

getAllDirectEdges(filter:(e:[Edge]()) => boolean)

Parameters

|        |                         |                       |
| ------ | ----------------------- | --------------------- |
| filter | (e:[Edge]()) => boolean | Optional edge filter. |

Return value

Array<[Edge]()>

#### getAllEdges[​](#getalledges "Direct link to getAllEdges")

Gets all of the edges connected to this node, both on the node itself and on all of its ports.

Signature

getAllEdges(filter:(e:[Edge]()) => boolean)

Parameters

|        |                         |                       |
| ------ | ----------------------- | --------------------- |
| filter | (e:[Edge]()) => boolean | Optional Edge filter. |

Return value

Array<[Edge]()>

#### getAllSourceEdges[​](#getallsourceedges "Direct link to getAllSourceEdges")

Gets all of the Edges connected to this Node, both on the Node itself and on all of its Ports, where this node/port is the source of edge

Signature

getAllSourceEdges()

Return value

Array<[Edge]()>

#### getAllTargetEdges[​](#getalltargetedges "Direct link to getAllTargetEdges")

Gets all of the Edges connected to this Node, both on the Node itself and on all of its Ports, where this node/port is the target of edge

Signature

getAllTargetEdges()

Return value

Array<[Edge]()>

#### getDirectEdges[​](#getdirectedges "Direct link to getDirectEdges")

Gets all Edges directly connected to this Vertex, ie. not to one of the Ports on the Vertex. This is an alias for `getEdges`.

Signature

getDirectEdges(filter:(e:[Edge]()) => boolean)

Parameters

|        |                         |                       |
| ------ | ----------------------- | --------------------- |
| filter | (e:[Edge]()) => boolean | Optional Edge filter. |

Return value

Array<[Edge]()>

#### getDirectSourceEdges[​](#getdirectsourceedges "Direct link to getDirectSourceEdges")

Gets all Edges directly connected to this Vertex, ie. not to one of the Ports on the Vertex, where this Vertex is the source.

<br />

This is an alias for `getSourceEdges`.

Signature

getDirectSourceEdges()

Return value

Array<[Edge]()>

#### getDirectTargetEdges[​](#getdirecttargetedges "Direct link to getDirectTargetEdges")

Gets all Edges directly connected to this Vertex, ie. not to one of the Ports on the Vertex, where this Vertex is the target.

<br />

This is an alias for `getTargetEdges`.

Signature

getDirectTargetEdges()

Return value

Array<[Edge]()>

#### getEdges[​](#getedges "Direct link to getEdges")

Gets all edges where this vertex is either the source or the target of the edge.

<br />

Note that this does *not* retrieve edges on any ports associated with this Vertex - for that,

Signature

getEdges(params:{

<br />

  filter:(e:[Edge]()) => boolean

<br />

})

Parameters

|        |                                                |   |
| ------ | ---------------------------------------------- | - |
| params | {<br />  filter:(e:[Edge]()) => boolean<br />} |   |

Return value

Array<[Edge]()>

#### getFullId[​](#getfullid "Direct link to getFullId")

Gets the Vertex's id, which, for Nodes and Groups, is just the `id` property. This method is overridden by Ports.

Signature

getFullId()

Return value

string

#### getIndegreeCentrality[​](#getindegreecentrality "Direct link to getIndegreeCentrality")

Gets this Node's "indegree" centrality; a measure of how many other Nodes are connected to this Node as the target of some Edge.

Signature

getIndegreeCentrality()

Return value

number

#### getInternalEdges[​](#getinternaledges "Direct link to getInternalEdges")

Gets all the edges to/from the group, any ports the Group has, and any edges connected to all child vertices of the group.

Signature

getInternalEdges(filter:(e:[Edge]()) => boolean)

Parameters

|        |                         |                                                                    |
| ------ | ----------------------- | ------------------------------------------------------------------ |
| filter | (e:[Edge]()) => boolean | Optional edge filter to apply to all members and the group itself. |

Return value

Array<[Edge]()>

#### getMemberCount[​](#getmembercount "Direct link to getMemberCount")

Gets how many members the group has.

Signature

getMemberCount()

Return value

number

#### getMembers[​](#getmembers "Direct link to getMembers")

Gets the group members

Signature

getMembers()

Return value

Array<[Node]()>

#### getOutdegreeCentrality[​](#getoutdegreecentrality "Direct link to getOutdegreeCentrality")

Gets this Node's "outdegree" centrality; a measure of how many other Nodes this Node is connected to as the source of some Edge.

Signature

getOutdegreeCentrality()

Return value

number

#### getPort[​](#getport "Direct link to getPort")

Gets the Port with the given id, null if nothing found.

Signature

getPort(portId:string)

Parameters

|        |        |          |
| ------ | ------ | -------- |
| portId | string | Port id. |

Return value

[Port]()

#### getPortEdges[​](#getportedges "Direct link to getPortEdges")

Gets all Edges that are connected to Ports on this Node, not directly to the Node itself.

Signature

getPortEdges(filter:(e:[Edge]()) => boolean)

Parameters

|        |                         |                      |
| ------ | ----------------------- | -------------------- |
| filter | (e:[Edge]()) => boolean | Optional edge filter |

Return value

Array<[Edge]()>

#### getPorts[​](#getports "Direct link to getPorts")

Gets all Ports associated with this Node.

Signature

getPorts()

Return value

Array<[Port]()>

#### getPortSourceEdges[​](#getportsourceedges "Direct link to getPortSourceEdges")

Gets all Edges that are connected to Ports on this Node, not directly to the Node itself, where the Port on this Node is the source of the edge.

Signature

getPortSourceEdges()

Return value

Array<[Edge]()>

#### getPortTargetEdges[​](#getporttargetedges "Direct link to getPortTargetEdges")

Gets all Edges that are connected to Ports on this Node, not directly to the Node itself, where the Port on this Node is the target of the edge.

Signature

getPortTargetEdges()

Return value

Array<[Edge]()>

#### getSourceEdges[​](#getsourceedges "Direct link to getSourceEdges")

Gets all Edges where this Vertex is the source.

Signature

getSourceEdges()

Return value

Array<[Edge]()>

#### getTargetEdges[​](#gettargetedges "Direct link to getTargetEdges")

Gets all Edges where this Vertex is the target.

Signature

getTargetEdges()

Return value

Array<[Edge]()>

#### inspect[​](#inspect "Direct link to inspect")

Returns a string representation of the Vertex.

<br />

\*

Signature

inspect()

Return value

string

## Data format[​](#data-format "Direct link to Data format")

On load and save, groups are represented by a `GroupData` object with this definition:

Sorry - we could not find this document.

## Adding Groups[​](#adding-groups "Direct link to Adding Groups")

TBD

## Removing Groups[​](#removing-groups "Direct link to Removing Groups")

TBD
