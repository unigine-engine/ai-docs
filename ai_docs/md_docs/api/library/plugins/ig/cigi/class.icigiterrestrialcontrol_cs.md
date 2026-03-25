# CigiTerrestrialControl Class (CS)

**Inherits from:** CigiHostPacket


## CigiTerrestrialControl Class

### Properties

## 🔒︎ int RegionID

The Environmental region ID specified in the packet.
## 🔒︎ int SurfaceID

The value of the **Surface Condition ID** specified in the packet. Determines surface condition or contaminant.
> **Notice:** Multiple conditions can be specified by sending multiple Terrestrial Surface Conditions Control packets.


## 🔒︎ int SurfaceEnabled

The value of the **Surface Condition Enable** parameter specified in the packet.
## 🔒︎ int Scope

The value of the **Scope** parameter specified in the packet. Determines whether the surface conditions are applied globally, regionally, or to an environmental entity.
## 🔒︎ int Severity

The value of the **Severity** parameter specified in the packet.
## 🔒︎ int Coverage

The value of the **Coverage** parameter specified in the packet. Determines the degree of coverage of the specified surface contaminant.
### Members

---
