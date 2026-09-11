# Procedural Meshes (CS)


**Procedural meshes** are meshes generated at runtime using code and algorithms to define their geometry vertex by vertex. They're useful for things like small updates such as animated arrows or progress indicators in a 3D UI, stretching cables or beams that move every frame, deforming or breaking objects during gameplay, or even populating large scenes with procedurally-generated content (PCG) at runtime.


To create procedural geometry in your world, you can use either **[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md)** API or **[ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_cs.md)** (and related ***[ObjectGuiMesh](../../../api/library/objects/class.objectguimesh_cs.md)***, ***[DecalMesh](../../../api/library/decals/class.decalmesh_cs.md)***, ***[ObjectMeshCluster](../../../api/library/objects/class.objectmeshcluster_cs.md)***, ***[ObjectMeshClutter](../../../api/library/objects/class.objectmeshclutter_cs.md)***).


> **Notice:** While both **[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md)** or **[ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_cs.md)** can be used in similar ways, **we consider [ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_cs.md) (and related classes) in the procedural mode is the better choice for procedural geometry generation**, as it offers greater control over memory management and generation performance. However, for cases such as working with [ropes](../../../principles/physics/bodies/rope/index.md) or [cloth](../../../principles/physics/bodies/cloth/index.md), you must use *ObjectMeshDynamic*.


| ![](procedural_sphere.gif) |
|---|


This article provides a detailed overview of procedural geometry, covering different generation modes and their impact on performance, memory usage, and overall efficiency.


> **Notice:** All links provided in this article refer to the **[ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_cs.md)** class API. However, all methods mentioned here are equally applicable to ***[ObjectGuiMesh](../../../api/library/objects/class.objectguimesh_cs.md)***, ***[DecalMesh](../../../api/library/decals/class.decalmesh_cs.md)***, ***[ObjectMeshCluster](../../../api/library/objects/class.objectmeshcluster_cs.md)***, ***[ObjectMeshClutter](../../../api/library/objects/class.objectmeshclutter_cs.md)***.


### See Also


C# Component samples with different approaches to generating procedural meshes:


-
-


## Procedural Meshes Workflow


The procedural mesh workflow can be divided into **three stages**:


1. **Create a Mesh Object and select procedural mode** - This determines how and where the object will store its data (in RAM, VRAM, or on disk).
2. **Define the logic to update Mesh data** - You can generate mesh data procedurally using algorithms or load pre-built models as input.
3. **Apply new Mesh data to the object** - Choose the appropriate method to apply the data. Pay attention to the differences between methods and select the one that best fits your use case.


### Selecting Procedural Mode


Static meshes support [streaming](../../../principles/data_streaming/index.md), allowing geometry data to be loaded from disk on demand to optimize memory usage. However, when procedural mode is enabled, the streaming behavior varies depending on the selected procedural mode. Some modes retain all geometry data in **RAM and VRAM**, while others enable **disk-based access**. These differences have a **direct impact on both runtime performance and memory consumption**.


