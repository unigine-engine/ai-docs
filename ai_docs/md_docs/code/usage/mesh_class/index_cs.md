# Mesh Class (CS)


The *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* class provides an interface for mesh loading, manipulating and saving.


By using this class, you can create a mesh, add geometry to it (e.g. box, plane, capsule or cylinder surface), add animations and bones (if you want to create a skinned mesh) and then use it to create the following objects:


| - [Static mesh](../../../api/library/objects/class.objectmeshstatic_cs.md) - [Skinned mesh](../../../api/library/objects/class.objectmeshskinned_cs.md) | - [Dynamic mesh](../../../api/library/objects/class.objectmeshdynamic_cs.md) - [Decal mesh](../../../api/library/decals/class.decalmesh_cs.md) | - [Gui mesh](../../../api/library/objects/class.objectguimesh_cs.md) - [Water mesh](../../../api/library/objects/class.objectwatermesh_cs.md) |
|---|---|---|


Also you can get geometry of all of these objects via the Mesh class.


Mesh Features:


- **Several Morph Targets** Each surface supports multiple morph targets (also known as blend shapes), enabling vertex-level animation for expressions, shape changes, or deformations.
- **Quaternion-Based Tangent Basis** The tangent space (normal, tangent, bitangent) for each surface is encoded using quaternions.
- **8-Bit Vertex Colors** Vertex colors are stored using 8-bit precision per channel.
- **Dual Indexing System** Each vertex is associated with two buffers:

  - Coordinate buffer: stores vertex positions
  - Triangle buffer: stores unique vertex attributes
- **Two UV Sets per Vertex** Surfaces support two sets of texture coordinates per vertex.


### Mesh Structure


Each Mesh instance contains:


