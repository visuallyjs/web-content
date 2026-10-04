# Changelog

## 1.2.9[​](#129 "Direct link to 1.2.9")

4th October 2026

### General[​](#general "Direct link to General")

* Refactored bulk loader code to implement a 4x performance improvement
* Updated packages to remove the `publishConfig` section of the package.json. This improves the portability of the built artifacts, allowing them to be uploaded to private NPM repositories without retaining the reference to the VisuallyJs repository URL.
* Added support for `minZoom` and `maxZoom` options on overlays: overlays can now be hidden/shown based upon the zoom level of the UI.

## 1.2.8[​](#128 "Direct link to 1.2.8")

26th September 2026

### General[​](#general-1 "Direct link to General")

* Added a new `GraphPropagationEngine` class, plus associated `GraphPropagationEnginePlugin`. This offers a way to propagate properties from one vertex to another, based on a set of rules.
* Added support for `readOnly` on a `ShapePropertyDefinition` - inspectors will show you the value but not allow you to edit it.
* Fixed an issue in `ShapePropertiesInspector` components where radio buttons for a given value were not all assigned the same name
* Updated our private NPM repository to respond to the NPM `/whoami` endpoint. This facilitates usage of our NPM repository as a remote repository in apps such as JFrog.
* Updated our Logic Gates starter apps to include the graph propagation engine.
* Added support for `graphPropagation` to `DiagramOptions`
* Added support for `cells.templateEvents` in `DiagramOptions`, allowing delegated event handlers to be attached to elements inside rendered shape templates and receive the associated `DiagramCell`.

### Angular[​](#angular "Direct link to Angular")

* Fixed an issue in `ShapePropertiesInspector` components where radio buttons for a given value were not all assigned the same name

### React[​](#react "Direct link to React")

* Fixed an issue in `ShapePropertiesInspector` components where radio buttons for a given value were not all assigned the same name

### Vue[​](#vue "Direct link to Vue")

* Fixed an issue in `ShapePropertiesInspector` components where radio buttons for a given value were not all assigned the same name

### Svelte[​](#svelte "Direct link to Svelte")

* Fixed an issue in `ShapePropertiesInspector` components where radio buttons for a given value were not all assigned the same name

## 1.2.7[​](#127 "Direct link to 1.2.7")

21st September 2026

### General[​](#general-2 "Direct link to General")

* Added new Scada/HMI starter app to all libraries. This app provides a solid foundation on which you can build your own Scada/HMI apps, with a look and feel that is aligned with the HMI ISA-101 Standard.

* Update bubble/scatter chart custom marker code to not require namespaced elements in the SVG snippets returned from a `resolveMarker` call

* Added `name` to `PropertyMappings`. This is an optional human readable name that is used by inspectors.

* Updated overlay definition code to handle the case that an overlay/marker is specified as an object with "type" but no "options"

* Improved CSS/rendering for the edge type picker

* Added support for boolean false for 'rotatable' property of `Label`/`Custom` overlay: with this set, the label never rotates to make the text upright.

* Added new CSS vars to resize tools/diagram tools plugins:

  <!-- -->

  * `--vjs-resize-handle-fill-color` For the fill of the resize handles, defaults to #FFFFFF
  * `--vjs-resize-frame-line-width` For the stroke width of the resize frame, defaults to 2px

### React[​](#react-1 "Direct link to React")

* Made the `options` prop of all charts reactive, so that the chart re-initializes if it changes
* Added `EdgePropertyMappingsInspector` component - an inspector that automatically renders a form for managing the properties of an edge from the installed edge property mappings.
* Added `ShapePropertiesInspector` component - an inspector that automatically renders a form for managing the properties of some shape defined in a shape set

### Angular[​](#angular-1 "Direct link to Angular")

* Made the `data`, `url` and `options` inputs reactive on all charts
* Added `EdgePropertyMappingsInspector` component - an inspector that automatically renders a form for managing the properties of an edge from the installed edge property mappings.
* Added `ShapePropertiesInspector` component - an inspector that automatically renders a form for managing the properties of some shape defined in a shape set

### Svelte[​](#svelte-1 "Direct link to Svelte")

* Made the `data`, `url` and `options` props reactive on all charts
* Added `EdgePropertyMappingsInspector` component - an inspector that automatically renders a form for managing the properties of an edge from the installed edge property mappings.
* Added `ShapePropertiesInspector` component - an inspector that automatically renders a form for managing the properties of some shape defined in a shape set
*

