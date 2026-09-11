# CigiTrajectoryDef Class (CS)

**Inherits from:** CigiHostPacket


## CigiTrajectoryDef Class

### Properties

## 🔒︎ int EntityID

The entity ID specified in the packet.
## 🔒︎ vec3 Acceleration

The coordinates of the accceleration vector specified in the packet.
## 🔒︎ float RetardationRate

The value of the **Retardation Rate** parameter specified in the packet. Determines the magnitude of an acceleration applied against the entity�s instantaneous linear velocity vector. This is used to simulate drag and other frictional forces acting upon the [entity](#getEntityID_int).
## 🔒︎ float TerminalVelocity

The value of the **Terminal Velocity** parameter specified in the packet. Determines the maximum velocity the entity can obtain.
### Members

---
