# Load, save and export

Getting data into and out of a VisuallyJs diagram is easy. There are a few different approaches you can use:

* You can [load/save JSON](#loading-json) directly on a Diagram, either as a JS object or via a URL;

* You can supply an initial dataset or URL to load data into certain UI components - read more here]\(component-load);

* You can [export](#export) a diagram as SVG, PNG or JPEG.

Appending Data

Data can be appended via the `load` method, since it does not cause the underlying model to be cleared.

***

## Diagram JSON Syntax[​](#diagram-json-syntax "Direct link to Diagram JSON Syntax")

The JSON representation of a diagram consists of a JSON object with arrays for `nodes`, `groups` and `edges`. All of these are optional, but of course if you declare an edge then the nodes/groups for that edge must be present in the dataset.

Each node/group definition declares a `type`, which maps it to a shape, as well as, optionally, a `category`, which provides the name of the shape library the shape belongs to. If you diagram has only one shape library installed, `category` is not necessary. Shapes also include positioning information and, optionally, labels, as well as information about the shape's appearance, including such things as fill, outline width, outline color etc.

Here's an example dataset for a flowchart, with 2 shapes and 1 edge:

```javascript
{
  "nodes": [
    { 
        "id":"1", 
        "label":"foo", 
        "type":"process", 
        "category":"flowchart", 
        "width":80, 
        "height":60, 
        "x":50, 
        "y":60  
    },
    { 
        "id":"3", 
        "name":"foo", 
        "type":"rectangle", 
        "category":"basic", 
        "width":180, 
        "height":20, 
        "x":50, 
        "y":260, 
        "fill":"#565623"  
    }
  ],
  "edges":[
    { "source":"1", "target":"3" }
  ]
}

```

The previous example shows nodes and edges - here's an example BPMN dataset, showing 2 groups, and how the `group` member is used to indicate which group a shape has as its parent:

```javascript
{
    "groups":[
        {
            "id":"g1",
            "type":"pool",
            "category":"bpmn2",
            "label":"BPMN Pool",
            "x":0,
            "y":0,
            "width":600,
            "height":250
        },
        {
            "id":"l1",
            "type":"lane",
            "label":"BPMN Lane",
            "category":"bpmn2",
            "x":0,
            "y":0,
            "width":600,
            "height":250
        }
    ],
    "nodes": [
        {
            "id":"1",
            "type":"gateway",
            "category":"bpmn2",
            "width":40,
            "height":40,
            "x":50,
            "y":60,
            "group":"l1"
        },
        {
            "id":"3",
            "type":"start-event",
            "category":"bpmn2",
            "width":40,
            "height":40,
            "x":50,
            "y":260,
            "fill":"#565623",
            "group":"l1"
        }
    ],
     "edges":[
        { "source":"1", "target":"3" }
    ]
}

```

## Loading JSON[​](#loading-json "Direct link to Loading JSON")

```javascript
diagram.load({
  url:"http://mydata.com?xyz"
});

```
