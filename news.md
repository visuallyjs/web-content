## [Release 1.2.8](./news-2026-09-26-release-1.2.8.md)

September 26, 2026 ·

<!-- -->

2 min read

Release 1.2.8 is now available. In this release:

### General[​](#general "Direct link to General")

* Added a new `GraphPropagationEngine` class, plus associated `GraphPropagationEnginePlugin`. This offers a way to propagate properties from one vertex to another, based on a set of rules.
* Added support for `readOnly` on a `ShapePropertyDefinition` - inspectors will show you the value but not allow you to edit it.
* Fixed an issue in `ShapePropertiesInspector` components where radio buttons for a given value were not all assigned the same name
* Updated our private NPM repository to respond to the NPM `/whoami` endpoint. This facilitates usage of our NPM repository as a remote repository in apps such as JFrog.
* Updated our [Logic Gates starter apps](./demonstrations-logic-gates.md) to include the graph propagation engine.
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
