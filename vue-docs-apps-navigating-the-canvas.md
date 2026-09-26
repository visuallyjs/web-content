# Navigating the canvas

The surface widget offers a number of methods you can use to assist your users in navigating their way around the canvas. You'll need to access the surface to use these methods programmatically - expand the section below for details.

How to access the surface

### From your app component[​](#from-your-app-component "Direct link to From your app component")

To access the surface from inside a component that uses a `SurfaceComponent`, declare a `ref` of type [SurfaceComponent]() and assign it in the template.

You can then access the surface through the ref's value, which is of type [SurfaceComponent]()

```html
<script setup lang="ts">
import { ref } from "vue"
import { SurfaceComponent} from "@visuallyjs/browser-ui-vue"

const surfaceRef = ref<SurfaceComponent>(null)
    
function centerContent() {
    surfaceRef.value.surface.centerContent()
}
</script>
<template>
  <SurfaceComponent ref={surfaceRef}/>
  <button onClick={() => centerContent()}>Center Content!</button>
</template>

```

### From a different component[​](#from-a-different-component "Direct link to From a different component")

If you have a component somewhere in your tree from which you wish to interact with the surface, you can use the `useSurface()` hook in conjunction with a `SurfaceProvider` to access the surface. Your app component should look something like this:

```html
<script setup lang="ts">
</script>
<template>
  <SurfaceProvider>
    <SurfaceComponent ref={surfaceRef}/>
    <MyOtherComponent/>
  </SurfaceProvider>
</template>

```

Then the implementation of `MyOtherComponent` can use the `useSurface` hook:

```html
<script setup lang="ts">

  import { useSurface } from "@visuallyjs/browser-ui-vue"
  import { Surface } from "@visuallyjs/browser-ui"
    
  const surface:Surface = useSurface() // this is reactive state

  function addANode() {
    surface.centerContent()
  }
    
</script>
<template>
  <div><button onClick={() => centerContent()}>Center Content!</button></div>
</template>

```

## Positioning[​](#positioning "Direct link to Positioning")

#### centerOn[​](#centeron "Direct link to centerOn")

Takes a single node/group, or an array of nodes/groups, and positions the surface canvas such that the given vertex/vertices is/are at the center in both axes. It does NOT change the zoom.

Signature

centerOn(element:string | Element | [Vertex]() | Array\<string | Element | [Vertex]()>, doNotAnimate:boolean)

Parameters

|              |                                                                            |                                                                                                   |
| ------------ | -------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| element      | string \| Element \| [Vertex]() \| Array\<string \| Element \| [Vertex]()> | The element(s) to center. Can be a DOM element, vertex id, or a Node/Group, or an array of these. |
| doNotAnimate | boolean                                                                    |                                                                                                   |

Return value

void

#### centerOnHorizontally[​](#centeronhorizontally "Direct link to centerOnHorizontally")

Takes a node/group as argument and positions the surface canvas such that the given node is at the center in the horizontal axis.

Signature

centerOnHorizontally(element:string | Element | [Vertex]())

Parameters

|         |                                 |                                                                         |
| ------- | ------------------------------- | ----------------------------------------------------------------------- |
| element | string \| Element \| [Vertex]() | The element to center. Can be a DOM element, vertex id, or a Node/Group |

Return value

void

#### centerOnVertically[​](#centeronvertically "Direct link to centerOnVertically")

Takes a node/group as argument and positions the surface canvas such that the given node is at the center in the vertical axis.

Signature

centerOnVertically(element:string | Element | [Vertex]())

Parameters

|         |                                 |                                                                         |
| ------- | ------------------------------- | ----------------------------------------------------------------------- |
| element | string \| Element \| [Vertex]() | The element to center. Can be a DOM element, vertex id, or a Node/Group |

Return value

void

#### centerContent[​](#centercontent "Direct link to centerContent")

Centers the tracked content inside the viewport, but does not adjust the current zoom (so the content may still extend past the viewport bounds)

Signature

centerContent(options:[CenterContentOptions]())

Parameters

|         |                          |                    |
| ------- | ------------------------ | ------------------ |
| options | [CenterContentOptions]() | Method parameters. |

Return value

void

#### pan[​](#pan "Direct link to pan")

Pans the canvas by a given amount in X and Y.

Signature

pan(dx:number, dy:number, doNotAnimate:boolean)

Parameters

|              |         |                                           |
| ------------ | ------- | ----------------------------------------- |
| dx           | number  | Amount to pan in X direction              |
| dy           | number  | Amount to pan in Y direction              |
| doNotAnimate | boolean | By default this operation uses animation. |

