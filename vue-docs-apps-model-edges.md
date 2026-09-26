# Edges

## Model object[​](#model-object "Direct link to Model object")

### Edge

An edge connects two vertices.

### Class Members[​](#class-members "Direct link to Class Members")

| Name   | Type       | Description         |
| ------ | ---------- | ------------------- |
| cost   | number     | Edge cost           |
| source | [Vertex]() | Source of the Edge. |
| target | [Vertex]() | Target of the Edge. |
| type   | string     | Object's type.      |

### Class Methods[​](#class-methods "Direct link to Class Methods")

#### getCost[​](#getcost "Direct link to getCost")

Gets the cost for this edge. Defaults to 1.

Signature

getCost()

Return value

number

#### getFullId[​](#getfullid "Direct link to getFullId")

Alias for the getId method.

Signature

getFullId()

Return value

string

#### getId[​](#getid "Direct link to getId")

Gets the id for this Edge.

Signature

getId()

Return value

string

#### isDirected[​](#isdirected "Direct link to isDirected")

Gets whether or not the Edge is directed.

Signature

isDirected()

Return value

boolean

Internally, the model class represents an edge.

## Data format[​](#data-format "Direct link to Data format")

On load and save, edges are represented by a `EdgeData` object with this definition:

EdgeData

The default type that represents an edge in a dataset to load or a saved dataset. Edges differ slightly from nodes and groups in that there are fields which are mandatory: `source` and `data`. Edges also differ from nodes and groups in that any backing data for an edge (including its `id` and/or `type`) need to be provided in the `data` member of the edge, not in the root as with nodes and groups.

| Name      | Type                                                                            | Description                                                                                                                                   |
| --------- | ------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| anchors?  | {<br />  source:[ObjectAnchorSpec](),<br />  target:[ObjectAnchorSpec]()<br />} | Optional anchors for the edge.                                                                                                                |
| cost?     | number                                                                          | Cost to associate with the edge. Defaults to 1. This value can be used when computing shortest paths.                                         |
| data?     | [ObjectData]()                                                                  | Optional data to associate with the edge                                                                                                      |
| directed? | boolean                                                                         | Whether or not the given edge is directed, ie. when computing a path the edge can only be traversed from source to target. Defaults to false. |
| geometry? | [Geometry]()                                                                    | Optional geometry that defines the edge's path                                                                                                |
| source    | string \| [PointXY]()                                                           | Either the ID of the source vertex or a canvas location.                                                                                      |
| target    | string \| [PointXY]()                                                           | Either the ID of the target vertex or a canvas location.                                                                                      |

## Adding Edges[​](#adding-edges "Direct link to Adding Edges")

TBD

## Removing Edges[​](#removing-edges "Direct link to Removing Edges")

TBD
