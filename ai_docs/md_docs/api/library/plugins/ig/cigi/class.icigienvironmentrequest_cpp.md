# CigiEnvironmentRequest Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiEnvironmentRequest Class

### Members

---

## int getRequestID ( ) const

Returns the value of the **Request ID** parameter specified in the packet. Identifies the environmental conditions request.
### Return value

Request ID.
## int getRequestType ( ) const

Returns the value of the **Request Type** parameter specified in the packet. Determines with which packet the IG shall respond.
### Return value

Request Type parameter value. The following values are supported:
- 1 - [Maritime Surface Conditions](../../../../../api/library/plugins/ig/cigi/class.icigimaritimeresponse_cpp.md).
- 2 - [Terrestrial Surface Conditions](../../../../../api/library/plugins/ig/cigi/class.icigiterrestrialresponse_cpp.md).
- 4 - [Weather Conditions](../../../../../api/library/plugins/ig/cigi/class.icigiweatherresponse_cpp.md).
- 8 - [Aerosol Concentration](../../../../../api/library/plugins/ig/cigi/class.icigiaerosolresponse_cpp.md).


## Math:: dvec3 getPosition ( ) const

Returns the three-component vector of the values of the **Latitude, Longitude and Altitude** parameters specified in the packet. Specifies the geodetic latitude, longitude, and altitude at which the environmental state is requested.
### Return value

Three-component vector of the **[Latitude, Longitude, Altitude]** parameters values.
