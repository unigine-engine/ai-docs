# CigiTerrestrialControl Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiTerrestrialControl Class

### Members

---

## int getRegionID ( ) const

Returns the Environmental region ID specified in the packet.
### Return value


- **Entity ID** if [Scope](#getScope_int) is set to Entity (2).
- **Region ID** if [Scope](#getScope_int) is set to Regional (1).


> **Notice:** This value will be ignored if [Scope](#getScope_int) is set to Global (0).


## int getSurfaceID ( ) const

Returns the value of the **Surface Condition ID** specified in the packet. Determines surface condition or contaminant.
> **Notice:** Multiple conditions can be specified by sending multiple Terrestrial Surface Conditions Control packets.


### Return value

**Surface Condition ID** parameter value. The following values are supported:
- **0** - Dry (reset).
- **> 0** - Defined by IG.


> **Notice:** When this parameter is set to Dry (0), all existing surface conditions will be removed within the specified scope.


## int getSurfaceEnabled ( ) const

Returns the value of the **Surface Condition Enable** parameter specified in the packet.
### Return value

**Surface Condition Enable** parameter: 1 - surface condition attribute identified by the [Surface Condition ID](#getSurfaceID_int) parameter shall be enabled; otherwise, 0.
## int getScope ( ) const

Returns the value of the **Scope** parameter specified in the packet. Determines whether the surface conditions are applied globally, regionally, or to an environmental entity.
### Return value

**Scope** parameter value. The following values are supported:
- 0 - Global
- 1 - Regional
- 2 - Entity


## int getSeverity ( ) const

Returns the value of the **Severity** parameter specified in the packet.
### Return value

**Severity** parameter value: 0 � 31 (least to most severe).
## int getCoverage ( ) const

Returns the value of the **Coverage** parameter specified in the packet. Determines the degree of coverage of the specified surface contaminant.
### Return value

**Coverage** parameter value in the [0; 100] range.
