# CigiPositionRequest Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiPositionRequest Class

### Members

---

## int getObjectID ( ) const

Returns the Object ID specified in the packet.
### Return value

Object ID. The following ranges of values are supported depending on [Object Class](#getObjectClass_int):
- [0; 65535] - If Object Class is in the [0; 2] range.
- [1; 255] - If Object Class=3.
- [0; 255] - If Object Class=4.


## int getPartID ( ) const

Returns the value of the **Articulated Part ID** parameter specified in the packet. Identifies the articulated part whose position is being requested.
### Return value

Articulated Part ID.
## int getUpdateMode ( ) const

Returns the value of the **Update Mode** parameter specified in the packet. Determines whether the IG will report the position of the requested object each frame.
### Return value

Update Mode parameter value. The following values are supported:
- 0 - One-Shot.
- 1 - Continuous.


## int getObjectClass ( ) const

Returns the value of the **Object Class** parameter specified in the packet. Indicates the type of object whose position is being requested.
### Return value

Object Class parameter value. The following values are supported:
- 0 - [Entity](../../../../../api/library/plugins/ig/api/class.entity_cpp.md).
- 1 - [Articulated Part](../../../../../api/library/plugins/ig/api/class.articulatedpart_cpp.md).
- 2 - [View](../../../../../api/library/plugins/ig/api/class.view_cpp.md).
- 3 - [View Group](../../../../../api/library/plugins/ig/api/class.viewgroup_cpp.md).
- 4 - Motion Tracker.


## int getCoordSystem ( ) const

Returns the value of the **Coordinate System** parameter specified in the packet. Determines the desired coordinate system relative to which the position and orientation will be given.
### Return value

Coordinate System parameter value. The following values are supported:
- 0 - Geodetic. Position shall be specified as a geodetic latitude, longitude, and altitude. Orientation shall be given with respect to the reference plane.
- 1 - Parent Entity. Position and orientation shall be with respect to the entity to which the specified entity or view is attached. This value shall be invalid for top-level entities.
- 2 - Submodel. Position and orientation shall be specified with respect to the articulated part�s reference coordinate system. This value shall be valid only when [Object Class](#getObjectClass_int) is set to Articulated Part (1).


> **Notice:** If Object Class is set to Motion Tracker (4), the coordinate system is defined by the tracking device and this parameter
