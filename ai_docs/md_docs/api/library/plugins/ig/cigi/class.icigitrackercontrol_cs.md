# CigiTrackerControl Class (CS)

**Inherits from:** CigiHostPacket


## CigiTrackerControl Class

### Properties

## 🔒︎ int ViewID

The view ID specified in the packet.
## 🔒︎ int TrackerID

The tracker ID specified in the packet.
## 🔒︎ int TrackerEnabled

The value of the **Tracker Enable** parameter specified in the packet.
## 🔒︎ int BoresightEnabled

The value of the **Boresight Enable** parameter specified in the packet. The boresight enable mode is used to reestablish the tracker�s �center� position at the current position and orientation.
## 🔒︎ int GroupSelect

The value of the **View/View Group Select** parameter specified in the packet.
## 🔒︎ ivec3 PositionEnabled

The Vector of three integer values. Each value determines the corresponding coordinate (X, Y, Z).three-component vector providing **X, Y, and Z** coordinates.
## 🔒︎ ivec3 RotationEnabled

The three-component vector combining **Roll/Pitch/Yaw Enable** values specified in the packet. Each value determines whether the rotation around the corresponding axis (roll, pitch, yaw) is enabled.
### Members

---
