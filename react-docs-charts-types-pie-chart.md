# Pie Chart

Pie charts show proportions of a whole by dividing a circle into slices.

```jsx
import {PieChartComponent} from "@visuallyjs/browser-ui-react"

export default function MyChart() {

  const data = ...
  
  const options = {
  title: {
    text: "Fuel Consumption"
  },
  series: [
    {
      valueField: "value",
      label: "Fuel Type"
    }
  ]
}    
    
  return <PieChartComponent options={options} className="my-chart"/>
}

```

The data loaded into this example is:

```javascript
const data = [
    { id: 'Petrol', value: 938899 },
    { id: 'Diesel', value: 1229600 },
    { id: 'Electricity', value: 325251 },
    { id: 'Other', value: 238751 }
]

```

Each entry in the array is represented as a slice of the pie, with its value being extracted from whatever field you map as the `valueField` - in this case, `"value"`.

### Selected Slice[​](#selected-slice "Direct link to Selected Slice")

You can set the selected slice of the pie using the `selectedCategory` option. Setting `interactive: true` allows users to select different slices.

```jsx
import {PieChartComponent} from "@visuallyjs/browser-ui-react"

export default function MyChart() {

  const data = ...
  
  const options = {
  title: {
    text: "Fuel Consumption"
  },
  subtitle: {
    text: "Comparison of sources"
  },
  selectedCategory: 0,
  interactive: true,
  series: [
    {
      valueField: "value",
      label: "Fuel Type"
    }
  ]
}    
    
  return <PieChartComponent options={options} className="my-chart"/>
}

```

## Doughnut Charts[​](#doughnut-charts "Direct link to Doughnut Charts")

You can create a doughnut chart by specifying an `innerRadius`. The format of the value is that it is a fraction of the total radius (between 0 and 1). The chart will not throw an error if you provide a value outside that range.

```jsx
import {PieChartComponent} from "@visuallyjs/browser-ui-react"

export default function MyChart() {

  const data = ...
  
  const options = {
  innerRadius: 0.55,
  series: [
    {
      valueField: "value",
      label: "Fuel Type"
    }
  ]
}    
    
  return <PieChartComponent options={options} className="my-chart"/>
}

```

## Labels[​](#labels "Direct link to Labels")

The `showLabels` config option determines what information is displayed on the chart labels. It has five possible values:

### label[​](#label "Direct link to label")

Displays the label of the slice.

```jsx
import {PieChartComponent} from "@visuallyjs/browser-ui-react"

export default function MyChart() {

  const data = ...
  
  const options = {
  showLabels: "label",
  series: [
    {
      valueField: "value",
      label: "Fuel Type"
    }
  ]
}    
    
  return <PieChartComponent options={options} className="my-chart"/>
}

```

### value[​](#value "Direct link to value")

Displays the numeric value of the slice.

```jsx
import {PieChartComponent} from "@visuallyjs/browser-ui-react"

export default function MyChart() {

  const data = ...
  
  const options = {
  showLabels: "value",
  series: [
    {
      valueField: "value",
      label: "Fuel Type"
    }
  ]
}    
    
  return <PieChartComponent options={options} className="my-chart"/>
}

```

### percentage[​](#percentage "Direct link to percentage")

Displays the percentage of the whole that the slice represents.

```jsx
import {PieChartComponent} from "@visuallyjs/browser-ui-react"

export default function MyChart() {

  const data = ...
  
  const options = {
  showLabels: "percentage",
  series: [
    {
      valueField: "value",
      label: "Fuel Type"
    }
  ]
}    
    
  return <PieChartComponent options={options} className="my-chart"/>
}

```

### label-value[​](#label-value "Direct link to label-value")

Displays both the label and the value of the slice.

```jsx
import {PieChartComponent} from "@visuallyjs/browser-ui-react"

export default function MyChart() {

  const data = ...
  
  const options = {
  showLabels: "label-value",
  series: [
    {
      valueField: "value",
      label: "Fuel Type"
    }
  ]
}    
    
  return <PieChartComponent options={options} className="my-chart"/>
}

```

### label-percentage[​](#label-percentage "Direct link to label-percentage")

Displays both the label and the percentage of the slice.

```jsx
import {PieChartComponent} from "@visuallyjs/browser-ui-react"

export default function MyChart() {

  const data = ...
  
  const options = {
  showLabels: "label-percentage",
  series: [
    {
      valueField: "value",
      label: "Fuel Type"
    }
  ]
}    
    
  return <PieChartComponent options={options} className="my-chart"/>
}

```

## Label Position[​](#label-position "Direct link to Label Position")

The `labelPosition` config option determines where the labels are placed relative to the slices.

### Outside[​](#outside "Direct link to Outside")

This is the default, which places the labels outside of the slices of pie.

```jsx
import {PieChartComponent} from "@visuallyjs/browser-ui-react"

export default function MyChart() {

  const data = ...
  
  const options = {
  showLabels: "label",
  labelPosition: "outside",
  series: [
    {
      valueField: "value",
      label: "Fuel Type"
    }
  ]
}    
    
  return <PieChartComponent options={options} className="my-chart"/>
}

```

### Inside[​](#inside "Direct link to Inside")

When you set `labelPosition:"inside"`, labels are placed at 0.7 of the radius of the pie:

