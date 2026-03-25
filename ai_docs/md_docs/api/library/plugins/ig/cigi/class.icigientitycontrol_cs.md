# CigiEntityControl Class (CS)

**Inherits from:** CigiHostPacket


## CigiEntityControl Class

### Enums

## CIGI_ENTITY

| Name | Description |
|---|---|
| **NO_CLAMP** = 0 | Altitude clamping for entity is disabled. |
| **NON_CONFORMAL** = 1 | Altitude parameter specifies an offset of the entity above the ground level. |
| **CONFORMAL** = 2 | Altitude parameter specifies an offset of the entity above the sea level. |

## CIGI_ANIMATION

| Name | Description |
|---|---|
| **STOP** = 0 | Stop entity animation playback. |
| **PAUSE** = 1 | Pause entity animation playback. |
| **PLAY** = 2 | Start entity animation playback. |
| **CONTINUE** = 3 | Resume entity animation playback. |

### Properties

## 🔒︎ int EntityID

The entity ID.
## 🔒︎ int ParentID

The ID of the entity parent.
## 🔒︎ int EntityType

The entity type.
## 🔒︎ int EntityState

The entity state.
## 🔒︎ int AttachState

The value of the **Attach State** parameter. It specifies whether the entity is be attached as a child to a [parent](#getParentID_int).
## 🔒︎ int Collision

The value indicating if collision detecton shall be enabled for the entity.
## 🔒︎ int InheritAlpha

The value indicating if the entity uses the alpha value of its [parent](#getParentID_int).
## 🔒︎ int GroundClamp

The value of the **Ground/Ocean Clamp** parameter.
## 🔒︎ int AnimationBack

The entity's animation playback direction.
## 🔒︎ int AnimationLoop

The entity's animation playback mode.
## 🔒︎ int AnimationState

The entity's animation playback state.
## 🔒︎ int Interpolation

The a value indicating if interpolation and extrapolation are enabled.
## 🔒︎ int Alpha

The alpha value, that determines transparency of entity geometry.
## 🔒︎ vec3 Rotation

The entity rotation value.
## 🔒︎ dvec3 Position

The entity position.
### Members

---
