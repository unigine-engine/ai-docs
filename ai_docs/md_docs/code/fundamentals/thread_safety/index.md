# Thread Safety in API


[Unigine API](../../../api/index.md) objects are guaranteed to be used safely in the [main loop](../../../code/fundamentals/execution_sequence/main_loop.md). When it comes to multiple user threads, things get a bit more complicated.


As not all of API classes are thread-safe, you should take into consideration the behaviour type of an API member to reach safe multithreading in your application.


All types require special approaches described in this article.


### See Also


- [*Thread* Class](../../../api/library/common/mt/class.thread_cpp.md)
- [*AsyncQueue* Class](../../../api/library/filesystem/class.asyncqueue_cpp.md)
- The C++ API sample **Threads** demonstrating how to create and run custom threads using the [*Thread*](../../../api/library/common/mt/class.thread_cpp.md) class.


## Dealing with Multiple Threads


### Thread-Safe Objects


Fully thread-safe objects are free to use in any thread, be it the main loop or a user's one. This is provided due to thread synchronization mechanisms making all critical operations atomic and protecting data structures, it negates issues like *race condition* and others.


Only one thread is allowed to access data at the same time, while data is locked for other threads, that is why multiple threads may have to wait for each other until their tasks are finished.


> **Notice:** Many requests to data from multiple threads may cause additional performance loss due to synchronization.


The following API members are considered to be thread-safe:


- [**Filesystem**](../../../api/library/filesystem/class.filesystem_cpp.md)
- [**AsyncQueue**](../../../api/library/filesystem/class.asyncqueue_cpp.md)
- [**Log**](../../../api/library/common/class.log_cpp.md)
- [**Visualizer**](../../../api/library/engine/class.visualizer_cpp.md)


#### Avoiding Deadlocks


There is a possibility of mutual locking, also known as *deadlock*, on condition that a function of a locked object executes a *callback* function which in turn calls a function of the same locked object.


> **Notice:** To prevent deadlocks you should avoid calling potentially locked objects from their callback functions.


#### Operations with Landscape Terrain


[*ObjectLandscapeTerrain* classes](../../../api/library/objects/landscape_terrain/index.md) contain a set of thread-safe methods intended for fetching landscape data and intersection detection.


<details>
<summary>AppWorldLogic.h | Close</summary>

**AppWorldLogic.h**


```cpp
#include <UnigineLogic.h>
#include <UnigineStreams.h>
#include <UnigineThread.h>

class AppWorldLogic : public Unigine::WorldLogic
{
public:
	AppWorldLogic();
	~AppWorldLogic() override;

	int init() override;
	int shutdown() override;
private:

	Unigine::Vector<Unigine::Thread*> threads;

};


```

</details>


<details>
<summary>AppWorldLogic.cpp | Close</summary>

**AppWorldLogic.cpp**


