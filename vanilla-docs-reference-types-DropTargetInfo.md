DropTargetInfo

When a new vertex was dropped onto an existing vertex, the onVertexAdded callback is passed an object of this type to describe the vertex onto which the new vertex was dropped.

{

<br />

  pos:[PointXY](),

<br />

  size:[Size](),

<br />

  vertex:[Node]() | [Group]()

<br />

}
