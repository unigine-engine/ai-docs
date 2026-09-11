# Unigine::Plugins::Syncker::Master Class (CPP)

**Header:** #include <plugins/Unigine/Syncker/UnigineSyncker.h>

**Inherits from:** Syncker


This class represents the master interface of the Syncker.


> **Notice:** [Syncker](../../../../code/plugins/syncker/index.md) plugin must be loaded.


## Master Class

### Enums

## CALLBACK_INDEX

Callback types.
| Name | Description |
|---|---|
| **SESSION_STARTED** = 0 | Callback function to be fired on starting a session (all Slaves are connected, MTU is determined). Callback signature: ```text callback_function_name(void) ``` |
| **SESSION_CONTINUED** = | Callback function to be fired on continuing a session. Callback signature: ```text callback_function_name(Vector <long long> slaves_id) ``` |
| **SESSION_FINISHED** = 2 | Callback function to be fired on closing a session. Callback signature: ```text callback_function_name(void) ``` |
| **SLAVE_CONNECTED** = 3 | Callback function to be fired on successful connection of a new Slave. Callback signature: ```text callback_function_name(int slave_num) ``` |
| **SLAVE_DISCONNECTED** = 4 | Callback function to be fired before disconnecting a Slave. The reason for disconnection specified in string format ("disconnected by slave", "timeout", etc.) Callback signature: ```text callback_function_name(int slave_num, const char *reason) ``` |
| **MASTER_SETUP_CHANGED** = 5 | Callback to be fired on changing settings on the Master. Callback signature: ```text void callback_function_name(void); ``` |
| **SLAVE_SETUP_CHANGED** = 6 | Callback to be fired on changing settings on a Slave. Callback signature: ```text void callback_function_name(int slave_num); ``` |

## SYNC_MASK

Node synchronization mask.
| Name | Description |
|---|---|
| **NODE_FLAGS** = 1 | Update only simple node flag (*enabled*, *immovable*, etc.) |
| **TRANSFORM** = 1 << 1 | Update node transform (with interpolation). |
| **BASE** = 3 | Update base information *NODEFLAGS & TRANSFORM*. |
| **DERIVED** = 31 << 3 | Update information of derived class (11111000 - without the first 3 bits). This mask allows synchronizing the node subtype (such as player, light, decal, etc.) parameters. |
| **OBJECT** = 1 << 3 | Update object parameters. All other parameters of objects except for *NODE_FLAGS* and *TRANSFORM* (particles trasform for object particles, bones transform for object skinned) |
| **OBJECT_SURFACE** = 1 << 4 | Update all parameters of surfaces (surface flags and information about inherited materials for each surface). |

## DEFAULT_SYNC_NODES

Types of nodes that will be synchronized automatically after world loading.
| Name | Description |
|---|---|
| **LIGHT_WORLD** = 1 | World light. See the [LightWorld](../../../../api/library/lights/class.lightworld_cpp.md) class. |
| **WATER_GLOBAL** = 1 << 1 | Global water. See the [ObjectWaterGlobal](../../../../api/library/objects/class.objectwaterglobal_cpp.md) class. |
| **CLOUD_LAYER** = 1 << 2 | Cloud layer. See the [ObjectCloudLayer](../../../../api/library/objects/class.objectcloudlayer_cpp.md) class. |
| **OBJECT_PARTICLES** = 1 << 3 | Particle system. See the [ObjectParticles](../../../../api/library/objects/class.objectparticles_cpp.md) class. |

### Members

## int getNumSyncMaterials () const

Returns the current total number of materials in the synchronization queue.
### Return value

Current total number of materials in the synchronization queue.
## int getNumSyncNodes () const

Returns the current total number of nodes in the synchronization queue.
### Return value

Current total number of nodes in the synchronization queue.
## void setDefaultSyncNodes ( unsigned char nodes )

