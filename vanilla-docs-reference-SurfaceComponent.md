# Surface

Provides a pannable and zoomable canvas on which nodes, edges and groups can be drawn, with support for layouts and various plugins.

## Usage[​](#usage "Direct link to Usage")

This component is at the heart of VisuallyJs, and is very customizable, but there are three main sections of options that you should be familiar with:

* **renderOptions** This option contains all of the settings that control the behaviour and appearance of the component itself - what layout to use, whether to zoom to fit a dataset when it has been loaded, whether or not to use a grid, plugins, etc. It also contains the `view`.

* **view** This contains the mapping from node/edge/group types to their visual representation and behaviour. For nodes and groups this means mapping a component to use to render them; for edges this means specifying details of the connector to use to draw an edge, and how the edge should be anchored. You can also supply event mappings in your `view` to hook into user interaction with the various parts of the UI.

* **modelOptions** This is used less often than `view` and `renderOptions`, but this is how you can provide settings for the underlying model.

To create a surface, you'll need an HTML element to mount it into. Note also that you should include the `visuallyjs.css` stylesheet in your page:

```html
<!doctype html>
<html>
    <head>
        <link rel="stylesheet" href="node_modules/@visuallyjs/browser-ui/css/visuallyjs.css">
    </head>
    <body>
      <div id="myContainer"></div>
    </body>
</html>

```

Then you can use `createSurface` to create it:

```typescript
import { createSurface } from "@visuallyjs/browser-ui"
    
const renderOptions = { 
  view:{
    nodes:{
      default:{
        template:`<div>{{id}}</div>`
      }
    }
  }
}

const data = { 
    nodes:[
        { id:"1", left:50, top:50 }
    ]
}

const surface = createSurface(document.getElementById("myContainer"), renderOptions)


```

## Class Definition[​](#class-definition "Direct link to Class Definition")

### Surface

Provides a canvas on which nodes, groups and edges can be rendered, with support for pan/zoom, layouts and various plugins. This is not a class that API users should instantiate directly: for users of a library integration, a Surface will be created internally by the appropriate component; for users of vanilla VisuallyJs, a Surface is created either via the createSurface factory method, or via a `render` call on an instance of the BrowserUIModel.

### Class Members[​](#class-members "Direct link to Class Members")

| Name         | Type                    | Description                                                                                                                                                                                         |
| ------------ | ----------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| clipboard    | [BrowserUIClipboard]()  | Clipboard for copy/paste of data.                                                                                                                                                                   |
| dataSource   | [DataSource]()          | The data model that is being rendered. In the majority of cases this points to the same object as `model`, but you can render some subset of a data model, such as a dynamically updated Selection. |
| model        | [BrowserUIModel]()      |                                                                                                                                                                                                     |
| objectFilter | (b:[Base]()) => boolean | Optional filter used to determine whether or not we want to render some specific object.                                                                                                            |

### Class Methods[​](#class-methods "Direct link to Class Methods")

#### $getCapabilityConfig[​](#getcapabilityconfig "Direct link to $getCapabilityConfig")

Gets the config for some capability. May be an empty object. A capability provider may be registered at the point that a capability is registered - the function is provided by the code that registers the capability.

Signature

$getCapabilityConfig(c:UICapabilities)

Parameters

|   |                |   |
| - | -------------- | - |
| c | UICapabilities |   |

Return value

Record\<string,any>

#### $hasCapability[​](#hascapability "Direct link to $hasCapability")

Test whether the specific capability is available on this instance of the UI.

Signature

$hasCapability(c:UICapabilities)

Parameters

|   |                |   |
| - | -------------- | - |
| c | UICapabilities |   |

Return value

boolean

#### addBackground[​](#addbackground "Direct link to addBackground")

Adds a background. Theoretically you can add multiple backgrounds but the end result of that is indeterminate.

Signature

addBackground(background:Background)

Parameters

|            |            |   |
| ---------- | ---------- | - |
| background | Background |   |

Return value

void

#### addClass[​](#addclass "Direct link to addClass")

Adds a class to the DOM element represented by `el`, which can be a Selection, or an instance of many different types - see the `SupportsClassManipulation` interface for a complete list.

Signature

addClass(el:[VisuallyJsSelection]() | SupportsClassManipulation, clazz:string)

Parameters

|       |                                                      |   |
| ----- | ---------------------------------------------------- | - |
| el    | [VisuallyJsSelection]() \| SupportsClassManipulation |   |
| clazz | string                                               |   |

Return value

void

#### addDragClassnameFilter[​](#adddragclassnamefilter "Direct link to addDragClassnameFilter")

Adds a CSS class name filter to the drag handler - without the `.`.

Signature

addDragClassnameFilter(clazz:string | Array\<string>)

Parameters

|       |                          |                                                                                                 |
| ----- | ------------------------ | ----------------------------------------------------------------------------------------------- |
| clazz | string \| Array\<string> | Either a single class name, or a comma separated list of classnames, or an array of classnames. |

Return value

void

#### addDragFilter[​](#adddragfilter "Direct link to addDragFilter")

Adds a filter to the drag handler.

Signature

addDragFilter(filter:(e:MouseEvent) => boolean, exclude:boolean)

Parameters

|         |                           |   |
| ------- | ------------------------- | - |
| filter  | (e:MouseEvent) => boolean |   |
| exclude | boolean                   |   |

Return value

void

#### addDragSelectorFilter[​](#adddragselectorfilter "Direct link to addDragSelectorFilter")

Adds a CSS3 selector filter to the drag handler. A drag cannot start on an element that matches this selector. For more fine-grained control over dragging, see #addVertexDragFilter.

Signature

addDragSelectorFilter(selector:string)

Parameters

|          |        |                        |
| -------- | ------ | ---------------------- |
| selector | string | A valid CSS3 selector. |

Return value

void

#### addElementEventFilter[​](#addelementeventfilter "Direct link to addElementEventFilter")

Adds a CSS3 selector filter which will exclude the given element (and descendants) from reporting element events. Used internally by popups, but exposed in the API as it may be useful.

Signature

addElementEventFilter(selector:string)

Parameters

|          |        |                        |
| -------- | ------ | ---------------------- |
| selector | string | A valid CSS3 selector. |

Return value

void

#### addPlugin\<O,P>[​](#addpluginop "Direct link to addpluginop")

Add a plugin to the UI. You can provide a type parameter to this method to avoid having to cast the return

<br />

value, if you need to retain a reference to the plugin.

Signature

addPlugin(pluginSpec:[UIPluginSpec\<O>]())

Type Parameters

|   |                                        |                                                                       |
| - | -------------------------------------- | --------------------------------------------------------------------- |
| O | [UIPluginOptions]()                    | Defines the options type for the plugin to add                        |
| P | [UIPlugin<]()[BrowserElement](),O,any> | Defines the type of the plugin that will be returned from this method |

Parameters

|            |                      |   |
| ---------- | -------------------- | - |
| pluginSpec | [UIPluginSpec\<O>]() |   |

Return value

P

#### addToDragGroup[​](#addtodraggroup "Direct link to addToDragGroup")

Adds the given element(s) to the given drag group.

Signature

addToDragGroup(spec:[DragGroupSpec](), els:Array\<string | [Node]() | [Group]() | [BrowserElement]()>)

Parameters

|      |                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| ---- | ------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| spec | [DragGroupSpec]()                                             | Either the ID of some drag group, in which case the elements are all added as 'active', or an object containing the ID of the drag group and the element's participation in the group. `active` participation, which is the default, indicates whether dragging the given element(s) should cause all the elements in the drag group to be dragged. If `active` is false it means the given element(s) is "passive" and should only move when an active member of the drag group is dragged. The elements passed in to this method will be added to the drag group with an `added` membership flag, meaning any drag group an element has been added to via this method will take precedence over a drag group an element gets added to via a drag group assigner (see the DragGroupsPlugin for a discussion of automatically assigning elements to drag groups) |
| els  | Array\<string \| [Node]() \| [Group]() \| [BrowserElement]()> | Elements to add to the drag group.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |

Return value

void

#### addVertexDragFilter[​](#addvertexdragfilter "Direct link to addVertexDragFilter")

Adds a filter function to the drag handler. A drag cannot start if this function returns false. See also #addDragSelectorFilter

Signature

addVertexDragFilter(f:[VertexDragFilter<]()[BrowserElement]()>)

Parameters

|   |                                          |                                                  |
| - | ---------------------------------------- | ------------------------------------------------ |
| f | [VertexDragFilter<]()[BrowserElement]()> | Function that can return false to disallow drag. |

Return value

void

#### addWheelSelectorFilter[​](#addwheelselectorfilter "Direct link to addWheelSelectorFilter")

Adds a CSS selector filter to the wheel event.

Signature

addWheelSelectorFilter(selector:string)

Parameters

|          |        |   |
| -------- | ------ | - |
| selector | string |   |

Return value

void

#### adHocGroupLayout[​](#adhocgrouplayout "Direct link to adHocGroupLayout")

Run an adhoc layout on the given group. The layout will be applied one time, and then the previous layout will be restored (but not run, of course, otherwise the results of this adhoc layout would be overwritten!).

Signature

adHocGroupLayout(group:string | [Group](), layoutParams:{

<br />

  options:[LayoutParameters](),

<br />

  type:string

<br />

})

Parameters

|              |                                                                  |                                            |
| ------------ | ---------------------------------------------------------------- | ------------------------------------------ |
| group        | string \| [Group]()                                              | The group on which to run an adhoc layout. |
| layoutParams | {<br />  options:[LayoutParameters](),<br />  type:string<br />} | Params for the adhoc layout.               |

