# CigiEntityControl Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiEntityControl Class

### Enums

## CIGI_ENTITY

| Name | Description |
|---|---|
| **CIGI_ENTITY_NO_CLAMP** = 0 | Altitude clamping for entity is disabled. |
| **CIGI_ENTITY_NON_CONFORMAL** = 1 | Altitude parameter specifies an offset of the entity above the ground level. |
| **CIGI_ENTITY_CONFORMAL** = 2 | Altitude parameter specifies an offset of the entity above the sea level. |

## CIGI_ANIMATION

| Name | Description |
|---|---|
| **CIGI_ANIMATION_STOP** = 0 | Stop entity animation playback. |
| **CIGI_ANIMATION_PAUSE** = 1 | Pause entity animation playback. |
| **CIGI_ANIMATION_PLAY** = 2 | Start entity animation playback. |
| **CIGI_ANIMATION_CONTINUE** = 3 | Resume entity animation playback. |

### Members

---

## int getEntityID ( ) const

Returns the entity ID.
### Return value

Entity ID.
## int getParentID ( ) const

Returns the ID of the entity parent.
### Return value

Entity parent ID.
## int getEntityType ( ) const

Returns the current entity type.
### Return value

Entity type.
## int getEntityState ( ) const

Returns the current entity state.
### Return value

Current entity state. One of the [CIGI_STATE_*](../../../../../api/library/plugins/ig/cigi/class.cigi_connector_cpp.md#CIGI_STATE_DISABLED) values.
## int getAttachState ( ) const

Returns the value of the **Attach State** parameter. It specifies whether the entity is be attached as a child to a [parent](#getParentID_int).
### Return value

**Attach State** parameter value. 1 the entity shall be or remain attached to the entity specified by the [Parent ID parameter](#getParentID_int); 0 - the entity shall be detached from its parent.
## int getCollision ( ) const

Returns the value indicating if collision detecton shall be enabled for the entity.
### Return value

**Collision Detection Enable** parameter value. 1 collision detecton for the entity shall be enabled; 0 - collision detecton for the entity shall be enabled.
## int getInheritAlpha ( ) const

Returns the value indicating if the entity uses the alpha value of its [parent](#getParentID_int).
### Return value

1 if the entity uses the alpha value of its [parent](#getParentID_int); otherwise, 0.
## int getGroundClamp ( ) const

Returns the value of the **Ground/Ocean Clamp** parameter.
### Return value

**Ground/Ocean Clamp** parameter value. One of the [CIGI_ENTITY_*](#CIGI_ENTITY_NO_CLAMP) values.
## int getAnimationBack ( ) const

Returns the current entity's animation playback direction.
### Return value

Direction of the entity's animation playback (forward or backward).
## int getAnimationLoop ( ) const

Returns the current entity's animation playback mode.
### Return value

Mode of the entity's animation playback (single-shot or looped).
## int getAnimationState ( ) const

Returns the current entity's animation playback state.
### Return value

State of the entity's animation playback. One of the [CIGI_ANIMATION_*](#CIGI_ANIMATION_STOP) values.
## int getInterpolation ( ) const

Returns a value indicating if interpolation and extrapolation are enabled.
### Return value

1 if interpolation and extrapolation are enabled; otherwise, 0.
## int getAlpha ( ) const

Returns the current alpha value, that determines transparency of entity geometry.
### Return value

Alpha value.
## Math:: vec3 getRotation ( ) const

Returns the current entity rotation euler angles.
### Return value

Entity rotation euler angles (roll, pitch, yaw).
## Math:: vec3 getPosition ( ) const

Returns the current entity position.
### Return value

Entity position coordinates.
> **Notice:** Geo-coordinates will be returned if there is no parent entity assigned, otherwise - local coordinates will be returned.
