# VRObjectHandleRotatable Component

**Inherits from:** VRBaseInteractable


VRObjectHandleRotatable extends **[VRBaseInteractable](../../../../api/templates/template_vr_csharp/base/class.vrbaseinteractable.md)** to implement a rotatable handle (e.g., valve, knob). When grabbed, the object rotates around a specified axis within configurable angle limits. Emits signal events proportional to the rotation. Supports optional toggle mode with animation and sound effects. Implements ISignalEmitter.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Use Anchor | *Bool* | Whether to use a custom anchor point for rotation. |
| Anchor | *Node* | Custom anchor node for the rotation center. |
| Min Angle | *Float* | Minimum rotation angle limit. |
| Max Angle | *Float* | Maximum rotation angle limit. |
| Toggled | *Bool* | Whether the handle operates in toggle mode. |
| Animation Time | *Float* | Duration of the toggle animation (available when Toggled is enabled). |
| Rotation Axis | *MathLib.AXIS* | Axis around which the handle rotates. |
| Sound Start Filepath | *File* | Sound played when rotation begins. |
| Sound Loop Filepath | *File* | Sound played during rotation. |
| Sound Stop Filepath | *File* | Sound played when rotation ends. |
| Sound Min Distance | *Float* | Minimum distance for sound attenuation. |
| Sound Max Distance | *Float* | Maximum distance for sound attenuation. |
| Acceleration Factor | *Float* | Smoothing factor for rotation acceleration. |


### See Also


- **[VRBaseInteractable](../../../../api/templates/template_vr_csharp/base/class.vrbaseinteractable.md)**
- **[VRObjectHandleTranslatable](../../../../api/templates/template_vr_csharp/interactions/class.vrobjecthandletranslatable.md)**


## VRObjectHandleRotatable Class
