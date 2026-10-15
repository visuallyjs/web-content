## [Release 1.2.0](/news/2026/07/15/release-1.2.0.md)

July 15, 2026 ·

<!-- -->

5 min read

sporritt

This release focuses on a few main things:

## Hooks and Reactivity[​](#hooks-and-reactivity "Direct link to Hooks and Reactivity")

We've updated each of our integrations to be more reactive - the React hooks, for instance, now return reactive state instead of Promises and the Angular service exposes its various members as signals, instead of getters with callbacks. Additionally, we've added a `useVisuallyJsUpdate()` hook to each of our integrations, allowing you to easily extract a dynamically updating value from the underlying model.

## Inspectors[​](#inspectors "Direct link to Inspectors")

Our Vue and Svelte inspectors have been updated to interoperate seamlessly with a piece of reactive state, cutting down on the amount of boilerplate you're required to write

## Starter apps[​](#starter-apps "Direct link to Starter apps")

Each of our library integrations - Vue, React, Svelte and Angular - offers the same full list of starter apps, and all of our starter apps have been updated to take advantage of the many updates 1.2.0 has to offer.

## Changelog[​](#changelog "Direct link to Changelog")

### General updates[​](#general-updates "Direct link to General updates")

* Circular layout has new `centerContent` option, to avoid placing nodes in negative space (useful when used inside a Group in particular)
* New config `groupProperty` added to model options. You can set the name of the property that identifies group membership in your node/group data, if the default value of `group` clashes with your dataset.
* Added `SelectionGenerator` type, defining the `generator` function that can be used to fill a `VisuallyJsSelection`
* Updated transaction handling to ensure the `transaction(...)` method could be nested cleanly
* Added functionality to the `Palette` in "tap" mode where you can tap an item again to exit the drag (previously you'd have to press Escape)

### React[​](#react "Direct link to React")

* `data` and `url` are now reactive props in the React `SurfaceComponent`. A small but very powerful change, allowing much greater composability of the `SurfaceComponent` in your apps
* Added new React `PaperComponent`, which functions as a static version of a surface - no pan/zoom or dragging, and the content is zoomed to fit the viewport at all times.
* Added new `useVisuallyJsUpdate` hook. This hook lets you respond to updates in the underlying model, and is handy for such use cases as components which display information about the current state of the model.
* (breaking) The `useZoom()`, `useVisuallyJsModel()` and `useDiagram()` React hooks now return a reactive state object instead of a Promise.

### Angular[​](#angular "Direct link to Angular")

* Added new `useVisuallyJsUpdate` hook. This hook lets you respond to updates in the underlying model, and is handy for such use cases as components which display information about the current state of the model.
* Added new `useZoom` hook, providing access to a signal containing the current zoom for the UI in context.
* Converted the `VisuallyJsService` to expose model/surface/paper/diagram as signals, and deprecated the previous callback approach to accessing these members.
* Updated the `Gantt` starter app to have feature parity with the React Gantt

### Svelte[​](#svelte "Direct link to Svelte")

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

### Vue[​](#vue "Direct link to Vue")

* Added new `useVisuallyJsUpdate` composable
* Updated the `Gantt` starter app to have feature parity with the React Gantt
* Updated `InspectorComponent` to support passing in a `v-model`, which is a reactive object that references the current selected object. Using this, you can do away with the need for `refresh` and `renderEmptyContainer` functions (and that approach is now deprecated)
* Added `BPMN` starter app
* Added `useSurface`, `usePaper` and `useDiagram` composables, for access to the UI in scope
* (breaking) Updated `useZoom` to not take a `ui` as argument, instead resolving the UI from the context
* Added `ERD` starter app - an entity relationship diagram
* Added `Mindmap` starter app
* Added new `NetworkInfrastructure` starter app

### Breaking[​](#breaking "Direct link to Breaking")

* The `useZoom()`, `useVisuallyJsModel()` and `useDiagram()` React hooks now return a reactive state object instead of a Promise.
* The `useZoom()` hook in the Svelte integration no longer takes `ui` as a prop; it finds the UI from the context
* The `useZoom()` composable in the Vue integration no longer takes a `ui` as argument, instead resolving the UI from the context

### Deprecated[​](#deprecated "Direct link to Deprecated")

* The `getModel`, `getSurface`, `getPaper`, `getInspector` and `getDiagrams` methods of the Angular `VisuallyJsService` are deprecated. Use the signals based approach instead.
* The `refresh` and `renderEmptyContainer` functions in the `InspectorComponent` for both the Vue and Svelte integrations are deprecated; see above for alternatives.

[**Read more**](/news/2026/07/15/release-1.2.0.md)