### Vue[​](#vue-1 "Direct link to Vue")

* Made the `data`, `url` and `options` props reactive on all charts
* Added `EdgePropertyMappingsInspector` component - an inspector that automatically renders a form for managing the properties of an edge from the installed edge property mappings.
* Added `ShapePropertiesInspector` component - an inspector that automatically renders a form for managing the properties of some shape defined in a shape set

## 1.2.6[​](#126 "Direct link to 1.2.6")

10th September 2026

### General[​](#general-3 "Direct link to General")

* Improved label placement for SVG shapes when label position is "top" or "bottom"
* Added support for SVG shape label background.

### Svelte[​](#svelte-2 "Direct link to Svelte")

* Fixed issue in the ShapePaletteComponent with auto edge options

## 1.2.5[​](#125 "Direct link to 1.2.5")

7th September 2026

### General[​](#general-4 "Direct link to General")

* Added support for rotating elements that are being dragged from a palette by tapping/holding a specific key
* Added the concept of "auto edge connect": elements that are being dragged from the palette can be automatically connected to existing vertices by dragging them over connection points.
* The `ShapePalette` and `DiagramPalette` classes now support `allowDropOnEdge` - you can drag a shape onto an edge and drop it, and the edge will be automatically split.
* Fixed painting issue with lasso in SVG containers
* Fixed issue with incorrect location of port elements on a rotated node in an SVG container
* Aesthetic improvements to the lasso in both apps and diagrams, including exposing several new CSS vars for theming.
* Added support for `data-vjs-anchor`, `data-vjs-source-anchor` and `data-vjs-target-anchor` to edge drag/click to add functionality.

### Starter Apps[​](#starter-apps "Direct link to Starter Apps")

* New starter app `Fault Tree Analysis` added. This is a dashboard containing a Fault Tree Analysis chart, with a Cut Sets view and a Risk Contribution view
* New starter app `Logic Gates` added
* New starter app `Circuit Diagram` added

### Vue[​](#vue-2 "Direct link to Vue")

* Made the `data` and `url` props of the `SurfaceComponent` and `PaperComponent` reactive, making these components easier to work with inside a Vue app.
* Added support for rotating elements that are being dragged from a palette by tapping a specific key
* Added auto edge connect support to `PaletteComponent`, `DiagramPaletteComponent` and `ShapePaletteComponent`

### Svelte[​](#svelte-3 "Direct link to Svelte")

* Made the `data` and `url` props of the `SurfaceComponent` and `PaperComponent` reactive, making these components easier to work with inside a Svelte app.
* Added support for rotating elements that are being dragged from a palette by tapping a specific key
* Added auto edge connect support to `PaletteComponent`, `DiagramPaletteComponent` and `ShapePaletteComponent`

### React[​](#react-2 "Direct link to React")

* Added support for rotating elements that are being dragged from a palette by tapping a specific key
* Added auto edge connect support to `PaletteComponent`, `DiagramPaletteComponent` and `ShapePaletteComponent`

### Angular[​](#angular-2 "Direct link to Angular")

* Added support for rotating elements that are being dragged from a palette by tapping a specific key
* Added auto edge connect support to `PaletteComponent`, `DiagramPaletteComponent` and `ShapePaletteComponent`

### Breaking[​](#breaking "Direct link to Breaking")

* The new `updateTypeOnPaletteTap` option for shape palettes and diagram palettes technically constitutes a breaking change, as this flag switches on behaviour that was previously on by default: when something is selected in the canvas and you click a shape in the palette, the selected vertices' type is changed to match the clicked shape.

## 1.2.4[​](#124 "Direct link to 1.2.4")

18th August 2026

### General[​](#general-5 "Direct link to General")

* Added new `Bowtie` layout - a two sided hierarchy, such as you might use in a Mindmap.
* Added support for `autoArm` and `armTimeout` to the lasso plugin - the plugin switches on after a long press on the canvas, without the user needing to switch the surface to select mode.
* An update was made to `PaperComponent` to fix an alignment issue.

### Starter Apps[​](#starter-apps-1 "Direct link to Starter Apps")

* Our Mindmap starter apps were updated to use the new `Bowtie` layout instead of the custom layout they were previously using.
* Ported JsPlumb's "neighbourhood views" starter app to VisuallyJs - an app that shows how you provide several different views of the same dataset on a single page

