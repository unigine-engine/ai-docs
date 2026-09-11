# Unigine::Plugins::IG::Entity Class (CPP)

**Header:** #include <plugins/Unigine/IG/UnigineIG.h>


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

### Members

---

## long long getID ( ) const

Returns the unique ID of the entity instance.
### Return value

Entity ID.
## Ptr < Node > getNode ( ) const

Returns the node assigned to the entity.
### Return value

Node assigned to the entity.
## Ptr < NodeReference > getNodeReference ( ) const

Returns the node reference assigned to the entity.
### Return value

NodeReference assigned to the entity.
## void setGeoPosition ( const Math::dvec3& position , double timestamp )

Sets the entity position in geo-coordinates (lat, lon, alt).
### Arguments

- *const  Math::dvec3&* **position** - New geo-coordinates of entity position to be set.
- *double* **timestamp** - Timestamp, indicating the time when entity position in geo-coordinates is to be set.

## Math:: dvec3 getGeoPosition ( ) const

Returns the current entity position in geo-coordinates (lat, lon, alt).
### Return value

Entity position coordinates.
> **Notice:** Geo-coordinates will be returned if there is no parent entity assigned, otherwise � local coordinates will be returned.


## void setRotationEuler ( const Math::vec3& euler , double timestamp )

Sets the entity rotation at the specified time.
### Arguments

- *const  Math::vec3&* **euler** - Entity rotation Euler angles to set.
- *double* **timestamp** - Timestamp, indicating the time when rotation is to be set.

## Math:: vec3 getRotationEuler ( ) const

Returns the current entity rotation euler angles.
### Return value

Entity rotation euler angles.
## void setPositionOffset ( const Math::dvec3& offset , double timestamp )

Sets the entity position offset at the specified time.
### Arguments

- *const  Math::dvec3&* **offset** - Position offset to be set for the entity.
- *double* **timestamp** - Timestamp, indicating the time when position offset is to be set.

## Math:: dvec3 getPositionOffset ( ) const

Returns the current entity position offset.
### Return value

Current entity position offset.
## void setType ( long long id )

