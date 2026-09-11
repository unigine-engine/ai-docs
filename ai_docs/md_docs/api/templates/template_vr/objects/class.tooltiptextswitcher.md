# TooltipTextSwitcher Component

**Inherits from:** ComponentBase


TooltipTextSwitcher sets different tooltip text depending on whether the application is running in VR or PC mode. On initialization, it finds the **[Tooltip](../../../../api/modules/vr/components/objects/tooltip/class.tooltip.md)** component on the specified node and sets the appropriate text.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| tooltip_node | *Node* | Node with a **[Tooltip](../../../../api/modules/vr/components/objects/tooltip/class.tooltip.md)** component whose text will be set. |
| text_for_pc | *String* | Tooltip text used in PC (non-VR) mode. |
| text_for_vr | *String* | Tooltip text used in VR mode. |


### See Also


- **[Tooltip](../../../../api/modules/vr/components/objects/tooltip/class.tooltip.md)**
