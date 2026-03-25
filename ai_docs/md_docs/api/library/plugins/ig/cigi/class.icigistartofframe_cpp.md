# CigiStartOfFrame Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>


## CigiStartOfFrame Class

### Members

---

## void setDatabase ( int db )

Sets the value of the **Database Number** parameter to be specified in the packet.
### Arguments

- *int* **db** - **Database Number** parameter value.

## void setIGMode ( int mode )

Sets the value of the **IG Mode** parameter to be specified in the packet.
### Arguments

- *int* **mode** - **IG Mode** parameter value. One of the [CIGI_MODE_*](../../../../../api/library/plugins/ig/cigi/class.cigi_connector_cpp.md#CIGI_MODE_STANDBY) values.

## void setIGStatus ( int mode )

Sets the value of the **IG Status** parameter to be specified in the packet.
### Arguments

- *int* **mode** - **IG Status** parameter value. The following values are supported:

  - 0 - normal
  - 1-255 - an error has occurred

## void setTimeValid ( int valid )

Sets the value of the **Timestamp Valid** parameter to be specified in the packet.
### Arguments

- *int* **valid** - **Timestamp Valid** parameter value.

## void setEarthModel ( int model )

Sets the value of the **Earth Reference Model** parameter to be specified in the packet.
### Arguments

- *int* **model** - **Earth Reference Model** parameter value. The following values are supported:

  - 0 - WGS 84
  - 1 - Host-defined

## void setIGFrame ( unsigned int frame )

Sets the value of the **IG Frame Number** parameter to be specified in the packet.
### Arguments

- *unsigned int* **frame** - **IG Frame Number** parameter value.

## void setTimeStamp ( unsigned int time )

Sets the value of the **Timestamp** parameter to be specified in the packet.
### Arguments

- *unsigned int* **time** - **Timestamp** parameter value.
