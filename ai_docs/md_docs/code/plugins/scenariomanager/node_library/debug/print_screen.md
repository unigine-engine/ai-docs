# Print to Screen


![](../img/print_to_screen.png)

### Description

Draws a message directly on the screen, which makes it useful for watching a value change while the scenario runs.


**X** and **Y** give the position in screen coordinates, where 0 is the left or top edge and 1 is the right or bottom edge. **Duration** sets how long the message stays visible, in seconds; with the default 0 it is shown for a single frame, so trigger the node every frame to keep it on the screen.


> **Notice:** The message is drawn by the visualizer, which has to be enabled for anything to appear. Use the [Console Command](../../../../../code/plugins/scenariomanager/node_library/debug/console.md) node or the console itself to turn it on with *show_visualizer 1*.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Action** | Triggers the node. |
| ![](../img/types/string.png) | **Message** | The text to draw. |
| ![](../img/types/float.png) | **X** | The horizontal position, from 0 at the left edge to 1 at the right edge. |
| ![](../img/types/float.png) | **Y** | The vertical position, from 0 at the top edge to 1 at the bottom edge. |
| ![](../img/types/float.png) | **Duration** | How long the message stays visible, in seconds. |
| ![](../img/types/exec.png) | **Event** | Fires after the message has been drawn. |


## See Also


- [Log](../../../../../code/plugins/scenariomanager/node_library/debug/log.md)
- [Format Log](../../../../../code/plugins/scenariomanager/node_library/debug/flog.md)
- [Console Command](../../../../../code/plugins/scenariomanager/node_library/debug/console.md)
