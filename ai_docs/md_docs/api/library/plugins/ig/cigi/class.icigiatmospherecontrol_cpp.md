# CigiAtmosphereControl Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiAtmosphereControl Class

### Members

---

## int getModelEnabled ( ) const

Returns the value of the **Atmospheric Model Enable** parameter specified in the packet.
### Return value

**Atmospheric Model Enable** parameter: 1 if the IG will use an atmospheric model to determine spectral radiances for sensor applications; otherwise, 0.
## int getHumidity ( ) const

Returns the value of the **Global Humidity** parameter specified in the packet.
### Return value

**Global Humidity** parameter value in the [0; 100] range.
## float getTemperature ( ) const

Returns the value of the **Global Air Temperature** parameter specified in the packet.
### Return value

**Global Air Temperature** parameter value, in degrees Celsius.
## float getVisibility ( ) const

Returns the value of the **Global Visibility Range** parameter specified in the packet.
### Return value

**Global Visibility Range** parameter value.
## float getWindSpeedHorizontal ( ) const

Returns the value of the **Global Horizontal Wind Speeed** parameter specified in the packet.
### Return value

**Global Horizontal Wind Speeed** parameter value.
## float getWindSpeedVertical ( ) const

Returns the value of the **Global Vertical Wind Speeed** parameter specified in the packet.
### Return value

**Global Vertical Wind Speeed** parameter value.
## float getWindDirection ( ) const

Returns the value of the **Global Wind Direction** parameter specified in the packet.
### Return value

**Global Wind Direction** parameter value in the [0; 360] range.
## float getPressure ( ) const

Returns the value of the **Global Barometric Pressure** parameter specified in the packet.
### Return value

**Global Barometric Pressure** parameter value.
