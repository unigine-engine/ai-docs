# CigiSymbolLineDef Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiSymbolLineDef Class

### Enums

## CIGI_LINE

| Name | Description |
|---|---|
| **CIGI_LINE_POINT** = 0 | Point primitive type. |
| **CIGI_LINE_LINE** = 1 | Line primitive type. |
| **CIGI_LINE_LINE_STRIP** = 2 | Line Strip primitive type. |
| **CIGI_LINE_LINE_LOOP** = 3 | Line Loop primitive type. |
| **CIGI_LINE_TRIANGLE** = 4 | Triangle primitive type. |
| **CIGI_LINE_TRIANGLE_STRIP** = 5 | Triangle Strip primitive type. |
| **CIGI_LINE_TRIANGLE_FAN** = 6 | Triangle fan primitive type. |

### Members

---

## int getSymbolID ( ) const

Returns the Symbol ID specified in the packet.
### Return value

Symbol ID.
## int getPrimitiveType ( ) const

Returns the **Primitive Type** specified in the packet. Determines the type of point or line primitive defined by this packet.
### Return value

Primitive Type parameter value. One of the [CIGI_LINE_*](#CIGI_LINE_POINT) values.
## int getStipplePattern ( ) const

Returns the value of the **Stipple Pattern** parameter specified in the packet. Determines the dash pattern to be used when drawing the line.
### Return value

Stipple Pattern parameter value.
> **Notice:** If the value of this parameter is 0xFFFF, then the IG shall draw a solid line. If the value is 0x00, then the IG shall not draw the line.


## float getPatternLength ( ) const

Returns the value of the **Stipple Pattern Length** parameter specified in the packet. Determines the length of one complete repetition of the stipple pattern.
### Return value

Pattern Length parameter value.
## float getLineWidth ( ) const

Returns the value of the **Line Width** parameter specified in the packet. Specifies the line thickness that the IG shall use when drawing the primitives defined in this packet.
### Return value

Line Width parameter value.
## int getNumVertex ( ) const

Returns the number of vertices in line. Determines the number of vertices by which the line is specified
### Return value

**Num Vertex**.
## Math:: vec3 getVertex ( int num ) const

Returns a three-component vector UV coordinates of the given vertex. This vector combines the values of the **Center U** and **Center V** parameters specified in the packet.
### Arguments

- *int* **num** - Index of vertex.

### Return value

Three-component vector with the UV coordinates of the given vertex **(Center U, Center V, Z)**, in symbol�s local coordinate system.
> **Notice:** The third component of the vector is ignored.
