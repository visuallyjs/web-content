# Quick Start

## Installation[​](#installation "Direct link to Installation")

First create a new Angular application (if you need to, otherwise skip this and move to the install command below).

```bash
ng new visuallyjs-app

```

Then `cd` into your project directory and install VisuallyJs:

* npm
* pnpm
* yarn
* bun

```bash
npm install @visuallyjs/browser-ui-angular

```

```bash
pnpm add @visuallyjs/browser-ui-angular

```

```bash
yarn add @visuallyjs/browser-ui-angular

```

```bash
bun add @visuallyjs/browser-ui-angular

```

### Module setup[​](#module-setup "Direct link to Module setup")

If your app is using standalone components you don't need to import the VisuallyJs module. But if you are not using standalone components you'll need to open up `app.module.js` and include the VisuallyJs module:

```typescript
import { CUSTOM_ELEMENTS_SCHEMA } from "@angular/core"
import { VisuallyJsModule } from '@visuallyjs/browser-ui-angular'

...

@NgModule({
    imports:      [ BrowserModule, VisuallyJsModule],
    declarations: [ SomeComponent ],
    bootstrap:    [ SomeComponent ],
    schemas:[ CUSTOM_ELEMENTS_SCHEMA ]
})

```

note

Be sure to import the `CUSTOM_ELEMENTS_SCHEMA` schema when you import the VisuallyJs module. Without this import you will not be able to map components to node/group types.

## MCP[​](#mcp "Direct link to MCP")

To speed up your development you can optionally setup our MCP server with your agent - we provide tools for searching the docs and the apidocs for each library integration. A full discussion of our MCP servers are available on [this page](/angular/docs/mcp.md), but if you've done this before, this is the command you need:

```bash
npx @visuallyjs/browser-ui-angular-mcp

```

## Start building[​](#start-building "Direct link to Start building")

What do you want to build? VisuallyJs can be used to build a variety of different solutions. We split them up into four main categories:

#### [Apps](#apps)[​](#apps "Direct link to apps")

Apps use <!-- -->Angular<!-- --> components to render each node/group in the display. Functionality can be encapsulated in these components. Node/group sizes in an App are typically dependent on CSS and are managed automatically by VisuallyJs. Apps are great when you need rich content in your nodes/groups and you don't want to be limited to using SVG.

#### [Diagrams](#diagrams)[​](#diagrams "Direct link to diagrams")

Diagrams are pure SVG applications, that draw SVG shapes into an SVG canvas, and provide an API to manipulate each cell/link individually. VisuallyJs offers a <!-- -->Angular<!-- --> component that you can use to seamlessly embed a Diagram into your application, as well as several other components such as a miniview, a palette (from which shapes can be dragged onto the canvas), and basic controls such as pan/zoom/undo/redo etc.

#### [Charts](#charts)[​](#charts "Direct link to charts")

VisuallyJs includes a wide range of chart types—from standard Line and Bar charts to more specialized Pie, Donut, and Scatter charts, which can be rendered standalone, or integrated with the data model that is powering an App or Diagram on the same page.

#### [Dashboards](#dashboards)[​](#dashboards "Direct link to dashboards")

A powerful feature of VisuallyJs is the ability to mix and match different types of components on a single page. You can create a dashboard that combines a rich node-based canvas or a diagram with real-time charts, all powered by the same underlying data model.

For example, you might have an app representing a manufacturing process where clicking on a machine (a node in the app) updates a set of charts showing that machine's performance metrics. Or a supply chain visualizer with an attached sankey diagram giving you insights into the flow of materials - there are endless possibilities.

<!-- -->

### Build an App[​](#build-an-app "Direct link to Build an App")

We'll use the `vjs-surface` component from `@visuallyjs/browser-ui-angular` to render a zoomable and pannable canvas.

* app.ts
* app.html
* css

Remove all the code from `app.ts` and replace with this:

```typescript
import { Component } from '@angular/core';
import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular"

@Component({
  selector: 'app-root',
  imports: [VisuallyJsModule],
  templateUrl: './app.html',
  styleUrl: './app.css'
})
export class App {
    
    data = {
        nodes:[
            { id:"1", label:"Hello", left:50, top:50 },
            { id:"2", label:"World", left:50, top:250 }
        ],
        edges:[
            { source:"1", target:"2" }
        ]
    }
    
}


```

Replace the contents of `app.html` with this:

```html
<vjs-surface [data]="data"/>

```

