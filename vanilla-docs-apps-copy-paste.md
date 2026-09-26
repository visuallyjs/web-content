# Copy/paste

VisuallyJs offers an easy to use API for copy/paste - the `Surface` and `Paper` components expose a `clipboard` member, which offers a number of different methods. All paste operations are executed within a transaction and can be rolled-back/re-run as an atomic unit.

## Copying objects[​](#copying-objects "Direct link to Copying objects")

Call the `copy` method to add items to the clipboard. The signature of the `copy` method is:

#### copy[​](#copy "Direct link to copy")

Copy some set of objects into the clipboard.

Signature

copy(obj:[Base]() | [VisuallyJsSelection]() | Array<[Base]()> | [Path]())

Parameters

|     |                                                                    |                                                      |
| --- | ------------------------------------------------------------------ | ---------------------------------------------------- |
| obj | [Base]() \| [VisuallyJsSelection]() \| Array<[Base]()> \| [Path]() | The object, or objects, to copy in to the clipboard. |

Return value

void

You can pass a variety of different types in to this method - any node, group or edge, or an array of these, or a [Selection](/vanilla/docs/apps/model/selections.md) or [Path](/vanilla/docs/apps/model/paths.md).

In this first example, our canvas initially has two nodes. The `addItemsToSelection` function connects these two nodes with a programmatic call to `addEdge`, and it then copies both nodes and the new edge into the clipboard. The `pasteItems` method pastes the contents of the clipboard, to canvas origin `{50, 250}` (paste origin is discussed below).

<!-- -->

When you paste the contents of this clipboard, a copy of `source` will be created, a copy of `target` will be created, and a copy of `edge` - whose source and target are the new vertices - will also be created.

Copy itemsPaste items

<br />

Note that the pasted items are always pasted to the same place in this example - because we use `{origin:{x:50, y:250}}` in our paste command. The section below on paste options discusses the paste origin and what options are available to you.

<br />

***

## Pasting clipboard contents[​](#pasting-clipboard-contents "Direct link to Pasting clipboard contents")

Use the `paste` method to paste the current contents of the clipboard.

#### paste[​](#paste "Direct link to paste")

Paste the clipboard's most recent entry, optionally removing it from the clipboard afterwards.

Signature

paste(options:[BrowserUIPasteOptions]())

Parameters

|         |                           |                        |
| ------- | ------------------------- | ---------------------- |
| options | [BrowserUIPasteOptions]() | Options for the paste. |

Return value

[ClonedSet]()

info

### Paste origin[​](#paste-origin "Direct link to Paste origin")

A set of vertices has an implicit origin, which is computed as the `x` position of the leftmost vertex, and the `y` position of the topmost vertex. When you call paste without providing an `origin`, the new objects are placed on top of the existing object. When you call `paste` and provide an `origin` - as we did in the example above - the location of each vertex to be pasted is translated by the delta between the paste origin and the computed origin of the clipboard:

```text
surface.clipboard.paste({origin:{x:50, y:250}})

```

### Event as origin[​](#event-as-origin "Direct link to Event as origin")

In real world use cases it is the user who generally decides where to paste content. The clipboard allows you to use a `MouseEvent` as the origin instead of specifying it yourself. At any point, the canvas for a given Surface has been panned in one or both axes, and is likely zoomed in or out to some value other than 1:1. When you provide a `MouseEvent` as the origin for a paste, the location of this event is automatically mapped to a location onto the Surface. In this next example, first press `Copy Items` to populate the clipboard. Then you can click anywhere on the canvas to paste the copied content:

**********

Copy items

<br />

The code for this is as shown here - note our `EVENT_CANVAS_CLICK` listener in the render options. We pass the event from that method into the paste method.

<!-- -->

### Vertices not in clipboard[​](#vertices-not-in-clipboard "Direct link to Vertices not in clipboard")

In this snippet we create two nodes and an edge, and then we copy one of the nodes and the edge into the clipboard:

```javascript

// ... import and create a clipboard

const source = model.addNode({id:"source"})
const target = model.addNode({id:"target"})
const edge = model.addEdge({source, target})

surface.clipboard.copy([source, edge])       // copy source node only and the edge


```

