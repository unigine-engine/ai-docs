# CigiTerrestrialResponse Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>


## CigiTerrestrialResponse Class

### Members

---

## void setRequestID ( int id )

Sets the value of the **Request ID** parameter to be specified in the packet.
### Arguments

- *int* **id** - **Request ID** parameter value.

## void setSurfaceID ( int id )

Sets the value of the **Surface Condition ID** parameter to be specified in the packet.
### Arguments

- *int* **id** - **Surface Condition ID** parameter value in the [0, 65535] range. > **Notice:** Used to indicate the presence of a specific surface condition or contaminant at the test point. Surface condition codes are IG-dependent.
