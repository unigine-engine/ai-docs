# Unigine::Plugins::IG::Manager Class (CPP)

**Header:** #include <plugins/Unigine/IG/UnigineIG.h>

> **Notice:** This class is a singleton.


This class represents the IG Manager interface.


> **Notice:** IG plugin must be loaded.


## Manager Class

### Enums

## DEBUG_MODE

| Name | Description |
|---|---|
| **DEBUG_MODE_REQUEST_DEBUG** = 0 | Debug mode visualizing where LOS/HAT/HOT requests are sent to. |
| **DEBUG_MODE_ENTITY_PATH_TRACE** = 1 | Debug mode with entity path tracing - positions between frames and data sent over the network. Blue points mark data from the server; pink arrows - movement between frames. |
| **DEBUG_MODE_ENTITY_PATH_TRACE_TIME** = 2 | Debug mode visualizing entity path tracing time. |
| **DEBUG_MODE_ENTITY_COLLISION_SEGMENT** = 3 | Debug mode visualizing collision segments for every entity. |
| **DEBUG_MODE_ENTITY_COLLISION_VOLUME** = 4 | Debug mode visualizing collision volumes for every entity. |
| **DEBUG_MODE_ENTITY_INFO** = 5 | Debug mode visualizing the basis for every CIGI and DIS entity with the ID, type, and type name specified (information is taken from the [IG configuration](../../../../../ig/config.md) file). |
| **DEBUG_MODE_METEO** = 6 | Debug mode visualizing meteo information. |
| **DEBUG_MODE_INTERPOLATION_INFO** = 7 | Debug mode visualizing the interpolation timer parameters and states on the screen. Displaying of these data can also be enabled by the console command ig_debug_interpolation. |

### Members

## void setDebugScale ( float scale )

Sets a new scale multiplier for [Debug](../../../../../ig/debug/index.md) visualizer elements.
### Arguments

- *float* **scale** - The scale multiplier for [Debug](../../../../../ig/debug/index.md) visualizer elements.

## float getDebugScale () const

Returns the current scale multiplier for [Debug](../../../../../ig/debug/index.md) visualizer elements.
### Return value

Current scale multiplier for [Debug](../../../../../ig/debug/index.md) visualizer elements.
## void setDebugDepth ( bool depth )

Sets a new value indicating if depth testing for the [Debug](../../../../../ig/debug/index.md) visualizer elements is enabled (if elements should be obscured by the ones closer to the camera).
### Arguments

- *bool* **depth** - Set **true** to enable depth testing for the [Debug](../../../../../ig/debug/index.md) visualizer elements; **false** - to disable it.

## bool isDebugDepth () const

Returns the current value indicating if depth testing for the [Debug](../../../../../ig/debug/index.md) visualizer elements is enabled (if elements should be obscured by the ones closer to the camera).
### Return value

**true** if depth testing for the [Debug](../../../../../ig/debug/index.md) visualizer elements is enabled ; otherwise **false**.
## void setDebugScreenspace ( bool screenspace )

Sets a new value indicating the type of dimension to be used when rendering [Debug](../../../../../ig/debug/index.md) visualizer elements: the screen-space dimension or the world-space dimension.
### Arguments

- *bool* **screenspace** - Set **true** to enable Debug visualization in the screen-space dimension; **false** - to disable it.

## bool isDebugScreenspace () const

Returns the current value indicating the type of dimension to be used when rendering [Debug](../../../../../ig/debug/index.md) visualizer elements: the screen-space dimension or the world-space dimension.
### Return value

**true** if Debug visualization in the screen-space dimension is enabled ; otherwise **false**.
## void setDebugDuration ( float duration )

Sets a new time period during which [Debug](../../../../../ig/debug/index.md) visualizer elements are displayed.
### Arguments

- *float* **duration** - The time interval during which [Debug](../../../../../ig/debug/index.md) visualizer elements are displayed, in seconds.

## float getDebugDuration () const

Returns the current time period during which [Debug](../../../../../ig/debug/index.md) visualizer elements are displayed.
### Return value

Current time interval during which [Debug](../../../../../ig/debug/index.md) visualizer elements are displayed, in seconds.
## void setDebugEnabled ( bool enabled )

Sets a new value indicating if the [Debug mode](../../../../../ig/debug/index.md) is enabled. This mode allows inspecting the IG application at run-time.
### Arguments

- *bool* **enabled** - Set **true** to enable [Debug mode](../../../../../ig/debug/index.md); **false** - to disable it.

## bool isDebugEnabled () const

Returns the current value indicating if the [Debug mode](../../../../../ig/debug/index.md) is enabled. This mode allows inspecting the IG application at run-time.
### Return value

**true** if [Debug mode](../../../../../ig/debug/index.md) is enabled ; otherwise **false**.
## void setCollisionVolumeMask ( int mask )

Sets a new collision volume mask for entities.
### Arguments

- *int* **mask** - The collision volume mask for entities.

## int getCollisionVolumeMask () const

Returns the current collision volume mask for entities.
### Return value

Current collision volume mask for entities.
## void setTerrainIntersectionMask ( int mask )

