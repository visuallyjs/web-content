# Groups

Groups act as a container for zero or more nodes or other groups. In the UI, these can be collapsed, and edges to/from the nodes/groups inside the group are then temporarily relocated to the group container. There is no limit imposed on how deeply groups may be nested.

Groups have in common with nodes, edges and ports the two concepts of `id` and of `type`, and as with the other graph objects, `type` will be set to `"default"` if it cannot be determined. Group IDs and types either follow the default rules (ie. they are given by the `id` and `type` parameters, respectively, in the group's data), or they are derived by applying the current `idFunction` and `typeFunction`.

Groups, as with the other graph objects, can have arbitrary JSON data associated with them.

## Rendering[​](#rendering "Direct link to Rendering")

As shown in the various examples at the start of this page, groups are rendered using client side templates just as nodes are. They are declared inside a view alongside nodes, edges and ports, and broadly follow the same syntax as node definitions - but there are a number of extra flags that can be set on a group definition.

A simple example to start:

```javascript
viewOptions = {
    groups:{
        groupType1:{
            template:`<div class="my-group"><h1>This is a group</h1></div>`,
            constrain:true
        }
    }
}

```

Here we declare that member of groups of type `groupType1` are constrained to the group element (that is, they cannot be dragged outside of the group's bounds).

## Collapse/Expand[​](#collapseexpand "Direct link to Collapse/Expand")

You can collapse/expand a group using the `collapseGroup` and `expandGroup` methods on the `Surface` widget. When you collapse a group, any edges from any of the member nodes/groups in the group to nodes/groups outside of the group are relocated to the group's container, and a CSS class is applied to the group's container, indicating the collapsed state. When you subsequently expand the group, the edges are placed back onto their appropriate nodes/groups.

It is important to note that when a group is collapsed, VisuallyJs does not hide the member nodes/groups automatically for you. But a CSS class of `vjs-group-collapsed` is added to the group's container, for you to handle this in your CSS.

The anchor to be used in the collapsed state can be specified in the group definition in the `viewOptions`:

```javascript
import { AnchorLocations } from "@visuallyjs/browser-ui"

const view = {
    groups:{
        groupType1:{
            template:`<div class="my-group"><h1>This is a group</h1></div>`,
            anchor:AnchorLocations.Continuous
        }
    }
}

```

Any valid anchor can be used here.

### Collapsed Group Size[​](#collapsed-group-size "Direct link to Collapsed Group Size")

When you're using the model for your vertex sizes (ie. you're not relying on CSS to establish sizes), and a group is collapsed, the UI resolves the size to render it at by working through a chain of four sources, from highest to lowest priority.

***

#### 1. `getGroupCollapsedSize` (constructor option)[​](#1-getgroupcollapsedsize-constructor-option "Direct link to 1-getgroupcollapsedsize-constructor-option")

An optional function `(group: Group, currentSize: Size) => Size` passed when constructing the surface or UI instance. It is called first on every collapse. If it returns a non-null value, that value is used and the chain stops.

Return `null` or `undefined` to fall through to the next source. This is the right place for size logic that depends on runtime state or per-instance group data.

***

#### 2. `collapsedSize` on `GroupMapping`[​](#2-collapsedsize-on-groupmapping "Direct link to 2-collapsedsize-on-groupmapping")

A static `Size` value declared in the view definition for a group type. Used when `getGroupCollapsedSize` was not supplied or returned null. Applies uniformly to every group of that type.

***

#### 3. `collapsedSize` on `ShapeType`[​](#3-collapsedsize-on-shapetype "Direct link to 3-collapsedsize-on-shapetype")

A static `Size` value on a shape library shape definition. Only consulted when the shape's `objectType` is `Group`. Useful in shape-library-driven UIs where group appearance is controlled through the shape library rather than the view.

***

#### 4. `defaultCollapsedGroupSize` (constructor option)[​](#4-defaultcollapsedgroupsize-constructor-option "Direct link to 4-defaultcollapsedgroupsize-constructor-option")

A `Size` value passed when constructing the surface or UI instance. Acts as a global fallback for all groups when none of the above sources produce a value. If omitted, the built-in default of `{ width: 200, height: 150 }` is used.

***

### Magnetizing when collapsed/expanded[​](#magnetizing-when-collapsedexpanded "Direct link to Magnetizing when collapsed/expanded")

By default, the surface widget will run the [Magnetizer](/vanilla/docs/apps/magnetizer.md) whenever a group is collapsed or expanded: when a group is expanded, surrounding elements are adjusted so as to ensure the group does not intersect with any other element. When a group is collapsed, the rest of the elements in the view are gathered in towards the collapsed group. This behaviour can be switched off - see the `afterGroupChange` flag in the [Surface widget magnetizer options](/vanilla/docs/apps/magnetizer.md#surface-widget)

## Templating[​](#templating "Direct link to Templating")

### Specifying the canvas[​](#specifying-the-canvas "Direct link to Specifying the canvas")

It is not necessarily the case that you wish to use your entire group template as the parent of the group's members. You can set a `data-vjs-group-content` attribute on the element that you wish to have acting as the parent for the members (you might have noticed this in the examples above):

```html
<div class="aGroup">
  <h1>A Group</h1>
  <div data-vjs-group-content="true" class="aGroupInner">
    <!-- Child elements go here -->
  </div>
</div>

```

Whenever a group is resized by the [auto sizing code](#autosizing-groups) in the surface, the surface looks for an element in the group with this attribute, and if found, this is the element to which the surface applies the change of size. Otherwise the size is applied to the group's main element. Keep this in mind from a CSS perspective: your CSS should allow the size of the content area to mandate the size of its parent. Scroll/auto overflow is not supported inside a group element.

## Autosizing Groups[​](#autosizing-groups "Direct link to Autosizing Groups")

Groups can be configured to automatically resize themselves to encompass the extents of their child nodes/groups, via the `autoSize` flag on a group definition in a view:

```javascript
{
  groups:{
    "groupType1":{
      ...
      autoSize:true
      ...
    },
    "groupType2":{
      ...
      autoSize:true,
      maxSize:{width:600, height:600}
      ...
    }
  }
}

```

In this example, both group types are declared to auto size, but `groupType2` will grow to a maximum of 600 pixels in each axis.

Autosizing is run after a data load or when data exists in a model instance and it is rendered to some surface.

### On-demand autosizing[​](#on-demand-autosizing "Direct link to On-demand autosizing")

You can run auto sizing on demand on a list of groups, or on all groups, with the `autoSizeGroups` method of the UI:

autoSizeGroups(groups:Array<[Group]()>, force:boolean)

[show definition]()

or on a single group:

autoSizeGroup(group:[Group](), force:boolean)

[show definition]()

## Layouts[​](#layouts "Direct link to Layouts")

By default, every group has an `Absolute` layout assigned to it. If your node data has `left`/`top` properties in it, these values will automatically be used to place nodes/groups inside of their parent groups.

### Specifying in the view[​](#specifying-in-the-view "Direct link to Specifying in the view")

To specify the layout for a specific type of group, set it in that group's entry in your view:

```javascript
 {
    ...
    groups:{
      "someGroupType":{
        ...
        layout:{
            type:HierarchyLayout.type, 
            options:{
                orientation:"vertical"
            }
        }
      }
    }
 
    ...
 }

```

The format of the `layout` parameter is identical to the `layout` parameter in the root of the `view`.

### Layout on demand[​](#layout-on-demand "Direct link to Layout on demand")

You can force a layout in a group with the `relayoutGroup` method:

relayoutGroup(groupOrId:string | [Group](), reason:GroupRelayoutReason)

[show definition]()

This will cause a layout to be run immediately on the given group (which may be passed in as the group object, or just its id)

### Ad-hoc group layout[​](#ad-hoc-group-layout "Direct link to Ad-hoc group layout")

You can run an ad-hoc layout on a group at any time:

adHocGroupLayout(group:string | [Group](), layoutParams:{

<br />

  options:[LayoutParameters](),

<br />

  type:string

<br />

})

[show definition]()

This will cause the group's layout to be temporarily swapped out with a layout conforming to the spec you provide in `layoutParams`, the ad-hoc layout will then be run, and the original group layout reinstated (but without running the original layout again of course!)

#### Relationship to group size[​](#relationship-to-group-size "Direct link to Relationship to group size")

By default, a layout in a group will cause the auto size routine to be run for the group immediately afterwards.

***

## Elastic groups[​](#elastic-groups "Direct link to Elastic groups")

Elastic groups allow your users to dynamically resize a group by dragging its child elements around inside of it. To setup a group as elastic:

```javascript
{
    groups:{
        default:{
            elastic:true,
            minSize:{ width:250, height:250 }    // optional, but it does tend to help aesthetically to have a minSize.
        }
    }
}

```

### Dragging elements out of an elastic group[​](#dragging-elements-out-of-an-elastic-group "Direct link to Dragging elements out of an elastic group")

To drag a child node out of an elastic group, hold down the Shift key prior to the drag (and hold it for the duration of the drag):

**********

Suppressing resize

Ordinarily, dragging a child vertex of an elastic group will cause the group to resize to fit its content. Holding the `shift` key can also be used to switch off elastic resize while an element is being dragged.

### Resizing an elastic group from left/top[​](#resizing-an-elastic-group-from-lefttop "Direct link to Resizing an elastic group from left/top")

By default an elastic group (in fact *any* group) will not resize from the left and/or top edge. We call this "shrink from origin", and you can switch it on via a flag on a group definition:

```javascript
 {
     groups:{
         default:{
             elastic:true,
             allowShrinkFromOrigin:true,
             minSize:{ width:250, height:250 }    // optional, but it does tend to help aesthetically to have a minSize.
         }
     }
 }

```

or on an ad-hoc basis by holding down the meta key (command on Macs) prior to the drag.

### Nested elastic groups[​](#nested-elastic-groups "Direct link to Nested elastic groups")

Elastic groups which are themselves children of another elastic group will relay size changes during dragging to their parent, so that the user can see what changes will be made to all the groups.

***

## View options[​](#view-options "Direct link to View options")

The full list of options that are available on a group mapping is:

GroupMapping

The mapping for the definition of a group inside a view.

| Name                  | Type                                                                                          | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| --------------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| allowLoopback?        | boolean                                                                                       | Whether or not to allow edges from this vertex back to itself. Defaults to true. This flag will not prevent an edge from a port back to the node/group to which it belongs - for that, see `allowVertexLoopback`.                                                                                                                                                                                                                                                                                                                             |
| allowVertexLoopback?  | boolean                                                                                       | Whether or not to allow edges from a port back to the vertex it belongs to. Defaults to true.                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| anchor?               | [AnchorSpec]()                                                                                | Spec for the anchor to use for connections to children of the group when they are transferred to the group in its collapsed state.                                                                                                                                                                                                                                                                                                                                                                                                            |
| anchorPositionFinder? | [AnchorPositionFinder\<any>]()                                                                | Optional function to call on connection drop, to determine the location for the target anchor for the new connection. Returning null from this indicates no preference, and VisuallyJs will use its own computed value.                                                                                                                                                                                                                                                                                                                       |
| anchorPositions?      | Array<[ObjectAnchorSpec]()>                                                                   | Optional array of anchor positions to use.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| autoGrow?             | boolean                                                                                       | Defaults to false, meaning that the group will not be resized if an item addition/removal or drag causes the bounds of the child members to change and the new size is greater than the previous size.                                                                                                                                                                                                                                                                                                                                        |
| autoShrink?           | boolean                                                                                       | False by default. If true indicates that if a child member is dragged/added/removed and the group's size is recalculated to be smaller than the previous size, the new size should be applied. This also works if the group needs to shrink from its left and/or top edge. If you don't want that behaviour, set `allowShrinkFromOrigin` to false.                                                                                                                                                                                            |
| autoSize?             | boolean                                                                                       | False by default. This flag switches on both `autoShrink` and `autoGrow` and also enables support for shrinking a group from its left or top edge                                                                                                                                                                                                                                                                                                                                                                                             |
| canDrop?              | (v:[Node]() \| [Group]()) => boolean                                                          | Optional interceptor that will be invoked to test whether a given node/group may be dropped onto this group.                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| collapsedSize?        | [Size]()                                                                                      | The size to use for this group type when it is collapsed.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| constrain?            | boolean                                                                                       | False by default - nodes/groups may be dragged outside of the bounds of the group.                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| defaultSize?          | [Size]()                                                                                      | Optional default size to use for the vertex. This is not used to set the size in the DOM for a vertex - it is used to insert `width` and `height` values into the backing data for any vertex of this type that does not have them set.                                                                                                                                                                                                                                                                                                       |
| edgeType?             | string                                                                                        | Type to assign to edges connected to this vertex as a source.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| elastic?              | boolean                                                                                       | Similar to autoGrow, but the UI shows a visual prompt when a group will be resized as a result of dragging a child.                                                                                                                                                                                                                                                                                                                                                                                                                           |
| elementsDraggable?    | boolean                                                                                       | True by default - indicates that child members may be dragged around inside the group.                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| events?               | [GroupEventOptions\<EL>]()                                                                    | Optional map of event bindings.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| fitToGrid?            | boolean                                                                                       | When sizing the group, ensure it fits the underlying grid, if there is one.                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ignore?               | boolean                                                                                       | If true, vertices of this type will be ignored by this UI and not rendered.                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| layout?               | {<br />  options:[LayoutParameters](),<br />  type:string<br />}                              | Options for the group's layout.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| locked?               | boolean                                                                                       | Whether or not the group is locked.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| maxConnections?       | number                                                                                        | Maximum number of connections this vertex supports. Default is 1. A value of -1 means no limit.                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| maxSize?              | [Size]()                                                                                      | Maximum size the group can grow to. If not specified the group can grow to an arbitrary size. Note that this behaviour can also be enforced via CSS.                                                                                                                                                                                                                                                                                                                                                                                          |
| mergeStrategy?        | string                                                                                        | When merging a type description into its parent(s), values in the child for `connector`, `anchor` and `anchors` will always overwrite any such values in the parent. But other values, such as `overlays`, will be merged with their parent's entry for that key. You can force a child's type to override *every* corresponding value in its parent by setting `mergeStrategy:'override'`.                                                                                                                                                   |
| minSize?              | [Size]()                                                                                      | Minimum size the group can be.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| padding?              | number                                                                                        | Optional padding to set inside a group when computing an auto size.                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| parameters?           | Record\<string,any>                                                                           | A map of parameters that the template engine will merge with the backing data when rendering the vertex.                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| parent?               | string \| Array\<string>                                                                      | Optional ID of one or more edge definitions to include in this definition. The child definition is merged on top of the parent definition(s). Circular references are not allowed and will throw an error.                                                                                                                                                                                                                                                                                                                                    |
| template?             | string                                                                                        | Template to use for a vertex of this type. This is only for 'vanilla' VisuallyJs: if you are using an integration such as React/Angular/Vue/Svelte, you will not need to provide this. If you provide this and also `templateId`, this will take precedence.                                                                                                                                                                                                                                                                                  |
| templateId?           | string                                                                                        | ID of the template to use for a vertex of this type. This is only for 'vanilla' VisuallyJs: if you are using an integration such as React/Angular/Vue, you will not need to provide this. This parameter is distinct from `template` in that when you provide `templateId` you are expecting VisuallyJs to resolve the template for you, either from a `templates` block in a `render` call, or by looking for a script element in the DOM with the appropriate ID. If you provide this and also `template`, `template` will take precedence. |
| templateIdResolver?   | (data:[ObjectData](), ui:UICore\<EL>, model:[VisuallyJsModel](), object:[Vertex]()) => string | A function that can resolve the ID of the template to use for the given vertex. This is an advanced configuration that is not often needed, and is only for 'vanilla' VisuallyJs. This function will take precedence over both `template` and `templateId`.                                                                                                                                                                                                                                                                                   |
