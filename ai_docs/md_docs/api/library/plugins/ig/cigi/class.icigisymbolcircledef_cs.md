# CigiSymbolCircleDef Class (CS)

**Inherits from:** CigiHostPacket


## CigiSymbolCircleDef Class

### Properties

## 🔒︎ int SymbolID

The **Symbol ID** specified in the packet.
## 🔒︎ int DrawStyle

The value of the **Drawing Style** parameter specified in the packet. Determines whether the circles and arcs defined in this packet are defined as curved lines or filled volumes.
## 🔒︎ int StipplePattern

The value of the **Stipple Pattern** parameter specified in the packet. Specifies the dash pattern to be used when drawing the curved line of a circle or arc.
## 🔒︎ float PatternLength

The value of the **Stipple Pattern Length** parameter specified in the packet. Specifies the length of one complete repetition of the stipple pattern.
## 🔒︎ float LineWidth

The value of the **Line Width** parameter specified in the packet. Specifies the line thickness that the IG shall use when drawing the circles and arcs defined in this packet.
## 🔒︎ int NumCircles

The number of circles in the instance.
### Members

---

## vec3 GetCenter ( int num )

Returns a three-component vector with the UV coordinates of the center of the given circle. This vector combines the values of the **Center U** and **Center V** parameters specified in the packet.
### Arguments

- *int* **num** - Index of circle.

### Return value

Three-component vector with the UV coordinates of the center of the given circle **(Center U, Center V, Z)**.
> **Notice:** The third component of the vector is ignored.


## float GetOuterRadius ( int num )

Returns the value of the **Radius** parameter specified in the packet. Determines the radius of the outer circumference of the given circle or arc.
### Arguments

- *int* **num** - Index of circle.

### Return value

Radius parameter value which is greater than InnerRadius parameter value.
## float GetInnerRadius ( int num )

Returns the value of the **Inner Radius** parameter specified in the packet. Determines the inner radius of the given filled circle or arc.
### Arguments

- *int* **num** - Index of circle.

### Return value

Inner Radius parameter value which is >0.
## float GetStartAngle ( int num )

Returns the value of the **Start Angle** parameter specified in the packet. Determines the starting angle of the given arc.
### Arguments

- *int* **num** - Index of circle.

### Return value

Start Angle parameter value.
## float GetEndAngle ( int num )

Returns the value of the **End Angle** parameter specified in the packet. Determines the ending angle of the given arc.
### Arguments

- *int* **num** - Index of circle.

### Return value

**End Angle** parameter value.
