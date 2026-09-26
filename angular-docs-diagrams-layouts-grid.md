# Grid Layout

This layout arranges elements into a grid. If you do not provide hints, the number of rows and columns is calculated such that the two values are as close to equal as possible. For instance, this dataset has 11 nodes, and is rendered with 3 rows of 3 columns, with the last row having 2 columns.

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';
import { GridLayout } from "@visuallyjs/browser-ui"


@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  layout: {
    type: GridLayout.type
  }
};
}

```

### Fixed column/row count[​](#fixed-columnrow-count "Direct link to Fixed column/row count")

You can fix the number of columns/rows via the `columns` or `rows` option - here we display the same dataset but with 2 columns.

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';
import { GridLayout } from "@visuallyjs/browser-ui"


@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  layout: {
    type: GridLayout.type,
    options: {
      columns: 2
    }
  }
};
}

```

note

If you supply a fixed value for `columns` and for `rows`, the layout will only honour the `columns` value.

### Sorting entries[​](#sorting-entries "Direct link to Sorting entries")

By default, the order in which entries are placed into the grid depends on the order they are returned from the data source. You can provide a `sort` function to the grid layout to specify an order:

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';
import { GridLayout } from "@visuallyjs/browser-ui"


@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  layout: {
    type: GridLayout.type,
    options: {
      sort: (a,b) => parseInt(b.id, 10) - parseInt(a.id, 10)
    }
  }
};
}

```

In this example we sort based on reverse order of the node ids, so we see node `11` placed first:

The `sort` function receives two arguments, `a` and `b`, which are either `Node` or `Group` objects, and it should return a number indicating their relative order, just like a standard JavaScript sort function.

### Parameters[​](#parameters "Direct link to Parameters")

GridLayoutParameters

Options for the GridLayout.

| Name                 | Type                                                         | Description                                                                                                                                                                                        |
| -------------------- | ------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| columns?             | number                                                       | Optional fixed number of columns. By default this is set to -1 - meaning not fixed - which will result in the layout making its best effort at drawing a grid of equal width and height            |
| height?              | number                                                       | Optional fixed height for the layout.                                                                                                                                                              |
| horizontalAlignment? | [GridLayoutHorizontalAlignment]()                            | Optional alignment for horizontal placement in cells. Defaults to center.                                                                                                                          |
| locationFunction?    | [LocationFunction]()                                         | Optional function that, given some vertex, can provide the x/y location of the vertex on the canvas                                                                                                |
| orientation?         | [GridLayoutOrientation]()                                    | Whether to lay out items row first or column first. Additionally, this setting will determine where any extra items are placed if the dataset does not conform to a grid of equal width and height |
| padding?             | [PointXY]()                                                  | Optional padding to put around the elements.                                                                                                                                                       |
| rows?                | number                                                       | Optional fixed number of rows. By default this is set to -1 - meaning not fixed - which will result in the layout making its best effort at drawing a grid of equal width and height.              |
| sort?                | (a:[Node]() \| [Group](), b:[Node]() \| [Group]()) => number | Optional sort function to run before layout.                                                                                                                                                       |
| verticalAlignment?   | [GridLayoutVerticalAlignment]()                              | Optional alignment for vertical placement in cells. Defaults to center.                                                                                                                            |
| width?               | number                                                       | Optional fixed width for the layout.                                                                                                                                                               |