Return value

void

#### adHocLayout\<LP>[​](#adhoclayoutlp "Direct link to adhoclayoutlp")

Run an adhoc layout on the viewport, inside a transaction, so the entire operation can be undone at once.

<br />

Note that invoking this method also has the effect of clearing the geometry of every edge and resetting edge

<br />

paths to the default computed values: edge paths are linked to their vertex locations, and this method can

<br />

move any vertex from its current location.

Signature

adHocLayout(layoutParams:{

<br />

  options:LP,

<br />

  type:string

<br />

})

Type Parameters

|    |                      |   |
| -- | -------------------- | - |
| LP | [LayoutParameters]() |   |

Parameters

|              |                                                |                              |
| ------------ | ---------------------------------------------- | ---------------------------- |
| layoutParams | {<br />  options:LP,<br />  type:string<br />} | Spec for the layout to apply |

Return value

void

#### alignBackground[​](#alignbackground "Direct link to alignBackground")

Positions the widget so that the edges of the background align with the viewport. This method is useful for snapping to a corner of the background.

Signature

alignBackground(axes:string, animationDuration:number)

Parameters

|                   |        |                                                                                                                                                                                                                                              |
| ----------------- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| axes              | string | Spec for the axes to align to. This should be a space-separated string containing a value<br />for the x (allowed values `left` and `right`) and, optionally, y (allowed values `top` and `bottom`) axes. The default value is `"left top"`. |
| animationDuration | number | Defaults to 150ms                                                                                                                                                                                                                            |

Return value

void

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

#### attachMiniview[​](#attachminiview "Direct link to attachMiniview")

Attach a miniview to this Surface. This is a shortcut for adding one via addPlugin.

Signature

attachMiniview(options:[MiniviewPluginOptions]())

Parameters

|         |                           |   |
| ------- | ------------------------- | - |
| options | [MiniviewPluginOptions]() |   |

Return value

void

#### autoSizeGroup[​](#autosizegroup "Direct link to autoSizeGroup")

Run the group auto size routine on a given group (as well as any ancestor groups), and moves elements around as necessary

Signature

autoSizeGroup(group:[Group](), force:boolean)

Parameters

|       |           |                                                                                                  |
| ----- | --------- | ------------------------------------------------------------------------------------------------ |
| group | [Group]() | The group to auto size                                                                           |
| force | boolean   | If true, this flag will override an `autoSize:false` directive on the Group (and any ancestors). |

Return value

GroupResizeResult<[BrowserElement]()>

#### autoSizeGroups[​](#autosizegroups "Direct link to autoSizeGroups")

Update the size of the given list of groups so that its content area encompasses all of the child elements of the group, unless `force` is not specified and a specific group has `autoSize` set to false.

Signature

autoSizeGroups(groups:Array<[Group]()>, force:boolean)

Parameters

|        |                  |                                                                                                               |
| ------ | ---------------- | ------------------------------------------------------------------------------------------------------------- |
| groups | Array<[Group]()> | Groups to size. If null, every group is auto sized.                                                           |
| force  | boolean          | If true, this flag will override an autoSize<!-- -->:false<!-- --> directive on the Group (and any ancestors) |

Return value

Record\<string,GroupResizeResult\<EL>>

#### batch[​](#batch "Direct link to batch")

Wraps the underlying model's `batch` function with the added step of first suspending events being fired from this renderer.

Signature

batch(fn:() => any)

Parameters

|    |           |                                                                |
| -- | --------- | -------------------------------------------------------------- |
| fn | () => any | Function to run while rendering and events are both suspended. |

Return value

void

#### bind\<T>[​](#bindt "Direct link to bindt")

Bind a listener to the named event, optionally inserting the listener at the head of the queue for the given event.

Signature