```jsx
import {PieChartComponent} from "@visuallyjs/browser-ui-react"

export default function MyChart() {

  const data = ...
  
  const options = {
  showLabels: "label",
  labelPosition: "inside",
  series: [
    {
      valueField: "value",
      label: "Fuel Type"
    }
  ]
}    
    
  return <PieChartComponent options={options} className="my-chart"/>
}

```

## Label font[​](#label-font "Direct link to Label font")

You can specify details for the font to use in a pie chart's labels via the `labelFont` option:

```jsx
import {PieChartComponent} from "@visuallyjs/browser-ui-react"

export default function MyChart() {

  const data = ...
  
  const options = {
  labelFont: {
    size: 14,
    weight: "bold"
  },
  series: [
    {
      valueField: "value",
      label: "Fuel Type"
    }
  ]
}    
    
  return <PieChartComponent options={options} className="my-chart"/>
}

```

This is of type [FontSpec]().

## Summing data[​](#summing-data "Direct link to Summing data")

A common use case for pie charts is to sum the data prior to plotting. For example, consider this dataset:

```javascript
const summingData = [
    { name: 'record1', red: 4, green: 2, blue: 3 },
    { name: 'record2', red: 5, green: 2, blue: 3 },
    { name: 'record3', red: 1, green: 2, blue: 3 }
]

```

It consists of 3 records, each of which has a name and a `red`, `green` and `blue` value. To create a pie chart which shows the sum of each of these, we use a [summing series](/react/docs/charts/concepts/series.md#summing-series):

```jsx
import {PieChartComponent} from "@visuallyjs/browser-ui-react"

export default function MyChart() {

  const data = ...
  
  const options = {
  series: [
    {
      type: "summing",
      fields: [
        "red",
        "green",
        "blue"
      ]
    }
  ]
}    
    
  return <PieChartComponent options={options} className="my-chart"/>
}

```

## Assigning Colors[​](#assigning-colors "Direct link to Assigning Colors")

To assign colors in a Pie chart, you have four options:

* Do nothing. You will get a randomly generated color for each slice of pie.
* The `defaultColor` option from `BaseChartOptions` allows you to specify a color that will be used for every slice of the pie.
* The `colors` option in `PieChartOptions` allows you to specify a list of colors to be used for the slices of the pie.
* The `colorGenerator` option gives you finer-grained control over what color will be assigned to each slice.

### Default color[​](#default-color "Direct link to Default color")

```jsx
import {PieChartComponent} from "@visuallyjs/browser-ui-react"

export default function MyChart() {

  const data = [
    {name:"record1",red:4,green:2,blue:3},
     {name:"record2",red:5,green:2,blue:3},
     {name:"record3",red:1,green:2,blue:3}
]
  
  const options = {
  defaultColor: "forestgreen",
  series: [
    {
      type: "summing",
      fields: [
        "red",
        "green",
        "blue"
      ]
    }
  ]
}    
    
  return <PieChartComponent options={options} className="my-chart" data={data}/>
}

```

### List of colors[​](#list-of-colors "Direct link to List of colors")

```jsx
import {PieChartComponent} from "@visuallyjs/browser-ui-react"

export default function MyChart() {

  const data = [
    {name:"record1",red:4,green:2,blue:3},
     {name:"record2",red:5,green:2,blue:3},
     {name:"record3",red:1,green:2,blue:3}
]
  
  const options = {
  colors: [
    "#FF0000",
    "#00FF00",
    "#0000FF"
  ],
  series: [
    {
      type: "summing",
      fields: [
        "red",
        "green",
        "blue"
      ]
    }
  ]
}    
    
  return <PieChartComponent options={options} className="my-chart" data={data}/>
}

```

In a `summing` series, the order of the `fields` array directly matches the order of the `colors` array. This makes it straightforward to assign specific colors to specific data fields:

However, for a `collation` series, the order in which values are encountered in the dataset determines the order of the slices. Because this order can be unpredictable, matching a `colors` array to specific values in a `collation` series can be hit and miss, and you're better off using the `colorGenerator` option.

### Color Generators[​](#color-generators "Direct link to Color Generators")

This is a function that returns a color for a given index or data point, providing more flexibility in how colors are assigned. You can provide this either as your own ad-hoc function, or use one of the color generators [that VisuallyJS ships with](/react/docs/charts/concepts/colors.md#color-generators).

```typescript
const chartOptions = {
    // ... other options
    colorGenerator: {
        // return a color based on the data
        generate:(point:PieChartDataPoint) => point.data.color
    }
}

```

PieChartDataPoint

Defines the data point type used in a PieChart. The object that is passed to a color generator is of this type.

{

<br />

  arc:number,

<br />

  arcStart:number,

<br />

  data:[ObjectData](),

<br />

  label:string,

<br />

  p:number,

<br />

  value:number

<br />

}

## CSS Classes[​](#css-classes "Direct link to CSS Classes")

| Class                    | Description                                       |
| ------------------------ | ------------------------------------------------- |
| `vjs-pie-chart`          | CSS class set on a pie chart.                     |
| `vjs-pie-slice`          | CSS class set on a slice in a pie chart.          |
| `vjs-pie-slice-selected` | CSS class set on a selected slice in a pie chart. |
