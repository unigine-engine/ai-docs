# CigiLosExtResponse Class (CS)

**Inherits from:** CigiIGPacket


## CigiLosExtResponse Class

### Members

---

## void SetLosID ( int id )

Sets the value of the **LOS ID** parameter to be specified in the packet.
### Arguments

- *int* **id** - **LOS ID** parameter value.

## void SetEntityID ( int id )

Sets the value of the **Entity ID** parameter to be specified in the packet.
### Arguments

- *int* **id** - **Entity ID** parameter value.

## void SetEntityValid ( int valid )

Sets the value of the **Entity Valid** parameter to be specified in the packet.
### Arguments

- *int* **valid** - **Entity ID Valid** parameter value. The following values are supported:

  - 0 - invalid (if the intersected polygon was not a part of an entity)
  - 1 - valid (if the intersected polygon was a part of an entity)

## void SetResponseValid ( int valid )

Sets the value of the **Response Valid** parameter to be specified in the packet.
### Arguments

- *int* **valid** - **Valid** parameter value. The following values are supported:

  - 0 - invalid (no intersection occurred)
  - 1 - valid (one or more intersections occurred)

## void SetResponseCount ( int count )

Sets the value of the **Response Count** parameter to be specified in the packet. This parameter indicates the total number of Line of Sight Response packets the IG will return for the corresponding request.
### Arguments

- *int* **count** - **Response Count** parameter value.

## void SetRangeValid ( int valid )

Sets the value of the **Range Valid** parameter to be specified in the packet.
### Arguments

- *int* **valid** - **Range Valid** parameter value. The following values are supported: The range will be invalid if an intersection occurs before the minimum range or beyond the maximum range specified in an LOS vector request. The range will also be invalid if this packet is in response to a LOS segment request.

  - 0 - invalid
  - 1 - valid

## void SetVisible ( int v )

Sets the value of the **Visible** parameter to be specified in the packet.
### Arguments

- *int* **v** - **Visible** parameter value. The following values are supported:

  - 0 - occluded (not visible)
  - 1 - visible

## void SetRange ( double r )

Sets the value of the **Range** parameter to be specified in the packet.
### Arguments

- *double* **r** - **Range** parameter value.

## void SetPosition ( dvec3 p )

Sets the values of parameters that determine the **Position** to be specified in the packet.
### Arguments

- *dvec3* **p** - Entity position coordinates.

  - For geodetic coordinate system: (Lat, Lon, Alt)
  - For entity coordinate system: (X-offset, Y-offset, Z-offset)

## void SetColor ( vec4 c )

Sets the values of parameters that determine the **Color** of the surface at the point of intersection to be specified in the packet.
### Arguments

- *vec4* **c** - Color of the surface at the point of intersection: (Red, Green, Blue, Alpha).

## void SetAzimuth ( float a )

Sets the value of the **Normal Vector Azimuth** parameter to be specified in the packet.
### Arguments

- *float* **a** - **Normal Vector Azimuth** parameter value.

## void SetElevation ( float e )

Sets the value of the **Normal Vector Elevation** parameter to be specified in the packet.
### Arguments

- *float* **e** - **Normal Vector Elevation** parameter value.

## void SetMaterialCode ( uint code )

Sets the value of the **Material Code** parameter to be specified in the packet.
### Arguments

- *uint* **code** - **Material Code** parameter value.