### Vue[​](#vue-3 "Direct link to Vue")

* The renderer was updated to ensure that the `vertex` passed to Surface/Paper vertex components is marked raw, and not converted to a Proxy by Vue.
* Added support for optional `dataType` prop on the Surface/Paper components

### React[​](#react-3 "Direct link to React")

* Added support for optional `dataType` prop on the Surface/Paper components

### Svelte[​](#svelte-4 "Direct link to Svelte")

* Added support for optional `dataType` prop on the Surface/Paper components

### Angular[​](#angular-3 "Direct link to Angular")

* Added support for optional `dataType` prop on the Surface/Paper components

## 1.2.3[​](#123 "Direct link to 1.2.3")

7th August 2026

### General[​](#general-6 "Direct link to General")

* A new "line crossings" plugin was added. This plugin works alongside the `Orthogonal` connector (or a Straight connector with orthogonal constraint applied) to draw markers where two edges intersect. Markers may be a bridge, a gap or a dot, and may be placed on either the horizontal or vertical segment at an intersection.
* Connector and anchor computation was updated to snap values to a half pixel increment. This helps avoid painting issues related to antialiasing, particularly at high zoom levels.

## 1.2.2[​](#122 "Direct link to 1.2.2")

1st August 2026

### General[​](#general-7 "Direct link to General")

* Internal updates to the `update***` methods to ensure that any associated type change is grouped along with the updates in a transaction.
* Added new `relayoutOnVertexRemove` option to Surface and Paper. Useful when you're using a static layout such as the Hierarchy layout.

### Vue[​](#vue-4 "Direct link to Vue")

* Added `BackgroundComponent`, `GridBackgroundComponent`, `ImageBackgroundComponent` and `TiledImageBackgroundComponent`
* Internal updates to the re-render mechanism

### Angular[​](#angular-4 "Direct link to Angular")

* Added `BackgroundComponent`, `GridBackgroundComponent`, `ImageBackgroundComponent` and `TiledImageBackgroundComponent`
* Added new `$edgeData()`, `$sourceData()` and `$targetData()` signals to the `BaseAngularOverlayComponent`. These give you reactive access to the data for the edge and for its source and target vertices.

### Svelte[​](#svelte-5 "Direct link to Svelte")

* Added `BackgroundComponent`, `GridBackgroundComponent`, `ImageBackgroundComponent` and `TiledImageBackgroundComponent`
* Added `usePaper` hook
* Added `hide` prop to the snippet passed to `SurfacePopup`.
* Updated Svelte component overlays to make the `edge` (and its `source`/`target`) reactive, so the overlay can now show a live view of the edge's backing data or that of its source/target.

### Issue Fixes[​](#issue-fixes "Direct link to Issue Fixes")

* \#5 - Lasso consumes tap event on edge
* Vue/Angular Fix for the `SurfacePopup`'s hide function - it was not locating the ref correctly.

### Breaking[​](#breaking-1 "Direct link to Breaking")

* The `refreshLayoutOnEdgeConnect` Surface/Paper render option was renamed to `relayoutOnEdgeConnect`

## 1.2.1[​](#121 "Direct link to 1.2.1")

28 July 2026

### General[​](#general-8 "Direct link to General")

* The `EVENT_GRAPH_CLEARED` event, fired by the model, now passes the model that fired it as a payload.
* The Surface was updated to fix an issue where it was holding on to stale viewport dimensions: calling `zoomToFit` after external change to viewport element size would use the cached dimensions.
* Added the `data-vjs-no-events` attribute which can be set on any element inside a node vertex, marking it as excluded from firing mouse events for that vertex.
* Updated `centerOn` and `centerOnAndZoom` in the Surface to support optional centering on multiple elements as opposed to just a single one.
* Added support for a `vjs-port` attribute on controls inside an inspector. This allows you to edit properties on ports inside your vertices from the vertex inspector.

### Breaking[​](#breaking-2 "Direct link to Breaking")

* The previous `Index` class was renamed to `GraphSearchIndex`
* In `BaseAngularOverlayComponent`, the `surface` member was renamed to `ui`; its type is now derived from a type parameter on the class (which you declare when you create a subclass)

### React[​](#react-4 "Direct link to React")

