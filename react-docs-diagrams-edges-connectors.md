# Connectors

This page contains definitions and examples for the various connectors that ship with VisuallyJs.

## Bezier[​](#bezier "Direct link to Bezier")

Provides a cubic Bezier path (having two control points) between the two anchors.

```javascript

{
  "connector": "Bezier"
}

```

**********

### Scale[​](#scale "Direct link to Scale")

The key measurement in the Bezier connector is how far the control points are from the anchors. This is controlled by the `scale` option, which is a measure of the ratio of a control point's distance from its anchor compared to the distance between the two anchors in the edge. By default this is 0.45. Increasing this value will make the connector more curvy - in the canvas below we have set it to 0.85:

```javascript

{
  "connector": {
    "type": "Bezier",
    "options": {
      "scale": 0.85
    }
  }
}

```

**********

You can set this to any number, even numbers greater than 1.

### Stubs[​](#stubs "Direct link to Stubs")

You can set a `stub` on the connector:

```javascript

{
  "connector": {
    "type": "Bezier",
    "options": {
      "stub": 25
    }
  }
}

```

**********

### Gap[​](#gap "Direct link to Gap")

You can set a `gap` on the connector to leave some space between the anchor point and the connector line:

```javascript

{
  "connector": {
    "type": "Bezier",
    "options": {
      "gap": 10
    }
  }
}

```

**********

### Options[​](#options "Direct link to Options")

BezierConnectorOptions

Options for CubicBezierConnector

| Name              | Type   | Description                                                                                                                                                                                                                                                                                                 |
| ----------------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| cssClass?         | string | Optional class to set on the element used to render the connector.                                                                                                                                                                                                                                          |
| gap?              | number | Defines a number of pixels between the end of the connector and its anchor point. Defaults to zero.                                                                                                                                                                                                         |
| hoverClass?       | string | Optional class to set on the element used to render the connector when the mouse is hovering over the connector.                                                                                                                                                                                            |
| loopbackDistance? | number | When the connector's source and target is the same vertex, this is a measure of how far the control point will<br />be placed from the element. Defaults to 62 pixels                                                                                                                                       |
| scale?            | number | Where to put the control point relative to the source/target. The number provided here should be a decimal, whose value defines the proportional distance between the source and target that the control point should be located at. The default value is 0.45. Larger values will make the Bezier curvier. |
| stub?             | number | Stub defines a number of pixels that the connector travels away from its element before the connector's actual path begins.                                                                                                                                                                                 |

***

## Straight[​](#straight "Direct link to Straight")

Draws a series of one or more straight line segments between the source and target, with options to smooth to a curve or to round the corners between segments. The default computation creates a single segment, but if you have vertex avoidance switched on, or if you edit the path, then the connector will have multiple segments.

```javascript

{
  "connector": "Straight"
}

```

**********

### Stubs[​](#stubs-1 "Direct link to Stubs")

You can set a `stub` on the connector:

```javascript

{
  "connector": {
    "type": "Straight",
    "options": {
      "stub": 25
    }
  }
}

```

**********

### Gap[​](#gap-1 "Direct link to Gap")

You can set a `gap` on the connector to leave some space between the anchor point and the connector line:

```javascript

{
  "connector": {
    "type": "Straight",
    "options": {
      "gap": 10
    }
  }
}

```

**********

### Geometry[​](#geometry "Direct link to Geometry")

You can supply a `geometry` object for the edge that the connector represents for when you want multiple segments:

```javascript
edges:[
{ 
    "source":"1", 
    "target":"3",
    "geometry":{
        source:{ curX:170, curY:90, ox:1, oy:0, x:1, y:0.5 },
        target:{ curX:510, curY:230, ox:0, oy:1, x:0.5, y:1 },
        segments:[
            { x1: 170, y1: 90, x2:250, y2:90 },
            { x1: 250, y1: 90, x2:400, y2:310 },
            { x1: 400, y1:310, x2:510, y2:230 }
        ]
    }
 }
]

```

```javascript

{
  "connector": "Straight"
}

```

**********

### Smoothing[​](#smoothing "Direct link to Smoothing")

You can also specify that you want to smooth the connector via the `smooth` option:

```javascript

{
  "connector": {
    "type": "Straight",
    "options": {
      "smooth": true
    }
  }
}

```

**********

note

