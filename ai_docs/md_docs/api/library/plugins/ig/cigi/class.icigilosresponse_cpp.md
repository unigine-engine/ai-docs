# CigiLosResponse Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>


## CigiLosResponse Class

### Members

---

## void setLosID ( int id )

Sets the value of the **LOS ID** parameter to be specified in the packet.
### Arguments

- *int* **id** - **LOS ID** parameter value.

## void setEntityID ( int id )

Sets the value of the **Entity ID** parameter to be specified in the packet.
### Arguments

- *int* **id** - **Entity ID** parameter value.

## void setEntityValid ( int valid )

Sets the value of the **Entity Valid** parameter to be specified in the packet.
### Arguments

- *int* **valid** - **Entity ID Valid** parameter value. The following values are supported:

  - 0 - invalid (if the intersected polygon was not a part of an entity)
  - 1 - valid (if the intersected polygon was a part of an entity)

## void setResponseValid ( int valid )

Sets the value of the **Response Valid** parameter to be specified in the packet.
### Arguments

- *int* **valid** - **Valid** parameter value. The following values are supported:

  - 0 - invalid (no intersection occurred)
  - 1 - valid (one or more intersections occurred)

## void setResponseCount ( int count )

Sets the value of the **Response Count** parameter to be specified in the packet. This parameter indicates the total number of Line of Sight Response packets the IG will return for the corresponding request.
### Arguments

- *int* **count** - **Response Count** parameter value.

## void setVisible ( int v )

Sets the value of the **Visible** parameter to be specified in the packet.
### Arguments

- *int* **v** - **Visible** parameter value. The following values are supported:

  - 0 - occluded (not visible)
  - 1 - visible

## void setRange ( double range )

Sets the value of the **Range** parameter to be specified in the packet.
### Arguments

- *double* **range** - **Range** parameter value.
