# CigiSymbolControl Class (CS)

**Inherits from:** CigiHostPacket


## CigiSymbolControl Class

### Properties

## 🔒︎ int SymbolID

The **Symbol ID** specified in the packet. Determines the symbol to which this packet shall be applied.
## 🔒︎ int ParentID

The **Parent Symbol ID** specified in the packet. Determines the parent to which the IG shall attach the symbol.
## 🔒︎ int SurfaceID

The **Surface ID** specified in the packet. Determines the symbol surface on which the IG shall draw the symbol.
## 🔒︎ int SymbolState

The value of the **Symbol State** parameter specified in the packet. Determines whether the symbol is hidden, visible, or destroyed.
## 🔒︎ int AttachState

The value of the **Attach State** parameter specified in the packet. Determines whether the symbol will be attached as a child to a parent symbol.
## 🔒︎ int FlashControl

The value of the **Flash Control** parameter specified in the packet. Determines whether the IG shall continue the symbol�s flash cycle from its present state or restart it from the beginning.
## 🔒︎ int InheritColor

The value of the **Inherit Color** parameter specified in the packet. Determines whether the symbol inherits its color from the symbol to which it is attached.
## 🔒︎ int Layer

The value of the **Layer** parameter specified in the packet. Determines the layer to which the symbol shall be assigned.
## 🔒︎ int FlashDuty

The value of the **Flash Duty Cycle Percentage** parameter specified in the packet. Determines the duty cycle for a flashing symbol, measured as a percentage of the flash period.
## 🔒︎ float FlashPeriod

The value of the **Flash Period** parameter specified in the packet. This parameter specifies the duration of a single flash cycle. The IG makes the symbol visible for the duration of the duty cycle period and invisible for the remainder of the flash period.
## 🔒︎ float Rotation

The value of the **Rotation** parameter specified in the packet. Determines the contrast of the sensor display.
## 🔒︎ vec3 Position

The Returns the UV position of the symbol as a three-component vector combining **Position U and Position V** parameters specified in the packet.
> **Notice:** For top-level (non-child) symbols, the IG defines position of the symbol with respect to the symbol surface�s 2D coordinate system.
>
>
> For child symbols - with respect to the parent symbol�s local coordinate system.


## 🔒︎ vec3 Scale

The scale vector of the symbol as a three-component vector combining **Scale U and Scale V** parameters specified in the packet.
## 🔒︎ vec4 Color

The color of the symbol as a four-component vector combining **Red, Green, Blue, and Alpha** parameters specified in the packet.
### Members

---