Return value

void

#### setPan[​](#setpan "Direct link to setPan")

Sets the position of the panned content's origin.

Signature

setPan(left:number, top:number, animate:boolean, onComplete:(p:[PointXY]()) => any)

Parameters

|            |                        |                                                                          |
| ---------- | ---------------------- | ------------------------------------------------------------------------ |
| left       | number                 | Position in pixels of the left edge of the panned content.               |
| top        | number                 | Position in pixels of the top edge of the panned content.                |
| animate    | boolean                | Whether or not to animate the pan. Defaults to false.                    |
| onComplete | (p:[PointXY]()) => any | If `animate` is set to true, an optional callback for the end of the pan |

Return value

void

<!-- -->

<!-- -->

<!-- -->

#### alignContent[​](#aligncontent "Direct link to alignContent")

Pan the canvas to align the content in one or both axes.

Signature

alignContent(options:[AlignContentOptions]())

Parameters

|         |                         |   |
| ------- | ----------------------- | - |
| options | [AlignContentOptions]() |   |

Return value

void

#### alignContentLeft[​](#aligncontentleft "Direct link to alignContentLeft")

Pan the canvas to align the content such that the left edge of the leftmost element is at the left of the viewport.

Signature

alignContentLeft(options:[AlignContentToFaceOptions]())

Parameters

|         |                               |   |
| ------- | ----------------------------- | - |
| options | [AlignContentToFaceOptions]() |   |

Return value

void

#### alignContentRight[​](#aligncontentright "Direct link to alignContentRight")

Pan the canvas to align the content such that the right edge of the rightmost element is at the right of the viewport.

Signature

alignContentRight(options:[AlignContentToFaceOptions]())

Parameters

|         |                               |   |
| ------- | ----------------------------- | - |
| options | [AlignContentToFaceOptions]() |   |

Return value

void

#### alignContentTop[​](#aligncontenttop "Direct link to alignContentTop")

Pan the canvas to align the content such that the top edge of the topmost element is at the top of the viewport.

Signature

alignContentTop(options:[AlignContentToFaceOptions]())

Parameters

|         |                               |   |
| ------- | ----------------------------- | - |
| options | [AlignContentToFaceOptions]() |   |

Return value

void

#### alignContentBottom[​](#aligncontentbottom "Direct link to alignContentBottom")

Pan the canvas to align the content such that the bottom edge of the bottom element is at the bottom of the viewport.

Signature

alignContentBottom(options:[AlignContentToFaceOptions]())

Parameters

|         |                               |   |
| ------- | ----------------------------- | - |
| options | [AlignContentToFaceOptions]() |   |

Return value

void

***

## Zooming[​](#zooming "Direct link to Zooming")

You can zoom the canvas in a number of different ways:

#### zoomToFit[​](#zoomtofit "Direct link to zoomToFit")

Zooms the display so that all the tracked elements fit inside the viewport. This method will also, by default, increase the zoom if necessary - meaning the default behaviour is to adjust the zoom so that the content fills the viewport. You can suppress zoom increase by setting `doNotZoomIfVisible:true` on the parameters to this method.

Signature

zoomToFit(params:[ZoomToFitOptions]())

Parameters

|        |                      |   |
| ------ | -------------------- | - |
| params | [ZoomToFitOptions]() |   |

Return value

void

#### zoomToFitIfNecessary[​](#zoomtofitifnecessary "Direct link to zoomToFitIfNecessary")

Zooms the display so that all the tracked elements fit inside the viewport, but does not make any adjustments to zoom if all the elements are currently visible (it still does center the content though).

Signature

zoomToFitIfNecessary(params:[ZoomToFitIfNecessaryOptions]())

Parameters

|        |                                 |   |
| ------ | ------------------------------- | - |
| params | [ZoomToFitIfNecessaryOptions]() |   |

Return value

void

#### zoomToElements[​](#zoomtoelements "Direct link to zoomToElements")

Zooms the viewport so that all of the given elements are visible.

Signature

zoomToElements(zParams:[ZoomToElementsOptions<]()[BrowserElement]()>)

Parameters

|         |                                               |   |
| ------- | --------------------------------------------- | - |
| zParams | [ZoomToElementsOptions<]()[BrowserElement]()> |   |

Return value

void

#### zoomToExtents[​](#zoomtoextents "Direct link to zoomToExtents")

Zooms the display to fit the given extents, which may be a single box or an array of boxes; in the latter case VisuallyJs will calculate a minimum bounding box for all the boxes provided.

Signature

zoomToExtents(zParams:[ZoomToExtentsOptions]())