Sets a new [intersection mask](../../../../../principles/bit_masking/index.md#intersection_mask) that is used to define the ground/landing surface.
### Arguments

- *int* **mask** - The intersection mask.

## int getTerrainIntersectionMask () const

Returns the current [intersection mask](../../../../../principles/bit_masking/index.md#intersection_mask) that is used to define the ground/landing surface.
### Return value

Current intersection mask.
## bool isTerrainCurved () const

Returns the current value indicating if terrain is curved.
### Return value

**true** if terrain is curved; otherwise **false**.
## Math:: dvec3 getGeodeticOrigin () const

Returns the current geodetic origin coordinates.
### Return value

Current geodetic origin coordinates.
## Ptr < GeodeticPivot > getGeodeticPivot () const

Returns the current geodetic pivot used to curve the terrain.
### Return value

Current geodetic pivot used to curve the terrain.
## Ptr < ObjectTerrainGlobal > getTerrain () const

Returns the current Global Terrain object.
### Return value

Current currently used Global Terrain object.
## void setInterpolation ( bool interpolation )

Sets a new value indicating if [interpolation and extrapolation](../../../../../ig/index.md#interpolation) for the IG is enabled.
### Arguments

- *bool* **interpolation** - Set **true** to enable [interpolation and extrapolation](../../../../../ig/index.md#interpolation) for the IG; **false** - to disable it.

## bool isInterpolation () const

Returns the current value indicating if [interpolation and extrapolation](../../../../../ig/index.md#interpolation) for the IG is enabled.
### Return value

**true** if [interpolation and extrapolation](../../../../../ig/index.md#interpolation) for the IG is enabled ; otherwise **false**.
## void setInterpolationLerpFactor ( double factor )

Sets a new
interpolation lerp factor value for the IG. The *lower* the value the smoother movement will be, but it will feel like objects move underwater or in a jelly, *higher* values result in higher positioning accuracy (objects positions will be closer to actual ones for the current frame), but objects will move with a noticeable jitter.


> **Notice:** [Frame-to-frame interpolation](#setInterpolationLerp_int_void) mode must be enabled.


### Arguments

- *double* **factor** - The interpolation lerp factor value.

## double getInterpolationLerpFactor () const

Returns the current
interpolation lerp factor value for the IG. The *lower* the value the smoother movement will be, but it will feel like objects move underwater or in a jelly, *higher* values result in higher positioning accuracy (objects positions will be closer to actual ones for the current frame), but objects will move with a noticeable jitter.


> **Notice:** [Frame-to-frame interpolation](#setInterpolationLerp_int_void) mode must be enabled.


### Return value

Current interpolation lerp factor value.
## void setExtrapolationPeriod ( double period = 0.2 )

Sets a new extrapolation period value for the IG.
### Arguments

- *double* **period** - The extrapolation period value, in seconds.

## double getExtrapolationPeriod () const

Returns the current extrapolation period value for the IG.
### Return value

Current extrapolation period value, in seconds.
## void setInterpolationPeriod ( double period = 0.04 )

Sets a new interpolation period value for the IG.
### Arguments

- *double* **period** - The interpolation period value, in seconds.

## double getInterpolationPeriod () const

Returns the current interpolation period value for the IG.
### Return value

Current interpolation period value, in seconds.
## void setInterpolationTime ( double time )

Sets a new interpolation time value for the IG.
### Arguments

- *double* **time** - The interpolation time value, in seconds.

## double getInterpolationTime () const

Returns the current interpolation time value for the IG.
### Return value

Current interpolation time value, in seconds.
## void setInterpolationLerp ( bool lerp )

Sets a new value indicating if interpolation between the current and previous frames for the IG is enabled.
### Arguments

- *bool* **lerp** - Set **true** to enable interpolation between the current and previous frames for the IG; **false** - to disable it.

## bool isInterpolationLerp () const

Returns the current value indicating if interpolation between the current and previous frames for the IG is enabled.
### Return value

**true** if interpolation between the current and previous frames for the IG is enabled ; otherwise **false**.
## void setInterpolationBufferSize ( int size )

Sets a new size of the [interpolation](../../../../../ig/index.md#interpolation) buffer. It is recommended to set buffer size equal to the number of messages received during two [interpolation periods](#setInterpolationPeriod_double_void).
### Arguments

- *int* **size** - The size of the interpolation buffer (number of messages).

## int getInterpolationBufferSize () const

Returns the current size of the [interpolation](../../../../../ig/index.md#interpolation) buffer. It is recommended to set buffer size equal to the number of messages received during two [interpolation periods](#setInterpolationPeriod_double_void).
### Return value

Current size of the interpolation buffer (number of messages).
## void setCurrentView ( int view )

Sets a new view by its ID. If the view with the specified ID does not exist, it will be created automatically.
### Arguments

- *int* **view** - The ID of the rendered view.

## int getCurrentView () const

Returns the current view by its ID. If the view with the specified ID does not exist, it will be created automatically.
### Return value

Current ID of the rendered view.
## Unigine::Plugins::Geodetics::Converter * getConverter () const

Returns the current *[converter](../../../../../api/library/geodetics/geodetics_plugin/class.transformer_cpp.md)* interface.
### Return value

Current converter interface.
## NEDConverter * getNEDConverter () const

Returns the current *[NEDConverter](../../../../../api/library/plugins/ig/api/class.nedconverter_cpp.md)* interface.
### Return value

Current NEDConverter interface.
## LightController * getLightController () const

Returns the current light controller interface.
### Return value

Current light controller interface.
## Meteo * getMeteo () const

Returns the current Meteo interface.
### Return value

Current Meteo interface.
## SkyMap * getSkyMap () const

Returns the current SkyMap interface.
### Return value

Current SkyMap interface.
## IGConfig * getConfig () const

Returns the current IG configuration as an [IGConfig](../../../../../api/library/plugins/ig/api/class.igconfig_cpp.md) class instance.
### Return value

Current IG Configuration interface.
## bool isDatabaseLoaded () const

Returns the current value indicating if any database is currently loaded.
### Return value

**true** if any database is currently loaded; otherwise **false**.
## int getCurrentDatabaseID () const

Returns the current identifier of the currently loaded world database stored in the IG configuration file (`ig_config.xml`).
### Return value

Current identifier of the world database, or 0, if no world is loaded.
## float getIFps () const

Returns the current inverse FPS value (the time in seconds it took to complete the last frame). This method is similar to the [*Game::getIFps()*](../../../../../api/library/engine/class.game_cpp.md#getIFps_float) but it is more preferred for multi-channel systems as it implements more accurate frame time calculation (including spike-periods).
### Return value

Current inverse FPS value (1/FPS) - the time in seconds it took to complete the last frame, in seconds.
## void setFreeze ( bool freeze )

Sets a new value indicating if execution of IG logic is temporarily put on hold (paused) or resumed.
### Arguments

- *bool* **freeze** - Set **true** to enable pause of IG logic execution; **false** - to disable it.

## bool isFreeze () const

Returns the current value indicating if execution of IG logic is temporarily put on hold (paused) or resumed.
### Return value

**true** if pause of IG logic execution is enabled ; otherwise **false**.
## bool isReady () const

Returns the current value indicating if all Slaves that were waited for by the IG have connected.
### Return value

**true** if all Slaves that were waited for by the IG have connected; otherwise **false**.
## bool isMaster () const

Returns the current value indicating if the IG application is a Syncker-Master or runs in a single mode without the [Syncker](../../../../../code/plugins/syncker/index.md) at all; or if the IG application is a Syncker-Slave.
### Return value

true if the IG application is a Syncker-Master or runs in a single mode without the [Syncker](../../../../../code/plugins/syncker/index.md) at all; false if the IG application is a Syncker-Slave.
---

## void reloadConfig ( )

Reloads the [IG Configuration file](../../../../../ig/config.md) (`ig_config.xml`).
## void reloadGeodetics ( )

Forces a runtime update of georeferencing data, which is useful for on-the-fly projection changes.
## bool loadDatabase ( int database_id )

Loads the database with the specified ID and sets it to be used.
### Arguments

- *int* **database_id** - ID of the database to be used.

### Return value

true means that the database with the specified ID is loaded successfully; otherwise, false.
## void reloadDatabase ( )

***Console*:**`database_reload`Reloads the current database.
## void unloadDatabase ( )

Unloads the current database.
## int getDatabaseID ( const char * world_name ) const

Returns the identifier of the world database with the specified name stored in the IG configuration file (`ig_config.xml`).
### Arguments

- *const char ** **world_name** - World database name.

### Return value

Identifier of the specified world database, or 0, if no world is loaded.
## const char * getDatabaseName ( int id ) const

Returns the name of the world database stored in the IG configuration file (`ig_config.xml`).
### Arguments

- *int* **id** - Identifier of the world database.

### Return value

The world database name.
## SymbolsController * getSymbolsController ( ) const

Returns the interface of the symbols controller.
### Return value

Symbols controller interface.
## View * getView ( int view_id , bool auto_create )

Returns the [interface](../../../../../api/library/plugins/ig/api/class.view_cpp.md) of the specified view.
### Arguments

- *int* **view_id** - ID of the view.
- *bool* **auto_create** - true to automatically create the view with the specified ID if it doesn't exist yet; false - to return nullptr in case the view doesn't exist.

### Return value

Pointer to the view interface if it exists; otherwise - nullptr.
## void getViews ( Unigine:: Vector < View *> & views_ret ) const

Returns the list of all existing views (if any).
### Arguments

- *Unigine::[Vector](../../../../../api/library/containers/vector/class.vector_cpp.md) < [View](../../../../../api/library/plugins/ig/api/class.view_cpp.md) *> &* **views_ret** - Vector containing all existing views (if any).

## bool removeView ( int view_id )

Removes the view with the specified ID.
### Arguments

- *int* **view_id** - ID of the view to be removed.

### Return value

true if the view with the specified ID is removed successfully; otherwise - false.
## bool isViewExist ( int view_id ) const

Returns a value indicating if the view with the specified ID exists.
### Arguments

- *int* **view_id** - ID of the view.

### Return value

true if the view with the specified ID exists; otherwise - false.
## ViewGroup * getViewGroup ( int group_id , bool auto_create )

Returns the [interface](../../../../../api/library/plugins/ig/api/class.viewgroup_cpp.md) of the specified view group.
### Arguments

- *int* **group_id** - ID of the view group.
- *bool* **auto_create** - true to automatically create the view group with the specified ID if it doesn't exist yet; false - to return nullptr in case the view group doesn't exist.

### Return value

Pointer to the view group interface if it exists; otherwise - nullptr.
## bool removeViewGroup ( int group_view_id )

Removes the view group with the specified ID.
### Arguments

- *int* **group_view_id** - ID of the view group to be removed.

### Return value

true if the view group with the specified ID is removed successfully; otherwise - false.
## bool isViewGroupExist ( int group_view_id ) const

Returns a value indicating if the view group with the specified ID exists.
### Arguments

- *int* **group_view_id** - ID of the view group.

### Return value

true if the view group with the specified ID exists; otherwise - false.
## Entity * getEntity ( long long entity_id , bool auto_create = true )

Returns the [interface](../../../../../api/library/plugins/ig/api/class.entity_cpp.md) of the specified entity.
### Arguments

- *long long* **entity_id** - ID of the entity. > **Notice:** The value should be the [entity ID](../../../../../api/library/plugins/ig/api/class.entity_cpp.md#getID_llong), **not** the [type ID](../../../../../api/library/plugins/ig/api/class.entity_cpp.md#getType_llong).
- *bool* **auto_create** - true to automatically create the entity with the specified ID if it doesn't exist yet; false - to return nullptr in case the entity doesn't exist.

### Return value

Pointer to the entity interface.
## bool removeEntity ( long long entity_id )

Removes the entity with the specified ID.
### Arguments

- *long long* **entity_id** - ID of the entity to be removed. > **Notice:** The value should be the [entity ID](../../../../../api/library/plugins/ig/api/class.entity_cpp.md#getID_llong), **not** the [type ID](../../../../../api/library/plugins/ig/api/class.entity_cpp.md#getType_llong).

### Return value

true if the entity with the specified ID is removed successfully; otherwise - false.
## bool isEntityExist ( long long entity_id ) const

Returns a value indicating if the entity with the specified ID exists.
### Arguments

- *long long* **entity_id** - ID of the entity. > **Notice:** The value should be the [entity ID](../../../../../api/library/plugins/ig/api/class.entity_cpp.md#getID_llong), **not** the [type ID](../../../../../api/library/plugins/ig/api/class.entity_cpp.md#getType_llong).

### Return value

true if the entity with the specified ID exists; otherwise - false.
## void getEntities ( Unigine:: Vector < Entity *> & entities_ret ) const

Fills the list of entities with all existing entities.
### Arguments

- *Unigine::[Vector](../../../../../api/library/containers/vector/class.vector_cpp.md)<[Entity](../../../../../api/library/plugins/ig/api/class.entity_cpp.md) *> &* **entities_ret** - List of entities.

## Entity * findEntity ( const Ptr < Node > & node ) const

Returns the [interface](../../../../../api/library/plugins/ig/api/class.entity_cpp.md) of the entity represented by the specified node.
### Arguments

- *const [Ptr](../../../../../api/library/common/class.ptr_cpp.md)<[Node](../../../../../api/library/nodes/class.node_cpp.md)> &* **node** - Node for which an entity is to be found.

### Return value

Pointer to the entity interface if it exists; otherwise - nullptr.
## long long findEntityType ( const char * type_name ) const


Returns the ID of the entity type by its name. Entity type ID and name define the type of the entity to be used for a specific instance and are set in the [entity definition section](../../../../../ig/config.md#config_entities) of the IG configuration file as follows:


```xml
<entity_types>
	<entity id="111" name="b52">
	</entity>
</entity_types>

```


### Arguments

- *const char ** **type_name** - Entity type name.

### Return value

Entity type ID.
## int findComponentID ( long long entity_type , const char * name ) const

Returns the ID of the component with the given name, which belongs to the specified entity type.
### Arguments

- *long long* **entity_type** - Entity type ID. > **Notice:** Entity type ID is defined in the [entity definition section](../../../../../ig/config.md#config_entities) of the IG configuration file.
- *const char ** **name** - Component name.

### Return value

Component ID.
## int findArticulatedPartID ( long long entity_type , const char * name ) const

Returns the identifier of an articulated part by its name and the type of the entity it belongs to, stored in the IG configuration file (`ig_config.xml`).
### Arguments

- *long long* **entity_type** - Entity [type identifier](../../../../../ig/config.md#typeid) indicated in the IG configuration file (`ig_config.xml`).
- *const char ** **name** - Name of an articulated part indicated in the IG configuration file (`ig_config.xml`).

### Return value

Identifier of an articulated part.
## bool getHatHot ( const Vec3 & geo_position , double & ret_hat , double & ret_hot , IGIntersection & ret_intersection ) const

Checks if there is anything in the given geodetic position and returns HAT/HOT as well as surface normal, exact object over which the request was made, intersected surface, world coordinates of the intersection point, etc. to the specified output variables.
### Arguments

- *const [Vec3](../../../../../api/library/math/class.vec3_cpp.md) &* **geo_position** - Geodetic position.
- *double &* **ret_hat** - Address for the return HAT value.
- *double &* **ret_hot** - Address for the return HOT value.
- *IGIntersection &* **ret_intersection** - [Information on intersection](../../../../../api/library/plugins/ig/api/class.igintersection_cpp.md) at the given geodetic position, such as exact object over which the request was made, intersected surface, world coordinates of the intersection point, etc.

### Return value

true, if there is anything in the given geodetic position, otherwise false.
## bool getIntersection ( const Vec3 & p0 , const Vec3 & p1 , int mask , Unigine:: Vector <IGIntersection> & ret ) const

Checks if the ray with set points intersects with anything.
### Arguments

- *const [Vec3](../../../../../api/library/math/class.vec3_cpp.md) &* **p0** - Ray origin.
- *const [Vec3](../../../../../api/library/math/class.vec3_cpp.md) &* **p1** - Point along the ray.
- *int* **mask** - Intersection mask.
- *Unigine::[Vector](../../../../../api/library/containers/vector/class.vector_cpp.md)<IGIntersection> &* **ret** - Vector containing [information on intersections](../../../../../api/library/plugins/ig/api/class.igintersection_cpp.md).

### Return value

true, if the ray intersects with anything, otherwise false.
## Water * getWater ( ) const

Returns the interface of the water control.
### Return value

Water control interface.
## Unigine::Plugins::Syncker::Syncker * getSyncker ( ) const

Returns the [Syncker Interface](../../../../../api/library/plugins/syncker/class.syncker_syncker_cpp.md).
### Return value

Pointer to the Syncker::Syncker interface.
## Unigine::Plugins::Syncker::Master * getSynckerMaster ( ) const

Returns the [Syncker Master Interface](../../../../../api/library/plugins/syncker/class.syncker_master_cpp.md).
### Return value

Pointer to the Syncker::Master interface.
## Unigine::Plugins::Syncker::Slave * getSynckerSlave ( ) const

Returns the [Syncker Slave Interface](../../../../../api/library/plugins/syncker/class.syncker_slave_cpp.md).
### Return value

Pointer to the Syncker::Slave interface.
## Ptr < Node > loadNode ( const char * file_path )


Loads a node from the specified file to the world on the Master and all Slaves. This is a network analogue of the [loadNode()](../../../../../api/library/engine/class.world_cpp.md#loadNode_cstr_int_Node) method of the *World* class.


> **Notice:** This is a safe analogue of the [Syncker](../../../../../api/library/plugins/syncker/index.md) method *[loadNode()](../../../../../api/library/plugins/syncker/class.syncker_master_cpp.md#loadNode_cstr_uchar_Mat4_Node)* that has an internal check if this method runs on the master and if Syncker is running.


### Arguments

- *const char ** **file_path** - Path to the `*.node` file.

### Return value

Loaded node or nullptr if an error has occurred.
## void syncNode ( const Ptr < Node > & node , unsigned char mask = 255 )


Enables synchronization of parameters of the given node via the UDP protocol. Scene nodes are not synchronized by default, this method is used to add a particular node to the synchronization queue.


> **Notice:** This is a safe analogue of the [Syncker](../../../../../api/library/plugins/syncker/index.md) method *[addSyncNode()](../../../../../api/library/plugins/syncker/class.syncker_master_cpp.md#addSyncNode_Node_uchar_void)* that has an internal check if this method runs on the master and if Syncker is running. If this method is called on a slave, it does nothing.


### Arguments

- *const [Ptr](../../../../../api/library/common/class.ptr_cpp.md)<[Node](../../../../../api/library/nodes/class.node_cpp.md)> &* **node** - Node to synchronize.
- *unsigned char* **mask** - Synchronization mask.

## void synckerCreate ( const Ptr < Node > & node , unsigned char mask = 255 )


Synchronizes creation of the given node on all Slaves. This method is **to be called after node creation on the Master**. It is recommended to use the [*loadNode()*](#loadNode_cstr_Node) method whenever possible as this approach **allows adding nodes of all types**, unlike the [*synckerCreate()*](#synckerCreate_Node_uchar_void) method that supports only a limited number of them.


> **Notice:** This is a safe analogue of the [Syncker](../../../../../api/library/plugins/syncker/index.md) method [createNode()](../../../../../api/library/plugins/syncker/class.syncker_master_cpp.md#createNode_Node_uchar_bool) that has an internal check if this method runs on the master and if Syncker is running. If this method is called on a slave, it does nothing.


### Arguments

- *const [Ptr](../../../../../api/library/common/class.ptr_cpp.md)<[Node](../../../../../api/library/nodes/class.node_cpp.md)> &* **node** - Node to create.
- *unsigned char* **mask** - Synchronization mask.

## void synckerDestroy ( const Ptr < Node > & in_node )


Synchronizes deletion of the given node (with all its children) on the Master and all Slaves.


> **Notice:** This is a safe analogue of the [Syncker](../../../../../api/library/plugins/syncker/index.md) method [deleteNode()](../../../../../api/library/plugins/syncker/class.syncker_master_cpp.md#deleteNode_Node_void) that has an internal check if this method runs on the master and if Syncker is running. If this method is called on a slave, it does nothing.


### Arguments

- *const [Ptr](../../../../../api/library/common/class.ptr_cpp.md)<[Node](../../../../../api/library/nodes/class.node_cpp.md)> &* **in_node** - Node to delete.

## bool isSyncNode ( const Ptr < Node > & in_node ) const


Returns a value indicating if synchronization of the given node is enabled. Using this method you can quickly check if a node is monitored by the Syncker (node's states are dispatched to Slaves over the network).


> **Notice:** This is a safe analogue of the [Syncker](../../../../../api/library/plugins/syncker/index.md) method [isSyncNode()](../../../../../api/library/plugins/syncker/class.syncker_master_cpp.md#isSyncNode_Node_bool) that has an internal check if this method runs on the master and if Syncker is running. If this method is called on a slave, it does nothing.


### Arguments

- *const [Ptr](../../../../../api/library/common/class.ptr_cpp.md)<[Node](../../../../../api/library/nodes/class.node_cpp.md)> &* **in_node** - Node to be checked.

### Return value

true if synchronization of the given node is enabled; otherwise, false.
## bool checkEntityType ( long long entity_type ) const

Checks if the given entity type is supported by IG.
### Arguments

- *long long* **entity_type** - Entity [type identifier](../../../../../ig/config.md#typeid)

### Return value

true, if the given entity type is supported, otherwise false.
## void sendUserMessage ( unsigned char packet_code , const Ptr < Blob > & send_message )

Sends user message from the master to a slave.
### Arguments

- *unsigned char* **packet_code** - Packet ID.
- *const [Ptr](../../../../../api/library/common/class.ptr_cpp.md)<[Blob](../../../../../api/library/common/class.blob_cpp.md)> &* **send_message** - User message

## void * addOnUserMessageReceivedCallback ( uint8_t packet_code , Unigine:: CallbackBase1 < Unigine:: Blob Ptr >* callback )

Executes the callback function when the [user message](#sendUserMessage_uchar_Blob_void) from the master is received.
### Arguments

- *uint8_t* **packet_code** - Packet ID.
- *Unigine::[CallbackBase1](../../../../../api/library/common/callbacks/class.callbackbase1_cpp.md) <  Unigine::[Blob](../../../../../api/library/common/class.blob_cpp.md)Ptr >** **callback** - Callback pointer. The callback function must have the following signature: void (*Unigine::BlobPtr* ***blob**)

### Return value

Callback subscriber ID. This ID can be used to [remove](#removeOnUserMessageReceivedCallback_void_ptr_bool) this callback when necessary.
## void removeOnUserMessageReceivedCallback ( void * subscriber )

Removes a callback on receiving a user message for the specified subscriber.
### Arguments

- *void ** **subscriber** - Callback subscriber ID specified when [adding](#addOnUserMessageReceivedCallback_uchar_CallbackBase1_ptr_void) it.

## void clearOnUserMessageReceivedCallbacks ( )

Clears all [added](#addOnUserMessageReceivedCallback_uchar_CallbackBase1_ptr_void) callbacks on on receiving a user message.
## Manager * get ( )

Returns the [Manager](../../../../../api/library/plugins/ig/api/class.managerinterface_cpp.md) interface.
### Return value

Pointer to the [manager interface](../../../../../api/library/plugins/ig/api/class.managerinterface_cpp.md).
## void setDistanceScale ( float d )


Sets the global distance scale for all rendering distance parameters: shadow distance, light distance, LOD distances, etc. (see [render_distance_scale](../../../../../code/console/index.md#render_distance_scale) console command) and for the IG Simplifier component. The Simplifier component can help optimize rendering of your entities. When assigned to an entity, it enables you to define which parts of its model can be neglected starting at certain distance levels (e.g., hide flaps, ailerons, and rudders at 1km, engines at 5 km, etc.) and which substitutes can be used to represent an entity at a large distance (e.g., a flashing strobe light, when the plane is just a point on the screen).


> **Notice:** This method calls the [*setDistanceScale()*](../../../../../api/library/rendering/class.render_cpp.md#setDistanceScale_float_void) of the *Render* class.


### Arguments

- *float* **d** - Global rendering distance scale and Simplifier component (IG LOD manager).

## void setAdaptiveQualitySystemMode ( int mode )

Sets a new Adaptive Quality System mode. This system provides automatic real-time adjustment of levels of detail depending on current performance ([render_distance_scale](../../../../../code/console/index.md#render_distance_scale) and simplifier_distance_scale).
### Arguments

- *int* **mode** - Adaptive Quality System mode to be set. One of the following values:

  - 0 - real-time quality adjustment is disabled
  - 1 - degradation mode only (image quality is degraded if the performance goes down)
  - 2 - automatic real-time adjustment (image quality is degraded if the performance is low, and improved if the performance increases)

## void destroyObjects ( )

Destroys all [entities](../../../../../api/library/plugins/ig/api/class.entity_cpp.md), [views](../../../../../api/library/plugins/ig/api/class.view_cpp.md), and [view groups](../../../../../api/library/plugins/ig/api/class.viewgroup_cpp.md).
## void setSlaveViewByName ( const char * slave_name , int view_id )

Sets a view with the specified ID to be used for the specified Slave (available for Master IG only).
### Arguments

- *const char ** **slave_name** - Slave name (-computer_name "").
- *int* **view_id** - ID of the view to be set as current for the specified Slave.

## void setSlaveView ( int index , int view_id )

Sets a view with the specified ID to be used for a certain Slave by its index (available for Master IG only).
### Arguments

- *int* **index** - Slave index in the range from 0 to the [total numer of Slaves](#getNumSlaves_int).
- *int* **view_id** - ID of the view to be set as current for the specified Slave.

## int getSlaveViewByName ( const char * slave_name ) const

Returns the current view ID used for a certain Slave by its name.
### Arguments

- *const char ** **slave_name** - Slave name.

### Return value

ID of the view used for the Slave with the specified name.
## int getSlaveView ( int slave_index ) const

Returns the current view ID used for a certain Slave by its index (available for Master IG only).
### Arguments

- *int* **slave_index** - Slave index in the range from 0 to the [total numer of Slaves](#getNumSlaves_int).

### Return value

ID of the view used for the Slave with the specified index.
## void clearInterpolationData ( )

Clears all interpolation data for all entities.
## Plugins::Geodetics::Transformer * getGeodeticsTransformer ( ) const

Returns a pointer to the instance of the [Geodetics::Transformer](../../../../../api/library/geodetics/geodetics_plugin/class.transformer_cpp.md) class if the [Geodetics](../../../../../code/plugins/geodetics/index_cpp.md) plugin is loaded. This class is used to transform geodetic coordinates (latitude, longitude and altitude) to the 3D world position and vice versa.
## int getNumSlaves ( ) const

Returns the total number of Slaves (available for Master IG only).
### Return value

Total number of IG Slaves.
## const char * getSlaveName ( int index ) const

Returns Slave name by its index (available for Master IG only).
### Arguments

- *int* **index** - Slave index.

### Return value

Name of the Slave with the specified index.
## const char * getSynckerName ( ) const

Returns the current name of the IG host.
### Return value

Current name of the IG host.
## void setDebugMode ( IG::Manager::DEBUG_MODE mode , bool enabled )

Sets a value indicating if the specified [Debug mode](../../../../../ig/debug/index.md) is enabled. This mode allows inspecting the IG application at run-time
### Arguments

- *IG::Manager::DEBUG_MODE* **mode** - Debug mode type. One of the [DEBUG_MODE_*](#DEBUG_MODE) values.
- *bool* **enabled** - true - to enable the specified [Debug mode](../../../../../ig/debug/index.md); false - to disable it.

## bool isDebugMode ( IG::Manager::DEBUG_MODE mode ) const

Returns a value indicating if the specified [Debug mode](../../../../../ig/debug/index.md) is enabled. This mode allows inspecting the IG application at run-time
### Arguments

- *IG::Manager::DEBUG_MODE* **mode** - Debug mode type. One of the [DEBUG_MODE_*](#DEBUG_MODE) values.

### Return value

true if the specified IG Debug mode is enabled; otherwise, false.
## float calcDebugScale ( float v ) const

Returns the actual scale of [Debug](../../../../../ig/debug/index.md) visualizer elements calculated for the specified value based on the current [type of dimensions](#setDebugScreenspace_int_void) (world/screen) and the current [debug scale](#setDebugScale_float_void) value.
### Arguments

- *float* **v** - Initial scale value.

### Return value

Actual scale of [Debug](../../../../../ig/debug/index.md) visualizer elements calculated for the specified value. The scale is calculated based on the current [debug scale](#setDebugScale_float_void) value.
## void * addOnCreateViewCallback ( void * subscriber , CallbackBase * callback )

Adds a callback function to be executed on creating a new [view](../../../../../api/library/plugins/ig/api/class.view_cpp.md). The signature of the callback function is as follows:


```text
void(View *)
```


### Arguments

- *void ** **subscriber** - Callback subscriber. Can be used to remove the added callback via the *[removeOnCreateViewCallback()](#removeOnCreateViewCallback_void_ptr_void)* method.
- *[CallbackBase](../../../../../api/library/common/callbacks/class.callbackbase_cpp.md) ** **callback** - Callback function to be executed.

### Return value

ID of the last added Create View callback, if the callback was added successfully; otherwise, **nullptr**. This ID can be used to [remove](#removeOnCreateViewCallback_void_ptr_void) this callback when necessary.
## void removeOnCreateViewCallback ( void * subscriber )

Removes a callback function for the specified subscriber from the list of callbacks to be executed on creating a new [view](../../../../../api/library/plugins/ig/api/class.view_cpp.md).
### Arguments

- *void ** **subscriber** - Callback subscriber.

## void clearOnCreateViewCallbacks ( )

Clears all [added](#addOnCreateViewCallback_void_ptr_CallbackBase_ptr_void) Create View callbacks.
## void * addOnCreateViewGroupCallback ( void * subscriber , CallbackBase * callback )

Adds a callback function to be executed on creating a new [view](../../../../../api/library/plugins/ig/api/class.view_cpp.md). The signature of the callback function is as follows:


```text
void(ViewGroup *)
```


### Arguments

- *void ** **subscriber** - Callback subscriber. Can be used to remove the added callback via the *[removeOnCreateViewGroupCallback()](#removeOnCreateViewGroupCallback_void_ptr_void)* method.
- *[CallbackBase](../../../../../api/library/common/callbacks/class.callbackbase_cpp.md) ** **callback** - Callback function to be executed.

## void removeOnCreateViewGroupCallback ( void * subscriber )

Removes a callback function for the specified subscriber from the list of callbacks to be executed on creating a new [view group](../../../../../api/library/plugins/ig/api/class.viewgroup_cpp.md).
### Arguments

- *void ** **subscriber** - Callback subscriber.

## void clearOnCreateViewGroupCallbacks ( )

Clears all [added](#addOnCreateViewGroupCallback_void_ptr_CallbackBase_ptr_void) Create ViewGroup callbacks.
## void addOnCreateEntityCallback ( void * subscriber , CallbackBase * callback )

Adds a callback function to be executed on creating a new [entity](../../../../../api/library/plugins/ig/api/class.entity_cpp.md). The signature of the callback function is as follows:


```text
void(IG::ICollisionVolume *volume, Unigine::ContactPtr contact, int contacted_entity, int contacted_volume)
```


### Arguments

- *void ** **subscriber** - Callback subscriber. Can be used to remove the added callback via the *[removeOnCreateEntityCallback()](#removeOnCreateEntityCallback_void_ptr_void)* method.
- *[CallbackBase](../../../../../api/library/common/callbacks/class.callbackbase_cpp.md) ** **callback** - Callback function to be executed.

## void removeOnCreateEntityCallback ( void * subscriber )

Removes a callback function for the specified subscriber from the list of callbacks to be executed on creating a new [entity](../../../../../api/library/plugins/ig/api/class.entity_cpp.md).
### Arguments

- *void ** **subscriber** - Callback subscriber.

## void clearOnCreateEntityCallbacks ( )

Clears all [added](#addOnCreateEntityCallback_void_ptr_CallbackBase_ptr_void) Create Entity callbacks.
## void addOnCollisionVolumeDetectedCallback ( void * subscriber , CallbackBase * callback )

Adds a callback function to be executed on detecting an intersection with a [collision volume](../../../../../api/library/plugins/ig/api/class.collisionvolume_cpp.md). The signature of the callback function is as follows:


```text
void(IG::ICollisionVolume *volume, Unigine::ContactPtr contact, int contacted_entity, int contacted_volume)
```


### Arguments

- *void ** **subscriber** - Callback subscriber. Can be used to remove the added callback via the *[removeOnCollisionVolumeDetectedCallback()](#removeOnCollisionVolumeDetectedCallback_void_ptr_void)* method.
- *[CallbackBase](../../../../../api/library/common/callbacks/class.callbackbase_cpp.md) ** **callback** - Callback function to be executed.

## void removeOnCollisionVolumeDetectedCallback ( void * subscriber )

Removes a callback function for the specified subscriber from the list of callbacks to be executed on detecting an intersection with a [collision volume](../../../../../api/library/plugins/ig/api/class.collisionvolume_cpp.md).
### Arguments

- *void ** **subscriber** - Callback subscriber.

## void clearOnCollisionVolumeDetectedCallbacks ( )

Clears all [added](#addOnCollisionVolumeDetectedCallback_void_ptr_CallbackBase_ptr_void) CollisionVolume Detected callbacks.
## void addOnCollisionSegmentDetectedCallback ( void * subscriber , CallbackBase * callback )

Adds a callback function to be executed on detecting an intersection with a [collision segment](../../../../../api/library/plugins/ig/api/class.collisionsegment_cpp.md). The signature of the callback function is as follows:


```text
void(IG::ICollisionSegment *segment, Unigine::ObjectPtr object, Unigine::WorldIntersectionPtr intersection)
```


### Arguments

- *void ** **subscriber** - Callback subscriber. Can be used to remove the added callback via the *[removeOnCollisionSegmentDetectedCallback()](#removeOnCollisionSegmentDetectedCallback_void_ptr_void)* method.
- *[CallbackBase](../../../../../api/library/common/callbacks/class.callbackbase_cpp.md) ** **callback** - Callback function to be executed.

## void removeOnCollisionSegmentDetectedCallback ( void * subscriber )

Removes a callback function for the specified subscriber from the list of callbacks to be executed on detecting an intersection with a [collision segment](../../../../../api/library/plugins/ig/api/class.collisionsegment_cpp.md).
### Arguments

- *void ** **subscriber** - Callback subscriber.

## void clearOnCollisionSegmentDetectedCallbacks ( )

Clears all [added](#addOnCollisionSegmentDetectedCallback_void_ptr_CallbackBase_ptr_void) CollisionSegment Detected callbacks.
## void addOnIGReadyCallback ( void * subscriber , CallbackBase * callback )

Adds a callback function to be executed when all Slaves that were waited for by the IG are connected. The signature of the callback function is as follows:


```text
void()
```


### Arguments

- *void ** **subscriber** - Callback subscriber. Can be used to remove the added callback via the *[removeOnIGReadyCallback()](#removeOnIGReadyCallback_void_ptr_void)* method.
- *[CallbackBase](../../../../../api/library/common/callbacks/class.callbackbase_cpp.md) ** **callback** - Callback function to be executed.

## void removeOnIGReadyCallback ( void * subscriber )

Removes a callback function for the specified subscriber from the list of callbacks to be executed when all Slaves that were waited for by the IG are connected.
### Arguments

- *void ** **subscriber** - Callback subscriber.

## void clearOnIGReadyCallbacks ( )

Clears all [added](#addOnIGReadyCallback_void_ptr_CallbackBase_ptr_void) IG Ready callbacks.
## void addOnSlaveConnectedCallback ( void * subscriber , CallbackBase * callback )

Adds a callback function to be executed on connecting a new Slave. The signature of the callback function is as follows:


```text
void(int slave_index, const char * slave_name)
```


### Arguments

- *void ** **subscriber** - Callback subscriber. Can be used to remove the added callback via the *[removeOnSlaveConnectedCallback()](#removeOnSlaveConnectedCallback_void_ptr_void)* method.
- *[CallbackBase](../../../../../api/library/common/callbacks/class.callbackbase_cpp.md) ** **callback** - Callback function to be executed.

## void removeOnSlaveConnectedCallback ( void * subscriber )

Removes a callback function for the specified subscriber from the list of callbacks to be executed on connecting a new Slave.
### Arguments

- *void ** **subscriber** - Callback subscriber.

## void clearOnSlaveConnectedCallbacks ( )

Clears all [added](#addOnSlaveConnectedCallback_void_ptr_CallbackBase_ptr_void) Slave Connected callbacks.
## void addOnSlaveDisconnectedCallback ( void * subscriber , CallbackBase * callback )

Adds a callback function to be executed on disconnecting a Slave. The signature of the callback function is as follows:


```text
void(int slave_index)
```


### Arguments

- *void ** **subscriber** - Callback subscriber. Can be used to remove the added callback via the *[removeOnSlaveDisconnectedCallback()](#removeOnSlaveDisconnectedCallback_void_ptr_void)* method.
- *[CallbackBase](../../../../../api/library/common/callbacks/class.callbackbase_cpp.md) ** **callback** - Callback function to be executed.

## void removeOnSlaveDisconnectedCallback ( void * subscriber )

Removes a callback function for the specified subscriber from the list of callbacks to be executed on disconnecting a Slave.
### Arguments

- *void ** **subscriber** - Callback subscriber.

## void clearOnSlaveDisconnectedCallbacks ( )

Clears all [added](#addOnSlaveDisconnectedCallback_void_ptr_CallbackBase_ptr_void) Slave Disconnected callbacks.
## void setPropertyWarningEnabled ( bool v )

Sets the value indicating if the property-related warnings should be displayed in the console. This is a convenience method that might be useful when working with C# components.
### Arguments

- *bool* **v** - true to display property-related warnings; false to disable them.
