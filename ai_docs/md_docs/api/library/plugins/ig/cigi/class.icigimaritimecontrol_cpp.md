# CigiMaritimeControl Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiMaritimeControl Class

### Members

---

## int getRegionID ( ) const

Returns the Environmental region ID specified in the packet.
### Return value


- **Entity ID** if [Scope](#getScope_int) is set to Entity (2).
- **Region ID** if [Scope](#getScope_int) is set to Regional (1).


> **Notice:** This value will be ignored if [Scope](#getScope_int) is set to Global (0).


## int getSurfaceEnabled ( ) const

Returns the value of the **Surface Conditions Enable** parameter specified in the packet.
### Return value

**Surface Conditions Enable** parameter value: 1 - surface conditions are to be defined by this packet; 0 - surface conditions within the region or entity will be the same as the global maritime surface conditions.
## int getWhitecapEnabled ( ) const

Returns the value of the **Whitecap Enable** parameter specified in the packet.
### Return value

**Whitecap Enable** parameter value: 1 if whitecaps are enabled; otherwise, 0.
## int getScope ( ) const

Returns the value of the **Scope** parameter specified in the packet. Determines whether the weather is global, regional, or assigned to an entity.
### Return value

**Scope** parameter value. The following values are supported:
- 0 - Global
- 1 - Regional
- 2 - Entity


## float getHeight ( ) const

Returns the value of the **Sea Surface Height** parameter to be specified in the packet.
### Return value

**Sea Surface Height** parameter value.
## float getTemperature ( ) const

Returns the value of the **Surface Water Temperature** parameter to be specified in the packet.
### Return value

**Surface Water Temperature** parameter value, in degrees Celsius.
## float getClarity ( ) const

Returns the value of the **Surface Clarity** parameter to be specified in the packet.
### Return value

**Surface Clarity** parameter value in the [0; 100] range.
