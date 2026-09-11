# CigiTrackerControl Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiTrackerControl Class

### Members

---

## int getViewID ( ) const

Returns the view ID specified in the packet.
### Return value

View ID.
## int getTrackerID ( ) const

Returns the tracker ID specified in the packet.
### Return value

Tracker ID.
## int getTrackerEnabled ( ) const

Returns the value of the **Tracker Enable** parameter specified in the packet.
### Return value

**Tracker Enable** parameter value: 1 if the tracking device is enabled; otherwise, 0.
## int getBoresightEnabled ( ) const

Returns the value of the **Boresight Enable** parameter specified in the packet. The boresight enable mode is used to reestablish the tracker�s �center� position at the current position and orientation.
### Return value

**Boresight Enable** parameter value: 1 if the boresight state of the tracking device is enabled; otherwise, 0.
> **Notice:** When enabled, the Host shall send a Motion Tracker Control packet with Boresight Enable set to Disable (0) to return the tracker to normal operation. The IG shall continue to update the boresight position each frame until that occurs.


## int getGroupSelect ( ) const

Returns the value of the **View/View Group Select** parameter specified in the packet.
### Return value

**View/View Group Select** parameter value: 1 if the tracking device is attached to a view group; 0 - if the tracking device is attached to a single view.
## Math:: ivec3 getPositionEnabled ( ) const

Returns a three-component vector providing **X, Y, and Z** coordinates.
### Return value

Vector of three integer values. Each value determines the corresponding coordinate (X, Y, Z).
## Math:: ivec3 getRotationEnabled ( ) const

Returns a three-component vector combining **Roll/Pitch/Yaw Enable** values specified in the packet. Each value determines whether the rotation around the corresponding axis (roll, pitch, yaw) is enabled.
### Return value

Vector of three integer values. Each value determines whether the rotation around the corresponding axis (Roll, Pitch, Yaw) is enabled: 1 - enabled; 0 - disabled.
