# CigiSegmentDef Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** CigiHostPacket


## CigiSegmentDef Class

### Members

---

## int getEntityID ( )

Returns the entity ID specified in the packet.
### Return value

Entity ID.
## int getSegmentID ( )

Returns the segment ID specified in the packet.
### Return value

Segment ID.
## int getSegmentEnabled ( )

Returns the value of the **Segment Enable** parameter specified in the packet.
### Return value

**Segment Enable** parameter: 1 - the segment will be considered during collision testing; otherwise, 0.
## unsigned int getMaterialMask ( )

Returns the value of the **Material Mask** parameter specified in the packet. Determines the environmental and cultural features to be included in or excluded from consideration for collision testing.
### Return value

**Material Mask** parameter value. Each bit represents a range of material code values. Setting that bit to 1 shall cause the IG to register hits with materials within the corresponding range. Setting this field to 0h has the effect of disabling collision testing for this segment.
## getPoint1 ( )

Returns the coordinates of the first point of the collision segment specified in the packet.
### Return value

Coordinates of the first point of the collision segment.
## getPoint2 ( )

Returns the coordinates of the second point of the collision segment specified in the packet.
### Return value

Coordinates of the second point of the collision segment.
