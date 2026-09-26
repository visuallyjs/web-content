# Loading and saving

Getting data into and out of VisuallyJs is easy. There are a few different approaches you can use:

* You can load/save to/from the underlying model directly, either using JS objects or via ajax. When you do this the dataset consists of just the nodes, edges and groups in your model, without any UI specific information such as the current state of the pan, zoom etc. Loading and saving to/from the model is discussed [here](/vue/docs/apps/load-save-export/model-load-save.md)

* You can supply an initial dataset or URL to load data into certain UI components - read more here]\(component-load)

* The `Surface` component offers `exportData`, `load` and `save` methods which export/load/save the dataset as well as the pan/zoom of the Surface, plus any context for attached inspectors.

### Appending Data[​](#appending-data "Direct link to Appending Data")

Data can be appended via the `load` method, since it does not cause the underlying Graph to be cleared.

## Data Formats[​](#data-formats "Direct link to Data Formats")

VisuallyJs ships with support for two JSON formats for loading and saving data. Should you need to, you can create custom load/save handlers for your own syntax.

### Graph JSON Syntax[​](#graph-json-syntax "Direct link to Graph JSON Syntax")

This JSON syntax - the default - consists of a JSON object with an array for `nodes`, `groups` and `edges`. All of these are optional, but of course if you declare an edge then the nodes/groups for that edge must be present in the dataset.

#### Example: Nodes and Edges[​](#example-nodes-and-edges "Direct link to Example: Nodes and Edges")

```javascript
{
  "nodes": [
    { id:"1", name:"foo"  },
    { id:"2", name:"baz"  },
    { id:"3", name:"foo"  },
    { id:"4", name:"ding" },
    { id:"5", name:"dong" },
    { id:"6", name:"ping" },
    { id:"7", name:"pong" }
  ],
  "edges":[
    { source:"1", target:"2" },
    { source:"1", target:"3" },
    { source:"2", target:"4" },
    { source:"2", target:"5" },
    { source:"3", target:"6" },
    { source:"3", target:"7" }                
  ]
}

```

#### Example: Groups, Nodes and Edges[​](#example-groups-nodes-and-edges "Direct link to Example: Groups, Nodes and Edges")

```javascript
{
  "groups":[
    { "id":"group1", name:"Group One" },
    { "id":"group2", name:"Group Two" }
  ],
  "nodes": [
    { id:"1", name:"foo", group:"group1"  },
    { id:"2", name:"baz"  },
    { id:"3", name:"foo"  },
    { id:"4", name:"ding", group:"group2" },
    { id:"5", name:"dong", group:"group2" },
    { id:"6", name:"ping" },
    { id:"7", name:"pong" }
  ],
  "edges":[
    { source:"1", target:"2" },
    { source:"1", target:"3" },
    { source:"2", target:"4" },
    { source:"2", target:"5" },
    { source:"3", target:"6" },
    { source:"3", target:"7" }                
  ]
}

```

#### Loading Graph JSON[​](#loading-graph-json "Direct link to Loading Graph JSON")

```javascript
model.load({
  type:"json",
  url:"http://mydata.com?xyz"
});

```

Since Graph JSON is the default syntax, you can in fact omit the `type` parameter in the above example:

```javascript
model.load({
  url:"http://mydata.com?xyz"
});

```

### Hierarchical JSON Syntax[​](#hierarchical-json-syntax "Direct link to Hierarchical JSON Syntax")

This JSON syntax represents hierarchical data, in which every node may have zero or more child nodes. It is assumed that there is an edge between a node and each of its child nodes. Note that the `children` member on each node's data is optional.

```javascript
{
  "id":"foo",
  "name":"FOO!",
  "children":[
    {
      "id":"bar",
      "name":"BAR!",
      "children":[
        {
          "id":"baz",
          "name":"BAZ!"
        }
      ]
    },
    {
      "id":"qux",
      "name":"QUX!"
    }
  ]
}

```

#### Loading Hierarchical JSON[​](#loading-hierarchical-json "Direct link to Loading Hierarchical JSON")

```javascript
model.load({
  type:"hierarchical-json",
  url:"http://myhierarchicaldata.com?xyz"
});

```

***
