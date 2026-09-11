# CigiLosVectorRequest Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiLosVectorRequest Class

### Members

---

## int getLosID ( ) const

Returns the LOS ID specified in the packet.
### Return value

LOS ID.
## int getEntityID ( ) const

Returns the Entity ID specified in the packet.
### Return value

Entity ID.
> **Notice:** This parameter shall be ignored if [Source Point Coordinate System](#getSrcCoordSystem_int) is set to Geodetic (0).


## int getRequestType ( ) const

Returns the value of the **Request Type** parameter specified in the packet. Determines what type of response the IG will return for this request.
### Return value

Request Type parameter value. The following values are supported:
- 0 - Basic. The IG shall respond with a [Line of Sight Response](../../../../../api/library/plugins/ig/cigi/class.icigilosresponse_cpp.md) packet.
- 1 - Extended. The IG shall respond with a [Line of Sight Extended Response](../../../../../api/library/plugins/ig/cigi/class.icigilosextresponse_cpp.md) packet.


## int getSrcCoordSystem ( ) const

Returns the value of the **Source Point Coordinate System** parameter specified in the packet. This parameter indicates the coordinate system relative to which the test vector source point is specified.
### Return value

Source Point Coordinate System parameter value. The following values are supported:
- 0 - Geodetic. The point shall be given by latitude, longitude, and altitude. The vector, specified by Azimuth and Elevation, shall be defined relative to the Geodetic coordinate system.
- 1 - Entity. The point shall be defined relative to the reference point of the entity specified by [Entity ID](#getEntityID_int). The vector shall also be specified relative to the entity�s coordinate system.


## int getRespCoordSystem ( ) const

Returns the value of the **Response Coordinate System** parameter specified in the packet. This parameter specifies the coordinate system to be used in the response.
### Return value

Response Coordinate System parameter value. The following values are supported:
- 0 - Geodetic. The intersection point shall be reported as a latitude, longitude, and altitude.
- 1 - Entity. The intersection point shall be reported as an XYZ offset relative to the reference point of the intersected entity.


## int getAlphaThreshold ( ) const

Returns the value of the **Alpha Threshold** parameter specified in the packet. Defines the minimum alpha value (i.e., minimum opacity) a surface may have for an LOS response to be generated.
### Return value

Alpha Threshold parameter value.
## int getUpdatePeriod ( ) const

Returns the value of the **Update Period** parameter specified in the packet. Determines the interval between successive responses to this request.
### Return value

Update Period parameter value. The following values are supported:
- 0 - One-Shot request. The IG shall return a single response.
- >0 - Indicates update period. The value of n>0 indicates that the IG shall return response every n th frame.


## int getMaterialMask ( ) const

Returns the value of the **Material Mask** parameter specified in the packet. Determines the environmental and cultural features to be included in LOS segment testing.
### Return value

**Material Mask** parameter value. Each bit represents a material code range; setting that bit to one (1) shall cause the IG to register intersections with polygons whose material codes are within that range.
> **Notice:** Material code ranges are IG-dependent.


## float getAzimuth ( ) const

Returns the value of the **Azimuth** parameter specified in the packet. Determines the horizontal angle of the LOS test vector.
### Return value

Azimuth parameter value in the **[-180.0; 180.0]** range.
## float getElevation ( ) const

Returns the value of the **Elevation** parameter specified in the packet. Determines the vertical angle of the LOS test vector.
### Return value

Elevation parameter value in the **[-90.0; 90.0]** range.
## float getMinRange ( ) const

Returns the value of the **Minimum Range** parameter specified in the packet. Specifies minimum range along the LOS test vector at which intersection testing shall Maximum Range occur.
### Return value

Minimum Range parameter value which is greater than 0.
## float getMaxRange ( ) const

Returns the value of the **Maximum Range** parameter specified in the packet. Specifies the maximum range along the LOS test vector at which intersection testing shall occur.
### Return value

Maximum Range parameter value which is greater than the **Minimum Range** parameter value.
## Math:: dvec3 getPosition ( ) const

Returns the Source Point position represented as a three-component vector of the **Source Latitude, Source Longitude, Source Altitude** or **Source X Offset, Source Y Offset, Source Z Offset** parameters values specified in the packet corresponding to the value of [Source Point Coordinate System](#getSrcCoordSystem_int) parameter.
### Return value

Three-component coordinates vector:
- [Latitude, Longitude, Altitude] - if Source Point Coordinate System is set to Geodetic (0).
- [X Offset, Y Offset, Z Offset] - if Source Point Coordinate System is set to Entity (1).
