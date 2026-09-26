# Sankey Chart

A Sankey chart is a type of flow diagram in which the width of the arrows is proportional to the flow rate. It is ideal for visualizing energy balances, material flows, or any system with defined quantities moving between nodes.

## Example[​](#example "Direct link to Example")

The following example demonstrates a Sankey chart visualizing energy flows. It uses data loaded from a CSV file.

## Usage[​](#usage "Direct link to Usage")

To use the Sankey chart, you need to provide a container element and configuration options, including the source of the data. Data can be sourced from:

* a CSV file, via URL or as a string;
* JSON in the [VisuallyJsDefaultJSON]() format via URL;
* A JS object in the [VisuallyJsDefaultJSON]() format;
* a [DataSource]() - some existing instance of the VisuallyJs model.

```typescript
import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular"
import { Component } from '@angular/core'
    
@Component({
  selector: 'app-root',
  imports: [VisuallyJsModule],
  template: '<vjs-sankeychart [options]="chartOptions"/>',
  styleUrl: './app.css'
})
export class App {
    
  data = ...
    
  chartOptions = {
  url: "/data/sankey-energy-data.csv",
  linkColorStrategy: "source-target",
  height: 600
}   
}

```

### CSV Format[​](#csv-format "Direct link to CSV Format")

The Sankey chart expects data in a CSV format to have `source`, `target`, and `value` columns. For example:

```csv
source,target,value
Agricultural 'waste',Bio-conversion,124.729
Bio-conversion,Liquid,0.597
Bio-conversion,Losses,26.862
Bio-conversion,Solid,280.322
Bio-conversion,Gas,81.144
...

```

The header line should be present.

## Loading data[​](#loading-data "Direct link to Loading data")

### Loading from a URL[​](#loading-from-a-url "Direct link to Loading from a URL")

The Sankey chart will use the extension of a URL to determine what type it expects the data to be in - `.json` or `.csv`.

### Loading CSV data directly[​](#loading-csv-data-directly "Direct link to Loading CSV data directly")

Use the `csvData` option if have CSV as a string that you wish to load:

```javascript
const myCsvData =...

```

```typescript
import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular"
import { Component } from '@angular/core'
    
@Component({
  selector: 'app-root',
  imports: [VisuallyJsModule],
  template: '<vjs-sankeychart [options]="chartOptions"/>',
  styleUrl: './app.css'
})
export class App {
    
  data = ...
    
  chartOptions = {
  csvData: myCsvData,
  linkColorStrategy: "source-target",
  height: 600
}   
}

```

### Loading JS data directly[​](#loading-js-data-directly "Direct link to Loading JS data directly")

```javascript
const myJson:VisuallyJsDefaultJSON =...

```

```typescript
import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular"
import { Component } from '@angular/core'
    
@Component({
  selector: 'app-root',
  imports: [VisuallyJsModule],
  template: '<vjs-sankeychart [options]="chartOptions"/>',
  styleUrl: './app.css'
})
export class App {
    
  data = ...
    
  chartOptions = {
  jsonData: myJson,
  linkColorStrategy: "source-target",
  height: 600
}   
}

```

### Using a DataSource[​](#using-a-datasource "Direct link to Using a DataSource")

Sankey diagrams can also be given a `dataSource` as input, which is of type `VisuallyJsModel`. This is particularly useful for dashboards where you want to show a flow-based overview of an underlying interactive diagram model.

In Angular, you can instruct a Sankey to use a datasource by setting the `useModel` input. This will tell the Sankey to locate the `VisuallyJsService` that is in scope, and retrieve the model from there:

```typescript

import { Component } from "@angular/core"

@Component({
    template:`<div style="display:flex">
	<vjs-surface url="/data/my-diagram.json" />
	<vjs-sankey-chart [useModel]="true" [options]="sankeyOptions"/>
</div>`
})
export class MyComponent {
    sankeyOptions = {
        linkColorStrategy: "source"
    }
}


```

