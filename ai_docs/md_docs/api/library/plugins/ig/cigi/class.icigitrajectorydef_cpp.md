# CigiTrajectoryDef Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiTrajectoryDef Class

### Members

---

## int getEntityID ( ) const

Returns the entity ID specified in the packet.
### Return value

Entity ID.
## Math:: vec3 getAcceleration ( ) const

Returns the coordinates of the accceleration vector specified in the packet.
### Return value

Acceleration vector of the [entity](#getEntityID_int).
## float getRetardationRate ( ) const

Returns the value of the **Retardation Rate** parameter specified in the packet. Determines the magnitude of an acceleration applied against the entity�s instantaneous linear velocity vector. This is used to simulate drag and other frictional forces acting upon the [entity](#getEntityID_int).
### Return value

**Retardation Rate** parameter value.
## float getTerminalVelocity ( ) const

Returns the value of the **Terminal Velocity** parameter specified in the packet. Determines the maximum velocity the entity can obtain.
### Return value

**Terminal Velocity** parameter value.
