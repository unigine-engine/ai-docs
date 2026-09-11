# VRObjectHandleTranslatable Component

**Inherits from:** VRBaseInteractable


VRObjectHandleTranslatable extends **[VRBaseInteractable](../../../../api/templates/template_vr_csharp/base/class.vrbaseinteractable.md)** to implement a translatable handle (e.g., slider, lever). When grabbed, the object moves along a line defined by min/max positions. Supports optional toggle mode with animation, sound effects, and acceleration smoothing.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Sound Start Filepath | *File* | Sound played when movement begins. |
| Sound Loop Filepath | *File* | Sound played during movement. |
| Sound Stop Filepath | *File* | Sound played when movement ends. |
| Sound Min Distance | *Float* | Minimum distance for sound attenuation. |
| Sound Max Distance | *Float* | Maximum distance for sound attenuation. |
| Use Anchor | *Bool* | Whether to use a custom anchor point. |
| Anchor Node | *Node* | Custom anchor node. |
| Min Handle Position | *Vec3* | Minimum position limit for the handle. |
| Max Handle Position | *Vec3* | Maximum position limit for the handle. |
| Toggled | *Bool* | Whether the handle operates in toggle mode. |
| Animation Time | *Float* | Duration of the toggle animation. |
| Acceleration Factor | *Float* | Smoothing factor for movement acceleration. |


### See Also


- **[VRBaseInteractable](../../../../api/templates/template_vr_csharp/base/class.vrbaseinteractable.md)**
- **[VRObjectHandleRotatable](../../../../api/templates/template_vr_csharp/interactions/class.vrobjecthandlerotatable.md)**
