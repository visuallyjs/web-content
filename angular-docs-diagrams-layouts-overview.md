# Layouts

A core piece of functionality offered by the VisuallyJs UI is support for layouts - a means to control the positioning of the vertices in your application.

The default layout used is the [Absolute layout](/angular/docs/diagrams/layouts/absolute.md).

## Applying a layout[​](#applying-a-layout "Direct link to Applying a layout")

<!-- -->

To apply a layout to an app, supply the spec for the layout in your render options:

```typescript
import { ForceDirectedLayout } from "@visuallyjs/browser-ui"
import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular";
import {Component} from "@angular/core";

@Component({
    template:`<div style="width:100%;height:500px">
<vjs-diagram [data]="data" [options]="options"/>
</div>`
export class MyComponent {
    data = ...
    
    options = {
  layout: {
    type: ForceDirectedLayout.type,
    options: {
      spacing: 150
    }
  }
}
}

```

The contents of `options` depend on the specific layout you are configuring.

## Available layouts[​](#available-layouts "Direct link to Available layouts")

The available layouts are:

* [Absolute](/angular/docs/diagrams/layouts/absolute.md) This layout positions vertices dependent on values in each vertex's backing data. For many applications in which the position of vertices is under the control of a user, this layout is a good choice. It can be combined with other layouts, such as the ForceDirected layout, to implement a scheme whereby vertices untouched by a user are placed automatically and vertices touched by a user are placed wherever the user chose.

* [ForceDirected](/angular/docs/diagrams/layouts/force-directed.md) Positions vertices in an optimum position relative to vertices to which they are connected. This layout is an extension of the Absolute layout, which can be instructed to honour user-supplied values for vertices if present.

* [Balloon](/angular/docs/diagrams/layouts/balloon.md) This layout groups vertices into clusters. This is a useful layout for certain types of unstructured data such as mind maps.

* [Hierarchy](/angular/docs/diagrams/layouts/hierarchy.md) Positions vertices in a hierarchy, oriented either vertically or horizontally. The classic use cases for this layout are such things as a family tree or an org chart.

* [Circular](/angular/docs/diagrams/layouts/circular.md) Arranges vertices instance into a circle, with a radius sufficiently large that no two vertices overlap.

* [Grid](/angular/docs/diagrams/layouts/grid.md) Arranges vertices into a grid, optionally with restrictions placed on the number of columns or rows.

* [Column](/angular/docs/diagrams/layouts/column.md) Arranges vertices into a column - a specialized instance of the Grid layout.

* [Row](/angular/docs/diagrams/layouts/row.md) Arranges vertices into a row - a specialized instance of the Grid layout.
