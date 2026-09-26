# Edge Routing

The [Hierarchy Layout](/vanilla/docs/apps/layouts/Hierarchy) has the ability to generate routing information for edges. This routing information generates paths in such a way that each edge avoids any nodes in the UI.

The edge routing plugin operates in one of two modes - either 'direct' or 'orthogonal'. Additionally, in orthogonal mode, you can switch on [bus routing](#bus-routing)

## Setup[​](#setup "Direct link to Setup")

You add this plugin as you would any other - but you must also be using a `Hierarchy` layout, so we've included that here:

```javascript
import { newInstance, EdgeRoutingPlugin } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  layout: {
    type: HierarchyLayout.type,
    options: {
      generateRouting: true
    }
  },
  plugins: [
    {
      type: EdgeRoutingPlugin.type
    }
  ]
})

```

***

## Direct routing[​](#direct-routing "Direct link to Direct routing")

This is the default you'll get when you configure an edge routing plugin on your UI, as shown in the code above:

**********

tip

This concept is related to [vertex avoidance](/vanilla/docs/apps/edges/vertex-avoidance.md), but in this plugin the routing data is calculated statically at layout time, and not recomputed until the layout is re-run. We're looking at ways to fold these two related approaches into a single configuration.

## Orthogonal routing[​](#orthogonal-routing "Direct link to Orthogonal routing")

Orthogonal routing uses horizontal and vertical line segments and ensures that lines do not overlap.

```javascript
import { newInstance, EdgeRoutingPlugin } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  layout: {
    type: HierarchyLayout.type,
    options: {
      generateRouting: true
    }
  },
  plugins: [
    {
      type: EdgeRoutingPlugin.type,
      options: {
        mode: "orthogonal"
      }
    }
  ]
})

```

**********

### Bus routing[​](#bus-routing "Direct link to Bus routing")

Bus routing is orthogonal routing where instead of assigning a separate slot for each edge, edges travelling along the same path are grouped as a bus.

```javascript
import { newInstance, EdgeRoutingPlugin, OrthogonalRouterModes } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  layout: {
    type: HierarchyLayout.type,
    options: {
      generateRouting: true
    }
  },
  plugins: [
    {
      type: EdgeRoutingPlugin.type,
      options: {
        mode: "orthogonal",
        orthogonalMode: OrthogonalRouterModes.bus
      }
    }
  ]
})

```

**********

***

## Options[​](#options "Direct link to Options")

EdgeRoutingPluginOptions

Options for the edge routing plugin.

| Name               | Type                      | Description                                                                                                                                                                                                                             |
| ------------------ | ------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| mode               | [EdgeRoutingPluginMode]() | Mode to use to draw edges. 'orthogonal' is like the orthogonal connector - segments that are either vertical or horizontal.<br />`direct` draws straight lines through regions. Both modes assign a separate anchor point to each edge. |
| orthogonalMode?    | [OrthogonalRouterMode]()  | When mode is 'orthogonal' this instructs VisuallyJs whether to group edges in buses, or to route each edge separately.                                                                                                                  |
| orthogonalPadding? | number                    | How much space to leave between stacked orthogonal edges. Defaults to 10 pixels.                                                                                                                                                        |
