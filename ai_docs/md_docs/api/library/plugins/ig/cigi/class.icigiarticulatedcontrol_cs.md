# CigiArticulatedControl Class (CS)

**Inherits from:** CigiHostPacket


## CigiArticulatedControl Class

### Properties

## 🔒︎ int EntityID

The entity ID specified in the packet.
## 🔒︎ int PartID

The articulated part ID specified in the packet.
## 🔒︎ int PartEnabled

The value of the **Articulated Part Enable** parameter specified in the packet.
## 🔒︎ ivec3 OffsetEnabled

The three-component vector combining **Offset Enable** values specified in the packet. Each value determines whether the offset for the corresponding axis(X - back, Y - left, Z - down) is enabled
## 🔒︎ ivec3 RotationEnabled

The three-component vector combining **Roll/Pitch/Yaw Enable** values specified in the packet. Each value determines whether the rotation around the corresponding axis(roll, pitch, yaw) is enabled.
## 🔒︎ vec3 Offset

The offset of the articulated part in the submodel coordinate system (SCS) specified in the packet.
## 🔒︎ vec3 Rotation

The rotation of the articulated part in the submodel coordinate system (SCS) specified in the packet.
### Members

---
