# CigiHatHotRequest Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiHatHotRequest Class

### Members

---

## int getHatHotID ( ) const

Returns the value of the **HAT/HOT ID** parameter specified in the packet.
### Return value

**HAT/HOT ID** parameter value.
## int getEntityID ( ) const

Returns the entity ID specified in the packet.
### Return value

Entity ID.
## int getRequestType ( ) const

Returns the value of the **Request Type** parameter specified in the packet.
### Return value

**Request Type** parameter value. The following values are supported:
- 0 - HAT
- 1 - HOT
- 2 - Extended


## int getCoordSystem ( ) const

Returns the value of the **Coordinate System** parameter specified in the packet.
### Return value

**Coordinate System** parameter value. The following values are supported:
- 0 - Geodetic
- 1 - Entity


## int getUpdatePeriod ( ) const

Returns the value of the **Update Period** parameter specified in the packet. Determines the interval between successive responses to this request.
### Return value

**Update Period** parameter value:
- 0 - One-Shot request
- > 0 - update period


## Math:: dvec3 getPosition ( ) const

Returns the coordinates of the point, from which the HAT/HOT request is being made.
### Return value

Coordinates of the point, from which the HAT/HOT request is being made.
