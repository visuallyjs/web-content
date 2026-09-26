## [Annotating objects with drag groups](/news/2025/04/09/annotating-objects-with-drag-groups.md)

May 18, 2026 ·

<!-- -->

8 min read

One of the key differentiators between VisuallyJs and other libraries in this space is VisuallyJs's level of configurability - more often than not you'll find that once you hit a blocker in some other library, VisuallyJs will offer you the ability to do what you need.

A great example of this is VisuallyJs's concept of a `DragGroup`. Simply put, this is a group of vertices that should be dragged together - but as we'll see, it's not quite as simple as that, and it can be used to great effect with minimal work required on your part.

### Active vs passive members[​](#active-vs-passive-members "Direct link to Active vs passive members")

In this canvas, try dragging the large green box around. You'll see the two red boxes drag along with it. Now try dragging one of the red boxes - nothing else moves. This is because all of the nodes are inside a drag group, but the large green node is marked `active` and the red nodes are marked `passive`:

**********

**Tags:**

* [svg](/news/tags/svg.md)
* [flowchart](/news/tags/flowchart.md)
* [inspector](/news/tags/inspector.md)
* [erd](/news/tags/erd.md)
* [svg export](/news/tags/svg-export.md)
* [png](/news/tags/png.md)
* [jpeg](/news/tags/jpeg.md)
* [jpg](/news/tags/jpg.md)
* [apidocs](/news/tags/apidocs.md)
* [gantt](/news/tags/gantt.md)
* [gantt chart](/news/tags/gantt-chart.md)
* [network topology](/news/tags/network-topology.md)
* [jointjs](/news/tags/jointjs.md)
* [reactflow](/news/tags/reactflow.md)
* [gojs](/news/tags/gojs.md)

[**Read more**](/news/2025/04/09/annotating-objects-with-drag-groups.md)