If you set `smooth:true` on a `Straight` connector but don't provide a a value for `stub` then you won't see any curve when there's only one segment, as the smoothing is only applied when the connector has more than one segment. If you provide a small value for `stub` you will see quite a pronounced hook, as in the following example where we set `stub` to 10.

```javascript

{
  "connector": {
    "type": "Straight",
    "options": {
      "stub": 10,
      "smooth": true
    }
  }
}

```

**********

Compare with the same dataset and a `stub` of 50:

```javascript

{
  "connector": {
    "type": "Straight",
    "options": {
      "stub": 50,
      "smooth": true
    }
  }
}

```

**********

Smoothing works better when there are multiple segments in the connector, or when it does not just consist of one straight segment and stubs.

### Rounded corners[​](#rounded-corners "Direct link to Rounded corners")

An alternative to smoothing is rounded corners:

```javascript

{
  "connector": {
    "type": "Straight",
    "options": {
      "cornerRadius": 15
    }
  }
}

```

**********

### Options[​](#options-1 "Direct link to Options")

StraightConnectorOptions

Options for a straight connector.

| Name                | Type                           | Description                                                                                                                                                                                                                                                                                                                                                                                                                          |
| ------------------- | ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| alwaysRespectStubs? | boolean                        | Defaults to true, meaning always draw a stub of the desired length, even when the source and target elements are very close together. This only applies when constrain is set to PATH\_CONSTRAIN\_ORTHOGONAL.                                                                                                                                                                                                                        |
| constrain?          | [ConnectorPathConstrainment]() | Optional constraint on the direction path segments can travel in. Options are PATH\_CONSTRAIN\_NONE, PATH\_CONSTRAIN\_ORTHOGONAL (segments are vertical and/or horizontal lines) and PATH\_CONSTRAIN\_DIAGONAL (segments are vertical, horizontal, or 45 degree lines). You can also use PATH\_CONSTRAIN\_MANHATTAN as an alias for PATH\_CONSTRAIN\_ORTHOGONAL or PATH\_CONSTRAIN\_METRO as an alias for PATH\_CONSTRAIN\_DIAGONAL. |
| cornerRadius?       | number                         | Optional radius to apply to corners. If you have set `smooth:true` this will be ignored.                                                                                                                                                                                                                                                                                                                                             |
| cssClass?           | string                         | Optional class to set on the element used to render the connector.                                                                                                                                                                                                                                                                                                                                                                   |
| gap?                | number                         | Defines a number of pixels between the end of the connector and its anchor point. Defaults to zero.                                                                                                                                                                                                                                                                                                                                  |
| hoverClass?         | string                         | Optional class to set on the element used to render the connector when the mouse is hovering over the connector.                                                                                                                                                                                                                                                                                                                     |
| loopbackRadius?     | number                         | For a loopback connection (when constrain is set to orthogonal), the size of the loop.                                                                                                                                                                                                                                                                                                                                               |
| midpoint?           | number                         | The point to use as the halfway point between the source and target when constrain is set to orthogonal. Defaults to 0.5.                                                                                                                                                                                                                                                                                                            |
| slightlyWonky?      | boolean                        | If true, and a cornerRadius is set, the lines are drawn in such a way that they look slightly hand drawn.                                                                                                                                                                                                                                                                                                                            |
| smooth?             | boolean                        | Whether or not to smooth the connector. Defaults to false. It is not recommended to use this in conjunction with `orthogonal` or `diagonal` constrain, as the line tends to take on a bit of a hand-drawn appearance. It's not without charm but it's also not for everyone.                                                                                                                                                         |
| smoothing?          | number                         | The amount of smoothing to apply. The default is 0.15. Values that deviate too much from the default will make your lines look weird.                                                                                                                                                                                                                                                                                                |
| stub?               | number                         | Stub defines a number of pixels that the connector travels away from its element before the connector's actual path begins.                                                                                                                                                                                                                                                                                                          |

***

## Orthogonal[​](#orthogonal "Direct link to Orthogonal")

Draws a connection that consists of a series of vertical or horizontal segments - the classic flowchart look. Internally this connector is an alias for a `Straight` connector with `constrain:"orthogonal"`.

```javascript

{
  "connector": "Orthogonal"
}

```

**********

### Stubs[​](#stubs-2 "Direct link to Stubs")

You can set a `stub` on the connector.

```javascript

{
  "connector": {
    "type": "Orthogonal",
    "options": {
      "stub": 25
    }
  }
}

```

**********

### Gap[​](#gap-2 "Direct link to Gap")

You can set a `gap` on the connector to leave some space between the anchor point and the connector line:

