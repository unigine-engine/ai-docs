# Unigine::Plugins::Syncker::Master Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Syncker


This class represents the master interface of the Syncker.


> **Notice:** [Syncker](../../../../code/plugins/syncker/index.md) plugin must be loaded.


## Master Class

### Members

## int getNumSyncMaterials () const

Returns the current total number of materials in the synchronization queue.
### Return value

Current total number of materials in the synchronization queue.
## int getNumSyncNodes () const

Returns the current total number of nodes in the synchronization queue.
### Return value

Current total number of nodes in the synchronization queue.
## void setDefaultSyncNodes ( int nodes )

Sets a new mask defining types of nodes that will be synchronized automatically after world loading. This mask can be used for optimization reasons limiting the number of nodes to be synchronized and thus reducing network load. For example, you can restrict automatic synchronization to global water, and clouds only:
```cpp
master.setDefaultSyncNodes(MASTER_WATER_GLOBAL | MASTER_CLOUD_LAYER);
```


### Arguments

- *int* **nodes** - The mask defining types of nodes that will be synchronized automatically after world loading.

## int getDefaultSyncNodes () const

Returns the current mask defining types of nodes that will be synchronized automatically after world loading. This mask can be used for optimization reasons limiting the number of nodes to be synchronized and thus reducing network load. For example, you can restrict automatic synchronization to global water, and clouds only:
```cpp
master.setDefaultSyncNodes(MASTER_WATER_GLOBAL | MASTER_CLOUD_LAYER);
```


### Return value

Current mask defining types of nodes that will be synchronized automatically after world loading.
## void setSyncWorldLoad ( int load )

Sets a new value indicating whether synchronization of world loading via the UDP protocol is enabled.
### Arguments

- *int* **load** - The synchronization of world loading via the UDP protocol

## int isSyncWorldLoad () const

Returns the current value indicating whether synchronization of world loading via the UDP protocol is enabled.
### Return value

Current synchronization of world loading via the UDP protocol
## void setSyncRender ( int render )

Sets a new A value indicating if synchronization of all render parameters via the UDP protocol (light scattering, occlusion, etc.) is enabled.
> **Notice:** When all slaves use the same rendering settings, synchronization of render parameters can be disabled.


### Arguments

- *int* **render** - The synchronization of all render parameters via the UDP protocol

## int isSyncRender () const

Returns the current A value indicating if synchronization of all render parameters via the UDP protocol (light scattering, occlusion, etc.) is enabled.
> **Notice:** When all slaves use the same rendering settings, synchronization of render parameters can be disabled.


### Return value

Current synchronization of all render parameters via the UDP protocol
## void setSyncViewOffset ( int offset )

Sets a new value indicating whether synchronization of view offset for projections is enabled.
### Arguments

- *int* **offset** - The synchronization of view offset for projections via the UDP protocol

## int isSyncViewOffset () const

Returns the current value indicating whether synchronization of view offset for projections is enabled.
### Return value

Current synchronization of view offset for projections via the UDP protocol
## void setSyncPlayer ( int player )

Sets a new value indicating whether synchronization of the current player's parameters via the UDP protocol is enabled.
The following parameters are synchronized:


- Its transformation
- Projection matrix
- Viewport mask
- Mask for reflections
- Applied post-materials (if any)


> **Notice:** Current player synchronization is used only when all slaves use the same camera.


### Arguments

- *int* **player** - The synchronization of the current player's parameters (transformation, projection matrix, viewport and reflection masks, applied post-materials) via the UDP protocol

## int isSyncPlayer () const

Returns the current value indicating whether synchronization of the current player's parameters via the UDP protocol is enabled.
The following parameters are synchronized:


- Its transformation
- Projection matrix
- Viewport mask
- Mask for reflections
- Applied post-materials (if any)


> **Notice:** Current player synchronization is used only when all slaves use the same camera.


### Return value

Current synchronization of the current player's parameters (transformation, projection matrix, viewport and reflection masks, applied post-materials) via the UDP protocol
## float getNumSlaves () const

Returns the current total number of the slaves connected to the master.
### Return value