Delete the contents of `app.css`, and then add these lines to `styles.css`:

```css
@import "@visuallyjs/browser-ui/css/visuallyjs.css";
@import "@visuallyjs/browser-ui-angular/css/visuallyjs-angular.css";

app-root {
    width:100vw;
    height:80vh;
    display:block;
}

vjs-surface {
    width:100%;
    height:100%;
}


```

<br />

And that's it! It's very easy to quickly build apps with VisuallyJs. That example uses a default component to render the nodes, which is great to get you up and running, but you'll typically want to provide your own. In this next snippet we supply the component to render each node and we add a miniview and some controls:

* app.ts
* app.html
* my.component.ts
* css

Remove all the code from `app.ts` and replace with this:

```typescript
import { Component } from '@angular/core';
import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular"

@Component({
  selector: 'app-root',
  imports: [VisuallyJsModule],
  templateUrl: './app.html',
  styleUrl: './app.css'
})
export class App {
    
    data = {
        nodes:[
            { id:"1", label:"Hello", left:50, top:50, bg:"cadetblue" },
            { id:"2", label:"World", left:50, top:250, bg:"forestgreen" }
        ],
        edges:[
            { source:"1", target:"2" }
        ]
    }
    
    viewOptions = {
      nodes:{
        default:{
          component:MyComponent
        }
      }        
    }        
}


```

Replace the contents of `app.html` with this:

```html
<vjs-surface [data]="data" [viewOptions]="viewOptions"/>
<vjs-controls/>
<vjs-miniview/>

```

Create a new component:

```bash
ng generate component MyComponent

```

and then inside `my.component.ts`, put this:

```typescript
import {Component} from "@angular/core"
import {BaseNodeComponent} from "@visuallyjs/browser-ui-angular"

@Component({
    template:`<div style="background-color:{{data['bg']}};padding:0.5rem;">
        <span (click)="displayAlert()">{{data['label']}}</span>
  </div>`,
    styleUrl:"./my-component.css"
})
export class MyComponent extends BaseNodeComponent {

    displayAlert() {
        alert(`You clicked on vertex ${this.getNode().id}`)
    }
}

```

Delete the contents of `app.css`, and then add these lines to `styles.css`:

```css
@import "@visuallyjs/browser-ui/css/visuallyjs.css";
@import "@visuallyjs/browser-ui-angular/css/visuallyjs-angular.css";

app-root {
    width:100vw;
    height:80vh;
    display:block;
}

vjs-surface {
    width:100%;
    height:100%;
}

```

