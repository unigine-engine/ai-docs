# CigiWaveControl Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiWaveControl Class

### Members

---

## int getRegionID ( ) const

Returns the Environmental region ID specified in the packet.
### Return value


- **Entity ID** if [Scope](#getScope_int) is set to Entity (2).
- **Region ID** if [Scope](#getScope_int) is set to Regional (1).


> **Notice:** This value will be ignored if [Scope](#getScope_int) is set to Global (0).


## int getWaveID ( ) const

Returns the value of the **Wave ID** specified in the packet.
### Return value

**Wave ID** parameter value.
## int getWaveEnabled ( ) const

Returns the value of the **Wave Enable** parameter specified in the packet.
### Return value

**Wave Enable** parameter: 1 - wave is enabled and will contribute to the shape of water's surface; otherwise, 0.
## int getScope ( ) const

Returns the value of the **Scope** parameter specified in the packet. Determines whether the wave is defined for global, regional, or entity-controlled maritime surface conditions.
### Return value

**Scope** parameter value. The following values are supported:
- 0 - Global
- 1 - Regional
- 2 - Entity


## int getBreaker ( ) const

Returns the value of the **Breaker Type** parameter specified in the packet.
### Return value

**Breaker Type** parameter value. The following values are supported:
- 0 - Plunging. Plunging waves peak until the wave forms a vertical wall, at which point the crest moves faster than the base of the breaker. The wave shall then break violently into the wave trough.
- 1 - Spilling. Spilling breakers break gradually over a great distance. White water shall form over the crest, which spills down the face of the breaker.
- 2 - Surging. Surging breakers advance toward the beach as vertical walls of water. Unlike with plunging and spilling breakers, the crest shall not fall over the front of the wave.


## float getHeight ( ) const

Returns the value of the **Wave Height** parameter specified in the packet.
### Return value

**Wave Height** parameter value.
## float getLength ( ) const

Returns the value of the **Wavelength** parameter specified in the packet.
### Return value

**Wavelength** parameter value.
## float getPeriod ( ) const

Returns the value of the **Period** parameter specified in the packet. Determines the time required for one complete oscillation of the wave.
### Return value

**Period** parameter value.
## float getWindDirection ( ) const

Returns the value of the Wind **Direction** parameter specified in the packet. Determines the direction in which the wave propagates.
### Return value

**Direction** parameter value in the [0; 360] range.
## float getOffset ( ) const

Returns the value of the **Phase Offset** parameter specified in the packet. Determines the phase offset of the wave.
### Return value

**Phase Offset** parameter value in the [-360; 360] range.
## float getLeading ( ) const

Returns the value of the **Leading** parameter specified in the packet.
### Return value

**Leading** parameter value.