What happens now if we paste this?

```javascript
clipboard.paste({event:someMouseEvent})

```

By default, the clipboard will create a copy of `source`, and a copy of `edge`. The cloned source will be the source for the cloned edge, but the target for the cloned edge will be the *original target* vertex. You can see that in this example:

**********

Copy items

<br />

This behaviour can be modified via the use of the `hermetic` flag.

```javascript
clipboard.paste({event:someMouseEvent, hermetic:true})

```

In this call, `hermetic:true` instructs the clipboard to only paste edges for which both the source and target vertices were also in the clipboard. So in this case, only a clone of the `source` vertex will be pasted, and the edge will **not** be pasted. `hermetic` defaults to `false`.

### Edge geometry[​](#edge-geometry "Direct link to Edge geometry")

An edge that has "geometry" attached to it is an edge that has either been loaded with a `geometry` section in the JSON, or has been edited by a connector editor, using the mouse, or fingers. When you copy an edge with geometry and subsequently paste it, the rules for the associated geometry are:

* if you copy and paste the edge and both its source and target vertices, the pasted edge has geometry attached, the value for which is the original edge's geometry translated according to the transformation of the origin as discussed above.

* if you copy and paste an edge but not both its source and target vertices, the pasted edge does *not* have geometry attached, and will be painted according to VisuallyJs's default algorithm for the specific connector.

### Nested groups and nodes[​](#nested-groups-and-nodes "Direct link to Nested groups and nodes")

If you copy and paste a group that has child nodes or groups, the child nodes or groups will also be copied, and pasted as children of the pasted group. This mechanism works to an arbitrary level of nesting. If you wish to copy a group without any of its child content, you can specify a "shallow" paste, by setting `shallow:true` on the paste call:

```typescript
clipboard.paste({event, shallow:true}) 

```

In this canvas we have copied the main group into the clipboard on load. When you left-click on the canvas, the group is pasted with all of its descendants at the point you clicked. When you right-click, the group is "shallow" pasted - only the group itself, not any of its descendants.

**********

<br />

This is the code we used:

<!-- -->

## Pasting the current selection[​](#pasting-the-current-selection "Direct link to Pasting the current selection")

As discussed in the [Selection docs](/vanilla/docs/apps/model/selections.md), each VisuallyJs model maintains a list of currently selected objects, and various parts of the UI add/remove objects to/from the current selection. You can paste the current selection for some model via the `pasteCurrentSelection` method:

#### pasteCurrentSelection[​](#pastecurrentselection "Direct link to pasteCurrentSelection")

Copies and pastes the contents of the associated model instance's current selection into the clipboard. This method is equivalent to calling `copyCurrentSelection()` first and then calling `paste(..)`.

Signature

pasteCurrentSelection(options:[PasteOptions]())

Parameters

|         |                  |                        |
| ------- | ---------------- | ---------------------- |
| options | [PasteOptions]() | Options for the paste. |

Return value

[ClonedSet]()

```javascript
import { newInstance, EVENT_TAP, EVENT_CANVAS_CLICK } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  events: {
    [EVENT_CANVAS_CLICK]: (ui, event) => ui.clipboard.pasteCurrentSelection({event})
  },
  view: {
    nodes: {
      default: {
        events: {
          [EVENT_TAP]: (p) => p.model.toggleSelection(p.obj)
        }
      }
    }
  }
})

```

In this canvas, when you tap a vertex it will be added to the model's current selection. Subsequently clicking on the canvas will paste a copy of the vertices in the current selection at the location you clicked. To clear the selection, use the `Clear selection` button in the controls.

**********

<br />

## Clearing the clipboard[​](#clearing-the-clipboard "Direct link to Clearing the clipboard")

The clipboard offers a `clear` method that will remove all copied content:

```text
clipboard.clear()

```

You can also instruct the clipboard to clear the content that was just pasted:

```javascript
clipboard.paste({origin:{x:50, y:50}, clear:true})

```
