# VRTooltip Component

**Inherits from:** Component


VRTooltip creates a floating tooltip with configurable text, colors, borders, an optional line hint connecting the tooltip to a target, and an optional directional arrow. The tooltip scales based on distance from the viewer.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Info GUI | *Node* | Node containing the tooltip GUI. |
| Tooltip Text | *String* | Text displayed in the tooltip. |
| Tooltip Text Font Size | *Int* | Font size of the tooltip text. |
| Info Pane Background Color | *Color* | Background color of the tooltip pane. |
| Info Pane Border Color | *Color* | Border color of the tooltip pane. |
| Info Pane Border Thickness | *Float* | Border thickness of the tooltip pane. |
| Enable Line Hint | *Bool* | Whether to display a line connecting the tooltip to a target. |
| Start Point | *Node* | Line hint start point node. |
| End Point | *Node* | Line hint end point node. |
| Min Distance | *Float* | Minimum distance for tooltip scale interpolation. |
| Max Distance | *Float* | Maximum distance for tooltip scale interpolation. |
| Min Scale | *Float* | Tooltip scale at minimum distance. |
| Max Scale | *Float* | Tooltip scale at maximum distance. |
| Start Point Position | *StartPointPosition* | Side of the tooltip pane where the line hint starts. |
| Line Material | *Material* | Material applied to the line hint mesh. |
| Line Width | *Float* | Width of the line hint. |
| Enable Direction Hint | *Bool* | Whether to display a directional arrow hint. |
| Arrow Hint Filepath | *File* | Path to the arrow hint mesh file. |


## VRTooltip Class
