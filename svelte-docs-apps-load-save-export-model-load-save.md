# Model Data

## Loading data into the model[​](#loading-data-into-the-model "Direct link to Loading data into the model")

To load data into the model, use the `load` method on an instance of `VisuallyJs`. You can load data from a remote source - using ajax - or directly from an object in memory.

tip

For loading data it's usually more simple to load it straight into the `SurfaceComponent` (either as JS object or from a URL), rather than have to setup some code to run on load. See the [UI Load & Save](/svelte/docs/apps/load-save-export/ui-load-save.md) docs for details.

### Loading data via ajax[​](#loading-data-via-ajax "Direct link to Loading data via ajax")

```html
<script>
  import { SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
  import { onMount } from "svelte"

  let surfaceComponent

  onMount(() => {
    const surface = surfaceComponent.getSurface()
    const model = surface.model
    
   model.load({
     url:"someUrl.json",
     onload:() => {                
       // called after the data has loaded.	
     }
   })
  })
</script>

<SurfaceComponent bind:this={surfaceComponent}/>

```

In the example above, it is assumed that the data is in the default JSON format (discussed below). You can, however, instruct VisuallyJs that the data is in some other format, bv providing a `type` parameter:

```html
<script>
  import { SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
  import { onMount } from "svelte"

  let surfaceComponent

  onMount(() => {
    const surface = surfaceComponent.getSurface()
    const model = surface.model
    
   model.load({
     type:"hierarchicalJson",
     url:"someUrl.json",
     onload:() => {                
       // called after the data has loaded.	
     }
   })
  })
</script>

<SurfaceComponent bind:this={surfaceComponent}/>

```

#### Specifying HTTP Headers[​](#specifying-http-headers "Direct link to Specifying HTTP Headers")

By default, VisuallyJs will set the HTTP header `Accept` to the value `application/json`. You can override this by providing your own HTTP headers in the `load` call:

```html
<script>
  import { SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
  import { onMount } from "svelte"

  let surfaceComponent

  onMount(() => {
    const surface = surfaceComponent.getSurface()
    const model = surface.model
    
   model.load({
   type:"xml",
   url:"someUrl.xml",
   headers:{
     Accept:"text/xml",
     X-My-Header:"FOO"
   },
   onload:() => {                
     // called after the data has loaded.	
   }
   })
  })
</script>

<SurfaceComponent bind:this={surfaceComponent}/>

```

*Note*: if you provide `headers` you must set an `Accept` header (if you want it to be set), because VisuallyJs will not write a value for `Accept` into an HTTP headers object that does not have it.

### Loading data from memory[​](#loading-data-from-memory "Direct link to Loading data from memory")

```html
<script>
  import { SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
  import { onMount } from "svelte"

  let surfaceComponent

  onMount(() => {
    const surface = surfaceComponent.getSurface()
    const model = surface.model
    
   model.load({
   data:{
     nodes:[
       { id:"foo", value1:"foo", value2:34 },
       { id:"bar", value1:"bar", value2:24 }
     ],
     edges:[
       { source:"foo", target:"bar", data: { value1:89 } }
     ]
   })
  })
</script>

<SurfaceComponent bind:this={surfaceComponent}/>

```

In the example above, it is assumed that the data is in the default JSON format (discussed below). You can, however, instruct VisuallyJs that the data is in some other format, bv providing a `type` parameter. Here we specify `hierarchicalJson` (also discussed in the data formats section below):

```html
<script>
  import { SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
  import { onMount } from "svelte"

  let surfaceComponent

  onMount(() => {
    const surface = surfaceComponent.getSurface()
    const model = surface.model
    
   model.load({
     type:"hierarchicalJson",
     data:{
       "id":"rootNode",
       "children":[
         { "id":"childOne" }, { "id":"childTwo" }  
       ]
     }
   })
  })
</script>

<SurfaceComponent bind:this={surfaceComponent}/>

```

caution

The load method performs an incremental load: the existing data is not cleared when you call `load`. If you wish to replace the entire dataset, first call the `clear()` method. If you have not cleared the data when you reload some dataset, VisuallyJs will not load new items if an item of the given type with that id already exists, which is generally the case for nodes/groups, but often edges are not loaded with their own ids, and therefore on reload will be duplicated.

### Decorators[​](#decorators "Direct link to Decorators")

