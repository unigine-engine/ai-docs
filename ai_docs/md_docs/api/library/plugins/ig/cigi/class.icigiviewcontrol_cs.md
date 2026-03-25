# CigiViewControl Class (CS)

**Inherits from:** CigiHostPacket


## CigiViewControl Class

### Properties

## 🔒︎ int ViewID

The view ID specified in the packet.
## 🔒︎ int GroupID

The view group ID specified in the packet.
## 🔒︎ int EntityID

The entity ID specified in the packet.
> **Notice:** This value shall be ignored if the view is in a group.


## 🔒︎ ivec3 OffsetEnabled

The three-component vector combining **Offset Enable** values specified in the packet. Each value determines whether the offset for the corresponding axis(X - back, Y - left, Z - down) is enabled.
## 🔒︎ ivec3 RotationEnabled

The three-component vector combining **Roll/Pitch/Yaw Enable** values specified in the packet. Each value determines whether the rotation around the corresponding axis(roll, pitch, yaw) is enabled.
## 🔒︎ vec3 Offset

The offset of the view specified in the packet.
## 🔒︎ vec3 Rotation

The rotation euler angles of the view specified in the packet.
### Members

---
