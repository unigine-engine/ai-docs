# Unigine::Plugins::IG::Manager Class (CS)

> **Notice:** This class is a singleton.


This class represents the IG Manager interface.


> **Notice:** IG plugin must be loaded.


## Manager Class

### Enums

## DEBUG_MODE

| Name | Description |
|---|---|
| **REQUEST_DEBUG** = 0 | Debug mode visualizing where LOS/HAT/HOT requests are sent to. |
| **ENTITY_PATH_TRACE** = 1 | Debug mode with entity path tracing - positions between frames and data sent over the network. Blue points mark data from the server; pink arrows - movement between frames. |
| **ENTITY_PATH_TRACE_TIME** = 2 | Debug mode visualizing entity path tracing time. |
| **ENTITY_COLLISION_SEGMENT** = 3 | Debug mode visualizing collision segments for every entity. |
| **ENTITY_COLLISION_VOLUME** = 4 | Debug mode visualizing collision volumes for every entity. |
| **ENTITY_INFO** = 5 | Debug mode visualizing the basis for every CIGI and DIS entity with the ID, type, and type name specified (information is taken from the [IG configuration](../../../../../ig/config.md) file). |
| **METEO** = 6 | Debug mode visualizing meteo information. |
| **INTERPOLATION_INFO** = 7 | Debug mode visualizing the interpolation timer parameters and states on the screen. Displaying of these data can also be enabled by the console command ig_debug_interpolation. |

### Properties

## float DebugScale

The scale multiplier for [Debug](../../../../../ig/debug/index.md) visualizer elements.
## bool DebugDepth

The value indicating if depth testing for the [Debug](../../../../../ig/debug/index.md) visualizer elements is enabled (if elements should be obscured by the ones closer to the camera).
## bool DebugScreenspace

The value indicating the type of dimension to be used when rendering [Debug](../../../../../ig/debug/index.md) visualizer elements: the screen-space dimension or the world-space dimension.
## float DebugDuration

The time period during which [Debug](../../../../../ig/debug/index.md) visualizer elements are displayed.
## bool DebugEnabled

The value indicating if the [Debug mode](../../../../../ig/debug/index.md) is enabled. This mode allows inspecting the IG application at run-time.
## int CollisionVolumeMask

The collision volume mask for entities.
## int TerrainIntersectionMask

