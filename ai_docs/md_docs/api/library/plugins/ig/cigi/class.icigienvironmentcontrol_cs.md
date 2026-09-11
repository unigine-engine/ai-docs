# CigiEnvironmentControl Class (CS)

**Inherits from:** CigiHostPacket


## CigiEnvironmentControl Class

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
## 🔒︎ double Latitude

The value of the **Latitude** parameter specified in the packet.
## 🔒︎ double Longitude

The value of the **Longitude** parameter specified in the packet.
## 🔒︎ float SizeX

The value of the **Size X** parameter specified in the packet. Determines the length of the environmental region along its X-axis at the geoid surface.
> **Notice:** This length does not include the width of the transition perimeter.


## 🔒︎ float SizeY

The value of the **Size Y** parameter specified in the packet. Determines the length of the environmental region along its Y-axis at the geoid surface.
> **Notice:** This length does not include the width of the transition perimeter.


## 🔒︎ float Radius

The value of the **Corner Radius** parameter specified in the packet. Determines the radius of the corner of the rounded rectangle. The smaller the radius, the �tighter� the corner.
## 🔒︎ float Rotation

The value of the **Rotation** parameter specified in the packet. Determines the yaw angle of the rounded rectangle.
## 🔒︎ float Transition

The value of the **Transition Perimeter** parameter specified in the packet. Determines the transition perimeter around the environmental region. This perimeter is a region through which the weather conditions are interpolated between those inside the environmental region and those immediately outside the perimeter.
### Members

---
