AutoPanBoundsStrategy

Strategy for determining whether something that is moving is considered out of bounds. Options are 'contained', ie the element must be fully contained inside the root bounds, or 'intersecting', ie. the element must intersect the root bounds by some amount. Prior to 1.1.4 the behaviour was 'contained', but a change in 1.1.4 switched this to 'intersecting', which does not necessarily provide the best UX when the canvas is hard up against the edge of the screen, because it isnt always possible to move the mouse far enough that the element is not intersecting, and in those situations panning stops. From 1.2.1 onwards the default is once again `contained`, but you can change that via the `autoPanBoundsStrategy` option on the surface's dragOptions.

`"contained" | "intersecting"`