Current total number of the slaves connected to the master.
## void setAllowExtraSlaves ( int slaves )

Sets a new value indicating whether new Slaves can connect to the Master after starting the session. This can be used, for example, to connect a Slave which is used as a tool for configuring projections and does not operate as an IG.
### Arguments

- *int* **slaves** - The true permits new Slaves to connect to the Master after starting the session; false - forbids it.

## int isAllowExtraSlaves () const

Returns the current value indicating whether new Slaves can connect to the Master after starting the session. This can be used, for example, to connect a Slave which is used as a tool for configuring projections and does not operate as an IG.
### Return value

Current true permits new Slaves to connect to the Master after starting the session; false - forbids it.
## void setSendRate ( float rate )

Sets a new
frequency of sending packets to Slaves. Use this method when network load is too high and slows down the whole IG system. It is recommended to use this method with [interpolation](../../../../api/library/plugins/syncker/class.syncker_syncker_usc.md#setInterpolation_int_void) enabled.


```cpp
//On the Master
master->setSendRate(15.0f); // send packets 15 times per second

//Both on the Master and all Slaves
syncker->setInterpolationPeriod(0.1f); // 100 ms delay

```


### Arguments

- *float* **rate** - The frequency of sending packets to Slaves. The default value is -1 (every frame). > **Notice:** The value should not be less than ***1�/�[getInterpolationPeriod()](../../../../api/library/plugins/syncker/class.syncker_syncker_usc.md#getInterpolationPeriod_double)***, otherwise the image shall be "stuttering".

## float getSendRate () const

Returns the current
frequency of sending packets to Slaves. Use this method when network load is too high and slows down the whole IG system. It is recommended to use this method with [interpolation](../../../../api/library/plugins/syncker/class.syncker_syncker_usc.md#setInterpolation_int_void) enabled.


```cpp
//On the Master
master->setSendRate(15.0f); // send packets 15 times per second

//Both on the Master and all Slaves
syncker->setInterpolationPeriod(0.1f); // 100 ms delay

```


### Return value

Current frequency of sending packets to Slaves.
The default value is -1 (every frame).


> **Notice:** The value should not be less than ***1�/�[getInterpolationPeriod()](../../../../api/library/plugins/syncker/class.syncker_syncker_usc.md#getInterpolationPeriod_double)***, otherwise the image shall be "stuttering".

---

## string getSlaveAddress ( int num )

Returns the network address of the given slave computer.
### Arguments

- *int* **num** - Slave number.

### Return value

Network address of the slave computer.
## int getSlavePort ( int num )

Returns the UDP port used by the slave with the specified number.
### Arguments

- *int* **num** - Slave number.

### Return value

UDP port of the specified slave computer. 0 - means any unused port available.
## long getSlaveID ( int num )

Returns the ID of the slave with the specified number. A unique Slave ID consists of two parts: IP (32 bits) + port (16 bits)
### Arguments

- *int* **num** - Slave number.

### Return value

ID of the slave with the specified number.
## string getSlaveWorldName ( int num )

Returns the name of the world file currently loaded on the specified slave.
### Arguments

- *int* **num** - Slave number.

### Return value

Name of the world file currently loaded on the specified slave.
## void addSyncNode ( Node node , int sync_mask = SYNC_MASK::NODE_FLAGS | SYNC_MASK::TRANSFORM )


Enables synchronization of parameters of the given node via the UDP protocol.


> **Notice:** Scene nodes are not synchronized by default, this method is used to add a particular node to the synchronization queue.


### Arguments

- *[Node](../../../../api/library/nodes/class.node_usc.md)* **node** - Node to synchronize.
- *int* **sync_mask** - Synchronization mask, one of the [SYNC_MASK](#SYNC_MASK) values. By default, only node transformation is synchronized. To sync other parameters, select the corresponding mask.

## void addSyncNodes ( Vector< Node > nodes , int sync_mask = SYNC_MASK::NODE_FLAGS | SYNC_MASK::TRANSFORM )


Enables synchronization of parameters of given nodes via the UDP protocol.


> **Notice:** Scene nodes are not synchronized by default, this method is used to add particular nodes to the synchronization queue.


### Arguments

- *Vector<[Node](../../../../api/library/nodes/class.node_usc.md)>* **nodes** - List of nodes to synchronize.
- *int* **sync_mask** - Synchronization mask, one of the [SYNC_MASK](#SYNC_MASK) values. By default, only node transformation is synchronized. To sync other parameters, select the corresponding mask.

## void setSyncNodeMask ( Node node , int sync_mask )

Sets a new synchronization mask for the specified node. Synchronization mask can be used for optimization reasons limiting the amount of data to be synchronized and thus reducing network load. For example, for moving parts of a helicopter we can set a mask to synchronize only node transformations:
```cpp
master.setSyncNodeMask(fan_small, MASTER_TRANSFORM);
master.setSyncNodeMask(fan_big, MASTER_TRANSFORM);

```


### Arguments

- *[Node](../../../../api/library/nodes/class.node_usc.md)* **node** - Node for which a new synchronization mask is to be set.
- *int* **sync_mask** - New synchronization mask to be set for the specified node, one of the [SYNC_MASK](#SYNC_MASK) values.

## bool isSyncNode ( Node node )

Returns a value indicating if synchronization of the given node is enabled. Using this method you can quickly check if a node is monitored by the Syncker (node's states are dispatched to Slaves over the network).
### Arguments

- *[Node](../../../../api/library/nodes/class.node_usc.md)* **node** - Node to be checked.

### Return value

true if synchronization of the given node is enabled; otherwise, false.
## Node getSyncNode ( int num )

Returns the synchronized node with the given number.
### Arguments

- *int* **num** - Node number in the synchronization queue.

### Return value

Synchronized node.
## void removeSyncNode ( int num )

Removes the specified node from the synchronization queue.
### Arguments

- *int* **num** - Node number in the synchronization queue.

## void removeSyncNode ( Node node )

Removes the specified node from the synchronization queue.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_usc.md)* **node** - Node to be removed from synchronization.

## void removeSyncNodeID ( int node_id )

Removes the specified node from the synchronization queue by its ID.
### Arguments

- *int* **node_id** - ID of the node to be removed from the synchronization queue.

## void removeSyncNodes ( Vector< Node > nodes )

Removes the specified nodes from the synchronization queue.
### Arguments

- *Vector<[Node](../../../../api/library/nodes/class.node_usc.md)>* **nodes** - List of nodes to be removed from the synchronization queue.

## void clearSyncNodes ( )

Removes all nodes from the synchronization queue.
## void addSyncMaterial ( Material material )


Enables synchronization of the given material via the UDP protocol.


> **Notice:** Scene materials are not synchronized by default, this method is used to add a particular material to the synchronization queue.


### Arguments

- *[Material](../../../../api/library/rendering/class.material_usc.md)* **material** - Material to synchronize.

## void addSyncMaterials ( Vector< Material > materials )


Enables synchronization of given materials via the UDP protocol.


> **Notice:** Scene materials are not synchronized by default, this method is used to add particular materials to the synchronization queue.


### Arguments

- *Vector<[Material](../../../../api/library/rendering/class.material_usc.md)>* **materials** - List of materials to synchronize.

## bool isSyncMaterial ( Material mat )

Returns a value indicating if synchronization of the given material is enabled. Using this method you can quickly check if a material is monitored by the Syncker (material's states are dispatched to Slaves over the network).
### Arguments

- *[Material](../../../../api/library/rendering/class.material_usc.md)* **mat** - Material to be checked.

### Return value

true if synchronization of the given material is enabled; otherwise, false.
## Material getSyncMaterial ( int num )

Returns the synchronized material with the given number.
### Arguments

- *int* **num** - Material number in the synchronization queue.

### Return value

Synchronized material.
## void removeSyncMaterial ( int num )

Removes the material with the given number from the synchronization queue.
### Arguments

- *int* **num** - Material number in the synchronization queue.

## void removeSyncMaterial ( Material material )

Removes the specified material from the synchronization queue.
### Arguments

- *[Material](../../../../api/library/rendering/class.material_usc.md)* **material** - Material to be removed from the synchronization queue.

## void removeSyncMaterials ( Vector< Material > materials )

Removes the specified materials from the synchronization queue.
### Arguments

- *Vector<[Material](../../../../api/library/rendering/class.material_usc.md)>* **materials** - List of materials to be removed from the synchronization queue.

## void clearSyncMaterials ( )

Removes all materials from the synchronization queue.
## bool createNode ( Node node , int sync_mask = 0 )


Synchronizes creation of the given node on all Slaves. This method is **to be called after node creation on the Master**.


> **Notice:** It is recommended to use the [*loadNode()*](#loadNode_cstr_uchar_Mat4_Node) or [*loadNodereference()*](#loadNodeReference_cstr_uchar_Mat4_NodeReference) methods whenever possible as this approach **allows adding nodes of all types**, unlike the [*createNode()*](#createNode_Node_uchar_bool) method that supports only a limited number of them.

 **Example:**
```cpp
Node node = new NodeDummy();
master.createNode(node);

```


### Arguments

- *[Node](../../../../api/library/nodes/class.node_usc.md)* **node** - Node to create.
- *int* **sync_mask** - Synchronization mask, one of the [SYNC_MASK](#SYNC_MASK) values.

### Return value

true if the node was created successfully; otherwise, false.
## void deleteNode ( Node node )

Synchronizes deletion of the given node (with all its children) on the Master and all Slaves. Similar to calling *deleteLater()* for the node.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_usc.md)* **node** - Node to delete.

## int isNodeCreatedBySyncker ( Node node )

Returns a value indicating if the given node was created via the [*createNode()*](#createNode_Node_uchar_bool) method. Using this method you can quickly check if a node is in the run-time objects creation buffer.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_usc.md)* **node** - Node to be checked.

### Return value

**1** if the given node was created via the [*createNode()*](#createNode_Node_uchar_bool) method; otherwise, **0**.
## void setViewOffset ( vec3 offset )

Sets a new player's head position on the Master.
### Arguments

- *vec3* **offset** - New player's head position coordinates to be set.

## void loadWorld ( string name )

Loads a world from the specified file on the Master and all Slaves. Syncker is able to automatically synchronize the current world, but it works as follows: Slaves shall only start loading a new world after it is completely loaded on the Master. This method provides a 2x speedup of world loading process, as it forces all hosts to start loading the world almost simultaneously.
### Arguments

- *string* **name** - Path to the `*.world` file to be loaded.

## Node loadNode ( string path , int sync_mask = 0 , Mat4 init_transform )

Loads a node from the specified file to the world on the Master and all Slaves and places it to the specified ititial transformation. This is a network analogue of the *[loadNode()](../../../../api/library/engine/class.world_usc.md#loadNode_cstr_int_Node)* method of the *World* class. By default, the loaded node is not synchronized, which is suitable for static objects at run time and at the same time saves performance. For dynamic objects to be synchronized, the suitable synchronization mask should be set.
### Arguments

- *string* **path** - Path to the `*.node` file.
- *int* **sync_mask** - Synchronization mask, one of the [SYNC_MASK](#SYNC_MASK) values.
- *Mat4* **init_transform** - Initial transformation of the node.

### Return value

Loaded node or nullptr if an error has occurred.
## Node loadNode ( string path , int sync_mask = 0 )

Loads a node from the specified file to the world on the Master and all Slaves and places it at the origin with the default transformation. This is a network analogue of the *[loadNode()](../../../../api/library/engine/class.world_usc.md#loadNode_cstr_int_Node)* method of the *World* class. By default, the loaded node is not synchronized, which is suitable for static objects at run time and at the same time saves performance. For dynamic objects to be synchronized, the suitable synchronization mask should be set.
### Arguments

- *string* **path** - Path to the `*.node` file.
- *int* **sync_mask** - Synchronization mask, one of the [SYNC_MASK](#SYNC_MASK) values.

### Return value

Loaded node or nullptr if an error has occurred.
## NodeReference loadNodeReference ( string path , int sync_mask = 0 , Mat4 init_transform )

Loads a node reference from the specified file to the world on the Master and all Slaves and places it to the specified ititial transformation. This is a network analogue of the [NodeReference class constructor](../../../../api/library/nodes/class.nodereference_usc.md#NodeReference_constchar). By default, the loaded node is not synchronized, which is suitable for static objects at run time and at the same time saves performance. For dynamic objects to be synchronized, the suitable synchronization mask should be set.
### Arguments

- *string* **path** - Path to the `*.node` file.
- *int* **sync_mask** - Synchronization mask, one of the [SYNC_MASK](#SYNC_MASK) values.
- *Mat4* **init_transform** - Initial transformation of the node.

### Return value

Node Reference instance if it was loaded successfully; otherwise nullptr.
## NodeReference loadNodeReference ( string path , int sync_mask = 0 )

Loads a node reference from the specified file to the world on the Master and all Slaves and places it to the origin with default transformation. This is a network analogue of the [NodeReference class constructor](../../../../api/library/nodes/class.nodereference_usc.md#NodeReference_constchar). By default, the loaded node is not synchronized, which is suitable for static objects at run time and at the same time saves performance. For dynamic objects to be synchronized, the suitable synchronization mask should be set.
### Arguments

- *string* **path** - Path to the `*.node` file.
- *int* **sync_mask** - Synchronization mask, one of the [SYNC_MASK](#SYNC_MASK) values.

### Return value

Node Reference instance if it was loaded successfully; otherwise nullptr.
## bool isNodeLoadedBySyncker ( Node node )

Returns a value indicating if the given node was loaded by the Syncker via the [*loadNode()*](#loadNode_cstr_uchar_Mat4_Node) or the [*loadNodeReference()*](#loadNodeReference_cstr_uchar_Mat4_NodeReference) method.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_usc.md)* **node** - Node to be checked.

### Return value

**1** if the given node was created via the [*createNode()*](#createNode_Node_uchar_bool) method; otherwise, **0**.
## Variable addCallback ( int callback , Variable func )

Adds a callback of the specified type. Callback functions can be used to determine actions to be performed when sending or receiving user messages, as well as when changing settings on the Master or a Slave. The signature of the callback function can be one of the following:
```cpp
// for the Syncker.Master.SESSION_STARTED type
void callback_function_name(void);

// for the Syncker.Master.SESSION_FINISHED type
void callback_function_name(void);

// for the Syncker.Master.SLAVE_CONNECTED type
void callback_function_name(int slave_num);

// for the Syncker.Master.SLAVE_DISCONNECTED type
void callback_function_name(int slave_num);

// for the Syncker.Master.MASTER_SETUP_CHANGED type
void callback_function_name(void);

// for the Syncker.Master.SLAVE_SETUP_CHANGED type
void callback_function_name(int slave_num);

```


### Arguments

- *int* **callback** - Callback type. One of the following values:

  - [SESSION_STARTED](#SESSION_STARTED)
  - [SESSION_CONTINUED](#SESSION_CONTINUED)
  - [SESSION_FINISHED](#SESSION_FINISHED)
  - [SLAVE_CONNECTED](#SLAVE_CONNECTED)
  - [SLAVE_DISCONNECTED](#SLAVE_DISCONNECTED)
  - [MASTER_SETUP_CHANGED](#MASTER_SETUP_CHANGED)
  - [SLAVE_SETUP_CHANGED](#SLAVE_SETUP_CHANGED)
- *Variable* **func** - There are two ways you can specify a callback function:

  - **by name** - when you call a function, declared globally.
  - **by ID** - when you call a member function of a certain class. > **Notice:** An ID can be obtained via [functionid()](../../../../api/library/common/class.system_usc.md#functionid_variable_int).

### Return value

Number of the last added callback of the specified type, if the callback was added successfully; otherwise, **-1**.
## bool removeCallback ( int callback , Variable func )

Removes a given callback from the list of callbacks of the specified type. Callback functions can be used to determine actions to be performed when sending or receiving user messages, as well as when changing settings on the Master or a Slave.
### Arguments

- *int* **callback** - Callback type. One of the following values:

  - [SESSION_STARTED](#SESSION_STARTED)
  - [SESSION_CONTINUED](#SESSION_CONTINUED)
  - [SESSION_FINISHED](#SESSION_FINISHED)
  - [SLAVE_CONNECTED](#SLAVE_CONNECTED)
  - [SLAVE_DISCONNECTED](#SLAVE_DISCONNECTED)
  - [MASTER_SETUP_CHANGED](#MASTER_SETUP_CHANGED)
  - [SLAVE_SETUP_CHANGED](#SLAVE_SETUP_CHANGED)
- *Variable* **func** - There are two ways you can specify a callback function:

  - **by name** - when you call a function, declared globally.
  - **by ID** - when you call a member function of a certain class. > **Notice:** An ID can be obtained via [functionid()](../../../../api/library/common/class.system_usc.md#functionid_variable_int).

### Return value

true if the position callback with the given ID was removed successfully; otherwise false.
## int addMessageToBuffer ( string channel , Blob message )

Adds a message to the buffer to be received by [additional slaves](#setAllowExtraSlaves_int_void) as soon as they connect.
### Arguments

- *string* **channel** - Channel name. Multiple systems may use Syncker's network simultaneously (e.g. [IG](../../../../ig/index.md) and user's application). For convenience, all messages are sent and received via named channels.
- *[Blob](../../../../api/library/common/class.blob_usc.md)* **message** - Buffer containing the user message.

### Return value

Message ID.
## int getNumBufferedMessages ( string channel )

Returns the total number of buffered messages.
### Arguments

- *string* **channel** - Channel name. Multiple systems may use Syncker's network simultaneously (e.g. [IG](../../../../ig/index.md) and user's application). For convenience, all messages are sent and received via named channels.

### Return value

Total number of buffered messages.
## int getBufferedMessageID ( string channel , int index )

Returns the ID of the buffered message by its index.
### Arguments

- *string* **channel** - Channel name. Multiple systems may use Syncker's network simultaneously (e.g. [IG](../../../../ig/index.md) and user's application). For convenience, all messages are sent and received via named channels.
- *int* **index** - Message index number.

### Return value

Message ID.
## Blob getBufferedMessage ( string channel , int id )

Returns the buffer containing the message.
### Arguments

- *string* **channel** - Channel name. Multiple systems may use Syncker's network simultaneously (e.g. [IG](../../../../ig/index.md) and user's application). For convenience, all messages are sent and received via named channels.
- *int* **id** - Message ID.

### Return value

Buffer containing the user message.
## void removeBufferedMessage ( string channel , int id )

Removes the specified message from the buffer.
### Arguments

- *string* **channel** - Channel name. Multiple systems may use Syncker's network simultaneously (e.g. [IG](../../../../ig/index.md) and user's application). For convenience, all messages are sent and received via named channels.
- *int* **id** - Message ID.

## void clearBufferedMessages ( string channel )

Removes all messages from the buffer.
### Arguments

- *string* **channel** - Channel name. Multiple systems may use Syncker's network simultaneously (e.g. [IG](../../../../ig/index.md) and user's application). For convenience, all messages are sent and received via named channels.

## string getSlaveComputerName ( int num )

Returns the name of the slave computer with the specified index. If no name has been specified for the slave computer using the `-computer_name` startup argument, the system name is returned.
### Arguments

- *int* **num** - Slave index.

### Return value

Slave computer name.
## Node cloneNode ( Node node , int sync_mask = 0 )

Clones the specified node and synchronizes its cloning on all Slaves.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_usc.md)* **node** - Node to clone.
- *int* **sync_mask** - Synchronization mask, one of the [SYNC_MASK](#SYNC_MASK) values.

### Return value

Cloned node.
## Node cloneNode ( Node node , int sync_mask , Mat4 init_transform )

Clones the specified node with the specified transformation and synchronizes its cloning on all Slaves.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_usc.md)* **node** - Node to clone.
- *int* **sync_mask** - Synchronization mask, one of the [SYNC_MASK](#SYNC_MASK) values.
- *Mat4* **init_transform** - Cloned node position and rotation (if not specified, the source node transformation is used).

### Return value

Cloned node.
