# CigiSensorResponse Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiIGPacket


## CigiSensorResponse Class

### Members

---

## void setViewID ( int id )

Sets the value of the **View ID** parameter to be specified in the packet.
### Arguments

- *int* **id** - **View ID** parameter value.

## void setSensorID ( int id )

Sets the value of the **Sensor ID** parameter to be specified in the packet.
### Arguments

- *int* **id** - **Sensor ID** parameter value.

## void setSensorStatus ( int status )

Sets the value of the **Sensor Status** parameter to be specified in the packet.
### Arguments

- *int* **status** - **Sensor Status** parameter value. The following values are supported:

  - 0 - Searching for target
  - 1 - Tracking target
  - 2 - Impending breaklock
  - 3 - Breaklock

## void setGateSize ( const Math::ivec3& size )

Sets the values of parameters that determine the **Gate Size** to be specified in the packet.
### Arguments

- *const  Math::ivec3&* **size** - **Gate Sizes**, in pixels: (X-size, Y-size). > **Notice:** Only the first two components of the vector are used.

## void setGateOffset ( const Math::vec3& offset )

Sets the values of parameters that determine the **Gate Position** to be specified in the packet.
### Arguments

- *const  Math::vec3&* **offset** - **Gate Position** coordinates: (X-coordinate, Y-coordinate). > **Notice:** Only the first two components of the vector are used.