```cpp
#include "AppWorldLogic.h"
#include <UniginePlayers.h>
#include <UnigineGame.h>
#include <UnigineVisualizer.h>
#include <UnigineObjects.h>
#include <UnigineWorld.h>

using namespace Unigine;
using namespace Math;

class TerrainIntersectionThread : public Thread
{
public:
	TerrainIntersectionThread(PlayerPtr m)
	{
		main_player = m;
	}

	void process() override
	{
		if (!main_player)
			return;
		while (isRunning())
		{

			float x = Game::getRandomFloat(-1000.0f, 1000.0f);
			float y = Game::getRandomFloat(-1000.0f, 1000.0f);

			if (!fetch)
			{
				// create fetch
				fetch = LandscapeFetch::create();

				// set mask
				fetch->setUsesHeight(true);
				fetch->setUsesNormal(true);
				fetch->setUsesAlbedo(true);
				fetch->setUsesMask(0, true);
				fetch->setUsesMask(1, true);
				fetch->setUsesMask(2, true);
				fetch->setUsesMask(3, true);

				fetch->intersectionAsync(Vec3{ x, y, 10000.0f }, Vec3{ x, y, 0.0 }, false);
			}
			else
			{
				if (fetch->isAsyncCompleted())
				{
					if (fetch->isIntersection())
					{
						Vec3 point = fetch->getPosition();
						Visualizer::renderVector(point, point + Vec3_up * 10, vec4_blue);
						Visualizer::renderVector(point, point + Vec3(fetch->getNormal() * 10), vec4_red);
						Visualizer::renderSolidSphere(1, translate(point), vec4_black);

						String string;
						string += String::format("Height : %f\n", fetch->getHeight());

						string += "Masks: \n";

						auto terrain = Landscape::getActiveTerrain();
						for (int i = 0; i < 4; i++)
						{
							// getName() is not thread-safe,
							// do not change the mask name in other threads when getting
							string += String::format(" - \"%s\": %.2f\n", terrain->getDetailMask(i)->getName(), fetch->getMask(i));
						}
						Visualizer::renderMessage3D(point, vec3(1, 1, 0), string.get(), vec4_green, 1);
					}
					else
					{
						Visualizer::renderMessage3D(Vec3(x, y, 0), vec3(1, 1, 0), "Out of terrain", vec4_red, 1);
					}

					fetch->intersectionAsync(Vec3{ x, y, 10000.0f }, Vec3{ x, y, 0.0 }, false);
				}
			}
		}
	}

private:
	LandscapeFetchPtr fetch;
	PlayerPtr main_player;
};

int AppWorldLogic::init()
{

	PlayerPtr main_player = checked_ptr_cast<Player>(World::getNodeByName("main_player"));

	int num_thread = 4;
	for (int i = 0; i < num_thread; ++i)
	{
		Thread* thread = new TerrainIntersectionThread(main_player);
		thread->run();
		threads.push_back(thread);
	}
	Visualizer::setEnabled(true);

	return 1;
}

int AppWorldLogic::shutdown()
{

	for (Thread* thread : threads)
	{
		thread->stop();
		delete thread;
	}

	return 1;
}


```

</details>


#### Intersections with Global Terrain


*[ObjectTerrainGlobal](../../../api/library/objects/class.objectterrainglobal_cpp.md)* contains a set of thread-safe methods intended for some special use cases.


<details>
<summary>AppWorldLogic.h | Close</summary>

**AppWorldLogic.h**


```cpp
#include <UnigineLogic.h>
#include <UnigineStreams.h>
#include <UnigineThread.h>

class AppWorldLogic : public Unigine::WorldLogic
{
public:
	AppWorldLogic();
	~AppWorldLogic() override;

	int init() override;
	int shutdown() override;
private:

	Unigine::Vector<Unigine::Thread*> threads;

};


```

</details>


<details>
<summary>AppWorldLogic.cpp | Close</summary>

**AppWorldLogic.cpp**


```cpp
#include "AppWorldLogic.h"
#include <UniginePlayers.h>
#include <UnigineGame.h>
#include <UnigineVisualizer.h>
#include <UnigineObjects.h>
#include <UnigineWorld.h>

using namespace Unigine;
using namespace Math;

class TerrainIntersectionThread : public Thread
{
public:
	TerrainIntersectionThread(ObjectTerrainGlobalPtr terrain_)
	{
		terrain = terrain_;
		intersection = ObjectIntersection::create();
	}

	void process() override
	{
		while (isRunning())
		{
			float x = Game::getRandomFloat(-1000.0f, 1000.0f);
			float y = Game::getRandomFloat(-1000.0f, 1000.0f);

			int success = terrain->getIntersection(Vec3{ x, y, 10000.0f }, Vec3{ x, y, 0.0 }, intersection, 0);
			if (success)
			{
				const auto intersection_point = intersection->getPoint();
				Log::message("Thread %d: %f %f %f\n", getID(), intersection_point.x, intersection_point.y, intersection_point.z);
			}
		}
	}

private:
	ObjectTerrainGlobalPtr terrain;
	ObjectIntersectionPtr intersection;
};

int AppWorldLogic::init()
{

	const auto terrain = checked_ptr_cast<ObjectTerrainGlobal>(World::getNodeByName("Landscape"));

	int num_thread = 4;
	for (int i = 0; i < num_thread; ++i)
	{
		Thread* thread = new TerrainIntersectionThread(terrain);
		thread->run();
		threads.push_back(thread);
	}

	return 1;
}

int AppWorldLogic::shutdown()
{

	for (Thread* thread : threads)
	{
		thread->stop();
		delete thread;
	}

	return 1;
}


```

</details>


### Main-Loop-Dependent Objects


The *[Node](../../../api/library/nodes/class.node_cpp.md)* class and the [Node-Related classes](../../../api/library/nodes/index.md) are directly involved into threads of the main loop. They don't have synchronization mechanisms provided.


