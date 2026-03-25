# Procedural Meshes (CPP)


**Procedural meshes** are meshes generated at runtime using code and algorithms to define their geometry vertex by vertex. They're useful for things like small updates such as animated arrows or progress indicators in a 3D UI, stretching cables or beams that move every frame, deforming or breaking objects during gameplay, or even populating large scenes with procedurally-generated content (PCG) at runtime.


To create procedural geometry in your world, you can use either **[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)** API or **[ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_cpp.md)** (and related ***[ObjectGuiMesh](../../../api/library/objects/class.objectguimesh_cpp.md)***, ***[DecalMesh](../../../api/library/decals/class.decalmesh_cpp.md)***, ***[ObjectMeshCluster](../../../api/library/objects/class.objectmeshcluster_cpp.md)***, ***[ObjectMeshClutter](../../../api/library/objects/class.objectmeshclutter_cpp.md)***).


> **Notice:** While both **[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)** or **[ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_cpp.md)** can be used in similar ways, **we consider [ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_cpp.md) (and related classes) in the procedural mode is the better choice for procedural geometry generation**, as it offers greater control over memory management and generation performance. However, for cases such as working with [ropes](../../../principles/physics/bodies/rope/index.md) or [cloth](../../../principles/physics/bodies/cloth/index.md), you must use *ObjectMeshDynamic*.


| ![](procedural_sphere.gif) |
|---|


This article provides a detailed overview of procedural geometry, covering different generation modes and their impact on performance, memory usage, and overall efficiency.


> **Notice:** All links provided in this article refer to the **[ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_cpp.md)** class API. However, all methods mentioned here are equally applicable to ***[ObjectGuiMesh](../../../api/library/objects/class.objectguimesh_cpp.md)***, ***[DecalMesh](../../../api/library/decals/class.decalmesh_cpp.md)***, ***[ObjectMeshCluster](../../../api/library/objects/class.objectmeshcluster_cpp.md)***, ***[ObjectMeshClutter](../../../api/library/objects/class.objectmeshclutter_cpp.md)***.


### See Also


C++ samples with different approaches to generating procedural meshes:


-
-


## Procedural Meshes Workflow


The procedural mesh workflow can be divided into **three stages**:


1. **Create a Mesh Object and select procedural mode** - This determines how and where the object will store its data (in RAM, VRAM, or on disk).
2. **Define the logic to update Mesh data** - You can generate mesh data procedurally using algorithms or load pre-built models as input.
3. **Apply new Mesh data to the object** - Choose the appropriate method to apply the data. Pay attention to the differences between methods and select the one that best fits your use case.


### Selecting Procedural Mode


Static meshes support [streaming](../../../principles/data_streaming/index.md), allowing geometry data to be loaded from disk on demand to optimize memory usage. However, when procedural mode is enabled, the streaming behavior varies depending on the selected procedural mode. Some modes retain all geometry data in **RAM and VRAM**, while others enable **disk-based access**. These differences have a **direct impact on both runtime performance and memory consumption**.


