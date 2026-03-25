# CigiSymbolCircleDef Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiSymbolCircleDef Class

### Members

---

## int getSymbolID ( ) const

Returns the **Symbol ID** specified in the packet.
### Return value

Symbol ID.
## int getDrawStyle ( ) const

Returns the value of the **Drawing Style** parameter specified in the packet. Determines whether the circles and arcs defined in this packet are defined as curved lines or filled volumes.
### Return value

Draw Style parameter value. The following values are supported:
- 0 - Line.
- 1 - Fill.


## int getStipplePattern ( ) const

Returns the value of the **Stipple Pattern** parameter specified in the packet. Specifies the dash pattern to be used when drawing the curved line of a circle or arc.
### Return value

**Stipple Pattern** parameter value.
> **Notice:** If the value of this parameter is 0xFFFF, then the IG shall draw a solid line. If the value is 0x00, then the IG shall not draw the line.


## float getPatternLength ( ) const

Returns the value of the **Stipple Pattern Length** parameter specified in the packet. Specifies the length of one complete repetition of the stipple pattern.
### Return value

Stipple Pattern Length parameter, in symbol surface units.
## float getLineWidth ( ) const

Returns the value of the **Line Width** parameter specified in the packet. Specifies the line thickness that the IG shall use when drawing the circles and arcs defined in this packet.
### Return value

Line Width parameter value, in symbol surface units.
## int getNumCircles ( ) const

Returns the number of circles in the instance.
### Return value

Number of circles.
## Math:: vec3 getCenter ( int num ) const

Returns a three-component vector with the UV coordinates of the center of the given circle. This vector combines the values of the **Center U** and **Center V** parameters specified in the packet.
### Arguments

- *int* **num** - Index of circle.

### Return value

Three-component vector with the UV coordinates of the center of the given circle **(Center U, Center V, Z)**.
> **Notice:** The third component of the vector is ignored.


## float getOuterRadius ( int num ) const

Returns the value of the **Radius** parameter specified in the packet. Determines the radius of the outer circumference of the given circle or arc.
### Arguments

- *int* **num** - Index of circle.

### Return value

Radius parameter value which is greater than InnerRadius parameter value.
## float getInnerRadius ( int num ) const

Returns the value of the **Inner Radius** parameter specified in the packet. Determines the inner radius of the given filled circle or arc.
### Arguments

- *int* **num** - Index of circle.

### Return value

Inner Radius parameter value which is >0.
## float getStartAngle ( int num ) const

Returns the value of the **Start Angle** parameter specified in the packet. Determines the starting angle of the given arc.
### Arguments

- *int* **num** - Index of circle.

### Return value

Start Angle parameter value.
## float getEndAngle ( int num ) const

Returns the value of the **End Angle** parameter specified in the packet. Determines the ending angle of the given arc.
### Arguments

- *int* **num** - Index of circle.

### Return value

**End Angle** parameter value.