Sets a new mask defining types of nodes that will be synchronized automatically after world loading. This mask can be used for optimization reasons limiting the number of nodes to be synchronized and thus reducing network load. For example, you can restrict automatic synchronization to global water, and clouds only:
```cpp
master->setDefaultSyncNodes(Syncker::Master::WATER_GLOBAL | Syncker::Master::CLOUD_LAYER);
```


### Arguments

- *unsigned char* **nodes** - The mask defining types of nodes that will be synchronized automatically after world loading.

## unsigned char getDefaultSyncNodes () const

Returns the current mask defining types of nodes that will be synchronized automatically after world loading. This mask can be used for optimization reasons limiting the number of nodes to be synchronized and thus reducing network load. For example, you can restrict automatic synchronization to global water, and clouds only:
```cpp
master->setDefaultSyncNodes(Syncker::Master::WATER_GLOBAL | Syncker::Master::CLOUD_LAYER);
```


### Return value

Current mask defining types of nodes that will be synchronized automatically after world loading.
## void setSyncWorldLoad ( bool load )

Sets a new value indicating whether synchronization of world loading via the UDP protocol is enabled.
### Arguments

- *bool* **load** - Set **true** to enable synchronization of world loading via the UDP protocol; **false** - to disable it.

## bool isSyncWorldLoad () const

Returns the current value indicating whether synchronization of world loading via the UDP protocol is enabled.
### Return value

**true** if synchronization of world loading via the UDP protocol is enabled ; otherwise **false**.
## void setSyncRender ( bool render )

Sets a new A value indicating if synchronization of all render parameters via the UDP protocol (light scattering, occlusion, etc.) is enabled.
> **Notice:** When all slaves use the same rendering settings, synchronization of render parameters can be disabled.


### Arguments

- *bool* **render** - Set **true** to enable synchronization of all render parameters via the UDP protocol; **false** - to disable it.

## bool isSyncRender () const

Returns the current A value indicating if synchronization of all render parameters via the UDP protocol (light scattering, occlusion, etc.) is enabled.
> **Notice:** When all slaves use the same rendering settings, synchronization of render parameters can be disabled.


### Return value

**true** if synchronization of all render parameters via the UDP protocol is enabled ; otherwise **false**.
## void setSyncViewOffset ( bool offset )

Sets a new value indicating whether synchronization of view offset for projections is enabled.
### Arguments

- *bool* **offset** - Set **true** to enable synchronization of view offset for projections via the UDP protocol; **false** - to disable it.

## bool isSyncViewOffset () const

Returns the current value indicating whether synchronization of view offset for projections is enabled.
### Return value

**true** if synchronization of view offset for projections via the UDP protocol is enabled ; otherwise **false**.
## void setSyncPlayer ( bool player )

Sets a new value indicating whether synchronization of the current player's parameters via the UDP protocol is enabled.
The following parameters are synchronized:


- Its transformation
- Projection matrix
- Viewport mask
- Mask for reflections
- Applied post-materials (if any)


> **Notice:** Current player synchronization is used only when all slaves use the same camera.


### Arguments

- *bool* **player** - Set **true** to enable synchronization of the current player's parameters (transformation, projection matrix, viewport and reflection masks, applied post-materials) via the UDP protocol; **false** - to disable it.

## bool isSyncPlayer () const

Returns the current value indicating whether synchronization of the current player's parameters via the UDP protocol is enabled.
The following parameters are synchronized:


- Its transformation
- Projection matrix
- Viewport mask
- Mask for reflections
- Applied post-materials (if any)


> **Notice:** Current player synchronization is used only when all slaves use the same camera.


### Return value

**true** if synchronization of the current player's parameters (transformation, projection matrix, viewport and reflection masks, applied post-materials) via the UDP protocol is enabled ; otherwise **false**.
## float getNumSlaves () const

Returns the current total number of the slaves connected to the master.
### Return value

