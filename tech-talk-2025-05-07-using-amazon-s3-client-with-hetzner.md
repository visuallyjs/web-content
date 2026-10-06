# Using Amazon's Java S3 client with Hetzner

May 7, 2025 ·

<!-- -->

4 min read

[![Simon Porritt](https://avatars.githubusercontent.com/u/262720?s=60\&v=4)](https://github.com/sporritt)

[Simon Porritt](https://github.com/sporritt)

VisuallyJs Development

info

This post is from JsPlumb, which is now in maintenance mode.

We recently completed a migration of infrastructure from AWS to Hetzner, saving quite a bit of cash in the process. It was quite straightforward for the most part - we created Cloud instances in Hetzner to replace our EC2 boxes, and span up a Postgres instance on a box of its own to replace RDS. We store packages for our private NPM repository on S3; Hetzner has Object Storage for that, so we migrated those, and we were pretty much done. But then a quick look at Hetzner's docs for Object Storage did not show any official Java libraries for interfacing with Object Storage, and in any case we had a whole persistence layer sitting on S3 that we were not particularly keen to rewrite!

From reading Hetzner's website we reached the conclusion that "S3 Compatible" *probably* meant we could access our buckets via the Amazon S3 client in Java, but how? Our original code looked like this:

```java
import software.amazon.awssdk.regions.Region
import software.amazon.awssdk.services.s3.S3Client

S3Client s3Client = S3Client.builder().region(Region.MY_REGION).build()

```

To access an AWS API, you need to tell it an access key and a secret access key (which you've created in your AWS console). This code doesn't tell AWS anything about credentials, so how does it know what to use? The AWS client code tests various places looking for an access key and a secret access key. In our case we were using a `credentials` file in the `~/aws` for development, and environment variables in production.

<!-- -->

### The full story[​](#the-full-story "Direct link to The full story")

The single line of code above, due to the automatic credentials resolution process, is hiding a few key details. AWS actually needs to know 3 things when it makes an S3 request:

* What is the access key?
* What is the secret access key?
* What is the S3 endpoint?

The first two questions are answered by the credential resolution. The details for the S3 endpoint are filled in by AWS because we told it which Region to use. So to use a Hetzner bucket we need to be able to supply both the access key details and the Hetzner endpoint. We can do the first of these by supplying a *CredentialsProvider*, and the second by an *endpointOverride*.

### Credentials Provider[​](#credentials-provider "Direct link to Credentials Provider")

We wrote our own credentials provider and a credentials model class:

```java
import software.amazon.awssdk.auth.credentials.{AwsCredentials, AwsCredentialsProvider}

class JsPlumbCredentials implements AwsCredentials {

  String accessKey;
  String secretKey;

  constructor(Configuration conf, String accessKeyProperty, String secretKeyProperty) {
    this.accessKey = conf.get(accessKeyProperty);
    this.secretKey = conf.get(secretKeyProperty);
  }

  String accessKeyId() {
    return this.accessKey;
  }

  String secretAccessKey() {
    return this.secretKey;
  }
}

class JsPlumbCredentialsProvider implements AwsCredentialsProvider {

  Configuration conf;
  String accessKeyProperty;
  String secretKeyProperty;

  constructor(Configuration conf, String accessKeyProperty, String secretKeyProperty) {
    this.conf = conf;
    this.accessKeyProperty = accessKeyProperty;
    this.secretKeyProperty = secretKeyProperty;
  }

  AwsCredentials resolveCredentials() {
    return new JsPlumbCredentials(this.conf, this.accessKeyProperty, this.secretKeyProperty);
  }
}


```

`Configuration` here is actually a class in the Play framework, but that's probably one implementation detail that will vary widely between implementations.

Now to tell AWS about this credentials provider:

```java
S3Client s3Client = S3Client.builder()
        .credentialsProvider(new JsPlumbCredentialsProvider(conf, "accessKeyProperty", "secretKeyProperty"))
        .region(Region.MY_REGION)
        .build()

```

### Supplying the endpoint[​](#supplying-the-endpoint "Direct link to Supplying the endpoint")

The other thing that we need to tell AWS about is the endpoint for our Hetzner bucket:

```java
S3Client s3Client = S3Client.builder()
        .credentialsProvider(new JsPlumbCredentialsProvider(conf, "accessKeyProperty", "secretKeyProperty"))
        .region(Region.MY_REGION)
        .endpointOverride(new URI("https://nbg1.your-objectstorage.com"))
        .build()

```

That URL is for Hetzner's Nuremberg storage. They have a couple of others.

And that's it. With those couple of changes we were able to retain our entire persistence API but swap out AWS for Hetzner under the hood.

### Why are you still supplying `region` when connecting to Hetzner?[​](#why-are-you-still-supplying-region-when-connecting-to-hetzner "Direct link to why-are-you-still-supplying-region-when-connecting-to-hetzner")

Perhaps you noticed in these last two code snippets that we're still supplying the region to AWS, and I said above that the reason we were supplying region was for it to figure out the S3 endpoint. Why am I still supplying it? Because computers, that's why! Because when I took it out the AWS client was unhappy and would not connect.

***

***

### Try VisuallyJs[​](#try-visuallyjs "Direct link to Try VisuallyJs")

VisuallyJs offers an extensive list of starter apps, diagrams, charts and dashboards to quick start your development, in React, Angular, Vue, Svelte and Typescript/Javascript.

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/callflow-1200.png)

Call Flow

Use VisuallyJs to build a visual Call Flow editor

![VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](https://static.visuallyjs.com/img/app-card/ai-agent-builder-1200.png)

AI Agent Builder

Use VisuallyJs to create an advanced AI agent builder

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/chatbot-1200.png)

Chatbot

Use VisuallyJs to build a Chatbot editor, with actions, messages, input and choices

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/flowchart-1200.png)

Flowchart

Fully featured flowchart builder including support for custom shapes, edge routing to avoid vertices, shape resize/rotate, SVG/PNG/JPG export and more

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/bpmn-1200.png)

BPMN

BPMN editor for modelling the steps of a business process. Pools, lanes, and a full set of task, event and gateway types

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/erd-1200.png)

