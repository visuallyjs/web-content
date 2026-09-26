# Templating

This page provides a reference for VisuallyJs's internal template engine. You'll use this template engine:

* to write shapes for a shape set in a diagram;
* to write custom marker SVG for charts that support them;
* if you're using Vanilla VisuallyJs - to write templates for your nodes and groups.

<!-- -->

### Template format[​](#template-format "Direct link to Template format")

* Format is **strict** XHTML: *all* tags must be closed. This means:

```html
<input type="text"></input>

```

for example.

* Use **only double quotes** for attributes:

```html
<div class="foo"></div>

```

*not*

```html
<div class='foo'></div>

```

Inside attribute values, however, you can use single quotes:

```html
<r-if test="value == 'foo'">...</r-if>

```

***

### Limitations[​](#limitations "Direct link to Limitations")

Your templates must return a *single root node*. If you return multiple nodes, VisuallyJs will use the first node only.

***

### Interpolating values[​](#interpolating-values "Direct link to Interpolating values")

To extract some value from a node/group that a given template is rendering, use this syntax:

```html
<h1>{{name}}</h1>

```

So for some node with this dataset:

```javascript
{
    name:"My Node"
}

```

You'd get this output:

```html
<h1>My Node</h1>

```

#### Values within attributes[​](#values-within-attributes "Direct link to Values within attributes")

The template engine will extract values from the dataset within attributes, with some limitations. Let's enhance the heading example from above with a title attribute:

```html
<h1 aria-label="{{title}}" title="{{title}}">{{name}}</h1>

```

So for some node with this dataset:

```javascript
{
    name:"My Node",
    title:"This is the name of the node"
}

```

You'd get this output:

```html
<h1 aria-label="This is the name of the node" title="This is the name of the node">My Node</h1>

```

##### Limitations[​](#limitations-1 "Direct link to Limitations")

You can use basic math inside an attribute value, for instance:

```html
<div>
    <svg:svg width="{{width}}" height="{{height}}">
        <svg:circle cx="{{width / 2}}" cy="{{height / 2}}" rx="{{width / 2}}" ry="{{height / 2}}"
    </svg:svg>
</div>

```

These expressions can include parentheses:

```html
<div>
    <svg:svg width="{{width}}" height="{{height}}">
        <svg:circle cx="{{(width-10) / 2}}" cy="{{(height-10) / 2}}" rx="{{(width-10) / 2}}" ry="{{(height-10) / 2}}"
    </svg:svg>
</div>

```

what you cannot do, though, is eval arbitrary Javascript:

```html
<div>
    <svg:svg width="{{width}}" height="{{height}}">
        <svg:circle cx="{{calcCenterX(width)}}" cy="{{calcCenterHeight(height)}}" rx="{{calcRx(width)}}" ry="{{calcRy(height)}}"
    </svg:svg>
</div>

```

