# VRAttachToHand Component

**Inherits from:** Component


VRAttachToHand attaches a node to a VR hand controller. The attached node follows the hand position with an optional custom transform offset. Supports left and right hand selection.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Side | *Side (Left/Right)* | Which hand to attach to. |
| Use Self Transform | *Bool* | Whether to use the node's own transform as the offset. |
| Position | *Vec3* | Custom positional offset (available when Use Self Transform is disabled). |
| Rotation | *vec3* | Custom rotational offset in Euler angles (available when Use Self Transform is disabled). |


## VRAttachToHand Class