ERD

ERD editor for modelling the steps of a business process

![VisuallyJs - callflow builders, sankey charts, database schemas, ERD diagrams and more](https://static.visuallyjs.com/img/app-card/gantt-1200.png)

Gantt

Interactive Gantt chart featuring tasks, task groups and milestones

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/kanban-1200.png)

Kanban

Fully featured Kanban board. Drag items between columns and use the inspector to update items and columns

![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/schema-1200.png)

Database Schema

Database Schema builder with support for tables, views, multiple columns types, and column relationships

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/orgchart-1200.png)

Org Chart

Uses the classic org chart layout and provides an inspector from which the user can navigate around

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/circuit-diagram-1200.png)

Circuit Diagram

Fully featured starter app containing a circuit diagram builder

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/scada-hmi-1200.png)

Scada/HMI

Professional and modern Scada/HMI application with fluid, heating/cooling & instrumentation shapes, adhering to the HMI ISA-101 Design Standard

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/mindmap-1200.png)

Mindmap

The mindmap builder highlights several advanced features, such as custom layouts, parsers and exporters

![VisuallyJs - callflow builders, sankey charts, database schemas, ERD diagrams and more](https://static.visuallyjs.com/img/app-card/neighbourhood-views-1200.png)

Neighbourhood Views

Demonstrates how to include multiple views of a dataset on one page

![VisuallyJs - industry standard diagramming and rich visual UI Javascript and Typescript library](https://static.visuallyjs.com/img/app-card/logic-gates-1200.png)

Logic Gates

Fully featured starter app containing a logic gates diagram builder

![VisuallyJs - callflow builders, sankey charts, database schemas, ERD diagrams and more](https://static.visuallyjs.com/img/app-card/template-1200.png)

Template

Basic starter app demonstrating how to setup VisuallyJs and its main features

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/area-line-chart-1200.png)

Area & Line charts

Use VisuallyJs to create area and line charts

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/bar-column-chart-1200.png)

Bar & Column charts

Multiple series, stacked, grouped, pivoted, and much more

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/scatter-bubble-chart-1200.png)

Scatter & Bubble charts

Circle, rectangle, triangle or custom markers, multiple series, fully customizable

![VisuallyJs - industry standard diagramming and rich visual UI Javascript and Typescript library](https://static.visuallyjs.com/img/app-card/sankey-1200.png)

Sankey chart

Use VisuallyJs to create a professional Sankey chart, with support for pivoting

![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/supply-chain-1200.png)

Supply Chain Analyzer

Dashboard for managing and analyzing supply chains

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/network-infrastructure-1200.png)

Network Infrastructure

Combine a network management diagram with charts showing projected cost and resource usage

![VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](https://static.visuallyjs.com/img/app-card/list-manager-1200.png)

Scrolling Lists

Use the ListManager plugin to manage scrolling lists: as elements are scrolled out of the view, their edges are moved to the list container

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/fifaworldcup-1200.png)

FIFA World Cup

A visualizer for the FIFA World cup - group stages, team journeys and a tournament view.

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/fault-tree-analysis-1200.png)

Fault Tree Analysis

Combines a fault tree analysis diagram with charts showing risk and list of cut sets
