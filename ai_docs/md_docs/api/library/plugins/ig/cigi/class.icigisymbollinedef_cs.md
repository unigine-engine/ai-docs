# CigiSymbolLineDef Class (CS)

**Inherits from:** CigiHostPacket


## CigiSymbolLineDef Class

### Enums

## CIGI_LINE

| Name | Description |
|---|---|
| **POINT** = 0 | Point primitive type. |
| **LINE** = 1 | Line primitive type. |
| **LINE_STRIP** = 2 | Line Strip primitive type. |
| **LINE_LOOP** = 3 | Line Loop primitive type. |
| **TRIANGLE** = 4 | Triangle primitive type. |
| **TRIANGLE_STRIP** = 5 | Triangle Strip primitive type. |
| **TRIANGLE_FAN** = 6 | Triangle fan primitive type. |

### Properties

## 🔒︎ int SymbolID

The Symbol ID specified in the packet.
## 🔒︎ int PrimitiveType

The **Primitive Type** specified in the packet. Determines the type of point or line primitive defined by this packet.
## 🔒︎ int StipplePattern

The value of the **Stipple Pattern** parameter specified in the packet. Determines the dash pattern to be used when drawing the line.
## 🔒︎ float PatternLength

The value of the **Stipple Pattern Length** parameter specified in the packet. Determines the length of one complete repetition of the stipple pattern.
## 🔒︎ float LineWidth

The value of the **Line Width** parameter specified in the packet. Specifies the line thickness that the IG shall use when drawing the primitives defined in this packet.
## 🔒︎ int NumVertex

The number of vertices in line. Determines the number of vertices by which the line is specified
### Members

---

## vec3 GetVertex ( int num )

Returns a three-component vector UV coordinates of the given vertex. This vector combines the values of the **Center U** and **Center V** parameters specified in the packet.
### Arguments

- *int* **num** - Index of vertex.

### Return value

Three-component vector with the UV coordinates of the given vertex **(Center U, Center V, Z)**, in symbol�s local coordinate system.
> **Notice:** The third component of the vector is ignored.