Use *[setMeshProceduralMode()](../../../api/library/objects/class.objectmeshstatic_cpp.md#setMeshProceduralMode_int_int_void)* based on the type of geometry being used (whether it is static and requires infrequent updates or is intensively modified and effectively used to create animation-like effects) as well as on the current memory usage of your world. The following modes are available, each with its own characteristics and trade-offs:


| Mode | Description | Memory Usage | Update Speed | Typical Use Case |
|---|---|---|---|---|
| **DISABLE (default)** | Disables procedural mode. No procedural data is stored or managed. | Mesh data is loaded from a file, [streaming](../../../principles/data_streaming/index.md) works as usual. | - | Used for prebuilt meshes that never change at runtime, such as environment or architectural assets. |
| **[DYNAMIC](../../../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE_DYNAMIC)** | Provides the fastest performance, but with the highest RAM and VRAM usage. Meshes are not automatically unloaded, manual memory cleanup is required using *[deleteDynamicMesh()](../../../api/library/objects/class.objectmeshstatic_cpp.md#deleteDynamicMesh_int)*. | The procedural data is stored in RAM and VRAM. Not automatically unloaded. | Fastest | This mode is intended only for a small number of lightweight objects that are updated very frequently. For example water waves in a fountain, destruction effects, or fast-moving game objects whose shape changes continuously. |
| **[BLOB](../../../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE_BLOB)** | In this mode, all procedural data is stored and compressed into the temporary *[Blob](../../../api/library/common/class.blob_cpp.md)*. VRAM and RAM are loaded directly from this Blob. Modifications are faster compared to FILE mode, but at the cost of increased RAM usage. | Procedural data is offloaded to RAM when not in use. | Moderate | Ideal for dynamic geometry where frequent updates are needed but memory efficiency is still a concern. For example, procedurally changing vegetation, destructible surfaces, or reactive environments such as dynamic surface details. |
| **[FILE](../../../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE_FILE)** | In this mode, procedural mesh data is stored as temporary files on disk. Each time a procedural mesh is modified, the corresponding file is updated. This allows the engine to unload both RAM and VRAM when needed, at the cost of slightly lower performance due to disk I/O operations. | Procedural data is offloaded to DISK when not in use. | Slowest | Large procedural meshes that change rarely, like level geometry, where minimizing memory usage is critical. |


Configuration for the **FILE** mode is available through **[`*.boot`](../../../code/configuration_file_cpp.md)** or *[Console](../../../code/console/index.md)*, but only takes effect at engine startup.


- *[mesh_procedural_path](../../../code/console/index.md#mesh_procedural_path)*: defines the path where temporary procedural files are stored.
- *[mesh_procedural_read_only](../../../code/console/index.md#mesh_procedural_read_only)*: disables writing to disk (works as [BLOB](#blob_mode)).


> **Notice:** Disabling procedural mode for a mesh will delete its corresponding file. When multiple engine instances share the same *[mesh_procedural_path](../../../code/console/index.md#mesh_procedural_path)*, this action may remove files that are still in use by other instances.


### Generating Mesh


After selecting the appropriate procedural mode, you can proceed with geometry creation or loading. You can fully define the geometry in code (vertices, indices, surfaces, and other attributes) using the *[Mesh](../../../api/library/rendering/class.mesh_cpp.md)* class API, or reuse predefined assets as input data.


The following example from the **[Procedural Mesh Modification](#see_also)** sample demonstrates creating a wave-like surface from scratch:


<details>
<summary>Creating Wave-like Surface | Close</summary>

```cpp
void ProceduralMeshModifier::update_mesh(MeshPtr mesh)
{
	UNIGINE_PROFILER_FUNCTION;

	float time = Game::getTime();

	// Ensure exactly one surface and clear previous data
	if (mesh->getNumSurfaces() != 1)
	{
		mesh->clear();
		mesh->addSurface("");
	}
	else
	{
		mesh->clearSurface();
	}

	// Generate a grid of vertices with an animated wave
	auto &vertices = mesh->getVertices();
	vertices.reserve(size * size);

	for (int y = 0; y < size; y++)
	{
		float Y = y * isize - 15.0f;
		float Z = cos(Y + time);

		for (int x = 0; x < size; x++)
		{
			float X = x * isize - 15.0f;
			vertices.append(vec3(X, Y, Z * sin(X + time)));
		}
	}

	// Reserve enough memory for indices so vector won't be reallocated
	// every time it's capacity ends
	auto &cindices = mesh->getCIndices();
	cindices.reserve((size - 1) * (size - 1) * 6);
	auto &tindices = mesh->getTIndices();
	tindices.reserve((size - 1) * (size - 1) * 6);

	// Append the same indices to both coordinate and triangle index buffers
	auto addIndex = [&cindices, &tindices](int index) {
		cindices.append(index);
		tindices.append(index);
	};

	// Build triangles for each quad in the grid
	for (int y = 0; y < size - 1; y++)
	{
		int offset = size * y;
		for (int x = 0; x < size - 1; x++)
		{
			addIndex(offset);
			addIndex(offset + 1);
			addIndex(offset + size);
			addIndex(offset + size);
			addIndex(offset + 1);
			addIndex(offset + size + 1);
			offset++;
		}
	}

	mesh->createTangents();

	{
		UNIGINE_PROFILER_SCOPED("CreateCollisionData");

		// If you plan to use intersections or collisions with this mesh,
		// it's recommended to create CollisionData. Otherwise, intersection
		// and collision checks will be highly inefficient.

		if (is_collision_enabled)
		{
			// Creates both Spatial Tree and Edges
			// for effective intersection and collision respectively
			mesh->createCollisionData();

			// If needed, you can create only one:

			// mesh->createSpatialTree();		// intersection only
			// mesh->createEdges();				// collision only
		}
		else
			// You can also create a mesh without CollisionData, or remove existing data
			// if it's not needed.
			// To check whether a mesh has CollisionData, use:
			//		mesh->hasCollisionData();
			//		mesh->hasSpatialTree();
			//		mesh->hasEdges();
			mesh->clearCollisionData();
	}

	// Update bounds after geometry changes
	mesh->createBounds();
}


```

</details>


If the mesh is intended to participate in collision and intersection checks, you must explicitly call *[createCollisionData()](../../../api/library/rendering/class.mesh_cpp.md#createCollisionData_int_int_void)* (or separately *[createSpatialTree()](../../../api/library/rendering/class.mesh_cpp.md#createSpatialTree_int_void)* for intersections, and *[createEdges()](../../../api/library/rendering/class.mesh_cpp.md#createEdges_int_void)* for collisions) after modifying the mesh data and before calling any apply methods. This ensures that the required internal data structures (such as edges and spatial tree) are generated and up to date.


Keep in mind that generating these structures can be time and memory intensive. If the generated mesh is used purely for visual purposes, these structures are not required, and the related operations become unnecessary. Skipping them can significantly speed up the generation process.

 Best PracticeWhen generating a spatial tree, you can adjust its precision and performance by changing the number of triangles stored per leaf node using *[Mesh::setSpatialTreeTriangles()](../../../api/library/rendering/class.mesh_cpp.md#setSpatialTreeTriangles_int_void)*. Lower values increase accuracy but consume more time and memory, while higher values improve performance at the cost of detection precision.
### Applying New Geometry


Procedural mesh data in ObjectMeshStatic can be updated in two primary ways, depending on your control and performance requirements:


- **Simplified Generation API** - for high-level, callback-based generation.
- **Manual Update methods** - for finer control over timing, memory, and threading behavior.


> **Warning:** All procedural mesh update operations **must be executed from the Main Thread**!


#### Simplified Generation


For common procedural workflows, the *[runGenerateMeshProceduralAsync()](../../../api/library/objects/class.objectmeshstatic_cpp.md#runGenerateMeshProceduralAsync_GenerateMeshProcedural_int_int)* and *[runGenerateMeshProceduralForce()](../../../api/library/objects/class.objectmeshstatic_cpp.md#runGenerateMeshProceduralForce_GenerateMeshProcedural_int_int)* methods allow you to schedule mesh generation via callbacks. In your callback, you define how the geometry is built (populate Mesh), and the engine will apply it automatically.


```cpp
ObjectMeshStaticPtr obj = ObjectMeshStatic::create();

// The createMesh function is a minimal procedural example.
// Real implementations usually apply complex mesh generation logic.
void createMesh(MeshPtr mesh)
{
	// Create a simple box surface
	// Usually you have to build/rebuild vertices manually
	mesh->addBoxSurface("box", Math::vec3(1));
}

int AppWorldLogic::init()
{
	// This call will build and apply box surface to a mesh:
	obj->runGenerateMeshProceduralAsync(MakeCallback(&createMesh));
	return 1;
}


```


In case of frequent asynchronous generation, it is recommended to use *[isMeshProceduralDone()](../../../api/library/objects/class.objectmeshstatic_cpp.md#isMeshProceduralDone_int)* and *[isMeshProceduralActive()](../../../api/library/objects/class.objectmeshstatic_cpp.md#isMeshProceduralActive_int)* to check the current mesh state and coordinate updates, preventing race conditions and ensuring deterministic results.


```cpp
int AppWorldLogic::update()
{
	// Always check if the mesh is ready before launching the next async generation.
	if (obj->isMeshProceduralDone())
	{
		obj->runGenerateMeshProceduralAsync(MakeCallback(&createMesh));
	}

	return 1;
}


```


When using the **DirectX 12** graphics API, you can explicitly specify where the MeshRender **indices** and **vertices** are stored using the *mesh_render_flags* attribute or [setting corresponding flags manually](../../../api/library/rendering/class.meshrender_cpp.md#setFlags_int_void).


#### Manual Generation


You can also apply mesh data directly using a set of methods that differ by update strategy. All of them serve the same purpose: **replace the current mesh with new data**. The procedural generation API provides greater flexibility and control over how new geometry is applied.


These methods differ by data transfer type (*copy* or *move*) and execution mode (*force* or *async*). The combination of these two aspects determines how memory is managed and when the operation is performed.


| Transfer Type | Behavior | Typical Use Case |
|---|---|---|
| **Copy** | Duplicates vertex and index data from the source mesh into the object. The source remains unchanged. | When the same mesh data must be reused by multiple objects. |
| **Move** | Swaps mesh data between the object and the given mesh, so the given mesh no longer contains its original vertex data and its contents are replaced. This avoids the cost of copying operations and allows for faster updates. | When you want to avoid extra memory copying and perform faster updates. |
| Execution Mode | Behavior | Typical Use Case |
| **Force** | Executes immediately in the main thread, blocking until finished. | For real-time updates when delay is unacceptable. In [*PROCEDURAL_MODE_DYNAMIC*](../../../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE_DYNAMIC), forced move behaves identically to its asynchronous variant. |
| **Async** | Executes in the background without blocking the main thread. | Useful in [*PROCEDURAL_MODE_FILE*](../../../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE_FILE) or [*PROCEDURAL_MODE_BLOB*](../../../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE_BLOB) modes, where disk I/O or memory streaming can be offloaded. |


Choose the method that matches your needs, e.g. use *[applyCopyMeshProceduralForce()](../../../api/library/objects/class.objectmeshstatic_cpp.md#applyCopyMeshProceduralForce_ConstMesh_int_int)* for an **immediate copy**, or *[applyMoveMeshProceduralAsync()](../../../api/library/objects/class.objectmeshstatic_cpp.md#applyMoveMeshProceduralAsync_Mesh_int_int)* to **transfer** data **without blocking** the main thread.


##### MeshRender Handling in Move-Based Procedural Updates


All **move** methods provide an overload that accepts both *[Mesh](../../../api/library/rendering/class.mesh_cpp.md)* and *[MeshRender](../../../api/library/rendering/class.meshrender_cpp.md)* as arguments, allowing you to create and manage the MeshRender manually.

 Prior Knowledge
The *[Mesh](../../../api/library/rendering/class.mesh_cpp.md)* class represents the *CPU-side* geometry data used for generation, modification, and processing. It contains vertices, indices, surfaces, and other structural information.


The *[MeshRender](../../../api/library/rendering/class.meshrender_cpp.md)* class represents the *GPU-side* data used for rendering. It stores vertex and index buffers in VRAM and is optimized for drawing operations.


When applying new geometry in **move** mode, the MeshRender can either be created automatically by the engine or provided explicitly by the user, depending on the selected overload:


- *[applyMoveMeshProceduralForce(const Ptr<Mesh> & mesh, int mesh_render_flags)](../../../api/library/objects/class.objectmeshstatic_cpp.md#applyMoveMeshProceduralForce_Mesh_int_int)* or *[applyMoveMeshProceduralAsync(const Ptr<Mesh> & mesh, int mesh_render_flags)](../../../api/library/objects/class.objectmeshstatic_cpp.md#applyMoveMeshProceduralAsync_Mesh_int_int)* In this case, the **MeshRender** object and its underlying data **are created and initialized automatically** by the Engine. This may take some time, as it includes allocating buffers and transferring data to VRAM.
- *[applyMoveMeshProceduralForce(const Ptr<Mesh> & mesh, const Ptr<MeshRender> & mesh_vram)](../../../api/library/objects/class.objectmeshstatic_cpp.md#applyMoveMeshProceduralForce_Mesh_MeshRender_int)* or *[applyMoveMeshProceduralAsync(const Ptr<Mesh> & mesh, const Ptr<MeshRender> & mesh_vram)](../../../api/library/objects/class.objectmeshstatic_cpp.md#applyMoveMeshProceduralAsync_Mesh_MeshRender_int)* In this variant, creation and configuration of the **MeshRender** object are the responsibility of the user. This provides full control over its lifetime, flags, and memory usage. [Flags and usage settings](../../../api/library/rendering/class.meshrender_cpp.md#USAGE_DYNAMIC_VERTEX) can be specified when creating the **MeshRender** instance. To upload data from RAM to VRAM, the *[load(const Ptr<ConstMesh> & mesh)](../../../api/library/rendering/class.meshrender_cpp.md#load_ConstMesh_int)* method must be called on the dedicated *[GPU_STREAM](../../../api/library/filesystem/class.asyncqueue_cpp.md#ASYNC_THREAD_GPU_STREAM)* thread (for example, by using *[AsyncQueue](../../../api/library/filesystem/class.asyncqueue_cpp.md)*), which is designed specifically for transferring resources from RAM to VRAM.


## Usage Examples


Let's take a closer look at how each part of the procedural mesh workflow operates in detail. Step by step, we'll examine how to correctly apply geometry manually across different modes depending on your needs.


### Mesh Deformations


The following component example allows you to modify the mesh of any **[ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_cpp.md)** in the scene. When the left mouse button is pressed, the vertices closest to the raycast intersection point will be displaced outward, creating a localized deformation effect:


> **Notice:** This example uses [dynamic mode](#dynamic_mode) for maximum update speed. However, this mode does not perform automatic unloading of data from RAM or VRAM, so memory usage will accumulate if applied to many objects.


![](mesh_deformation.gif)


> **Warning:** This *VertexMover* example is provided for demonstration purposes only. Do **not use** this approach in production projects without **proper validation and optimization**.
>
>
> For instance, if the intersected mesh is extremely complex, iterating over all vertices each frame may cause noticeable stuttering or performance spikes.


<details>
<summary>VertexMover.h</summary>

```cpp
#pragma once
#include <UnigineComponentSystem.h>
#include <UnigineMathLib.h>
#include <UnigineGame.h>

// WARNING: This example is for demonstration purposes only.
// Iterating over all vertices may cause stuttering on complex meshes.
// Do not use this approach in production without proper validation.

using namespace Unigine;
using namespace Math;

// Moves nearby vertices of a static mesh on mouse click.
class VertexMover : public ComponentBase {
public:
    COMPONENT_DEFINE(VertexMover, ComponentBase);
    COMPONENT_UPDATE(update);

    // Radius of influence (in world units)
    PROP_PARAM(Float, radius, 0.5f);

    // Vertex displacement multiplier
    PROP_PARAM(Float, strength, 0.1f);

    // Raycast distance from player
    PROP_PARAM(Float, distance, 50.0f);

private:
    void update();

    // Mesh buffer used for modification
    MeshPtr working_mesh = Mesh::create();

    // Stores intersection data
    Unigine::WorldIntersectionPtr intersection = Unigine::WorldIntersection::create();
};

```

</details>


<details>
<summary>VertexMover.cpp</summary>

```cpp
#include "VertexMover.h"

using namespace Unigine;
using namespace Math;

REGISTER_COMPONENT(VertexMover);

// WARNING: This example is for demonstration purposes only.
// Iterating over all vertices may cause stuttering on complex meshes.
// Do not use this approach in production without proper validation.

void VertexMover::update()
{
	// Mouse check
	if (!Input::isMouseButtonPressed(Input::MOUSE_BUTTON_LEFT))
	{
		return;
	}

	// Intersection setup
	Math::ivec2 mouse = Input::getMousePosition();
	Vec3 p0 = Game::getPlayer()->getWorldPosition();
	Vec3 dir = Vec3(Game::getPlayer()->getDirectionFromMainWindow(mouse.x, mouse.y));
	Vec3 p1 = p0 + dir * distance;

	// Raycast intersection
	ObjectPtr obj = World::getIntersection(p0, p1, 1, intersection);
	if (!obj || obj->getType() != Node::OBJECT_MESH_STATIC)
	{
		return;
	}

	// Setting up static mesh for procedural modification
	ObjectMeshStaticPtr mesh_object = static_ptr_cast<ObjectMeshStatic>(obj);
	mesh_object->setMeshProceduralMode(ObjectMeshStatic::PROCEDURAL_MODE_DYNAMIC);
	working_mesh = mesh_object->getMeshDynamicRAM();

	// Convert hit coordinates to local mesh space
	Mat4 inv_wt = inverse(mesh_object->getWorldTransform());
	Vec3 hit_local = inv_wt * intersection->getPoint();

	float r2 = radius * radius;

	// Iterate over all vertices and apply displacement
	int vertex_count = working_mesh->getNumVertex(0);
	for (int i = 0; i < vertex_count; i++)
	{
		Vec3 v = Vec3(working_mesh->getVertex(i));
		Vec3 dv = Vec3(v - hit_local);
		float d2 = dot(dv, dv);
		if (d2 >= r2)
			continue;

		float dist = Math::sqrt(d2);
		float falloff = 1.0f - dist / radius;
		Vec3 dir = dv / dist;

		v += dir * strength * falloff;
		working_mesh->setVertex(i, vec3(v));
	}

	// Recreate collision data and bounds
	working_mesh->clearCollisionData();
	working_mesh->createCollisionData();
	working_mesh->createBounds();

	// Apply modified mesh to the object
	mesh_object->applyMoveMeshProceduralForce(working_mesh, MeshRender::USAGE_DYNAMIC_ALL);
}

```

</details>


### Procedural Mesh Modification Sample


Procedural Mesh Modification provides all possible ways to **apply** new geometry to an object. To explore it yourself, [download the sample](../../../sdk/index.md#samples) from the SDK Browser, where you can switch modes and states at runtime to see the differences firsthand.


![](procedural_waves.gif)

*Procedural Mesh Modification Sample*


1. **Initialization** First, all working objects are created: a mesh in RAM for geometry generation, a mesh in VRAM for rendering, and a visible ObjectMeshStatic. The procedural mode is enabled, which defines how and where data will be stored. ```cpp void ProceduralMeshModifier::init() { is_deleted = false; updated_meshvram_manual = is_meshvram_manual; isize = 30.f / size; // Prepare RAM/VRAM mesh objects and the scene object mesh_ram = Mesh::create(); mesh_vram = MeshRender::create(); object = ObjectMeshStatic::create(); object->setMeshProceduralMode(current_mode); object->setWorldPosition(Vec3_one); } ```
2. **Update Cycle** Each frame the update function checks if generation is already in progress. If the procedural mode has changed, the object is recreated. Depending on the configuration, geometry is built either in a background thread (async) or directly on the main thread. ```cpp void ProceduralMeshModifier::update() { UNIGINE_PROFILER_FUNCTION; // Skip if an update/apply is already running if (is_running || object->isMeshProceduralActive()) return; is_running = true; is_meshvram_manual = updated_meshvram_manual; // Recreate object if procedural mode changed if (object->getMeshProceduralMode() != current_mode) { object.deleteLater(); object = ObjectMeshStatic::create(); object->setMeshProceduralMode(current_mode); object->setWorldPosition(Vec3_one); } // Choose where to build the mesh: background thread (async) or main thread if (is_thread_async) { // Builds the mesh on a background thread without blocking the main thread. // Mesh modifications are processed on a separate thread as long as needed, // without impacting performance. AsyncQueue::runAsync(AsyncQueue::ASYNC_THREAD_BACKGROUND, MakeCallback(this, &ProceduralMeshModifier::async_update_ram)); } else { // Build and apply in this frame on the main thread update_ram(); if (is_meshvram_manual) update_vram(); apply_data(); } } ```
3. **Mesh Generation** This is where the new geometry is actually created. An algorithm builds a simple grid, animated using sine and cosine functions to form a wave. Indices are then added to connect the vertices into triangles. Optional collision data and updated bounds are created at the end. <details> <summary>Details</summary> ```cpp void ProceduralMeshModifier::update_mesh(MeshPtr mesh) { UNIGINE_PROFILER_FUNCTION; float time = Game::getTime(); // Ensure exactly one surface and clear previous data if (mesh->getNumSurfaces() != 1) { mesh->clear(); mesh->addSurface(""); } else { mesh->clearSurface(); } // Generate a grid of vertices with an animated wave auto &vertices = mesh->getVertices(); vertices.reserve(size * size); for (int y = 0; y < size; y++) { float Y = y * isize - 15.0f; float Z = cos(Y + time); for (int x = 0; x < size; x++) { float X = x * isize - 15.0f; vertices.append(vec3(X, Y, Z * sin(X + time))); } } // Reserve enough memory for indices so vector won't be reallocated // every time it's capacity ends auto &cindices = mesh->getCIndices(); cindices.reserve((size - 1) * (size - 1) * 6); auto &tindices = mesh->getTIndices(); tindices.reserve((size - 1) * (size - 1) * 6); // Append the same indices to both coordinate and triangle index buffers auto addIndex = [&cindices, &tindices](int index) { cindices.append(index); tindices.append(index); }; // Build triangles for each quad in the grid for (int y = 0; y < size - 1; y++) { int offset = size * y; for (int x = 0; x < size - 1; x++) { addIndex(offset); addIndex(offset + 1); addIndex(offset + size); addIndex(offset + size); addIndex(offset + 1); addIndex(offset + size + 1); offset++; } } mesh->createTangents(); { UNIGINE_PROFILER_SCOPED("CreateCollisionData"); // If you plan to use intersections or collisions with this mesh, // it's recommended to create CollisionData. Otherwise, intersection // and collision checks will be highly inefficient. if (is_collision_enabled) { // Creates both Spatial Tree and Edges // for effective intersection and collision respectively mesh->createCollisionData(); // If needed, you can create only one: // mesh->createSpatialTree();		// intersection only // mesh->createEdges();				// collision only } else // You can also create a mesh without CollisionData, or remove existing data // if it's not needed. // To check whether a mesh has CollisionData, use: //		mesh->hasCollisionData(); //		mesh->hasSpatialTree(); //		mesh->hasEdges(); mesh->clearCollisionData(); } // Update bounds after geometry changes mesh->createBounds(); } ``` </details>
4. **RAM and VRAM Updates** Once the way to build a geometry is defined, it can be called to update RAM and VRAM mesh data. ```cpp void ProceduralMeshModifier::update_ram() { UNIGINE_PROFILER_FUNCTION; // Return if the main thread side is shutting down if (is_deleted.fetch()) return; // Lock mesh_ram so other threads won't interfere mesh update ScopedLock sl(mesh_lock); update_mesh(mesh_ram); } void ProceduralMeshModifier::update_vram() { UNIGINE_PROFILER_FUNCTION; // Return if the main thread side is shutting down if (is_deleted.fetch()) return; // Upload RAM mesh to VRAM mesh ScopedLock sl(mesh_lock); mesh_vram->load(mesh_ram); } ```
5. **Asynchronous Operations (optional)** Asynchronous versions of the update functions run on background or GPU threads and then return control to the main thread when the mesh is ready. ```cpp void ProceduralMeshModifier::async_update_ram() { // Build RAM mesh update_ram(); if (is_meshvram_manual) { // Load MeshRender on the GPU Stream thread when doing it manually AsyncQueue::runAsync(AsyncQueue::ASYNC_THREAD_GPU_STREAM, MakeCallback(this, &ProceduralMeshModifier::async_update_vram)); } else { // If you don't need to load MeshRender manualy and automatic loading inside // apllyMeshProcedural methods is enough, then return to Main thread AsyncQueue::runAsync(AsyncQueue::ASYNC_THREAD_MAIN, MakeCallback([this, check = node]() { // Check that sample's logic on Main thread is still alive. If it's not then stop // modification and return if (!check || check.isDeleted()) return; apply_data(); })); } } void ProceduralMeshModifier::async_update_vram() { // Update MeshRender update_vram(); // Return to Main thread to apply new mesh AsyncQueue::runAsync(AsyncQueue::ASYNC_THREAD_MAIN, MakeCallback([this, check = node]() { // Check that sample's logic on Main thread is still alive. If it's not then stop // modification and return if (!check || check.isDeleted()) return; apply_data(); })); } ```
6. **Apply Mesh Data** Finally, the generated mesh is applied to the object. Copy modes duplicate data; move modes transfer it directly for better performance. Asynchronous and force variants define whether the main thread is blocked during application. ```cpp // Apply procedural mesh only on the main thread! void ProceduralMeshModifier::apply_data() { UNIGINE_PROFILER_FUNCTION; // In async mode, apply is processed on a separate thread without blocking the main thread. if (is_async_mode) { if (is_meshvram_manual) { // Manual MeshRender is supported only with "Move" mode object->applyMoveMeshProceduralAsync(mesh_ram, mesh_vram); } else { if (is_copy_mode) // In "Copy" mode, data from mesh_ram is duplicated for internal use, // while mesh_ram itself remains unchanged. object->applyCopyMeshProceduralAsync(mesh_ram, current_mesh_render_flag); else // In "Move" mode, data is taken from mesh_ram for internal use, // which modifies mesh_ram in the process. object->applyMoveMeshProceduralAsync(mesh_ram, current_mesh_render_flag); } } // In force mode, the main thread remains blocked until apply has finished. else { if (is_meshvram_manual) { object->applyMoveMeshProceduralForce(mesh_ram, mesh_vram); } else { if (is_copy_mode) object->applyCopyMeshProceduralForce(mesh_ram, current_mesh_render_flag); else object->applyMoveMeshProceduralForce(mesh_ram, current_mesh_render_flag); } } // Full cycle of mesh modification is finished is_running = false; } ```
