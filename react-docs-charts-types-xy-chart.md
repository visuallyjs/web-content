# XY Chart

XY charts are base charts containing an X and a Y axis, one of which displays chart categories and the other values.

## Example[​](#example "Direct link to Example")

```jsx
import {XYChartComponent} from "@visuallyjs/browser-ui-react";

export default function XYChartExample() {

    const options = {
        title:{
            text:"XY Chart Example",
        },
        series:[
            {
                valueField:"value",
                label:"Series 1"
            }
        ],
        data:[
            {id:"A", value:10},
            {id:"B", value:20},
            {id:"C", value:15}
        ]
    }

    return <XYChartComponent options={options} 
                              className="vjs-inline-example"/>

}

```
