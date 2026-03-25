# CigiEnvironmentPolygonControl Class (CS)

**Inherits from:** CigiHostPacket


## CigiEnvironmentPolygonControl Class

### Properties

## 🔒︎ int RegionID

The Environmental region ID specified in the packet.
## 🔒︎ int RegionState

The Environmental region state specified in the packet.
## 🔒︎ int MergeWeather

The value of the **Merge Weather Properties** parameter specified in the packet. Determines whether atmospheric conditions within this region will be merged with those of other regions within areas of overlap.
## 🔒︎ int MergeAerosol

The value of the **Merge Aerosol Concentrations** parameter specified in the packet. Determines whether atmospheric conditions within this region will be merged with those of other regions within areas of overlap.
## 🔒︎ int MergeMaritime

The value of the **Merge Maritime Surface Conditions** parameter specified in the packet. Determines whether the maritime surface conditions found within this region will be merged with those of other regions within areas of overlap.
## 🔒︎ int MergeTerrestrial

The value of the **Merge Terrestrial Surface Conditions** parameter specified in the packet. Determines whether the terrestrial surface conditions found within this region will be merged with those of other regions within areas of overlap.
## 🔒︎ float Transition

The value of the **Transition Perimeter** parameter specified in the packet. Determines the transition perimeter around the environmental region. This perimeter is a region through which the weather conditions are interpolated between those inside the environmental region and those immediately outside the perimeter.
## 🔒︎ dvec2[] PolygonGeoPoints

The list of geocoordinates of vertices forming the polygon environmental region specified in the packet.
### Members

---
