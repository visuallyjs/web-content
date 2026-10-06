# Dashboards

Creating dashboards - using the same model for both an interactive diagram (like a flowchart or process builder) and real-time charts - is a straightforward process, and makes for very powerful UIs. The chart consumes the model directly, so any interaction with the canvas is immediately reflected in any connected charts.

## Real-World Applications[​](#real-world-applications "Direct link to Real-World Applications")

### 1. Supply Chain Management[​](#1-supply-chain-management "Direct link to 1. Supply Chain Management")

In a supply chain management app, a user can use a flowchart-style interface to map out the movement of goods from "Manufacturer" to "Warehouse" to "Retailer." Each node defines some specific location, and then the edges between the nodes can store the quantity of goods that passes between nodes, as well as other information such as the shipping method and carrier.

A separate Sankey view can then provide the user with a summary of the flow, with the ability to pivot on specific values in the edge data such as the transit mode or carrier. You can see this in action in our <!-- -->[Supply Chain Analyzer](/demonstrations/supply-chain.md) starter app:

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/supply-chain-2400.png)

### 2. Infrastructure & Cloud Resource Management[​](#2-infrastructure--cloud-resource-management "Direct link to 2. Infrastructure & Cloud Resource Management")

Cloud architects often use diagramming tools to design VPCs, subnets, and server clusters. Charts can be linked to these diagrams to show information such as projected monthly spend, or total number of assets, etc. Take a look at our <!-- -->[Network Infrastructure](/demonstrations/network-infrastructure.md) dashboard to see a working example of this.

### 3. Business Process Optimization (BPMN)[​](#3-business-process-optimization-bpmn "Direct link to 3. Business Process Optimization (BPMN)")

Business analysts use process builders to define workflows (e.g., an insurance claim approval process).

* **The Model:** The steps and decision gateways of the business process.
* **Real-time Charts:** While simulating or monitoring the process, a Histogram could show the "Bottleneck Score" for each node in the flowchart. If the user moves a "Manual Review" step to a different team in the diagram, the charts would update to show how that change impacts the overall "Mean Time to Resolution."

### 4. Smart Manufacturing[​](#4-smart-manufacturing "Direct link to 4. Smart Manufacturing")

Digital twins of factory floors are often represented as diagrams showing the connection between various machines (PLC units).

* **The Model:** The physical layout and logical connection of the assembly line.
* **Real-time Charts:** If a machine node in the diagram reports an error state (changing its color or icon), a linked Donut Chart could immediately show the impact on the day's OEE (Overall Equipment Effectiveness) or the percentage of the line that is currently "Down."

### 5. Financial Portfolio & Risk Mapping[​](#5-financial-portfolio--risk-mapping "Direct link to 5. Financial Portfolio & Risk Mapping")

Financial analysts often map out complex relationships between parent companies, subsidiaries, and investment vehicles.

* **The Model:** The ownership structure and flow of capital.
* **Real-time Charts:** As the user adjusts the "Ownership %" on an edge between two company nodes using an inspector, a Treemap chart could update to show the weighted risk exposure across the entire portfolio based on the new structural data.

[Getting Started](./getting-started)

[Learn how to build a simple dashboard with VisuallyJs](./getting-started)