Sets the type of the entity. Entity type ID is defined in the [entity definition section](../../../../../ig/config.md#config_entities) of the IG configuration file as follows:
```xml
<entity_types>
	<entity id="111" name="b52">
	</entity>
</entity_types>

```

 Setting the type to 0 removes the entity from the scene.
### Arguments

- *long long* **id** - Entity type to be set. 0 removes the entity from the scene.

## long long getType ( ) const

Returns the type of the entity. Entity type ID is defined in the [entity definition section](../../../../../ig/config.md#config_entities) of the IG configuration file as follows:
```xml
<entity_types>
	<entity id="111" name="b52">
	</entity>
</entity_types>

```


### Return value

Entity type.
## long long getInternalType ( ) const

Returns the internal type of the entity.
### Return value

Internal entity type.
## void setAutoTypeMatchEnabled ( bool enabled )

Sets the value indicating if automatic type matching shall be enabled for the entity. When enabled, prevents from setting a non-existent type to the entity.
### Arguments

- *bool* **enabled** - true to enable automatic type matching for the entity; false � to disable.

## bool isAutoTypeMatchEnabled ( ) const

Returns the value indicating if automatic type matching shall be enabled for the entity. When enabled, prevents from setting a non-existent type to the entity.
### Return value

true if automatic type matching for the entity is enabled; false, otherwise.
## void setState ( Entity::STATE id )

Sets the state of the entity.
### Arguments

- *[Entity::STATE](../../../../../api/library/plugins/ig/api/class.entity_cpp.md#STATE)* **id** - Entity state to be set.

## Entity::STATE getState ( ) const

Returns the current entity state.
### Return value

Current entity state.
## void setCollision ( bool enabled )

Sets the value indicating if collision detecton shall be enabled for the entity.
### Arguments

- *bool* **enabled** - true to enable collision detecton for the entity; false � to disable.

## bool isCollision ( ) const

Returns the value indicating if collision detecton shall be enabled for the entity.
### Return value

**Collision Detection Enable** parameter value. true collision detecton for the entity shall be enabled; false � collision detecton for the entity shall be enabled.
## void setParent ( Entity * entity )

Attaches the entity as a child to the specified parent entity.
### Arguments

- *[Entity](../../../../../api/library/plugins/ig/api/class.entity_cpp.md) ** **entity** - Parent entity.

## void unparent ( )

Detaches the entity from its parent.
## long long getParentID ( ) const

Returns the ID of the entity parent.
### Return value

Entity parent ID.
## int getAttachState ( ) const

Returns the value of the **Attach State** parameter. It specifies whether the entity is be attached as a child to a [parent](#getParentID_llong).
### Return value

**Attach State** parameter value. 1 the entity shall be or remain attached to the entity specified by the [Parent ID parameter](#getParentID_llong); 0 � the entity shall be detached from its parent.
## void setAlpha ( int byte_value )

Sets the alpha value, that determines transparency of entity geometry.
### Arguments

- *int* **byte_value** - Alpha value to be set.

## int getAlpha ( ) const

Returns the current alpha value, that determines transparency of entity geometry.
### Return value

Alpha value.
## void setInheritAlpha ( bool enabled )

Sets the value indicating if the entity uses the alpha value of its [parent](#getParentID_llong).
### Arguments

- *bool* **enabled** - true the entity shall use the alpha value of its [parent](#getParentID_llong); false � the entity shall use its own alpha value.

## bool isInheritAlpha ( ) const

Returns the value indicating if the entity uses the alpha value of its [parent](#getParentID_llong).
### Return value

true if the entity uses the alpha value of its [parent](#getParentID_llong); otherwise, false.
## void setGroundClamp ( Entity::CLAMP clamp )

Sets the value of the **Ground/Ocean Clamp** parameter.
### Arguments

- *[Entity::CLAMP](../../../../../api/library/plugins/ig/api/class.entity_cpp.md#CLAMP)* **clamp** - **Ground/Ocean Clamp** parameter value.

## Entity::CLAMP getGroundClamp ( ) const

Returns the value of the **Ground/Ocean Clamp** parameter.
### Return value

**Ground/Ocean Clamp** parameter value.
## void setGroundClampHeightMode ( Entity::CLAMP_HEIGHT_MODE height_mode )

Sets the value of the **clamp height mode** parameter used for [clamping](#setGroundClamp_int_void). By default, the Ground Clamp Height Mode is set to RELATIVE � the entity is clamped to the ground and the height is calculated from the ground. With the mode set to IGNORE, the entity is clamped to the ground and the height is ignored.
### Arguments

- *[Entity::CLAMP_HEIGHT_MODE](../../../../../api/library/plugins/ig/api/class.entity_cpp.md#CLAMP_HEIGHT_MODE)* **height_mode** - **Clamp height mode** parameter value.

## Entity::CLAMP_HEIGHT_MODE getGroundClampHeightMode ( ) const

Returns the value of the **clamp height mode** parameter used for [clamping](#setGroundClamp_int_void). By default, the Ground Clamp Height Mode is set to RELATIVE � the entity is clamped to the ground and the height is calculated from the ground. With the mode set to IGNORE, the entity is clamped to the ground and the height is ignored.
### Return value

**Clamp height mode** parameter value.
## Math:: dvec3 getGroundClampPoint ( ) const

Returns the current ground clamping point coordinates for the entity. Clamping is performed relative to the ground and sea level.
## void setAnimationDirection ( Entity::ANIMATION_DIRECTION animation_direction )

Sets the entity's animation playback direction.
### Arguments

- *[Entity::ANIMATION_DIRECTION](../../../../../api/library/plugins/ig/api/class.entity_cpp.md#ANIMATION_DIRECTION)* **animation_direction** - Direction of the entity's animation playback.

## Entity::ANIMATION_DIRECTION getAnimationDirection ( ) const

Returns the current entity's animation playback direction.
### Return value

Direction of the entity's animation playback.
## void setAnimationLoop ( Entity::ANIMATION_LOOP animation_loop )

Sets the entity's animation playback mode.
### Arguments

- *[Entity::ANIMATION_LOOP](../../../../../api/library/plugins/ig/api/class.entity_cpp.md#ANIMATION_LOOP)* **animation_loop** - Mode of the entity's animation playback.

## Entity::ANIMATION_LOOP getAnimationLoop ( ) const

Returns the current entity's animation playback mode.
### Return value

Mode of the entity's animation playback.
## void setAnimationState ( Entity::ANIMATION_STATE animation_state )

Sets the entity's animation playback state.
### Arguments

- *[Entity::ANIMATION_STATE](../../../../../api/library/plugins/ig/api/class.entity_cpp.md#ANIMATION_STATE)* **animation_state** - State of the entity's animation playback.

## Entity::ANIMATION_STATE getAnimationState ( ) const

Returns the current entity's animation playback state.
### Return value

State of the entity's animation playback.
## void setInterpolation ( bool id )

Sets a value indicating if interpolation and extrapolation are enabled.
### Arguments

- *bool* **id** - true to enable interpolation and extrapolation; false � to disable.

## bool isInterpolation ( ) const

Returns a value indicating if interpolation and extrapolation are enabled.
### Return value

true if interpolation and extrapolation are enabled; otherwise, false.
## void clearInterpolationData ( )

Clears all interpolation data for the entity.
## void setExtrapolationCoordSystem ( Entity::COORDINATE_SYSTEM animation_state )

Sets the reference coordinate system to which the linear and angular velocity and acceleration are applied. If the reference coordinate system is set to [WORLD](#COORDINATE_SYSTEM_WORLD), and the entity is a top-level (non-child) entity, the velocity and acceleration are defined relative to the database. Linear velocity and acceleration describe a path along and above the surface of the geoid. Angular velocity and acceleration describe a rotation relative to a reference plane. If the entity is a child entity, the velocity and acceleration are defined relative to the parent�s local coordinate system. If the reference coordinate system is set to [LOCAL](#COORDINATE_SYSTEM_LOCAL), the velocity and acceleration are defined relative to the entity�s local coordinate system.
### Arguments

- *[Entity::COORDINATE_SYSTEM](../../../../../api/library/plugins/ig/api/class.entity_cpp.md#COORDINATE_SYSTEM)* **animation_state** - Coordinate system used for extrapolation.

## Entity::COORDINATE_SYSTEM getExtrapolationCoordSystem ( ) const

Returns the current reference coordinate system to which the linear and angular velocity and acceleration are applied. If the reference coordinate system is set to [WORLD](#COORDINATE_SYSTEM_WORLD), and the entity is a top-level (non-child) entity, the velocity and acceleration are defined relative to the database. Linear velocity and acceleration describe a path along and above the surface of the geoid. Angular velocity and acceleration describe a rotation relative to a reference plane. If the entity is a child entity, the velocity and acceleration are defined relative to the parent�s local coordinate system. If the reference coordinate system is set to [LOCAL](#COORDINATE_SYSTEM_LOCAL), the velocity and acceleration are defined relative to the entity�s local coordinate system.
### Return value

Extrapolation coordinate system.
## void setVelocity ( const Math::dvec3& linear , const Math::vec3& angular_deg )

Sets linear and angular velocity for the entity.
### Arguments

- *const  Math::dvec3&* **linear** - Linear velocity vector to be set.
- *const  Math::vec3&* **angular_deg** - Angular velocity vector (roll, pitch, yaw), in degrees per second.

## Math:: dvec3 getLinearVelocity ( ) const

Returns the linear velocity of the entity.
### Return value

Linear velocity vector.
## Math:: vec3 getAngularVelocity ( ) const

Returns the angular velocity of the entity.
### Return value

Angular velocity vector (roll, pitch, yaw), in degrees per second.
## void setAcceleration ( const Math::dvec3& linear , const Math::vec3& angular_deg )

Sets linear and angular acceleration for the entity.
### Arguments

- *const  Math::dvec3&* **linear** - Linear acceleration vector to be set.
- *const  Math::vec3&* **angular_deg** - Angular acceleration vector (roll, pitch, yaw), in degrees per second.

## Math:: dvec3 getLinearAcceleration ( ) const

Returns the linear acceleration of the entity.
### Return value

Linear acceleration vector.
## Math:: vec3 getAngularAcceleration ( ) const

Returns the angular acceleration of the entity.
### Return value

Angular acceleration vector (roll, pitch, yaw), in degrees per second.
## void setTerminalVelocity ( float terminal_velocity )

Sets the maximum velocity that the entity can sustain.
### Arguments

- *float* **terminal_velocity** - The maximum velocity that the entity can sustain.

## float getTerminalVelocity ( ) const

Returns the current maximum velocity that the entity can sustain.
### Return value

The maximum velocity that the entity can sustain.
## void setRetardationRate ( float retardation_rate )

Sets the retardation rate, the parameter that specifies the magnitude of an acceleration applied against the entity's instantaneous linear velocity vector. It is used to simulate drag and other frictional forces acting upon the entity.
### Arguments

- *float* **retardation_rate** - The retardation rate, the parameter that specifies the magnitude of an acceleration applied against the entity's instantaneous linear velocity vector.

## float getRetardationRate ( ) const

Returns the current retardation rate, the parameter that specifies the magnitude of an acceleration applied against the entity's instantaneous linear velocity vector. It is used to simulate drag and other frictional forces acting upon the entity.
### Return value

The retardation rate, the parameter that specifies the magnitude of an acceleration applied against the entity's instantaneous linear velocity vector.
## void restoreGeoPosition ( )

Resets the current transformation of the entity to the last known geo coordinates. Recommended in such cases as changing the projection parameters on the fly.
## Component * getComponent ( int id , bool auto_create )

Returns the [interface](../../../../../api/library/plugins/ig/api/class.component_cpp.md) of the specified component.
### Arguments

- *int* **id** - ID of the component.
- *bool* **auto_create** - true to automatically create the component with the specified ID if it doesn't exist yet; false - to return nullptr in case the component doesn't exist.

### Return value

Component interface if it exists, or nullptr otherwise.
## Vector < IG::Component * > getComponents ( ) const

Returns the list of all [components](../../../../../api/library/plugins/ig/api/class.component_cpp.md) associated with the entity.
## ArticulatedPart * getArticulatedPart ( int id , bool auto_create )

Returns the [interface](../../../../../api/library/plugins/ig/api/class.articulatedpart_cpp.md) of the specified articulated part.
### Arguments

- *int* **id** - ID of the articulated part.
- *bool* **auto_create** - true to automatically create the articulated part with the specified ID if it doesn't exist yet; false - to return nullptr in case the articulated part doesn't exist.

### Return value

Articulated part interface if it exists, or nullptr otherwise.
## Vector < IG::ArticulatedPart * > getArticulatedParts ( ) const

Returns the list of all [articulated parts](../../../../../api/library/plugins/ig/api/class.articulatedpart_cpp.md) associated with the entity.
## CollisionSegment * getCollisionSegment ( int id , bool auto_create )

Returns the interface of the specified collision segment.
### Arguments

- *int* **id** - ID of the collision segment.
- *bool* **auto_create** - true to automatically create the collision segment with the specified ID if it doesn't exist yet; false - to return nullptr in case the collision segment doesn't exist.

### Return value

Collision segment interface if it exists, or nullptr otherwise.
## Vector < IG::CollisionSegment * > getCollisionSegments ( ) const

Returns the list of all [collision segments](../../../../../api/library/plugins/ig/api/class.collisionsegment_cpp.md) associated with the entity.
## CollisionVolume * getCollisionVolume ( int id , bool auto_create )

Returns the interface of the specified collision volume.
### Arguments

- *int* **id** - ID of the collision volume.
- *bool* **auto_create** - true to automatically create the collision volume with the specified ID if it doesn't exist yet; false - to return nullptr in case the collision volume doesn't exist.

### Return value

Collision volume interface if it exists, or nullptr otherwise.
## Vector < IG::CollisionVolume * > getCollisionVolumes ( ) const

Returns the list of all [collision volumes](../../../../../api/library/plugins/ig/api/class.collisionvolume_cpp.md) associated with the entity.
## Vector < Ptr < Node > > getObjects ( ) const

Returns the vector of all nodes, that constitute the entity.
### Return value

Vector of nodes, that constitute the entity.
## int64_t getEntityTypeFromDIS ( uint8_t kind , uint8_t domain , uint16_t country , uint8_t cat , uint8_t subcat , uint8_t spec , uint8_t extra )

Returns the entity type identifier (defined in the [entity definition section](../../../../../ig/config.md#config_entities)) based on the given arguments. This method is used to convert the entity's ID from DIS type to the IG type.
You can also set the type using a DIS-style ID:
```xml
<entity_types>
	<entity id="1.2.222.4.14.0.0" name="vehicle">
	</entity>
</entity_types>

```


### Arguments

- *uint8_t* **kind** - Entity kind
- *uint8_t* **domain** - Domain
- *uint16_t* **country** - Country
- *uint8_t* **cat** - Category
- *uint8_t* **subcat** - Sub Category
- *uint8_t* **spec** - Specific
- *uint8_t* **extra** - Extra

### Return value

Entity type identifier
## bool getDISTypeFromEntityType ( int64_t entity_type , uint8_t & kind , uint8_t & domain , uint16_t & country , uint8_t & cat , uint8_t & subcat , uint8_t & spec , uint8_t & extra )

Returns the DIS-style entity type identifier (by setting values for the given arguments: kind, domain, etc.) based on the specified entity type ID used in the IG (see the [entity definition section](../../../../../ig/config.md#config_entities)). This method is used to convert the entity's ID from IG type to the DIS type.
Entity type can be specified using a DIS-style ID:
```xml
<entity_types>
	<entity id="1.2.222.4.14.0.0" name="vehicle">
	</entity>
</entity_types>

```


### Arguments

- *int64_t* **entity_type** - Entity type identifier.
- *uint8_t &* **kind** - Kind
- *uint8_t &* **domain** - Domain
- *uint16_t &* **country** - Country
- *uint8_t &* **cat** - Category
- *uint8_t &* **subcat** - Sub Category
- *uint8_t &* **spec** - Specific
- *uint8_t &* **extra** - Extra

### Return value

true, if the entity type ID conversion from IG to DIS is successfull, otherwise false.
## int64_t getEntityIDFromDISID ( uint16_t app , uint16_t id )

Returns the result of entity ID conversion from DIS to IG. In case of DIS an entity is identified by a pair: Application ID + Entity ID (Site ID is ignored by IG).
### Arguments

- *uint16_t* **app** - Application ID.
- *uint16_t* **id** - Entity ID used in DIS application.

### Return value

Entity ID used in IG.
## void getDISIDFromEntityID ( int64_t entity_id , uint16_t & app , uint16_t & id )

Converts entity ID from IG to DIS and puts the result to variables specified via **app** and **id** arguments. In case of DIS an entity is identified by a pair: Application ID + Entity ID (Site ID is ignored by IG).
### Arguments

- *int64_t* **entity_id** - Entity ID used in IG.
- *uint16_t &* **app** - Application ID used in DIS.
- *uint16_t &* **id** - Entity ID used in DIS.

## const char * getTypeName ( ) const

Returns the name of the entity type (defined in the [entity definition section](../../../../../ig/config.md#config_entities)).
### Return value

Entity type name.
## bool isPrespawned ( ) const

Returns a value indicating if the entity is prespawned (i.e. created via UnigineEditor and already exists in the world).
### Return value

true if the entity is prespawned, otherwise false.
## void * addOnBeforeChangeTypeCallback ( CallbackBase2 < int64_t, int64_t > * func )

Adds a callback to be fired before changing the entity type.
### Arguments

- *[CallbackBase2](../../../../../api/library/common/callbacks/class.callbackbase2_cpp.md) < int64_t, int64_t > ** **func** - Callback pointer. The callback function must have the following signature: *void (int64_t **old_type**, int64_t **old_type**)*.

### Return value

ID of the last added Before Change Type callback, if the callback was added successfully; otherwise, **nullptr**. This ID can be used to [remove](#removeOnBeforeChangeTypeCallback_void_ptr_bool) this callback when necessary.
## bool removeOnBeforeChangeTypeCallback ( void * id )

Removes the specified callback from the list of Before Change Type callbacks.
### Arguments

- *void ** **id** - Callback ID obtained when [adding a Before Change Type callback](#addOnBeforeChangeTypeCallback_CallbackBase2_ptr_void_ptr).

### Return value

true if the Before Change Type callback with the given ID was removed successfully; otherwise false.
## void clearOnBeforeChangeTypeCallback ( )

Clears all [added](#addOnBeforeChangeTypeCallback_CallbackBase2_ptr_void_ptr) Before Change Type callbacks.
## void * addOnAfterChangeTypeCallback ( CallbackBase2 < int64_t, int64_t > * func )

Adds a callback to be fired after changing the entity type.
### Arguments

- *[CallbackBase2](../../../../../api/library/common/callbacks/class.callbackbase2_cpp.md) < int64_t, int64_t > ** **func** - Callback pointer. The callback function must have the following signature: *void (int64_t **old_type**, int64_t **old_type**)*.

### Return value

ID of the last added After Change Type callback, if the callback was added successfully; otherwise, **nullptr**. This ID can be used to [remove](#removeOnAfterChangeTypeCallback_void_ptr_bool) this callback when necessary.
## bool removeOnAfterChangeTypeCallback ( void * id )

Removes the specified callback from the list of After Change Type callbacks.
### Arguments

- *void ** **id** - Callback ID obtained when [adding a After Change Type callback](#addOnAfterChangeTypeCallback_CallbackBase2_ptr_void_ptr).

### Return value

true if the After Change Type callback with the given ID was removed successfully; otherwise false.
## void clearOnAfterChangeTypeCallback ( )

Clears all [added](#addOnAfterChangeTypeCallback_CallbackBase2_ptr_void_ptr) After Change Type callbacks.
## void setOwnerID ( int id )

Sets the ID of the entity owner.
### Arguments

- *int* **id** - Owner ID to be set.

## int getOwnerID ( ) const

Returns the ID of the entity owner.
### Return value

Entity owner ID.
## void setDebugDescription ( String description )

Sets the debug description for the entity.
### Arguments

- *[String](../../../../../api/library/common/class.string_cpp.md)* **description** - Debug description to be set.

## String getDebugDescription ( ) const

Returns the debug description of the entity.
### Return value

Debug description of the entity.
## void setEntityName ( const char * name )

Sets the name of the entity.
### Arguments

- *const char ** **name** - Entity name to be set.

## const char * getEntityName ( ) const

Returns the name of the entity.
### Return value

Entity name.
