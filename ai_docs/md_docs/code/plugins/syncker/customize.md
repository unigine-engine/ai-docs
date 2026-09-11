# Implementing Syncker Logic for a Custom Project


## Initializing Syncker


First of all, you should initialize *Syncker*. To do so you can simply add the following code to the **AppSystemLogic** class for both *Master* and *Slave* applications.


Insert the following *Syncker* initialization code to the *AppSystemLogic::init()* method:


```cpp
#include "AppSystemLogic.h"
#include <plugins/Unigine/Syncker/UnigineSyncker.h>

 /* .. */

using namespace Unigine;
using namespace Plugins;

/* .. */

int AppSystemLogic::init()
{
	// update application even if focus was lost
	Engine::get()->setBackgroundUpdate(Engine::BACKGROUND_UPDATE_RENDER_NON_MINIMIZED);

	// get the Syncker manager interface
	Syncker::Manager* syncker_manager = Syncker::Manager::get();

	// initialize the Syncker using command line arguments
	// or you can initialize Syncker as Master or Slave directly
	//	via initMaster() or initSlave() methods without using command-line arguments
	syncker_manager->initSyncker();

	// enable debug information in right bottom corner
	syncker_manager->getSyncker()->setDebug(true);

	return 1;
}


```


In the `AppWorldLogic.cpp` file add the code to get the pointer to the manager and *Master* interface for further use in the *AppWorldLogic::init()* method:


```cpp
#include "AppWorldLogic.h"
#include <plugins/Unigine/Syncker/UnigineSyncker.h>
#include <UnigineWorld.h>
#include <UnigineGame.h>

using namespace Unigine;
using namespace Plugins;
using namespace Math;

int AppWorldLogic::init()
{

	Syncker::Manager *syncker_manager = Syncker::Manager::get();
	if (syncker_manager && syncker_manager->isMasterInitialized())
		syncker_master = syncker_manager->getMaster();

	return 1;
}


```


## Synchronizing Nodes/Materials


Objects of the following types are synchronized automatically: *[ObjectWaterGlobal](../../../objects/objects/water/water_object.md), [ObjectCloudLayer](../../../objects/objects/cloud_layer/index.md), [ObjectParticles](../../../objects/effects/particles/index.md), [WorldLight](../../../objects/lights/world/index.md)* if they present in the `*.world` file on all computers.


Synchronization of transformations is supported for all types of nodes. As for other type-specific parameters synchronization is available only for the following ones:


| - [NodeDummy](../../../api/library/nodes/class.nodedummy_cpp.md) - [NodeReference](../../../api/library/nodes/class.nodereference_cpp.md) - [FieldAnimation](../../../api/library/fields/class.fieldanimation_cpp.md) - [FieldHeight](../../../api/library/fields/class.fieldheight_cpp.md) - [FieldWeather](../../../api/library/fields/class.fieldweather_cpp.md) - [LightEnvironmentProbe](../../../api/library/lights/class.lightenvironmentprobe_cpp.md) - [LightOmni](../../../api/library/lights/class.lightomni_cpp.md) - [LightProj](../../../api/library/lights/class.lightproj_cpp.md) - [LightWorld](../../../api/library/lights/class.lightworld_cpp.md) |  | - [ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_cpp.md) - [ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cpp.md) - [ObjectParticles](../../../api/library/objects/class.objectparticles_cpp.md) - [ObjectVolumeSphere](../../../api/library/objects/class.objectvolumesphere_cpp.md) - [ObjectVolumeBox](../../../api/library/objects/class.objectvolumebox_cpp.md) - [ObjectVolumeOmni](../../../api/library/objects/class.objectvolumeomni_cpp.md) - [ObjectVolumeProj](../../../api/library/objects/class.objectvolumeproj_cpp.md) - [ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_cpp.md) - [ObjectWaterMesh](../../../api/library/objects/class.objectwatermesh_cpp.md) |  | - [ObjectSky](../../../api/library/objects/class.objectsky_cpp.md) - [ObjectCloudLayer](../../../api/library/objects/class.objectcloudlayer_cpp.md) - [NodeExtern](../../../api/library/nodes/class.nodeextern_cpp.md) - [ObjectExtern](../../../api/library/objects/class.objectextern_cpp.md) - [WorldExtern](../../../api/library/worlds/class.worldextern_cpp.md) - [WorldTransformJoint](../../../api/library/worlds/class.worldtransformjoint_cpp.md) - [PlayerDummy](../../../api/library/players/class.playerdummy_cpp.md) - [PlayerSpectator](../../../api/library/players/class.playerspectator_cpp.md) - [PlayerActor](../../../api/library/players/class.playeractor_cpp.md) |
|---|---|---|---|---|