For performance improvements, nodes can be created and loaded in user threads **before being integrated** into the main loop. This includes:


- Creating nodes via the **[API](../../../api/library/nodes/class.node_cpp.md#create_node)**
- Loading node from files using *[World::loadNode()](../../../api/library/engine/class.world_cpp.md#loadNode_cstr_int_Node)*
- The **[AsyncQueue](../../../api/library/filesystem/class.asyncqueue_cpp.md)** class provides methods for asynchronous loading of resources.
- The **[Async](../../../api/library/common/class.async_cpp.md)** class is intended for running background tasks in an asynchronous way.


Nodes can be fully configured and populated with data in the user thread where they were created.


Nodes prepared in background threads **are not automatically added to the engine's main loop**. To make a node participate in rendering, updates, and physics, it must become part of the main loop by calling the *[Node::updateEnabled()](../../../api/library/nodes/class.node_cpp.md#updateEnabled_void)* method from the main thread. Once enabled, the node becomes bound to the main loop, and all further operations (e.g. transforms, property changes, material updates) must be performed from the main thread.


The following example demonstates how to create a node in a separate thread and attach it to the main loop.


<details>
<summary>NodeLoader.h | Close</summary>

```cpp
#pragma once
#include <UnigineComponentSystem.h>
#include <memory>

using namespace Unigine;
using namespace Math;

// A simple component that loads a node in a user thread
class NodeLoader : public ComponentBase
{
public:
	COMPONENT_DEFINE(NodeLoader, ComponentBase)

	COMPONENT_INIT(init);
	COMPONENT_UPDATE(update);
	COMPONENT_SHUTDOWN(shutdown);

private:
	// A thread that loads a node from file in the background
	class UserThread final : public Unigine::Thread
	{
	public:
		UserThread();
		~UserThread();
		NodePtr my_node;			// The node loaded in this thread

	private:
		void process() override;	// The thread main execution function
	};

private:
	void init();
	void update();
	void shutdown();

private:
	std::unique_ptr<UserThread> node_creation_thread;
};

```

</details>


<details>
<summary>NodeLoader.cpp | Close</summary>

```cpp
#include "NodeLoader.h"
#include <UnigineConsole.h>
#include <iostream>
#include <memory>

using namespace Unigine;
using namespace Unigine::Math;

NodeLoader::UserThread::UserThread()  {}
NodeLoader::UserThread::~UserThread() {}

void NodeLoader::UserThread::process()
{
	// Simulate some workload
	sleep(1000);

	//Assume we are loading node "material_ball.node" from "data" folder
	my_node = World::loadNode("material_ball.node");

	// If the node was loaded successfully, set its position
	if (my_node)
	{
		my_node->setWorldPosition(Vec3(0, 0, 0));
	}

	// Additional simulated workload
	sleep(1000);
}

REGISTER_COMPONENT(NodeLoader)

void NodeLoader::init()
{
	// Start the background thread for node loading
	node_creation_thread = std::make_unique<UserThread>();
	node_creation_thread->run();
}

void NodeLoader::update()
{
	// Once the background thread has finished its work
	if (!node_creation_thread->isRunning())
	{
		// Enable the node in the main thread to make it main-loop-dependent
		node_creation_thread->my_node->updateEnabled();
	}
}

void NodeLoader::shutdown()
{
	if (node_creation_thread->isRunning())
	{
		node_creation_thread->stop();
	}
}

```

</details>


The example below shows how to achieve the same behavior using C#


<details>
<summary>NodeLoader.cs | Close</summary>

```csharp
using System.Collections;
using System.Collections.Generic;
using System.Threading;
using Unigine;

// A simple component that loads a node in a user thread
public partial class NodeLoader : Component
{
	// A thread that loads a node from file in the background
	Thread separateNodeCreation;
	Node ball;

	void Init()
	{
		separateNodeCreation = new Thread(() =>
			{
				// Simulate some workload
				Thread.Sleep(2000);

				//Assume we are loading node "material_ball.node" from "data" folder
				ball = World.LoadNode("material_ball.node");
				ball.Position = new dvec3(2.0f, 25.0f, 0.0f);

				// Additional simulated workload
				Thread.Sleep(2000);
			}
		);
		// Start the background thread for node loading
		separateNodeCreation.Start();
	}

	void Update()
	{
		// Once the background thread has finished its work
		if (!separateNodeCreation.IsAlive)
		{
			// Enable the node in the main thread to make it main-loop-dependent
			ball.UpdateEnabled();
		}

	}
}

```

</details>


If you need to modify nodes that are already part of the main loop from a background thread, you must first pause the main loop to avoid conflicts, make your changes, and then resume the loop.


> **Notice:** [GPU-related methods](#gpu_objects) **must always** be called in the main loop.


Thread safety is ensured by synchronization of all **engine's threads** dealing with main-loop-dependent objects with *[Engine::swap()](../../../code/fundamentals/execution_sequence/main_loop.md#swap)*, where delayed deletion of objects is performed. But **user threads** can be executed in parallel with *[Engine::swap()](../../../code/fundamentals/execution_sequence/main_loop.md#swap)* in the main thread, in such cases you **shouldn't perform any manipulations with main-loop dependent objects (such as nodes) during *Engine::swap()*.**


### Main-Loop-Independent Objects


There are also API members which are not involved into the main loop, they don't have synchronization algorithms as well.


You can fully manage such an object in any thread, but please note that if you need to send it to another thread, either the main loop or a user's thread, you have to provide manual synchronization for its data consistency.


For this purpose you are free to use any methods and classes contained in the `include/UnigineThread.h` file or other mechanisms at your discretion.


The following API members are considered to be independent of the main loop threads:


| - [**Blob**](../../../api/library/common/class.blob_cpp.md) - [**Camera**](../../../api/library/rendering/class.camera_cpp.md) - [**Dir**](../../../api/library/filesystem/class.dir_cpp.md) - [**Ellipsoid**](../../../api/library/geodetics/class.ellipsoid_cpp.md) - [**File**](../../../api/library/filesystem/class.file_cpp.md) - [**GameIntersection**](../../../api/library/engine/class.gameintersection_cpp.md) - [**Image**](../../../api/library/common/class.image_cpp.md) - [**Json**](../../../api/library/common/class.json_cpp.md) - [**Mesh**](../../../api/library/rendering/class.mesh_cpp.md) - [**MeshDynamic**](../../../api/library/rendering/class.meshdynamic_cpp.md) - [**ObjectIntersection**](../../../api/library/objects/class.objectintersection_cpp.md) - [**ObjectIntersectionNormal**](../../../api/library/objects/class.objectintersectionnormal_cpp.md) - [**ObjectIntersectionTexCoord**](../../../api/library/objects/class.objectintersectiontexcoord_cpp.md) |  | - [**Path**](../../../api/library/common/class.path_cpp.md) - [**PathRouteIntersection**](../../../api/library/pathfinding/class.pathrouteintersection_cpp.md) - [**PhysicsIntersection**](../../../api/library/physics/class.physicsintersection_cpp.md) - [**PhysicsIntersectionNormal**](../../../api/library/physics/class.physicsintersectionnormal_cpp.md) - [**RegExp**](../../../api/library/common/class.regexp_cpp.md) - [**ShapeContact**](../../../api/library/physics/class.shapecontact_cpp.md) - [**Socket**](../../../api/library/networking/class.socket_cpp.md) - [**Stream**](../../../api/library/common/class.stream_cpp.md) - [**TilesetFile**](../../../api/library/objects/class.tilesetfile_cpp.md) - [**Viewport**](../../../api/library/rendering/class.viewport_cpp.md) - [**WorldIntersection**](../../../api/library/worlds/class.worldintersection_cpp.md) - [**WorldIntersectionNormal**](../../../api/library/worlds/class.worldintersectionnormal_cpp.md) - [**WorldIntersectionTexCoord**](../../../api/library/worlds/class.worldintersectiontexcoord_cpp.md) - [**Xml**](../../../api/library/common/class.xml_cpp.md) |
|---|---|---|


### GPU-Related Objects


Some member methods interact with Graphics API, which is available only in the main loop. Once you need to call a GPU-related function, you have to pass the object to the main loop and perform calling in it.


The [**Rendering-Related**](../../../api/library/rendering/index.md) Classes (e.g. *[MeshDynamic](../../../api/library/rendering/class.meshdynamic_cpp.md)*) should be considered as GPU-related.


Also, the [**Object-Related**](../../../api/library/objects/index.md) Classes have rendering-related methods, such as *[*render()*](../../../api/library/objects/class.object_cpp.md#render_int_int_void)* and other ones.


Below you'll find the source code of the *[dynamic_03](../../../code/uniginescript/samples/objects/dynamic_03.md)* default sample which demonstrates how to create a dynamic mesh by using the Marching Cubes algorithm performed asynchronously.


<details>
<summary>dynamic_03.usc | Close</summary>

**dynamic_03.usc**


```cpp
#include <core/scripts/samples.h>
#include <samples/objects/dynamic_01.h>

/*
 */
Async async_0;
Async async_1;
int size = 32;
float field_0[size * size * size];
float field_1[size * size * size];
int flags_0[size * size * size];
int flags_1[size * size * size];
ObjectMeshDynamic mesh_0;
ObjectMeshDynamic mesh_1;

using Unigine::Samples;

/*
 */
string mesh_material_names[] = ( "objects_mesh_red", "objects_mesh_green", "objects_mesh_blue", "objects_mesh_orange", "objects_mesh_yellow" );

string get_mesh_material(int material) {
	return mesh_material_names[abs(material) % mesh_material_names.size()];
}

/*
 */
void update_thread() {

	while(1) {

		float time = engine.game.getTime();

		// wait async
		if(async_1 == NULL) async_1 = new Async();
		while(async_1 != NULL && async_1.isRunning()) wait;
		if(async_1 == NULL) continue;
		async_1.clearResult();

		// copy mesh
		Mesh mesh = new Mesh();
		mesh_1.getMesh(mesh);
		mesh_0.setMesh(mesh);
		mesh_0.setMaterial(get_mesh_material(1),"*");
		delete mesh;

		// wait async
		if(async_0 == NULL) async_0 = new Async();
		while(async_0 != NULL && async_0.isRunning()) wait;
		if(async_0 == NULL) continue;
		async_0.clearResult();

		// swap buffers
		field_1.swap(field_0);
		flags_1.swap(flags_0);

		// create field
		float angle = sin(time) + 3.0f;
		mat4 transform = rotateZ(time * 25.0f) * scale(vec3(5.0f / size)) * translate(vec3(-size / 2.0f));
		async_0.run(functionid(create_field),field_0.id(),flags_0.id(),size,transform,angle);

		// create mesh
		async_1.run(functionid(marching_cubes),mesh_1,field_1.id(),flags_1.id(),size);

		wait;
	}
}

/*
 */
int init() {

	createInterface("samples/objects/dynamic_03.world");
	engine.render.loadSettings(fullPath("samples/common/world/render.render"));
	createDefaultPlayer(Vec3(30.0f,0.0f,20.0f));
	createDefaultPlane();

	mesh_0 = addToEditor(new ObjectMeshDynamic(OBJECT_DYNAMIC_ALL));
	mesh_0.setWorldTransform(Mat4(scale(vec3(16.0f / size)) * translate(-size / 2.0f,-size / 2.0f,0.0f)));

	mesh_1 = new ObjectMeshDynamic(1);
	mesh_1.setEnabled(0);

	setDescription(format("Async dynamic marching cubes on %dx%dx%d grid",size,size,size));

	thread("update_thread");

	return 1;
}

/*
 */
void shutdown() {

	if(async_0 != NULL) async_0.wait();
	if(async_1 != NULL) async_1.wait();
	return 1;
}


```

</details>


### Multithreaded Rendering (DirectX12 only)


When *[render_multithreaded](../../../code/console/index.md#render_multithreaded)* is enabled (e.g. via [console](../../../code/console/index.md#render_multithreaded) or [API](../../../api/library/rendering/class.render_cpp.md#setMultithreaded_int_void)), surface rendering is distributed across multiple threads to improve performance. This introduces **specific usage restrictions** due to concurrent data access.


You must **avoid modifying properties** that affect surface rendering while the rendering stage is active. This includes render settings such as *[render_distance_scale](../../../code/console/index.md#render_distance_scale)*, material parameters like textures and colors, and object parameters such as node transforms or visibility. Modifying these properties can create **race conditions** between the main thread and rendering threads, possibly leading to unexpected behavior.


To safely modify rendering properties, perform changes from the main thread during *[Engine::update()](../../../code/fundamentals/execution_sequence/main_loop.md#update)* or *[Engine::swap()](../../../code/fundamentals/execution_sequence/main_loop.md#swap)* when rendering threads are idle.


## Threads in UnigineScript


When using UnigineScript workflow, you should also keep in mind that main-loop-dependent objects must not be directly modified out of the main loop. Instead, it is suggested to create a *twin* for such an object which will be modified asynchronously and then swapped with the original object on the *flush* step.


> **Notice:** Non-reentrant UnigineScript functions are not suitable for multithreaded usage. You will have to create a separate function for each thread. For that you can use [Templates](../../../code/uniginescript/language/templates.md).


Below you'll find a UnigineScript sample on managing several mesh clusters asynchronously. You can copy and paste it to the world script file of your project.


<details>
<summary>cluster_03.usc | Close</summary>

**cluster_03.usc**


```cpp
#include <core/unigine.h>
#include <core/scripts/samples.h>

using Unigine::Samples;

#define NUM_CLUSTERS 4
int size = 60;

// a class for asynchronous mesh cluster
class AsyncCluster
{
	public:
	Mat4 transforms[0];
	// original mesh cluster
	ObjectMeshCluster cluster;
	// a twin for async modification
	ObjectMeshCluster cluster_async;
	Async async;
};
AsyncCluster clusters[NUM_CLUSTERS];

string mesh_material_names[] = ( "stress_mesh_red", "stress_mesh_green", "stress_mesh_blue", "stress_mesh_orange", "stress_mesh_yellow" );

string get_mesh_material(int material) {
	return mesh_material_names[abs(material) % mesh_material_names.size()];
}

// a template to generate a function transforming a cluster in each thread
template async_transforms<NUM, OFFSET_X, OFFSET_Y> void async_transforms_ ## NUM(ObjectMeshCluster cluster_async, float transforms[], float time, int size) {

	Vec3 offset = Vec3(OFFSET_X - 0.5f, OFFSET_Y - 0.5f, 0.0f) * (size + 0.5f) * 2;

	int num = 0;
	for(int y = -size; y <= size; y++) {
		for(int x = -size; x <= size; x++) {
			float rand = sin(frac(num * 0.333f) + x * y * (NUM + 1));

			Vec3 pos = (Vec3(x, y, sin(time * rand * 2.0f) + 1.5f) + offset) * 2.0f;
			transforms[num] = translate(pos) * rotateZ(time * 25 * rand);
			num++;
		}
	}

	cluster_async.createMeshes(transforms);
}

async_transforms<0,0,0>;
async_transforms<1,0,1>;
async_transforms<2,1,0>;
async_transforms<3,1,1>;

void update_thread() {

	while(1) {

		// wait async
		for(int i = 0; i < NUM_CLUSTERS; i++) {
			while(clusters[i].async.isRunning())
				wait;
		}

		for(int i = 0; i < NUM_CLUSTERS; i++) {
			AsyncCluster c = clusters[i];

			c.async.clearResult();
			c.cluster.swap(c.cluster_async);
			c.cluster.setEnabled(1);
			c.cluster_async.setEnabled(0);
			c.async.run("async_transforms_" + i, c.cluster_async, c.transforms.id(), engine.game.getTime(), size);
		}

		wait;
	}
}

int init() {
	// create scene
	PlayerSpectator player = new PlayerSpectator();
	player.setPosition(Vec3(30.0f,0.0f,20.0f));
	player.setDirection(vec3(-1.0f, 0.0f, -0.5f));
	engine.game.setPlayer(player);

	for(int i = 0; i < NUM_CLUSTERS; i++) {
		AsyncCluster c = new AsyncCluster();
		c.cluster = new ObjectMeshCluster(fullPath("samples/common/meshes/box.mesh"));
		c.cluster.setMaterial(get_mesh_material(i),"*");
		c.cluster_async = class_append(node_cast(c.cluster.clone()));
		c.async = new Async();
		int num = pow(size * 2 + 1, 2);
		c.transforms.resize(num);
		clusters[i] = c;
	}

	thread("update_thread");

	int num = pow(size * 2 + 1, 2) * NUM_CLUSTERS;
	log.message("ObjectMeshCluster with %d dynamic instances",num);

	return 1;
}

/*
 */
void shutdown() {

	for(int i = 0; i < NUM_CLUSTERS; i++) {
		clusters[i].async.wait();
	}

	return 1;
}


```

</details>
