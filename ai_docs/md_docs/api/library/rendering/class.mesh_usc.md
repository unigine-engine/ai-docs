# Unigine.Mesh Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


The *Mesh* class is a container that provides an interface for loading, manipulating, and saving meshes.


By using this class, you can create a mesh, add geometry to it (e.g. box, plane, capsule or cylinder surface) and then use it to create the following objects:


- [Static mesh](../../../api/library/objects/class.objectmeshstatic_usc.md)
- [Dynamic mesh](../../../api/library/objects/class.objectmeshdynamic_usc.md)
- [Decal mesh](../../../api/library/decals/class.decalmesh_usc.md)
- [Gui mesh](../../../api/library/objects/class.objectguimesh_usc.md)
- [Water mesh](../../../api/library/objects/class.objectwatermesh_usc.md)


You can also access the geometry of all these objecs through the Mesh class.


Mesh Features:


- **Quaternion-Based Tangent Basis** The tangent space (normal, tangent, bitangent) for each surface is encoded using quaternions.
- **8-Bit Vertex Colors** Vertex colors are stored using 8-bit precision per channel.
- **Dual Indexing System** Each vertex is associated with two buffers:

  - Coordinate buffer: stores vertex positions
  - Triangle buffer: stores unique vertex attributes
- **Two UV Sets per Vertex** Surfaces support two sets of texture coordinates per vertex.


### Mesh Structure


Each Mesh instance contains:


