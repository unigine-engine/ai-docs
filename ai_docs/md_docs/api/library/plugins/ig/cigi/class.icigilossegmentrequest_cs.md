# CigiLosSegmentRequest Class (CS)

**Inherits from:** CigiHostPacket


## CigiLosSegmentRequest Class

### Properties

## 🔒︎ int LosID

The LOS ID specified in the packet.
## 🔒︎ int SrcEntityID

The Source Entity ID specified in the packet.
## 🔒︎ int DestEntityID

The value of the **Destination Entity ID** parameter specified in the packet. Defines the entity to which the test segment endpoints shall be relative.
## 🔒︎ int SrcCoordSystem

The value of the **Source Point Coordinate System** parameter specified in the packet. It indicates the coordinate system relative to which the test segment source endpoint is specified.
## 🔒︎ int RequestType

The value of the **Request Type** parameter specified in the packet. Determines what type of response the IG will return for this request.
## 🔒︎ int DestCoordSystem

The value of the **Destination Point Coordinate System** parameter specified in the packet. It indicates the coordinate system relative to which the test segment destination endpoint is specified.
## 🔒︎ int RespCoordSystem

The value of the **Response Coordinate System** parameter specified in the packet. This value specifies the coordinate system to be used in the response.
## 🔒︎ int DestEntityValid

The value of the **Destination Entity ID Valid** parameter specified in the packet. Determines whether the [Destination Entity ID](#getDestEntityID_int) parameter contains a valid entity ID.
## 🔒︎ int AlphaThreshold

The value of the **Alpha Threshold** parameter specified in the packet. Defines the minimum alpha value (i.e., minimum opacity) a surface may have for an LOS response to be generated.
## 🔒︎ dvec3 DestPosition

The Three-component vector that defines Destination Point position. The following values are supported:
- [Latitude, Longitude, Altitude] - if Destination Point Coordinate System is set to Geodetic (0).
- [X Offset, Y Offset, Z Offset] - if Destination Point Coordinate System is set to Entity (1). This offset may be relative to either the source entity or destination entity, depending upon the value of the Destination Entity ID Valid flag.


## 🔒︎ dvec3 SrcPosition

The Three-component vector that defines Source Point position. The following values are supported:
- [Latitude, Longitude, Altitude] - if Source Point Coordinate System is set to Geodetic (0).
- [X Offset, Y Offset, Z Offset] - if Source Point Coordinate System is set to Entity (1).


## 🔒︎ int MaterialMask

The value of the **Material Mask** parameter specified in the packet. Specifies the environmental and cultural features to be included in LOS segment testing.
## 🔒︎ int UpdatePeriod

The value of the **Update Period** parameter specified in the packet. Specifies the interval between successive responses to this request.
### Members

---
