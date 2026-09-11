# AttachToHand Component

**Inherits from:** ComponentBase


AttachToHand attaches a node to the **VR** player's hand at initialization. This is useful for tools, menus, or other objects that should always be positioned relative to the hand.


The attachment can use either the node's current transform or a custom position/rotation offset.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Side | *Switch* | Which hand to attach to (Left or Right). |
| Use Self Transform | *Toggle* | Use the node's current transform instead of offsets. |
| Position | *Vec3* | Position offset from hand. |
| Rotation | *Vec3* | Rotation offset in euler angles. |


### See Also


- **[AttachToHead](../../../../../api/modules/vr/components/objects/class.attachtohead.md)**
