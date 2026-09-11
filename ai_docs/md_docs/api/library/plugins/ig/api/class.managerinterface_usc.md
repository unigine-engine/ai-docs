# Unigine::Plugins::IG::Manager Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


This class represents the IG Manager interface.


> **Notice:** IG plugin must be loaded.


## Manager Class

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
## getGeodeticOrigin () const

Returns the current geodetic origin coordinates.
### Return value

Current geodetic origin coordinates.
## getGeodeticPivot () const

Returns the current geodetic pivot used to curve the terrain.
### Return value

Current geodetic pivot used to curve the terrain.
## getTerrain () const

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
## getConverter () const

Returns the current *[converter](../../../../../api/library/geodetics/geodetics_plugin/class.transformer_usc.md)* interface.
### Return value

Current converter interface.
## getNEDConverter () const

Returns the current *[NEDConverter](../../../../../api/library/plugins/ig/api/class.nedconverter_usc.md)* interface.
### Return value

Current NEDConverter interface.
## getLightController () const

Returns the current light controller interface.
### Return value

Current light controller interface.
## getMeteo () const

Returns the current Meteo interface.
### Return value

Current Meteo interface.
## getSkyMap () const

Returns the current SkyMap interface.
### Return value

Current SkyMap interface.
## getConfig () const

Returns the current IG configuration as an [IGConfig](../../../../../api/library/plugins/ig/api/class.igconfig_usc.md) class instance.
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