```javascript

{
  "connector": {
    "type": "Orthogonal",
    "options": {
      "gap": 10
    }
  }
}

```

**********

### Rounded corners[​](#rounded-corners-1 "Direct link to Rounded corners")

```javascript

{
  "connector": {
    "type": "Orthogonal",
    "options": {
      "cornerRadius": 5
    }
  }
}

```

**********

### Slightly wonky[​](#slightly-wonky "Direct link to Slightly wonky")

We stumbled across this effect in error while developing the orthogonal connector and we thought it had a certain charm, so we put it on a flag - it gives your connectors a slightly hand-drawn feel. You need to set a `cornerRadius` when you set this flag or you won't see any effect. Here we've used a corner radius of 5 pixels. Feel free to experiment, but in our experience numbers much larger than that tend to reduce the charm.

```javascript

{
  "connector": {
    "type": "Orthogonal",
    "options": {
      "slightlyWonky": true,
      "cornerRadius": 5
    }
  }
}

```

**********

### Options[​](#options-2 "Direct link to Options")

OrthogonalConnectorOptions

Options for an orthogonal connector.

| Name                | Type    | Description                                                                                                                           |
| ------------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| alwaysRespectStubs? | boolean | Defaults to true, meaning always draw a stub of the desired length, even when the source and target elements are very close together. |
| cornerRadius?       | number  | Optional curvature of the corners in the connector. Defaults to 0.                                                                    |
| cssClass?           | string  | Optional class to set on the element used to render the connector.                                                                    |
| gap?                | number  | Defines a number of pixels between the end of the connector and its anchor point. Defaults to zero.                                   |
| hoverClass?         | string  | Optional class to set on the element used to render the connector when the mouse is hovering over the connector.                      |
| loopbackRadius?     | number  | For a loopback connection, the size of the loop.                                                                                      |
| midpoint?           | number  | The point to use as the halfway point between the source and target. Defaults to 0.5.                                                 |
| slightlyWonky?      | boolean | If true, and a cornerRadius is set, the lines are drawn in such a way that they look slightly hand drawn.                             |
| stub?               | number  | Stub defines a number of pixels that the connector travels away from its element before the connector's actual path begins.           |

***

## QuadraticBezier[​](#quadraticbezier "Direct link to QuadraticBezier")

Draws slightly curved lines, similar to the connectors you may have seen in software like GraphViz.

```javascript

{
  "connector": "QuadraticBezier"
}

```

**********

### Curviness[​](#curviness "Direct link to Curviness")

You can set the `curviness` of the connector to adjust how pronounced the curve is, by changing the position of the control with respect to the midpoint of the two anchors. The default value is 10. There is no limit to what you can set this value to be, although large values do tend to be less pleasing. You can also set this to be a negative number, which will result in the connector curving in the opposite way to the default.

```javascript

{
  "connector": {
    "type": "QuadraticBezier",
    "options": {
      "curviness": 30
    }
  }
}

```

**********

### Stubs[​](#stubs-3 "Direct link to Stubs")

You can set a `stub` on the connector:

```javascript

{
  "connector": {
    "type": "QuadraticBezier",
    "options": {
      "stub": 25
    }
  }
}

```

**********

### Gap[​](#gap-3 "Direct link to Gap")

You can set a `gap` on the connector to leave some space between the anchor point and the connector line:

```javascript

{
  "connector": {
    "type": "QuadraticBezier",
    "options": {
      "gap": 10
    }
  }
}

```

**********

### Options[​](#options-3 "Direct link to Options")

QuadraticBezierConnectorOptions

Options for a QuadraticBezierConnector

| Name              | Type   | Description                                                                                                                                                           |
| ----------------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| cssClass?         | string | Optional class to set on the element used to render the connector.                                                                                                    |
| curviness?        | number | A measure of how "curvy" the bezier is. In terms of maths what this translates to is how far from the midpoint of the curve the control points is positioned.         |
| gap?              | number | Defines a number of pixels between the end of the connector and its anchor point. Defaults to zero.                                                                   |
| hoverClass?       | string | Optional class to set on the element used to render the connector when the mouse is hovering over the connector.                                                      |
| loopbackDistance? | number | When the connector's source and target is the same vertex, this is a measure of how far the control point will<br />be placed from the element. Defaults to 62 pixels |
| stub?             | number | Stub defines a number of pixels that the connector travels away from its element before the connector's actual path begins.                                           |
