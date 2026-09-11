# Mesh File Formats


UNIGINE uses the following file formats for mesh geometry:


- `*.mesh` - static, non-deformable geometry.
- `*.mesh_skinned` - skinned geometry with morph targets and vertex weights. Each `*.mesh_skinned` file references a shared `*.skeleton` file that defines the joint hierarchy and bind pose.


See also [Skeleton and Animation File Formats](../../code/formats/animations_formats.md) for the related `*.skeleton` and `*.anim` formats.


Here are some general notes that are valid for any of the formats listed above.


- All data is in the little-endian notation.
- *float* is a 32-bit IEEE754 floating-point type. It has a range of **3.4 e-38** to **3.4 e+38**.
- *int* here is a compact signed integer. > **Notice:** To read / write compact integer values use *[readInt2()](../../api/library/common/class.stream_cpp.md#readInt2_int)* / *[writeInt2()](../../api/library/common/class.stream_cpp.md#writeInt2_int_int)* methods respectively.
- *int32* is a signed 32-bit two's complement integer. It has a range of **�2,147,483,648** to **2,147,483,647**.
- *long* is a signed 64-bit integer.
- *short* is a signed 16-bit integer. It has a range of **-32,768** to **32,767**.
- *unsigned short* is an unsigned 16-bit integer. It has a range of **0** to **65,535**.
- *char* is a signed 8-bit two's complement integer. It has a range of **-128** to **127**.
- *unsigned char* is a 8-bit unsigned integer. It has a range of **0** to **255**.
- *bool* is an 8-bit boolean value (**0** or **1**).
- *string* must be null terminated. The string size should include this terminating null character.
- Mesh formats (`*.mesh` and `*.mesh_skinned`) allow multiple surfaces.


The **mesh limitations** set in UNIGINE:


| Maximum number of **vertices** per mesh | 2,147,483,647 |
|---|---|
| Maximum number of **surfaces** per mesh | 32,767 |
| Maximum amount of **weights** per vertex (`*.mesh_skinned`) | 4 |


### Compression and Decompression of Tangents


**Compression** of normalized floating-point tangents into *short* format is performed in the following way:


```cpp
x = (short)(clamp((int)(tangent.x * 32767.0f), -32767, 32767));
y = (short)(clamp((int)(tangent.y * 32767.0f), -32767, 32767));
z = (short)(clamp((int)(tangent.z * 32767.0f), -32767, 32767));
w = (short)(clamp((int)(tangent.w * 32767.0f), -32767, 32767));

```


Here:


- *tangent* is a normalized float tangent.
- *x*, *y*, *z* and *w* are short compressed tangent values.


**Decompression** of tangents that are compressed into the *short* format can be performed as follows:


```cpp
tangent.x = (compressed_tangent.x / 32767.0f);
tangent.y = (compressed_tangent.y / 32767.0f);
tangent.z = (compressed_tangent.z / 32767.0f);
tangent.w = (compressed_tangent.w / 32767.0f);

```


Here:


- *compressed_tangent* is a short compressed tangent.
- *tangent* is a normalized float tangent.


### Compression and Decompression of Weights


**Compression** of normalized floating-point weights into *unsigned short* format is performed in the following way:


```cpp
w = (unsigned short)clamp((int)(weight * 65535.0f), 0, 65535);

```


Here:


- *weight* is a normalized float weight.
- *w* is unsigned short compressed weight.


**Decompression** of weights that are compressed into the *unsigned short* format can be performed as follows:


```cpp
weight = compression_weight / 65535.0f;

```


Here:


- *compression_weight* is an unsigned short compressed weight.
- *weight* is a normalized float weight.


## Storing Meshes


**MESH** is a file format for static, non-deformable geometry used for environment props, buildings, terrain, and other objects that do not require skeletal animation or morph targets. The format stores vertices, tangents, texture coordinates, vertex colors, and collision data (edges, spatial tree) for each surface.


### MESH File Format


1. File format identifier (*int32* **"ms15"** (**'m'** | (**'s' << 8**) | (**'1' << 16**) | (**'5' << 24**)))
2. Spatial tree triangles (*[int](#c_int)*)
3. Bounding volume of the whole mesh: <details> <summary>View Data | Show</summary> - Mesh bounding box minimum (*float[3]*) - Mesh bounding box maximum (*float[3]*) - Mesh bounding sphere center (*float[3]*) - Mesh bounding sphere radius (*float*) </details>
4. Number of surfaces (*[int](#c_int)*)
5. Header information for each surface: <details> <summary>View Data | Show</summary> - Name of the surface. It is a null-terminated *string* that contains: 1. The number of characters in the string including the null character (*[int](#c_int)*). 2. Surface name of the specified length (*char[length]*) - UV channel used for the surface lightmap (*char*) - Surface lightmap resolution (*char*) - Number of coordinate indices for surface (*[int](#c_int)*) - Number of triangle indices for surface (*[int](#c_int)*) - Surface bounding box minimum (*float[3]*) - Surface bounding box maximum (*float[3]*) - Surface bounding sphere center (*float[3]*) - Surface bounding sphere radius (*float*) - Number of surface vertices (*[int](#c_int)*) </details>
6. Estimated RAM memory usage in bytes (*long*)
7. File format identifier (*int32* **"ms15"**)
8. Data on each surface geometry: > **Notice:** The actual surface geometry data is not stored directly in structured form. Instead, it is serialized into a **[Blob](../../api/library/common/class.blob_cpp.md)**, then compressed using a **[LZ4](../../api/library/common/class.compress_cpp.md#lz4Compress_void_ptr_size_t_ref_const_void_ptr_size_t_bool_bool)** compression algorithm and stored as follows: > - Uncompressed size (8 bytes) > - Compressed size (8 bytes) > - Compressed data (n bytes) <details> <summary>View Data | Show</summary> - Surface vertex data: 1. Vertices of the surface (*float[3*num_vertex]*), where *num_vertex* is the number of surface vertices specified in the header. 2. Number of tangents (*[int](#c_int)*) 3. For each tangent: - X, Y, Z, and W components are of the *short* type and represent a quaternion. - Number of texture coordinates in the 1st UV set (*[int](#c_int)*) - For each of texture coordinates: 1. 1st UV texture coordinates (*float[2]*) - Number of texture coordinates in the 2nd UV set (*[int](#c_int)*) - For each of texture coordinates: 1. 2nd UV texture coordinates (*float[2]*) - Number of 8-bit vertex colors (*[int](#c_int)*). - For each color: 1. Color value (*unsigned char[4]*) - Coordinate indices for each vertex of the surface. The number of indices is specified in the header. 1. If the surface contains less than 256 coordinate vertices, all the indices are *unsigned char[length]* 2. If the surface contains less than 65536 coordinate vertices, all the indices are *unsigned short[length]* 3. Otherwise, all the indices are *[int](#c_int)[length]* - Triangle indices for each vertex of the surface. The number of indices is specified in the header. 1. If the surface contains less than 256 triangle vertices, all the indices are *unsigned char[length]* 2. If the surface contains less than 65536 triangle vertices, all the indices are *unsigned short[length]* 3. Otherwise, all the indices are *[int](#c_int)[length]* </details>
9. File format identifier (*int32* **"ms15"**)
10. Edges and Spatial tree for each surface: > **Notice:** The actual edges and spatial tree data for each surface is not stored directly in structured form. Instead, it is serialized into a **[Blob](../../api/library/common/class.blob_cpp.md)**, then compressed using a **[LZ4](../../api/library/common/class.compress_cpp.md#lz4Compress_void_ptr_size_t_ref_const_void_ptr_size_t_bool_bool)** compression algorithm and stored as follows: > - Uncompressed size (8 bytes) > - Compressed size (8 bytes) > - Compressed data (n bytes)

  1. Edges: <details> <summary>View Data | Show</summary> - The number of edges (*[int](#c_int)*) - All the edges data for the surface (*char* for each edge) </details>
  2. Spatial tree: <details> <summary>View Data | Show</summary> - The number of node indices for spatial tree (*[int](#c_int)*) - Each node index of the Spatial tree (*[int](#c_int)*) - The number of nodes in the Spatial tree (*[int](#c_int)*) - For each node of the Spatial tree: splitting axis (*char*), indices of left and right children, start offset and end offset in node indices array. (*[int](#c_int)*) - For each node of the Spatial tree: node bounding box minimum and maximum (*float[3]*) - For each node of the Spatial tree: node split distance (*float*) </details>
11. File format identifier (*int32* **"ms15"**)
12. An offset for each surface, pointing to the beginning of its compressed data block in the file. (*long*)
13. File format identifier (*int32* **"ms15"**)


## Storing Skinned Meshes


**MESH_SKINNED** is a file format for geometry that can be deformed by a skeleton, used for animated characters, creatures, and any objects driven by skeletal animation. The format stores vertices, tangents, texture coordinates, vertex colors, morph targets (blend shapes), and per-vertex skinning weights (up to 4 joints per vertex). Each `*.mesh_skinned` file references a shared `*.skeleton` file that defines the joint hierarchy and bind pose.


### MESH_SKINNED File Format


1. File format identifier (*int32* **"sk10"** (**'s'** | (**'k' << 8**) | (**'1' << 16**) | (**'0' << 24**)))
2. Spatial tree triangles (*[int](#c_int)*)
3. Bounding volume of the whole mesh: <details> <summary>View Data | Show</summary> - Mesh bounding box minimum (*float[3]*) - Mesh bounding box maximum (*float[3]*) - Mesh bounding sphere center (*float[3]*) - Mesh bounding sphere radius (*float*) </details>
4. Number of joints (*int32*)
5. Header information for each joint: <details> <summary>View Data | Show</summary> - Name of the joint. It is a null-terminated *string* that contains: 1. The number of characters in the string including the null character (*[int](#c_int)*). 2. Joint name of the specified length (*char[length]*). - Parent of the joint. In case of the root joint without a parent, **-1** is used. (*short*) </details>
6. Number of bind transforms (*int32*)
7. Bind pose transform for each joint: <details> <summary>View Data | Show</summary> - Joint position along X, Y, Z axes (*float[3]*) - Joint rotation quaternion (*float[4]*) - Joint scale along X, Y, Z axes (*float[3]*) </details>
8. Number of rest transforms (*int32*)
9. Rest pose transform for each joint (same structure as bind transforms): <details> <summary>View Data | Show</summary> - Joint position along X, Y, Z axes (*float[3]*) - Joint rotation quaternion (*float[4]*) - Joint scale along X, Y, Z axes (*float[3]*) </details>
10. Shared skeleton file reference: <details> <summary>View Data | Show</summary> - Shared skeleton file GUID. It is a null-terminated *string* that contains: 1. The number of characters in the string including the null character (*int32*). 2. GUID string of the specified length (*char[length]*). - Shared skeleton file path. It is a null-terminated *string* that contains: 1. The number of characters in the string including the null character (*int32*). 2. Path string of the specified length (*char[length]*). </details>
11. Number of surfaces (*[int](#c_int)*)
12. Header information for each surface: <details> <summary>View Data | Show</summary> - Name of the surface. It is a null-terminated *string* that contains: 1. The number of characters in the string including the null character (*[int](#c_int)*). 2. Surface name of the specified length (*char[length]*) - Number of coordinate indices for surface (*[int](#c_int)*) - Number of triangle indices for surface (*[int](#c_int)*) - Surface bounding box minimum (*float[3]*) - Surface bounding box maximum (*float[3]*) - Surface bounding sphere center (*float[3]*) - Surface bounding sphere radius (*float*) - Number of the surface morph targets (*[int](#c_int)*) - Header information for each morph target: 1. Name of the morph target. It is a null-terminated *string* that contains: - The number of characters in the string including the null character (*[int](#c_int)*). - Morph target name of the specified length (*char[length]*) 2. Number of vertices (*[int](#c_int)*) </details>
13. Estimated RAM memory usage in bytes (*long*)
14. File format identifier (*int32* **"sk10"**)
15. Data on each surface geometry: > **Notice:** The actual surface geometry data is not stored directly in structured form. Instead, it is serialized into a **[Blob](../../api/library/common/class.blob_cpp.md)**, then compressed using a **[LZ4](../../api/library/common/class.compress_cpp.md#lz4Compress_void_ptr_size_t_ref_const_void_ptr_size_t_bool_bool)** compression algorithm and stored as follows: > - Uncompressed size (8 bytes) > - Compressed size (8 bytes) > - Compressed data (n bytes) <details> <summary>View Data | Show</summary> - Data on each morph target of the surface: 1. Vertices of the morph target (*float[3*num_vertex]*), where *num_vertex* is specified in the morph target header. 2. Number of tangents (*[int](#c_int)*) 3. For each tangent: - X, Y, Z, and W components are of the *short* type and represent a quaternion. - Number of surface weights (*[int](#c_int)*) - For each surface weight: 1. Number of joints that affect the vertex (the maximum value is 4) (*unsigned char*) 2. For each joint that affects the vertex: - Joint index (*short*) - Joint weight (*unsigned short*) - Number of texture coordinates in the 1st UV set (*[int](#c_int)*) - For each of texture coordinates: 1. 1st UV texture coordinates (*float[2]*) - Number of texture coordinates in the 2nd UV set (*[int](#c_int)*) - For each of texture coordinates: 1. 2nd UV texture coordinates (*float[2]*) - Number of 8-bit vertex colors (*[int](#c_int)*). - For each color: 1. Color value (*unsigned char[4]*) - Coordinate indices for each vertex of the surface. The number of indices is specified in the header. 1. If the zero morph target contains less than 256 coordinate vertices, all the indices are *unsigned char[length]* 2. If the zero morph target contains less than 65536 coordinate vertices, all the indices are *unsigned short[length]* 3. Otherwise, all the indices are *[int](#c_int)[length]* - Triangle indices for each vertex of the surface. The number of indices is specified in the header. 1. If the zero morph target contains less than 256 triangle vertices, all the indices are *unsigned char[length]* 2. If the zero morph target contains less than 65536 triangle vertices, all the indices are *unsigned short[length]* 3. Otherwise, all the indices are *[int](#c_int)[length]* </details>
16. File format identifier (*int32* **"sk10"**)
17. An offset for each surface, pointing to the beginning of its compressed data block in the file. (*long*)
18. File format identifier (*int32* **"sk10"**)
