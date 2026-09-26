# Removing edges

There are a few ways to remove edges in VisuallyJs. On this page we'll discuss edge deletion in the UI, but it's also possible to remove an edge programmatically from a diagram.

## Removing via drag/drop[​](#removing-via-dragdrop "Direct link to Removing via drag/drop")

You can grab an edge near one of its anchors and then drag it off the vertex. In the canvas below we have applied a CSS class to make these zones visible on hover; by default this does not occur (the CSS classes we target are `.vjs-connector-source-drag` and `.vjs-connector-target-drag`).

By default, a diagram is configured to allow "unattached" edges, so the default behaviour when you drag an edge and drop it in whitespace is to just leave it there, unattached. You need to specify `allowUnattached` if you do not want this:

<!-- -->

**********

## Rettaching[​](#rettaching "Direct link to Rettaching")

VisuallyJs's default behaviour is to discard any edges that a user has dropped in whitespace. You can override this via a setting:

<!-- -->

In this canvas if you drag one end of the edge and drop it in whitespace VisuallyJs will reattach it:

**********

## Disabling detach[​](#disabling-detach "Direct link to Disabling detach")

You can disable detach via mouse/touch events with the `detachable` setting in the `edges` options:

<!-- -->

In this canvas VisuallyJs will not allow you to detach the edge using the mouse/touch events:

**********

How, then, could your users delete an edge via the UI? One solution is to specify a **deleteButton**.

## Showing a delete button[​](#showing-a-delete-button "Direct link to Showing a delete button")

<!-- -->

**********

The delete button will be assigned a CSS class of `.vjs-edge-delete`.

### Custom CSS class[​](#custom-css-class "Direct link to Custom CSS class")

You can provide one or more extra classes to set on the delete button via the `deleteButtonClass` property:

<!-- -->

### Showing on hover only[​](#showing-on-hover-only "Direct link to Showing on hover only")

`deleteButton` can be specified either as a boolean, or as a constant that specifies its `visibility`. To have a delete button that only appears on hover, for example:

<!-- -->

**********

### Managing edge removal[​](#managing-edge-removal "Direct link to Managing edge removal")

You may want to manage the removal of some specific edge - perhaps some condition is met in your app that means the edge cannot be removed, or perhaps you want to hit the server to confirm edge deletion first, etc. For that you can use the `deleteConfirm` property:

<!-- -->

**********

The argument for `deleteConfirm` should be a function of this type:

EdgeDeleteConfirmationFunction

Definition of the function you can provide as `deleteConfirm` on an edge definition. VisuallyJs gives you the edge to be possibly deleted and the pointer event that instigated the deletion. If you wish to delete the edge you must invoke the `proceed()` function.

`(params:{
  e:Event,
  edge:Edge
}, proceed:() => any) => any`

You are given the edge that is a candidate for deletion, and the event that initiated the deletion. If you wish to confirm the edge removal, you must invoke the `proceed` method.
