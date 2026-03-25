# Dynamic Meshes (CS)


The article describes operations on dynamic meshes via code by using methods of the *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md)* class. This class is used to procedurally create dynamic meshes and modify them in runtime. You can also load an existing mesh as a dynamic one to modify it.


### See Also


- An [ObjectMeshDynamic class](../../../api/library/objects/class.objectmeshdynamic_cs.md) to edit dynamic meshes via UnigineScript
- A set of samples located in the `data/samples/objects/` directory:

  - [`dynamic_00`](../../../code/uniginescript/samples/objects/dynamic_00.md)
  - [`dynamic_01`](../../../code/uniginescript/samples/objects/dynamic_01.md)
  - [`dynamic_02`](../../../code/uniginescript/samples/objects/dynamic_02.md)
  - [`dynamic_03`](../../../code/uniginescript/samples/objects/dynamic_03.md)
  - [`dynamic_04`](../../../code/uniginescript/samples/objects/dynamic_04.md)
  - [`dynamic_05`](../../../code/uniginescript/samples/objects/dynamic_05.md)


## Creating a Dynamic Mesh


There are three methods to add a new dynamic mesh:


- Add a [new dynamic mesh via UnigineEditor](../../../objects/objects/mesh_dynamic/index.md#adding).
- [Create a new dynamic mesh by adding vertices](#new).
- [Create a new dynamic mesh from the existing mesh](#existing).


### Creating a New Dynamic Mesh


This chapter describes how to create a new dynamic mesh by allocating memory and adding vertices for a new mesh. You can allocate memory for a [moderate number of triangles](#moderate) or for a [big number of vertices](#big_number).


#### Adding triangles


You can create a dynamic mesh from scratch, by adding one triangle after another. This variant is suitable for creating meshes with a moderate number of triangles. To create a new dynamic mesh you should do the following:


1. Reserve a necessary space in a vertex buffer for triangle vertices and add indices for them to the index buffer. This is done by calling one of the following methods: All these functions allocate memory for polygons of the corresponding form.

  - *[addTriangles()](../../../api/library/objects/class.objectmeshdynamic_cs.md#addTriangles_int_void)*
  - *[addTriangleStrip()](../../../api/library/objects/class.objectmeshdynamic_cs.md#addTriangleStrip_int_void)*
  - *[addTriangleQuads()](../../../api/library/objects/class.objectmeshdynamic_cs.md#addTriangleQuads_int_void)*
  - *[addTriangleFan()](../../../api/library/objects/class.objectmeshdynamic_cs.md#addTriangleFan_int_void)*
2. Add the corresponding number of vertices via *[addVertex()](../../../api/library/objects/class.objectmeshdynamic_cs.md#addVertex_vec3_void)* method.
3. After each call of the *addVertex()* function, you can set up properties of the last added vertex manually via calling: All these functions are optional, you can call them as needed.

  - *[addTexCoord()](../../../api/library/objects/class.objectmeshdynamic_cs.md#addTexCoord_vec4_void)*
  - *[addColor()](../../../api/library/objects/class.objectmeshdynamic_cs.md#addColor_vec4_void)*
  - *[addTangent()](../../../api/library/objects/class.objectmeshdynamic_cs.md#addTangent_quat_void)*
4. Calculate tangent vectors for all vertices via *[updateTangents()](../../../api/library/objects/class.objectmeshdynamic_cs.md#updateTangents_int)*.
5. Calculate a bounding box and a bounding sphere for the created mesh by calling *[updateBounds()](../../../api/library/objects/class.objectmeshdynamic_cs.md#updateBounds_int)*.
6. If necessary, you can remove duplicated vertices of the created mesh and optimize it for faster rendering. Use *[updateIndices()](../../../api/library/objects/class.objectmeshdynamic_cs.md#updateIndices_int)* function, for example, if a quad polygon is created via *addTriangles(2)* (six vertices are created) instead of an optimized *addTriangleQuads(1)* (four vertices are created).


##### Usage Example


The following example shows how to create a quad polygon by using the *[addTriangleQuads()](../../../api/library/objects/class.objectmeshdynamic_cs.md#addTriangleQuads_int_void)* function.


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

#if UNIGINE_DOUBLE
	using Vec3 = Unigine.dvec3;
#else
	using Vec3 = Unigine.vec3;
#endif

public partial class DynamicMeshes : Component
{

	ObjectMeshDynamic mesh;

	private void Init()
	{

		// create a dynamic mesh
		mesh = new ObjectMeshDynamic();

		mesh.WorldTransform = MathLib.Translate(new Vec3(0.0f, 0.0f, 2.0f));

		// allocate space in a vertex buffer and create vertex indices
		mesh.AddTriangleQuads(1);

		// add vertices and assign texture coordinates, if necessary
		mesh.AddVertex(new vec3(-1.0f, -1.0f, 0.0f));
		mesh.AddTexCoord(new vec4(0, 0, 0, 0));

		mesh.AddVertex(new vec3(1.0f, -1.0f, 0.0f));
		mesh.AddTexCoord(new vec4(1, 0, 0, 0));

		mesh.AddVertex(new vec3(1.0f, 1.0f, 0.0f));
		mesh.AddTexCoord(new vec4(1, 1, 0, 0));

		mesh.AddVertex(new vec3(-1.0f, 1.0f, 0.0f));
		mesh.AddTexCoord(new vec4(0, 1, 0, 0));

		// calculate tangent vectors
		mesh.UpdateTangents();
		// optimize vertex and index buffers, if necessary
		//mesh.UpdateIndices();

		// calculate a mesh bounding box
		mesh.UpdateBounds();
	}


```


#### Adding a Large Number of Vertices


To create dynamic meshes with a huge number of vertices, it is better to use the more optimized approach: instead of allocating memory in small chunks (which can be costly), all necessary memory is preallocated first and filled with data after that.


1. Allocate space for triangle vertices in an index buffer using *[allocateIndices()](../../../api/library/objects/class.objectmeshdynamic_cs.md)*.
2. Allocate space for vertices in a vertex buffer using *[allocateVertex()](../../../api/library/objects/class.objectmeshdynamic_cs.md)*.
3. Add the corresponding number of vertices via *[addVertex()](../../../api/library/objects/class.objectmeshdynamic_cs.md)* method.
4. Add the corresponding number of indices via *[addIndex()](../../../api/library/objects/class.objectmeshdynamic_cs.md)* method.
5. Follow steps [3-6 described above](#instructions).


##### Usage Example


The following example shows how to create a plane by adding vertex by vertex.


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

#if UNIGINE_DOUBLE
	using Vec3 = Unigine.dvec3;
#else
	using Vec3 = Unigine.vec3;
#endif

public partial class DynamicMeshes : Component
{

	ObjectMeshDynamic mesh;

	private void Init()
	{

		// create a dynamic mesh
		mesh = new ObjectMeshDynamic();

		mesh.WorldTransform = MathLib.Translate(new Vec3(0.0f,0.0f,2.0f));

		// allocate space in index and vertex buffers
		mesh.AllocateIndices(6);
		mesh.AllocateVertex(4);
		// add vertices
		mesh.AddVertex(new vec3(-1.0f,-1.0f,0.0f));
		mesh.AddVertex(new vec3(1.0f, -1.0f, 0.0f));
		mesh.AddVertex(new vec3(1.0f, 1.0f, 0.0f));
		mesh.AddVertex(new vec3(-1.0f, 1.0f, 0.0f));
		// add indices for created vertices
		mesh.AddIndex(0);
		mesh.AddIndex(1);
		mesh.AddIndex(2);
		mesh.AddIndex(0);
		mesh.AddIndex(2);
		mesh.AddIndex(3);

		// calculate tangent vectors
		mesh.UpdateTangents();
		// optimize vertex and index buffers, if necessary

		// calculate a mesh bounding box
		mesh.UpdateBounds();
	}


```


### Creating a Dynamic Mesh Based on the Existing Mesh


There are some ways to create a dynamic mesh from the existing mesh:


- Create a new instance of the *ObjectMeshDynamic* class by [passing the *Mesh* class instance as an argument to the constructor.](#passing_mesh_constructor)
- [Copy the Mesh class instance to the existing ObjectMeshDynamic instance](#passing_mesh_function) by passing the *Mesh* class instance as an argument to the *[setMesh()](../../../api/library/objects/class.objectmeshdynamic_cs.md#setMesh_Mesh_int)* function.


#### Passing a Mesh to a New Dynamic Mesh


To create a new *ObjectMeshDynamic* instance from this existing mesh, you should pass the existing *Mesh* class instance to the *ObjectMeshDynamic* class constructor.


##### Usage Example


The following example shows how to create a new dynamic mesh from the existing *Mesh* class instance. It is supposed that you already have the *Mesh* instance, but in this example we create a new instance of the *Mesh* class with the box surface.


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

#if UNIGINE_DOUBLE
	using Vec3 = Unigine.dvec3;
#else
	using Vec3 = Unigine.vec3;
#endif

public partial class DynamicMeshes : Component
{

	ObjectMeshDynamic dynamic_mesh;

	private void Init()
	{

		// create the mesh with the box surface
		Mesh mesh = new Mesh();
		mesh.AddBoxSurface("box", new vec3(1.0f));

		// create a new ObjectMeshDynamic instance by passing mesh as an argument
		dynamic_mesh = new ObjectMeshDynamic(mesh);
	}


```


#### Copy a Mesh to the Existing Dynamic Mesh


To copy the mesh from the *Mesh* instance to an existing dynamic mesh, you should use the *[setMesh()](../../../api/library/objects/class.objectmeshdynamic_cs.md#setMesh_Mesh_int)* function and pass the *Mesh* instance as an argument to it. This function copies a given mesh into the current dynamic mesh.


##### Usage Example


The following example shows how to copy the mesh from the *Mesh* instance to the *ObjectMeshDynamic* instance. It is supposed that you already have the *Mesh* instance, but in this example we create a new instance of the *Mesh* class with the box surface.


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

#if UNIGINE_DOUBLE
	using Vec3 = Unigine.dvec3;
#else
	using Vec3 = Unigine.vec3;
#endif

public partial class DynamicMeshes : Component
{

	ObjectMeshDynamic dynamic_mesh;

	private void Init()
	{

		// existing mesh with a box surface
		Mesh mesh = new Mesh();
		mesh.AddBoxSurface("box", new vec3(2.2f));

		// create a new ObjectMeshDynamic
		ObjectMeshDynamic dynamic_mesh = new ObjectMeshDynamic();

		// copy the existing mesh to the ObjectMeshDynamic
		dynamic_mesh.SetMesh(mesh);
	}


```


## Adding Physics to Dynamic Meshes


To add some physical properties to the dynamic mesh so that it could participate in interactions between objects or external physical forces, it should have a body. You can easily assign it from code or in UnigineEditor.


### Usage Example


The following example shows how to add the rigid body with a shape to the dynamic mesh. In the example, the dynamic mesh is created from the existing mesh with the box surface.


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

#if UNIGINE_DOUBLE
	using Vec3 = Unigine.dvec3;
#else
	using Vec3 = Unigine.vec3;
#endif

public partial class DynamicMeshes : Component
{

	ObjectMeshDynamic dynamic_mesh;

	private void Init()
	{

		// create a mesh instance with a box surface
		Mesh mesh = new Mesh();
		mesh.AddBoxSurface("box", new vec3(0.2f));

		// create a new dynamic mesh from the Mesh instance and add it to editor
		dynamic_mesh = new ObjectMeshDynamic(mesh);

		dynamic_mesh.WorldTransform = MathLib.Translate(new Vec3(0.0f, 0.0f, 2.0f));

		// assign a body and a shape to the dynamic mesh
		BodyRigid body = new BodyRigid(dynamic_mesh);
		ShapeBox shape = new ShapeBox(body, new vec3(0.2f));
	}


```


### See Also


- The article about [Physical bodies](../../../principles/physics/bodies/index.md)
- The article about [Shapes](../../../principles/physics/shapes/index.md)


## Intersections with Dynamic Meshes


To detect if the dynamic mesh intersects a line or bounds of the specified volume, you should use one of the following functions:


- *[getIntersection()](../../../api/library/objects/class.object_cs.md#getIntersection_Vec3_Vec3_ObjectIntersection_int_int)* of the Object class that detects the intersection of the specified object with a tracing line.
- *[getIntersection()](../../../api/library/engine/class.world_cs.md#getIntersectionNodeVariables_Variable_int_VECint_int)* functions of the World class that detect all the objects and nodes in the specific bounding volume or the first object intersection with the invisible tracing line. See [examples of the world intersections](../../../code/usage/intersections/index_cs.md#world_intersection).
- *[getIntersection()](../../../api/library/physics/class.physics_cs.md#getIntersection_Vec3_Vec3_int_int_Variable)* functions of the Physics class that detect intersections with a shape of bodies. If the object has no body, this function detects intersection with surfaces (polygons) of the object with the [intersection flag](../../../api/library/objects/class.object_cs.md#setIntersection_int_int_void). See a usage example of the [physics intersections here](../../../code/usage/intersections/index_cs.md#physics_intersection).
- *[getIntersection()](../../../api/library/physics/class.shape_cs.md#getIntersection_Vec3_Vec3_PhysicsIntersection_int)* of the Shape class detects the intersection of the specified shape with a tracing line. See the example of [shape intersection here](../../../api/library/physics/class.shape_cs.md#shape_intersection).


Read the [Intersections](../../../code/usage/intersections/index_cs.md) article to know more about intersections.


## Saving a Dynamic Mesh to a File


To save the dynamic mesh into a file, you should copy it to the *Mesh* class instance. By using the *[save()](../../../api/library/rendering/class.mesh_cs.md#save_cstr_int)* function of the *Mesh* class, you can save the mesh with the specified name.


### Usage Example


The following example shows how to save the dynamic mesh to the file. It is supposed that you have a dynamic mesh to save. You should pass a path as an argument to the *[save()](../../../api/library/rendering/class.mesh_cs.md#save_cstr_int)* function of the *Mesh* class. The path is relative to the `data/` folder of your project.


```csharp
// create a mesh instance
Mesh mesh_0 = new Mesh();
// copy the dynamic mesh to the Mesh class instance
dynamic_mesh.GetMesh(mesh_0);

// save the mesh to the data/meshes/dynamic_mesh.mesh file
mesh_0.Save("meshes/dynamic_mesh.mesh");


```
