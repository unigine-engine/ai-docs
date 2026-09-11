# NodeSwitchEnableByGrab Component

**Inherits from:** ComponentBase, VRInteractable


NodeSwitchEnableByGrab toggles the enabled state of a set of nodes when the component's owner node is grabbed by the player. Each grab action switches the target nodes between enabled and disabled states.


The component implements the **[VRInteractable](../../../../api/modules/vr/components/class.vrinteractable.md)** interface to receive grab events from the VR interaction system.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| nodes_to_switch | *Array<Node>* | List of nodes whose enabled state will be toggled on grab. |
| default_nodes_state | *Switch* | Initial state of the target nodes: Enabled, Disabled. |


### See Also


- **[VRInteractable](../../../../api/modules/vr/components/class.vrinteractable.md)**
- **[NodeSwitchEnableByGesture](../../../../api/templates/template_vr/global/class.nodeswitchenablebygesture.md)**
- **[NodeSwitchEnableByKey](../../../../api/templates/template_vr/global/class.nodeswitchenablebykey.md)**


## NodeSwitchEnableByGrab Class

---

## void grabIt ( )

Called when the player grabs this object. Toggles the enabled state of all target nodes.
### Arguments
