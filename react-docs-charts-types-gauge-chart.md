# Gauge Chart

The Gauge chart displays a single value within a defined range, often represented as a needle on a circular arc.

### Default Gauge[​](#default-gauge "Direct link to Default Gauge")

A gauge with no zones that shows the needle by default.

```jsx
import {GaugeChartComponent} from "@visuallyjs/browser-ui-react"

export default function MyChart() {

  const data = ...
  
  const options = {
  title: {
    text: "Default Gauge"
  },
  value: 65
}    
    
  return <GaugeChartComponent options={options} className="my-chart"/>
}

```

### Zones and Needle[​](#zones-and-needle "Direct link to Zones and Needle")

A gauge configured with multiple color zones and a needle.

```jsx
import {GaugeChartComponent} from "@visuallyjs/browser-ui-react"

export default function MyChart() {

  const data = ...
  
  const options = {
  title: {
    text: "Gauge with Zones and Needle"
  },
  value: 75,
  zones: [
    {
      from: 0,
      to: 33,
      color: "#ff4d4d"
    },
    {
      from: 33,
      to: 66,
      color: "#ffdb4d"
    },
    {
      from: 66,
      to: 100,
      color: "#4dff4d"
    }
  ]
}    
    
  return <GaugeChartComponent options={options} className="my-chart"/>
}

```

### Zones without Needle[​](#zones-without-needle "Direct link to Zones without Needle")

A gauge that has zones but doesn't show the needle. In this case, the zones are only painted up to the current value.

```jsx
import {GaugeChartComponent} from "@visuallyjs/browser-ui-react"

export default function MyChart() {

  const data = ...
  
  const options = {
  title: {
    text: "Gauge with Zones, No Needle"
  },
  value: 45,
  showNeedle: false,
  zones: [
    {
      from: 0,
      to: 100,
      color: "#4d94ff"
    }
  ]
}    
    
  return <GaugeChartComponent options={options} className="my-chart"/>
}

```

### Gradient Zones[​](#gradient-zones "Direct link to Gradient Zones")

A gauge with two zones that each have a gradient.

```jsx
import {GaugeChartComponent} from "@visuallyjs/browser-ui-react"

export default function MyChart() {

  const data = ...
  
  const options = {
  title: {
    text: "Gauge with Gradient Zones"
  },
  value: 80,
  zones: [
    {
      from: 0,
      to: 50,
      gradient: {
        stops: [
          {
            offset: 0,
            color: "#ff4d4d"
          },
          {
            offset: 100,
            color: "#ffdb4d"
          }
        ]
      }
    },
    {
      from: 50,
      to: 100,
      gradient: {
        stops: [
          {
            offset: 0,
            color: "#ffdb4d"
          },
          {
            offset: 100,
            color: "#4dff4d"
          }
        ]
      }
    }
  ]
}    
    
  return <GaugeChartComponent options={options} className="my-chart"/>
}

```

### Ticks[​](#ticks "Direct link to Ticks")

The `ticks` object allows you to configure the appearance and interval of the tick marks on the gauge.

```jsx
import {GaugeChartComponent} from "@visuallyjs/browser-ui-react"

export default function MyChart() {

  const data = ...
  
  const options = {
  title: {
    text: "Gauge with Custom Ticks"
  },
  value: 65,
  ticks: {
    interval: 10,
    show: true,
    width: 2,
    length: 10,
    color: "#666"
  }
}    
    
  return <GaugeChartComponent options={options} className="my-chart"/>
}

```

### Labels[​](#labels "Direct link to Labels")

The `labels` object is used to configure the numeric labels displayed around the gauge arc.

```jsx
import {GaugeChartComponent} from "@visuallyjs/browser-ui-react"

export default function MyChart() {

  const data = ...
  
  const options = {
  title: {
    text: "Custom Labels"
  },
  value: 45,
  labels: {
    show: true,
    fontSize: 14,
    fontWeight: "bold",
    fontColor: "#4d94ff"
  }
}    
    
  return <GaugeChartComponent options={options} className="my-chart"/>
}

```

## CSS Classes[​](#css-classes "Direct link to CSS Classes")

| Class                    | Description                                           |
| ------------------------ | ----------------------------------------------------- |
| `vjs-gauge-chart`        | Assigned to the container for a gauge chart           |
| `vjs-gauge-label`        | Assigned to each label element in a GaugeChart.       |
| `vjs-gauge-needle`       | Assigned to the needle element in a GaugeChart.       |
| `vjs-gauge-needle-pivot` | Assigned to the needle pivot element in a GaugeChart. |
| `vjs-gauge-tick`         | Assigned to each tick element in a GaugeChart.        |
| `vjs-gauge-track`        | Assigned to the track element in a GaugeChart.        |
| `vjs-gauge-zone`         | Assigned to each zone element in a GaugeChart.        |
