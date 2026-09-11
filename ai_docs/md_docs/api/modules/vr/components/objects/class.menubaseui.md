# MenuBaseUI Component

**Inherits from:** ComponentBase


MenuBaseUI is a base component for creating in-world UI menus in VR. It provides integration with ObjectGui and ObjectGuiMesh for rendering GUI elements on 3D surfaces.


Extend this class to create custom VR menus with interactive UI elements.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| use_custom_gui | *Toggle* | Use a custom ObjectGui reference. |
| object_gui_parameter | *Node* | Reference to ObjectGui node. |
| use_custom_gui_mesh | *Toggle* | Use a custom ObjectGuiMesh reference. |
| object_gui_mesh_parameter | *Node* | Reference to ObjectGuiMesh node. |


### See Also


- **[VRPlayer](../../../../../api/modules/vr/components/players/class.vrplayer.md)**


## MenuBaseUI Class

---

## void init ( )

Initializes the menu component and GUI references.
## void init_gui ( )

Override this method to initialize custom GUI elements.
