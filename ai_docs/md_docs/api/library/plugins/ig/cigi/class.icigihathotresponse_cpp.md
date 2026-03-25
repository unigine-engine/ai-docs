# CigiHatHotResponse Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>


## CigiHatHotResponse Class

### Members

---

## void setHatHotID ( int id )

Sets the value of the **HAT/HOT ID** parameter to be specified in the packet.
### Arguments

- *int* **id** - **HAT/HOT ID** parameter value.

## void setResponseType ( int type )

Sets the value of the **Response Type** parameter to be specified in the packet.
### Arguments

- *int* **type** - **Response Type** parameter value. The following values are supported:

  - 0 - HAT
  - 1 - HOT

## void setResponseValid ( int valid )

Sets the value of the **Response Valid** parameter to be specified in the packet.
### Arguments

- *int* **valid** - **Response Valid** parameter value. The following values are supported:

  - 0 - invalid (update period limit is exceeded)
  - 1 - valid (update period limit is not exceeded)

## void setHeight ( double height )

Sets the value of the **Height** parameter to be specified in the packet.
### Arguments

- *double* **height** - **Height** parameter value.
