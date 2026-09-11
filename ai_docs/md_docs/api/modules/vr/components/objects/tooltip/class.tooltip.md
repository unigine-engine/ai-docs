# Tooltip Component

**Inherits from:** ComponentBase


Tooltip displays floating text hints in 3D space with optional connector lines. Tooltips can show static text or dynamic content with button hints that update based on input bindings.


The component scales based on distance from the player and can draw a curved line between a start and end point to visually connect the tooltip to an object.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Text Group |  |  |
| Info Gui Parameter | *Node* | **GUI** node for tooltip rendering. |
| Tooltip Text | *String* | Text to display. |
| Tooltip Text Font Size | *Int* | Font size (*default: 275*). |
| Appearance Group |  |  |
| Info Pane Background Color | *Color* | Background color. |
| Info Pane Border Color | *Color* | Border color. |
| Info Pane Border Thickness | *Float* | Border width (*default: 0.15*). |
| Line Hint Group |  |  |
| Enable Line Hint | *Toggle* | Show connector line. |
| Start Point | *Node* | Start point of the connector line. Visible when Enable Line Hint is enabled. |
| End Point | *Node* | End point of the connector line. Visible when Enable Line Hint is enabled. |
| Start Point Pos | *Switch* | Start point anchor position: bottom, up, left, right. |
| Line Material | *Material* | Material applied to the connector line. |
| Line Width | *Float* | Width of the connector line. Default: *0.005*. |
| Enable Direction Hint | *Toggle* | Show directional arrow hint. |
| Arrow Hint Filepath | *File* | File path for the arrow hint asset. Visible when Enable Direction Hint is enabled. |
| Distance Scaling Group |  |  |
| Min Distance | *Float* | Minimum visibility distance. |
| Max Distance | *Float* | Maximum visibility distance. |
| Min Scale | *Float* | Scale at minimum distance. |
| Max Scale | *Float* | Scale at maximum distance. |


### See Also


- **[VRController](../../../../../../api/modules/vr/components/players/class.vrcontroller.md)**


## Tooltip Class

---

## void setVisible ( )

Shows or hides the tooltip.
### Arguments

## void setFontSize ( )

Sets the tooltip text font size.
### Arguments

## void setText ( )

Sets the tooltip text content.
### Arguments

## void setTextWithKey ( )

Sets tooltip text with a button hint that shows the current binding.
### Arguments