Parameters

|         |                          |                      |
| ------- | ------------------------ | -------------------- |
| zParams | [ZoomToExtentsOptions]() | Options for the zoom |

Return value

void

#### zoomToBackground[​](#zoomtobackground "Direct link to zoomToBackground")

Zooms the display so that the background (if one is set) fits inside the viewport.

Signature

zoomToBackground(params:{

<br />

  doNotAnimate:boolean,

<br />

  onComplete:(p:[PointXY]()) => any

<br />

})

Parameters

|        |                                                                                |   |
| ------ | ------------------------------------------------------------------------------ | - |
| params | {<br />  doNotAnimate:boolean,<br />  onComplete:(p:[PointXY]()) => any<br />} |   |

Return value

void

#### zoomToDecorator[​](#zoomtodecorator "Direct link to zoomToDecorator")

Zooms the display to fit the canvas and content plus any elements added by the given decorator.

Signature

zoomToDecorator(zParams:{

<br />

  decorator:string | [Decorator](),

<br />

  doNotAnimate:boolean,

<br />

  doNotFirePanEvent:boolean,

<br />

  doNotZoomIfVisible:boolean,

<br />

  fill:number,

<br />

  onComplete:(p:[PointXY]()) => any,

<br />

  onStep:() => any

<br />

})

Parameters

|         |                                                                                                                                                                                                                                            |   |
| ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | - |
| zParams | {<br />  decorator:string \| [Decorator](),<br />  doNotAnimate:boolean,<br />  doNotFirePanEvent:boolean,<br />  doNotZoomIfVisible:boolean,<br />  fill:number,<br />  onComplete:(p:[PointXY]()) => any,<br />  onStep:() => any<br />} |   |

Return value

void

***

## Finding elements[​](#finding-elements "Direct link to Finding elements")

Several methods are available to assist you to find elements in the canvas.

#### findIntersectingVertices[​](#findintersectingvertices "Direct link to findIntersectingVertices")

Finds all of the vertices that intersect the rectangle described by `origin` and `dimensions`.

Signature

findIntersectingVertices(options:[IntersectingVerticesOptions]())

Parameters

|         |                                 |                                 |
| ------- | ------------------------------- | ------------------------------- |
| options | [IntersectingVerticesOptions]() | Options for the find operation. |

Return value

Array<[IntersectingVertex<]()[BrowserElement]()>>

<!-- -->

<!-- -->

***

## Mapping coordinates[​](#mapping-coordinates "Direct link to Mapping coordinates")

Every now and then you'll likely want to map between the surface's coordinate system and the page coordinate system. The surface offers a few methods to assist with this.

#### isInViewport[​](#isinviewport "Direct link to isInViewport")

Returns whether or not the given point (relative to page origin) is within the viewport for the widget.

Signature

isInViewport(x:number, y:number)

Parameters

|   |        |                             |
| - | ------ | --------------------------- |
| x | number | X location of point to test |
| y | number | Y location of point to test |

Return value

boolean

#### fromPageLocation[​](#frompagelocation "Direct link to fromPageLocation")

Maps the given page location to a value relative to the canvas origin, allowing for zoom and pan of the canvas.

<br />

This takes into account the offset of the canvas in the page so that what you get back is the mapped position

<br />

relative to the target element's \[left,top] corner

Signature

fromPageLocation(left:number, top:number, roundValues:boolean)

Parameters

|             |         |                                                        |
| ----------- | ------- | ------------------------------------------------------ |
| left        | number  | X location                                             |
| top         | number  | Y location                                             |
| roundValues | boolean | If true, the location is returned as integers for x/y. |

Return value

[PointXY]()

#### toPageLocation[​](#topagelocation "Direct link to toPageLocation")

Maps the given canvas location to a page location, allowing for zoom and pan of the canvas. Note that `page` in this method takes scroll into account. If you wish to map to just the visible section of the browser, use `toWindowLocation`.

Signature

toPageLocation(left:number, top:number)

Parameters

|      |        |            |
| ---- | ------ | ---------- |
| left | number | X location |
| top  | number | Y location |

Return value

[PointXY]()

#### fromWindowLocation[​](#fromwindowlocation "Direct link to fromWindowLocation")

Maps the given window location to a value relative to the canvas origin. The window means the browser's visible

<br />

window, and is not the same as the page, because of scroll.

Signature

fromWindowLocation(left:number, top:number, roundValues:boolean)

Parameters

|             |         |   |
| ----------- | ------- | - |
| left        | number  |   |
| top         | number  |   |
| roundValues | boolean |   |

Return value

[PointXY]()

***
