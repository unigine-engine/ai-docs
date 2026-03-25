# CigiEarthModelDef Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiEarthModelDef Class

### Members

---

## int getCustomEnabled ( ) const

Returns the value of the **Custom ERM Enable** parameter specified in the packet.
### Return value

**Custom ERM Enable** parameter value: 1 - the IG shall use the [Equatorial Radius](#getRadius_double) and [Flattening](#getFlattening_double) values to characterize the ellipsoid; 0 - the IG shall use the **WGS 84** reference model and all other parameters in this packet shall be ignored.
## double getRadius ( ) const

Returns the value of the **Equatorial Radius** parameter specified in the packet.
### Return value

**Equatorial Radius** parameter value. Determines the semi-major axis of the ellipsoid.
## double getFlattening ( ) const

Returns the value of the **Flattening** parameter specified in the packet.
### Return value

**Flattening** parameter value. Determines the flattening of the ellipsoid.
