# Unigine::Plugins::IG::Entity Class (CS)


This class represents the IG Entity interface.


> **Notice:** IG plugin must be loaded.


## Entity Class

### Enums

## STATE

| Name | Description |
|---|---|
| **STATE_INACTIVE** = 0 | The entity is inactive. |
| **STATE_ACTIVE** = 1 | The entity is active. |
| **STATE_DESTROYED** = 2 | The entity is destroyed. |

## CLAMP

| Name | Description |
|---|---|
| **CLAMP_NO_CLAMP** = 0 | Altitude clamping for entity is disabled. |
| **CLAMP_NON_CONFORMAL** = 1 | Altitude parameter specifies an offset of the entity above the ground level. |
| **CLAMP_CONFORMAL** = 2 | Altitude parameter specifies an offset of the entity above the sea level. |

## CLAMP_HEIGHT_MODE

| Name | Description |
|---|---|
| **CLAMP_HEIGHT_MODE_RELATIVE** = 0 | Clamp height mode that makes the entity to be clamped to the ground and the height be calculated from the ground. |
| **CLAMP_HEIGHT_MODE_IGNORE** = 1 | Clamp height mode that makes the entity to be clamped to the ground and the height be ignored. |

## ANIMATION_DIRECTION

| Name | Description |
|---|---|
| **ANIMATION_DIRECTION_FORWARD** = 0 | Forward direction of the entity animation playback. |
| **ANIMATION_DIRECTION_BACKWARD** = 1 | Backward direction of the entity animation playback. |

## ANIMATION_LOOP

| Name | Description |
|---|---|
| **ANIMATION_LOOP_ONESHOT** = 0 | Oneshot mode of the entity animation playback. |
| **ANIMATION_LOOP_CONTINUOUS** = 1 | Continuous mode of the entity animation playback. |

## ANIMATION_STATE

| Name | Description |
|---|---|
| **ANIMATION_STATE_STOP** = 0 | Stop entity animation playback. |
| **ANIMATION_STATE_PAUSE** = 1 | Pause entity animation playback. |
| **ANIMATION_STATE_PLAY** = 2 | Start entity animation playback. |
| **ANIMATION_STATE_CONTINUE** = 3 | Resume entity animation playback. |

## COORDINATE_SYSTEM

| Name | Description |
|---|---|
| **COORDINATE_SYSTEM_WORLD** = 0 | If the reference coordinate system is set to this value, and the entity is a top-level (non-child) entity, the velocity and acceleration are defined relative to the database. Linear velocity and acceleration describe a path along and above the surface of the geoid. Angular velocity and acceleration describe a rotation relative to a reference plane. If the entity is a child entity, the velocity and acceleration are defined relative to the parent�s local coordinate system. |
| **COORDINATE_SYSTEM_LOCAL** = 1 | If the reference coordinate system is set to this value, the velocity and acceleration are defined relative to the entity�s local coordinate system. |

### Properties

## 🔒︎ vec3 AngularAcceleration

The angular acceleration of the entity.
## 🔒︎ dvec3 LinearAcceleration

The linear acceleration of the entity.
## 🔒︎ vec3 AngularVelocity

The angular velocity of the entity.
## 🔒︎ dvec3 LinearVelocity

The linear velocity of the entity.
## 🔒︎ float RetardationRate

The retardation rate, the parameter that specifies the magnitude of an acceleration applied against the entity's instantaneous linear velocity vector. It is used to simulate drag and other frictional forces acting upon the entity.
## 🔒︎ float TerminalVelocity

The maximum velocity that the entity can sustain.
## Entity.COORDINATE_SYSTEM ExtrapolationCoordSystem

