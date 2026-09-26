# Shapes

<!-- -->

Shapes in a Diagram are provided by one or more **Shape Sets**. A shape set is a collection of named SVG shapes that the Diagram can use to render its nodes and groups.

## Configuration[​](#configuration "Direct link to Configuration")

You configure the shapes for a Diagram using the `shapes` option to a diagram. This option accepts either a single `ShapeSet` or an array of `ShapeSet` objects.

```typescript
import { FLOWCHART_SHAPES, BASIC_SHAPES } from "@visuallyjs/browser-ui"
import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular";
import {Component} from "@angular/core";

@Component({
    template:`<div style="width:100%;height:500px">
<vjs-diagram [data]="data" [options]="options"/>
</div>`
export class MyComponent {
    data = ...
    
    options = {
  shapes: [ FLOWCHART_SHAPES, BASIC_SHAPES ]
}
}

```

## Available shape sets[​](#available-shape-sets "Direct link to Available shape sets")

VisuallyJs ships with two shape sets in the `browser-ui` package and a set of BPMN shapes:

### Flowchart[​](#flowchart "Direct link to Flowchart")

```javascript
import { FLOWCHART_SHAPES } from "@visuallyjs/browser-ui"

```

***

### Basic[​](#basic "Direct link to Basic")

```javascript
import { BASIC_SHAPES } from "@visuallyjs/browser-ui"

```

### BPMN[​](#bpmn "Direct link to BPMN")

```javascript
import { BPMN2_SHAPES } from "@visuallyjs/bpmn"

```

info

These shapes are shipped in the `@visuallyjs/bpmn` library - you'll need to import it.

## Custom shape sets[​](#custom-shape-sets "Direct link to Custom shape sets")

It's straightforward to make your own shape set - they consist of an id and then a list of shapes, for each of which you provide SVG.

Here we have made a set of faces:

**********

```javascript
const shapes = {
    id:"faces",
    shapes:[
        {
            type:"impassive",
            template:`<g>
<circle cx="{{width/2}}" cy="{{height/2}}" r="{{(width/2)}}"/>
    <path d="M {{width/4}} {{height*3/4}} L {{width*3/4}} {{height*3/4}}"/>
    <circle cx="{{width/4}}" cy="{{height/4}}" r="10"/>
    <circle cx="{{width*3/4}}" cy="{{height/4}}" r="10"/>
    <circle cx="{{width/2}}" cy="{{height/2}}" r="10"/>
    </g>`,
        label:"Impassive"
    },
    {
        type:"pleased",
        template:`<g>
            <circle cx="{{width/2}}" cy="{{height/2}}" r="{{(width/2)}}"/>            
            <circle cx="{{width/4}}" cy="{{height/4}}" r="10"/>
            <circle cx="{{width*3/4}}" cy="{{height/4}}" r="10"/>
            <circle cx="{{width/2}}" cy="{{height/2}}" r="10"/>
            <path d="M {{width/4}} {{height*3/4}} C {{width/4}} {{height*7/8}}, {{width*3/4}} {{height*7/8}} {{width*3/4}} {{height*3/4}}"/>
            </g>`,
        label:"Pleased"
    },
    {
        type:"notpleased",
        template:`<g>
              <circle cx="{{width/2}}" cy="{{height/2}}" r="{{(width/2)}}"/>            
              <circle cx="{{width/4}}" cy="{{height/4}}" r="10"/>
              <circle cx="{{width*3/4}}" cy="{{height/4}}" r="10"/>
              <circle cx="{{width/2}}" cy="{{height/2}}" r="10"/>
              <path d="M {{width/4}} {{height*3/4}} C {{width/4}} {{height*5/8}}, {{width*3/4}} {{height*5/8}} {{width * 0.75}} {{height * 0.75}}"/>
              </g>`,
        label:"Not Pleased"
    }
    ]
}

```