* The `useZoom` hook no longer requires that a `ui` can be passed in: it can derive one from the context.
* `overlays` is now marked optional in the `ReactEdgeMapping` interface used in view options
* Added `SurfacePopup` component, an automatic mechanism for launching a popup on a vertex component and keeping it located correctly as the user pans, zooms and drags the vertex.
* `InspectorComponent` updated to function correctly inside a `PaperProvider` or `PaperComponent`

### Vue[​](#vue-5 "Direct link to Vue")

* Added `SurfacePopup` component, an automatic mechanism for launching a popup on a vertex component and keeping it located correctly as the user pans, zooms and drags the vertex.
* Added support for Vue component overlays

### Svelte[​](#svelte-6 "Direct link to Svelte")

* Added `SurfacePopup` component, an automatic mechanism for launching a popup on a vertex component and keeping it located correctly as the user pans, zooms and drags the vertex.
* Added support for Svelte component overlays

### Angular[​](#angular-5 "Direct link to Angular")

* Added `SurfacePopup` component, an automatic mechanism for launching a popup on a vertex component and keeping it located correctly as the user pans, zooms and drags the vertex.
* Added several new signals to the `BaseVertexComponent` - `sourceEdges()`, `allSourceEdges()`, `targetEdges()` and `allTargetEdges()`. With these signals you can dynamically respond to connectivity changes inside your templates.
* Added `PaperComponent` - a fixed view version of SurfaceComponent, with the same support for rendering but no pan/zoom, and which automatically adjusts its dimensions to fit into its viewport.
* Updated `PaperComponent`, `SurfaceComponent` and `DiagramComponent` to make the url/data input signals

## 1.2.0[​](#120 "Direct link to 1.2.0")

July 14th 2026

### General updates[​](#general-updates "Direct link to General updates")

