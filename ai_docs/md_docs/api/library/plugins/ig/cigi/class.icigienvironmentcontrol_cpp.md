# CigiEnvironmentControl Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiEnvironmentControl Class

### Members

---

## int getRegionID ( ) const

Returns the Environmental region ID specified in the packet.
### Return value

Environmental region ID.
## int getRegionState ( ) const

Returns the Environmental region state specified in the packet.
### Return value

Environmental region state. The following values are supported:
- 0 - Inactive
- 1 - Active
- 2 - Destroyed


## int getMergeWeather ( ) const

Returns the value of the **Merge Weather Properties** parameter specified in the packet. Determines whether atmospheric conditions within this region will be merged with those of other regions within areas of overlap.
### Return value

**Merge Weather Properties** parameter value. The following values are supported:
- 1 - merge
- 0 - use the data from the last Weather Control packet.


## int getMergeAerosol ( ) const

Returns the value of the **Merge Aerosol Concentrations** parameter specified in the packet. Determines whether atmospheric conditions within this region will be merged with those of other regions within areas of overlap.
### Return value

**Merge Aerosol Concentrations** parameter value. The following values are supported:
- 1 - merge
- 0 - use the data from the last Weather Control packet.


## int getMergeMaritime ( ) const

Returns the value of the **Merge Maritime Surface Conditions** parameter specified in the packet. Determines whether the maritime surface conditions found within this region will be merged with those of other regions within areas of overlap.
### Return value

**Merge Maritime Surface Conditions** parameter value. The following values are supported:
- 1 - merge
- 0 - use the data from the last Maritime Surface Conditions Control packet.


## int getMergeTerrestrial ( ) const

Returns the value of the **Merge Terrestrial Surface Conditions** parameter specified in the packet. Determines whether the terrestrial surface conditions found within this region will be merged with those of other regions within areas of overlap.
### Return value

**Merge Terrestrial Surface Conditions** parameter value. The following values are supported:
- 1 - merge
- 0 - use the data from the last Terrestrial Surface Conditions Control packet.


## double getLatitude ( ) const

Returns the value of the **Latitude** parameter specified in the packet.
### Return value

**Latitude** parameter value.
## double getLongitude ( ) const

Returns the value of the **Longitude** parameter specified in the packet.
### Return value

**Longitude** parameter value.
## float getSizeX ( ) const

Returns the value of the **Size X** parameter specified in the packet. Determines the length of the environmental region along its X-axis at the geoid surface.
> **Notice:** This length does not include the width of the transition perimeter.


### Return value

**Size X** parameter value.
## float getSizeY ( ) const

Returns the value of the **Size Y** parameter specified in the packet. Determines the length of the environmental region along its Y-axis at the geoid surface.
> **Notice:** This length does not include the width of the transition perimeter.


### Return value

**Size Y** parameter value.
## float getRadius ( ) const

Returns the value of the **Corner Radius** parameter specified in the packet. Determines the radius of the corner of the rounded rectangle. The smaller the radius, the �tighter� the corner.
### Return value

**Corner Radius** parameter value.
## float getRotation ( ) const

Returns the value of the **Rotation** parameter specified in the packet. Determines the yaw angle of the rounded rectangle.
### Return value

**Rotation** parameter value.
## float getTransition ( ) const

Returns the value of the **Transition Perimeter** parameter specified in the packet. Determines the transition perimeter around the environmental region. This perimeter is a region through which the weather conditions are interpolated between those inside the environmental region and those immediately outside the perimeter.
### Return value

**Transition Perimeter** parameter value.
