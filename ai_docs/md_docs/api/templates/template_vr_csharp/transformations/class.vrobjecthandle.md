# VRObjectHandle Component

**Inherits from:** VRBaseInteractable


VRObjectHandle extends **[VRBaseInteractable](../../../../api/templates/template_vr_csharp/base/class.vrbaseinteractable.md)** to implement a grabbable handle that constrains movement to configurable position and/or rotation ranges.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Change Position | *Bool* | Whether the handle can be moved. |
| Handle Min Pos | *Vec3* | Minimum position limit. |
| Handle Max Pos | *Vec3* | Maximum position limit. |
| Change Rotation | *Bool* | Whether the handle can be rotated. |
| Handle Min Rot | *Vec3* | Minimum rotation limit (Euler angles). |
| Handle Max Rot | *Vec3* | Maximum rotation limit (Euler angles). |
