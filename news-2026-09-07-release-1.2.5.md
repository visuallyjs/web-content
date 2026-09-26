# Release 1.2.5

September 7, 2026 ·

<!-- -->

3 min read

Release 1.2.5 is now available, and it's a big one! In this release:

### General[​](#general "Direct link to General")

* Added support for rotating elements that are being dragged from a palette by tapping/holding a specific key
* Added the concept of "auto edge connect": elements that are being dragged from the palette can be automatically connected to existing vertices by dragging them over connection points.
* The `ShapePalette` and `DiagramPalette` classes now support `allowDropOnEdge` - you can drag a shape onto an edge and drop it, and the edge will be automatically split.
* Fixed painting issue with lasso in SVG containers
* Fixed issue with incorrect location of port elements on a rotated node in an SVG container
* Aesthetic improvements to the lasso in both apps and diagrams, including exposing several new CSS vars for theming.
* Added support for `data-vjs-anchor`, `data-vjs-source-anchor` and `data-vjs-target-anchor` to edge drag/click to add functionality.

### Starter Apps[​](#starter-apps "Direct link to Starter Apps")

* New starter app `Fault Tree Analysis` added. This is a dashboard containing a Fault Tree Analysis chart, with a Cut Sets view and a Risk Contribution view

![fault tree analysis](https://static.visuallyjs.com/img/app-card/fault-tree-analysis-2400.png)

* New starter app `Logic Gates` added

![fault tree analysis](https://static.visuallyjs.com/img/app-card/logic-gates-2400.png)

* New starter app `Circuit Diagram` added

![fault tree analysis](https://static.visuallyjs.com/img/app-card/circuit-diagram-2400.png)

### Vue[​](#vue "Direct link to Vue")

* Made the `data` and `url` props of the `SurfaceComponent` and `PaperComponent` reactive, making these components easier to work with inside a Vue app.
* Added support for rotating elements that are being dragged from a palette by tapping a specific key
* Added auto edge connect support to `PaletteComponent`, `DiagramPaletteComponent` and `ShapePaletteComponent`

### Svelte[​](#svelte "Direct link to Svelte")

* Made the `data` and `url` props of the `SurfaceComponent` and `PaperComponent` reactive, making these components easier to work with inside a Svelte app.
* Added support for rotating elements that are being dragged from a palette by tapping a specific key
* Added auto edge connect support to `PaletteComponent`, `DiagramPaletteComponent` and `ShapePaletteComponent`

### React[​](#react "Direct link to React")

* Added support for rotating elements that are being dragged from a palette by tapping a specific key
* Added auto edge connect support to `PaletteComponent`, `DiagramPaletteComponent` and `ShapePaletteComponent`

### Angular[​](#angular "Direct link to Angular")

* Added support for rotating elements that are being dragged from a palette by tapping a specific key
* Added auto edge connect support to `PaletteComponent`, `DiagramPaletteComponent` and `ShapePaletteComponent`

### Breaking[​](#breaking "Direct link to Breaking")

* The new `updateTypeOnPaletteTap` option for shape palettes and diagram palettes technically constitutes a breaking change, as this flag switches on behaviour that was previously on by default: when something is selected in the canvas and you click a shape in the palette, the selected vertices' type is changed to match the clicked shape.
