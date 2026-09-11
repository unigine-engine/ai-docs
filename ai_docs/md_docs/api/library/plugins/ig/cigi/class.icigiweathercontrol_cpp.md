# CigiWeatherControl Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiWeatherControl Class

### Members

---

## int getRegionID ( ) const

Returns the Environmental region ID specified in the packet.
### Return value


- **Entity ID** if [Scope](#getScope_int) is set to Entity (2).
- **Region ID** if [Scope](#getScope_int) is set to Regional (1).


> **Notice:** This value will be ignored if [Scope](#getScope_int) is set to Global (0).


## int getLayerID ( ) const

Returns the layer ID specified in the packet.
### Return value

Layer ID. The following values are supported:
- 0 - Ground Fog
- 1 - Cloud Layer 1
- 2 - Cloud Layer 2
- 3 - Cloud Layer 3
- 4 - Rain
- 5 - Snow
- 6 - Sleet
- 7 - Hail
- 8 - Sand
- 9 - Dust
- 10 � 255 - Defined by IG


## int getWeatherEnabled ( ) const

Returns the value of the **Weather Enable** parameter specified in the packet.
### Return value

**Weather Enable** parameter value: 1 if a weather layer/entity and its atmospheric effects are enabled; otherwise, 0.
## int getScudEnabled ( ) const

Returns the value of the **Scud Enable** parameter specified in the packet.
### Return value

**Scud Enable** parameter value: 1 if the weather layer produces scud effects within its transition bands; otherwise, 0.
## int getWindEnabled ( ) const

Returns the value of the **Random Winds Enable** parameter specified in the packet.
### Return value

**Random Winds Enable** parameter value: 1 if a random frequency and duration will be applied to the local wind effects; otherwise, 0.
## int getLightingEnabled ( ) const

Returns the value of the **Random Lightning Enable** parameter specified in the packet.
### Return value

**Random Lightning Enable** parameter value: 1 if the weather layer or entity exhibits random lightning effects; otherwise, 0.
> **Notice:** The frequency and severity of the lightning shall vary according to the [Severity](#getSeverity_int) parameter


## int getCloudType ( ) const

Returns the value of the **Cloud Type** parameter specified in the packet.
### Return value

**Cloud Type** parameter value. The following values are supported:
- 0 - None
- 1 - Altocumulus
- 2 - Altostratus
- 3 - Cirrocumulus
- 4 - Cirrostratus
- 5 - Cirrus
- 6 - Cumulonimbus
- 7 - Cumulus
- 8 - Nimbostratus
- 9 - Stratocumulus
- 10 - Stratus
- 11 � 15 - Other


## int getScope ( ) const

Returns the value of the **Scope** parameter specified in the packet. Determines whether the weather is global, regional, or assigned to an entity.
### Return value

**Scope** parameter value. The following values are supported:
- 0 - Global
- 1 - Regional
- 2 - Entity


## int getSeverity ( ) const

Returns the value of the **Severity** parameter specified in the packet.
### Return value

**Severity** parameter value: 0 � 5 (least to most severe).
## int getHumidity ( ) const

Returns the value of the **Humidity** parameter specified in the packet.
### Return value

**Humidity** parameter value in the [0; 100] range.
## float getTemperature ( ) const

Returns the value of the **Air Temperature** parameter specified in the packet.
### Return value

**Air Temperature** parameter value, in degrees Celsius.
## float getVisibility ( ) const

Returns the value of the **Visibility Range** parameter specified in the packet.
### Return value

**Visibility Range** parameter value.
## float getScudFrequency ( ) const

Returns the value of the **Scud Frequency** parameter specified in the packet.
### Return value

**Scud Frequency** parameter value in the [0; 100] range.
## float getCoverage ( ) const

Returns the value of the **Coverage** parameter specified in the packet.
### Return value

**Coverage** parameter value in the [0; 100] range.
## float getElevation ( ) const

Returns the value of the **Base Elevation** parameter specified in the packet. Determines the altitude of the base (bottom) of the weather layer.
### Return value

**Base Elevation** parameter value.
## float getThickness ( ) const

Returns the value of the **Thickness** parameter specified in the packet. Determines the vertical thickness of the weather layer. The altitude of the top of the layer is equal to this value plus that specified by [Base Elevation](#getElevation_float).
### Return value

**Thickness** parameter value.
## float getWindSpeedHorizontal ( ) const

Returns the value of the **Horizontal Wind Speeed** parameter specified in the packet.
### Return value

**Horizontal Wind Speeed** parameter value.
## float getWindSpeedVertical ( ) const

Returns the value of the **Vertical Wind Speeed** parameter specified in the packet.
### Return value

**Vertical Wind Speeed** parameter value.
## float getWindDirection ( ) const

Returns the value of the **Wind Direction** parameter specified in the packet.
### Return value

**Wind Direction** parameter value in the [0; 360] range.
## float getPressure ( ) const

Returns the value of the **Barometric Pressure** parameter specified in the packet.
### Return value

**Barometric Pressure** parameter value.
## float getAerosol ( ) const

Returns the value of the **Aerosol Concentration** parameter specified in the packet. Determines the concentration of water, smoke, dust, or other particles suspended in the air.
> **Notice:** This parameter is provided primarily for sensor applications; any visual effect is secondary and is IG- and layer-dependent.


### Return value

**Aerosol Concentration** parameter value.
## float getTransitionThicknessTop ( ) const

Returns the thickness of the top **Transition Band** specified in the packet.
### Return value

Thickness of the top **Transition Band**, in meters.
## float getTransitionThicknessBottom ( ) const

Returns the thickness of the bottom **Transition Band** specified in the packet.
### Return value

Thickness of the bottom **Transition Band**, in meters.
