# CigiEnvironmentPolygonControl Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiEnvironmentPolygonControl Class

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


## float getTransition ( ) const

Returns the value of the **Transition Perimeter** parameter specified in the packet. Determines the transition perimeter around the environmental region. This perimeter is a region through which the weather conditions are interpolated between those inside the environmental region and those immediately outside the perimeter.
### Return value

**Transition Perimeter** parameter value.
## Vector < Math:: dvec2 > getPolygonGeoPoints ( ) const

Returns the list of geocoordinates of vertices forming the polygon environmental region specified in the packet.
### Return value

Array of polygon vertex geocoordinates.
