## [Adding graph propagation to our logic gates app](./tech-talk-2026-09-25-adding-graph-propagation-to-logic-gate-simulator.md)

September 25, 2026 ·

<!-- -->

9 min read

![Logic gates app](https://static.visuallyjs.com/img/app-card/logic-gates-2400.png)

We shipped a [Logic Gates diagram builder](https://visuallyjs.com/demonstrations/logic-gates) app for React, Angular, Vue and Svelte a few weeks ago. It's a cool app, allowing users to construct diagrams with some nifty features like auto edge connect while dragging, and auto connect when dropping on an existing edge:

![](https://static.visuallyjs.com/img/blog/1.2.5/logic-gates-drop-on-edge.gif)

what it didn't do, though, was offer the ability for someone to see the flow of logic through the diagrams they had created. And so that's the topic of today's article - we're going to run through how we went about adding a simulator function to this app.

## Input/output shapes[​](#inputoutput-shapes "Direct link to Input/output shapes")

The current set of shapes does not contain anything I can use to inject or read values. So I had a quick chat with an agent about it:

[**Read more**](./tech-talk-2026-09-25-adding-graph-propagation-to-logic-gate-simulator.md)
