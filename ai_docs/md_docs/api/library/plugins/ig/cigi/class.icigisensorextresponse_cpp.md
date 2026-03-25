# CigiSensorExtResponse Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiIGPacket


## CigiSensorExtResponse Class

### Members

---

## void setViewID ( int id )

Sets the value of the **View ID** parameter to be specified in the packet.
### Arguments

- *int* **id** - **View ID** parameter value.

## void setEntityID ( int id )

Sets the value of the **Entity ID** parameter to be specified in the packet.
### Arguments

- *int* **id** - **Entity ID** parameter value.

## void setSensorID ( int id )

Sets the value of the **Sensor ID** parameter to be specified in the packet.
### Arguments

- *int* **id** - **Sensor ID** parameter value.

## void setEntityValid ( int valid )

Sets the value of the **Entity Valid** parameter to be specified in the packet.
### Arguments

- *int* **valid** - **Entity ID Valid** parameter value. The following values are supported:

  - 0 - invalid (if the target point being tracked is not a part of an entity)
  - 1 - valid (if the target point being tracked is a part of an entity)

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

## void setTrackPoint ( const Math::dvec3& point )

Sets the values of parameters that determine the **Track Point Coordinates** to be specified in the packet.
### Arguments

- *const  Math::dvec3&* **point** - Track point coordinates:(*Latitude, Longitude, Altitude*).

  - *Latitude* - [-90.0; 90.0] relative to the Equator.
  - *Longitude* - [-180.0; 180.0] relative to the Prime Meridian.
  - *Altitude* - meters above the Mean Sea Level.