* Circular layout has new `centerContent` option, to avoid placing nodes in negative space (useful when used inside a Group in particular)
* New config `groupProperty` added to model options. You can set the name of the property that identifies group membership in your node/group data, if the default value of `group` clashes with your dataset.
* Added `SelectionGenerator` type, defining the `generator` function that can be used to fill a `VisuallyJsSelection`
* Updated transaction handling to ensure the `transaction(...)` method could be nested cleanly
* Added functionality to the Palette in TAP mode where you can tap an item again to exit the drag (where previously you'd have to press Escape)

### React[​](#react-5 "Direct link to React")

* `data` and `url` are now reactive props in the React `SurfaceComponent`. A small but very powerful change, allowing much greater composability of the `SurfaceComponent` in your apps
* Added new React `PaperComponent`, which functions as a static version of a surface - no pan/zoom or dragging, and the content is zoomed to fit the viewport at all times.
* Added new `useVisuallyJsUpdate` hook. This hook lets you respond to updates in the underlying model, and is handy for such use cases as components which display information about the current state of the model.
* (breaking) The `useZoom()`, `useVisuallyJsModel()` and `useDiagram()` React hooks now return a reactive state object instead of a Promise.

### Angular[​](#angular-6 "Direct link to Angular")

* Added new `useVisuallyJsUpdate` hook. This hook lets you respond to updates in the underlying model, and is handy for such use cases as components which display information about the current state of the model.
* Added new `useZoom` hook, providing access to a signal containing the current zoom for the UI in context.
* Converted the `VisuallyJsService` to expose model/surface/paper/diagram as signals, and deprecated the previous callback approach to accessing these members.
* Updated the `Gantt` starter app to have feature parity with the React Gantt

### Svelte[​](#svelte-7 "Direct link to Svelte")

* Added new `useVisuallyJsUpdate` hook. This hook lets you respond to updates in the underlying model, and is handy for such use cases as components which display information about the current state of the model.
* Added new `NetworkInfrastructure` and `SupplyChain` starter apps. These are clones of the same apps that previously only existed for React/Angular, demonstrating how to build integrated dashboards with various VisuallyJs components sharing a single model.
* Added `BPMN` starter app
* Updated the `Gantt` starter app to have feature parity with the React Gantt
* Updated all of the chart components to source their data from a model in scope, when data/url not provided
* Replaced all usages of `<slot></slot>` elements with the modern `{@render children?.()}` syntax
* Updated `InspectorComponent` to optionally take a 2-way state object defining the current selection. This reduces the amount of boilerplate code required to use the inspector.
* Updated the `SankeyChartComponent` to set the `pivot` property to be reactive
* Added `Mindmap` starter app
* (breaking) The `useZoom()` hook no longer takes `ui` as a prop; it finds the UI from the context

### Vue[​](#vue-6 "Direct link to Vue")

* Added new `useVisuallyJsUpdate` composable
* Updated the `Gantt` starter app to have feature parity with the React Gantt
* Updated `InspectorComponent` to support passing in a `v-model`, which is a reactive object that references the current selected object. Using this, you can do away with the need for `refresh` and `renderEmptyContainer` functions (and that approach is now deprecated)
* Added `BPMN` starter app
* Added `useSurface`, `usePaper` and `useDiagram` composables, for access to the UI in scope
* (breaking) Updated `useZoom` to not take a `ui` as argument, instead resolving the UI from the context
* Added `ERD` starter app - an entity relationship diagram
* Added `Mindmap` starter app
* Added new `NetworkInfrastructure` starter app

### Breaking[​](#breaking-3 "Direct link to Breaking")

* The `useZoom()`, `useVisuallyJsModel()` and `useDiagram()` React hooks now return a reactive state object instead of a Promise.
* The `useZoom()` hook in the Svelte integration no longer takes `ui` as a prop; it finds the UI from the context
* The `useZoom()` composable in the Vue integration no longer takes a `ui` as argument, instead resolving the UI from the context

### Deprecated[​](#deprecated "Direct link to Deprecated")

* The `getModel`, `getSurface`, `getPaper`, `getInspector` and `getDiagrams` methods of the Angular `VisuallyJsService` are deprecated. Use the signals based approach instead.
* The `refresh` and `renderEmptyContainer` functions in the `InspectorComponent` for both the Vue and Svelte integrations are deprecated; see above for alternatives.

## 1.1.4[​](#114 "Direct link to 1.1.4")

29 Jun 2026

* Added support for the lasso inside of groups
* Added support for automatically panning the surface when the user lassos outside of the visible area.
* Lasso is shown on miniview while it is being used (can be switched off)
* Updated miniview so that it highlights vertices that are selected in the canvas
* UI fires `EVENT_EDGE_DRAG_START`, `EVENT_EDGE_DRAG`, `EVENT_EDGE_DRAG_END`, `EVENT_EDGE_DRAG_ABORT` events during edge drag lifecycle now
* Added support for auto pan of the canvas when a user is dragging a new edge or relocating an existing edge.
* Added `addVertexDragFilter(f:VertexDragFilter<BrowserElement>)` method to `Surface`
* Diagrams do not, by default, draw a border around a selected edge now. Use `edges.highlightSelected:true` in your Diagram options to enable this behaviour.
* Improved the way drag handles for edges are drawn to make it easier for users to locate them.

## 1.1.3[​](#113 "Direct link to 1.1.3")

13 Jun 2026

* Fix for issue #2: modelOptions.portSeparator not propagated to Model.

## 1.1.2[​](#112 "Direct link to 1.1.2")

10 Jun 2026

* Updated rotatable label/custom overlays so that the default behaviour is to ensure the overlay is "upright", ie. the text is not flipped, making the overlay difficult to read.
* Added 'strict' label/custom overlay rotate mode, in which the overlay is always rotated to the computed angle, even if it means it may be difficult for the user to read.

## 1.1.1[​](#111 "Direct link to 1.1.1")

9 Jun 2026

* Added support for rotatable custom overlays and HTML element overlays.
* Updated custom overlay `create` method to take edge, UI and model as arguments.

## 1.1.0[​](#110 "Direct link to 1.1.0")

1 Jun 2026

* Added `zoom()` signal to Angular base components, to support selective rendering of content based on zoom level
* Added `useZoom` hook to Svelte and React integrations, to support selective rendering of content based on zoom level
* Added `useZoom` composable to Vue integration, to support selective rendering of content based on zoom level
* Improved API docs
* Updated `ForceDirectedLayout` to ensure that attraction/repulsion is clamped to a specific range, to avoid blowouts in positioning.
* Added support for pluggable router
* Palette uses `.vjs-palette-drag-active` and `.vjs-palette-drag-hover` classes now, instead of using the same ones that are used in the edge drag lifecycle.
* Added scrolling list manager plugin
* Fixed issue in `Snaplines` plugin that would cause it to not reset if drag was aborted.
* Added the ability to provide `sort` function to the `GridLayout` (and `ColumnLayout`/`RowLayout`)
* Fixed positioning issue when labels on a chart were rotated 45 degrees to maximise space

## 1.0.3[​](#103 "Direct link to 1.0.3")

14 May 2026

* Expose `activeFiltering` flag on `DiagramOptions`

## 1.0.2[​](#102 "Direct link to 1.0.2")

13 May 2026

* Adjust source selectors to allow root level element drag in React

## 1.0.1[​](#101 "Direct link to 1.0.1")

13 May 2026

* Packaging updates (readme/issue list etc)

## 1.0.0[​](#100 "Direct link to 1.0.0")

11 May 2026

Initial release.

### Updates[​](#updates "Direct link to Updates")

#### New Features[​](#new-features "Direct link to New Features")

* 3x faster rendering engine
* Charts module, with support for a number of different 2D charts, and export to SVG/PNG/JPG
* SVG diagrams module - dedicated SVG renderer, with support for export to SVG/PNG/JPG
* Diagram tools
* BPMN shapes - tasks, events, pools, lanes, start, end
* Support for "click to add" edges
* Support for edge snap to targets
* Source/target markers (overlays placed at either end of an edge that the edge does not overlap)
* Rotate vertices tool

#### React[​](#react-6 "Direct link to React")

* Modernized API - streamlined and easier to use
* DiagramComponent
* ChartComponents
* InspectorComponent refactored to be far more simple to use
* MiniviewComponent, ControlsComponent, ExportControlsComponent and InspectorComponents can now be declared in your JSX as children of a SurfaceComponent

#### Angular[​](#angular-7 "Direct link to Angular")

* Modernized API - streamlined and easier to use
* A default component is now used for nodes/groups if you do not map one in your view - helpful for rapid prototyping or UIs that dont need complex content.
* Miniview, Controls, ExportControls and Inspector components can now be declared in your template as children of a Surface component

#### Vue[​](#vue-7 "Direct link to Vue")

* Modernized API - streamlined and easier to use
* Added Surface/Diagram providers, allowing for easier composition of UI
* Added injectable VisuallyJs service, exposing the Surface/Model/Diagram that is in the current context for some component.
* All starter apps are now available for Vue

#### Svelte[​](#svelte-8 "Direct link to Svelte")

* Modernized API - streamlined and easier to use
* Added Surface/Diagram providers, allowing for easier composition of UI
* All starter apps are now available for Svelte

#### Miscellaneous updates[​](#miscellaneous-updates "Direct link to Miscellaneous updates")

* Hierarchy layout align leaves on final layer
* Improved orthogonal + bezier connector editors
* Improved documentation
* New look and feel for controls, miniview and resize tools
* Full support for groups and nested groups in the SVG renderer
* SVG shapes updates - new Label shape, shapes publish properties, ShapeLibraryInspector
* Template updates - ability to use the '||' operator in attribute values. Applies when using Vanilla templates and also in the chart and shape library templating.
* Controls component "clear selection" button
* Snaplines plugin now takes rotation into account
* The `ResizingToolsPlugin` registers a drag filter on the underlying Surface, meaning you no longer need to add one in your render options.
* The `updateNode` and `updateGroup` methods now set the position of the vertex's DOM element if the update includes `left` or `top` (or, for a Diagram, `x` or `y`) values. Previously you had to use `setPosition(..)` and then `storePositionInModel(..)`
* Adhoc layouts are now run inside a transaction, and can be undone/redone.
* Added support for `cornerRadius` to Segmented connector.
* Added support for `panWithMetaKey` option to the Surface. With this set, users need to hold the meta/ctrl key in order to instigate a pan.
* Added support for auto entering edge edit mode when user taps (and auto exit when they tap whitespace in the canvas)
* Miniview elements now move as their related surface element is being dragged, unless you set `dynamic:false` on the miniview.

### Breaking changes[​](#breaking-changes "Direct link to Breaking changes")

#### General[​](#general-9 "Direct link to General")

* IMPORTANT: The `Size` interface was changed from `{w:number, h:number}` to `{width:number, height:number}`. This is a small change from a code perspective but with far-reaching effects - any part of a JsPlumb app in which you specify a size for something, be it a grid, or the size of icons in a shape library palette, or the max size for a group, etc, will need to be updated for VisuallyJs to use the new interface. We made this change to make the code more internally consistent: width/height were used by the drawing tools and are also standard for various DOM interfaces.
* The default anchor is now `Continuous`, where previously it was `Bottom`. We listed this above as a feature but if your app is relying on the default at any point you'll see a change.
* The concept of `Endpoint` has been removed. From a visual perspective, you can replace endpoints with the new `Dot`, `Rectangle` and `Ellipse` overlays, optionally registered as markers.
* `Orthogonal` connectors no longer support loading data in the JsPlumb 2.x format.
* The `legacy-json` datatype, in which ports are listed at the top level alongside nodes, groups and edges, is no longer supported.
* The list manager, which was part of JsPlumb Community edition, was removed.
* The concept of a `data manager` - an add-on that responds to changes in the data model - was removed. This functionality can be modelled, if desired, by listening to appropriate model events.
* Dotted notation for left/top values in vertex backing data is no longer supported. Your left/top properties must be in the top level of the backing data for each vertex.
* Removed constant `CLASS_DRAG_SELECT_DEFEAT` - it was a duplicate of `CLASS_SELECT_DEFEAT`

#### Drag/Drop[​](#dragdrop "Direct link to Drag/Drop")

* `SurfaceDropManager` and `DropManager` have been replaced with a new class `Palette`. This class has several enhancements to the previous classes:

  * it has a `click` mode where the user can select an item in the palette and then click on the canvas to drop it
  * it supports `ignoreDropOnNode`, a flag indicating that the palette should just ignore nodes altogether, and whenever something is dropped on a node or hovering over a node, the palette treats it as if it is over whitespace on the canvas

#### Surface[​](#surface "Direct link to Surface")

* Removed `autoExitSelectMode` flag from the surface render options. To set this up now you should provide an `autoExit` flag to the lasso plugin.
* Removed `enhancedView` flag from the surface render options. This behaviour is always switched on now.
* Removed `addToDragSelectionOnSelect` from the surface render options. What this means is that in VisuallyJs if you have one or more vertices in the current selection, they will not be dragged when some other vertex (not in the current selection) is dragged. This probably seems intuitive to you, which is why this flag has been defaulting to false and has now been removed. Use drag groups, or add all nodes you want to drag to the current selection, to drag multiple vertices.
* Removed `refreshAutomatically` flag from the surface render options. This behaviour is permanently switched on in VisuallyJs.
* Removed `storePositionsInModel` from the surface render options. This behaviour is permanently switched on in VisuallyJs.

#### Nodes/Groups[​](#nodesgroups "Direct link to Nodes/Groups")

* `filter` in the surface `dragOptions` is now a function. `cssFilter` has been introduced to replicate what `filter` used to do.

#### Edges[​](#edges "Direct link to Edges")

* Edge geometry uses an object based syntax now instead of array based.
* `simpleEdgeStyles` in render options has been moved into the new `edges` option (instead of `simpleEdgeStyles:true` you now need `{edges:{simpleEdgeStyles:true}}`)
* `propertyMappings` in render options has been moved into the new `edges` option (instead of `propertyMappings:{...}` you now need `{edges:{propertyMappings:{...}}}`)
* `editablePaths` in render options has been moved into the new `edges` option (instead of `editablePaths:true` you now need `{edges:{editable:true}}`)
* `slightlyWonky` option removed from Orthogonal connector

#### Plugins[​](#plugins "Direct link to Plugins")

* The `DrawingToolsPlugin` has been renamed to `ResizingToolsPlugin`, and the associated `.jtk-draw-...` classes have all been renamed to `.vjs-resize-...`. The type has changed from "drawingTools" to "resizingTools" (but its best to use `ResizingToolsPlugin.type` in your render options instead of a string anyway)
* The `ActiveFilteringPlugin` was removed, replaced with an `activeFiltering` option in the render options to a surface.

#### Angular[​](#angular-8 "Direct link to Angular")

* Components are prefixed with `vjs-` instead of `jtk-`

#### Vue[​](#vue-8 "Direct link to Vue")

* Vue 2 Integration removed. Vue 2 reached EOL on December 31st 2023 and is no longer receiving new features, updates or bug fixes.

#### CSS[​](#css "Direct link to CSS")

* The default stylesheet now declares `position:absolute` for `.jtk-miniview` (previously this was `position:relative`).
* Class names are prefixed with `vjs-` instead of `jtk-`.
