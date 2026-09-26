EVENT\_TAP

"tap"

A tap event is a synthesized event in which VisuallyJs captures a mousedown/touchstart followed by, within some time period, a mouseup/touchend. If the event target's position has not changed between the two events, a tap event is fired. It is generally preferable to bind to this event rather than EVENT\_CLICK, because a browser will fire a click event even if the event target has changed position between mousedown and mouseup. So you can get spurious click events reported while dragging elements, for example.
