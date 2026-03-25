# CigiLosVectorRequest Class (CS)

**Inherits from:** CigiHostPacket


## CigiLosVectorRequest Class

### Properties

## 🔒︎ int LosID

The LOS ID specified in the packet.
## 🔒︎ int EntityID

The Entity ID specified in the packet.
## 🔒︎ int RequestType

The value of the **Request Type** parameter specified in the packet. Determines what type of response the IG will return for this request.
## 🔒︎ int SrcCoordSystem

The value of the **Source Point Coordinate System** parameter specified in the packet. This parameter indicates the coordinate system relative to which the test vector source point is specified.
## 🔒︎ int RespCoordSystem

The value of the **Response Coordinate System** parameter specified in the packet. This parameter specifies the coordinate system to be used in the response.
## 🔒︎ int AlphaThreshold

The value of the **Alpha Threshold** parameter specified in the packet. Defines the minimum alpha value (i.e., minimum opacity) a surface may have for an LOS response to be generated.
## 🔒︎ int UpdatePeriod

The value of the **Update Period** parameter specified in the packet. Determines the interval between successive responses to this request.
## 🔒︎ int MaterialMask

The value of the **Material Mask** parameter specified in the packet. Determines the environmental and cultural features to be included in LOS segment testing.
## 🔒︎ float Azimuth

The value of the **Azimuth** parameter specified in the packet. Determines the horizontal angle of the LOS test vector.
## 🔒︎ float Elevation

The value of the **Elevation** parameter specified in the packet. Determines the vertical angle of the LOS test vector.
## 🔒︎ float MinRange

The value of the **Minimum Range** parameter specified in the packet. Specifies minimum range along the LOS test vector at which intersection testing shall Maximum Range occur.
## 🔒︎ float MaxRange

The value of the **Maximum Range** parameter specified in the packet. Specifies the maximum range along the LOS test vector at which intersection testing shall occur.
## 🔒︎ dvec3 Position

The Source Point position represented as a three-component vector of the **Source Latitude, Source Longitude, Source Altitude** or **Source X Offset, Source Y Offset, Source Z Offset** parameters values specified in the packet corresponding to the value of [Source Point Coordinate System](#getSrcCoordSystem_int) parameter.
### Members

---