The [intersection mask](../../../../../principles/bit_masking/index.md#intersection_mask) that is used to define the ground/landing surface.
## 🔒︎ bool IsTerrainCurved

The value indicating if terrain is curved.
## 🔒︎ dvec3 GeodeticOrigin

The geodetic origin coordinates.
## 🔒︎ GeodeticPivot GeodeticPivot

The geodetic pivot used to curve the terrain.
## 🔒︎ ObjectTerrainGlobal Terrain

The Global Terrain object.
## bool Interpolation

The value indicating if [interpolation and extrapolation](../../../../../ig/index.md#interpolation) for the IG is enabled.
## double InterpolationLerpFactor

The
interpolation lerp factor value for the IG. The *lower* the value the smoother movement will be, but it will feel like objects move underwater or in a jelly, *higher* values result in higher positioning accuracy (objects positions will be closer to actual ones for the current frame), but objects will move with a noticeable jitter.


> **Notice:** [Frame-to-frame interpolation](#setInterpolationLerp_int_void) mode must be enabled.


## double ExtrapolationPeriod

The extrapolation period value for the IG.
## double InterpolationPeriod

The interpolation period value for the IG.
## double InterpolationTime

The interpolation time value for the IG.
## bool InterpolationLerp

The value indicating if interpolation between the current and previous frames for the IG is enabled.
## int InterpolationBufferSize

The size of the [interpolation](../../../../../ig/index.md#interpolation) buffer. It is recommended to set buffer size equal to the number of messages received during two [interpolation periods](#setInterpolationPeriod_double_void).
## int CurrentView

The view by its ID. If the view with the specified ID does not exist, it will be created automatically.
## 🔒︎ Converter Converter

The *[converter](../../../../../api/library/geodetics/geodetics_plugin/class.transformer_cs.md)* interface.
## 🔒︎ NEDConverter NEDConverter

The *[NEDConverter](../../../../../api/library/plugins/ig/api/class.nedconverter_cs.md)* interface.
## 🔒︎ LightController LightController

The light controller interface.
## 🔒︎ Meteo Meteo

The Meteo interface.
## 🔒︎ SkyMap SkyMap

The SkyMap interface.
## 🔒︎ IGConfig Config

The IG configuration as an [IGConfig](../../../../../api/library/plugins/ig/api/class.igconfig_cs.md) class instance.
## 🔒︎ bool IsDatabaseLoaded

The value indicating if any database is currently loaded.
## 🔒︎ int CurrentDatabaseID

The identifier of the currently loaded world database stored in the IG configuration file (`ig_config.xml`).
## 🔒︎ float IFps

The inverse FPS value (the time in seconds it took to complete the last frame). This method is similar to the [*Game::getIFps()*](../../../../../api/library/engine/class.game_cs.md#getIFps_float) but it is more preferred for multi-channel systems as it implements more accurate frame time calculation (including spike-periods).
## bool Freeze

The value indicating if execution of IG logic is temporarily put on hold (paused) or resumed.
## 🔒︎ bool IsReady

The value indicating if all Slaves that were waited for by the IG have connected.
## 🔒︎ bool IsMaster

The value indicating if the IG application is a Syncker-Master or runs in a single mode without the [Syncker](../../../../../code/plugins/syncker/index.md) at all; or if the IG application is a Syncker-Slave.
### Members

---

## void ReloadConfig ( )

Reloads the [IG Configuration file](../../../../../ig/config.md) (`ig_config.xml`).
## void ReloadGeodetics ( )

Forces a runtime update of georeferencing data, which is useful for on-the-fly projection changes.
## bool LoadDatabase ( int database_id )

Loads the database with the specified ID and sets it to be used.
### Arguments

- *int* **database_id** - ID of the database to be used.

### Return value

true means that the database with the specified ID is loaded successfully; otherwise, false.
## void ReloadDatabase ( )

***Console*:**`database_reload`Reloads the current database.
## void UnloadDatabase ( )

Unloads the current database.
## int GetDatabaseID ( string world_name )

Returns the identifier of the world database with the specified name stored in the IG configuration file (`ig_config.xml`).
### Arguments

- *string* **world_name** - World database name.

### Return value

Identifier of the specified world database, or 0, if no world is loaded.
## string GetDatabaseName ( int id )

Returns the name of the world database stored in the IG configuration file (`ig_config.xml`).
### Arguments

- *int* **id** - Identifier of the world database.

### Return value

The world database name.
## SymbolsController * getSymbolsController ( )

Returns the interface of the symbols controller.
### Return value

Symbols controller interface.
## View GetView ( int view_id , bool auto_create )

Returns the [interface](../../../../../api/library/plugins/ig/api/class.view_cs.md) of the specified view.
### Arguments

- *int* **view_id** - ID of the view.
- *bool* **auto_create** - true to automatically create the view with the specified ID if it doesn't exist yet; false - to return nullptr in case the view doesn't exist.

### Return value

View interface if it exists; otherwise - NULL.
## bool RemoveView ( int view_id )

Removes the view with the specified ID.
### Arguments

- *int* **view_id** - ID of the view to be removed.

### Return value

true if the view with the specified ID is removed successfully; otherwise - false.
## bool IsViewExist ( int view_id )

Returns a value indicating if the view with the specified ID exists.
### Arguments

- *int* **view_id** - ID of the view.

### Return value

true if the view with the specified ID exists; otherwise - false.
## ViewGroup GetViewGroup ( int group_id , bool auto_create )

Returns the [interface](../../../../../api/library/plugins/ig/api/class.viewgroup_cs.md) of the specified view group.
### Arguments

- *int* **group_id** - ID of the view group.
- *bool* **auto_create** - true to automatically create the view group with the specified ID if it doesn't exist yet; false - to return nullptr in case the view group doesn't exist.

### Return value

View group interface if it exists; otherwise - NULL.
## bool RemoveViewGroup ( int group_view_id )

Removes the view group with the specified ID.
### Arguments

- *int* **group_view_id** - ID of the view group to be removed.

### Return value

true if the view group with the specified ID is removed successfully; otherwise - false.
## bool IsViewGroupExist ( int group_view_id )

Returns a value indicating if the view group with the specified ID exists.
### Arguments

- *int* **group_view_id** - ID of the view group.

### Return value

true if the view group with the specified ID exists; otherwise - false.
## Entity GetEntity ( long entity_id , bool auto_create = true )

Returns the [interface](../../../../../api/library/plugins/ig/api/class.entity_cs.md) of the specified entity.
### Arguments

- *long* **entity_id** - ID of the entity. > **Notice:** The value should be the [entity ID](../../../../../api/library/plugins/ig/api/class.entity_cs.md#getID_llong), **not** the [type ID](../../../../../api/library/plugins/ig/api/class.entity_cs.md#getType_llong).
- *bool* **auto_create** - true to automatically create the entity with the specified ID if it doesn't exist yet; false - to return nullptr in case the entity doesn't exist.

### Return value

## bool RemoveEntity ( long entity_id )

Removes the entity with the specified ID.
### Arguments

- *long* **entity_id** - ID of the entity to be removed. > **Notice:** The value should be the [entity ID](../../../../../api/library/plugins/ig/api/class.entity_cs.md#getID_llong), **not** the [type ID](../../../../../api/library/plugins/ig/api/class.entity_cs.md#getType_llong).

### Return value

true if the entity with the specified ID is removed successfully; otherwise - false.
## bool IsEntityExist ( long entity_id )

Returns a value indicating if the entity with the specified ID exists.
### Arguments

- *long* **entity_id** - ID of the entity. > **Notice:** The value should be the [entity ID](../../../../../api/library/plugins/ig/api/class.entity_cs.md#getID_llong), **not** the [type ID](../../../../../api/library/plugins/ig/api/class.entity_cs.md#getType_llong).

### Return value

true if the entity with the specified ID exists; otherwise - false.
## void getEntities ( Unigine::Vector< Entity *> & entities_ret )

Fills the list of entities with all existing entities.
### Arguments

- *Unigine::Vector<[Entity](../../../../../api/library/plugins/ig/api/class.entity_cs.md) *> &* **entities_ret** - List of entities.

## Entity FindEntity ( Node node )

Returns the [interface](../../../../../api/library/plugins/ig/api/class.entity_cs.md) of the entity represented by the specified node.
### Arguments

- *[Node](../../../../../api/library/nodes/class.node_cs.md)* **node** - Node for which an entity is to be found.

### Return value

## long FindEntityType ( string type_name )


Returns the ID of the entity type by its name. Entity type ID and name define the type of the entity to be used for a specific instance and are set in the [entity definition section](../../../../../ig/config.md#config_entities) of the IG configuration file as follows:


```xml
<entity_types>
	<entity id="111" name="b52">
	</entity>
</entity_types>

```


### Arguments

- *string* **type_name** - Entity type name.

### Return value

Entity type ID.
## int FindComponentID ( long entity_type , string name )

Returns the ID of the component with the given name, which belongs to the specified entity type.
### Arguments

- *long* **entity_type** - Entity type ID. > **Notice:** Entity type ID is defined in the [entity definition section](../../../../../ig/config.md#config_entities) of the IG configuration file.
- *string* **name** - Component name.

### Return value

Component ID.
## int FindArticulatedPartID ( long entity_type , string name )

Returns the identifier of an articulated part by its name and the type of the entity it belongs to, stored in the IG configuration file (`ig_config.xml`).
### Arguments

- *long* **entity_type** - Entity [type identifier](../../../../../ig/config.md#typeid) indicated in the IG configuration file (`ig_config.xml`).
- *string* **name** - Name of an articulated part indicated in the IG configuration file (`ig_config.xml`).

### Return value

Identifier of an articulated part.
## bool GetHatHot ( dvec3 geo_position , out double ret_hat , out double ret_hot , IGIntersection ret_intersection )

Checks if there is anything in the given geodetic position and returns HAT/HOT as well as surface normal, exact object over which the request was made, intersected surface, world coordinates of the intersection point, etc. to the specified output variables.
### Arguments

- *dvec3* **geo_position** - Geodetic position.
- *out double* **ret_hat** - Address for the return HAT value.
- *out double* **ret_hot** - Address for the return HOT value.
- *IGIntersection* **ret_intersection** - [Information on intersection](../../../../../api/library/plugins/ig/api/class.igintersection_cs.md) at the given geodetic position, such as exact object over which the request was made, intersected surface, world coordinates of the intersection point, etc.

### Return value

true, if there is anything in the given geodetic position, otherwise false.
## bool GetIntersection ( dvec3 p0 , dvec3 p1 , int mask , ICollection<IGIntersection> ret )

Checks if the ray with set points intersects with anything.
### Arguments

- *dvec3* **p0** - Ray origin.
- *dvec3* **p1** - Point along the ray.
- *int* **mask** - Intersection mask.
- *ICollection<IGIntersection>* **ret** - Vector containing [information on intersections](../../../../../api/library/plugins/ig/api/class.igintersection_cs.md).

### Return value

true, if the ray intersects with anything, otherwise false.
## Water GetWater ( )

Returns the interface of the water control.
### Return value

Water control interface.
## Node LoadNode ( string file_path )


Loads a node from the specified file to the world on the Master and all Slaves. This is a network analogue of the [loadNode()](../../../../../api/library/engine/class.world_cs.md#loadNode_cstr_int_Node) method of the *World* class.


> **Notice:** This is a safe analogue of the [Syncker](../../../../../api/library/plugins/syncker/index.md) method *[loadNode()](../../../../../api/library/plugins/syncker/class.syncker_master_cs.md#loadNode_cstr_uchar_Mat4_Node)* that has an internal check if this method runs on the master and if Syncker is running.


### Arguments

- *string* **file_path** - Path to the `*.node` file.

### Return value

Loaded node or NULL if an error has occurred.
## void SyncNode ( Node node , byte mask = 255 )


Enables synchronization of parameters of the given node via the UDP protocol. Scene nodes are not synchronized by default, this method is used to add a particular node to the synchronization queue.


> **Notice:** This is a safe analogue of the [Syncker](../../../../../api/library/plugins/syncker/index.md) method *[addSyncNode()](../../../../../api/library/plugins/syncker/class.syncker_master_cs.md#addSyncNode_Node_uchar_void)* that has an internal check if this method runs on the master and if Syncker is running. If this method is called on a slave, it does nothing.


### Arguments

- *[Node](../../../../../api/library/nodes/class.node_cs.md)* **node** - Node to synchronize.
- *byte* **mask** - Synchronization mask.

## void SynckerCreate ( Node node , unsigned char mask = 255 )


Synchronizes creation of the given node on all Slaves. This method is **to be called after node creation on the Master**. It is recommended to use the [*loadNode()*](#loadNode_cstr_Node) method whenever possible as this approach **allows adding nodes of all types**, unlike the [*synckerCreate()*](#synckerCreate_Node_uchar_void) method that supports only a limited number of them.


> **Notice:** This is a safe analogue of the [Syncker](../../../../../api/library/plugins/syncker/index.md) method [createNode()](../../../../../api/library/plugins/syncker/class.syncker_master_cs.md#createNode_Node_uchar_bool) that has an internal check if this method runs on the master and if Syncker is running. If this method is called on a slave, it does nothing.


### Arguments

- *[Node](../../../../../api/library/nodes/class.node_cs.md)* **node** - Node to create.
- *unsigned char* **mask** - Synchronization mask.

## void SynckerDestroy ( Node in_node )


Synchronizes deletion of the given node (with all its children) on the Master and all Slaves.


> **Notice:** This is a safe analogue of the [Syncker](../../../../../api/library/plugins/syncker/index.md) method [deleteNode()](../../../../../api/library/plugins/syncker/class.syncker_master_cs.md#deleteNode_Node_void) that has an internal check if this method runs on the master and if Syncker is running. If this method is called on a slave, it does nothing.


### Arguments

- *[Node](../../../../../api/library/nodes/class.node_cs.md)* **in_node** - Node to delete.

## bool IsSyncNode ( Node in_node )


Returns a value indicating if synchronization of the given node is enabled. Using this method you can quickly check if a node is monitored by the Syncker (node's states are dispatched to Slaves over the network).


> **Notice:** This is a safe analogue of the [Syncker](../../../../../api/library/plugins/syncker/index.md) method [isSyncNode()](../../../../../api/library/plugins/syncker/class.syncker_master_cs.md#isSyncNode_Node_bool) that has an internal check if this method runs on the master and if Syncker is running. If this method is called on a slave, it does nothing.


### Arguments

- *[Node](../../../../../api/library/nodes/class.node_cs.md)* **in_node** - Node to be checked.

### Return value

true if synchronization of the given node is enabled; otherwise, false.
## bool CheckEntityType ( long entity_type )

Checks if the given entity type is supported by IG.
### Arguments

- *long* **entity_type** - Entity [type identifier](../../../../../ig/config.md#typeid)

### Return value

true, if the given entity type is supported, otherwise false.
## void SendUserMessage ( byte packet_code , Blob send_message )

Sends user message from the master to a slave.
### Arguments

- *byte* **packet_code** - Packet ID.
- *[Blob](../../../../../api/library/common/class.blob_cs.md)* **send_message** - User message

## IntPtr AddOnUserMessageReceivedCallback ( byte packet_code , OnUserMessageReceivedDelegate callback )

Executes the callback function when the [user message](#sendUserMessage_uchar_Blob_void) from the master is received.
### Arguments

- *byte* **packet_code** - Packet ID.
- *OnUserMessageReceivedDelegate* **callback** - Callback function with the following signature: void OnUserMessageReceived(*Blob* **blob**)

### Return value

Callback subscriber ID. This ID can be used to [remove](#removeOnUserMessageReceivedCallback_void_ptr_bool) this callback when necessary.
## void RemoveOnUserMessageReceivedCallback ( IntPtr subscriber )

Removes a callback on receiving a user message for the specified subscriber.
### Arguments

- *IntPtr* **subscriber** - Callback subscriber ID specified when [adding](#addOnUserMessageReceivedCallback_uchar_CallbackBase1_ptr_void) it.

## void ClearOnUserMessageReceivedCallbacks ( )

Clears all [added](#addOnUserMessageReceivedCallback_uchar_CallbackBase1_ptr_void) callbacks on on receiving a user message.
## void SetDistanceScale ( float d )


Sets the global distance scale for all rendering distance parameters: shadow distance, light distance, LOD distances, etc. (see [render_distance_scale](../../../../../code/console/index.md#render_distance_scale) console command) and for the IG Simplifier component. The Simplifier component can help optimize rendering of your entities. When assigned to an entity, it enables you to define which parts of its model can be neglected starting at certain distance levels (e.g., hide flaps, ailerons, and rudders at 1km, engines at 5 km, etc.) and which substitutes can be used to represent an entity at a large distance (e.g., a flashing strobe light, when the plane is just a point on the screen).


> **Notice:** This method calls the [*setDistanceScale()*](../../../../../api/library/rendering/class.render_cs.md#setDistanceScale_float_void) of the *Render* class.


### Arguments

- *float* **d** - Global rendering distance scale and Simplifier component (IG LOD manager).

## void SetAdaptiveQualitySystemMode ( int mode )

Sets a new Adaptive Quality System mode. This system provides automatic real-time adjustment of levels of detail depending on current performance ([render_distance_scale](../../../../../code/console/index.md#render_distance_scale) and simplifier_distance_scale).
### Arguments

- *int* **mode** - Adaptive Quality System mode to be set. One of the following values:

  - 0 - real-time quality adjustment is disabled
  - 1 - degradation mode only (image quality is degraded if the performance goes down)
  - 2 - automatic real-time adjustment (image quality is degraded if the performance is low, and improved if the performance increases)

## void DestroyObjects ( )

Destroys all [entities](../../../../../api/library/plugins/ig/api/class.entity_cs.md), [views](../../../../../api/library/plugins/ig/api/class.view_cs.md), and [view groups](../../../../../api/library/plugins/ig/api/class.viewgroup_cs.md).
## void SetSlaveViewByName ( string slave_name , int view_id )

Sets a view with the specified ID to be used for the specified Slave (available for Master IG only).
### Arguments

- *string* **slave_name** - Slave name (-computer_name "").
- *int* **view_id** - ID of the view to be set as current for the specified Slave.

## void SetSlaveView ( int index , int view_id )

Sets a view with the specified ID to be used for a certain Slave by its index (available for Master IG only).
### Arguments

- *int* **index** - Slave index in the range from 0 to the [total numer of Slaves](#getNumSlaves_int).
- *int* **view_id** - ID of the view to be set as current for the specified Slave.

## int GetSlaveViewByName ( string slave_name )

Returns the current view ID used for a certain Slave by its name.
### Arguments

- *string* **slave_name** - Slave name.

### Return value

ID of the view used for the Slave with the specified name.
## int GetSlaveView ( int slave_index )

Returns the current view ID used for a certain Slave by its index (available for Master IG only).
### Arguments

- *int* **slave_index** - Slave index in the range from 0 to the [total numer of Slaves](#getNumSlaves_int).

### Return value

ID of the view used for the Slave with the specified index.
## void ClearInterpolationData ( )

Clears all interpolation data for all entities.
## int GetNumSlaves ( )

Returns the total number of Slaves (available for Master IG only).
### Return value

Total number of IG Slaves.
## string GetSlaveName ( int index )

Returns Slave name by its index (available for Master IG only).
### Arguments

- *int* **index** - Slave index.

### Return value

Name of the Slave with the specified index.
## string GetSynckerName ( )

Returns the current name of the IG host.
### Return value

Current name of the IG host.
## IntPtr AddOnCreateViewCallback ( void * subscriber , CallbackBase * callback )

Adds a callback function to be executed on creating a new [view](../../../../../api/library/plugins/ig/api/class.view_cs.md). The signature of the callback function is as follows:


```text
void(View *)
```


### Arguments

- *void ** **subscriber** - Callback subscriber. Can be used to remove the added callback via the *[removeOnCreateViewCallback()](#removeOnCreateViewCallback_void_ptr_void)* method.
- *CallbackBase ** **callback** - Callback function to be executed.

### Return value

ID of the last added Create View callback, if the callback was added successfully; otherwise, **nullptr**. This ID can be used to [remove](#removeOnCreateViewCallback_void_ptr_void) this callback when necessary.
## void RemoveOnCreateViewCallback ( IntPtr subscriber )

Removes a callback function for the specified subscriber from the list of callbacks to be executed on creating a new [view](../../../../../api/library/plugins/ig/api/class.view_cs.md).
### Arguments

- *IntPtr* **subscriber** - Callback subscriber.

## void ClearOnCreateViewCallbacks ( )

Clears all [added](#addOnCreateViewCallback_void_ptr_CallbackBase_ptr_void) Create View callbacks.
## IntPtr AddOnCreateViewGroupCallback ( void * subscriber , CallbackBase * callback )

Adds a callback function to be executed on creating a new [view](../../../../../api/library/plugins/ig/api/class.view_cs.md). The signature of the callback function is as follows:


```text
void(ViewGroup *)
```


### Arguments

- *void ** **subscriber** - Callback subscriber. Can be used to remove the added callback via the *[removeOnCreateViewGroupCallback()](#removeOnCreateViewGroupCallback_void_ptr_void)* method.
- *CallbackBase ** **callback** - Callback function to be executed.

## void RemoveOnCreateViewGroupCallback ( IntPtr subscriber )

Removes a callback function for the specified subscriber from the list of callbacks to be executed on creating a new [view group](../../../../../api/library/plugins/ig/api/class.viewgroup_cs.md).
### Arguments

- *IntPtr* **subscriber** - Callback subscriber.

## void ClearOnCreateViewGroupCallbacks ( )

Clears all [added](#addOnCreateViewGroupCallback_void_ptr_CallbackBase_ptr_void) Create ViewGroup callbacks.
## void AddOnCreateEntityCallback ( IntPtr subscriber , CallbackBase * callback )

Adds a callback function to be executed on creating a new [entity](../../../../../api/library/plugins/ig/api/class.entity_cs.md). The signature of the callback function is as follows:


```text
void(IG::ICollisionVolume *volume, Unigine::ContactPtr contact, int contacted_entity, int contacted_volume)
```


### Arguments

- *IntPtr* **subscriber** - Callback subscriber. Can be used to remove the added callback via the *[removeOnCreateEntityCallback()](#removeOnCreateEntityCallback_void_ptr_void)* method.
- *CallbackBase ** **callback** - Callback function to be executed.

## void RemoveOnCreateEntityCallback ( IntPtr subscriber )

Removes a callback function for the specified subscriber from the list of callbacks to be executed on creating a new [entity](../../../../../api/library/plugins/ig/api/class.entity_cs.md).
### Arguments

- *IntPtr* **subscriber** - Callback subscriber.

## void ClearOnCreateEntityCallbacks ( )

Clears all [added](#addOnCreateEntityCallback_void_ptr_CallbackBase_ptr_void) Create Entity callbacks.
## void AddOnCollisionVolumeDetectedCallback ( IntPtr subscriber , CallbackBase * callback )

Adds a callback function to be executed on detecting an intersection with a [collision volume](../../../../../api/library/plugins/ig/api/class.collisionvolume_cs.md). The signature of the callback function is as follows:


```text
void(IG::ICollisionVolume *volume, Unigine::ContactPtr contact, int contacted_entity, int contacted_volume)
```


### Arguments

- *IntPtr* **subscriber** - Callback subscriber. Can be used to remove the added callback via the *[removeOnCollisionVolumeDetectedCallback()](#removeOnCollisionVolumeDetectedCallback_void_ptr_void)* method.
- *CallbackBase ** **callback** - Callback function to be executed.

## void RemoveOnCollisionVolumeDetectedCallback ( IntPtr subscriber )

Removes a callback function for the specified subscriber from the list of callbacks to be executed on detecting an intersection with a [collision volume](../../../../../api/library/plugins/ig/api/class.collisionvolume_cs.md).
### Arguments

- *IntPtr* **subscriber** - Callback subscriber.

## void ClearOnCollisionVolumeDetectedCallbacks ( )

Clears all [added](#addOnCollisionVolumeDetectedCallback_void_ptr_CallbackBase_ptr_void) CollisionVolume Detected callbacks.
## void AddOnCollisionSegmentDetectedCallback ( IntPtr subscriber , CallbackBase * callback )

Adds a callback function to be executed on detecting an intersection with a [collision segment](../../../../../api/library/plugins/ig/api/class.collisionsegment_cs.md). The signature of the callback function is as follows:


```text
void(IG::ICollisionSegment *segment, Unigine::ObjectPtr object, Unigine::WorldIntersectionPtr intersection)
```


### Arguments

- *IntPtr* **subscriber** - Callback subscriber. Can be used to remove the added callback via the *[removeOnCollisionSegmentDetectedCallback()](#removeOnCollisionSegmentDetectedCallback_void_ptr_void)* method.
- *CallbackBase ** **callback** - Callback function to be executed.

## void RemoveOnCollisionSegmentDetectedCallback ( IntPtr subscriber )

Removes a callback function for the specified subscriber from the list of callbacks to be executed on detecting an intersection with a [collision segment](../../../../../api/library/plugins/ig/api/class.collisionsegment_cs.md).
### Arguments

- *IntPtr* **subscriber** - Callback subscriber.

## void ClearOnCollisionSegmentDetectedCallbacks ( )

Clears all [added](#addOnCollisionSegmentDetectedCallback_void_ptr_CallbackBase_ptr_void) CollisionSegment Detected callbacks.
## void AddOnIGReadyCallback ( IntPtr subscriber , CallbackBase * callback )

Adds a callback function to be executed when all Slaves that were waited for by the IG are connected. The signature of the callback function is as follows:


```text
void()
```


### Arguments

- *IntPtr* **subscriber** - Callback subscriber. Can be used to remove the added callback via the *[removeOnIGReadyCallback()](#removeOnIGReadyCallback_void_ptr_void)* method.
- *CallbackBase ** **callback** - Callback function to be executed.

## void RemoveOnIGReadyCallback ( IntPtr subscriber )

Removes a callback function for the specified subscriber from the list of callbacks to be executed when all Slaves that were waited for by the IG are connected.
### Arguments

- *IntPtr* **subscriber** - Callback subscriber.

## void ClearOnIGReadyCallbacks ( )

Clears all [added](#addOnIGReadyCallback_void_ptr_CallbackBase_ptr_void) IG Ready callbacks.
## void AddOnSlaveConnectedCallback ( IntPtr subscriber , CallbackBase * callback )

Adds a callback function to be executed on connecting a new Slave. The signature of the callback function is as follows:


```text
void(int slave_index, const char * slave_name)
```


### Arguments

- *IntPtr* **subscriber** - Callback subscriber. Can be used to remove the added callback via the *[removeOnSlaveConnectedCallback()](#removeOnSlaveConnectedCallback_void_ptr_void)* method.
- *CallbackBase ** **callback** - Callback function to be executed.

## void RemoveOnSlaveConnectedCallback ( IntPtr subscriber )

Removes a callback function for the specified subscriber from the list of callbacks to be executed on connecting a new Slave.
### Arguments

- *IntPtr* **subscriber** - Callback subscriber.

## void ClearOnSlaveConnectedCallbacks ( )

Clears all [added](#addOnSlaveConnectedCallback_void_ptr_CallbackBase_ptr_void) Slave Connected callbacks.
## void AddOnSlaveDisconnectedCallback ( IntPtr subscriber , CallbackBase * callback )

Adds a callback function to be executed on disconnecting a Slave. The signature of the callback function is as follows:


```text
void(int slave_index)
```


### Arguments

- *IntPtr* **subscriber** - Callback subscriber. Can be used to remove the added callback via the *[removeOnSlaveDisconnectedCallback()](#removeOnSlaveDisconnectedCallback_void_ptr_void)* method.
- *CallbackBase ** **callback** - Callback function to be executed.

## void RemoveOnSlaveDisconnectedCallback ( IntPtr subscriber )

Removes a callback function for the specified subscriber from the list of callbacks to be executed on disconnecting a Slave.
### Arguments

- *IntPtr* **subscriber** - Callback subscriber.

## void ClearOnSlaveDisconnectedCallbacks ( )

Clears all [added](#addOnSlaveDisconnectedCallback_void_ptr_CallbackBase_ptr_void) Slave Disconnected callbacks.
## void SetPropertyWarningEnabled ( bool v )

Sets the value indicating if the property-related warnings should be displayed in the console. This is a convenience method that might be useful when working with C# components.
### Arguments

- *bool* **v** - true to display property-related warnings; false to disable them.
