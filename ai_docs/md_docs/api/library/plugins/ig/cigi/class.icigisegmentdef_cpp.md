# CigiSegmentDef Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiSegmentDef Class

### Members

---

## int getEntityID ( ) const

Returns the entity ID specified in the packet.
### Return value

Entity ID.
## int getSegmentID ( ) const

Returns the segment ID specified in the packet.
### Return value

Segment ID.
## int getSegmentEnabled ( ) const

Returns the value of the **Segment Enable** parameter specified in the packet.
### Return value

**Segment Enable** parameter: 1 - the segment will be considered during collision testing; otherwise, 0.
## unsigned int getMaterialMask ( ) const

Returns the value of the **Material Mask** parameter specified in the packet. Determines the environmental and cultural features to be included in or excluded from consideration for collision testing.
### Return value

**Material Mask** parameter value. Each bit represents a range of material code values. Setting that bit to 1 shall cause the IG to register hits with materials within the corresponding range. Setting this field to 0h has the effect of disabling collision testing for this segment.
## Math:: vec3 getPoint1 ( ) const

Returns the coordinates of the first point of the collision segment specified in the packet.
### Return value

Coordinates of the first point of the collision segment.
## Math:: vec3 getPoint2 ( ) const

Returns the coordinates of the second point of the collision segment specified in the packet.
### Return value

Coordinates of the second point of the collision segment.