## Pivoting[​](#pivoting "Direct link to Pivoting")

You can `pivot` a Sankey chart, providing the name of a property that is present on each edge in your data. Pivoting a Sankey diagram means that instead of just showing the direct flows between nodes, the diagram groups the edges by the value of the specified property.

A classic example of this is in the Supply Chain demonstration. In that demo, the Sankey chart can be pivoted on `transitMode` (e.g., Air, Sea, Road) or `carrier` (e.g., FedEx, DHL). When pivoted on `transitMode`, the diagram shows the flow of goods broken down by how they were transported, even if they share the same source and target.

Here we see the default Sankey for the supply chain, in which there's a node for each entity, and edges connecting them showing the flow between them:

Edges in this dataset have this data:

```javascript
{
  "value": 300,
  "label": "Global Distribution",
  "transitMode": "Air",
  "carrier": "FedEx"
}

```

We can instruct the Sankey to pivot on an edge value to get a different view of the data. For instance, let's pivot on `transitMode`:

```typescript
import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular"
import { Component } from '@angular/core'
    
@Component({
  selector: 'app-root',
  imports: [VisuallyJsModule],
  template: '<vjs-sankeychart [options]="chartOptions"/>',
  styleUrl: './app.css'
})
export class App {
    
  data = ...
    
  chartOptions = {
  jsonData: myJson,
  linkColorStrategy: "source-target",
  pivot: "transitMode"
}   
}

```

### Dynamic pivot[​](#dynamic-pivot "Direct link to Dynamic pivot")

In Angular, `pivot` is an input on the Sankey chart component, so you can wire up a signal to it and control it from elsewhere in the UI:

* HTML
* Component

```html
<div style="position: relative">
  <div class="controls-panel">
    <label class="pivot-label">Pivot:</label>
    <select class="pivot-select" [value]="pivot()" (change)="onPivotChange($event)">
      <option value="">No pivot</option>
      <option value="transitMode">Transit Mode</option>
      <option value="carrier">Carrier</option>
    </select>
  </div>
  <vjs-sankey-chart url="/dataset.json" [pivot]="pivot()" [options]="options"/>
</div>

```

```typescript
import { Component, signal } from '@angular/core';
import { SankeyOptions } from "@visuallyjs/browser-ui";
import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular";

@Component({
  selector: 'app-root',
  imports: [VisuallyJsModule],
  templateUrl: './app.html'
})
export class App {
  pivot = signal('');

  options:SankeyOptions = {
    ...
  };

  onPivotChange(event: Event) {
    const target = event.target as HTMLSelectElement;
    this.pivot.set(target.value);
  }
}

```

Pivot: Transit Mode (transitMode)

## Link color[​](#link-color "Direct link to Link color")

The `linkColorStrategy` option determines how the links (edges) between nodes are colored. The following strategies are available:

* `static`: Uses a single color for all links. The color can be specified using the `linkColor` option, which defaults to `#444444`.
* `source`: Links are colored using the color of their source node.
* `target`: Links are colored using the color of their target node.
* `source-target`: Links are colored using a gradient that transitions from the source node's color to the target node's color.

## CSS Classes[​](#css-classes "Direct link to CSS Classes")

| Class                   | Description                                                                                                       |
| ----------------------- | ----------------------------------------------------------------------------------------------------------------- |
| `vjs-sankey`            | Assigned to the sankey chart container                                                                            |
| `vjs-sankey-edge`       | Assigned to edges in Sankey chart                                                                                 |
| `vjs-sankey-label`      | Assigned to labels in a sankey chart                                                                              |
| `vjs-sankey-node`       | Assigned to nodes in a sankey chart                                                                               |
| `vjs-sankey-selected`   | Assigned to edges/nodes in Sankey chart when the edge/node forms part of the selected path.                       |
| `vjs-sankey-unselected` | Assigned to edges/nodes in Sankey chart when something is selected but this edge/node is not in the selected path |