Returns the current inverse FPS value (the time in seconds it took to complete the last frame). This method is similar to the [*Game::getIFps()*](../../../../../api/library/engine/class.game_usc.md#getIFps_float) but it is more preferred for multi-channel systems as it implements more accurate frame time calculation (including spike-periods).
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
## int getDatabaseID ( )

Returns the identifier of the world database with the specified name stored in the IG configuration file (`ig_config.xml`).
### Arguments

### Return value

Identifier of the specified world database, or 0, if no world is loaded.
## getDatabaseName ( int id )

Returns the name of the world database stored in the IG configuration file (`ig_config.xml`).
### Arguments

- *int* **id** - Identifier of the world database.

### Return value

The world database name.
## SymbolsController * getSymbolsController ( )

Returns the interface of the symbols controller.
### Return value

Symbols controller interface.
## getView ( int view_id , bool auto_create )

Returns the [interface](../../../../../api/library/plugins/ig/api/class.view_usc.md) of the specified view.
### Arguments

- *int* **view_id** - ID of the view.
- *bool* **auto_create** - **1** to automatically create the view with the specified ID if it doesn't exist yet; **0** - to return nullptr in case the view doesn't exist.

### Return value

## bool removeView ( int view_id )

Removes the view with the specified ID.
### Arguments

- *int* **view_id** - ID of the view to be removed.

### Return value

**1** if the view with the specified ID is removed successfully; otherwise - **0**.
## bool isViewExist ( int view_id )

Returns a value indicating if the view with the specified ID exists.
### Arguments

- *int* **view_id** - ID of the view.

### Return value

**1** if the view with the specified ID exists; otherwise - **0**.
## getViewGroup ( int group_id , bool auto_create )

Returns the [interface](../../../../../api/library/plugins/ig/api/class.viewgroup_usc.md) of the specified view group.
### Arguments

- *int* **group_id** - ID of the view group.
- *bool* **auto_create** - **1** to automatically create the view group with the specified ID if it doesn't exist yet; **0** - to return nullptr in case the view group doesn't exist.

### Return value

## bool removeViewGroup ( int group_view_id )

Removes the view group with the specified ID.
### Arguments

- *int* **group_view_id** - ID of the view group to be removed.

### Return value

**1** if the view group with the specified ID is removed successfully; otherwise - **0**.
## bool isViewGroupExist ( int group_view_id )

Returns a value indicating if the view group with the specified ID exists.
### Arguments

- *int* **group_view_id** - ID of the view group.

### Return value

**1** if the view group with the specified ID exists; otherwise - **0**.
## getEntity ( bool auto_create = true )

Returns the [interface](../../../../../api/library/plugins/ig/api/class.entity_usc.md) of the specified entity.
### Arguments

- *bool* **auto_create** - **1** to automatically create the entity with the specified ID if it doesn't exist yet; **0** - to return nullptr in case the entity doesn't exist.

### Return value

## bool removeEntity ( )

Removes the entity with the specified ID.
### Arguments

### Return value

**1** if the entity with the specified ID is removed successfully; otherwise - **0**.
## bool isEntityExist ( long entity_id )

Returns a value indicating if the entity with the specified ID exists.
### Arguments

- *long* **entity_id** - ID of the entity. > **Notice:** The value should be the [entity ID](../../../../../api/library/plugins/ig/api/class.entity_usc.md#getID_llong), **not** the [type ID](../../../../../api/library/plugins/ig/api/class.entity_usc.md#getType_llong).

### Return value

**1** if the entity with the specified ID exists; otherwise - **0**.
## void getEntities ( Unigine::Vector<Entity *> & entities_ret )

Fills the list of entities with all existing entities.
### Arguments

- *Unigine::Vector<Entity *> &* **entities_ret** - List of entities.

## findEntity ( )

Returns the [interface](../../../../../api/library/plugins/ig/api/class.entity_usc.md) of the entity represented by the specified node.
### Arguments

### Return value

## findEntityType ( )


Returns the ID of the entity type by its name. Entity type ID and name define the type of the entity to be used for a specific instance and are set in the [entity definition section](../../../../../ig/config.md#config_entities) of the IG configuration file as follows:


```xml
<entity_types>
	<entity id="111" name="b52">
	</entity>
</entity_types>

```


### Arguments

### Return value

Entity type ID.
## int findComponentID ( )

Returns the ID of the component with the given name, which belongs to the specified entity type.
### Arguments

### Return value

Component ID.
## int findArticulatedPartID ( )

Returns the identifier of an articulated part by its name and the type of the entity it belongs to, stored in the IG configuration file (`ig_config.xml`).
### Arguments

### Return value

Identifier of an articulated part.
## bool getHatHot ( )

Checks if there is anything in the given geodetic position and returns HAT/HOT as well as surface normal, exact object over which the request was made, intersected surface, world coordinates of the intersection point, etc. to the specified output variables.
### Arguments

### Return value

true, if there is anything in the given geodetic position, otherwise false.
## bool getIntersection ( int mask )

Checks if the ray with set points intersects with anything.
### Arguments

- *int* **mask** - Intersection mask.

### Return value

**1**, if the ray intersects with anything, otherwise **0**.
## getWater ( )

Returns the interface of the water control.
### Return value

Water control interface.
## loadNode ( )


Loads a node from the specified file to the world on the Master and all Slaves. This is a network analogue of the [loadNode()](../../../../../api/library/engine/class.world_usc.md#loadNode_cstr_int_Node) method of the *World* class.


> **Notice:** This is a safe analogue of the [Syncker](../../../../../api/library/plugins/syncker/index.md) method *[loadNode()](../../../../../api/library/plugins/syncker/class.syncker_master_usc.md#loadNode_cstr_uchar_Mat4_Node)* that has an internal check if this method runs on the master and if Syncker is running.


### Arguments

### Return value

## void syncNode ( )


Enables synchronization of parameters of the given node via the UDP protocol. Scene nodes are not synchronized by default, this method is used to add a particular node to the synchronization queue.


> **Notice:** This is a safe analogue of the [Syncker](../../../../../api/library/plugins/syncker/index.md) method *[addSyncNode()](../../../../../api/library/plugins/syncker/class.syncker_master_usc.md#addSyncNode_Node_uchar_void)* that has an internal check if this method runs on the master and if Syncker is running. If this method is called on a slave, it does nothing.


### Arguments

## void synckerCreate ( unsigned char mask = 255 )


Synchronizes creation of the given node on all Slaves. This method is **to be called after node creation on the Master**. It is recommended to use the [*loadNode()*](#loadNode_cstr_Node) method whenever possible as this approach **allows adding nodes of all types**, unlike the [*synckerCreate()*](#synckerCreate_Node_uchar_void) method that supports only a limited number of them.


> **Notice:** This is a safe analogue of the [Syncker](../../../../../api/library/plugins/syncker/index.md) method [createNode()](../../../../../api/library/plugins/syncker/class.syncker_master_usc.md#createNode_Node_uchar_bool) that has an internal check if this method runs on the master and if Syncker is running. If this method is called on a slave, it does nothing.


### Arguments

- *unsigned char* **mask** - Synchronization mask.

## void synckerDestroy ( )


Synchronizes deletion of the given node (with all its children) on the Master and all Slaves.


> **Notice:** This is a safe analogue of the [Syncker](../../../../../api/library/plugins/syncker/index.md) method [deleteNode()](../../../../../api/library/plugins/syncker/class.syncker_master_usc.md#deleteNode_Node_void) that has an internal check if this method runs on the master and if Syncker is running. If this method is called on a slave, it does nothing.


### Arguments

## bool isSyncNode ( )


Returns a value indicating if synchronization of the given node is enabled. Using this method you can quickly check if a node is monitored by the Syncker (node's states are dispatched to Slaves over the network).


> **Notice:** This is a safe analogue of the [Syncker](../../../../../api/library/plugins/syncker/index.md) method [isSyncNode()](../../../../../api/library/plugins/syncker/class.syncker_master_usc.md#isSyncNode_Node_bool) that has an internal check if this method runs on the master and if Syncker is running. If this method is called on a slave, it does nothing.


### Arguments

### Return value

true if synchronization of the given node is enabled; otherwise, false.
## bool checkEntityType ( )

Checks if the given entity type is supported by IG.
### Arguments

### Return value

**1**, if the given entity type is supported, otherwise **0**.
## void sendUserMessage ( )

Sends user message from the master to a slave.
### Arguments

## addOnUserMessageReceivedCallback ( )

Executes the callback function when the [user message](#sendUserMessage_uchar_Blob_void) from the master is received.
### Arguments

### Return value

Callback subscriber ID. This ID can be used to [remove](#removeOnUserMessageReceivedCallback_void_ptr_bool) this callback when necessary.
## void setDistanceScale ( float d )


Sets the global distance scale for all rendering distance parameters: shadow distance, light distance, LOD distances, etc. (see [render_distance_scale](../../../../../code/console/index.md#render_distance_scale) console command) and for the IG Simplifier component. The Simplifier component can help optimize rendering of your entities. When assigned to an entity, it enables you to define which parts of its model can be neglected starting at certain distance levels (e.g., hide flaps, ailerons, and rudders at 1km, engines at 5 km, etc.) and which substitutes can be used to represent an entity at a large distance (e.g., a flashing strobe light, when the plane is just a point on the screen).


> **Notice:** This method calls the [*setDistanceScale()*](../../../../../api/library/rendering/class.render_usc.md#setDistanceScale_float_void) of the *Render* class.


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

Destroys all [entities](../../../../../api/library/plugins/ig/api/class.entity_usc.md), [views](../../../../../api/library/plugins/ig/api/class.view_usc.md), and [view groups](../../../../../api/library/plugins/ig/api/class.viewgroup_usc.md).
## void setSlaveViewByName ( int view_id )

Sets a view with the specified ID to be used for the specified Slave (available for Master IG only).
### Arguments

- *int* **view_id** - ID of the view to be set as current for the specified Slave.

## void setSlaveView ( int index , int view_id )

Sets a view with the specified ID to be used for a certain Slave by its index (available for Master IG only).
### Arguments

- *int* **index** - Slave index in the range from 0 to the [total numer of Slaves](#getNumSlaves_int).
- *int* **view_id** - ID of the view to be set as current for the specified Slave.

## int getSlaveViewByName ( )

Returns the current view ID used for a certain Slave by its name.
### Arguments

### Return value

ID of the view used for the Slave with the specified name.
## int getSlaveView ( int slave_index )

Returns the current view ID used for a certain Slave by its index (available for Master IG only).
### Arguments

- *int* **slave_index** - Slave index in the range from 0 to the [total numer of Slaves](#getNumSlaves_int).

### Return value

ID of the view used for the Slave with the specified index.
## void clearInterpolationData ( )

Clears all interpolation data for all entities.
## int getNumSlaves ( )

Returns the total number of Slaves (available for Master IG only).
### Return value

Total number of IG Slaves.
## getSlaveName ( int index )

Returns Slave name by its index (available for Master IG only).
### Arguments

- *int* **index** - Slave index.

### Return value

Name of the Slave with the specified index.
## getSynckerName ( )

Returns the current name of the IG host.
### Return value

Current name of the IG host.
## void setPropertyWarningEnabled ( int v )

Sets the value indicating if the property-related warnings should be displayed in the console. This is a convenience method that might be useful when working with C# components.
### Arguments

- *int* **v** - **1** to display property-related warnings; **0** to disable them.
