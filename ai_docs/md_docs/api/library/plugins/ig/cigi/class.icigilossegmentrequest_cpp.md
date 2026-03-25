# CigiLosSegmentRequest Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiLosSegmentRequest Class

### Members

---

## int getLosID ( ) const

Returns the LOS ID specified in the packet.
### Return value

LOS ID.
## int getSrcEntityID ( ) const

Returns the Source Entity ID specified in the packet.
### Return value

Source Entity ID.
## int getDestEntityID ( ) const

Returns the value of the **Destination Entity ID** parameter specified in the packet. Defines the entity to which the test segment endpoints shall be relative.
### Return value

Destination Entity ID.
## int getRequestType ( ) const

Returns the value of the **Request Type** parameter specified in the packet. Determines what type of response the IG will return for this request.
### Return value

**Request Type** parameter value. The following values are supported:
- 0 - Basic. The IG shall respond with a [**Line of Sight Response**](../../../../../api/library/plugins/ig/cigi/class.icigilosresponse_cpp.md) packet.
- 1 - Extended. The IG shall respond with a [**Line of Sight Extended Response**](../../../../../api/library/plugins/ig/cigi/class.icigilosextresponse_cpp.md) packet.


## int getSrcCoordSystem ( ) const

Returns the value of the **Source Point Coordinate System** parameter specified in the packet. It indicates the coordinate system relative to which the test segment source endpoint is specified.
### Return value

Source Point Coordinate System parameter value. The following values are supported:
- 0 - Geodetic. The point shall be given by latitude, longitude, and altitude.
- 1 - Entity. The point shall be defined relative to the reference point of the entity specified by [Entity ID](#getSrcEntityID_int).


## int getDestCoordSystem ( ) const

Returns the value of the **Destination Point Coordinate System** parameter specified in the packet. It indicates the coordinate system relative to which the test segment destination endpoint is specified.
### Return value

Destination Point Coordinate System parameter value. The following values are supported:
- 0 - Geodetic. The endpoint shall be given as a latitude, longitude, and altitude.
- 1 - Entity. There are two cases:

  1. If [**Destination Entity ID Valid**](#getDestEntityValid_int) is set to Not Valid (0) than the endpoint shall be defined relative to the reference point of the entity specified by [Source Entity ID](#getSrcEntityID_int).
  2. If [**Destination Entity ID Valid**](#getDestEntityValid_int) is set to Valid (1) than the endpoint shall be defined relative to the reference point of the entity specified by [Destination Entity ID](#getDestEntityID_int).


## int getRespCoordSystem ( ) const

Returns the value of the **Response Coordinate System** parameter specified in the packet. This value specifies the coordinate system to be used in the response.
### Return value

Response Coordinate System parameter value. The following values are supported:
- 0 - Geodetic. The intersection point shall be reported as a latitude, longitude, and altitude.
- 1 - Entity. The intersection point shall be specified relative to the reference point of the intersected entity.


## int getDestEntityValid ( ) const

Returns the value of the **Destination Entity ID Valid** parameter specified in the packet. Determines whether the [Destination Entity ID](#getDestEntityID_int) parameter contains a valid entity ID.
### Return value

Destination entity valid parameter value. The following values are supported:
- 0 - Not Valid. The destination endpoint shall be defined with respect to either the source entity (specified by [Source Entity ID](#getSrcEntityID_int)) or the Geodetic coordinate system as determined by the [Destination Point Coordinate System](#getDestCoordSystem_int) parameter.
- 1 - Valid. The destination endpoint shall be defined with respect to the entity specified by [Destination Entity ID](#getDestEntityID_int), only if [Destination Point Coordinate System](#getDestCoordSystem_int) is set to Entity (1).


## int getAlphaThreshold ( ) const

Returns the value of the **Alpha Threshold** parameter specified in the packet. Defines the minimum alpha value (i.e., minimum opacity) a surface may have for an LOS response to be generated.
### Return value

Alpha Threshold parameter value.
## int getUpdatePeriod ( ) const

Returns the value of the **Update Period** parameter specified in the packet. Specifies the interval between successive responses to this request.
### Return value

Update Period parameter value. The following values are supported:
- 0 - One-Shot request.
- >0 - update period. The value of n>0 indicates that the IG shall return response every n th frame.


## int getMaterialMask ( ) const

Returns the value of the **Material Mask** parameter specified in the packet. Specifies the environmental and cultural features to be included in LOS segment testing.
### Return value

Material Mask parameter value. Each bit represents a material code range; setting that bit to one (1) shall cause the IG to register intersections with polygons whose material codes are within that range.
> **Notice:** Material code ranges are IG-dependent.


## Math:: dvec3 getSrcPosition ( ) const

Returns Source Point position represented as a three-component vector of **Source Latitude, Source Longitude, Source Altitude** or **Source X Offset, Source Y Offset, Source Z Offset** parameters values specified in the packet corresponding to the [Source Point Coordinate System](#getSrcCoordSystem_int) parameter value.
### Return value

Three-component vector that defines Source Point position. The following values are supported:
- [Latitude, Longitude, Altitude] - if Source Point Coordinate System is set to Geodetic (0).
- [X Offset, Y Offset, Z Offset] - if Source Point Coordinate System is set to Entity (1).


## Math:: dvec3 getDestPosition ( ) const

Returns Destination Point position represented as a three-component vector of **Destination Latitude, Destination Longitude, Destination Altitude** or **Destination X Offset, Destination Y Offset, Destination Z Offset** parameters values specified in the packet corresponding to the [Destination Point Coordinate System](#getDestCoordSystem_int) parameter value.
### Return value

Three-component vector that defines Destination Point position. The following values are supported:
- [Latitude, Longitude, Altitude] - if Destination Point Coordinate System is set to Geodetic (0).
- [X Offset, Y Offset, Z Offset] - if Destination Point Coordinate System is set to Entity (1). This offset may be relative to either the source entity or destination entity, depending upon the value of the Destination Entity ID Valid flag.
