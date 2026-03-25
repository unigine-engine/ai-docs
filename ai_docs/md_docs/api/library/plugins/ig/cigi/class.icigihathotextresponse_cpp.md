# CigiHatHotExtResponse Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>


## CigiHatHotExtResponse Class

### Members

---

## void setHatHotID ( int id )

Sets the value of the **HAT/HOT ID** parameter to be specified in the packet.
### Arguments

- *int* **id** - **HAT/HOT ID** parameter value.

## void setResponseValid ( int valid )

Sets the value of the **Response Valid** parameter to be specified in the packet.
### Arguments

- *int* **valid** - **Response Valid** parameter value. The following values are supported:

  - 0 - invalid (update period limit is exceeded)
  - 1 - valid (update period limit is not exceeded)

## void setHeightAbove ( double height )

Sets the value of the **HAT** parameter to be specified in the packet.
### Arguments

- *double* **height** - **HAT** parameter value.

## void setHeightOf ( double height )

Sets the value of the **HOT** parameter to be specified in the packet.
### Arguments

- *double* **height** - **HOT** parameter value.

## void setAzimuth ( float a )

Sets the value of the **Normal Vector Azimuth** parameter to be specified in the packet.
### Arguments

- *float* **a** - **Normal Vector Azimuth** parameter value.

## void setElevation ( float e )

Sets the value of the **Normal Vector Elevation** parameter to be specified in the packet.
### Arguments

- *float* **e** - **Normal Vector Elevation** parameter value.

## void setMaterialCode ( unsigned int valid )

Sets the value of the **Material Code** parameter to be specified in the packet.
### Arguments

- *unsigned int* **valid** - **Material Code** parameter value.