This will **not** work. You can use [macros](#template-macros) to insert computed values.

***

### Rendering SVG[​](#rendering-svg "Direct link to Rendering SVG")

To render SVG elements you must prefix the tag with a namespace:

```xml
<svg:svg width="50" height="50">
  <svg:rect x="10" y="10" width="10" height="10"></svg:rect>
</svg:svg>

```

This is due to the fact that the templating code uses `createElementNS` to create elements.

***

### Updating Data[​](#updating-data "Direct link to Updating Data")

Given this template for some node type:

```xml
<div class="someNode">
    <span>{{title}}</span>
    <ul>    
        <r-each in="someDataMember">
            <li>{{id}}</li>
        </r-each>
    </ul>
</div>

```

and this call to a VisuallyJs instance:

```javascript
const node = model.addNode({
  title:"FOO",
  someDataMember:[
    { id:"one" },
    { id:"two" },
    { id:"three" }
  ]
});

```

You'll get a node element with a `span` that says `FOO`, and a list of three items: `one`, `two` and `three`.

Calling `updateNode` on the VisuallyJs instance associated with this node:

```javascript
model.updateNode(node, {
   title:"FOO-NEW",
   someDataMember:[
       { id:"un" },
       { id:"deux" },
       { id:"trois" }
   ]
});

```

will result in a node element with a `span` that says `FOO-NEW`, and a list of three items: `un`, `deux` and `trois`.

#### Updating the `class` attribute[​](#updating-the-class-attribute "Direct link to updating-the-class-attribute")

VisuallyJs **won't update the class attribute** once a template has been written. Since the `update` method can only write values for classes that were in the template, there's a risk that any classes added by other parts of your app would be removed. For example say you have this template:

```html
<div class="{{nodeType}}">
  FOO
</div>

```

If you render this with `{nodeType:"start-node"}` then you'd end up with a `div` with class `start-node`. Then say some code comes along and does this:

```javascript
myDiv.classList.add("selected");

```

Now you've got a `div` with class `start-node selected`. If you then called `update`, VisuallyJs would re-write the class attribute to have only the `nodeType` class; probably not at all what you want. In this scenario you are better off using [attribute selectors](https://css-tricks.com/attribute-selectors/).

***

### Template Macros[​](#template-macros "Direct link to Template Macros")

These are a means for you to inject values into your templates that require computation at runtime. You indicate to the template engine that you wish to invoke a macro by prefixing the value to interpolate with a hash. A slightly more convoluted version of the above example:

```html
<script type="jtk" id="tmplTable">
    <div data-id="{{id}}">
        <h1>{{#truncatedId}}</h1>
        <p>{{content}}</p>
        <p>{{#concatTags}}</p>
    </div>
</script>

```

We use two macros here:

```javascript
model.render(someElement, {
    templateMacros:{
        truncatedId:(data) => data.id.substring(0, 5),
        concatTags:(data) => data.tags.join(" ")
    }
})

```

The `data` argument passed in to each macro is the vertex's backing data. For example, for this setup, we might have this payload:

```json
{
  "id": "78947329843h2hjlkshkfasd789",
  "content": "Loretta ipsum",
  "tags": [ "foo", "bar", "qux"]
}

```

***

### Tag reference[​](#tag-reference "Direct link to Tag reference")

##### Each[​](#each "Direct link to Each")

###### With objects in an array[​](#with-objects-in-an-array "Direct link to With objects in an array")

```javascript
{
  someDataMember:[
    { id:"one", label:"value1" },
    { id:"two", label:"value2" }
  ]

```

```html
<ul>
    <r-each in="someDataMember">
        <li id="{{id}}">{{label}}</li>
    </r-each>
</ul>    

```

###### With Arrays in an Array[​](#with-arrays-in-an-array "Direct link to With Arrays in an Array")

```javascript
{
  someDataMember:[
    [ "one", "value1" ],
    [ "two", "value2" ]
  ]

```

```html
<ul>
    <r-each in="someDataMember">
        <li id="{{$value[0]}}">{{$value[1]}}</li>
    </r-each>
</ul>    

```

The point to note here is that the current array is exposed as the variable `$value`.

###### With an Object[​](#with-an-object "Direct link to With an Object")

```javascript
{
  someData : {
    id:"foo",
    label:"FOO is the label",
    active:true,
    count:14
  }

```

```html
<table>
  <r-each in="someData">
    <tr><td>{{$key}}</td><td>{{$value}}</td></tr>
  </r-each>
</table>

```

The point to note here is that each entry is presented to the template as an object with `$key` and `$value` members.

###### Uniquely identifying child nodes[​](#uniquely-identifying-child-nodes "Direct link to Uniquely identifying child nodes")

In some cases you might want to use the `r-each` element to loop through your data and add ports to your nodes. For instance:

```html
<ul class="table-columns">
    <r-each in="columns" key="id">
        <r-tmpl id="tmplColumn"/>
    </r-each>
</ul>

```

This is how the schema builder application renders the columns in a table. `tmplColumn` looks kind of like this:

```html
<script type="jtk" id="tmplColumn">
  <li class="table-column table-column-type-{{datatype}}" primary-key="{{primaryKey}}" data-vjs-port-id="{{id}}">
    
    ...
       
    
  </li>
</script>

```

with some details removed for brevity. The thing to note is that this template, which is looped over, generates ports for the node. Note the `key` attribute on the `r-each` element above. It instructs VisuallyJs on how to get a unique identifier for each value in the loop. Thus, if you change the data in some port, VisuallyJs will just update the port's element, since it can use the `key` property to identify the existing element. Similarly, if you add a new port, VisuallyJs will use the `key` to determine that it has no current element, and if you remove a port, VisuallyJs will use the `key` to determine that the element corresponding to that port is no longer needed, and will remove it.

VisuallyJs will log a message to the console any time the `r-each` element is used without a `key`. If you do not supply a `key` then VisuallyJs will not be able to perform an update of the loop.

##### If[​](#if "Direct link to If")

Inline `{{if ...}}` statements in attributes are not supported.

###### Existence[​](#existence "Direct link to Existence")

```html
<r-if test="someObjectRef">
    <div>hola</div>
</r-if>

```

An existence test will be evaluated according to Javascript's "falsy" rules. If you are unfamiliar with falsiness in Javascript, you might like to [take a look here](https://developer.mozilla.org/en-US/docs/Glossary/Falsy)

###### Expressions[​](#expressions "Direct link to Expressions")

```html
<r-if test="foo == 5">
    <div>hola</div>
</r-if>

```

Expressions are limited by the following rules:

* the only comparators supported are `==`, `===`, `<=`, `<`, `>`, `>=`
* javascript expressions are not supported (eg `someMethod(foo) == 5`)

##### Comments[​](#comments "Direct link to Comments")

Comments follow the standard XHTML syntax:

```xml
<div>
<!--
    a comment
    <span>Maybe some code was commented</span>
-->
</div>

```

Comments are stored in the parse tree for a template. This may or may not prove useful.

##### Embedding HTML[​](#embedding-html "Direct link to Embedding HTML")

By default VisuallyJs templates treat text as plain text.

##### Nested Templates[​](#nested-templates "Direct link to Nested Templates")

###### With specific context[​](#with-specific-context "Direct link to With specific context")

```html
<div>
  <r-tmpl id="nested" context="someItem"></r-tmpl>
</div>

```

###### Inheriting parent context[​](#inheriting-parent-context "Direct link to Inheriting parent context")

```html
<div>
  <r-tmpl id="nested"></r-tmpl>
</div>

```

The difference between these two examples is that in the first, an item called `someItem` is extracted from the current dataset, and passed in to the `nested` template, whereas in the second, the `nested` template is passed the exact same data that the parent is currently using to render itself.

###### Inside an r-each loop[​](#inside-an-r-each-loop "Direct link to Inside an r-each loop")

```html
<div>
    <r-each in="someList">
        <r-tmpl id="nested"></r-tmpl>
    </r-each>
</div>

```

This is similar to the example immediately above - the nested template inherits its parent's context, but in this case the parent's context is currently some item from the list. You can also use `context` in this situation:

```html
<div>
    <r-each in="someList">
        <r-tmpl id="nested" context="someMemberOfTheListItem"></r-tmpl>
    </r-each>
</div>

```

The context for the nested element here is the `someMemberOfTheListItem` member of each list item.

###### With complex context[​](#with-complex-context "Direct link to With complex context")

You are not limited to extracting single variables from the current context to pass in to a nested template. You can specify a complex object too:

```html
<div>
  <r-tmpl id="nested" context="{id:foo, label:'Hello'}"/>
</div>

```

In this example, `foo` will be extracted from the context in which the current template is executing, and `Hello` is a hardcoded string.

###### Accessing nested properties[​](#accessing-nested-properties "Direct link to Accessing nested properties")

You can also specify properties that are nested inside the current context, either with dotted notation:

```html
<div>
  <r-tmpl id="nested" context="{id:record.id, label:'Hello'}"/>
</div>

```

or by naming the property:

```html
<div>
  <r-tmpl id="nested" context="{id:record['id'], label:'Hello'}"/>
</div>

```

###### Dynamic Template Names[​](#dynamic-template-names "Direct link to Dynamic Template Names")

You can lookup the name of a nested template at runtime, for example consider these templates:

```html
<script type="jtk" id="someTemplate">
    <h3>{{title}}</h3>
    <r-tmpl lookup="{{nestedId}}" default="def"/>
</script>

<script type="jtk" id="green">
    <h3>GREEN</h3>
</script>

```

Here we see the ID of the nested template is derived from the `nestedId` property of the data we are rendering:

```javascript
{
    title:"example",
    nestedId:"green"
}

```

`default` allows you to provide the ID of a template to use if the lookup fails.