bind(event:"pan" | "zoom" | "group

<!-- -->

:removed

<!-- -->

" | "edge

<!-- -->

:removed

<!-- -->

" | "node

<!-- -->

:removed

<!-- -->

" | "edge

<!-- -->

:geometry

<!-- -->

" | "edge

<!-- -->

:dragStart

<!-- -->

" | "edge

<!-- -->

:drag

<!-- -->

" | "edge

<!-- -->

:dragEnd

<!-- -->

" | "edge

<!-- -->

:dragAbort

<!-- -->

" | "group:move

<!-- -->

:start

<!-- -->

" | "group

<!-- -->

:move

<!-- -->

" | "group:move

<!-- -->

:end

<!-- -->

" | "internal:edge

<!-- -->

:redraw

<!-- -->

" | "node:move

<!-- -->

:start

<!-- -->

" | "node

<!-- -->

:move

<!-- -->

" | "node:move

<!-- -->

:end

<!-- -->

" | "node:move

<!-- -->

:abort

<!-- -->

" | "destroy" | "internal.connection" | "internal.element

<!-- -->

:repainted

<!-- -->

" | "group

<!-- -->

:collapse

<!-- -->

" | "group

<!-- -->

:expand

<!-- -->

" | "render

<!-- -->

:start

<!-- -->

" | "render

<!-- -->

:end

<!-- -->

" | "adhocLayout" | "afterLayoutRefresh" | "group

<!-- -->

:relayout

<!-- -->

" | "group

<!-- -->

:render

<!-- -->

" | "internal.vertex

<!-- -->

:updated

<!-- -->

" | "node

<!-- -->

:render

<!-- -->

" | "node

<!-- -->

:visibility

<!-- -->

" | "plugin

<!-- -->

:added

<!-- -->

" | "plugin

<!-- -->

:removed

<!-- -->

" | "relayout" | "vertex

<!-- -->

:click

<!-- -->

" | "vertex

<!-- -->

:dblclick

<!-- -->

" | "vertex

<!-- -->

:dbltap

<!-- -->

" | "vertex

<!-- -->

:mouseout

<!-- -->

" | "vertex

<!-- -->

:mouseover

<!-- -->

" | "vertex

<!-- -->

:mousemove

<!-- -->

" | "vertex

<!-- -->

:mouseup

<!-- -->

" | "vertex

<!-- -->

:mousedown

<!-- -->

" | "vertex

<!-- -->

:contextmenu

<!-- -->

" | "vertex

<!-- -->

:tap

<!-- -->

" | "edge

<!-- -->

:click

<!-- -->

" | "edge

<!-- -->

:dblclick

<!-- -->

" | "edge

<!-- -->

:mouseout

<!-- -->

" | "edge

<!-- -->

:mouseover

<!-- -->

" | "edge

<!-- -->

:mouseup

<!-- -->

" | "edge

<!-- -->

:mousedown

<!-- -->

" | "edge

<!-- -->

:contextmenu

<!-- -->

" | "canvasClick" | "canvasDblClick" | "edge

<!-- -->

:redraw

<!-- -->

" | "modeChanged", listener:(payload:T, evt:any) => any, insertAtStart:boolean)

Type Parameters

|   |   |                                                                                                                                       |
| - | - | ------------------------------------------------------------------------------------------------------------------------------------- |
| T |   | The type of the payload you expect to be passed to your callback. Using this is helpful to ensure your callbacks are typed correctly. |

Parameters

|               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |                                                                                                                |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| event         | "pan" \| "zoom" \| "group<!-- -->:removed<!-- -->" \| "edge<!-- -->:removed<!-- -->" \| "node<!-- -->:removed<!-- -->" \| "edge<!-- -->:geometry<!-- -->" \| "edge<!-- -->:dragStart<!-- -->" \| "edge<!-- -->:drag<!-- -->" \| "edge<!-- -->:dragEnd<!-- -->" \| "edge<!-- -->:dragAbort<!-- -->" \| "group:move<!-- -->:start<!-- -->" \| "group<!-- -->:move<!-- -->" \| "group:move<!-- -->:end<!-- -->" \| "internal:edge<!-- -->:redraw<!-- -->" \| "node:move<!-- -->:start<!-- -->" \| "node<!-- -->:move<!-- -->" \| "node:move<!-- -->:end<!-- -->" \| "node:move<!-- -->:abort<!-- -->" \| "destroy" \| "internal.connection" \| "internal.element<!-- -->:repainted<!-- -->" \| "group<!-- -->:collapse<!-- -->" \| "group<!-- -->:expand<!-- -->" \| "render<!-- -->:start<!-- -->" \| "render<!-- -->:end<!-- -->" \| "adhocLayout" \| "afterLayoutRefresh" \| "group<!-- -->:relayout<!-- -->" \| "group<!-- -->:render<!-- -->" \| "internal.vertex<!-- -->:updated<!-- -->" \| "node<!-- -->:render<!-- -->" \| "node<!-- -->:visibility<!-- -->" \| "plugin<!-- -->:added<!-- -->" \| "plugin<!-- -->:removed<!-- -->" \| "relayout" \| "vertex<!-- -->:click<!-- -->" \| "vertex<!-- -->:dblclick<!-- -->" \| "vertex<!-- -->:dbltap<!-- -->" \| "vertex<!-- -->:mouseout<!-- -->" \| "vertex<!-- -->:mouseover<!-- -->" \| "vertex<!-- -->:mousemove<!-- -->" \| "vertex<!-- -->:mouseup<!-- -->" \| "vertex<!-- -->:mousedown<!-- -->" \| "vertex<!-- -->:contextmenu<!-- -->" \| "vertex<!-- -->:tap<!-- -->" \| "edge<!-- -->:click<!-- -->" \| "edge<!-- -->:dblclick<!-- -->" \| "edge<!-- -->:mouseout<!-- -->" \| "edge<!-- -->:mouseover<!-- -->" \| "edge<!-- -->:mouseup<!-- -->" \| "edge<!-- -->:mousedown<!-- -->" \| "edge<!-- -->:contextmenu<!-- -->" \| "canvasClick" \| "canvasDblClick" \| "edge<!-- -->:redraw<!-- -->" \| "modeChanged" | Name of the event to bind                                                                                      |
| listener      | (payload:T, evt:any) => any                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Function to bind to the event                                                                                  |
| insertAtStart | boolean                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Defaults to false. If true, this handler is inserted at the head of the list of listeners for the given event. |

Return value

EventGenerator

#### bindAll\<T>[​](#bindallt "Direct link to bindallt")

Bind a listener to all of the named events, optionally inserting each one at the head of the queue for the given event.

Signature

bindAll(events:Array<"pan" | "zoom" | "group

<!-- -->

:removed

<!-- -->

" | "edge

<!-- -->

:removed

<!-- -->

" | "node

<!-- -->

:removed

<!-- -->

" | "edge

<!-- -->

:geometry

<!-- -->

" | "edge

<!-- -->

:dragStart

<!-- -->

" | "edge

<!-- -->

:drag

<!-- -->

" | "edge

<!-- -->

:dragEnd

<!-- -->

" | "edge

<!-- -->

:dragAbort

<!-- -->

" | "group:move

<!-- -->

:start

<!-- -->

" | "group

<!-- -->

:move

<!-- -->

" | "group:move

<!-- -->

:end

<!-- -->

" | "internal:edge

<!-- -->

:redraw

<!-- -->

" | "node:move

<!-- -->

:start

<!-- -->

" | "node

<!-- -->

:move

<!-- -->

" | "node:move

<!-- -->

:end

<!-- -->

" | "node:move

<!-- -->

:abort

<!-- -->

" | "destroy" | "internal.connection" | "internal.element

<!-- -->

:repainted

<!-- -->

" | "group

<!-- -->

:collapse

<!-- -->

" | "group

<!-- -->

:expand

<!-- -->

" | "render

<!-- -->

:start

<!-- -->

" | "render

<!-- -->

:end

<!-- -->

" | "adhocLayout" | "afterLayoutRefresh" | "group

<!-- -->

:relayout

<!-- -->

" | "group

<!-- -->

:render

<!-- -->

" | "internal.vertex

<!-- -->

:updated

<!-- -->

" | "node

<!-- -->

:render

<!-- -->

" | "node

<!-- -->

:visibility

<!-- -->

" | "plugin

<!-- -->

:added

<!-- -->

" | "plugin

<!-- -->

:removed

<!-- -->

" | "relayout" | "vertex

<!-- -->

:click

<!-- -->

" | "vertex

<!-- -->

:dblclick

<!-- -->

" | "vertex

<!-- -->

:dbltap

<!-- -->

" | "vertex

<!-- -->

:mouseout

<!-- -->

" | "vertex

<!-- -->

:mouseover

<!-- -->

" | "vertex

<!-- -->

:mousemove

<!-- -->

" | "vertex

<!-- -->

:mouseup

<!-- -->

" | "vertex

<!-- -->

:mousedown

<!-- -->

" | "vertex

<!-- -->

:contextmenu

<!-- -->

" | "vertex

<!-- -->

:tap

<!-- -->

" | "edge

<!-- -->

:click

<!-- -->

" | "edge

<!-- -->

:dblclick

<!-- -->

" | "edge

<!-- -->

:mouseout

<!-- -->

" | "edge

<!-- -->

:mouseover

<!-- -->

" | "edge

<!-- -->

:mouseup

<!-- -->

" | "edge

<!-- -->

:mousedown

<!-- -->

" | "edge

<!-- -->

:contextmenu

<!-- -->

" | "canvasClick" | "canvasDblClick" | "edge

<!-- -->

:redraw

<!-- -->

" | "modeChanged">, listener:(payload:T, evt:any) => any, insertAtStart:boolean)

Type Parameters

|   |   |                                                                                                                                       |
| - | - | ------------------------------------------------------------------------------------------------------------------------------------- |
| T |   | The type of the payload you expect to be passed to your callback. Using this is helpful to ensure your callbacks are typed correctly. |

Parameters

|               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |   |
| ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | - |
| events        | Array<"pan" \| "zoom" \| "group<!-- -->:removed<!-- -->" \| "edge<!-- -->:removed<!-- -->" \| "node<!-- -->:removed<!-- -->" \| "edge<!-- -->:geometry<!-- -->" \| "edge<!-- -->:dragStart<!-- -->" \| "edge<!-- -->:drag<!-- -->" \| "edge<!-- -->:dragEnd<!-- -->" \| "edge<!-- -->:dragAbort<!-- -->" \| "group:move<!-- -->:start<!-- -->" \| "group<!-- -->:move<!-- -->" \| "group:move<!-- -->:end<!-- -->" \| "internal:edge<!-- -->:redraw<!-- -->" \| "node:move<!-- -->:start<!-- -->" \| "node<!-- -->:move<!-- -->" \| "node:move<!-- -->:end<!-- -->" \| "node:move<!-- -->:abort<!-- -->" \| "destroy" \| "internal.connection" \| "internal.element<!-- -->:repainted<!-- -->" \| "group<!-- -->:collapse<!-- -->" \| "group<!-- -->:expand<!-- -->" \| "render<!-- -->:start<!-- -->" \| "render<!-- -->:end<!-- -->" \| "adhocLayout" \| "afterLayoutRefresh" \| "group<!-- -->:relayout<!-- -->" \| "group<!-- -->:render<!-- -->" \| "internal.vertex<!-- -->:updated<!-- -->" \| "node<!-- -->:render<!-- -->" \| "node<!-- -->:visibility<!-- -->" \| "plugin<!-- -->:added<!-- -->" \| "plugin<!-- -->:removed<!-- -->" \| "relayout" \| "vertex<!-- -->:click<!-- -->" \| "vertex<!-- -->:dblclick<!-- -->" \| "vertex<!-- -->:dbltap<!-- -->" \| "vertex<!-- -->:mouseout<!-- -->" \| "vertex<!-- -->:mouseover<!-- -->" \| "vertex<!-- -->:mousemove<!-- -->" \| "vertex<!-- -->:mouseup<!-- -->" \| "vertex<!-- -->:mousedown<!-- -->" \| "vertex<!-- -->:contextmenu<!-- -->" \| "vertex<!-- -->:tap<!-- -->" \| "edge<!-- -->:click<!-- -->" \| "edge<!-- -->:dblclick<!-- -->" \| "edge<!-- -->:mouseout<!-- -->" \| "edge<!-- -->:mouseover<!-- -->" \| "edge<!-- -->:mouseup<!-- -->" \| "edge<!-- -->:mousedown<!-- -->" \| "edge<!-- -->:contextmenu<!-- -->" \| "canvasClick" \| "canvasDblClick" \| "edge<!-- -->:redraw<!-- -->" \| "modeChanged"> |   |
| listener      | (payload:T, evt:any) => any                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |   |
| insertAtStart | boolean                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |   |

Return value

EventGenerator

#### bindModelEvent\<T>[​](#bindmodeleventt "Direct link to bindmodeleventt")

Binds to a mouse event occurring on a given model object. This is a wrapper around the `on` event binding method, which searches for an associated model object for the given event. For instance, you might have a node template that has a button inside of it that you want to respond to. When the button is clicked you want to know the node associated with the button. This method provides that. It is possible to find the associated model object yourself, via the `getObjectInfo` method of the Surface, called with the event's target, but this method does that for you.

<br />

<br />

You can, optionally, provide a type hint to this method in order to fix the type of the returned model object, but note that this is erased at runtime and the type of the returned object is not guaranteed by the surface.

<br />

<br />

This method binds a delegated event handler on the container element used by the surface. You do not need to provide an element to which to bind; you just need to provide an appropriate selector

Signature

bindModelEvent(event:string, selector:string, callback:[ModelEventCallback\<T>]())

Type Parameters

|   |                                                             |   |
| - | ----------------------------------------------------------- | - |
| T | [Node]() \| [Edge]() \| [Group]() \| [Vertex]() \| [Port]() |   |

Parameters

|          |                            |                                                                                                                 |
| -------- | -------------------------- | --------------------------------------------------------------------------------------------------------------- |
| event    | string                     | Name of the event to bind to.                                                                                   |
| selector | string                     | CSS3 selector that identifies children of a vertex DOM element on which the event handler should<br />be bound. |
| callback | [ModelEventCallback\<T>]() | Function to call when the event is fired.                                                                       |

Return value

void

#### bindUnchecked\<T>[​](#binduncheckedt "Direct link to binduncheckedt")

Bind an event listener. This method can be used with a type parameter by call sites; although it's not necessary it can be helpful to use this to ensure you've thought about what the payload to your event handler is going to be.

Signature

bindUnchecked(event:string, listener:(a:T, e:any) => any, insertAtStart:boolean)

Type Parameters

|   |   |                                                                                                                                       |
| - | - | ------------------------------------------------------------------------------------------------------------------------------------- |
| T |   | The type of the payload you expect to be passed to your callback. Using this is helpful to ensure your callbacks are typed correctly. |

Parameters

|               |                     |                                                                                              |
| ------------- | ------------------- | -------------------------------------------------------------------------------------------- |
| event         | string              | Name of the event(s) to bind to.                                                             |
| listener      | (a:T, e:any) => any | Function to bind to the given event(s)                                                       |
| insertAtStart | boolean             | Whether or not to insert this listener at the head of the listener queue. Defaults to false. |

Return value

EventGenerator

#### centerBackground[​](#centerbackground "Direct link to centerBackground")

Position the surface so the background is centered in the viewport, without changing the current zoom.

Signature

centerBackground(params:{

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

#### centerContentHorizontally[​](#centercontenthorizontally "Direct link to centerContentHorizontally")

Centers the tracked content horizontally inside the viewport, but does not adjust the current zoom (so the content may still extend past the viewport bounds)

Signature

centerContentHorizontally(options:[CenterContentHorizontallyOptions]())

Parameters

|         |                                      |                    |
| ------- | ------------------------------------ | ------------------ |
| options | [CenterContentHorizontallyOptions]() | Method parameters. |

Return value

void

#### centerContentVertically[​](#centercontentvertically "Direct link to centerContentVertically")

Centers the tracked content vertically inside the viewport, but does not adjust the current zoom (so the content may still extend past the viewport bounds)

Signature

centerContentVertically(options:[CenterContentVerticallyOptions]())

Parameters

|         |                                    |                    |
| ------- | ---------------------------------- | ------------------ |
| options | [CenterContentVerticallyOptions]() | Method parameters. |

Return value

void

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

#### centerOnAndZoom[​](#centeronandzoom "Direct link to centerOnAndZoom")

Center on the current object/objects and zoom in on it/them.

Signature

centerOnAndZoom(element:string | Element | [Vertex]() | Array\<string | Element | [Vertex]()>, fillRatio:number, doNotAnimate:boolean)

Parameters

|              |                                                                            |                                                                                                                                  |
| ------------ | -------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| element      | string \| Element \| [Vertex]() \| Array\<string \| Element \| [Vertex]()> | The element(s) to center. Can be a DOM element, vertex id, or a Node/Group, or an array of these.                                |
| fillRatio    | number                                                                     | How much of the viewport to fill with the object we zoom in on. This will be limited by the current zoom range. Defaults to 0.6. |
| doNotAnimate | boolean                                                                    | by default, this operation will be animated.                                                                                     |

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

#### clearDragGroup[​](#cleardraggroup "Direct link to clearDragGroup")

Removes all members from the drag group with the given name.

Signature

clearDragGroup(name:string)

Parameters

|      |        |   |
| ---- | ------ | - |
| name | string |   |

Return value

void

#### clearPathEdits[​](#clearpathedits "Direct link to clearPathEdits")

Clear the edits for the given connection, returning its path to the automatically computed path.

Signature

clearPathEdits(edgeOrConnection:string | [Edge]() | [Connection<]()[BrowserElement]()>)

Parameters

|                  |                                                          |   |
| ---------------- | -------------------------------------------------------- | - |
| edgeOrConnection | string \| [Edge]() \| [Connection<]()[BrowserElement]()> |   |

Return value

boolean

#### cloneVertex[​](#clonevertex "Direct link to cloneVertex")

Clones the given vertex. NOTE: this does not clone the children of a group. Only the group will be cloned, and it will be empty.

Signature

cloneVertex(vertex:string | Element | [Node]() | [Group](), options:[SurfaceVertexCloneOptions]())

Parameters

|         |                                            |                                                           |
| ------- | ------------------------------------------ | --------------------------------------------------------- |
| vertex  | string \| Element \| [Node]() \| [Group]() |                                                           |
| options | [SurfaceVertexCloneOptions]()              | Optional position to use for the new vertex. May be null. |

Return value

[Node]() | [Group]()

#### collapseGroup[​](#collapsegroup "Direct link to collapseGroup")

Collapse the given group, hiding all of its internal edges and proxying any edges to internal members to the collapsed element (unless the group definition for this group specifies `proxied:false`). Every edge with a source/target that is a descendant of this group is a candidate for proxying.

Signature

collapseGroup(groupIdOrGroup:string | [Group]())

Parameters

|                |                     |   |
| -------------- | ------------------- | - |
| groupIdOrGroup | string \| [Group]() |   |

Return value

void

#### destroy[​](#destroy "Direct link to destroy")

Cleans up the Surface. When using a library integration such as Angular/React/Vue/Svelte, this method will be called automatically when the associated component is unloaded. If you're using vanilla VisaullyJs, you might want to call this method if you're cleaning up your UI and you don't need this Surface any longer.

Signature

destroy()

Return value

void

#### expandGroup[​](#expandgroup "Direct link to expandGroup")

Expand a collapsed group, unproxying any connections from the collapsed group to their original destination

Signature

expandGroup(groupIdOrGroup:string | [Group]())

Parameters

|                |                     |   |
| -------------- | ------------------- | - |
| groupIdOrGroup | string \| [Group]() |   |

Return value

void

#### findEnclosedVertices[​](#findenclosedvertices "Direct link to findEnclosedVertices")

Finds all of the vertices that are enclosed by the rectangle described by `origin` and `dimensions`.

Signature

findEnclosedVertices(options:[EnclosedVerticesOptions]())

Parameters

|         |                             |                                 |
| ------- | --------------------------- | ------------------------------- |
| options | [EnclosedVerticesOptions]() | Options for the find operation. |

Return value

Array<[IntersectingVertex<]()[BrowserElement]()>>

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

#### fixElement[​](#fixelement "Direct link to fixElement")

Appends an element to the viewport such that it is zoomed with everything else, but constrains placement in one or both axes so that the element remains fixed with respect to the viewport origin as the canvas pans and/or zooms. Note that this method will set `position:absolute` on the element you are fixing, because otherwise it would mess up the placement of the other content on the canvas. If you subsequently `unfix` an element, the UI does not remove the `position:absolute` style.

Signature

fixElement(el:[BrowserElement](), pos:[PointXY](), constraints:[FixedElementConstraints](), id:string, onTop:boolean)

Parameters

|             |                             |                                                            |
| ----------- | --------------------------- | ---------------------------------------------------------- |
| el          | [BrowserElement]()          | The BrowserElement to append.                              |
| pos         | [PointXY]()                 | Location of the element's origin.                          |
| constraints | [FixedElementConstraints]() | Flags to indicate optional constraint to each axis.        |
| id          | string                      | Optional ID to assign to the element, for future retrieval |
| onTop       | boolean                     |                                                            |

Return value

FixedElement

#### flashSelection[​](#flashselection "Direct link to flashSelection")

Flash the nodes and groups in the given selection.

Signature

flashSelection(sel:[VisuallyJsSelection](), duration:number, animName:string)

Parameters

|          |                         |                                                                                              |
| -------- | ----------------------- | -------------------------------------------------------------------------------------------- |
| sel      | [VisuallyJsSelection]() | Selection to flash nodes and groups for                                                      |
| duration | number                  | Optional; defaults to 1000ms. Duration of the animation, in milliseconds.                    |
| animName | string                  | Optional; the name of the CSS animation to apply. Defaults to ANIM\_SURFACE\_ELEMENT\_FLASH. |

Return value

void

#### flashVertex[​](#flashvertex "Direct link to flashVertex")

Flash the given vertex or vertices.

Signature

flashVertex(vertices:string | Element | [Node]() | [Group]() | Array\<string | Element | [Node]() | [Group]()>, duration:number, animName:string)

Parameters

|          |                                                                                                  |                                                                                              |
| -------- | ------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------- |
| vertices | string \| Element \| [Node]() \| [Group]() \| Array\<string \| Element \| [Node]() \| [Group]()> | Either a vertex, a vertex id, or an element, or an array of any of these.                    |
| duration | number                                                                                           | Optional; defaults to 1000ms. Duration of the animation in milliseconds.                     |
| animName | string                                                                                           | Optional; the name of the CSS animation to apply. Defaults to ANIM\_SURFACE\_ELEMENT\_FLASH. |

Return value

void

#### floatElement[​](#floatelement "Direct link to floatElement")

Appends an element to the viewport so that it floats above the content that is being zoomed and panned. The element will have `position:absolute` set on it. You can float any element you like, but note that the responsibility for setting an appropriate z index is yours.

Signature

floatElement(el:[BrowserElement](), pos:[PointXY]())

Parameters

|     |                    |                                                                                                                                                                               |
| --- | ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| el  | [BrowserElement]() | Element to float.                                                                                                                                                             |
| pos | [PointXY]()        | Position to float the element at. This is in page coordinates, ie. it ignores the pan/zoom of the surface, and defines a position relative to the viewport's top/left corner. |

Return value

void

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

#### gather[​](#gather "Direct link to gather")

Gather the elements in the display. If `focus` is provided the elements will be gathered around it. Otherwise, the elements will be gathered around the computed center of all the elements.

Signature

gather(focus:string | [Vertex]())

Parameters

|       |                      |                                                                                 |
| ----- | -------------------- | ------------------------------------------------------------------------------- |
| focus | string \| [Vertex]() | Optional ID of a Vertex, or the Vertex itself, around which to gather elements. |

Return value

void

#### getDecorator\<T>[​](#getdecoratort "Direct link to getdecoratort")

Gets the decorator with the given id, or null if not found.

Signature

getDecorator(id:string)

Type Parameters

|   |               |   |
| - | ------------- | - |
| T | [Decorator]() |   |

Parameters

|    |        |   |
| -- | ------ | - |
| id | string |   |

Return value

T

#### getEffectiveVisibleZoom[​](#geteffectivevisiblezoom "Direct link to getEffectiveVisibleZoom")

Gets the zoom as seen by the user, which is a function of the zoom of this surface and of any parent surface, plus any other scale transforms that may be in place in the DOM.

Signature

getEffectiveVisibleZoom()

Return value

number

#### getElementFromEvent[​](#getelementfromevent "Direct link to getElementFromEvent")

Get the model object + DOM element on which the given event occurred.

Signature

getElementFromEvent(e:MouseEvent)

Parameters

|   |            |   |
| - | ---------- | - |
| e | MouseEvent |   |

Return value

ViewportElement<[BrowserElement]()>

#### getGrid[​](#getgrid "Direct link to getGrid")

Get the grid for this instance. May be null.

Signature

getGrid()

Return value

[Grid]()

#### getGroupContentExtents[​](#getgroupcontentextents "Direct link to getGroupContentExtents")

Compute the extents of all the child members of the given group, by default with respect to the group's origin, which effectively gives you the internal size required by the group, or, if you set `relativeToCanvasOrigin`, with respect to the canvas origin.

Signature

getGroupContentExtents(group:[Group](), relativeToCanvasOrigin:boolean)

Parameters

|                        |           |                               |
| ---------------------- | --------- | ----------------------------- |
| group                  | [Group]() | The group to find extents for |
| relativeToCanvasOrigin | boolean   | Defaults to false.            |

Return value

Extents

#### getLabelLocationAttribute[​](#getlabellocationattribute "Direct link to getLabelLocationAttribute")

Gets the name of the attribute that is used to determine the label for the given edge.

Signature

getLabelLocationAttribute(edge:[Edge]())

Parameters

|      |          |   |
| ---- | -------- | - |
| edge | [Edge]() |   |

Return value

string

#### getLayout[​](#getlayout "Direct link to getLayout")

Gets the Layout this surface is currently using.

Signature

getLayout()

Return value

[AbstractLayout\<any>]()

#### getModelPositionAttributes[​](#getmodelpositionattributes "Direct link to getModelPositionAttributes")

Returns the names of the attributes used to store positioning information in the model. Mostly an internal

<br />

method but exposed in case it proves useful to someone.

Signature

getModelPositionAttributes()

Return value

{

<br />

  x:string,

<br />

  y:string

<br />

}

#### getObjectInfo\<V>[​](#getobjectinfov "Direct link to getobjectinfov")

Decodes the given input into a data structure containing a model object, its type, its ID, and the element used to represent it. Always returns a value even if no model object could be resolved for the given input, because in some circumstances the given input represents an element from the UI that is not in the model (such as when dragging a new edge)

Signature

getObjectInfo(obj:string | [Base]() | [ObjectData]() | [BrowserElement]() | [Connection<]()[BrowserElement]()>, createMissingPorts:boolean)

Type Parameters

|   |          |                                                                                                                                                                                        |
| - | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| V | [Base]() | The type of object you're expecting back from the method. This is for convenience, so that the `obj` member of the return value is typed conveniently for what you want to do with it. |

Parameters

|                    |                                                                                                  |                                                                                                                                        |
| ------------------ | ------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------- |
| obj                | string \| [Base]() \| [ObjectData]() \| [BrowserElement]() \| [Connection<]()[BrowserElement]()> | Object to decode. Can be in many different forms - an existing model object, a vertex id, an element, a Connection, some backing data. |
| createMissingPorts | boolean                                                                                          |                                                                                                                                        |

Return value

[UIObjectInfo<]()[V](),[BrowserElement]()>

#### getPan[​](#getpan "Direct link to getPan")

Gets the current origin of the panned content.

Signature

getPan()

Return value

[PointXY]()

#### getPath[​](#getpath "Direct link to getPath")

Gets a Path from some source Vertex to some target Vertex. This method is a wrapper around the model's `getPath` method, adding a few ui specific functions to the result.

Signature

getPath(params:[PathOptions]())

Parameters

|        |                 |                  |
| ------ | --------------- | ---------------- |
| params | [PathOptions]() | Path spec params |

Return value

UIPath

#### getPlugin\<P>[​](#getpluginp "Direct link to getpluginp")

Gets the plugin registered for the given type, null if nothing matching found.

Signature

getPlugin(pluginType:string)

Type Parameters

|   |                                          |   |
| - | ---------------------------------------- | - |
| P | [UIPlugin<]()[BrowserElement](),any,any> |   |

Parameters

|            |        |   |
| ---------- | ------ | - |
| pluginType | string |   |

Return value

P

#### getRenderedConnection[​](#getrenderedconnection "Direct link to getRenderedConnection")

Gets the underlying connection that was rendered for the Edge with the given id.

Signature

getRenderedConnection(edgeId:string)

Parameters

|        |        |                                                |
| ------ | ------ | ---------------------------------------------- |
| edgeId | string | ID of the Edge to retrieve the Connection for. |

Return value

[Connection<]()[BrowserElement]()>

#### getRenderedElement[​](#getrenderedelement "Direct link to getRenderedElement")

For some node/group, get the element that was used to render it.

Signature

getRenderedElement(obj:string | [Base]())

Parameters

|     |                    |   |
| --- | ------------------ | - |
| obj | string \| [Base]() |   |

Return value

[BrowserElement]()

#### getRenderedPort[​](#getrenderedport "Direct link to getRenderedPort")

Gets the DOM node that was rendered for the Port with the given id (does not retrieve `vjs-endpoint` elements)

Signature

getRenderedPort(portIdOrPort:string | [Port]())

Parameters

|              |                    |                                                                                                                                                                                                                    |
| ------------ | ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| portIdOrPort | string \| [Port]() | Either the port, or the id of the port for which to retrieve the rendered element. Note that you must supply a "full" id here, that is in dotted notation with the id of the Node/Group on which the port resides. |

Return value

[BrowserElement]()

#### getViewportBoundsInfo[​](#getviewportboundsinfo "Direct link to getViewportBoundsInfo")

Gets the current bounds information.

Signature

getViewportBoundsInfo()

Return value

[ViewportBounds]()

#### getZoom[​](#getzoom "Direct link to getZoom")

Gets the current zoom.

Signature

getZoom()

Return value

number

#### getZoomRange[​](#getzoomrange "Direct link to getZoomRange")

Gets the current zoom range.

Signature

getZoomRange()

Return value

[ZoomRange]()

#### hasClass[​](#hasclass "Direct link to hasClass")

Returns whether the DOM element represented by `el` - which can be an Edge, Connection, Node, Group, DOM element, or ID of some model object - has the given class.

Signature

hasClass(el:SupportsClassManipulationElement, clazz:string)

Parameters

|       |                                  |   |
| ----- | -------------------------------- | - |
| el    | SupportsClassManipulationElement |   |
| clazz | string                           |   |

Return value

boolean

#### isDraggable[​](#isdraggable "Direct link to isDraggable")

Helper method to get the draggable state of some element. Under the hood all this does is check for the

<br />

existence of the `data-vjs-not-draggable` attribute.

Signature

isDraggable(el:[BrowserElement]())

Parameters

|    |                    |                                     |
| -- | ------------------ | ----------------------------------- |
| el | [BrowserElement]() | Element to get draggable state for. |

Return value

boolean

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

#### isPageLocationInViewport[​](#ispagelocationinviewport "Direct link to isPageLocationInViewport")

Returns whether or not the given point (relative to page origin) is within the viewport for the widget.

Signature

isPageLocationInViewport(x:number, y:number)

Parameters

|   |        |                             |
| - | ------ | --------------------------- |
| x | number | X location of point to test |
| y | number | Y location of point to test |

Return value

boolean

#### isVisible[​](#isvisible "Direct link to isVisible")

Returns whether or not the given model object is visible.

Signature

isVisible(obj:[Base]())

Parameters

|     |          |   |
| --- | -------- | - |
| obj | [Base]() |   |

Return value

any

#### load[​](#load "Direct link to load")

Load the dataset and the current state of the Surface - its pan and zoom settings, as well as data for any registered data hooks.

Signature

load(data:[SurfaceSaveData](), onload:Function)

Parameters

|        |                     |                                         |
| ------ | ------------------- | --------------------------------------- |
| data   | [SurfaceSaveData]() |                                         |
| onload | Function            | Optional function to invoke after load. |

Return value

void

#### lockGroup[​](#lockgroup "Direct link to lockGroup")

Mark a group as "locked" : edges inside of it cannot be detached, removed or have their paths edited, edges cannot be established to child vertices.

Signature

lockGroup(groupIdOrGroup:string | [Group]())

Parameters

|                |                     |   |
| -------------- | ------------------- | - |
| groupIdOrGroup | string \| [Group]() |   |

Return value

void

#### magnetize[​](#magnetize "Direct link to magnetize")

Magnetize the elements in the display. If `focus` is provided it will be used as the origin for magnetization,

<br />

and not moved (unless `repositionFocus` is true). If no `focus` is provided, the computed center of all the

<br />

elements will be used as the origin.

Signature

magnetize(focus:string | [Vertex](), repositionFocus:boolean)

Parameters

|                 |                      |   |
| --------------- | -------------------- | - |
| focus           | string \| [Vertex]() |   |
| repositionFocus | boolean              |   |

Return value

void

#### magnetizeAtEvent[​](#magnetizeatevent "Direct link to magnetizeAtEvent")

Magnetize the elements in the display, using the location of the given MouseEvent as the origin.

Signature

magnetizeAtEvent(event:MouseEvent)

Parameters

|       |            |   |
| ----- | ---------- | - |
| event | MouseEvent |   |

Return value

void

#### magnetizeAtPoint[​](#magnetizeatpoint "Direct link to magnetizeAtPoint")

Magnetize the elements in the display, using the given point as the origin.

Signature

magnetizeAtPoint(origin:[PointXY]())

Parameters

|        |             |   |
| ------ | ----------- | - |
| origin | [PointXY]() |   |

Return value

void

#### mapEventLocation[​](#mapeventlocation "Direct link to mapEventLocation")

Maps the location of the given event on the page onto the coordinate space of this widget, returning a value representing where the given event appears to be with respect to the origin of the Surface's viewport.

Signature

mapEventLocation(event:MouseEvent)

Parameters

|       |            |   |
| ----- | ---------- | - |
| event | MouseEvent |   |

Return value

[PointXY]()

#### nudgeZoom[​](#nudgezoom "Direct link to nudgeZoom")

Nudges the zoom by the given amount. Zoom will be clamped to the current zoom range in effect and the value that was ultimately set is returned from this function. The value you pass in here is multiplied by 100 to give a percentage value: 1 is 100%, for instance, 0.05 is 5%.

Signature

nudgeZoom(delta:number, e:any)

Parameters

|       |        |                                                    |
| ----- | ------ | -------------------------------------------------- |
| delta | number | Amount to change zoom by.                          |
| e     | any    | Original event that caused the nudge. May be null. |

Return value

number

#### off[​](#off "Direct link to off")

Remove an event binding from the given element or elements.

Signature

off(el:Document | [BrowserElement]() | NodeListOf<[BrowserElement]()>, event:string, callback:Function)

Parameters

|          |                                                                  |                                                               |
| -------- | ---------------------------------------------------------------- | ------------------------------------------------------------- |
| el       | Document \| [BrowserElement]() \| NodeListOf<[BrowserElement]()> | Element, or elements, from which to remove the event binding. |
| event    | string                                                           | Name of the event to unbind.                                  |
| callback | Function                                                         | The function you wish to unbind.                              |

Return value

[Surface]()

#### on[​](#on "Direct link to on")

Bind an event listener to the given element or elements.

Signature

on(el:Document | [BrowserElement]() | NodeListOf<[BrowserElement]()>, event:string, callbackOrSelector:string | Function, callback:Function)

Parameters

|                    |                                                                  |                                                                                                                                                                                                                        |
| ------------------ | ---------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| el                 | Document \| [BrowserElement]() \| NodeListOf<[BrowserElement]()> | Element, or elements, to bind the event listener to.                                                                                                                                                                   |
| event              | string                                                           | Name of the event to bind to.                                                                                                                                                                                          |
| callbackOrSelector | string \| Function                                               | Either a callback function, or a CSS 3 selector. When this is a selector the event listener is bound as a "delegate", ie. the event listeners listens to events on children of the given `el` that match the selector. |
| callback           | Function                                                         | Callback function for event. Only supplied when you're binding a delegated event handler.                                                                                                                              |

Return value

[Surface]()

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

#### refresh[​](#refresh "Direct link to refresh")

Refreshes the layout. For some layouts this is the same as a full relayout.

Signature

refresh(doNotRepaintConnections:boolean)

Parameters

|                         |         |   |
| ----------------------- | ------- | - |
| doNotRepaintConnections | boolean |   |

Return value

void

#### registerDataHook[​](#registerdatahook "Direct link to registerDataHook")

Register a DataHook - a pair of functions that are invoked during a `load` and a `save`. This mechanism is a means you can use for storing/retrieving custom data from the payload the UI exports: in the save method you can decorate the data provided to you with anything you like, but you must ensure that it is serializable, ie. it must be pure data. In your load method you can read out this data and take appropriate action.

Signature

registerDataHook(hook:[DataHook]())

Parameters

|      |              |   |
| ---- | ------------ | - |
| hook | [DataHook]() |   |

Return value

void

#### registerTag[​](#registertag "Direct link to registerTag")

Register a custom tag on the UI. This will only take effect if the UI is using the default VisuallyJs template

<br />

renderer.

Signature

registerTag(tagName:string, handlers:[CustomTagOptions]())

Parameters

|          |                      |   |
| -------- | -------------------- | - |
| tagName  | string               |   |
| handlers | [CustomTagOptions]() |   |

Return value

void

#### relayout[​](#relayout "Direct link to relayout")

Runs a relayout of all vertices in the canvas, and of each group.

Signature

relayout(newParameters:any, doNotRepaintConnections:boolean)

Parameters

|                         |         |   |
| ----------------------- | ------- | - |
| newParameters           | any     |   |
| doNotRepaintConnections | boolean |   |

Return value

void

#### relayoutGroup[​](#relayoutgroup "Direct link to relayoutGroup")

Relayout the given group.

Signature

relayoutGroup(groupOrId:string | [Group](), reason:GroupRelayoutReason)

Parameters

|           |                     |                                                   |
| --------- | ------------------- | ------------------------------------------------- |
| groupOrId | string \| [Group]() | The group - or the ID of the group - to relayout. |
| reason    | GroupRelayoutReason |                                                   |

Return value

void

#### reload[​](#reload "Direct link to reload")

When the UI is rendering a Selection, this method triggers a reload on the selection, causing the UI to be cleared and recreated.

Signature

reload()

Return value

void

#### removeClass[​](#removeclass "Direct link to removeClass")

Removes a class from the DOM element represented by `el`, which can be a Selection, or an instance of many different types - see the `SupportsClassManipulation` interface for a complete list.

Signature

removeClass(el:[VisuallyJsSelection]() | SupportsClassManipulation, clazz:string)

Parameters

|       |                                                      |   |
| ----- | ---------------------------------------------------- | - |
| el    | [VisuallyJsSelection]() \| SupportsClassManipulation |   |
| clazz | string                                               |   |

Return value

void

#### removeDragClassnameFilter[​](#removedragclassnamefilter "Direct link to removeDragClassnameFilter")

Removes a CSS class filter from the drag handler.

Signature

removeDragClassnameFilter(clazz:string | Array\<string>)

Parameters

|       |                          |                                                                                                 |
| ----- | ------------------------ | ----------------------------------------------------------------------------------------------- |
| clazz | string \| Array\<string> | Either a single class name, or a comma separated list of classnames, or an array of classnames. |

Return value

void

#### removeFromDragGroup[​](#removefromdraggroup "Direct link to removeFromDragGroup")

Removes the given element(s) from any drag group they may be in. You don't need to supply the drag group id, as elements can only be in one drag group anyway.

Signature

removeFromDragGroup(els:Array\<string | [Node]() | [Group]() | [BrowserElement]()>)

Parameters

|     |                                                               |                                      |
| --- | ------------------------------------------------------------- | ------------------------------------ |
| els | Array\<string \| [Node]() \| [Group]() \| [BrowserElement]()> | Elements to remove from drag groups. |

Return value

void

#### repaintEdge[​](#repaintedge "Direct link to repaintEdge")

Repaint this edge.

Signature

repaintEdge(edge:[Edge]())

Parameters

|      |          |   |
| ---- | -------- | - |
| edge | [Edge]() |   |

Return value

void

#### repaintEdges[​](#repaintedges "Direct link to repaintEdges")

Repaint this set of edges.

Signature

repaintEdges(edges:Array<[Edge]()>)

Parameters

|       |                 |   |
| ----- | --------------- | - |
| edges | Array<[Edge]()> |   |

Return value

void

#### repaintEverything[​](#repainteverything "Direct link to repaintEverything")

Repaint every connection in the instance.

Signature

repaintEverything(doNotRefreshElements:boolean)

Parameters

|                      |         |   |
| -------------------- | ------- | - |
| doNotRefreshElements | boolean |   |

Return value

void

#### reset[​](#reset "Direct link to reset")

Clears all connections and managed elements from the instance of the UI. Does not also clear out

<br />

event listeners, selectors, or connection types - for that, use `destroy()`.

Signature

reset()

Return value

void

#### rotate[​](#rotate "Direct link to rotate")

Rotate the given vertex by the given number of degrees. The UI element representing the vertex is rotated and the view is updated, and an event is pushed to the undo stack.

Signature

rotate(obj:string | [Vertex](), amountInDegrees:number)

Parameters

|                 |                      |                                     |
| --------------- | -------------------- | ----------------------------------- |
| obj             | string \| [Vertex]() | Either a vertex ID, or a Node/Group |
| amountInDegrees | number               | Amount - in degrees - to rotate.    |

Return value

void

#### save[​](#save "Direct link to save")

Save the dataset and the current state of the Surface - its pan and zoom settings, as well as data for any registered data hooks.

Signature

save(options:[UIExportOptions]())

Parameters

|         |                     |   |
| ------- | ------------------- | - |
| options | [UIExportOptions]() |   |

Return value

[SurfaceSaveData]()

#### saveToUrl[​](#savetourl "Direct link to saveToUrl")

Saves the return value of this object's `save` method via ajax POST to a given URL.

Signature

saveToUrl(options:[SaveOptions]())

Parameters

|         |                 |              |
| ------- | --------------- | ------------ |
| options | [SaveOptions]() | Save options |

Return value

void

#### setApparentCanvasLocation[​](#setapparentcanvaslocation "Direct link to setApparentCanvasLocation")

Sets the apparent canvas location - see the notes for getApparentCanvasLocation.

Signature

setApparentCanvasLocation(left:number, top:number)

Parameters

|      |        |                                          |
| ---- | ------ | ---------------------------------------- |
| left | number | Value in pixels for left edge of canvas. |
| top  | number | Value in pixels for top edge of canvas.  |

Return value

[PointXY]()

#### setClamping[​](#setclamping "Direct link to setClamping")

Sets whether or not the widget clamps the movement of the canvas during pan/zoom to ensure that the managed content never disappears from view.

Signature

setClamping(clamping:boolean)

Parameters

|          |         |                                   |
| -------- | ------- | --------------------------------- |
| clamping | boolean | Whether or not to clamp movement. |

Return value

void

#### setDraggable[​](#setdraggable "Direct link to setDraggable")

Sets whether or not the given element, or element representing the given vertex, is draggable.

Signature

setDraggable(element:string | [Vertex]() | [BrowserElement](), draggable:boolean)

Parameters

|           |                                            |                                   |
| --------- | ------------------------------------------ | --------------------------------- |
| element   | string \| [Vertex]() \| [BrowserElement]() | Vertex id, vertex, or DOM element |
| draggable | boolean                                    |                                   |

Return value

void

#### setDragGroupState[​](#setdraggroupstate "Direct link to setDragGroupState")

Sets the active/passive state for the given element(s) in their respective drag groups (if any). You don't need to supply the drag group id, as elements can only be in one drag group anyway.

Signature

setDragGroupState(state:boolean, els:Array\<string | [Node]() | [Group]() | [BrowserElement]()>)

Parameters

|       |                                                               |                                     |
| ----- | ------------------------------------------------------------- | ----------------------------------- |
| state | boolean                                                       | true for active, false for passive. |
| els   | Array\<string \| [Node]() \| [Group]() \| [BrowserElement]()> |                                     |

Return value

void

#### setEnabled[​](#setenabled "Direct link to setEnabled")

Sets whether the given vertex is enabled for connection drag/drop.

Signature

setEnabled(v:[Vertex](), state:boolean)

Parameters

|       |            |                                      |
| ----- | ---------- | ------------------------------------ |
| v     | [Vertex]() | The vertex to set enabled state for. |
| state | boolean    |                                      |

Return value

boolean

#### setGrid[​](#setgrid "Direct link to setGrid")

Sets the current grid for element dragging, magnetization and group sizing.

Signature

setGrid(grid:[Grid]())

Parameters

|      |          |                                                                         |
| ---- | -------- | ----------------------------------------------------------------------- |
| grid | [Grid]() | Grid to use. If you provide null as the value the grid will be cleared. |

Return value

void

#### setLayout\<LP>[​](#setlayoutlp "Direct link to setlayoutlp")

Apply the given layout to the viewport, by default refreshing the viewport afterwards.

Signature

setLayout(layoutParams:{

<br />

  options:LP,

<br />

  type:string

<br />

}, doNotRefresh:boolean)

Type Parameters

|    |                      |   |
| -- | -------------------- | - |
| LP | [LayoutParameters]() |   |

Parameters

|              |                                                |                                                                              |
| ------------ | ---------------------------------------------- | ---------------------------------------------------------------------------- |
| layoutParams | {<br />  options:LP,<br />  type:string<br />} | Spec for the layout to set.                                                  |
| doNotRefresh | boolean                                        | Defaults to true. Whether or not to repaint the UI after setting the layout. |

Return value

void

#### setMagnetizedPosition[​](#setmagnetizedposition "Direct link to setMagnetizedPosition")

Sets the position of the given node/group and runs the magnetizer, updating the UI and storing results in the model. This operation is wrapped in a transaction so if undo is called then every element affected by the magnetize is relocated.

Signature

setMagnetizedPosition(vertex:string | [Node]() | [Group]() | [BrowserElement](), x:number, y:number)

Parameters

|        |                                                       |   |
| ------ | ----------------------------------------------------- | - |
| vertex | string \| [Node]() \| [Group]() \| [BrowserElement]() |   |
| x      | number                                                |   |
| y      | number                                                |   |

Return value

void

#### setMode[​](#setmode "Direct link to setMode")

Sets the current mode for the surface.

Signature

setMode(mode:[SurfaceMode](), doNotClearSelection:boolean)

Parameters

|                     |                 |                                                                                                                             |
| ------------------- | --------------- | --------------------------------------------------------------------------------------------------------------------------- |
| mode                | [SurfaceMode]() |                                                                                                                             |
| doNotClearSelection | boolean         | Defaults to false - when true, a mode change will not first cause the selection in the<br />underlying model to be cleared. |

Return value

void

#### setOverlayVisible[​](#setoverlayvisible "Direct link to setOverlayVisible")

Sets the visibility of some overlay.

Signature

setOverlayVisible(o:Overlay<[BrowserElement]()>, visible:boolean)

Parameters

|         |                             |                                                                          |
| ------- | --------------------------- | ------------------------------------------------------------------------ |
| o       | Overlay<[BrowserElement]()> | Overlay to hide or show                                                  |
| visible | boolean                     | If true, make the overlay visible, if false, make the overlay invisible. |

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

#### setPanAndZoom[​](#setpanandzoom "Direct link to setPanAndZoom")

Sets the pan and zoom for the Surface in one pass.

Signature

setPanAndZoom(x:number, y:number, zoom:number, animate:boolean)

Parameters

|         |         |                                                                                 |
| ------- | ------- | ------------------------------------------------------------------------------- |
| x       | number  | Value for pan in x axis                                                         |
| y       | number  | Value for pan in Y axis                                                         |
| zoom    | number  | Value fo zoom                                                                   |
| animate | boolean | Defaults to false. If true, the changes will be made with the widget animating. |

Return value

void

#### setPosition[​](#setposition "Direct link to setPosition")

Sets the position of some vertex and updates the model. This method will honour any grid that is currently in effect.

Signature

setPosition(vertex:string | [Node]() | [Group]() | [BrowserElement](), x:number, y:number, magnetize:boolean, force:boolean)

Parameters

|           |                                                       |                                                                                                                                                                                                                                                               |
| --------- | ----------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| vertex    | string \| [Node]() \| [Group]() \| [BrowserElement]() | Node/group id, or some node/group, or the element representing some node/group.                                                                                                                                                                               |
| x         | number                                                | X position, in canvas coordinates, to set.                                                                                                                                                                                                                    |
| y         | number                                                | Y position, in canvas coordinates, to set.                                                                                                                                                                                                                    |
| magnetize | boolean                                               | Whether or not to apply the magnetizer to move other vertices out of this vertex's way.                                                                                                                                                                       |
| force     | boolean                                               | Used in conjunction with magnetize. When null, or true, the element is positioned where requested<br />and other elements move. When false, the element is positioned as close to the requested position as<br />possible, without moving any other elements. |

Return value

void

#### setSize[​](#setsize "Direct link to setSize")

Sets the width and height of the given vertex, updating the UI and the model, and adding an event to the undo stack. NOTE this method may not have entirely the effect you want unless you have `useModelForSizes` set in the constructor options for this UI instance.

Signature

setSize(obj:string | [Vertex](), width:number, height:number)

Parameters

|        |                      |   |
| ------ | -------------------- | - |
| obj    | string \| [Vertex]() |   |
| width  | number               |   |
| height | number               |   |

Return value

void

#### setSuspendRendering[​](#setsuspendrendering "Direct link to setSuspendRendering")

Sets whether rendering is suspended or not.

Signature

setSuspendRendering(val:boolean, thenRefresh:boolean)

Parameters

|             |         |                                                              |
| ----------- | ------- | ------------------------------------------------------------ |
| val         | boolean |                                                              |
| thenRefresh | boolean | If true, the surface will refresh after the change in state. |

Return value

void

#### setViewportCenter[​](#setviewportcenter "Direct link to setViewportCenter")

Sets the location of the canvas such that the given point appears at the center of the viewport.

Signature

setViewportCenter(xy:[PointXY]())

Parameters

|    |             |                                                                                |
| -- | ----------- | ------------------------------------------------------------------------------ |
| xy | [PointXY]() | location of the point on the canvas to position in the center of the viewport. |

Return value

void

#### setVisible[​](#setvisible "Direct link to setVisible")

Sets the visible state of some model object or group of model objects. If the object is a vertex, the visible state will be applied to all edges connected to the given vertex.

<br />

<br />

By default this method will, for groups and nodes, cascade down to any nested vertices.

Signature

setVisible(obj:[Base]() | [FilterableDataset]() | ArrayLike<[Node]() | [Edge]() | [Group]() | [Port]()>, state:boolean, doNotCascade:boolean)

Parameters

|              |                                                                                               |                                                                                                 |
| ------------ | --------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| obj          | [Base]() \| [FilterableDataset]() \| ArrayLike<[Node]() \| [Edge]() \| [Group]() \| [Port]()> | Edge, Group, Node or Port, and array of these, or a `FilterableDataset`, such as a `Selection`. |
| state        | boolean                                                                                       | True if edges should be visible, false otherwise.                                               |
| doNotCascade | boolean                                                                                       | Defaults to false. If true, don't cascade down to any nested vertices.                          |

Return value

void

#### setZoom[​](#setzoom "Direct link to setZoom")

Sets the current zoom, clamping it to the allowed range. Returns the new zoom level - which may or may not be the value you asked for, as it might have been clamped to the current allowed zoom range.

Signature

setZoom(zoom:number, animate:boolean)

Parameters

|         |         |                                                                                                                         |
| ------- | ------- | ----------------------------------------------------------------------------------------------------------------------- |
| zoom    | number  | Zoom value. If this is outside the allowed bounds it will be clamped.                                                   |
| animate | boolean | If true, the surface will animate the transition in zoom by stepping through several intermediate levels in succession. |

Return value

number

#### setZoomRange[​](#setzoomrange "Direct link to setZoomRange")

Sets the current zoom range. By default, this method checks if the current zoom is within the new range, and if it is not then `setZoom` is called, which will cause the zoom to be clamped to an allowed value in the new range. You can disable this by passing `true` for `doNotClamp`.

Signature

setZoomRange(zr:[ZoomRange](), doNotClamp:boolean)

Parameters

|            |               |                                                                                             |
| ---------- | ------------- | ------------------------------------------------------------------------------------------- |
| zr         | [ZoomRange]() | New range, as an array consisting of \[lower, upper] values. Lower must be less than upper. |
| doNotClamp | boolean       | If true, will not check the current zoom to ensure it falls within the new range.           |

Return value

[ZoomRange]()

#### snapPageLocationToGrid[​](#snappagelocationtogrid "Direct link to snapPageLocationToGrid")

Maps the given x,y to canvas coordinates via `fromPageLocation`, snaps that canvas location to the given grid, and then converts the snapped canvas location back to page coordinates.

Signature

snapPageLocationToGrid(x:number, y:number, grid:[Grid]())

Parameters

|      |          |                                        |
| ---- | -------- | -------------------------------------- |
| x    | number   | X position, in page coordinates.       |
| y    | number   | Y position, in page coordinates        |
| grid | [Grid]() | Grid to apply - in canvas coordinates. |

Return value

[PointXY]()

#### snapToGrid[​](#snaptogrid "Direct link to snapToGrid")

Snaps one or all vertices to the current grid or to the grid provided to this method.

Signature

snapToGrid(el:string | [Vertex]() | [BrowserElement](), grid:[Grid]())

Parameters

|      |                                            |                                                                                                                                                              |
| ---- | ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| el   | string \| [Vertex]() \| [BrowserElement]() | ID of vertex, Vertex, or DOM element representing a Vertex.                                                                                                  |
| grid | [Grid]()                                   | Optional grid to snap to. If not provided, the Surface will use the `grid` passed in to its<br />constructor. If that is also null, nothing will be snapped. |

Return value

[MagnetizeResult]()

#### startEditingPath\<T>[​](#starteditingpatht "Direct link to starteditingpatht")

Start editing the given edge or connection, optionally with the given edit parameters.

Signature

startEditingPath(edgeOrConnection:[Edge]() | [Connection<]()[BrowserElement]()>, params:T)

Type Parameters

|   |                                                       |   |
| - | ----------------------------------------------------- | - |
| T | [ConnectorEditorActivateParams<]()[BrowserElement]()> |   |

Parameters

|                  |                                                |   |
| ---------------- | ---------------------------------------------- | - |
| edgeOrConnection | [Edge]() \| [Connection<]()[BrowserElement]()> |   |
| params           | T                                              |   |

Return value

void

#### stopEditingPath[​](#stopeditingpath "Direct link to stopEditingPath")

Stop editing any connector paths.

Signature

stopEditingPath()

Return value

void

#### storePositionsInModel[​](#storepositionsinmodel "Direct link to storePositionsInModel")

Writes the current position for each node into the data model. A common use case is to run an auto layout the

<br />

first time some dataset is seen, and then to save the locations of all the vertices once a human being has moved

<br />

things around.

Signature

storePositionsInModel(params:{

<br />

  leftAttribute:string,

<br />

  topAttribute:string

<br />

})

Parameters

|        |                                                                  |            |
| ------ | ---------------------------------------------------------------- | ---------- |
| params | {<br />  leftAttribute:string,<br />  topAttribute:string<br />} | Parameters |

Return value

void

#### toBack[​](#toback "Direct link to toBack")

Moves the specified element or vertex to the back of its parent’s children in the DOM order. Optionally moves its ancestors to the back as well.

Signature

toBack(v:string | [Vertex]() | [BrowserElement](), alsoSendAncestorsToBack:boolean)

Parameters

|                         |                                            |                                                                             |
| ----------------------- | ------------------------------------------ | --------------------------------------------------------------------------- |
| v                       | string \| [Vertex]() \| [BrowserElement]() | The element, vertex, or browser element to be moved to the back.            |
| alsoSendAncestorsToBack | boolean                                    | If true, the ancestors of the specified element are also moved to the back. |

Return value

void

#### toFront[​](#tofront "Direct link to toFront")

Brings the specified element or vertex to the front within its parent container. Optionally, this method can also ensure all ancestor elements are brought to the front.

Signature

toFront(v:string | [Vertex]() | [BrowserElement](), alsoBringAncestorsToFront:boolean)

Parameters

|                           |                                            |                                                                                                                              |
| ------------------------- | ------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------- |
| v                         | string \| [Vertex]() \| [BrowserElement]() | The element or vertex to be brought to the front. This can be a string identifier, a `Vertex` object, or a `BrowserElement`. |
| alsoBringAncestorsToFront | boolean                                    | Indicates whether the ancestors of the specified element should also be brought to the front. Defaults to `false`.           |

Return value

void

#### toggleClass[​](#toggleclass "Direct link to toggleClass")

Toggles a class on the DOM element represented by `el`, which can be a Selection, or an instance of many different types - see the SupportsClassManipulation type for a complete list.

Signature

toggleClass(el:[VisuallyJsSelection]() | SupportsClassManipulation, clazz:string)

Parameters

|       |                                                      |   |
| ----- | ---------------------------------------------------- | - |
| el    | [VisuallyJsSelection]() \| SupportsClassManipulation |   |
| clazz | string                                               |   |

Return value

void

#### toggleGroup[​](#togglegroup "Direct link to toggleGroup")

Expand a group if it is collapsed, or collapse it if it is expanded.

Signature

toggleGroup(group:string | [Group]())

Parameters

|       |                     |   |
| ----- | ------------------- | - |
| group | string \| [Group]() |   |

Return value

void

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

#### toViewportLocation[​](#toviewportlocation "Direct link to toViewportLocation")

Maps the given canvas location to a point, in page coordinates, relative to the surface container's origin. A return value of \[0,0] from this method indicates the top left corner of the surface's container as seen by the user; negative values for x and/or y mean that the point is not in the visible viewport. Similarly, values for x greater the container width, or y greater than the container height, indicate that the point is not in the visible viewport.

<br />

<br />

This method is useful when you want to position an element over the canvas at some specific canvas location. For instance, the SurfacePopup components use this to position themselves relative to the vertex they are currently referencing.

Signature

toViewportLocation(left:number, top:number)

Parameters

|      |        |   |
| ---- | ------ | - |
| left | number |   |
| top  | number |   |

Return value

[PointXY]()

#### trigger[​](#trigger "Direct link to trigger")

Trigger an event on the given element. Exposed for API users but mostly intended for internal use.

Signature

trigger(el:Document | [BrowserElement](), event:string, originalEvent:Event, payload:any, detail:number)

Parameters

|               |                                |                                                            |
| ------------- | ------------------------------ | ---------------------------------------------------------- |
| el            | Document \| [BrowserElement]() | Element to trigger the event on.                           |
| event         | string                         | Name of the event to trigger.                              |
| originalEvent | Event                          | Optional event that gave rise to this method being called. |
| payload       | any                            | Optional `payload` to set on the Event that is created.    |
| detail        | number                         | Optional detail for the Event that is created.             |

Return value

void

#### unbind[​](#unbind "Direct link to unbind")

Unbind the given event listener, or all listeners. If you call this method with no arguments then all event listeners are unbound.

Signature

unbind(eventOrListener:string | Function, listener:Function)

Parameters

|                 |                    |                                                                       |
| --------------- | ------------------ | --------------------------------------------------------------------- |
| eventOrListener | string \| Function | Either an event name, or an event handler function                    |
| listener        | Function           | If `eventOrListener` is defined, this is the event handler to unbind. |

Return value

EventGenerator

#### unbindModelEvent\<T>[​](#unbindmodeleventt "Direct link to unbindmodeleventt")

Unbinds a listener for a model event.

Signature

unbindModelEvent(event:string, handler:[ModelEventCallback\<T>]())

Type Parameters

|   |   |   |
| - | - | - |
| T |   |   |

Parameters

|         |                            |                              |
| ------- | -------------------------- | ---------------------------- |
| event   | string                     | Name of the event to unbind. |
| handler | [ModelEventCallback\<T>]() | Function to unbind.          |

Return value

void

#### unfixElement[​](#unfixelement "Direct link to unfixElement")

Removes an element that was previously fixed via the fixElement method.

Signature

unfixElement(el:[BrowserElement]())

Parameters

|    |                    |   |
| -- | ------------------ | - |
| el | [BrowserElement]() |   |

Return value

void

#### unlockGroup[​](#unlockgroup "Direct link to unlockGroup")

Unlock a group.

Signature

unlockGroup(groupIdOrGroup:string | [Group]())

Parameters

|                |                     |   |
| -------------- | ------------------- | - |
| groupIdOrGroup | string \| [Group]() |   |

Return value

void

#### zoomIn[​](#zoomin "Direct link to zoomIn")

Zooms in by one step, within the allowed zoom range.

Signature

zoomIn(canvasLoc:[PointXY]())

Parameters

|           |             |   |
| --------- | ----------- | - |
| canvasLoc | [PointXY]() |   |

Return value

void

#### zoomOut[​](#zoomout "Direct link to zoomOut")

Zooms out by one step, within the allowed zoom range.

Signature

zoomOut(canvasLoc:[PointXY]())

Parameters

|           |             |   |
| --------- | ----------- | - |
| canvasLoc | [PointXY]() |   |

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

#### zoomToSelection[​](#zoomtoselection "Direct link to zoomToSelection")

Zooms the display so that the current selected nodes are all visible, optionally animating the transition.

Signature

zoomToSelection(params:{

<br />

  doNotAnimate:boolean,

<br />

  doNotZoomIfVisible:boolean,

<br />

  fill:number,

<br />

  filter:(o:[Base]()) => boolean | [ObjectData](),

<br />

  selection:[VisuallyJsSelection]()

<br />

})

Parameters

|        |                                                                                                                                                                                                |                        |
| ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| params | {<br />  doNotAnimate:boolean,<br />  doNotZoomIfVisible:boolean,<br />  fill:number,<br />  filter:(o:[Base]()) => boolean \| [ObjectData](),<br />  selection:[VisuallyJsSelection]()<br />} | Optional method params |

Return value

void
