# Programmatic API

VisuallyJS supports both declarative and programmatic approaches to diagramming:

* **Declarative**: You can define the entire state of the diagram at once using a data object - this is often the preferred way when loading a saved diagram or when the UI is driven by external state.
* **Programmatic**: Once a diagram is created, you can interact with it at a granular level. You can add or remove individual cells and links, and you can manipulate existing cells by changing their properties (label, color, size, etc.) through the `DiagramCell` and `DiagramLink` classes.

To access the underlying Diagram in an Angular app, declare a `ViewChild()` and then access the `diagram` class member on it:

```typescript

import { Component, ViewChild } from '@angular/core'
import { DiagramComponent } from '@visuallyjs/browser-ui-angular'
import "@visuallyjs/browser-ui/css/visuallyjs.css"

@Component({
  template:'<vjs-diagram [data]="data" [options]="options"/>'
})
export class MyComponent {

  @ViewChild('diagramComponent') diagramComponent: DiagramComponent

  data = { ... }

  options = {...}

  doSomething() {
    const diagram = this.diagramComponent.diagram
    // now you can invoke methods on "diagram"
  } 
}

```

## Manipulating Diagram Cells[​](#manipulating-diagram-cells "Direct link to Manipulating Diagram Cells")

The `addCell` method on a `Diagram` instance returns an instance of `DiagramCell`. You can also retrieve an existing cell using the `getCell(id)` method.

### Getting a Cell[​](#getting-a-cell "Direct link to Getting a Cell")

```javascript
const cell = diagram.getCell("1");

```

The return value is of type [DiagramCell]().

### Setting Basic Properties[​](#setting-basic-properties "Direct link to Setting Basic Properties")

`DiagramCell` provides several methods to update its visual appearance and data:

* **`setLabel(label: string)`**: Updates the cell's label text.
* **`setFill(fill: string)`**: Sets the cell's fill color (e.g., "#ff0000").
* **`setOutline(outline: string)`**: Sets the color of the cell's outline.
* **`setOutlineWidth(width: number)`**: Sets the thickness of the cell's outline.
* **`setColor(color: string)`**: Sets the color of the cell's label text.

Example:

```javascript
cell.setLabel("Process Completed");
cell.setFill("#d4edda");
cell.setOutline("#28a745");
cell.setOutlineWidth(2);
cell.setColor("#155724");

```

### Positioning and Sizing[​](#positioning-and-sizing "Direct link to Positioning and Sizing")

You can move and resize cells programmatically:

* **`setPosition(p: PointXY)`**: Moves the cell to the specified coordinates `{x, y}`.
* **`setSize(s: Size)`**: Sets the cell's width and height `{width, height}`.

```javascript
cell.setPosition({ x: 250, y: 150 });
cell.setSize({ width: 150, height: 100 });

```

### Updating arbitrary data[​](#updating-arbitrary-data "Direct link to Updating arbitrary data")

You can update any data on a cell via the low-level **`update`** method. Each of the methods discussed previously on this page are in fact wrappers around a call to `update`, with the appropriate properties.

```javascript
cell.update({ foo:"someValue" });

```

### Z-Index and Visibility[​](#z-index-and-visibility "Direct link to Z-Index and Visibility")

* **`toFront()`**: Brings the cell to the front of all other cells.
* **`toBack()`**: Sends the cell behind all other cells.

### Removing a cell[​](#removing-a-cell "Direct link to Removing a cell")

To delete a cell and its associated model object from the diagram, call **`remove()`**:

```javascript
cell.remove()

```

caution

Once you have called `remove` on a cell, the cell is no longer attached to the diagram, and invoking any methods on it will give indefinite results.

## Adding Cells and Links Programmatically[​](#adding-cells-and-links-programmatically "Direct link to Adding Cells and Links Programmatically")

You can add new elements to the diagram at any time:

#### Adding a Cell[​](#adding-a-cell "Direct link to Adding a Cell")

The `addCell` method requires at least a `type` property. If dimensions or positions are omitted, defaults will be used.

```javascript
const newCell = diagram.addCell({
    type: "terminus",
    x: 400,
    y: 100,
    label: "End"
});

```

## Manipulating Links[​](#manipulating-links "Direct link to Manipulating Links")

#### Adding a Link[​](#adding-a-link "Direct link to Adding a Link")

The `addLink` method connects two cells. You can pass the `DiagramCell` objects directly or use their IDs.

```javascript
const link = diagram.addLink({
    source: cell,
    target: newCell
});

```

This method returns an instance of [DiagramLink]().

#### Styling Links[​](#styling-links "Direct link to Styling Links")

`DiagramLink` provides methods to update the visual appearance of a link, leveraging the "simple edge styles" functionality:

* **`setLabel(label: string)`**: Updates the link's label text.
* **`setColor(color: string)`**: Sets the link's stroke color.
* **`setLineWidth(width: number)`**: Sets the thickness of the link.
* **`setDashArray(dashArray: string)`**: Sets the dash pattern for the link (e.g., "5,5").
* **`setOutlineColor(color: string)`**: Sets the color of the link's outline.
* **`setOutlineWidth(width: number)`**: Sets the thickness of the link's outline.
* **`setLabelLocation(location: number)`**: Sets the position of the label along the link (0 to 1).

Example:

```javascript
link.setLabel("Depends On");
link.setColor("#007bff");
link.setLineWidth(2);
link.setDashArray("2,2");

```

#### Connectivity[​](#connectivity "Direct link to Connectivity")

You can change the source or target of an existing link:

* **`setSource(source: string | DiagramCell | PointXY)`**: Reconnects the link's source.
* **`setTarget(target: string | DiagramCell | PointXY)`**: Reconnects the link's target.

#### Z-Index and Lifecycle[​](#z-index-and-lifecycle "Direct link to Z-Index and Lifecycle")

* **`toFront()`**: Brings the link to the front.
* **`toBack()`**: Sends the link to the back.
* **`remove()`**: Deletes the link from the diagram.
