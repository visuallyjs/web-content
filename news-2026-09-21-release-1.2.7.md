# Release 1.2.7

September 21, 2026 ·

<!-- -->

3 min read

Release 1.2.7 is now available. In this release:

### General[​](#general "Direct link to General")

* Added new [Scada/HMI starter app](/demonstrations/scada-hmi.md) to all libraries. This app provides a solid foundation on which you can build your own Scada/HMI apps, with a look and feel that is aligned with the HMI ISA-101 Standard.

* Update bubble/scatter chart custom marker code to not require namespaced elements in the SVG snippets returned from a `resolveMarker` call

* Added `name` to `PropertyMappings`. This is an optional human readable name that is used by inspectors.

* Updated overlay definition code to handle the case that an overlay/marker is specified as an object with "type" but no "options"

* Improved CSS/rendering for the edge type picker

* Added support for boolean false for 'rotatable' property of `Label`/`Custom` overlay: with this set, the label never rotates to make the text upright.

* Added new CSS vars to resize tools/diagram tools plugins:

  <!-- -->

  * `--vjs-resize-handle-fill-color` For the fill of the resize handles, defaults to `#FFFFFF`
  * `--vjs-resize-frame-line-width` For the stroke width of the resize frame, defaults to `2px`

### React[​](#react "Direct link to React")

* Made the `options` prop of all charts reactive, so that the chart re-initializes if it changes
* Added `EdgePropertyMappingsInspector` component - an inspector that automatically renders a form for managing the properties of an edge from the installed edge property mappings.
* Added `ShapePropertiesInspector` component - an inspector that automatically renders a form for managing the properties of some shape defined in a shape set

### Angular[​](#angular "Direct link to Angular")

* Made the `data`, `url` and `options` inputs reactive on all charts
* Added `EdgePropertyMappingsInspector` component - an inspector that automatically renders a form for managing the properties of an edge from the installed edge property mappings.
* Added `ShapePropertiesInspector` component - an inspector that automatically renders a form for managing the properties of some shape defined in a shape set

### Svelte[​](#svelte "Direct link to Svelte")

* Made the `data`, `url` and `options` props reactive on all charts
* Added `EdgePropertyMappingsInspector` component - an inspector that automatically renders a form for managing the properties of an edge from the installed edge property mappings.
* Added `ShapePropertiesInspector` component - an inspector that automatically renders a form for managing the properties of some shape defined in a shape set
*

### Vue[​](#vue "Direct link to Vue")

* Made the `data`, `url` and `options` props reactive on all charts
* Added `EdgePropertyMappingsInspector` component - an inspector that automatically renders a form for managing the properties of an edge from the installed edge property mappings.
* Added `ShapePropertiesInspector` component - an inspector that automatically renders a form for managing the properties of some shape defined in a shape set
