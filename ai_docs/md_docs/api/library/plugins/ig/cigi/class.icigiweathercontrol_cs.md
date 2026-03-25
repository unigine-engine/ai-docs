# CigiWeatherControl Class (CS)

**Inherits from:** CigiHostPacket


## CigiWeatherControl Class

### Properties

## 🔒︎ int RegionID

The Environmental region ID specified in the packet.
## 🔒︎ int LayerID

The layer ID specified in the packet.
## 🔒︎ int WeatherEnabled

The value of the **Weather Enable** parameter specified in the packet.
## 🔒︎ int ScudEnabled

The value of the **Scud Enable** parameter specified in the packet.
## 🔒︎ int WindEnabled

The value of the **Random Winds Enable** parameter specified in the packet.
## 🔒︎ int LightingEnabled

The value of the **Random Lightning Enable** parameter specified in the packet.
## 🔒︎ int CloudType

The value of the **Cloud Type** parameter specified in the packet.
## 🔒︎ int Scope

The value of the **Scope** parameter specified in the packet. Determines whether the weather is global, regional, or assigned to an entity.
## 🔒︎ int Severity

The value of the **Severity** parameter specified in the packet.
## 🔒︎ int Humidity

The value of the **Humidity** parameter specified in the packet.
## 🔒︎ float Temperature

The value of the **Air Temperature** parameter specified in the packet.
## 🔒︎ float Visibility

The value of the **Visibility Range** parameter specified in the packet.
## 🔒︎ float ScudFrequency

The value of the **Scud Frequency** parameter specified in the packet.
## 🔒︎ float Coverage

The value of the **Coverage** parameter specified in the packet.
## 🔒︎ float Elevation

The value of the **Base Elevation** parameter specified in the packet. Determines the altitude of the base (bottom) of the weather layer.
## 🔒︎ float Thickness

The value of the **Thickness** parameter specified in the packet. Determines the vertical thickness of the weather layer. The altitude of the top of the layer is equal to this value plus that specified by [Base Elevation](#getElevation_float).
## 🔒︎ float TransitionThicknessTop

The thickness of the top **Transition Band** specified in the packet.
## 🔒︎ float TransitionThicknessBottom

The thickness of the bottom **Transition Band** specified in the packet.
## 🔒︎ float Aerosol

The value of the **Aerosol Concentration** parameter specified in the packet. Determines the concentration of water, smoke, dust, or other particles suspended in the air.
> **Notice:** This parameter is provided primarily for sensor applications; any visual effect is secondary and is IG- and layer-dependent.


## 🔒︎ float Pressure

The value of the **Barometric Pressure** parameter specified in the packet.
## 🔒︎ float WindDirection

The value of the **Wind Direction** parameter specified in the packet.
## 🔒︎ float WindSpeedVertical

The value of the **Vertical Wind Speeed** parameter specified in the packet.
## 🔒︎ float WindSpeedHorizontal

The value of the **Horizontal Wind Speeed** parameter specified in the packet.
### Members

---