The default JSON parser (`json`) accepts an optional `parameters` object that allows you to specify "decorator" functions. These functions provide a way to modify or augment the data for nodes, groups, and edges as they are being loaded, before they are officially added to the model.

#### Specifying Decorators[​](#specifying-decorators "Direct link to Specifying Decorators")

You can pass these decorators within the `parameters` argument when calling the load/parse method:

* **`nodeDecorator(data: ObjectData)`**: Called for every node. It receives the raw node data.
* **`groupDecorator(data: ObjectData)`**: Called for every group. It receives the raw group data.
* **`edgeDecorator(data: ObjectData, sourceData: ObjectData, targetData: ObjectData)`**: Called for every edge. It receives the edge's data payload along with the resolved data objects for both the source and the target.

#### Example Usage[​](#example-usage "Direct link to Example Usage")

## Saving the model[​](#saving-the-model "Direct link to Saving the model")

You can either tell the VisuallyJs model to save data on demand - using the `save` function - or configure it to save automatically, whenever it detects that the data model has changed.

VisuallyJs uses an HTTP POST to save data. You cannot configure it to use anything other than a POST. If you absolutely do not want to use POST, then you can use the method described at the bottom of this page to export the data, then save it yourself.

### Save on demand[​](#save-on-demand "Direct link to Save on demand")

```javascript
model.save({
  type:"json",
  url:"http://foo.com",
  parameters:{ "foo":1, "bar":2 },
  success:(responseText) => { },
  error:(responseText, responseStatus) => { },
  headers:{ "Optional":"Http Headers"}
})

```

Here, as with the `load` function, the type of the dataset is assumed to be VisuallyJs's default JSON syntax (see below for an example of how to write a custom exporter).

The allowed parameters are:

* **type** By default this is set to "json". Specifies the data type in which to format the data. This must match the name of a registered exporter.
* **url** Required. URL to POST data to.
* **parameters** Optional parameters to pass to the exporter. If you write a custom exporter you may wish to use this.
* **success** Optional callback to execute once the data has saved successfully. The server response is provided to this callback, but note that it is provided as text: if your server responds with JSON you should use `JSON.parse(responseText)` to get the response as JSON.
* **error** Optional callback to execute if there was an error saving the data. Both the server response and the response status code are passed to this callback.
* **headers** Optional headers to set on the ajax request. By default, VisuallyJs will send a `Content-Type:"application/json"` header. If you provide your own headers this header will continue to be sent, unless of course you override it.

### Save Automatically[​](#save-automatically "Direct link to Save Automatically")

You can configure VisuallyJs to save automatically, either with its own ajax call, or by invoking a function you supply. The bare minimum setup requires the `autoSave` flag to be set, and then either a `saveUrl`:

```html
<script>
  import { SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
  const modelOptions = {
  autoSave: true,
  saveUrl: "http://foo.com"
}
</script>

<SurfaceComponent {modelOptions}/>

```

...or an `autoSaveHandler` function for VisuallyJs to invoke:

```html
<script>
  import { SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
  const modelOptions = {
  autoSave: true,
  autoSaveHandler: (model) => {

  }
}
</script>

<SurfaceComponent {modelOptions}/>

```

#### Methods that invoke a save[​](#methods-that-invoke-a-save "Direct link to Methods that invoke a save")

VisuallyJs will save the dataset whenever one of these methods is called:

* `addNode`
* `removeNode`
* `addNodes`
* `addGroup`
* `removeGroup`
* `addEdge`
* `removeEdge`
* `addPort`
* `addNewPort`
* `removePort`
* `updateNode`
* `updateGroup`
* `updateEdge`
* `updatePort`
* `addToGroup`
* `removeFromGroup`

note

The dataset will *not* be saved automatically when you call the `clear` method.

#### Debouncing save operations[​](#debouncing-save-operations "Direct link to Debouncing save operations")

If you find that having this switched on is causing too much network traffic due to rapid changes in the dataset, you can instruct VisuallyJs to "debounce" these requests - limit the rate at which save requests will be made, via the `autoSaveDebounceTimeout` constructor parameter:

```html
<script>
  import { SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
  const modelOptions = {
  autoSave: true,
  saveUrl: "http://foo.com",
  autoSaveDebounceTimeout: 1000
}
</script>

<SurfaceComponent {modelOptions}/>

```

