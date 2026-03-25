# CigiPositionResponse Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiIGPacket


## CigiPositionResponse Class

### Members

---

## void setObjectID ( int id )

Sets the value of the **Object ID** parameter to be specified in the packet.
### Arguments

- *int* **id** - **Object ID** parameter value.

## void setPartID ( int id )

Sets the value of the **Part ID** parameter to be specified in the packet.
### Arguments

- *int* **id** - **Part ID** parameter value.

## void setObjectClass ( int c )

Sets the value of the **Object Class** parameter to be specified in the packet.
### Arguments

- *int* **c** - **Object Class** parameter value. The following values are supported:

  - 0 - [Entity](../../../../../api/library/plugins/ig/api/class.entity_cpp.md).
  - 1 - [Articulated Part](../../../../../api/library/plugins/ig/api/class.articulatedpart_cpp.md).
  - 2 - [View](../../../../../api/library/plugins/ig/api/class.view_cpp.md).
  - 3 - [View Group](../../../../../api/library/plugins/ig/api/class.viewgroup_cpp.md).
  - 4 - Motion Tracker.

## void setCoordSystem ( int s )

Sets the value of the **Coordinate System** parameter to be specified in the packet.
### Arguments

- *int* **s** - **Coordinate System** parameter value. The following values are supported:

  - 0 - Geodetic coordinate system.
  - 1 - Local entity coordinate system
  - 2 - Local submodel coordinate system

## void setPosition ( const Math::dvec3& p )

Sets the values of parameters that determine the **Position** to be specified in the packet.
### Arguments

- *const  Math::dvec3&* **p** - Position coordinates.

  - For geodetic coordinate system: (Lat, Lon, Alt)
  - For local coordinate systems: (X-offset, Y-offset, Z-offset)

## void setRotation ( const Math::vec3& r )

Sets the values of parameters that determine the **Rotation** to be specified in the packet.
### Arguments

- *const  Math::vec3&* **r** - Rotation euler angles: (Roll, Pitch, Yaw).
