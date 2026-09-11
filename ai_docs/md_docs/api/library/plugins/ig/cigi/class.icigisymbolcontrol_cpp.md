# CigiSymbolControl Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiSymbolControl Class

### Members

---

## int getSymbolID ( ) const

Returns the **Symbol ID** specified in the packet. Determines the symbol to which this packet shall be applied.
### Return value

Symbol ID.
## int getParentID ( ) const

Returns the **Parent Symbol ID** specified in the packet. Determines the parent to which the IG shall attach the symbol.
### Return value

Parent ID.
## int getSurfaceID ( ) const

Returns the **Surface ID** specified in the packet. Determines the symbol surface on which the IG shall draw the symbol.
### Return value

Surface ID.
## int getSymbolState ( ) const

Returns the value of the **Symbol State** parameter specified in the packet. Determines whether the symbol is hidden, visible, or destroyed.
### Return value

Symbol State parameter. The following values are supported:
- 0 - Hidden.
- 1 - Visible.
- 2 - Destroyed.


## int getAttachState ( ) const

Returns the value of the **Attach State** parameter specified in the packet. Determines whether the symbol will be attached as a child to a parent symbol.
### Return value

Attach State parameter value: 1 if the symbol is to be attached to a parent; otherwise, 0.
## int getFlashControl ( ) const

Returns the value of the **Flash Control** parameter specified in the packet. Determines whether the IG shall continue the symbol�s flash cycle from its present state or restart it from the beginning.
### Return value

Flash Control parameter value. One of the following values:
- 0 - continue
- 1 - restart


## int getInheritColor ( ) const

Returns the value of the **Inherit Color** parameter specified in the packet. Determines whether the symbol inherits its color from the symbol to which it is attached.
### Return value

Inherit Color parameter value: 1 if the color is inherited; otherwise, 0.
## int getLayer ( ) const

Returns the value of the **Layer** parameter specified in the packet. Determines the layer to which the symbol shall be assigned.
### Return value

Layer parameter value in the [0 - 255] range.
## int getFlashDuty ( ) const

Returns the value of the **Flash Duty Cycle Percentage** parameter specified in the packet. Determines the duty cycle for a flashing symbol, measured as a percentage of the flash period.
### Return value

Flash Duty parameter value in the [0 - 100] range.
## float getFlashPeriod ( ) const

Returns the value of the **Flash Period** parameter specified in the packet. This parameter specifies the duration of a single flash cycle. The IG makes the symbol visible for the duration of the duty cycle period and invisible for the remainder of the flash period.
### Return value

Flash Period parameter value.
## float getRotation ( ) const

Returns the value of the **Rotation** parameter specified in the packet. Determines the contrast of the sensor display.
### Return value

Rotation parameter value in the [0.0; 1.0] range.
## Math:: vec3 getPosition ( ) const

Returns the UV position of the symbol as a three-component vector combining **Position U and Position V** parameters specified in the packet.
### Return value

UV position of the symbol. The first two components specify the coordinates position of the symbol along U and V axes. The third component shall be ignored.
> **Notice:** For top-level (non-child) symbols, the IG defines position of the symbol with respect to the symbol surface�s 2D coordinate system.
>
>
> For child symbols - with respect to the parent symbol�s local coordinate system.


## Math:: vec3 getScale ( ) const

Returns the scale vector of the symbol as a three-component vector combining **Scale U and Scale V** parameters specified in the packet.
### Return value

**Scale** vector for the symbol. The first two components specify scaling factors of the symbol along its local U and V axes. The third component shall be ignored.
## Math:: vec4 getColor ( ) const

Returns the color of the symbol as a four-component vector combining **Red, Green, Blue, and Alpha** parameters specified in the packet.
### Return value

Four-component vector representing symbol color (Red, Green, Blue, Alpha).