Use *[MeshProceduralMode](../../../api/library/objects/class.objectmeshstatic_cs.md#setMeshProceduralMode_int_int_void)* based on the type of geometry being used (whether it is static and requires infrequent updates or is intensively modified and effectively used to create animation-like effects) as well as on the current memory usage of your world. The following modes are available, each with its own characteristics and trade-offs:


| Mode | Description | Memory Usage | Update Speed | Typical Use Case |
|---|---|---|---|---|
| **DISABLE (default)** | Disables procedural mode. No procedural data is stored or managed. | Mesh data is loaded from a file, [streaming](../../../principles/data_streaming/index.md) works as usual. | - | Used for prebuilt meshes that never change at runtime, such as environment or architectural assets. |
| **[DYNAMIC](../../../api/library/objects/class.objectmeshstatic_cs.md#PROCEDURAL_MODE_DYNAMIC)** | Provides the fastest performance, but with the highest RAM and VRAM usage. Meshes are not automatically unloaded, manual memory cleanup is required using *[DeleteDynamicMesh()](../../../api/library/objects/class.objectmeshstatic_cs.md#deleteDynamicMesh_int)*. | The procedural data is stored in RAM and VRAM. Not automatically unloaded. | Fastest | This mode is intended only for a small number of lightweight objects that are updated very frequently. For example water waves in a fountain, destruction effects, or fast-moving game objects whose shape changes continuously. |
| **[BLOB](../../../api/library/objects/class.objectmeshstatic_cs.md#PROCEDURAL_MODE_BLOB)** | In this mode, all procedural data is stored and compressed into the temporary *[Blob](../../../api/library/common/class.blob_cs.md)*. VRAM and RAM are loaded directly from this Blob. Modifications are faster compared to FILE mode, but at the cost of increased RAM usage. | Procedural data is offloaded to RAM when not in use. | Moderate | Ideal for dynamic geometry where frequent updates are needed but memory efficiency is still a concern. For example, procedurally changing vegetation, destructible surfaces, or reactive environments such as dynamic surface details. |
| **[FILE](../../../api/library/objects/class.objectmeshstatic_cs.md#PROCEDURAL_MODE_FILE)** | In this mode, procedural mesh data is stored as temporary files on disk. Each time a procedural mesh is modified, the corresponding file is updated. This allows the engine to unload both RAM and VRAM when needed, at the cost of slightly lower performance due to disk I/O operations. | Procedural data is offloaded to DISK when not in use. | Slowest | Large procedural meshes that change rarely, like level geometry, where minimizing memory usage is critical. |


Configuration for the **FILE** mode is available through **[`*.boot`](../../../code/configuration_file_cs.md)** or *[Console](../../../code/console/index.md)*, but only takes effect at engine startup.


- *[mesh_procedural_path](../../../code/console/index.md#mesh_procedural_path)*: defines the path where temporary procedural files are stored.
- *[mesh_procedural_read_only](../../../code/console/index.md#mesh_procedural_read_only)*: disables writing to disk (works as [BLOB](#blob_mode)).


> **Notice:** Disabling procedural mode for a mesh will delete its corresponding file. When multiple engine instances share the same *[mesh_procedural_path](../../../code/console/index.md#mesh_procedural_path)*, this action may remove files that are still in use by other instances.


### Generating Mesh


After selecting the appropriate procedural mode, you can proceed with geometry creation or loading. You can fully define the geometry in code (vertices, indices, surfaces, and other attributes) using the *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* class API, or reuse predefined assets as input data.


The following example from the **[Procedural Mesh Modification](#see_also)** sample demonstrates creating a wave-like surface from scratch:


<details>
<summary>Creating Wave-like Surface | Close</summary>

```csharp
private void UpdateMesh(Mesh mesh)
{
	int id = Profiler.BeginMicro("ProceduralMeshModifier.UpdateMesh");

	float time = Game.Time;

	// Ensure exactly one surface and clear previous data
	if (mesh.NumSurfaces != 1)
	{
		mesh.Clear();
		mesh.AddSurface("");
	}
	else
	{
		mesh.ClearSurface();
	}

	// Generate a grid of vertices with an animated wave
	var vertices = new vec3[size * size];

	for (int y = 0; y < size; y++)
	{
		float Y = y * isize - 15.0f;
		float Z = MathLib.Cos(Y + time);

		for (int x = 0; x < size; x++)
		{
			float X = x * isize - 15.0f;
			vertices[y * size + x] = (new vec3(X, Y, Z * MathLib.Sin(X + time)));
		}
	}

	mesh.AddVertex(vertices);

	// Reserve enough memory for indices so vector won't be reallocated
	// every time it's capacity ends
	var cindices = new List<int>();
	cindices.Capacity = (size - 1) * (size - 1) * 6;
	var tindices = new List<int>();
	tindices.Capacity = (size - 1) * (size - 1) * 6;

	// Append the same indices to both coordinate and triangle index buffers
	var addIndex = (int index) =>
	{
		cindices.Add(index);
		tindices.Add(index);
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

	mesh.AddCIndices(cindices.ToArray());
	mesh.AddTIndices(tindices.ToArray());

	cindices.Clear();
	tindices.Clear();

	mesh.CreateTangents();

	{
		int idScope = Profiler.BeginMicro("CreateCollisionData");

		// If you plan to use intersections or collisions with this mesh,
		// it's recommended to create CollisionData. Otherwise, intersection
		// and collision checks will be highly inefficient.
		if (isCollisionEnabled)
		{
			// Creates both Spatial Tree and Edges
			// for effective intersection and collision respectively
			mesh.CreateCollisionData();

			// If needed, you can create only one:

			// mesh.CreateSpatialTree();		// intersection only
			// mesh.CreateEdges();				// collision only
		}
		else
			// You can also create a mesh without CollisionData, or remove existing data
			// if it�s not needed.
			// To check whether a mesh has CollisionData, use:
			//		mesh.HasCollisionData();
			//		mesh.HasSpatialTree();
			//		mesh.HasEdges();
			mesh.ClearCollisionData();

		Profiler.EndMicro(idScope);
	}

	// Update bounds after geometry changes
	mesh.CreateBounds();

	Profiler.EndMicro(id);
}


```

</details>


If the mesh is intended to participate in collision and intersection checks, you must explicitly call *[CreateCollisionData()](../../../api/library/rendering/class.mesh_cs.md#createCollisionData_int_int_void)* (or separately *[CreateSpatialTree](../../../api/library/rendering/class.mesh_cs.md#createSpatialTree_int_void)* for intersections, and *[CreateEdges()](../../../api/library/rendering/class.mesh_cs.md#createEdges_int_void)* for collisions) after modifying the mesh data and before calling any apply methods. This ensures that the required internal data structures (such as edges and spatial tree) are generated and up to date.


Keep in mind that generating these structures can be time and memory intensive. If the generated mesh is used purely for visual purposes, these structures are not required, and the related operations become unnecessary. Skipping them can significantly speed up the generation process.

 Best PracticeWhen generating a spatial tree, you can adjust its precision and performance by changing the number of triangles stored per leaf node using *[Mesh.SpatialTreeTriangles](../../../api/library/rendering/class.mesh_cs.md#setSpatialTreeTriangles_int_void)*. Lower values increase accuracy but consume more time and memory, while higher values improve performance at the cost of detection precision.
### Applying New Geometry


Procedural mesh data in ObjectMeshStatic can be updated in two primary ways, depending on your control and performance requirements:


- **Simplified Generation API** - for high-level, callback-based generation.
- **Manual Update methods** - for finer control over timing, memory, and threading behavior.


> **Warning:** All procedural mesh update operations **must be executed from the Main Thread**!


#### Simplified Generation


For common procedural workflows, the *[RunGenerateMeshProceduralAsync()](../../../api/library/objects/class.objectmeshstatic_cs.md#runGenerateMeshProceduralAsync_GenerateMeshProcedural_int_int)* and *[runGenerateMeshProceduralForce()](../../../api/library/objects/class.objectmeshstatic_cs.md#runGenerateMeshProceduralForce_GenerateMeshProcedural_int_int)* methods allow you to schedule mesh generation via callbacks. In your callback, you define how the geometry is built (populate Mesh), and the engine will apply it automatically.


```csharp
ObjectMeshStatic obj = new ObjectMeshStatic();

    // The createMesh function is a minimal procedural example.
    // Real implementations usually apply complex mesh generation logic.
    void CreateMesh(Mesh mesh)
{
        // Create a simple box surface
        // Usually you have to build/rebuild vertices manually
        mesh.AddBoxSurface("box", vec3.ONE);
}

void Init()
{
        // This call will build and apply box surface to a mesh:
        obj.RunGenerateMeshProceduralAsync(CreateMesh);
}


```


In case of frequent asynchronous generation, it is recommended to use *[IsMeshProceduralDone](../../../api/library/objects/class.objectmeshstatic_cs.md#isMeshProceduralDone_int)* and *[IsMeshProceduralActive](../../../api/library/objects/class.objectmeshstatic_cs.md#isMeshProceduralActive_int)* to check the current mesh state and coordinate updates, preventing race conditions and ensuring deterministic results.


```csharp
void Update()
{
        // Always check if the mesh is ready before launching the next async generation.
        if (obj.IsMeshProceduralDone)
        {
            obj.RunGenerateMeshProceduralAsync(CreateMesh);
        }
    }
}


```


When using the **DirectX 12** graphics API, you can explicitly specify where the MeshRender **indices** and **vertices** are stored using the *mesh_render_flags* attribute or [setting corresponding flags manually](../../../api/library/rendering/class.meshrender_cs.md#setFlags_int_void).


#### Manual Generation


You can also apply mesh data directly using a set of methods that differ by update strategy. All of them serve the same purpose: **replace the current mesh with new data**. The procedural generation API provides greater flexibility and control over how new geometry is applied.


These methods differ by data transfer type (*copy* or *move*) and execution mode (*force* or *async*). The combination of these two aspects determines how memory is managed and when the operation is performed.


| Transfer Type | Behavior | Typical Use Case |
|---|---|---|
| **Copy** | Duplicates vertex and index data from the source mesh into the object. The source remains unchanged. | When the same mesh data must be reused by multiple objects. |
| **Move** | Swaps mesh data between the object and the given mesh, so the given mesh no longer contains its original vertex data and its contents are replaced. This avoids the cost of copying operations and allows for faster updates. | When you want to avoid extra memory copying and perform faster updates. |
| Execution Mode | Behavior | Typical Use Case |
| **Force** | Executes immediately in the main thread, blocking until finished. | For real-time updates when delay is unacceptable. In [*PROCEDURAL_MODE_DYNAMIC*](../../../api/library/objects/class.objectmeshstatic_cs.md#PROCEDURAL_MODE_DYNAMIC), forced move behaves identically to its asynchronous variant. |
| **Async** | Executes in the background without blocking the main thread. | Useful in [*PROCEDURAL_MODE_FILE*](../../../api/library/objects/class.objectmeshstatic_cs.md#PROCEDURAL_MODE_FILE) or [*PROCEDURAL_MODE_BLOB*](../../../api/library/objects/class.objectmeshstatic_cs.md#PROCEDURAL_MODE_BLOB) modes, where disk I/O or memory streaming can be offloaded. |


Choose the method that matches your needs, e.g. use *[applyCopyMeshProceduralForce()](../../../api/library/objects/class.objectmeshstatic_cs.md#applyCopyMeshProceduralForce_ConstMesh_int_int)* for an **immediate copy**, or *[applyMoveMeshProceduralAsync()](../../../api/library/objects/class.objectmeshstatic_cs.md#applyMoveMeshProceduralAsync_Mesh_int_int)* to **transfer** data **without blocking** the main thread.


##### MeshRender Handling in Move-Based Procedural Updates


All **move** methods provide an overload that accepts both *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* and *[MeshRender](../../../api/library/rendering/class.meshrender_cs.md)* as arguments, allowing you to create and manage the MeshRender manually.

 Prior Knowledge
The *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* class represents the *CPU-side* geometry data used for generation, modification, and processing. It contains vertices, indices, surfaces, and other structural information.


The *[MeshRender](../../../api/library/rendering/class.meshrender_cs.md)* class represents the *GPU-side* data used for rendering. It stores vertex and index buffers in VRAM and is optimized for drawing operations.


When applying new geometry in **move** mode, the MeshRender can either be created automatically by the engine or provided explicitly by the user, depending on the selected overload:


- *[ApplyMoveMeshProceduralForce(Mesh mesh, int mesh_render_flags)](../../../api/library/objects/class.objectmeshstatic_cs.md#applyMoveMeshProceduralForce_Mesh_int_int)* or *[ApplyMoveMeshProceduralAsync(Mesh mesh, int mesh_render_flags)](../../../api/library/objects/class.objectmeshstatic_cs.md#applyMoveMeshProceduralAsync_Mesh_int_int)* In this case, the **MeshRender** object and its underlying data **are created and initialized automatically** by the Engine. This may take some time, as it includes allocating buffers and transferring data to VRAM.
- *[ApplyMoveMeshProceduralForce(Mesh mesh_ram, MeshRender mesh_vram)](../../../api/library/objects/class.objectmeshstatic_cs.md#applyMoveMeshProceduralForce_Mesh_MeshRender_int)* or *[ApplyMoveMeshProceduralAsync(Mesh mesh_ram, MeshRender mesh_vram)](../../../api/library/objects/class.objectmeshstatic_cs.md#applyMoveMeshProceduralAsync_Mesh_MeshRender_int)* In this variant, creation and configuration of the **MeshRender** object are the responsibility of the user. This provides full control over its lifetime, flags, and memory usage. [Flags and usage settings](../../../api/library/rendering/class.meshrender_cs.md#USAGE_DYNAMIC_VERTEX) can be specified when creating the **MeshRender** instance. To upload data from RAM to VRAM, the *[Load(Mesh mesh)](../../../api/library/rendering/class.meshrender_cs.md#load_ConstMesh_int)* method must be called on the dedicated *[GPU_STREAM](../../../api/library/filesystem/class.asyncqueue_cs.md#ASYNC_THREAD_GPU_STREAM)* thread (for example, by using *[AsyncQueue](../../../api/library/filesystem/class.asyncqueue_cs.md)*), which is designed specifically for transferring resources from RAM to VRAM.


## Usage Examples


Let's take a closer look at how each part of the procedural mesh workflow operates in detail. Step by step, we'll examine how to correctly apply geometry manually across different modes depending on your needs.


### Mesh Deformations


The following component example allows you to modify the mesh of any **[ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_cs.md)** in the scene. When the left mouse button is pressed, the vertices closest to the raycast intersection point will be displaced outward, creating a localized deformation effect:


> **Notice:** This example uses [dynamic mode](#dynamic_mode) for maximum update speed. However, this mode does not perform automatic unloading of data from RAM or VRAM, so memory usage will accumulate if applied to many objects.


![](mesh_deformation.gif)


> **Warning:** This *VertexMover* example is provided for demonstration purposes only. Do **not use** this approach in production projects without **proper validation and optimization**.
>
>
> For instance, if the intersected mesh is extremely complex, iterating over all vertices each frame may cause noticeable stuttering or performance spikes.


<details>
<summary>VertexMover.cs</summary>

```csharp
using System.Collections;
using System.Collections.Generic;
using Unigine;

// WARNING: This example is for demonstration purposes only.
// Iterating over all vertices may cause stuttering on complex meshes.
// Do not use this approach in production without proper validation.

// Support for both single and double precision math configurations
#region Math Variables
#if UNIGINE_DOUBLE
	using Vec3 = Unigine.dvec3;
	using Mat4 = Unigine.dmat4;
#else
	using Vec3 = Unigine.vec3;
	using Mat4 = Unigine.mat4;
#endif
#endregion
 // <-- this line is generated automatically for a new component
public partial class VertexMover : Component
{
	public float radius = 0.5f;				// Area of effect around the hit point
	public float strength = 0.5f;			// Displacement strength for affected vertices

	private Mesh workingMesh = new Mesh();	// Mesh copy to modify in RAM

	void Update()
	{
		// Only run when the left mouse button is pressed
		if (!Input.IsMouseButtonPressed(Input.MOUSE_BUTTON.LEFT))
			return;

		// Define a ray from the player's position through the mouse cursor
		ivec2 mouse = Input.MousePosition;
		Vec3 rayOrigin = (Vec3)Game.Player.WorldPosition;
		Vec3 rayDir = Game.Player.GetDirectionFromMainWindow(mouse.x, mouse.y);
		Vec3 rayEnd = rayOrigin + rayDir * 50.0f;

		// Perform raycast to find intersection with a mesh object
		WorldIntersectionNormal hit = new WorldIntersectionNormal();
		Unigine.Object hitObj = World.GetIntersection(rayOrigin, rayEnd, 1, hit);
		ObjectMeshStatic hitMesh = hitObj as ObjectMeshStatic;
		if (hitMesh == null)
			return;

		// Create a modifiable copy of the mesh in RAM
		hitMesh.SetMeshProceduralMode(ObjectMeshStatic.PROCEDURAL_MODE.DYNAMIC);
		workingMesh = hitMesh.GetMeshDynamicRAM();

		// Convert hit point from world space to local mesh space
		Mat4 invWT = MathLib.Inverse(hitMesh.WorldTransform);
		Vec3 hitLocal = MathLib.Mul(invWT, hit.Point);

		float r2 = radius * radius;

		// Iterate through all vertices of the mesh
		int vertexCount = workingMesh.GetNumVertex(0);
		for (int i = 0; i < vertexCount; i++)
		{
			Vec3 v = workingMesh.GetVertex(i);
			Vec3 dv = v - hitLocal;
			double d2 = MathLib.Dot(dv, dv);
			if (d2 >= r2)
				continue;

			double dist = MathLib.Sqrt(d2);
			double falloff = 1.0f - dist / radius;
			Vec3 dir = (Vec3)(dv / dist);

			v += (Vec3)(dir * strength * falloff);
			workingMesh.SetVertex(i, (Unigine.vec3)v);
		}

		// Recalculate mesh properties for proper rendering and collision
		workingMesh.ClearCollisionData();

		workingMesh.CreateCollisionData();
		workingMesh.CreateBounds();

		// Apply modified mesh back to the object
		hitMesh.ApplyMoveMeshProceduralForce(workingMesh, MeshRender.USAGE_DYNAMIC_ALL);
	}
}

```

</details>


### Procedural Mesh Modification Sample


Procedural Mesh Modification provides all possible ways to **apply** new geometry to an object. To explore it yourself, [download the sample](../../../sdk/index.md#samples) from the SDK Browser, where you can switch modes and states at runtime to see the differences firsthand.


![](procedural_waves.gif)

*Procedural Mesh Modification Sample*


1. **Initialization** First, all working objects are created: a mesh in RAM for geometry generation, a mesh in VRAM for rendering, and a visible ObjectMeshStatic. The procedural mode is enabled, which defines how and where data will be stored. ```csharp void Init() { isDeleted = false; updatedMeshvramManual = isMeshvramManual; isize = 30.0f / size; // Prepare RAM/VRAM mesh objects and the scene object meshRAM = new Mesh(); meshVRAM = new MeshRender(); objectMesh = new ObjectMeshStatic(); objectMesh.SetMeshProceduralMode(currentMode); objectMesh.WorldPosition = Vec3.ONE; } ```
2. **Update Cycle** Each frame the update function checks if generation is already in progress. If the procedural mode has changed, the object is recreated. Depending on the configuration, geometry is built either in a background thread (async) or directly on the main thread. ```csharp void Update() { int id = Profiler.BeginMicro("Component Update"); // Skip if an update/apply is already running if (isRunning || objectMesh.IsMeshProceduralActive) { Profiler.EndMicro(id); return; } isRunning = true; isMeshvramManual = updatedMeshvramManual; // Recreate object if procedural mode changed if (objectMesh.MeshProceduralMode != currentMode) { objectMesh.DeleteLater(); objectMesh = new ObjectMeshStatic(); objectMesh.SetMeshProceduralMode(currentMode); objectMesh.WorldPosition = Vec3.ONE; } // Choose where to build the mesh: background thread (async) or main thread if (isThreadAsync) { // Builds the mesh on a background thread without blocking the main thread. // Mesh modifications are processed on a separate thread as long as needed, // without impacting performance. AsyncQueue.RunAsync(AsyncQueue.ASYNC_THREAD.BACKGROUND, AsyncUpdateRAM); } else { // Build and apply in this frame on the main thread UpdateRAM(); if (isMeshvramManual) UpdateVRAM(); ApplyData(); } Profiler.EndMicro(id); } ```
3. **Mesh Generation** This is where the new geometry is actually created. An algorithm builds a simple grid, animated using sine and cosine functions to form a wave. Indices are then added to connect the vertices into triangles. Optional collision data and updated bounds are created at the end. <details> <summary>Details</summary> ```csharp private void UpdateMesh(Mesh mesh) { int id = Profiler.BeginMicro("ProceduralMeshModifier.UpdateMesh"); float time = Game.Time; // Ensure exactly one surface and clear previous data if (mesh.NumSurfaces != 1) { mesh.Clear(); mesh.AddSurface(""); } else { mesh.ClearSurface(); } // Generate a grid of vertices with an animated wave var vertices = new vec3[size * size]; for (int y = 0; y < size; y++) { float Y = y * isize - 15.0f; float Z = MathLib.Cos(Y + time); for (int x = 0; x < size; x++) { float X = x * isize - 15.0f; vertices[y * size + x] = (new vec3(X, Y, Z * MathLib.Sin(X + time))); } } mesh.AddVertex(vertices); // Reserve enough memory for indices so vector won't be reallocated // every time it's capacity ends var cindices = new List<int>(); cindices.Capacity = (size - 1) * (size - 1) * 6; var tindices = new List<int>(); tindices.Capacity = (size - 1) * (size - 1) * 6; // Append the same indices to both coordinate and triangle index buffers var addIndex = (int index) => { cindices.Add(index); tindices.Add(index); }; // Build triangles for each quad in the grid for (int y = 0; y < size - 1; y++) { int offset = size * y; for (int x = 0; x < size - 1; x++) { addIndex(offset); addIndex(offset + 1); addIndex(offset + size); addIndex(offset + size); addIndex(offset + 1); addIndex(offset + size + 1); offset++; } } mesh.AddCIndices(cindices.ToArray()); mesh.AddTIndices(tindices.ToArray()); cindices.Clear(); tindices.Clear(); mesh.CreateTangents(); { int idScope = Profiler.BeginMicro("CreateCollisionData"); // If you plan to use intersections or collisions with this mesh, // it's recommended to create CollisionData. Otherwise, intersection // and collision checks will be highly inefficient. if (isCollisionEnabled) { // Creates both Spatial Tree and Edges // for effective intersection and collision respectively mesh.CreateCollisionData(); // If needed, you can create only one: // mesh.CreateSpatialTree();		// intersection only // mesh.CreateEdges();				// collision only } else // You can also create a mesh without CollisionData, or remove existing data // if it�s not needed. // To check whether a mesh has CollisionData, use: //		mesh.HasCollisionData(); //		mesh.HasSpatialTree(); //		mesh.HasEdges(); mesh.ClearCollisionData(); Profiler.EndMicro(idScope); } // Update bounds after geometry changes mesh.CreateBounds(); Profiler.EndMicro(id); } ``` </details>
4. **RAM and VRAM Updates** Once the way to build a geometry is defined, it can be called to update RAM and VRAM mesh data. ```csharp // updates Mesh private void UpdateRAM() { int id = Profiler.BeginMicro("ProceduralMeshModifier.UpdateRAM"); // Return if the main thread side is shutting down if (isDeleted) { Profiler.EndMicro(id); return; } // Lock meshRAM so other threads won't interfere mesh update lock (meshRAM) { UpdateMesh(meshRAM); } Profiler.EndMicro(id); } private void UpdateVRAM() { int id = Profiler.BeginMicro("ProceduralMeshModifier.UpdateVRAM"); // Return if the main thread side is shutting down if (isDeleted) { Profiler.EndMicro(id); return; } // lock so other threads won't interfere mesh update lock (meshRAM) { meshVRAM.Load(meshRAM); } // Upload RAM mesh to VRAM mesh Profiler.EndMicro(id); } ```
5. **Asynchronous Operations (optional)** Asynchronous versions of the update functions run on background or GPU threads and then return control to the main thread when the mesh is ready. ```csharp private void AsyncUpdateRAM() { // Build RAM mesh UpdateRAM(); if (isMeshvramManual) { // Load MeshRender on the GPU Stream thread when doing it manually AsyncQueue.RunAsync(AsyncQueue.ASYNC_THREAD.GPU_STREAM, AsyncUpdateVRAM); } else { // If you don't need to load MeshRender manualy and automatic loading inside // apllyMeshProcedural methods is enough, then return to Main thread AsyncQueue.RunAsync(AsyncQueue.ASYNC_THREAD.MAIN, () => { // Сheck that sample's logic on Main thread is still alive. If it's not then stop // modification and return if (!node || node.IsDeleted) return; ApplyData(); }); } } private void AsyncUpdateVRAM() { // Update MeshRender UpdateVRAM(); // Return to Main thread to apply new mesh AsyncQueue.RunAsync(AsyncQueue.ASYNC_THREAD.MAIN, () => { // Check that sample's logic on Main thread is still alive. If it's not then stop // modification and return if (!node || node.IsDeleted) return; ApplyData(); }); } ```
6. **Apply Mesh Data** Finally, the generated mesh is applied to the object. Copy modes duplicate data; move modes transfer it directly for better performance. Asynchronous and force variants define whether the main thread is blocked during application. ```csharp // Apply procedural mesh only on the main thread! private void ApplyData() { int id = Profiler.BeginMicro("ProceduralMeshModifier.ApplyData"); // In async mode, apply is processed on a separate thread without blocking the main thread. if (isAsyncMode) { if (isMeshvramManual) { // Manual MeshRender is supported only with "Move" mode objectMesh.ApplyMoveMeshProceduralAsync(meshRAM, meshVRAM); } else { if (isCopyMode) // In "Copy" mode, data from mesh_ram is duplicated for internal use, // while mesh_ram itself remains unchanged. objectMesh.ApplyCopyMeshProceduralAsync(meshRAM, currentMeshRenderFlag); else // In "Move" mode, data is taken from mesh_ram for internal use, // which modifies mesh_ram in the process. objectMesh.ApplyMoveMeshProceduralAsync(meshRAM, currentMeshRenderFlag); } } // In force mode, the main thread remains blocked until apply has finished. else { if (isMeshvramManual) { objectMesh.ApplyMoveMeshProceduralForce(meshRAM, meshVRAM); } else { if (isCopyMode) objectMesh.ApplyCopyMeshProceduralForce(meshRAM, currentMeshRenderFlag); else objectMesh.ApplyMoveMeshProceduralForce(meshRAM, currentMeshRenderFlag); } } // Full cycle of mesh modification is finished isRunning = false; Profiler.EndMicro(id); } ```
