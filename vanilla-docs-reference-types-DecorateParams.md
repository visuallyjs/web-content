DecorateParams

Parameters for a decorator. These are the parameters that are passed

<br />

in to a Decorator's `decorate` method when it is called.

{

<br />

  fixElement:(el:[BrowserElement](), pos:[PointXY](), constraints:[FixedElementConstraints](), id:string) => FixedElement,

<br />

  layout:[AbstractLayout\<any>](),

<br />

  setAbsolutePosition:(el:[BrowserElement](), xy:[PointXY]()) => void,

<br />

  surface:[Surface]()

<br />

}
