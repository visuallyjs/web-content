# Series

Charts display data sourced from one or more data series. VisuallyJs supports several types of data series:

* [RecordBasedSeries](#recordbased-series) In which the data is stored in a list of objects, and values are extracted from these objects via key names that you specify;
* [ArrayBasedSeries](#arraybased-series) In which the data is stored in an array inside some object. This type of series is what you'll use when you want to plot time-based information;
* [CollationSeries](#collation-series) In which occurrences of a specific field's values are counted;
* [SummingSeries](#summing-series) In which values from multiple fields in each data object are summed;
* [SummingCollationSeries](#summing-collation-series) In which records are grouped by the occurrence of some specific field, whose value is then summed per group.

## RecordBased series[​](#recordbased-series "Direct link to RecordBased series")

Data in a `RecordBasedSeries` is stored in a list of objects, each of which contains the data for some specific category in the chart. The number of records in the list corresponds to the number of categories in the chart. Each record in the list can be used as the datasource for multiple series, by defining multiple series with different value fields.

For example, consider a dataset containing population statistics for various countries, where the value for each year is a separately keyed value in the data for each country:

```javascript
[
    {
        id:"uk",
        "2010":62.8,
        "2011":63.5,
        "2012":63.7
    },
    {
        id:"ca",
        "2010":34,
        "2011":34.4,
        "2012":34.7
    }
]

```

We can create a chart of this by specifying a series for each year:

```javascript
const chartOptions = {
    series:[
        {
            valueField:"2010",
            label:"2010"
        },
        {
            valueField:"2011",
            label:"2011"
        },
        {
            valueField:"2012",
            label:"2012"
        }
    ],
    valueAxis:{
        title:{
            text:"Millions of inhabitants"
        }
    },
    title:{
        text:"Population growth"
    },
    subtitle:{
        text:"Source: https://macrotrends.net",
    }
}

```

VisuallyJs will, by default, use the `id` field of each object in this list to identify a category. In the dataset above we have used the ISO country code as the ID, so we see `uk` and `ca` as the category labels - for a discussion of axes, and how to label them, take a look at [the documentation for Axes](/vue/docs/charts/charts/concepts/axes).

## ArrayBased series[​](#arraybased-series "Direct link to ArrayBased series")

In an `ArrayBasedSeries`, data is stored in an array inside some object. The individual values from the array are used as the category values, ie. the number of entries in the array corresponds to the number of entries in the category axis. Each individual object represents a separate series.

This dataset demonstrates the structure. We are modelling the change of population across a few years:

```javascript
[
    {
        id:"uk",
        values:[55, 57, 59]
    },
    {
        id:"ca",
        values:[24, 26, 29]
    }
]

```

VisuallyJs assumes a data series is object based by default, so we need to instruct it that we're using an array based series:

```javascript
const chartOptions = {
    series:[
        {
            type:"array",
            startPoint:2010,
            step:1
        }
    ]
}

```

Here, we have specified `type` to be `"array"`, and we also provided:

* `startPoint` Tells VisuallyJs the number corresponding to the first entry in the list of values. In this case we have specified the year 2010. If you do not provide this, VisuallyJs will use a default value of 0.
* `step` As shown above, this is optional, and defaults to 1. It tells VisuallyJs how much to increment the label by for each value.

### Providing labels[​](#providing-labels "Direct link to Providing labels")

In the above example the labels for our data were numeric and increased at a constant rate. We provided a `startPoint` of 2010, and the chart incremented this value by one for each subsequent data point after the first one. This is fine for many types of numeric data, but it's not always what you want, and so there are a couple of ways you can provide your own labels array instead, in a series definition:

#### In a list[​](#in-a-list "Direct link to In a list")

The series definition can contain an array of strings that are the labels for the data points.

```javascript

chartOptions = {
    ...,
    series:[
        {
            type:"array",
            labels:["Year 1", "Year 2", "Year 3"]
        }
    ],
    ...
}

```

It is expected that the length of the `labels` array matches the values array in your data.

#### Via a function[​](#via-a-function "Direct link to Via a function")

You can also provide a `labelGenerator` function:

```javascript

chartOptions = {
    ...,
    series:[
        {
            type:"array",
            labelGenerator:(index, data) => {
                return `Label ${index}`    
            }
        }
    ],
    ...
}

```

This is the most flexible option, as it allows you complete control over the labels that are displayed.

## Collation series[​](#collation-series "Direct link to Collation series")

A `CollationSeries` is used to count the occurrences of specific values within a dataset. This is particularly useful for Pie charts where you want to show the distribution of a certain attribute across your data.

For example, given a list of people with a `meal` attribute:

```javascript
const collatingData = [
    { name: 'Marek', meal: "pizza" },
    { name: 'Dalek', meal: "pasta" },
    { name: 'John', meal: "pasta" },
    { name: 'Sue', meal: "steak" },
    { name: 'Andrew', meal: "steak" },
    { name: 'Juanita', meal: "pasta" },
    { name: 'Boris', meal: "pizza" },
]

```

You can create a Pie chart that shows the count of each meal preference by using a series of type `"collation"`:

```javascript
const chartOptions = {
    data: collatingData,
    series: [
        {
            type: "collation",
            valueField: "meal"
        }
    ]
}

```

VisuallyJs will count the occurrences of each value in the `color` field and use these counts as the values for the chart segments.

## Summing series[​](#summing-series "Direct link to Summing series")

A `SummingSeries` allows you to aggregate values from multiple fields within each data object. This is another great option for Pie charts when your data is structured such that each record contains multiple values that you want to compare as part of a whole.

Consider a dataset where each record represents a set of values:

```javascript
const summingData = [
    { name: 'record1', red: 4, green: 2, blue: 3 },
    { name: 'record2', red: 5, green: 2, blue: 3 },
    { name: 'record3', red: 1, green: 2, blue: 3 }
]

```

You can create a Pie chart that shows the total sum of each field across all records:

```javascript
const chartOptions = {
    data: summingData,
    colors: ["#FF0000", "#00FF00", "#0000FF"],
    series: [
        {
            type: "summing",
            fields: ["red", "green", "blue"]
        }
    ]
}

```

In this example, VisuallyJs will sum the `red`, `blue`, and `green` fields across all objects in `summingData` and display the totals in the Pie chart.

## Summing Collation series[​](#summing-collation-series "Direct link to Summing Collation series")

A `SummingCollationSeries` combined the grouping from a collation series with summing.

For example, let's add a `qty` field to the list of people with a `meal` attribute that we used in the collation series above:

```javascript
const summingCollatingData = [
    { name: 'Marek', meal: "pizza", qty:5 },
    { name: 'Dalek', meal: "pasta", qty:3 },
    { name: 'John', meal: "pasta", qty:4 },
    { name: 'Sue', meal: "steak", qty:2 },
    { name: 'Andrew', meal: "steak", qty:1 },
    { name: 'Juanita', meal: "pasta", qty:4 },
    { name: 'Boris', meal: "pizza", qty:1 },
]

```

You can create a Pie chart that first groups the record by `meal`, and then sums the `qty` for each meal:

```javascript
const chartOptions = {
    data: summingCollatingData,
    series: [
        {
            type: "summing-collation",
            categoryField: "meal",
            sumField:"qty"
        }
    ]
}

```
