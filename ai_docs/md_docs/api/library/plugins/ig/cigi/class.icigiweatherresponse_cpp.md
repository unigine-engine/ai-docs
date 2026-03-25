# CigiWeatherResponse Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>


## CigiWeatherResponse Class

### Members

---

## void setRequestID ( int id )

Sets the value of the **Request ID** parameter to be specified in the packet.
### Arguments

- *int* **id** - **Request ID** parameter value.

## void setHumidity ( int h )

Sets the value of the **Humidity** parameter to be specified in the packet.
### Arguments

- *int* **h** - **Humidity** parameter value in the [0; 100] range.

## void setTemperature ( float t )

Sets the value of the **Air Temperature** parameter to be specified in the packet.
### Arguments

- *float* **t** - **Air Temperature** parameter value, in degrees Celsius.

## void setVisibility ( float v )

Sets the value of the **Visibility Range** parameter to be specified in the packet.
### Arguments

- *float* **v** - **Visibility Range** parameter value.

## void setHorizontal ( float h )

Sets the value of the **Horizontal Wind Speeed** parameter to be specified in the packet.
### Arguments

- *float* **h** - **Horizontal Wind Speeed** parameter value.

## void setVertical ( float v )

Sets the value of the **Vertical Wind Speeed** parameter to be specified in the packet.
### Arguments

- *float* **v** - **Vertical Wind Speeed** parameter value.

## void setDirection ( float d )

Sets the value of the **Wind Direction** parameter to be specified in the packet.
### Arguments

- *float* **d** - **Wind Direction** parameter value in the [0; 360] range.

## void setPressure ( float p )

Sets the value of the **Barometric Pressure** parameter to be specified in the packet.
### Arguments

- *float* **p** - **Barometric Pressure** parameter value.
