# CigiVolumeDef Class (CS)

**Inherits from:** CigiHostPacket


## CigiVolumeDef Class

### Properties

## 🔒︎ int EntityID

The entity ID specified in the packet.
## 🔒︎ int VolumeID

The volume ID specified in the packet.
## 🔒︎ int VolumeEnabled

The value of the **Volume Enable** parameter specified in the packet.
## 🔒︎ int VolumeType

The value of the **Volume Type** parameter specified in the packet.
## 🔒︎ vec3 Center

The coordinates of the offset of the center of the collision volume specified in the packet.
> **Notice:** Measured with respect to the coordinate system of the entity specified by the [Entity ID](#getEntityID_int) parameter

## 🔒︎ vec3 Size

The size of the collision volume specified in the packet.
> **Notice:** For spherical volumes only the first component of the vector is considered - it is interpreted as radius.

## 🔒︎ vec3 Rotation

The rotation euler angles of the collision volume specified in the packet.
## 🔒︎ float Radius

The radius of the spherical collision volume specified in the packet.
### Members

---