- *[A Bounding Box](../../../api/library/rendering/class.mesh_cs.md#getBoundBox_BoundBox)*
- *[A Bounding Sphere](../../../api/library/rendering/class.mesh_cs.md#getBoundSphere_BoundSphere)*
- One or more surfaces


> **Notice:** Most methods that work with surfaces use surface index 0 by default. If a method should work on all surfaces, use -1 instead. These values are usually set as default methods parameters.


**Surfaces**


A surface is a subset of the object geometry (i.e. a mesh) that does not overlap other subsets. Each surface of a mesh contains:


- **[Name](../../../api/library/rendering/class.mesh_cs.md#setSurfaceName_int_cstr_void)** A unique string used to identify surface within the mesh.
- **[Bounding Box](../../../api/library/rendering/class.mesh_cs.md#getBoundBox_int_BoundBox)** Axis-aligned box enclosing the surface geometry.
- **[Bounding Sphere](../../../api/library/rendering/class.mesh_cs.md#getBoundSphere_int_BoundSphere)** Spherical bound around the surface geometry.
- **Texture Coordinates (UV Sets)** Each vertex stores two sets of UV coordinates: the first is typically used for base textures, and the second for lightmaps or additional effects.
- **Vertex Colors** Each vertex can optionally store an RGBA color, typically encoded as 8-bit per channel. While the mesh itself does not render vertex colors directly, they can be accessed and utilized in materials for effects like blending, masking, or procedural shading. See [example](../../../content/materials/graph/samples/vertex_color/index.md) for how to use vertex colors in a material.
- **Edges and spatial tree** Each surface stores edge data and a spatial tree to accelerate spatial queries such as intersection and collision detection.
- **Coordinate and triangle indices** Each surface includes two index buffers: coordinate indices and triangle indices. Their purpose is described in detail below.


### Vertex Data and Indices


Each mesh surface consists of triangles, with each triangle having 3 vertices. Therefore, the total number of vertices per surface is calculated as:


**Total Vertices = *3 * Number of Triangles***.


If a vertex is shared by multiple triangles, it would normally have to be stored multiple times, with each copy containing data such as position, normal, tangent, texture coordinates, and so on. To minimize redundancy and improve loading performance, UNIGINE uses an optimized layout that separates vertex data into two distinct buffers:


- **Coordinate Vertex Buffer (*CVertices*)**, which stores only vertex coordinates.
- **Triangle Vertex Buffer (*TVertices*)**, which stores vertex attributes such as normal, binormal, tangent, color, UV coordinates.


On the picture below, arrows are used to show [normals](#diff_normals):


![](tcindices.png)

*Surface that contains 2 adjacent triangles. HereC0...C3are coordinate vertices,T0...T5are triangle vertices*


The coordinate buffer is an array of **unique vertex positions**. In order to reduce data duplication, vertices of surface which have the same coordinates are stored **only once** in the buffer.


For example, the coordinate buffer for the surface presented on the picture above is the following:


```text
CVertices = [C0, C1, C2, C3]
```


Each triangle of the surface has 3 coordinates. We have 2 triangles, thus, we have 6 vertices, but we save in the CVertices buffer only 4, because 2 of them (C1 and C3) have the same coordinates. Each coordinate vertex contains coordinates (*float[3]*) of the vertex.


> **Notice:** Since the coordinate buffer stores only non-duplicated vertex positions, the total number of vertices in the mesh and the number of entries in the CVertices buffer are the same.


The triangle buffer is an array of **per-triangle vertex attribute entries**. For example, the triangle buffer for the surface presented on the picture above is the following:


```text
TVertices = [T0, T1, T2, T3, T4, T5]
```


Each triangle vertex can store:


- Normal
- Binormal
- Tangent
- 1st UV map texture coordinates
- 2nd UV map texture coordinates
- Color


> **Notice:** The number of vertices and triangle vertices can be different.


The number of entries in the triangle buffer (TVertices) depends on how a vertex is used across triangles:


- If a vertex is shared between multiple triangles but has different attributes (e.g., different normals or tangents), multiple attribute entries will be stored - one for each variation. In the picture above, coordinate vertex **C1** corresponds to two triangle vertices: **T1** and **T2**.
- If a vertex is shared and its attributes are identical across all triangles, a single attribute entry is sufficient and will be reused.


Both the coordinate and triangle vertex are **indexed**. There are **2 index buffers** to get proper CVertex and TVertex data for each vertex of each triangle of the mesh:


- **Coordinate Index Buffer (CIndices)** - coordinate indices, which are links to [CVertices](#cvertex) data.
- **Triangle Index Buffer (TIndices)** - triangle indices, which are links to [TVertices](#tvertex) data.


The number of elements in these index buffers is equal to the [total number of vertices](#total_vertex_number) of a mesh surface.


> **Notice:** There is no actual structure called a "triangle vertex." All vertex attributes (normals, tangents, UVs, etc.) are stored separately and linked via index buffers. The term "triangle vertex" is used here only for convenience to describe how attributes are associated with vertex positions.
> See the ***[Mesh File Formats](../../../code/formats/file_formats.md#mesh)*** article for details on how mesh structure is organized from a file layout perspective.


#### Coordinate Indices


Each vertex of a mesh surface has a **coordinate index** - a number of the corresponding element of the [coordinate buffer](#indices), where the data is stored. For the given surface the array of the coordinate indices is as follows:


```text
CIndices = [Ci0, Ci1, Ci3, Ci1, Ci2, Ci3]
```


Here:


- The first 3 elements are the coordinate indices of the first (bottom) triangle.
- The second 3 elements are the coordinate indices of the second (top) triangle.


#### Triangle Indices


Each vertex of a mesh surface also has a **triangle index** - a number of the corresponding element of the [triangle buffer](#indices), where the data is stored. For the given surface the array of the triangle indices is as follows:


```text
TIndices = [Ti0, Ti1, Ti5, Ti2, Ti3, Ti4]
```


Here:


- The first 3 elements are the triangle indices of the first (bottom) triangle.
- The second 3 elements are the triangle indices of the second (top) triangle.


> **Notice:** The number of the coordinate and triangle indices is the same.


### See Also


- Article on [Mesh File Formats](../../../code/formats/file_formats.md#mesh).
- Description of the [Mesh class](../../../api/library/rendering/class.mesh_cs.md) functions.


## Accessing a Mesh of a Mesh-Based Object


You can access the source mesh of a mesh-based object (e.g. a [static mesh](../../../api/library/objects/class.objectmeshstatic_cs.md), a [skinned mesh](../../../api/library/objects/class.objectmeshskinned_cs.md) and so on) via the specialized *getMesh...()* methods of the corresponding object class. These methods provide access to either standard or procedural meshes, with different loading strategies:


- *getMeshCurrentRAM()* - returns the current source mesh loaded in RAM (if available).
- *getMeshForceRAM()* - loads and returns the source mesh in RAM immediately.
- *getMeshAsyncRAM()* - loads and returns the source mesh in RAM asynchronously.
- *getMeshDynamicRAM()* - returns the procedural source mesh and ensures it is loaded into RAM.


For example, to access the Mesh of the ObjectMeshStatic, you can do the following:


<details>
<summary>MeshClass.cs | Close</summary>

`MeshClass.cs`


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class MeshClass : Component
{
	private void Init()
	{

	// a mesh-based object from which geometry will be obtained
	ObjectMeshStatic box = new ObjectMeshStatic("core/meshes/box.mesh");
	// create a mesh
	Mesh boxMesh = new Mesh();
	// copy the mesh of the ObjectMeshStatic into the created mesh
	boxMesh.AssignFrom(box.GetMeshForceRAM());

	}
}


```

</details>


The accessed mesh can be used at your discretion.


> **Notice:** The **[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md)** class provides only the **[GetMesh()](../../../api/library/objects/class.objectmeshdynamic_cs.md#getMesh_Mesh_int)** method.


## Copying a Mesh


You may need to copy a Mesh in the following cases:

- When you have a mesh-based object that should be copied into another mesh-based object (new or existing one).
- When you have a Mesh that should be copied into another Mesh.


### From One Mesh-Based Object to Another


You can copy a mesh of a mesh-based object into another object in one of the following ways:


- **By passing a Mesh to a new mesh-based object**:  For example, you can copy the ObjectMeshDynamic mesh to the new ObjectMeshDynamic as follows: <details> <summary>MeshClass.cs | Close</summary> `MeshClass.cs` ```csharp using System; using System.Collections; using System.Collections.Generic; using Unigine; public partial class MeshClass : Component { private void Init() { // get the existing ObjectMeshDynamic node by name ObjectMeshDynamic source = World.GetNodeByName("source_dynamic") as ObjectMeshDynamic; if (source != null) { // create a Mesh container Mesh mesh = new Mesh(); // copy the mesh data from the source object to the container source.GetMesh(mesh); // create a new ObjectMeshDynamic using the copied mesh ObjectMeshDynamic copy = new ObjectMeshDynamic(mesh); } } ``` </details>

  1. Get a source mesh-based object.
  2. Create a Mesh class instance as a container.
  3. Copy the mesh of the source mesh-based object by using the *getMesh()* function.
  4. Create a new mesh-based object from the Mesh instance.
- **By passing a Mesh to an existing mesh-based object**:  For example, you can copy the ObjectMeshDynamic mesh to the existing ObjectMeshDynamic as follows: <details> <summary>MeshClass.cs | Close</summary> `MeshClass.cs` ```csharp using System; using System.Collections; using System.Collections.Generic; using Unigine; public partial class MeshClass : Component { private void Init() { // create ObjectMeshDynamic instances ObjectMeshDynamic dynamic_0 = new ObjectMeshDynamic(); ObjectMeshDynamic dynamic_1 = new ObjectMeshDynamic(); // create a Mesh class instance Mesh mesh = new Mesh(); // copy geometry of the dynamic mesh to the Mesh class instance dynamic_0.GetMesh(mesh); // put the obtained mesh to the second dynamic mesh dynamic_1.SetMesh(mesh); } } ``` </details>

  1. Get two mesh-based objects.
  2. Create a Mesh class instance as a container.
  3. Copy the mesh of the source mesh-based object by using the *getMesh()* function.
  4. Set the copied mesh to the second mesh-based object by using the *setMesh()* function.


> **Notice:** You can return the transformed mesh from the Mesh class to the same ObjectMeshDynamic instance without creating a new one, if necessary.


### From One Mesh to Another


You can easily copy the existing mesh instance to a new one: pass the mesh instance as an argument to the constructor as follows:


<details>
<summary>MeshClass.cs | Close</summary>

`MeshClass.cs`


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class MeshClass : Component
{
	private void Init()
	{

	// create a source Mesh instance
	Mesh mesh_0 = new Mesh("core/meshes/box.mesh");
	// pass the source mesh to the constructor of the second mesh
	Mesh mesh_1 = new Mesh(mesh_0);

	}
}


```

</details>


## Accessing Mesh Surfaces


By using the Mesh class, you can add new surfaces to a mesh or copy surfaces from one mesh to another.


### Adding a New Surface to a Mesh


You can add a new surface to a mesh in one of the following ways:

- **Create a surface from scratch** and then add verties and indices to it.
- Create a surface **using one of the existing predefined surfaces**: a [plane](../../../api/library/rendering/class.mesh_cs.md#addPlaneSurface_cstr_float_float_float_int_int), a [prism](../../../api/library/rendering/class.mesh_cs.md#addPrismSurface_cstr_float_float_float_int_int_int), a [sphere](../../../api/library/rendering/class.mesh_cs.md#addSphereSurface_cstr_float_int_int_int_int), a [box](../../../api/library/rendering/class.mesh_cs.md#addBoxSurface_cstr_vec3_int_int), a [capsule](../../../api/library/rendering/class.mesh_cs.md#addCapsuleSurface_cstr_float_float_int_int_int_int), a [cylinder](../../../api/library/rendering/class.mesh_cs.md#addCylinderSurface_cstr_float_float_int_int_int_int), a [dodecahedron](../../../api/library/rendering/class.mesh_cs.md#addDodecahedronSurface_cstr_float_int_int), an [icosahedron](../../../api/library/rendering/class.mesh_cs.md#addIcosahedronSurface_cstr_float_int_int).


#### Creating a Surface from Scratch


The Mesh class allows creating a surface and adding vertices to it.


In the following example, we create a plane by adding vertices to the mesh:

1. Create a Mesh class instance, add a surface and 4 vertices to it.
2. Add 6 indices to create a plane. > **Notice:** You can add indices explicitly as in the example below, or you can create indices for recently added vertices by using the [*createIndices()*](../../../api/library/rendering/class.mesh_cs.md#createIndices_int_int) function.
3. Create tangents and normals by using the *[CreateTangents()](../../../api/library/rendering/class.mesh_cs.md#createTangents_int_int)* and *[CreateNormals()](../../../api/library/rendering/class.mesh_cs.md#createNormals_int_int)* functions.
4. Update bounds of the mesh to include all new vertices via the *[CreateBounds()](../../../api/library/rendering/class.mesh_cs.md#createBounds_int_void)* function.
5. Create an ObjectMeshDynamic instance using the mesh to check the result.


<details>
<summary>MeshClass.cs | Close</summary>

`MeshClass.cs`


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class MeshClass : Component
{
	private void Init()
	{

	// create a mesh instance
	Mesh mesh = new Mesh();

	// add a new surface
	mesh.AddSurface("surface_0");

	// add vertices of the plane
	mesh.AddVertex(new vec3(0.0f, 0.0f, 0.0f), 0);
	mesh.AddVertex(new vec3(0.0f, 0.0f, 1.0f), 0);
	mesh.AddVertex(new vec3(0.0f, 1.0f, 0.0f), 0);
	mesh.AddVertex(new vec3(0.0f, 1.0f, 1.0f), 0);

	// add indices
	mesh.AddIndex(0, 0);
	mesh.AddIndex(1, 0);
	mesh.AddIndex(2, 0);

	mesh.AddIndex(3, 0);
	mesh.AddIndex(2, 0);
	mesh.AddIndex(1, 0);

	// create tangents
	mesh.CreateTangents(0);
	// create mesh bounds
	mesh.CreateBounds(0);
	// create normals
	mesh.CreateNormals(0);

	// create an ObjectMeshDynamic from the Mesh instance
	ObjectMeshDynamic dynamicMesh = new ObjectMeshDynamic(mesh);

	}
}


```

</details>


#### Adding a Predefined Surface


To add a predefined surface to a Mesh instance, use the required function. For example, to add a new capsule surface to a mesh, do the following:

1. Create a Mesh class instance.
2. Add a capsule surface via the *[addCapsuleSurface()](../../../api/library/rendering/class.mesh_cs.md#addCapsuleSurface_cstr_float_float_int_int_int_int)* function.
3. Create an ObjectMeshDynamic instance using the mesh to check the result.


<details>
<summary>MeshClass.cs | Close</summary>

`MeshClass.cs`


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class MeshClass : Component
{
	private void Init()
	{

	// create a mesh instance
	Mesh mesh_0 = new Mesh();
	// add a capsule surface to the mesh
	mesh_0.AddCapsuleSurface("capsule_surface", 1.0f, 2.0f, 200, 100);
	// create an ObjectMeshDynamic from the Mesh instance
	ObjectMeshDynamic dynamicMesh = new ObjectMeshDynamic(mesh_0);

	}
}


```

</details>


### Copying Surfaces from One Mesh to Another


In the following example, we create two meshes with different surfaces. The first mesh has the capsule surface, the second has the box surface. We copy the box surface from the second mesh to the first. The execution sequence is:


- Create 2 instances of the Mesh class and add the capsule and box surfaces to them.
- Add the box surface from the second mesh (*mesh_1*) to the first mesh (*mesh_0*) by using the *[AddMeshSurface()](../../../api/library/rendering/class.mesh_cs.md#addMeshSurface_cstr_ConstMesh_int_int_int)* function.
- Create a new *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md)* mesh from the *mesh_0* instance.


<details>
<summary>MeshClass.cs | Close</summary>

`MeshClass.cs`


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class MeshClass : Component
{
	private void Init()
	{

	// create mesh instances
	Mesh mesh_0 = new Mesh();
	Mesh mesh_1 = new Mesh();

	// add surfaces for the added meshes
	mesh_0.AddCapsuleSurface("capsule_surface", 1.0f, 2.0f, 200, 100);
	mesh_1.AddBoxSurface("box_surface", new vec3(2.2f));

	// add the surface from the mesh_1 to the mesh_0 as a new surface
	// with the name "new_box_surface"
	mesh_0.AddMeshSurface("new_box_surface", mesh_1, 0);

	// create an ObjectMeshDynamic from the Mesh instance
	ObjectMeshDynamic dynamicMesh = new ObjectMeshDynamic(mesh_0);

	// set the position of the dynamic mesh
	dynamicMesh.WorldTransform = MathLib.Translate(new vec3(10.0f, 10.0f, 10.0f));

	}
}


```

</details>


In the result, the Mesh will have 2 surfaces.

> **Notice:** You can copy a surface from the source mesh and add it to the existing surface of the current mesh without creating a new surface by using the overloaded *[AddMeshSurface()](../../../api/library/rendering/class.mesh_cs.md#addMeshSurface_cstr_ConstMesh_int_int_int)* function.


The ObjectMeshDynamic mesh will appear in the editor:


![](add_mesh_surface.png)

*ObjectMeshDynamic with 2 surfaces*


### Adding a Surface to the Existing Mesh


In the following example, we add a surface to the existing mesh and then add necessary vertices and indices for the surface:


1. Create a new mesh instance from the file.
2. Add a new surface to the mesh.
3. Add vertices for the mesh surface.
4. Create indices for recently created vertices by using the *[CreateIndices()](../../../api/library/rendering/class.mesh_cs.md#createIndices_int_int)* function.
5. Update bounds of the mesh to include the created surface by using the *[CreateBounds()](../../../api/library/rendering/class.mesh_cs.md#createBounds_int_void)* function.
6. Change the surface color.


<details>
<summary>MeshClass.cs | Close</summary>

`MeshClass.cs`


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class MeshClass : Component
{
	private void Init()
	{

		// load a mesh from the file
		Mesh source_mesh = new Mesh("core/meshes/box.mesh");

		// add a new surface
		int surface_index = source_mesh.AddSurface("surface_triangle");

		// add 3 vertices to the new surface
		source_mesh.AddVertex(new vec3(-0.5f, 0.5f, 0.5f), 1);
		source_mesh.AddVertex(new vec3(-0.5f, -0.5f, 0.5f), 1);
		source_mesh.AddVertex(new vec3(-0.5f, -0.5f, 1.5f), 1);

		// create indices for the new surface
		source_mesh.CreateIndices(surface_index);
		// create a new boundbox for the mesh including new surface
		source_mesh.CreateBounds();

		// create an ObjectMeshStatic, switch it to procedural mode and set its mesh via the source_mesh instance
		ObjectMeshStatic staticMesh = new ObjectMeshStatic();

		// before changing mesh choose Procedural Mode:
		// - Disable - procedural mode is disabled
		// - Dynamic - fastest performance, stored in RAM and VRAM, not automatically unloaded from memory.
		// - Blob - moderate performance, stored in RAM and VRAM, automatically unloaded from memory.
		// - File - slowest performance, all data stored on disk, automatically unloaded from memory.
		staticMesh.SetMeshProceduralMode(ObjectMeshStatic.PROCEDURAL_MODE.DYNAMIC);

		// Apply new mesh. You can do it Force or Async.
		// Changing mesh_render_flag you can choose where to store MeshRender data: in RAM or VRAM
		// 0 - store everything in VRAM (default behavior)
		// USAGE_DYNAMIC_VERTEX - store vertices on RAM
		// USAGE_DYNAMIC_INDICES - store indices on RAM
		// USAGE_DYNAMIC_ALL - store both vertices and indices on RAM
		staticMesh.ApplyMoveMeshProceduralAsync(source_mesh, 0);

		// change the material color
		staticMesh.SetMaterialParameterFloat4("albedo_color", new vec4(255, 255, 0, 255), 1);

	}
}


```

</details>


The triangle surface added to the mesh:


![](mesh_new_surface.png)


## Changing Vertex Attributes


The Mesh class allows changing vertex attributes.


In the following example, we take a plane and change attributes of its vertices:


1. Create a Mesh and [add a new surface to it](#add_surface).
2. Print the current normal values of 2 vertices to the console.
3. Set new values for the normals and print the updated values to the console.
4. Print the current tangent values of 2 vertices to the console.
5. Set new values for the tangents and print the updated values to the console.
6. Create a new *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md)* from the Mesh instance to check the result.


<details>
<summary>MeshClass.cs | Close</summary>

`MeshClass.cs`


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class MeshClass : Component
{
	private void Init()
	{

	// create a mesh instance
	Mesh mesh = new Mesh();

	// add a new surface
	mesh.AddSurface("surface_0");

	// add vertices of the plane
	mesh.AddVertex(new vec3(0.0f, 0.0f, 0.0f), 0);
	mesh.AddVertex(new vec3(0.0f, 0.0f, 1.0f), 0);
	mesh.AddVertex(new vec3(0.0f, 1.0f, 0.0f), 0);
	mesh.AddVertex(new vec3(0.0f, 1.0f, 1.0f), 0);

	// add indices
	mesh.AddIndex(0, 0);
	mesh.AddIndex(1, 0);
	mesh.AddIndex(2, 0);

	mesh.AddIndex(3, 0);
	mesh.AddIndex(2, 0);
	mesh.AddIndex(1, 0);

	// create normals
	mesh.CreateNormals();
	// create tangents
	mesh.CreateTangents();
	// create mesh bounds
	mesh.CreateBounds();

	// get the normal vectors of the 1st and the 2nd normal before changing
	vec3 normal_0 = mesh.GetNormal(0, 0, 0);
	vec3 normal_1 = mesh.GetNormal(1, 0, 0);
	// print values of the normals to the console
	Log.Message("the 1st normal: {0}\n", normal_0.ToString());
	Log.Message("the 2nd normal: {0}\n", normal_1.ToString());

	// set new values for the normals
	mesh.SetNormal(0, new vec3(1.0f, 1.0f, 0.0f), 0, 0);
	mesh.SetNormal(1, new vec3(1.0f, 1.0f, 1.0f), 0, 0);

	// get the new normal vectors of the 1st and the 2nd normal
	vec3 new_normal_0 = mesh.GetNormal(0, 0, 0);
	vec3 new_normal_1 = mesh.GetNormal(1, 0, 0);
	// print values of the normals to the console
	Log.Message("the 1st normal: {0}\n", new_normal_0.ToString());
	Log.Message("the 2nd normal: {0}\n", new_normal_1.ToString());
	// get the tangent value
	quat tangent = mesh.GetTangent(0, 0, 0);
	// show the tangent value in the console
	Log.Message("tangent: {0}\n", tangent.ToString());

	// set a new value of the tangent
	mesh.SetTangent(0, new quat(new vec3(1.0f, 0.0f, 0.0f), 20), 0, 0);

	// get the new tangent value
	quat new_tangent = mesh.GetTangent(0, 0, 0);
	// show the tangent value after changing
	Log.Message("tangent: {0}\n", new_tangent.ToString());
	// create an ObjectMeshDynamic from the Mesh instance
	ObjectMeshDynamic newDynamicMesh = new ObjectMeshDynamic(mesh);

	// set the dynamic mesh position
	newDynamicMesh.WorldTransform = MathLib.Translate(new vec3(1.0f, 1.0f, 1.0f)) * (mat4)MathLib.RotateZ(90.0f);

	}
}


```

</details>


When you launch the project, in the console you'll see the following:


```text
the first normal is: -1 0 0 and the second is: -1 0 0
the first normal is: 1 1 0 and the second is: 1 1 1
tangent is: : 0,5 -0,5 -0,5 0,5
tangent is: : 0,1736 0 0 0,9848

```


When [*setTangent()*](../../../api/library/rendering/class.mesh_cs.md#setTangent_int_quat_int_void) and [*setNormal()*](../../../api/library/rendering/class.mesh_cs.md#setNormal_int_vec3_int_void) functions were called, the normal and the tangent changed their values.


Let's comment this part of the code:


<details>
<summary>MeshClass.cs | Close</summary>

`MeshClass.cs`


```csharp
// get the tangent value
quat tangent = mesh.GetTangent(0, 0, 0);
// show the tangent value in the console
Log.Message("tangent: {0}\n", tangent.ToString());

// set a new value of the tangent
mesh.SetTangent(0, new quat(new vec3(1.0f, 0.0f, 0.0f), 20), 0, 0);

// get the new tangent value
quat new_tangent = mesh.GetTangent(0, 0, 0);
// show the tangent value after changing
Log.Message("tangent: {0}\n", new_tangent.ToString());


```

</details>


The result will be different. You can see what influence the tangent has on the vertex:


| ![](plane_w_tangent.png) | ![](plane_wo_tangent.png) |
|---|---|
| *Plane with changed tangent* | *Plane with unchanged tangent* |


## Creating a Primitive


The following example shows the manual creation of a box primitive by specifying its vertices, normals and texture coordinates:


<details>
<summary>MeshClass.cs | Close</summary>

`MeshClass.cs`


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class MeshClass : Component
{
	private void Init()
	{

	// create a mesh instance
	Mesh mesh = new Mesh();

	// add a manually created box surface
	AddManualBoxSurface(mesh, new vec3(2.0f, 2.0f, 2.0f), "box");

	// create an ObjectMeshDynamic from the Mesh instance
	ObjectMeshDynamic dynamicMesh = new ObjectMeshDynamic(mesh);

	// clear the mesh pointer
	mesh.Clear();

	// set the position of the dynamic mesh
	dynamicMesh.WorldTransform = MathLib.Translate(vec3.ZERO);
	// set the texture
	dynamicMesh.SetMaterialTexture("albedo", "core/textures/common/checker_d.texture", 0);

	}
	private void AddManualBoxSurface(Mesh mesh, vec3 size, string name) {
	// add a new surface
	int surface_index = mesh.AddSurface(name);

	// array of vertices
	vec3[] vertex = {
		new vec3(-0.5f, -0.5f, -0.5f), new vec3(0.5f, -0.5f, -0.5f), new vec3(-0.5f, 0.5f, -0.5f), new vec3(0.5f, 0.5f, -0.5f),
		new vec3(-0.5f, -0.5f, 0.5f), new vec3(0.5f, -0.5f, 0.5f), new vec3(-0.5f, 0.5f, 0.5f), new vec3(0.5f, 0.5f, 0.5f) };

	// array of face normals
	vec3[] normals = {
		vec3.RIGHT, vec3.LEFT,
		vec3.FORWARD, vec3.BACK,
		vec3.UP, vec3.DOWN };

	// array of texture coordinates
	vec2[] texcoords = {
		new vec2(1.0f, 1.0f), new vec2(0.0f, 1.0f),
		new vec2(0.0f, 0.0f), new vec2(1.0f, 0.0f) };

	// list of indices for 6 polygons
	int[,] cindices = {
		{ 3, 1, 5, 7 },{ 0, 2, 6, 4 },
		{ 2, 3, 7, 6 },{ 1, 0, 4, 5 },
		{ 6, 7, 5, 4 },{ 0, 1, 3, 2 } };

	// list of indices for a single quad made of 2 triangles
	int[] indices = {
		0, 3, 2, 2, 1, 0 };

	// cycle through all quads
	for (int i = 0; i < 6; i++)
	{
		// cycle through all indices of a single quad
		for (int j = 0; j < 6; j++)
		{
			int index = indices[j];
			mesh.AddVertex(vertex[cindices[i,index]] * size, surface_index);
			mesh.AddNormal(normals[i], surface_index);
			if (i == 4)
			{
				mesh.AddTexCoord0((vec2.ONE - texcoords[index]), surface_index);

			}
			else
			{
				mesh.AddTexCoord0(texcoords[index], surface_index);
			}
		}
	}

	// create indices per each 3 added vertices
	mesh.CreateIndices(surface_index);

	// create tangents
	mesh.CreateTangents(surface_index);

	// create mesh bounds
	mesh.CreateBounds(surface_index);

	}
}


```

</details>


![](primitive.png)