This is a value in milliseconds.

#### Autosave Callbacks[​](#autosave-callbacks "Direct link to Autosave Callbacks")

You can supply callbacks for auto save success and error, as well as functions to run before and after an auto save operation. These functions are not invoked if you supply an `autoSaveHandler`, since VisuallyJs in that case does not perform the save operation itself.

```html
<script>
  import { SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
  const modelOptions = {
  autoSave: true,
  saveUrl: "http://foo.com",
  onAutoSaveError: (msg) => { ... },
  onAutoSaveSuccess: (response) => { ... },
  onBeforeAutoSave: () => { ... },
  onAfterAutoSave: () => { ... }
}
</script>

<SurfaceComponent {modelOptions}/>

```

#### Autosave HTTP Headers[​](#autosave-http-headers "Direct link to Autosave HTTP Headers")

To set headers as discussed [below](#setting-http-headers) when auto-saving, provide a `saveHeaders` object in VisuallyJs's model options.

These are only used when you supply a `saveUrl`. If you supply an `autoSaveHandler` these are ignored.

```html
<script>
  import { SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
  const modelOptions = {
  autoSave: true,
  saveUrl: "http://foo.com",
  saveHeaders: {
    X-My-Header: "My Header Value"
  }
}
</script>

<SurfaceComponent {modelOptions}/>

```

#### Content Type[​](#content-type "Direct link to Content Type")

VisuallyJs will, by default, set the `Content-Type` header on a save POST to:

```javascript
Content-Type:"application/json"

```

#### Specifying HTTP Headers[​](#specifying-http-headers-1 "Direct link to Specifying HTTP Headers")

You can set arbitrary headers (including to override `Content-Type`) via the `headers` parameter on a `save` call:

```javascript
model.save({
  url:"http://save-data.com",
  headers:{
    "X-My-Header":"headerValue"
  }
});

```

## Exporting[​](#exporting "Direct link to Exporting")

If you want to just export the data, you can do so from a `VisuallyJsModel` instance for the model data:

```javascript
const data = model.exportData();

```

This will assume you want the data in the default JSON syntax. If you have a custom exporter you wish to use, you can specify that using the `type` parameter. You can also pass in parameters for the export:

```javascript
const data = model.exportData({
  type:"myFormat",
  parameters:{
    importantNumber:34,
    somePrefix:"foo-"
  }
})

```

## Data formats[​](#data-formats "Direct link to Data formats")

### Default JSON[​](#default-json "Direct link to Default JSON")

The default data format used by VisuallyJs is a JS object containing `nodes`, `groups` and `edges`, defined by this interface:

VisuallyJsDefaultJSON

The default JSON format, consisting of optional lists of nodes, edges and groups.

| Name    | Type                 | Description     |
| ------- | -------------------- | --------------- |
| edges?  | Array<[EdgeData]()>  | List of edges.  |
| groups? | Array<[GroupData]()> | List of groups. |
| nodes?  | Array<[NodeData]()>  | List of nodes.  |

An example might be:

```javascript
{
    "nodes":[
        {
            "id":"someId",
            "key":"value",
            "left":50,
            "top":150
        },
        {
            "id":"someOtherId",
            "key":"value",
            "left":250,
            "top":150
        },
        {
            "id":"anotherId",
            "key":"value",
            "left":250,
            "top":150,
            "group":"groupOne"
        }
    ], 
    "groups":[
        {
            "id":"groupOne",
            "key":"value",
            "left":450,
            "top":250
        }
    ],
    "edges":[
        { "source":"someId", "target":"someOtherId" }
    ]
}

```

Not every dataset will contain `groups` - or even `edges`, in fact.

### Hierarchical JSON[​](#hierarchical-json "Direct link to Hierarchical JSON")

This is an alternative JSON format that is useful for some datasets. Edges are not described in this format: there is implicitly an edge from each node to each of its children. An example:

```javascript
{
    "id":"someId",
    "key":"value",
    "children":[
        {
            "id":"someOtherId",
            "children":[
                {
                    "id":"aThirdId"
                },
                {
                    "id":"aFourthId"
                }
            ]
        }
    ]
}

```

VisuallyJsHierarchicalJSON

The Hierarchical JSON format. Consists of a single root entry, which has a children array, each of which may have children, etc.

`VisuallyJsHierarchicalJSONEntry`
