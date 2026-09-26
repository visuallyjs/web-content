# Layouts

A core piece of functionality offered by the VisuallyJs UI is support for layouts - a means to control the positioning of the vertices in your application.

The default layout used is the [Absolute layout](/vanilla/docs/diagrams/layouts/absolute.md).

## Applying a layout[​](#applying-a-layout "Direct link to Applying a layout")

<!-- -->

To apply a layout to an app, supply the spec for the layout in your render options:

<!-- -->

The contents of `options` depend on the specific layout you are configuring.

## Available layouts[​](#available-layouts "Direct link to Available layouts")

The available layouts are:

* [Absolute](/vanilla/docs/diagrams/layouts/absolute.md) This layout positions vertices dependent on values in each vertex's backing data. For many applications in which the position of vertices is under the control of a user, this layout is a good choice. It can be combined with other layouts, such as the ForceDirected layout, to implement a scheme whereby vertices untouched by a user are placed automatically and vertices touched by a user are placed wherever the user chose.

* [ForceDirected](/vanilla/docs/diagrams/layouts/force-directed.md) Positions vertices in an optimum position relative to vertices to which they are connected. This layout is an extension of the Absolute layout, which can be instructed to honour user-supplied values for vertices if present.

* [Balloon](/vanilla/docs/diagrams/layouts/balloon.md) This layout groups vertices into clusters. This is a useful layout for certain types of unstructured data such as mind maps.

* [Hierarchy](/vanilla/docs/diagrams/layouts/hierarchy.md) Positions vertices in a hierarchy, oriented either vertically or horizontally. The classic use cases for this layout are such things as a family tree or an org chart.

* [Circular](/vanilla/docs/diagrams/layouts/circular.md) Arranges vertices instance into a circle, with a radius sufficiently large that no two vertices overlap.

* [Grid](/vanilla/docs/diagrams/layouts/grid.md) Arranges vertices into a grid, optionally with restrictions placed on the number of columns or rows.

* [Column](/vanilla/docs/diagrams/layouts/column.md) Arranges vertices into a column - a specialized instance of the Grid layout.

* [Row](/vanilla/docs/diagrams/layouts/row.md) Arranges vertices into a row - a specialized instance of the Grid layout.