- *[A Bounding Box](../../../api/library/rendering/class.mesh_usc.md#BoundBox)*
- *[A Bounding Sphere](../../../api/library/rendering/class.mesh_usc.md#BoundSphere)*
- One or more surfaces


> **Notice:** Most methods that work with surfaces use surface index 0 by default. If a method should work on all surfaces, use -1 instead. These values are usually set as default methods parameters.


**Surfaces**


A surface is a subset of the object geometry (i.e. a mesh) that does not overlap other subsets. Each surface of a mesh contains:


- **[Name](../../../api/library/rendering/class.mesh_usc.md#setSurfaceName_int_cstr_void)** A unique string used to identify surface within the mesh.
- **[Bounding Box](../../../api/library/rendering/class.mesh_usc.md#getBoundBox_int_BoundBox)** Axis-aligned box enclosing the surface geometry.
- **[Bounding Sphere](../../../api/library/rendering/class.mesh_usc.md#getBoundSphere_int_BoundSphere)** Spherical bound around the surface geometry.
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
>
>
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


### Serialization


You can save your created mesh to a file to be used later via the [*save()*](#save_cstr_int) method. Later on, you can create a new mesh from this file using the [constructor](#Mesh_constchar), or load a mesh via the [*load()*](#load_cstr_int) method.


> **Notice:** Normals of mesh are not serializable. The whole [tangent basis](#createTangents_int_int) is serialized instead.


So, to get your normals from a saved mesh you should do the following:


```cpp
// adding a surface and vertices to the mesh
Mesh mesh = new Mesh();
// adding a surface and vertices to the mesh
mesh.addSurface("0");
mesh.addVertex(vec3(1.f, 1.f, 0.f), 0);
mesh.addVertex(vec3(1.f, 0.f, 1.f), 0);
mesh.addVertex(vec3(0.f, 1.f, 1.f), 0);

// create normals
mesh.addNormal(vec3(0.f, 0.f, 1.f), 0);
mesh.addNormal(vec3(0.f, 0.f, 1.f), 0);
mesh.addNormal(vec3(0.f, 0.f, 1.f), 0);

// adding vertex indices
mesh.addIndex(0, 0);
mesh.addIndex(1, 0);
mesh.addIndex(2, 0);

// creating serializable tangent basis
mesh.createTangents();

// saving a mesh to a file
mesh.save("hello.mesh");

// ...

```


Now to get your normals after creating a mesh from a file:


```cpp
// creating a mesh from a previously saved file
Mesh mesh = new Mesh("hello.mesh");

// getting the total number of vertex tangent entries for the first surface of the mesh
int numTangents = mesh.getNumTangents(0);

// retrieving normals from the tangent basis for the first point of the first surface of the mesh
vec3 normal = mesh.getTangent(0, 0).getNormal();

// ...

```


### See Also


- Article on [Mesh File Formats](../../../code/formats/file_formats.md#mesh)
- [Mesh Class Usage Example](../../../code/usage/mesh_class/index_usc.md)


## Mesh Class

### Members

## BoundSphere getBoundSphere () const

Returns the current bounding sphere of the mesh.
### Return value

Current bounding sphere of the mesh
## BoundBox getBoundBox () const

Returns the current bounding box of the mesh.
### Return value

Current bounding box of the mesh
## int getNumSurfaces () const

Returns the current total number of mesh surfaces.
### Return value

Current total number of mesh surfaces
## int getMemoryUsage () const

Returns the current amount of memory used by the mesh, in bytes.
### Return value

Current amount of memory used by the mesh, in bytes
## void setSpatialTreeTriangles ( int triangles )

Sets a new number of triangles stored in each leaf node of the mesh's spatial tree.
Lower values (default is 4) improve the precision of intersection and collision detections, but increase spatial tree generation time and memory usage.


Higher values reduce generation cost and memory consumption at the expense of intersection and collision detections accuracy. Useful for high-poly meshes or frequently updated procedural geometry.


### Arguments

- *int* **triangles** - The number of triangles stored in each leaf node of the mesh's spatial tree

## int getSpatialTreeTriangles () const

Returns the current number of triangles stored in each leaf node of the mesh's spatial tree.
Lower values (default is 4) improve the precision of intersection and collision detections, but increase spatial tree generation time and memory usage.


Higher values reduce generation cost and memory consumption at the expense of intersection and collision detections accuracy. Useful for high-poly meshes or frequently updated procedural geometry.


### Return value

Current number of triangles stored in each leaf node of the mesh's spatial tree
---

## static Mesh ( )

Constructor. Creates an empty mesh.
## static Mesh ( string path )

Constructor. Creates a mesh using the specified file.
### Arguments

- *string* **path** - Path to the mesh file.

## void assignFrom ( ConstMesh mesh )

Copies the data including bones, surfaces, and animations from the specified source mesh.
### Arguments

- *ConstMesh* **mesh** - Source mesh instance.

## void swap ( Mesh mesh )

Swaps all internal data between this mesh and the specified one. Used to efficiently exchange geometry data without memory copying.
### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_usc.md)* **mesh** - The mesh to swap data with.

## void setBoundBox ( BoundBox bb , int surface )

Sets the bounding box for the given mesh surface.
### Arguments

- *BoundBox* **bb** - Bounding box to be set.
- *int* **surface** - Mesh surface number.

## void setBoundBox ( BoundBox bb )

Sets the bounding box for the current mesh.
### Arguments

- *BoundBox* **bb** - Bounding box to be set.

## BoundBox getBoundBox ( int surface )

Returns the bounding box of the given mesh surface.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Bounding box.
## void setBoundSphere ( BoundSphere bs )

Sets the bounding sphere for the current mesh.
### Arguments

- *BoundSphere* **bs** - Bounding sphere to be set.

## void setBoundSphere ( BoundSphere bs , int surface )

Sets the bounding sphere for the given mesh surface.
### Arguments

- *BoundSphere* **bs** - Bounding sphere to be set.
- *int* **surface** - Mesh surface number.

## BoundSphere getBoundSphere ( int surface )

Returns the bounding sphere of the given mesh surface.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Bounding sphere.
## void setCIndex ( int num , int index , int surface = 0 )

Sets the new [coordinate index](#cindices) for the given vertex of the given surface.
### Arguments

- *int* **num** - Vertex number in the range from 0 to the total number of coordinate indices for the given surface. > **Notice:** To get the total number of coordinate indices for the given surface, use the [getNumCIndices()](#getNumCIndices_int_int) method.
- *int* **index** - Coordinate index to be set in the range from 0 to the total number of coordinate vertices for the given surface. > **Notice:** To get the total number of coordinate vertices for the given surface, use the [getNumCVertex()](#getNumCVertex_int_int) method.
- *int* **surface** - Mesh surface number.

## int getCIndex ( int num , int surface = 0 )

Returns the [coordinate index](#cindices) for the given vertex of the given surface.
### Arguments

- *int* **num** - Vertex number in the range from 0 to the total number of coordinate indices for the given surface. > **Notice:** To get the total number of coordinate indices for the given surface, use the [getNumCIndices()](#getNumCIndices_int_int) method.
- *int* **surface** - Mesh surface number.

### Return value

Coordinate index.
## void setColor ( int num , vec4 color , int surface = 0 )

Sets the color for the given [triangle vertex](#tvertex) of the given surface.
### Arguments

- *int* **num** - [Triangle vertex](#tvertex) number in the range from 0 to the total number of vertex color entries of the given surface. > **Notice:** To get the total number of vertex color entries for the surface, call the [*getNumColors()*](#getNumColors_int_int) method.
- *vec4* **color** - Vertex color to be set.
- *int* **surface** - Mesh surface number.

## vec4 getColor ( int num , int surface = 0 )

Returns the color of the given [triangle vertex](#tvertex) of the given surface.
### Arguments

- *int* **num** - [Triangle vertex](#tvertex) number in the range from 0 to the total number of vertex color entries of the given surface. > **Notice:** To get the total number of vertex color entries for the surface, call the [*getNumColors()*](#getNumColors_int_int) method.
- *int* **surface** - Mesh surface number.

### Return value

Vertex color.
## void setIndex ( int num , int index , int surface = 0 )

Sets both [coordinate](#cindices) and [triangle](#tindices) indices for the given vertex of the given surface equal to the specified index.
### Arguments

- *int* **num** - Vertex number in the range from 0 to the total number of coordinate indices of the given surface. > **Notice:** To get the total number of coordinate indices for the surface, use the [getNumCIndices()](#getNumCIndices_int_int) method.
- *int* **index** - Index to be set in the range from 0 to the total number of coordinate vertices. > **Notice:** To get the total number of coordinate vertices, use the [getNumVertex()](#getNumVertex_int_int) method.
- *int* **surface** - Mesh surface number.

## int getIndex ( int num , int surface = 0 )

Returns the [coordinate index](#cindices) of the given vertex of the given surface if the coordinate index is equal to the [triangle index](#tindices).
### Arguments

- *int* **num** - Vertex number in the range from 0 to the total number of coordinate indices of the given surface. > **Notice:** To get the total number of coordinate indices for the surface, use the [getNumCIndices()](#getNumCIndices_int_int) method.
- *int* **surface** - Mesh surface number.

### Return value

[Coordinate index](#cindices).
## int getIntersection ( vec3 p0 , vec3 p1 , vec3 * OUT_ret_point , vec3 * OUT_ret_normal , int * OUT_ret_index , int surface )

Performs the search for the intersection of the given surface with the given traced line.


> **Notice:** Mesh local space coordinates are used for this method.


### Arguments

- *vec3* **p0** - Start point coordinates.
- *vec3* **p1** - End point coordinates.
- *vec3 ** **OUT_ret_point** - Return array to write the intersection point coordinates into. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *vec3 ** **OUT_ret_normal** - Return array to write the intersection point normal into. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int ** **OUT_ret_index** - Return array to write the intersection point indices into. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **surface** - Mesh surface number.

### Return value

1 if the intersection is found; otherwise, 0.
## void setNormal ( int num , vec3 normal , int surface = 0 )

Sets the normal for the given [triangle vertex](#tvertex) of the given surface.


> **Notice:** The normal of the vertex won't be written to the `*.mesh` file. It will be stored only in memory.


### Arguments

- *int* **num** - [Triangle vertex](#tvertex) number in the range from 0 to the total number of vertex normal entries of the given surface. > **Notice:** To get the total number of vertex normal entries for the surface, call the [*getNumNormals()*](#getNumNormals_int_int) method.
- *vec3* **normal** - Normal to be set.
- *int* **surface** - Mesh surface number.

## vec3 getNormal ( int num , int surface = 0 )

Returns the normal for the given [triangle vertex](#tvertex) of the given surface.
### Arguments

- *int* **num** - [Triangle vertex](#tvertex) number in the range from 0 to the total number of vertex normal entries of the given surface. > **Notice:** To get the total number of vertex normal entries for the surface, call the [*getNumNormals()*](#getNumNormals_int_int) method.
- *int* **surface** - Mesh surface number.

### Return value

Vertex normal.
## void setNumCIndices ( int size , int surface = 0 )

Sets the total number of [coordinate indices](#cindices) for the given surface.
### Arguments

- *int* **size** - Number of the coordinate indices to be set.
- *int* **surface** - Mesh surface number.

## int getNumCIndices ( int surface = 0 )

Returns the total number of [coordinate indices](#cindices) for the given surface.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Number of coordinate indices.
## void setNumColors ( int size , int surface = 0 )

Sets the total number of vertex color entries for the given surface.


> **Notice:** Colors are specified for [triangle vertices](#tvertex).


### Arguments

- *int* **size** - Number of vertex color entries to be set.
- *int* **surface** - Mesh surface number.

## int getNumColors ( int surface = 0 )

Returns the total number of vertex color entries for the given surface.


> **Notice:** Colors are specified for [triangle vertices](#tvertex).


### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Number of vertex color entries.
## int getNumCVertex ( int surface = 0 )

Returns the number of [coordinate vertices](#cvertex) of the given surface.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Number of coordinate vertices.
## void setNumIndices ( int size , int surface = 0 )

Sets the number of [indices](#indices) for the given surface: updates the number of coordinate and triangle indices.  For example, if you pass 5 as the first argument, the number of the coordinate indices and the number of triangle indices will be set to 5.
### Arguments

- *int* **size** - Number of indices to be set.
- *int* **surface** - Mesh surface number.

## int getNumIndices ( int surface = 0 )

Returns the number of [coordinate indices](#cindices) of the given surface if the number of the coordinate indices is equal to the number of triangle indices.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Number of coordinate indices.
## void setNumNormals ( int size , int surface = 0 )

Sets the total number of vertex normal entries for the given surface.


> **Notice:** Normals are specified for [triangle vertices](#tvertex).


### Arguments

- *int* **size** - Number of vertex normal entries to be set.
- *int* **surface** - Mesh surface number.

## int getNumNormals ( int surface = 0 )

Returns the total number of vertex normal entries for the given surface.


> **Notice:** Normals are specified for [triangle vertices](#tvertex).


### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Number of vertex normal entries for the given surface.
## void setNumTangents ( int size , int surface = 0 )

Sets the total number of vertex tangent entries for the given surface.


> **Notice:** Tangents are specified for [triangle vertices](#tvertex).


### Arguments

- *int* **size** - Number of vertex tangent entries to be set.
- *int* **surface** - Mesh surface number.

## int getNumTangents ( int surface )

Returns the total number of vertex tangent entries for the given surface.


> **Notice:** Tangents are specified for [triangle vertices](#tvertex).


### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Number of vertex tangent entries.
## void setNumTexCoords0 ( int size , int surface = 0 )

Sets the total number of the first UV map texture coordinate entries for the given mesh surface.


> **Notice:** First UV map texture coordinates are specified for [triangle vertices](#tvertex).


### Arguments

- *int* **size** - Number of the first UV map texture coordinate entries to be set.
- *int* **surface** - Mesh surface number.

## int getNumTexCoords0 ( int surface = 0 )

Returns the total number of the first UV map texture coordinate entries for the given mesh surface.


> **Notice:** First UV map texture coordinates are specified for [triangle vertices](#tvertex).


### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Total number of the first UV map texture coordinate entries.
## void setNumTexCoords1 ( int size , int surface )

Sets the total number of the second UV map texture coordinate entries for the given mesh surface.


> **Notice:** Second UV map texture coordinates are specified for [triangle vertices](#tvertex).


### Arguments

- *int* **size** - Number of the second UV map texture coordinates to be set.
- *int* **surface** - Mesh surface number.

## int getNumTexCoords1 ( int surface = 0 )

Returns the total number of the second UV map texture coordinate entries for the given mesh surface.


> **Notice:** Second UV map texture coordinates are specified for [triangle vertices](#tvertex).


### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Total number of the second UV map texture coordinate entries.
## void setNumTIndices ( int size , int surface = 0 )

Sets the total number of [triangle indices](#tindices) for the given surface.
### Arguments

- *int* **size** - Number of triangle indices to be set.
- *int* **surface** - Mesh surface number.

## int getNumTIndices ( int surface = 0 )

Returns the total number of [triangle indices](#tindices) for the given surface.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Number of triangle indices.
## int getNumTVertex ( int surface = 0 )

Returns the number of [triangle vertices](#tvertex) for the given mesh surface.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Number of the triangle vertices.
## void setNumVertex ( int size , int surface = 0 )

Sets the total number of vertices for the given surface.


> **Notice:** The numbers of vertices and [coordinate vertices](#cvertex) are equal.


### Arguments

- *int* **size** - Number of the vertices to be set.
- *int* **surface** - Mesh surface number.

## getNumVertex ( int surface )

Returns the total number of vertices for the given surface.


> **Notice:** The numbers of vertices and [coordinate vertices](#cvertex) are equal.


### Arguments

- *int* **surface** - Mesh surface number.

## void setSurfaceName ( int surface , string name )

Sets the name for the given mesh surface.
### Arguments

- *int* **surface** - Mesh surface number.
- *string* **name** - Surface name to be set.

## string getSurfaceName ( int surface )

Returns the name of the given surface.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Surface name.
## int setSurfaceTransform ( mat4 transform , int surface = -1 )

Sets the transformation matrix for the given surface.
### Arguments

- *mat4* **transform** - Transformation matrix to be set.
- *int* **surface** - Mesh surface number. The default value is -1 (apply to all of the mesh surfaces).

### Return value

1 if the transformation matrix is set successfully; otherwise, 0.
## void setSurfaceLightmapUVChannel ( int surface , char uv_channel )

Sets a new UV channel to be used for [lightmaps](../../../editor2/lighting/gi/lightmaps.md) of the surface with the specified number.
### Arguments

- *int* **surface** - Mesh surface number.
- *char* **uv_channel** - UV channel to be used for lightmaps of the surface with the specified number.

## char getSurfaceLightmapUVChannel ( int surface )

Returns the current UV channel used for [lightmaps](../../../editor2/lighting/gi/lightmaps.md) of the surface with the specified number.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

UV channel currently used for lightmaps of the surface with the specified number.
## void setSurfaceLightmapResolution ( int surface , int resolution )

Sets a new [lightmap](../../../editor2/lighting/gi/lightmaps.md) resolution for the surface with the specified number.
### Arguments

- *int* **surface** - Mesh surface number.
- *int* **resolution** - Lightmap resolution to be used for the surface with the specified number.

## int getSurfaceLightmapResolution ( int surface )

Returns the current [lightmap](../../../editor2/lighting/gi/lightmaps.md) resolution for the surface with the specified number.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Current lightmap resolution for the surface with the specified number.
## void setTangent ( int num , quat tangent , int surface = 0 )

Sets the new tangent for the given [triangle vertex](#tvertex) of the given surface.
### Arguments

- *int* **num** - [Triangle vertex](#tvertex) number in the range from 0 to the total number of vertex tangent entries of the given surface. > **Notice:** To get the total number of vertex tangent entries for the surface, call the [getNumTangents()](#getNumTangents_int_int) method.
- *quat* **tangent** - Tangent to be set.
- *int* **surface** - Mesh surface number.

## quat getTangent ( int num , int surface = 0 )

Returns the tangent for the given [triangle vertex](#tvertex) of the given surface.
### Arguments

- *int* **num** - [Triangle vertex](#tvertex) number in the range from 0 to the total number of vertex tangent entries of the given surface. > **Notice:** To get the total number of vertex tangent entries for the surface, call the [getNumTangents()](#getNumTangents_int_int) method.
- *int* **surface** - Mesh surface number.

### Return value

Vertex tangent.
## void setTexCoord0 ( int num , vec2 texcoord , int surface )

Sets first UV map texture coordinates for the given [triangle vertex](#tvertex) of the given surface.
### Arguments

- *int* **num** - [Triangle vertex](#tvertex) number in the range from 0 to the total number of first UV map texture coordinate entries of the given surface. > **Notice:** To get the total number of first UV map texture coordinate entries for the surface, call the [getNumTexCoords0()](#getNumTexCoords0_int_int) method.
- *vec2* **texcoord** - First UV map texture coordinates to be set.
- *int* **surface** - Mesh surface number.

## vec2 getTexCoord0 ( int num , int surface )

Returns first UV map texture coordinates for the given [triangle vertex](#tvertex) of the given surface.
### Arguments

- *int* **num** - [Triangle vertex](#tvertex) number in the range from 0 to the total number of first UV map texture coordinate entries of the given surface. > **Notice:** To get the total number of first UV map texture coordinate entries for the surface, call the [getNumTexCoords0()](#getNumTexCoords0_int_int) method.
- *int* **surface** - Mesh surface number.

### Return value

First UV map texture coordinates.
## void setTexCoord1 ( int num , vec2 texcoord , int surface = 0 )

Sets second UV map texture coordinates for the given [triangle vertex](#tvertex) of the given surface.
### Arguments

- *int* **num** - [Triangle vertex](#tvertex) number in the range from 0 to the total number of second UV map texture coordinate entries of the given surface. > **Notice:** To get the total number of second UV map texture coordinate entries for the surface, call the [getNumTexCoords1()](#getNumTexCoords1_int_int) method.
- *vec2* **texcoord** - Second UV map texture coordinates to be set.
- *int* **surface** - Mesh surface number.

## vec2 getTexCoord1 ( int num , int surface = 0 )

Returns second UV map texture coordinates for the given [triangle vertex](#tvertex) of the given surface.
### Arguments

- *int* **num** - [Triangle vertex](#tvertex) number in the range from 0 to the total number of second UV map texture coordinate entries of the given surface. > **Notice:** To get the total number of second UV map texture coordinate entries for the surface, call the [getNumTexCoords1()](#getNumTexCoords1_int_int) method.
- *int* **surface** - Mesh surface number.

### Return value

Second UV map texture coordinates.
## void setTIndex ( int num , int index , int surface = 0 )

Sets the new [triangle index](#tindices) for the given vertex of the given surface.
### Arguments

- *int* **num** - Vertex number in the range from 0 to the total number of triangle indices for the given surface. > **Notice:** To get the total number of triangle indices, use the [getNumTIndices()](#getNumTIndices_int_int) method.
- *int* **index** - Triangle index to be set in the range from 0 to the total number of triangle vertices for the given surface. > **Notice:** To get the total number of triangle vertices for the given surface, use the [getNumTVertex()](#getNumTVertex_int_int) method.
- *int* **surface** - Mesh surface number.

## int getTIndex ( int num , int surface = 0 )

Returns the [triangle index](#tindices) for the given surface by using the index number.
### Arguments

- *int* **num** - Vertex number in the range from 0 to the total number of triangle indices for the given surface. > **Notice:** To get the total number of triangle indices for the given surface, use the [getNumTIndices()](#getNumTIndices_int_int) method.
- *int* **surface** - Mesh surface number.

### Return value

Triangle index.
## void setVertex ( int num , vec3 vertex , int surface = 0 )

Sets the coordinates of the given [coordinate vertex](#cvertex) of the given surface.
### Arguments

- *int* **num** - [Coordinate vertex](#cvertex) number in the range from 0 to the total number of coordinate vertices for the given surface. > **Notice:** To get the total number of coordinate vertices for the given surface, use the [getNumCVertex()](#getNumCVertex_int_int) method.
- *vec3* **vertex** - Vertex coordinates to be set.
- *int* **surface** - Mesh surface number.

## int addBoxSurface ( string name , vec3 size , int collision_data_flags = COLLISION_DATA_ALL )

Appends a box surface to the current mesh.


```cpp
// create a mesh instance
Mesh mesh = new Mesh();
// add box surface with the name "box_surface" and the size of the surface is Vec3(1.0, 1.0, 1.0)
mesh.addBoxSurface("box_surface", Vec3(1.0f));

// create the ObjectMeshDynamic from the Mesh object
ObjectMeshDynamic dynamicMesh = new ObjectMeshDynamic(mesh);

// set the position of the mesh
dynamicMesh.setWorldTransform(translate(Vec3(10.0f,10.0f,10.0f)));

// set the name of the mesh
dynamicMesh.Name = "Dynamic Mesh";

```


The mesh will appear.


![](create_box_surface.png)


### Arguments

- *string* **name** - Surface name.
- *vec3* **size** - Box size along the X, Y and Z axes.
- *int* **collision_data_flags** - Bitmask that specifies which [types of collision data](#COLLISION_DATA_BOUNDS) to generate for the new surface.

### Return value

Added surface number.
## int addCapsuleSurface ( string name , float radius , float height , int stacks , int slices , int collision_data_flags = COLLISION_DATA_ALL )

Appends a capsule surface to the current mesh. The stacks and slices specify the surface's subdivision.


```cpp
// create a mesh instance
Mesh mesh = new Mesh();
// add capsule surface with the name "capsule_surface".
// the radius of the capsule is 1.0, the height is 2.0,
// stacks and slices are equals to 200 and 100, respectively
mesh.addCapsuleSurface("box_surface", 1.0f, 2.0f, 200, 100);

// create the ObjectMeshDynamic from the Mesh object
ObjectMeshDynamic dynamicMesh = new ObjectMeshDynamic(mesh);

// set the position of the mesh
dynamicMesh.setWorldTransform(translate(Vec3(10.0f,10.0f,10.0f)));

// set the name of the mesh
dynamicMesh.Name = "Dynamic Mesh";

```


The mesh will appear.


![](create_capsule_surface.png)


### Arguments

- *string* **name** - Surface name.
- *float* **radius** - Capsule radius.
- *float* **height** - Capsule height.
- *int* **stacks** - Number of stacks that divide the capsule radially.
- *int* **slices** - Number of slices that divide the capsule horizontally.
- *int* **collision_data_flags** - Bitmask that specifies which [types of collision data](#COLLISION_DATA_BOUNDS) to generate for the new surface.

### Return value

The added surface number.
## void addCIndex ( int index , int surface = 0 )

Appends a new [Coordinate index](#cindices) the array of coordinate indices for the given surface.
### Arguments

- *int* **index** - [Coordinate index](#cindices) to be added in the range from 0 to the total number of coordinate vertices. > **Notice:** To get the total number of coordinate vertices for the given surface, use the [getNumCVertex()](#getNumCVertex_int_int) method.
- *int* **surface** - Mesh surface number.

## void addColor ( vec4 color , int surface = 0 )

Appends the given color to the vertex color array of the given surface.
### Arguments

- *vec4* **color** - Color to be added.
- *int* **surface** - Mesh surface number.

## int addCylinderSurface ( string name , float radius , float height , int stacks , int slices , int collision_data_flags = COLLISION_DATA_ALL )

Appends a cylinder surface to the current mesh. The stacks and slices specify the surface's subdivision.


```cpp
// create a mesh instance
Mesh mesh = new Mesh();
// add cylinder surface with the name "cylinder_surface".
// the radius of the cylinder is 1.0, the height is 2.0,
// stacks and slices are equals to 200 and 100, respectively
mesh.addCylinderSurface("cylinder_surface", 1.0f, 2.0f, 200, 100);

// create the ObjectMeshDynamic from the Mesh object
ObjectMeshDynamic dynamicMesh = new ObjectMeshDynamic(mesh);

// set the position of the mesh
dynamicMesh.setWorldTransform(translate(Vec3(10.0f,10.0f,10.0f)));

// set the name of the mesh
dynamicMesh.Name = "Dynamic Mesh";

```


The mesh will appear.


![](create_cylinder_surface.png)


### Arguments

- *string* **name** - Surface name.
- *float* **radius** - Cylinder radius.
- *float* **height** - Cylinder height.
- *int* **stacks** - Number of stacks that divide the cylinder radially.
- *int* **slices** - Number of slices that divide the cylinder horizontally.
- *int* **collision_data_flags** - Bitmask that specifies which [types of collision data](#COLLISION_DATA_BOUNDS) to generate for the new surface.

### Return value

The added surface number.
## int addDodecahedronSurface ( string name , float radius , int collision_data_flags = COLLISION_DATA_ALL )

Appends a dodecahedron surface to the current mesh.


```cpp
// create a mesh instance
Mesh mesh = new Mesh();
// add dodecahedron surface with the name "dodecahedron_surface".
// the radius of the dodecahedron is 1.0
mesh.addDodecahedronSurface("dodecahedron_surface", 1.0f);

// create the ObjectMeshDynamic from the Mesh object
ObjectMeshDynamic dynamicMesh = new ObjectMeshDynamic(mesh);

// set the position of the mesh
dynamicMesh.setWorldTransform(translate(Vec3(10.0f,10.0f,10.0f)));

// set the name of the mesh
dynamicMesh.Name = "Dynamic Mesh";

```


After adding to the editor, the mesh will appear.


![](create_dodecahedron_surface.png)


### Arguments

- *string* **name** - Surface name.
- *float* **radius** - Dodecahedron radius.
- *int* **collision_data_flags** - Bitmask that specifies which [types of collision data](#COLLISION_DATA_BOUNDS) to generate for the new surface.

### Return value

The added surface number.
## int addEmptySurface ( string name , int num_vertex , int num_indices )

Appends a new empty surface to the current mesh.


> **Notice:** This function allocates only vertex and index arrays. Texture coordinates, tangent basis, weights and color arrays must be allocated manually.


### Arguments

- *string* **name** - Surface name.
- *int* **num_vertex** - Number of surface vertices.
- *int* **num_indices** - Number of surface indices.

### Return value

Number of the mesh surfaces.
## int addIcosahedronSurface ( string name , float radius , int collision_data_flags = COLLISION_DATA_ALL )

Appends an icosahedron surface to the current mesh.


```cpp
// create a mesh instance
Mesh mesh = new Mesh();
// add icosahedron surface with the name "icosahedron_surface".
// the radius of the icosahedron is 1.0
mesh.addIcosahedronSurface("icosahedron_surface", 1.0f);

// create the ObjectMeshDynamic from the Mesh object
ObjectMeshDynamic dynamicMesh = new ObjectMeshDynamic(mesh);

// set the position of the mesh
dynamicMesh.setWorldTransform(translate(Vec3(10.0f,10.0f,10.0f)));

// set the name of the mesh
dynamicMesh.Name = "Dynamic Mesh";

```


The mesh will appear.


![](create_icosahedron_surface.png)


### Arguments

- *string* **name** - Surface name.
- *float* **radius** - Icosahedron radius.
- *int* **collision_data_flags** - Bitmask that specifies which [types of collision data](#COLLISION_DATA_BOUNDS) to generate for the new surface.

### Return value

Added surface number.
## void addIndex ( int index , int surface = 0 )

Appends a given index to the arrays of [coordinate](#cindices) and [triangle](#tindices) indices for the given surface.
### Arguments

- *int* **index** - Index to be added in the range from 0 to the total number of [coordinate vertices](#cvertex) for the surface. > **Notice:** To get the total number of coordinate vertices for the surface, use the [getNumCVertex()](#getNumCVertex_int_int) method.
- *int* **surface** - Mesh surface number.

## void addNormal ( vec3 normal , int surface = 0 )

Appends a given normal to the array of normals of the given surface.
### Arguments

- *vec3* **normal** - Normal to be added.
- *int* **surface** - Mesh surface number.

## int addPlaneSurface ( string name , float width , float height , float step , int collision_data_flags = COLLISION_DATA_ALL )

Appends a plane surface to the current mesh. The plane is divided into equal squares whose size is defined by the given step.


```cpp
// create a mesh instance
Mesh mesh = new Mesh();
// add the plane surface with the name "plane_surface".
// the width is 2 and the height is 3
mesh.addPlaneSurface("plane_surface", 2.0f, 3.0f, 1.0f);

// create the ObjectMeshDynamic from the Mesh object
ObjectMeshDynamic dynamicMesh = new ObjectMeshDynamic(mesh);

// set the position of the mesh
dynamicMesh.setWorldTransform(translate(Vec3(10.0f,10.0f,10.0f)));

// set the name of the mesh
dynamicMesh.Name = "Dynamic Mesh";

```


The mesh will appear. You could see that the plane divided each 1 unit to equal squares.


![](create_plane_surface.png)


### Arguments

- *string* **name** - Surface name.
- *float* **width** - Plane width.
- *float* **height** - Plane height.
- *float* **step** - Step of surface subdivision (vertical and horizontal).
- *int* **collision_data_flags** - Bitmask that specifies which [types of collision data](#COLLISION_DATA_BOUNDS) to generate for the new surface.

### Return value

Added surface number.
## int addPrismSurface ( string name , float size_0 , float size_1 , float height , int sides , int collision_data_flags = COLLISION_DATA_ALL )

Appends a prism surface to the current mesh.


```cpp
// create a mesh instance
Mesh mesh = new Mesh();
// add the prism surface with the name "prism_surface".
// the radius of the top is 1.0f, of the bottom is 2.0f
// the height of the prism is 3.0f, and it has 4 sides
mesh.addPrismSurface("prism_surface", 1.0f, 2.0f, 3.0f, 4);

// create the ObjectMeshDynamic from the Mesh object
ObjectMeshDynamic dynamicMesh = new ObjectMeshDynamic(mesh);

// set the position of the mesh
dynamicMesh.setWorldTransform(translate(Vec3(10.0f,10.0f,10.0f)));

// set the name of the mesh
dynamicMesh.Name = "Dynamic Mesh";

```


The mesh will appear.


![](create_prism_surface.png)


### Arguments

- *string* **name** - Surface name.
- *float* **size_0** - Radius of the circle circumscribed about the top prism base.
- *float* **size_1** - Radius of the circle circumscribed about the bottom prism base.
- *float* **height** - Height of the prism.
- *int* **sides** - Number of the prism faces.
- *int* **collision_data_flags**

### Return value

The added surface number.
## int addSphereSurface ( string name , float radius , int stacks , int slices , int collision_data_flags = COLLISION_DATA_ALL )

Appends a sphere surface to the current mesh. The stacks and slices specify the surface's subdivision.


```cpp
// create a mesh instance
Mesh mesh = new Mesh();
// add the sphere surface with the name "sphere_surface".
// the radius of the sphere is 1.0f
// and it has 200 stacks and 100 slices
mesh.addSphereSurface("sphere_surface", 1.0f, 200, 100);

// create the ObjectMeshDynamic from the Mesh object
ObjectMeshDynamic dynamicMesh = new ObjectMeshDynamic(mesh);

// set the position of the mesh
dynamicMesh.setWorldTransform(translate(Vec3(10.0f,10.0f,10.0f)));

// set the name of the mesh
dynamicMesh.Name = "Dynamic Mesh";

```


The mesh will appear.


![](create_sphere_surface.png)


### Arguments

- *string* **name** - Surface name.
- *float* **radius** - Sphere radius.
- *int* **stacks** - Number of stacks that divide the sphere radially.
- *int* **slices** - Number of slices that divide the sphere horizontally.
- *int* **collision_data_flags** - Bitmask that specifies which [types of collision data](#COLLISION_DATA_BOUNDS) to generate for the new surface.

### Return value

Added surface number.
## int addSurface ( string name = 0 )

Appends a new surface with the given name to the current mesh.


In the following example, we create a new surface and add vertices and indices to create a plane.


```cpp
// create a mesh instance
Mesh mesh = new Mesh();

// add a new surface
mesh.addSurface("surface_0");

// add vertices of the plane
mesh.addVertex(vec3(0.0f,0.0f,0.0f),0);
mesh.addVertex(vec3(0.0f,0.0f,1.0f),0);
mesh.addVertex(vec3(0.0f,1.0f,0.0f),0);
mesh.addVertex(vec3(0.0f,1.0f,1.0f),0);

// add indices
mesh.addIndex(0,0);
mesh.addIndex(1,0);
mesh.addIndex(2,0);

mesh.addIndex(3,0);
mesh.addIndex(2,0);
mesh.addIndex(1,0);

// create tangents
mesh.createTangents();

// create mesh bounds
mesh.createBounds(0);

// create the ObjectMeshDynamic from the Mesh object
ObjectMeshDynamic dynamicMesh = new ObjectMeshDynamic(mesh);

// set the position of the mesh
dynamicMesh.setWorldTransform(translate(Vec3(10.0f,10.0f,10.0f)));

// set the name of the mesh
dynamicMesh.setName("new_mesh");

```


### Arguments

- *string* **name** - Surface name. This argument is empty by default.

### Return value

Number of mesh surfaces.
## void addTangent ( quat tangent , int surface = 0 )

Appends the given tangent to the array of tangents of the specified surface.
### Arguments

- *quat* **tangent** - Tangent to be added.
- *int* **surface** - Surface number.

## void addTexCoord0 ( vec2 texcoord , int surface )

Appends texture coordinates to the array of the first UV map coordinates of the given mesh surface.
### Arguments

- *vec2* **texcoord** - Coordinates of the first UV map to be added.
- *int* **surface** - Mesh surface number.

## void addTexCoord1 ( vec2 texcoord , int surface = 0 )

Appends texture coordinates to the array of the second UV map coordinates of the given mesh surface.
### Arguments

- *vec2* **texcoord** - Coordinates of the second UV map to be added.
- *int* **surface** - Mesh surface number.

## void addTIndex ( int index , int surface = 0 )

Appends an index of a [triangle vertex](#tvertex) to the array of triangle indices for the given surface.
### Arguments

- *int* **index** - Index number of the vertex in the [triangle buffer](#indices) in the range from 0 to the total number of triangle vertices. > **Notice:** To get the total number of triangle vertices for the given surface, use the [getNumTVertex()](#getNumTVertex_int_int) method.
- *int* **surface** - Number of the surface to which the triangle index is added.

## void addVertex ( vec3 vertex , int surface = 0 )

Appends a new [coordinate vertex](#cvertex) with the given coordinates to the morph target of the mesh surface.


In the following example, we create a new surface and add 4 vertices to it. We use local coordinates to define a vertex and specify the surface. After that we specify 6 indices to create a plane by using defined vertices.


```cpp
// create a mesh instance
Mesh mesh = new Mesh();

// add a new surface
mesh.addSurface("surface_0");

// add vertices of the plane
mesh.addVertex(vec3(0.0f,0.0f,0.0f),0);
mesh.addVertex(vec3(0.0f,0.0f,1.0f),0);
mesh.addVertex(vec3(0.0f,1.0f,0.0f),0);
mesh.addVertex(vec3(0.0f,1.0f,1.0f),0);

// add indices
mesh.addIndex(0,0);
mesh.addIndex(1,0);
mesh.addIndex(2,0);

mesh.addIndex(3,0);
mesh.addIndex(2,0);
mesh.addIndex(1,0);

// create tangents
mesh.createTangents();

// create mesh bounds
mesh.createBounds(0);

// create the ObjectMeshDynamic from the Mesh object
ObjectMeshDynamic dynamicMesh = new ObjectMeshDynamic(mesh);

// set the position of the mesh
dynamicMesh.setWorldTransform(translate(Vec3(10.0f,10.0f,10.0f)));

// set the name of the mesh
dynamicMesh.setName("new_mesh");

```


### Arguments

- *vec3* **vertex** - Coordinates of the vertex to be added.
- *int* **surface** - Mesh surface number.

## void clear ( )

Clears the mesh (including its bones, animation, surfaces and bounds).
## void createBounds ( int surface = -1 )

Creates bounds (a bounding box and a bounding sphere) for the given surface. If the default value is used as an argument, the bounds will be created for all of the mesh surfaces.
### Arguments

- *int* **surface** - Mesh surface number. The default value is -1 (all of the mesh surfaces).

## int createIndices ( int surface = -1 )

Creates indices for the given surface. If the default value is used as an argument, the indices will be created for all of the mesh surfaces.
### Arguments

- *int* **surface** - Mesh surface number. The default value is -1 (all of the mesh surfaces).

### Return value

1 if indices are created successfully; otherwise, 0.
## int createTangents ( int surface = -1 )

Creates tangents for the given surface.
### Arguments

- *int* **surface** - Mesh surface number. -1 means all of the mesh surfaces.

### Return value

1 if the tangents are created successfully; otherwise, 0.
## int findSurface ( string name )

Searches for the surface number by its name.
### Arguments

- *string* **name** - Mesh surface name.

### Return value

Mesh surface number, if it is found; otherwise, -1.
## int flipTangent ( int surface = -1 )

Flips the sign of the binormal component of the surface tangent space.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

1 if the sign of the binormal component is flipped successfully; otherwise, 0.
## int flipYZ ( int surface = -1 )

Flips the Y and Z axes for the given surface:


- Y axis becomes equal to -Z
- Z axis becomes equal to Y


### Arguments

- *int* **surface** - Mesh surface number.

### Return value

1 if the axes are flipped successfully; otherwise, 0.
## int info ( string path )

Returns the information about the given mesh or animation.
### Arguments

- *string* **path** - Mesh or animation name.

### Return value

1 if the information returned successfully; otherwise, 0.
## int load ( string path )

Loads the mesh with the given name for the current mesh.
### Arguments

- *string* **path** - Mesh name.

### Return value

1 if the mesh is loaded successfully; otherwise, 0.
## int optimizeIndices ( int flags , int surface = -1 )

Optimizes indices of the given mesh surface. As polygons are added to a surface, vertices of the adjacent polygons are duplicated (you can get the number of such the vertices by using the [getNumTVertex()](#getNumTVertex_int_int)), because normals, texture coordinates and tangents of such the vertices differ depending on the polygons, to which this vertices belongs. The optimizeIndices() function serves to decrease the number of such vertices and create indices for them that will be stored in the corresponding normals, tangents and texture coordinates.
### Arguments

- *int* **flags** - One of the flags used for indices' optimization: [*MESH_BACK_TO_FRONT*](#BACK_TO_FRONT) or [*MESH_VERTEX_CACHE*](#VERTEX_CACHE).
- *int* **surface** - Mesh surface number.

### Return value

1 if the indices are optimized successfully; otherwise, 0.
## void remapCVertex ( int surface = 0 )

Sets the size of the array of [coordinate indices](#cindices) to be equal to the size of the array of [triangle indices](#tindices) and increases the size of the vertex buffer to the size of the array of [triangle vertices](#tvertex) by using the coordinate vertex duplicating.
### Arguments

- *int* **surface** - Mesh surface number.

## int removeIndices ( int surface = -1 )

Clears the coordinate and [triangle indices](#tindices) of the given surface.
### Arguments

- *int* **surface** - The mesh surface number. -1 means all of the mesh surfaces.

### Return value

1 if the indices were cleared successfully; otherwise, 0.
## int save ( string path )

Saves the given mesh in the *[MESH](../../../code/formats/file_formats.md#mesh_ff)* file format. Creates the given mesh path if it doesn't exist yet (including subdirectories).
### Arguments

- *string* **path** - Path to the mesh including the file name and extension � `*.mesh`.

### Return value

1 if the mesh is saved successfully; otherwise, 0.
## void sortSurfaces ( )

Sort all surfaces by their names.
## int hasSpatialTree ( int surface )

Returns the value indicating if the specified mesh surface has a spatial tree.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

**1** if the mesh has a spatial tree, otherwise **0**.
## void createSpatialTree ( int surface = -1 )

Generates a spatial tree for the mesh (or its specified surface), if it doesn't have any.
### Arguments

- *int* **surface** - Mesh surface number.

## int hasEdges ( int surface = -1 )

Checks whether edge data has been generated for the specified surface. If -1 is passed, checks all surfaces.
### Arguments

- *int* **surface** - Index of the surface to check. If -1 is passed, all surfaces will be updated.

### Return value


true if edge data exists, or if the surface has no geometry (empty edges are assumed).


false if the surface has geometry, but no edge data has been generated.


## void createEdges ( int surface = -1 )

Generates edge data for the specified surface. If -1 is passed, edge data will be generated for all surfaces.
### Arguments

- *int* **surface** - Index of the surface to check. Index of the surface. If -1 is passed, the operation will be performed for all surfaces.

## void clearCollisionData ( int surface = -1 , int flags = COLLISION_DATA_ALL )

Clears the specified types of collision data for the given surface. The behavior is controlled by the flags parameter, which determines which data types to clear. If -1 is passed for the surface parameter, the operation will be performed for all surfaces.
### Arguments

- *int* **surface** - Index of the surface. If -1 is passed, collision data will be cleared for all surfaces.
- *int* **flags** - Bitmask that specifies which [types of collision data](#COLLISION_DATA_BOUNDS) to clear.

## void createCollisionData ( int surface = -1 , int flags = COLLISION_DATA_ALL )


Generates specified types of collision data for the given surface. The behavior is controlled by the flags parameter, which determines which data types are created.


> **Notice:** This method **must** be called after **any** modification of mesh geometry.
>
>
> Otherwise, intersections and collisions may produce **incorrect results** due to outdated internal mesh structures.


### Arguments

- *int* **surface** - Index of the surface to process. If -1 is passed, all surfaces will be updated.
- *int* **flags** - Bitmask that specifies which [types of collision data](#COLLISION_DATA_BOUNDS) to generate.

## int hasCollisionData ( int surface = -1 , int flags = COLLISION_DATA_ALL )


Checks whether the specified types of collision data exist for the given surface. The check is controlled by the flags parameter, which indicates which data types to validate. If -1 is passed for surface parameter, checks all surfaces in the mesh.


This method does not validate geometry content. Instead, if a surface lacks valid geometry (e.g., no indices, empty targets), it is treated as not requiring collision data, and the function returns true.


### Arguments

- *int* **surface** - Index of the surface to check. If -1 is passed, all surfaces in the mesh are checked.
- *int* **flags** - Bitmask that specifies which [types of collision data](#COLLISION_DATA_BOUNDS) to check.

### Return value

Returns true if collision data exists, or surface has no valid geometry, false otherwise.
## void clearSurface ( int surface = -1 )

Clears vertex data for the specified surface. If -1 is passed, all surfaces will be cleared.
### Arguments

- *int* **surface** - Index of the surface to clear. If -1 is passed, all surfaces will be cleared.

## int getRandomPoint ( vec3 & ret_point , vec3 & ret_normal , vec3 & ret_velocity , int surface )

Generates a random point on the specified surface, along with its normal. The velocity is always set to zero.
### Arguments

- *vec3 &* **ret_point** - Generated point on the surface.
- *vec3 &* **ret_normal** - Interpolated normal at the point.
- *vec3 &* **ret_velocity** - Always zero.
- *int* **surface** - Index of the surface to generate the random point on.

### Return value

Returns true if a valid surface was found and the point was generated, false otherwise.
## void clearSpatialTree ( int surface = -1 )

Clears the spatial tree data for the specified surface. If -1 is passed, the spatial tree will be cleared for all surfaces.
### Arguments

- *int* **surface** - Index of the surface. If -1 is passed, spatial trees will be cleared for all surfaces in the mesh.

## void clearEdges ( int surface = -1 )

Clears edge data for the specified surface. If -1 is passed, edge data will be cleared for all surfaces in the mesh.
### Arguments

- *int* **surface** - Index of the surface. If -1 is passed, edge data will be cleared for all surfaces in the mesh.
