# CigiSymbolSurfaceDef Class (CS)

**Inherits from:** CigiHostPacket


## CigiSymbolSurfaceDef Class

### Properties

## 🔒︎ int SurfaceID

The **Surface ID** specified in the packet.
## 🔒︎ int EntityID

The **Entity ID** specified in the packet.
## 🔒︎ int SurfaceState

The value of the **Surface State** parameter specified in the packet. Defines whether the surface will be active.
## 🔒︎ int AttachType

The value of the **Attach Type** parameter specified in the packet. Determines whether the surface will be attached to an entity or a view.
## 🔒︎ int Billboard

The value of the **Billboard** parameter specified in the packet. Determines the way of surface orientation.
## 🔒︎ int Perspective

The value of the **Perspective Growth Enable** parameter specified in the packet.
## 🔒︎ vec3 Offset

The offset of the given surface as a three-component vector of **X Offset, Y Offset and Z Offset** or **Left, Right and Top** parameters specified in the packet.
## 🔒︎ vec3 Rotation

The orientation of the given surface as a three-component vector of **Yaw, Pitch, and Roll** parameters (for Entity-attached surfaces) and value of **Bottom** parameter (for View-attached surfaces) specified in the packet.
## 🔒︎ float Width

The value of the **Width** parameter specified in the packet.
## 🔒︎ float Height

The value of the **Height** parameter specified in the packet.
## 🔒︎ vec3 Min

The three-component vector that contains the values of the **Min U, Min V** parameters specified in the packet. Specifies the UV coordinates that shall correspond to the leftmost and bottommost boundaries of the symbol surface.
## 🔒︎ vec3 Max

The three-component vector that contains the values of the **Max U, Max V** parameters specified in the packet. Specifies the UV coordinates that shall correspond to the rightmost and topmost boundaries of the symbol surface.
### Members

---