Current total number of the slaves connected to the master.
## void setAllowExtraSlaves ( bool slaves )

Sets a new value indicating whether new Slaves can connect to the Master after starting the session. This can be used, for example, to connect a Slave which is used as a tool for configuring projections and does not operate as an IG.
### Arguments

- *bool* **slaves** - true permits new Slaves to connect to the Master after starting the session; false - forbids it.

## bool isAllowExtraSlaves () const

Returns the current value indicating whether new Slaves can connect to the Master after starting the session. This can be used, for example, to connect a Slave which is used as a tool for configuring projections and does not operate as an IG.
### Return value

true permits new Slaves to connect to the Master after starting the session; false - forbids it.
## void setSendRate ( float rate )

Sets a new
frequency of sending packets to Slaves. Use this method when network load is too high and slows down the whole IG system. It is recommended to use this method with [interpolation](../../../../api/library/plugins/syncker/class.syncker_syncker_cpp.md#setInterpolation_int_void) enabled.


```cpp
//On the Master
master->setSendRate(15.0f); // send packets 15 times per second

//Both on the Master and all Slaves
syncker->setInterpolationPeriod(0.1f); // 100 ms delay

```


### Arguments

- *float* **rate** - The frequency of sending packets to Slaves. The default value is -1 (every frame). > **Notice:** The value should not be less than ***1�/�[getInterpolationPeriod()](../../../../api/library/plugins/syncker/class.syncker_syncker_cpp.md#getInterpolationPeriod_double)***, otherwise the image shall be "stuttering".

## float getSendRate () const

Returns the current
frequency of sending packets to Slaves. Use this method when network load is too high and slows down the whole IG system. It is recommended to use this method with [interpolation](../../../../api/library/plugins/syncker/class.syncker_syncker_cpp.md#setInterpolation_int_void) enabled.


```cpp
//On the Master
master->setSendRate(15.0f); // send packets 15 times per second

//Both on the Master and all Slaves
syncker->setInterpolationPeriod(0.1f); // 100 ms delay

```


### Return value

Current frequency of sending packets to Slaves.
The default value is -1 (every frame).


> **Notice:** The value should not be less than ***1�/�[getInterpolationPeriod()](../../../../api/library/plugins/syncker/class.syncker_syncker_cpp.md#getInterpolationPeriod_double)***, otherwise the image shall be "stuttering".

---

## const char * getSlaveAddress ( int num ) const

Returns the network address of the given slave computer.
### Arguments

- *int* **num** - Slave number.

### Return value

Network address of the slave computer.
## int getSlavePort ( int num ) const

Returns the UDP port used by the slave with the specified number.
### Arguments

- *int* **num** - Slave number.

### Return value

UDP port of the specified slave computer. 0 - means any unused port available.
## long long getSlaveID ( int num ) const

Returns the ID of the slave with the specified number. A unique Slave ID consists of two parts: IP (32 bits) + port (16 bits)
### Arguments

- *int* **num** - Slave number.

### Return value

ID of the slave with the specified number.
## const char * getSlaveWorldName ( int num ) const

Returns the name of the world file currently loaded on the specified slave.
### Arguments

- *int* **num** - Slave number.

### Return value

Name of the world file currently loaded on the specified slave.
## void addSyncNode ( const Ptr < Node > & node , unsigned char sync_mask = SYNC_MASK::NODE_FLAGS | SYNC_MASK::TRANSFORM )


Enables synchronization of parameters of the given node via the UDP protocol.


> **Notice:** Scene nodes are not synchronized by default, this method is used to add a particular node to the synchronization queue.


### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Node](../../../../api/library/nodes/class.node_cpp.md)> &* **node** - Node to synchronize.
- *unsigned char* **sync_mask** - Synchronization mask, one of the [SYNC_MASK](#SYNC_MASK) values. By default, only node transformation is synchronized. To sync other parameters, select the corresponding mask.

## void addSyncNodes ( const Vector < Ptr < Node >> & nodes , unsigned char sync_mask = SYNC_MASK::NODE_FLAGS | SYNC_MASK::TRANSFORM )


Enables synchronization of parameters of given nodes via the UDP protocol.


> **Notice:** Scene nodes are not synchronized by default, this method is used to add particular nodes to the synchronization queue.


### Arguments

- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Node](../../../../api/library/nodes/class.node_cpp.md)>> &* **nodes** - List of nodes to synchronize.
- *unsigned char* **sync_mask** - Synchronization mask, one of the [SYNC_MASK](#SYNC_MASK) values. By default, only node transformation is synchronized. To sync other parameters, select the corresponding mask.

## void setSyncNodeMask ( const Ptr < Node > & node , unsigned char sync_mask )

Sets a new synchronization mask for the specified node. Synchronization mask can be used for optimization reasons limiting the amount of data to be synchronized and thus reducing network load. For example, for moving parts of a helicopter we can set a mask to synchronize only node transformations:
```cpp
master->setSyncNodeMask(fan_small, Syncker::Master::TRANSFORM);
master->setSyncNodeMask(fan_big, Syncker::Master::TRANSFORM);

```


### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Node](../../../../api/library/nodes/class.node_cpp.md)> &* **node** - Node for which a new synchronization mask is to be set.
- *unsigned char* **sync_mask** - New synchronization mask to be set for the specified node, one of the [SYNC_MASK](#SYNC_MASK) values.

## unsigned char getSyncNodeMask ( const Ptr < Node > & node ) const

Returns the synchronization mask for the specified node.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Node](../../../../api/library/nodes/class.node_cpp.md)> &* **node** - Node, for which a synchronization mask is to be obtained.

### Return value

Synchronization mask of the specified node, one of the [SYNC_MASK](#SYNC_MASK) values.
## bool isSyncNode ( const Ptr < Node > & node ) const

Returns a value indicating if synchronization of the given node is enabled. Using this method you can quickly check if a node is monitored by the Syncker (node's states are dispatched to Slaves over the network).
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Node](../../../../api/library/nodes/class.node_cpp.md)> &* **node** - Node to be checked.

### Return value

true if synchronization of the given node is enabled; otherwise, false.
## Ptr < Node > getSyncNode ( int num ) const

Returns the synchronized node with the given number.
### Arguments

- *int* **num** - Node number in the synchronization queue.

### Return value

Synchronized node.
## void removeSyncNode ( int num )

Removes the specified node from the synchronization queue.
### Arguments

- *int* **num** - Node number in the synchronization queue.

## void removeSyncNode ( const Ptr < Node > & node )

Removes the specified node from the synchronization queue.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Node](../../../../api/library/nodes/class.node_cpp.md)> &* **node** - Node to be removed from synchronization.

## void removeSyncNodeID ( int node_id )

Removes the specified node from the synchronization queue by its ID.
### Arguments

- *int* **node_id** - ID of the node to be removed from the synchronization queue.

## void removeSyncNodes ( const Vector < Ptr < Node >> & nodes )

Removes the specified nodes from the synchronization queue.
### Arguments

- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Node](../../../../api/library/nodes/class.node_cpp.md)>> &* **nodes** - List of nodes to be removed from the synchronization queue.

## void clearSyncNodes ( )

Removes all nodes from the synchronization queue.
## void addSyncMaterial ( const Ptr < Material > & material )


Enables synchronization of the given material via the UDP protocol.


> **Notice:** Scene materials are not synchronized by default, this method is used to add a particular material to the synchronization queue.


### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Material](../../../../api/library/rendering/class.material_cpp.md)> &* **material** - Material to synchronize.

## void addSyncMaterials ( const Vector < Ptr < Material >> & materials )


Enables synchronization of given materials via the UDP protocol.


> **Notice:** Scene materials are not synchronized by default, this method is used to add particular materials to the synchronization queue.


### Arguments

- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Material](../../../../api/library/rendering/class.material_cpp.md)>> &* **materials** - List of materials to synchronize.

## bool isSyncMaterial ( const Ptr < Material > & mat ) const

Returns a value indicating if synchronization of the given material is enabled. Using this method you can quickly check if a material is monitored by the Syncker (material's states are dispatched to Slaves over the network).
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Material](../../../../api/library/rendering/class.material_cpp.md)> &* **mat** - Material to be checked.

### Return value

true if synchronization of the given material is enabled; otherwise, false.
## Ptr < Material > getSyncMaterial ( int num ) const

Returns the synchronized material with the given number.
### Arguments

- *int* **num** - Material number in the synchronization queue.

### Return value

Synchronized material.
## void removeSyncMaterial ( int num )

Removes the material with the given number from the synchronization queue.
### Arguments

- *int* **num** - Material number in the synchronization queue.

## void removeSyncMaterial ( const Ptr < Material > & material )

Removes the specified material from the synchronization queue.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Material](../../../../api/library/rendering/class.material_cpp.md)> &* **material** - Material to be removed from the synchronization queue.

## void removeSyncMaterials ( const Vector < Ptr < Material >> & materials )

Removes the specified materials from the synchronization queue.
### Arguments

- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Material](../../../../api/library/rendering/class.material_cpp.md)>> &* **materials** - List of materials to be removed from the synchronization queue.

## void clearSyncMaterials ( )

Removes all materials from the synchronization queue.
## bool createNode ( const Ptr < Node > & node , unsigned char sync_mask = 0 )


Synchronizes creation of the given node on all Slaves. This method is **to be called after node creation on the Master**.


> **Notice:** It is recommended to use the [*loadNode()*](#loadNode_cstr_uchar_Mat4_Node) or [*loadNodereference()*](#loadNodeReference_cstr_uchar_Mat4_NodeReference) methods whenever possible as this approach **allows adding nodes of all types**, unlike the [*createNode()*](#createNode_Node_uchar_bool) method that supports only a limited number of them.

 **Example:**
```cpp
NodePtr node = NodeDummy::create();
master->createNode(node);

```


### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Node](../../../../api/library/nodes/class.node_cpp.md)> &* **node** - Node to create.
- *unsigned char* **sync_mask** - Synchronization mask, one of the [SYNC_MASK](#SYNC_MASK) values.

### Return value

true if the node was created successfully; otherwise, false.
## void deleteNode ( const Ptr < Node > & node )

Synchronizes deletion of the given node (with all its children) on the Master and all Slaves. Similar to calling *deleteLater()* for the node.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Node](../../../../api/library/nodes/class.node_cpp.md)> &* **node** - Node to delete.

## bool isNodeCreatedBySyncker ( const Ptr < Node > & node ) const

Returns a value indicating if the given node was created via the [*createNode()*](#createNode_Node_uchar_bool) method. Using this method you can quickly check if a node is in the run-time objects creation buffer.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Node](../../../../api/library/nodes/class.node_cpp.md)> &* **node** - Node to be checked.

### Return value

true if the given node was created via the [*createNode()*](#createNode_Node_uchar_bool) method; otherwise, false.
## void setCustomPlayer ( const char * name , const Ptr < Player > & player )


Sets the specified player for the view, view group, or computer with the specified name.


> **Notice:** Synchronization of the [main master camera](../../../../code/plugins/syncker/index.md#main_camera) is disabled.


### Arguments

- *const char ** **name** - Name of a view, a view group, or a computer to set the custom player for. > **Notice:** The specified name will be checked in the following order: *view, view group, computer*. The specified player will be set for the first element found.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Player](../../../../api/library/players/class.player_cpp.md)> &* **player** - Player to be set.

## void setViewOffset ( const Math:: vec3 & offset )

Sets a new player's head position on the Master.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **offset** - New player's head position coordinates to be set.

## void loadWorld ( const char * name )

Loads a world from the specified file on the Master and all Slaves. Syncker is able to automatically synchronize the current world, but it works as follows: Slaves shall only start loading a new world after it is completely loaded on the Master. This method provides a 2x speedup of world loading process, as it forces all hosts to start loading the world almost simultaneously.
### Arguments

- *const char ** **name** - Path to the `*.world` file to be loaded.

## Ptr < Node > loadNode ( const char * path , unsigned char sync_mask = 0 , Math:: Mat4 & init_transform )

Loads a node from the specified file to the world on the Master and all Slaves and places it to the specified ititial transformation. This is a network analogue of the *[loadNode()](../../../../api/library/engine/class.world_cpp.md#loadNode_cstr_int_Node)* method of the *World* class. By default, the loaded node is not synchronized, which is suitable for static objects at run time and at the same time saves performance. For dynamic objects to be synchronized, the suitable synchronization mask should be set.
### Arguments

- *const char ** **path** - Path to the `*.node` file.
- *unsigned char* **sync_mask** - Synchronization mask, one of the [SYNC_MASK](#SYNC_MASK) values.
- *Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md) &* **init_transform** - Initial transformation of the node.

### Return value

Loaded node or nullptr if an error has occurred.
## Ptr < Node > loadNode ( const char * path , unsigned char sync_mask = 0 )

Loads a node from the specified file to the world on the Master and all Slaves and places it at the origin with the default transformation. This is a network analogue of the *[loadNode()](../../../../api/library/engine/class.world_cpp.md#loadNode_cstr_int_Node)* method of the *World* class. By default, the loaded node is not synchronized, which is suitable for static objects at run time and at the same time saves performance. For dynamic objects to be synchronized, the suitable synchronization mask should be set.
### Arguments

- *const char ** **path** - Path to the `*.node` file.
- *unsigned char* **sync_mask** - Synchronization mask, one of the [SYNC_MASK](#SYNC_MASK) values.

### Return value

Loaded node or nullptr if an error has occurred.
## Ptr < NodeReference > loadNodeReference ( const char * path , unsigned char sync_mask = 0 , Math:: Mat4 & init_transform )

Loads a node reference from the specified file to the world on the Master and all Slaves and places it to the specified ititial transformation. This is a network analogue of the [NodeReference class constructor](../../../../api/library/nodes/class.nodereference_cpp.md#NodeReference_constchar). By default, the loaded node is not synchronized, which is suitable for static objects at run time and at the same time saves performance. For dynamic objects to be synchronized, the suitable synchronization mask should be set.
### Arguments

- *const char ** **path** - Path to the `*.node` file.
- *unsigned char* **sync_mask** - Synchronization mask, one of the [SYNC_MASK](#SYNC_MASK) values.
- *Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md) &* **init_transform** - Initial transformation of the node.

### Return value

Node Reference instance if it was loaded successfully; otherwise nullptr.
## Ptr < NodeReference > loadNodeReference ( const char * path , unsigned char sync_mask = 0 )

Loads a node reference from the specified file to the world on the Master and all Slaves and places it to the origin with default transformation. This is a network analogue of the [NodeReference class constructor](../../../../api/library/nodes/class.nodereference_cpp.md#NodeReference_constchar). By default, the loaded node is not synchronized, which is suitable for static objects at run time and at the same time saves performance. For dynamic objects to be synchronized, the suitable synchronization mask should be set.
### Arguments

- *const char ** **path** - Path to the `*.node` file.
- *unsigned char* **sync_mask** - Synchronization mask, one of the [SYNC_MASK](#SYNC_MASK) values.

### Return value

Node Reference instance if it was loaded successfully; otherwise nullptr.
## bool isNodeLoadedBySyncker ( const Ptr < Node > & node ) const

Returns a value indicating if the given node was loaded by the Syncker via the [*loadNode()*](#loadNode_cstr_uchar_Mat4_Node) or the [*loadNodeReference()*](#loadNodeReference_cstr_uchar_Mat4_NodeReference) method.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Node](../../../../api/library/nodes/class.node_cpp.md)> &* **node** - Node to be checked.

### Return value

true if the given node was created via the [*createNode()*](#createNode_Node_uchar_bool) method; otherwise, false.
## void * addCallback ( Master::CALLBACK_INDEX callback , Unigine:: CallbackBase * func )

Adds a callback of the specified type. Callback functions can be used to determine actions to be performed when sending or receiving user messages, as well as when changing settings on the Master or a Slave. The signature of the callback function can be one of the following:
```cpp
// for the Syncker::Master::SESSION_STARTED type
void callback_function_name(void);

// for the Syncker::Master::SESSION_FINISHED type
void callback_function_name(void);

// for the Syncker::Master::SLAVE_CONNECTED type
void callback_function_name(int slave_num);

// for the Syncker::Master::SLAVE_DISCONNECTED type
void callback_function_name(int slave_num);

// for the Syncker::Master::MASTER_SETUP_CHANGED type
void callback_function_name(void);

// for the Syncker::Master::SLAVE_SETUP_CHANGED type
void callback_function_name(int slave_num);

```


### Arguments

- *Master::CALLBACK_INDEX* **callback** - Callback type. One of the following values:

  - [SESSION_STARTED](#SESSION_STARTED)
  - [SESSION_CONTINUED](#SESSION_CONTINUED)
  - [SESSION_FINISHED](#SESSION_FINISHED)
  - [SLAVE_CONNECTED](#SLAVE_CONNECTED)
  - [SLAVE_DISCONNECTED](#SLAVE_DISCONNECTED)
  - [MASTER_SETUP_CHANGED](#MASTER_SETUP_CHANGED)
  - [SLAVE_SETUP_CHANGED](#SLAVE_SETUP_CHANGED)
- *Unigine::[CallbackBase](../../../../api/library/common/callbacks/class.callbackbase_cpp.md) ** **func** - Callback pointer.

### Return value

Number of the last added callback of the specified type, if the callback was added successfully; otherwise, **-1**.
## bool removeCallback ( Master::CALLBACK_INDEX callback , void * func )

Removes a given callback from the list of callbacks of the specified type. Callback functions can be used to determine actions to be performed when sending or receiving user messages, as well as when changing settings on the Master or a Slave.
### Arguments

- *Master::CALLBACK_INDEX* **callback** - Callback type. One of the following values:

  - [SESSION_STARTED](#SESSION_STARTED)
  - [SESSION_CONTINUED](#SESSION_CONTINUED)
  - [SESSION_FINISHED](#SESSION_FINISHED)
  - [SLAVE_CONNECTED](#SLAVE_CONNECTED)
  - [SLAVE_DISCONNECTED](#SLAVE_DISCONNECTED)
  - [MASTER_SETUP_CHANGED](#MASTER_SETUP_CHANGED)
  - [SLAVE_SETUP_CHANGED](#SLAVE_SETUP_CHANGED)
- *void ** **func** - Callback pointer.

### Return value

true if the position callback with the given ID was removed successfully; otherwise false.
## void clearCallbacks ( Master::CALLBACK_INDEX callback )

Clears all added callbacks of the specified type. Callback functions can be used to determine actions to be performed when sending or receiving user messages, as well as when changing settings on the Master or a Slave.
### Arguments

- *Master::CALLBACK_INDEX* **callback** - Callback type. One of the following values:

  - [SESSION_STARTED](#SESSION_STARTED)
  - [SESSION_CONTINUED](#SESSION_CONTINUED)
  - [SESSION_FINISHED](#SESSION_FINISHED)
  - [SLAVE_CONNECTED](#SLAVE_CONNECTED)
  - [SLAVE_DISCONNECTED](#SLAVE_DISCONNECTED)
  - [MASTER_SETUP_CHANGED](#MASTER_SETUP_CHANGED)
  - [SLAVE_SETUP_CHANGED](#SLAVE_SETUP_CHANGED)

## int addMessageToBuffer ( const char * channel , const Ptr < Blob > & message )

Adds a message to the buffer to be received by [additional slaves](#setAllowExtraSlaves_int_void) as soon as they connect.
### Arguments

- *const char ** **channel** - Channel name. Multiple systems may use Syncker's network simultaneously (e.g. [IG](../../../../ig/index.md) and user's application). For convenience, all messages are sent and received via named channels.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Blob](../../../../api/library/common/class.blob_cpp.md)> &* **message** - Buffer containing the user message.

### Return value

Message ID.
## int getNumBufferedMessages ( const char * channel ) const

Returns the total number of buffered messages.
### Arguments

- *const char ** **channel** - Channel name. Multiple systems may use Syncker's network simultaneously (e.g. [IG](../../../../ig/index.md) and user's application). For convenience, all messages are sent and received via named channels.

### Return value

Total number of buffered messages.
## int getBufferedMessageID ( const char * channel , int index ) const

Returns the ID of the buffered message by its index.
### Arguments

- *const char ** **channel** - Channel name. Multiple systems may use Syncker's network simultaneously (e.g. [IG](../../../../ig/index.md) and user's application). For convenience, all messages are sent and received via named channels.
- *int* **index** - Message index number.

### Return value

Message ID.
## Ptr < Blob > getBufferedMessage ( const char * channel , int id ) const

Returns the buffer containing the message.
### Arguments

- *const char ** **channel** - Channel name. Multiple systems may use Syncker's network simultaneously (e.g. [IG](../../../../ig/index.md) and user's application). For convenience, all messages are sent and received via named channels.
- *int* **id** - Message ID.

### Return value

Buffer containing the user message.
## void removeBufferedMessage ( const char * channel , int id )

Removes the specified message from the buffer.
### Arguments

- *const char ** **channel** - Channel name. Multiple systems may use Syncker's network simultaneously (e.g. [IG](../../../../ig/index.md) and user's application). For convenience, all messages are sent and received via named channels.
- *int* **id** - Message ID.

## void clearBufferedMessages ( const char * channel )

Removes all messages from the buffer.
### Arguments

- *const char ** **channel** - Channel name. Multiple systems may use Syncker's network simultaneously (e.g. [IG](../../../../ig/index.md) and user's application). For convenience, all messages are sent and received via named channels.

## const char * getSlaveComputerName ( int num ) const

Returns the name of the slave computer with the specified index. If no name has been specified for the slave computer using the `-computer_name` startup argument, the system name is returned.
### Arguments

- *int* **num** - Slave index.

### Return value

Slave computer name.
## Ptr < Node > cloneNode ( const Ptr < Node > & node , unsigned char sync_mask = 0 )

Clones the specified node and synchronizes its cloning on all Slaves.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Node](../../../../api/library/nodes/class.node_cpp.md)> &* **node** - Node to clone.
- *unsigned char* **sync_mask** - Synchronization mask, one of the [SYNC_MASK](#SYNC_MASK) values.

### Return value

Cloned node.
## Ptr < Node > cloneNode ( const Ptr < Node > & node , unsigned char sync_mask , const Math:: Mat4 & init_transform )

Clones the specified node with the specified transformation and synchronizes its cloning on all Slaves.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Node](../../../../api/library/nodes/class.node_cpp.md)> &* **node** - Node to clone.
- *unsigned char* **sync_mask** - Synchronization mask, one of the [SYNC_MASK](#SYNC_MASK) values.
- *const  Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md) &* **init_transform** - Cloned node position and rotation (if not specified, the source node transformation is used).

### Return value

Cloned node.
