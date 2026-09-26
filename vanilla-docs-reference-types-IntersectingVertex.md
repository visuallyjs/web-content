IntersectingVertex\<EL>

Type Parameters

|    |   |                                                                                                         |
| -- | - | ------------------------------------------------------------------------------------------------------- |
| EL |   | The element type for the UI. In the browser-ui package this is BrowserElement - an HTML or SVG element. |

Details for a vertex that is enclosed by, or intersects, some specified region. The type parameter T will either be a Node or a Group. EL is the type parameter for the element in the UI.

{

<br />

  el:EL,

<br />

  enclosed:boolean,

<br />

  id:string,

<br />

  r:[RectangleXY](),

<br />

  v:[Node]() | [Group]()

<br />

}
