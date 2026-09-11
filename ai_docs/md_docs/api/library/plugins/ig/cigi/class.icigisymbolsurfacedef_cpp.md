# CigiSymbolSurfaceDef Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiSymbolSurfaceDef Class

### Members

---

## int getSurfaceID ( ) const

Returns the **Surface ID** specified in the packet.
### Return value

Surface ID.
## int getEntityID ( ) const

Returns the **Entity ID** specified in the packet.
### Return value

Entity ID.
## int getSurfaceState ( ) const

Returns the value of the **Surface State** parameter specified in the packet. Defines whether the surface will be active.
### Return value

Surface State parameter value: 1 (Active) if the surface is enabled; otherwise, 0 (Destroyed).
## int getAttachType ( ) const

Returns the value of the **Attach Type** parameter specified in the packet. Determines whether the surface will be attached to an entity or a view.
### Return value

Attach Type parameter value: 0 (Entity) specified by the [Entity ID](#getEntityID_int) parameter; otherwise, 1 (View).
> **Notice:** If the specified entity or view does not exist, this packet shall be ignored.


## int getBillboard ( ) const

Returns the value of the **Billboard** parameter specified in the packet. Determines the way of surface orientation.
### Return value

Billboard parameter value. The following values are supported:
- 1 � Billboard. The surface shall be oriented such that the normal vector from the center of the surface is parallel to the viewing vector.
- 0 - Non-Billboard. The surface shall be oriented in relation to the entity�s local coordinate system by the Yaw, Pitch, and Roll parameters.


> **Notice:** If the surface is attached to a view, then the IG shall ignore this parameter.


## int getPerspective ( ) const

Returns the value of the **Perspective Growth Enable** parameter specified in the packet.
### Return value

**Perspective Growth Enable** parameter: 1 (Enabled) if the perspective growth is enabled; otherwise, 0 (Disabled).
## Math:: vec3 getOffset ( ) const

Returns the offset of the given surface as a three-component vector of **X Offset, Y Offset and Z Offset** or **Left, Right and Top** parameters specified in the packet.
### Return value

Three-component vector:
- [X Offset, Y Offset, Z Offset] - if the surface is attached to an entity. The values are relative to the entity�s reference point.
- [Left, Right, Top] - if the surface is attached to a view. The IG shall place it at this distance from the left edge of the viewport to the surface�s leftmost and rightmost boundary and from the bottom edge of the viewport to the surface�s topmost boundary respectively. This distance is measured as a fraction of the viewport�s width.


## Math:: vec3 getRotation ( ) const

Returns the orientation of the given surface as a three-component vector of **Yaw, Pitch and Roll** parameters (for Entity-attached surfaces) and value of **Bottom** parameter (for View-attached surfaces) specified in the packet.
### Return value

Three-component vector. [Yaw, Pitch, Roll] values - if the surface is attached to an entity; otherwise, [Bottom, Y, Z].
> **Notice:** If the given surface is attached to View, than the last two components of the vector shall be ignored.


## float getWidth ( ) const

Returns the value of the **Width** parameter specified in the packet.
### Return value

**Width** parameter value in the [0.0; 180.0] range for surfaces which are entity-attached Billboards with disabled [Perspective Growth](#getPerspective_int); the value is **greater than 0** for entity-attached Billboards with enabled [Perspective Growth](#getPerspective_int) and Non-Billboards.
## float getHeight ( ) const

Returns the value of the **Height** parameter specified in the packet.
### Return value

**Height** parameter value in the [0.0; 180.0] range for surfaces which are Billboards, Entity-attached with disabled [Perspective Growth](#getPerspective_int); the value is **greater than 0** for entity-attached Billboards with enabled [Perspective Growth](#getPerspective_int) and Non-Billboards.
## Math:: vec3 getMin ( ) const

Returns the three-component vector that contains the values of the **Min U, Min V** parameters specified in the packet. Specifies the UV coordinates that shall correspond to the leftmost and bottommost boundaries of the symbol surface.
### Return value

Three-component vector of the [Min U, Min V] parameters values.
## Math:: vec3 getMax ( ) const

Returns the three-component vector that contains the values of the **Max U, Max V** parameters specified in the packet. Specifies the UV coordinates that shall correspond to the rightmost and topmost boundaries of the symbol surface.
### Return value

Three-component vector of the [Max U, Max V] parameters values.