The reference coordinate system to which the linear and angular velocity and acceleration are applied. If the reference coordinate system is set to [WORLD](#COORDINATE_SYSTEM_WORLD), and the entity is a top-level (non-child) entity, the velocity and acceleration are defined relative to the database. Linear velocity and acceleration describe a path along and above the surface of the geoid. Angular velocity and acceleration describe a rotation relative to a reference plane. If the entity is a child entity, the velocity and acceleration are defined relative to the parent�s local coordinate system. If the reference coordinate system is set to [LOCAL](#COORDINATE_SYSTEM_LOCAL), the velocity and acceleration are defined relative to the entity�s local coordinate system.
## bool Interpolation

The a value indicating if interpolation and extrapolation are enabled.
## Entity.ANIMATION_STATE AnimationState

The entity's animation playback state.
## Entity.ANIMATION_LOOP AnimationLoop

The entity's animation playback mode.
## Entity.ANIMATION_DIRECTION AnimationDirection

The entity's animation playback direction.
## Entity.CLAMP_HEIGHT_MODE GroundClampHeightMode

The value of the **clamp height mode** parameter used for [clamping](#setGroundClamp_int_void). By default, the Ground Clamp Height Mode is set to RELATIVE � the entity is clamped to the ground and the height is calculated from the ground. With the mode set to IGNORE, the entity is clamped to the ground and the height is ignored.
## Entity.CLAMP GroundClamp

The value of the **Ground/Ocean Clamp** parameter.
## bool InheritAlpha

The value indicating if the entity uses the alpha value of its [parent](#getParentID_llong).
## int Alpha

The alpha value, that determines transparency of entity geometry.
## 🔒︎ int AttachState

The value of the **Attach State** parameter. It specifies whether the entity is be attached as a child to a [parent](#getParentID_llong).
## 🔒︎ long ParentID

The ID of the entity parent.
## bool Collision

The value indicating if collision detecton shall be enabled for the entity.
## Entity.STATE State

The entity state.
## 🔒︎ bool IsPrespawned

The value indicating if the entity is prespawned (i.e. created via UnigineEditor and already exists in the world).
## 🔒︎ long InternalType

The internal type of the entity.
## long Type

The type of the entity. Entity type ID is defined in the [entity definition section](../../../../../ig/config.md#config_entities) of the IG configuration file as follows:
```xml
<entity_types>
	<entity id="111" name="b52">
	</entity>
</entity_types>

```


## 🔒︎ NodeReference NodeReference

The node reference assigned to the entity.
## 🔒︎ Node Node

The node assigned to the entity.
## 🔒︎ long ID

The unique ID of the entity instance.
## int OwnerID

The ID of the entity owner.
## string DebugDescription

The debug description string assigned to the entity.
## string EntityName

The name of the entity.
## 🔒︎ bool AutoTypeMatchEnabled

The value indicating if automatic type matching for the entity is enabled. When enabled, prevents from setting a non-existent type to the entity.
### Members

---

## void SetParent ( Entity entity )

Attaches the entity as a child to the specified parent entity.
### Arguments

- *[Entity](../../../../../api/library/plugins/ig/api/class.entity_cs.md)* **entity** - Parent entity.

## void unparent ( )

Detaches the entity from its parent.
## int getAttachState ( )

Returns the value of the **Attach State** parameter. It specifies whether the entity is be attached as a child to a [parent](#getParentID_llong).
### Return value

**Attach State** parameter value. 1 the entity shall be or remain attached to the entity specified by the [Parent ID parameter](#getParentID_llong); 0 � the entity shall be detached from its parent.
## dvec3 GetGroundClampPoint ( )

Returns the current ground clamping point coordinates for the entity. Clamping is performed relative to the ground and sea level.
## void SetVelocity ( dvec3 linear , vec3 angular_deg )

Sets linear and angular velocity for the entity.
### Arguments

- *dvec3* **linear** - Linear velocity vector to be set.
- *vec3* **angular_deg** - Angular velocity vector (roll, pitch, yaw), in degrees per second.

## void SetAcceleration ( dvec3 linear , vec3 angular_deg )

Sets linear and angular acceleration for the entity.
### Arguments

- *dvec3* **linear** - Linear acceleration vector to be set.
- *vec3* **angular_deg** - Angular acceleration vector (roll, pitch, yaw), in degrees per second.

## void SetTerminalVelocity ( float terminal_velocity )

Sets the maximum velocity that the entity can sustain.
### Arguments

- *float* **terminal_velocity** - The maximum velocity that the entity can sustain.

## float GetTerminalVelocity ( )

Returns the current maximum velocity that the entity can sustain.
### Return value

The maximum velocity that the entity can sustain.
## void SetRetardationRate ( float retardation_rate )

Sets the retardation rate, the parameter that specifies the magnitude of an acceleration applied against the entity's instantaneous linear velocity vector. It is used to simulate drag and other frictional forces acting upon the entity.
### Arguments

- *float* **retardation_rate** - The retardation rate, the parameter that specifies the magnitude of an acceleration applied against the entity's instantaneous linear velocity vector.

## float GetRetardationRate ( )

Returns the current retardation rate, the parameter that specifies the magnitude of an acceleration applied against the entity's instantaneous linear velocity vector. It is used to simulate drag and other frictional forces acting upon the entity.
### Return value

The retardation rate, the parameter that specifies the magnitude of an acceleration applied against the entity's instantaneous linear velocity vector.
## void RestoreGeoPosition ( )

Resets the current transformation of the entity to the last known geo coordinates. Recommended in such cases as changing the projection parameters on the fly.
## Component GetComponent ( int id , bool auto_create )

Returns the [interface](../../../../../api/library/plugins/ig/api/class.component_cs.md) of the specified component.
### Arguments

- *int* **id** - ID of the component.
- *bool* **auto_create** - true to automatically create the component with the specified ID if it doesn't exist yet; false - to return nullptr in case the component doesn't exist.

### Return value

Component interface if it exists, or nullptr otherwise.
## ArticulatedPart GetArticulatedPart ( int id , bool auto_create )

Returns the [interface](../../../../../api/library/plugins/ig/api/class.articulatedpart_cs.md) of the specified articulated part.
### Arguments

- *int* **id** - ID of the articulated part.
- *bool* **auto_create** - true to automatically create the articulated part with the specified ID if it doesn't exist yet; false - to return nullptr in case the articulated part doesn't exist.

### Return value

Articulated part interface if it exists, or nullptr otherwise.
## CollisionSegment GetCollisionSegment ( int id , bool auto_create )

Returns the interface of the specified collision segment.
### Arguments

- *int* **id** - ID of the collision segment.
- *bool* **auto_create** - true to automatically create the collision segment with the specified ID if it doesn't exist yet; false - to return nullptr in case the collision segment doesn't exist.

### Return value

Collision segment interface if it exists, or nullptr otherwise.
## CollisionVolume GetCollisionVolume ( int id , bool auto_create )

Returns the interface of the specified collision volume.
### Arguments

- *int* **id** - ID of the collision volume.
- *bool* **auto_create** - true to automatically create the collision volume with the specified ID if it doesn't exist yet; false - to return nullptr in case the collision volume doesn't exist.

### Return value

Collision volume interface if it exists, or nullptr otherwise.
## string GetTypeName ( )

Returns the name of the entity type (defined in the [entity definition section](../../../../../ig/config.md#config_entities)).
### Return value

Entity type name.
## bool IsPrespawned ( )

Returns a value indicating if the entity is prespawned (i.e. created via UnigineEditor and already exists in the world).
### Return value

true if the entity is prespawned, otherwise false.
## IntPtr AddOnBeforeChangeTypeCallback ( OnBeforeChangeTypeDelegate func )

Adds a callback to be fired before changing the entity type.
### Arguments

- *OnBeforeChangeTypeDelegate* **func** - Callback function with the following signature: void OnBeforeChangeTypeDelegate(*long* **old_type**, *long* **new_type**).

### Return value

ID of the last added Before Change Type callback, if the callback was added successfully; otherwise, **nullptr**. This ID can be used to [remove](#removeOnBeforeChangeTypeCallback_void_ptr_bool) this callback when necessary.
## bool RemoveOnBeforeChangeTypeCallback ( IntPtr id )

Removes the specified callback from the list of Before Change Type callbacks.
### Arguments

- *IntPtr* **id** - Callback ID obtained when [adding a Before Change Type callback](#addOnBeforeChangeTypeCallback_CallbackBase2_ptr_void_ptr).

### Return value

true if the Before Change Type callback with the given ID was removed successfully; otherwise false.
## void ClearOnBeforeChangeTypeCallback ( )

Clears all [added](#addOnBeforeChangeTypeCallback_CallbackBase2_ptr_void_ptr) Before Change Type callbacks.
## IntPtr AddOnAfterChangeTypeCallback ( OnAfterChangeTypeDelegate func )

Adds a callback to be fired after changing the entity type.
### Arguments

- *OnAfterChangeTypeDelegate* **func** - Callback function with the following signature: void OnAfterChangeTypeDelegate(*long* **old_type**, *long* **new_type**).

### Return value

ID of the last added After Change Type callback, if the callback was added successfully; otherwise, **nullptr**. This ID can be used to [remove](#removeOnAfterChangeTypeCallback_void_ptr_bool) this callback when necessary.
## bool RemoveOnAfterChangeTypeCallback ( IntPtr id )

Removes the specified callback from the list of After Change Type callbacks.
### Arguments

- *IntPtr* **id** - Callback ID obtained when [adding a After Change Type callback](#addOnAfterChangeTypeCallback_CallbackBase2_ptr_void_ptr).

### Return value

true if the After Change Type callback with the given ID was removed successfully; otherwise false.
## void ClearOnAfterChangeTypeCallback ( )

Clears all [added](#addOnAfterChangeTypeCallback_CallbackBase2_ptr_void_ptr) After Change Type callbacks.