> **Notice:** Automatic synchronization of run-time changes of the *Global Terrain* object is not supported, but it can be implemented manually [using custom messages](#cpp_sync_terrain).


To start synchronizing other nodes or materials (the logic is the same for both), that exist in the world, you just need to tell *Syncker* which of them you want. To do so you can add the following code to the ***AppWorldLogic::init()*** method of your master application:


```cpp
int AppWorldLogic::init()
{

/* ... */

	// checking if we have a Master interface
	if (syncker_master)
	{
		// getting a pointer for the node named "material_ball"
		NodePtr my_node = World::getNodeByName("material_ball");

		// add the existing node to synchronization
		syncker_master->addSyncNode(my_node, Syncker::Master::SYNC_MASK::TRANSFORM);
	}

	return 1;
}


```


Keep in mind that only node flags and transformation are synchronized by default:


```cpp
syncker_master->addSyncNode(my_node, Syncker::Master::SYNC_MASK::NODE_FLAGS | Syncker::Master::SYNC_MASK::TRANSFORM);

```


To sync other parameters using *[Master::addSyncNode()](../../../api/library/plugins/syncker/class.syncker_master_cpp.md#addSyncNode_Node_uchar_void)*, you need to add the corresponding masks. For example, add *[SYNC_MASK::DERIVED](../../../api/library/plugins/syncker/class.syncker_master_cpp.md#DERIVED)* to sync parameters of the derived node (such as Player, Light, Decal, etc.), and *[SYNC_MASK::OBJECT](../../../api/library/plugins/syncker/class.syncker_master_cpp.md#OBJECT)* if you also want to sync the object parameters of the node:


```cpp
syncker_master->addSyncNode(my_node, Syncker::Master::SYNC_MASK::NODE_FLAGS | Syncker::Master::SYNC_MASK::TRANSFORM | Syncker::Master::SYNC_MASK::DERIVED | Syncker::Master::SYNC_MASK::OBJECT);

```


Now, you can implement your logic for synchronized nodes in the *AppWorldLogic::update()* method for *Master*:


```cpp
int AppWorldLogic::update()
{

	/* ... */

	// checking if we have a Master interface
	if (syncker_master)
	{
		// getting a pointer for the node named "material_ball"
		NodePtr my_node = World::getNodeByName("material_ball");

		// changing node's rotation
		my_node->setRotation(my_node->getRotation() * Math::quat(0, 0, Game::getIFps()));
	}

	return 1;
}


```


## Creating/Deleting Nodes at Runtime


You can create and delete nodes at run time. To synchronize creation of a node on all connected *Slave* PCs, use the *[createNode()](../../../api/library/plugins/syncker/class.syncker_master_cpp.md#createNode_Node_uchar_bool)* function.


> **Notice:** Please note, that the *[createNode()](../../../api/library/plugins/syncker/class.syncker_master_cpp.md#createNode_Node_uchar_bool)* method support only a limited number of node types, so it is recomended to [load nodes](#cpp_load) from `*.node` files instead.


```cpp
/* ... */
int cube_created = 0;

int AppWorldLogic::update()
{

	/* ... */

	// checking if we have a Master interface and cube is not yet created
	if (syncker_master && !cube_created)
	{
		// creating a dynamic cube and set up its transformation
		ObjectMeshStaticPtr dynamic_cube = ObjectMeshStatic::create("core/meshes/box.mesh");
		dynamic_cube->setPosition(Math::Vec3(Game::getRandomFloat(-50, 50), Game::getRandomFloat(-50, 50), Game::getRandomFloat(0, 50)));
		dynamic_cube->setRotation(Math::quat(Game::getRandomFloat(0, 360), Game::getRandomFloat(0, 360), Game::getRandomFloat(0, 360)));

		// commanding Slaves to create a dynamic node and adding it to synchronization
		syncker_master->createNode(dynamic_cube);

		cube_created = 1;
	}

	return 1;
}


```


## Loading Nodes at Runtime


To synchronize node loading from a `*.node` file on all connected *Slave* PCs, use the *[loadNode()](../../../api/library/plugins/syncker/class.syncker_master_cpp.md#loadNode_cstr_uchar_Mat4_Node)* or *[loadNodereference()](../../../api/library/plugins/syncker/class.syncker_master_cpp.md#loadNodeReference_cstr_uchar_Mat4_NodeReference)* methods. This approach is **recommended as it allows adding nodes of all types**, unlike the *[createNode()](../../../api/library/plugins/syncker/class.syncker_master_cpp.md#createNode_Node_uchar_bool)* method that supports only a limited number of them.


```cpp
/* ... */
int node_loaded = 0;

int AppWorldLogic::update()
{

	/* ... */

	// checking if we have a Master interface and our node is not yet loaded
	if (syncker_master && !node_loaded)
	{

		// commanding Slaves to load a node and adding it to synchronization
		syncker_master->loadNode("my_node.node", Syncker::Master::SYNC_MASK::NODE_FLAGS | Syncker::Master::SYNC_MASK::TRANSFORM);

		node_loaded = 1;
	}

	return 1;
}


```


## Customizing Synchronization via User Messages


Let us consider the following simple example: we can set transformation for a node, by simply sending rotation and position via a [user message](../../../code/plugins/syncker/index.md#user_messages).


1. First step is to create an object on *Master* and on all *Slave* PCs as a static one (without adding it to synchronization).
2. Next, we implement a callback function:

  - **on_message_received** � to be called on receiving a user message. Here we extract the parameters from the received message and use them (in this case to change node's transformation).
3. And the last step is to set this callback using the *[setMessageReceivedCallback()](../../../api/library/plugins/syncker/class.syncker_syncker_cpp.md#setMessageReceivedCallback_cstr_CallbackBase_ptr_void)* method in *AppWorldLogic::init()* ```cpp // declaring and initializing pointers for the Master, Slave, and Syncker instances Unigine::Plugins::Syncker::Master* master = nullptr; Unigine::Plugins::Syncker::Slave* slave = nullptr; Unigine::Plugins::Syncker::Syncker* syncker = nullptr; // declaring a node, that we are going to transform via user messages NodePtr node; // declaring a blob to store our messages Unigine::BlobPtr blob = Unigine::Blob::create(); // declaring message types to be used enum MESSAGE_TYPE { REPORT, TRANSFORM, }; /* ... */ /// callback function to be fired on receiving a user message void AppWorldLogic::on_message_received(const Unigine::BlobPtr& message) { // reading an unsigned char from the blob defining message type (REPORT or TRANSFORM) unsigned char type = message->readUChar(); switch (type) { case REPORT: { // printing to the console that we have received a message Log::message("REPORT Message received!"); } break; case TRANSFORM: { // reading position and rotation from the message and using them to update node's transformation Vec3 pos = Vec3(message->readDVec3()); quat rot = message->readQuat(); node->setTransform(translate(pos) * Mat4(rotate(rot))); } break; } } int AppWorldLogic::init() { /* ... */ // trying to get a Manager interface auto manager = Syncker::Manager::get(); if (manager) { // checking if we have a Master interface if (manager->isMasterInitialized()) master = manager->getMaster(); else if (manager->isSlaveInitialized()) slave = manager->getSlave(); // getting a pointer to Master/Slave base class syncker = manager->getSyncker(); } // subscribing to network messages if (syncker) syncker->setMessageReceivedCallback("net", MakeCallback(this, &AppWorldLogic::on_message_received)); /* ... */ // somewhere in code... sending a REPORT message blob->clear(); blob->writeUChar(REPORT); syncker->sendMessage("net", blob); return 1; } int AppWorldLogic::update() { /* ... */ // sending a message with object's transform to all peers if (master) { Vec3 pos = node->getPosition(); quat rot = node->getRotation(); blob->clear(); blob->writeUChar(TRANSFORM); blob->writeDVec3(dvec3(pos)); blob->writeQuat(rot); syncker->sendMessage("net", blob); } /* ... */ return 1; } ```


### Synchronizing Terrain Modifications


Run-time changes of the *Global Terrain* object are not synchronized automatically, but you can do it manually using custom messages:


```cpp
Plugins::Syncker::Manager* syncker_manager = nullptr;

ObjectTerrainGlobalPtr terrain;

/// Method updating the Terrain
void AppWorldLogic::update_terrain(int detail, float threshold, float width, float contrast)
{
	// apply parameters to terrain
	terrain->getDetail(detail)->setMaskThreshold(threshold);
	terrain->getDetail(detail)->setMaskWidth(width);
	terrain->getDetail(detail)->setMaskContrast(contrast);

	if (syncker_manager)
	{
		auto master = syncker_manager->getMaster();
		if (master)
		{
			// send the "terrain_update" message with parameters
			BlobPtr blob = Blob::create();
			blob->writeInt(detail);
			blob->writeFloat(threshold);
			blob->writeFloat(width);
			blob->writeFloat(contrast);

			master->sendMessage("terrain_update", blob);
		}
	}
}

void AppWorldLogic::on_terrain_update(const Unigine::BlobPtr& message)
{
	// read parameters from the message in the same order
	int detail = message->readInt();
	float threshold = message->readFloat();
	float width = message->readFloat();
	float contrast = message->readFloat();
	// invoke update_terrain to apply parameters
	update_terrain(detail, threshold, width, contrast);
}

int AppWorldLogic::init()
{

	// getting the terrain object (this operation is performed once, so it should be in the init() method)
	terrain = checked_ptr_cast<ObjectTerrainGlobal>(World::getNodeByType(Node::OBJECT_TERRAIN_GLOBAL));

	// for Slave
	syncker_manager = Plugins::Syncker::Manager::get();
	if (syncker_manager)
	{
		auto slave = syncker_manager->getSlave();
		if (slave)
		{
			// set the on_terrain_update() method to be called on receiving the "terrain_update" message by a Slave.
			slave->setMessageReceivedCallback("terrain_update", MakeCallback(this, &AppWorldLogic::on_terrain_update));
		}
	}

	return 1;
}

int AppWorldLogic::update()
{

	 // for the Master
	if (Input::isKeyPressed(Input::KEY_T))
	{
		update_terrain(1, 2.0, 3.0f, 4.0f);
	}

	return 1;
}


```


## Changing Views and Cameras


You can change the viewport on the *Master* or *Slave* side. For this purpose you can use the following code (example):


```cpp
Plugins::Syncker::Manager* syncker_manager = nullptr;

	/* ...

	perform checks if the Syncker plugin is loaded
	and get the Syncker manager interface (Manager)

	 ... */

	// if syncker is initialized, assigning the config settings for the specified computer named "MyPC_1"
	if (syncker_manager->isSynckerInitialized())
		syncker_manager->getSyncker()->setComputerName("MyPC_1");

	/* ... */


```


You can also tell *Slave* to use another camera. To do so, you can use the following code (example):


```cpp
/* ... */

PlayerSpectatorPtr aux_player = nullptr;

/* ... */

int AppWorldLogic::update()
{

	/* ... */

	// checking if we have a Master interface
	if (syncker_master && !aux_player)
	{
		// creating a new auxiliary player (on Master and Slaves)
		aux_player = PlayerSpectator::create();
		aux_player->setPosition(Vec3(0.0f, -40.0f, 200.0f));
		aux_player->setDirection(vec3(0.0f, 1.0f, 0.0f), vec3_up);
		aux_player->setMinVelocity(10);
		aux_player->setMaxVelocity(aux_player->getMinVelocity() * 2);

		// commanding Slaves to create a new player and adding it to synchronization
		syncker_master->createNode(aux_player, ~0);

		// setting a new created player for the computer named "MyPC_1"
		syncker_master->setCustomPlayer("MyPC_1", aux_player);
	}

	/* ... */

	return 1;
}


```