Inside `my-component.css` put this (or any styles you'd like for your new component!):

```css
.vjs-node {
  width:100px;
  height:80px;
  display:flex;
  align-items: center;
  justify-content: center;
}


```

**********

Try clicking on the label for each node - you'll get a popup with its ID, which is sourced from the vertex tracked by the underlying `BaseNodeComponent`. This is a simple example but hopefully gives you an idea of what is possible when you use Angular components to render the nodes in your UI.

To find out more about building Angular apps with VisuallyJs, we'd suggest [starting here](/angular/docs/apps.md).

### Buid a Diagram[​](#buid-a-diagram "Direct link to Buid a Diagram")

***

Diagrams use SVG shapes to render their nodes and groups. It's straightforward to create one:

* app.ts
* app.html
* css

Remove all the code from `app.ts` and replace with this:

```typescript
import { Component } from '@angular/core';
import { FLOWCHART_SHAPES, ArrowOverlay } from "@visuallyjs/browser-ui"
import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular"

@Component({
  selector: 'app-root',
  imports: [VisuallyJsModule],
  templateUrl: './app.html',
  styleUrl: './app.css'
})
export class App {        
  data = {
    nodes:[
      { id:"1", label:"Begin", x:50, y:50, width:100, height:40, type:"terminus" },
      { id:"2", label:"Test", x:70, y:200, width:60, height:60, type:"decision" }
     ],
     edges:[
       { source:"1", target:"2" }
     ]
   }
   
   diagramOptions = {
     shapes:FLOWCHART_SHAPES,
     edges:{
       overlays:[
         { type:ArrowOverlay.type, options:{location:1}}
       ]
     },
     zoomToFit:true
   }            
}


```

Replace the contents of `app.html` with this:

```html
<vjs-diagram [data]="data" [options]="diagramOptions"/>

```

Delete the contents of `app.css`, and then add these lines to `styles.css`:

```css
@import "@visuallyjs/browser-ui/css/visuallyjs.css";
@import "@visuallyjs/browser-ui-angular/css/visuallyjs-angular.css";

```

**********

### Build a Chart[​](#build-a-chart "Direct link to Build a Chart")

***

VisuallyJs has support for many different types of charts. Here's a simple column chart:

which we generated with this code:

```typescript
import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular"
import { Component } from '@angular/core'
    
@Component({
  selector: 'app-root',
  imports: [VisuallyJsModule],
  template: '<vjs-column-chart [data]="data" [options]="chartOptions"/>',
  styleUrl: './app.css'
})
export class App {
    
  data = [
    {id:"USA",corn:387749,wheat:45321},
     {id:"China",corn:280000,wheat:140000},
     {id:"Brazil",corn:129000,wheat:10000},
     {id:"EU",corn:64300,wheat:140500},
     {id:"Argentina",corn:54000,wheat:19500},
     {id:"India",corn:34300,wheat:113500}
]
    
  chartOptions = {
  title: {
    text: "Corn vs wheat estimated production for 2023"
  },
  valueAxis: [
    {
      title: {
        text: "1000 metric tons (MT)"
      }
    }
  ],
  series: [
    {
      valueField: "corn",
      label: "Corn"
    },
    {
      valueField: "wheat",
      label: "Wheat"
    }
  ]
}   
}

```

Here we pass the data in to the chart when the chart is created, but there are a number of ways to supply data to chart, including the ability for a chart to source its data from the model backing an App or Diagram.

See the [charts docs](/angular/docs/charts/concepts/overview.md) for a full discussion of how to use VisuallyJs to render charts.

### Build a Dashboard[​](#build-a-dashboard "Direct link to Build a Dashboard")

***

It's easy to build dashboards with VisuallyJs where multiple components all reference the same data model. Here we'll show you a quick example which is from our [dashboards documentation](/angular/docs/dashboards.md) - a scatter chart that reflects the positions of the nodes in the canvas.

* app.ts
* app.html
* css

Remove all the code from `app.ts` and replace with this:

```typescript
    import { Component } from '@angular/core';
    import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular"

    @Component({
      selector: 'app-root',
      imports: [VisuallyJsModule],
      templateUrl: './app.html',
      styleUrl: './app.css'
    })
    export class App {
        
        data = {
            nodes:[
                { id:"1", label:"Hello", left:50, top:50 },
                { id:"2", label:"World", left:50, top:250 }
            ],
            edges:[
                { source:"1", target:"2" }
            ]
        }

chartOptions={
series:[
{
xAxisField:"left",
yAxisField:"top",
color:"#569934"
}
],
yAxis:{
inverted:true
}
}
        
    }
    

```

Replace the contents of `app.html` with this:

```html
<div class="my-container">
    <vjs-surface [data]="data"/>
    <vjs-scatter-chart [options]="chartOptions"/>
</div>

```

Delete the contents of `app.css`, and then add these lines to `styles.css`:

```css
@import "@visuallyjs/browser-ui/css/visuallyjs.css";
@import "@visuallyjs/browser-ui-angular/css/visuallyjs-angular.css";

app-root {
    width:100vw;
    height:80vh;
    display:block;
}

vjs-surface {
    width:100%;
    height:100%;
}
.my-container {
    width:600px;
    height:500px;
    position:relative;
    outline:1px solid;
    display:flex;
}

.vjs-surface {
    flex:0 0 50%;
    height:100%;
}

.vjs-scatter-chart {
    flex:0 0 50%;
    height:100%;
}


```

**********

## Next Steps[​](#next-steps "Direct link to Next Steps")

***

Where to from here?

[Apps](/angular/docs/apps.md)

[Read about building professional visual apps with Angular components](/angular/docs/apps.md)

[Diagrams](/angular/docs/diagrams.md)

[Read about how to build SVG diagrams with VisuallyJs](/angular/docs/diagrams.md)

[Charts](/angular/docs/charts)

[Read about VisuallyJs's powerful chart engine](/angular/docs/charts)

[Dashboards](/angular/docs/dashboards.md)

[Read more about how to build dashboards with VisuallyJs](/angular/docs/dashboards.md)

[Templates](/angular/templates)

[Clone an app, diagram or chart template project](/angular/templates)

[API Reference](/api-reference)

[Browse the VisuallyJs API docs](/api-reference)
