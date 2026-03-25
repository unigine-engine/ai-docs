# Skeleton and Animation File Formats


UNIGINE uses the following file formats for skeletal animation data:


- `*.skeleton` - skeleton joint hierarchy, bind pose, blend masks, and retargeting data. Shared by `*.mesh_skinned` and `*.anim` files.
- `*.anim` - skeletal animation (keyframed joint transforms over time) that references a shared `*.skeleton`.


When importing an animated character (e.g. from FBX), the importer produces a `*.skeleton` file from the joint hierarchy and bind pose, and one or more `*.anim` files for each animation clip. Multiple skinned meshes and animations can share the same `*.skeleton` file if their rigs are compatible.


Here are some general notes that are valid for any of the formats listed above.


- All data is in the little-endian notation.
- *float* is a 32-bit IEEE754 floating-point type. It has a range of **3.4 e-38** to **3.4 e+38**.
- *int* here is a compact signed integer. > **Notice:** To read / write compact integer values use *[readInt2()](../../api/library/common/class.stream_cpp.md#readInt2_int)* / *[writeInt2()](../../api/library/common/class.stream_cpp.md#writeInt2_int_int)* methods respectively.
- *int32* is a signed 32-bit two's complement integer. It has a range of **-2,147,483,648** to **2,147,483,647**.
- *short* is a signed 16-bit integer. It has a range of **-32,768** to **32,767**.
- *char* is a signed 8-bit two's complement integer. It has a range of **-128** to **127**.
- *bool* is an 8-bit boolean value (**0** or **1**).
- *string* must be null terminated. The string size should include this terminating null character.


## Storing Skeletons


**SKELETON** is a file format that defines the skeletal rig of a character. It stores the joint hierarchy (names, parent-child relationships), bind pose transforms, blend masks for partial animation blending, blend time and weight profiles, and retargeting data for transferring animations between different skeletons. A single `*.skeleton` file acts as a shared resource: multiple `*.mesh_skinned` and `*.anim` files can reference the same skeleton if their rigs are compatible.


### SKELETON File Format


1. File format identifier (*int32* **"sn10"** (**'s'** | (**'n' << 8**) | (**'1' << 16**) | (**'0' << 24**)))
2. Number of joints (*int32*)
3. Header information for each joint: <details> <summary>View Data | Show</summary> - Name of the joint. It is a null-terminated *string* that contains: 1. The number of characters in the string including the null character (*[int](#c_int)*). 2. Joint name of the specified length (*char[length]*). - Parent of the joint. In case of the root joint without a parent, **-1** is used. (*short*) </details>
4. Bind pose transform for each joint: <details> <summary>View Data | Show</summary> - Joint position along X, Y, Z axes (*float[3]*) - Joint rotation quaternion (*float[4]*) - Joint scale along X, Y, Z axes (*float[3]*) </details>
5. File format identifier (*int32* **"sn10"**)
6. Number of blend masks (*int32*)
7. For each blend mask: <details> <summary>View Data | Show</summary> - Name of the blend mask. It is a null-terminated *string* that contains: 1. The number of characters in the string including the null character (*int32*). 2. Blend mask name of the specified length (*char[length]*). - Number of joint influences (*int32*) - Joint influence values (*float[num_influences]*). Values in the range **[0.0, 1.0]** define partial or complete disabling of joints. </details>
8. Number of blend time profiles (*int32*)
9. For each blend time profile: <details> <summary>View Data | Show</summary> - Name of the blend time profile. It is a null-terminated *string* that contains: 1. The number of characters in the string including the null character (*int32*). 2. Profile name of the specified length (*char[length]*). - Number of joint time scales (*int32*) - Joint time scale values (*float[num_scales]*). Value of **1.0** means normal speed, **2.0** means twice as fast, etc. </details>
10. Number of blend weight profiles (*int32*)
11. For each blend weight profile: <details> <summary>View Data | Show</summary> - Name of the blend weight profile. It is a null-terminated *string* that contains: 1. The number of characters in the string including the null character (*int32*). 2. Profile name of the specified length (*char[length]*). - Number of joint weight scales (*int32*) - Joint weight scale values (*float[num_scales]*). </details>
12. Number of translations retarget data entries (*int32*)
13. For each translations retarget data entry (one per joint): <details> <summary>View Data | Show</summary> - Retarget mode (*int32*). Possible values: **0** (Pose), **1** (Bind), **2** (Proportion). - Custom length (*float*). A negative value indicates that the default length (calculated from the bind pose) is used. </details>
14. File format identifier (*int32* **"sn10"**)


## Storing Skinned Mesh Animation


**ANIM** is a file format for skeletal animation. It stores a sequence of keyframes, each containing position, rotation, and scale transforms for a subset of skeleton joints. The format also stores the animation frame rate (FPS) and a root motion flag indicating whether the animation includes root joint translation. Each `*.anim` file references a shared `*.skeleton` file for the joint hierarchy and bind pose.


`*.anim` files are designed to be lightweight and reusable: they contain only joint transforms, no geometry data. Multiple `*.anim` files (walk cycle, idle, attack, etc.) can reference the same `*.skeleton` and be applied to any `*.mesh_skinned` that uses a compatible skeleton.


### ANIM File Format


1. File format identifier (*int32* **"an12"** (**'a'** | (**'n' << 8**) | (**'1' << 16**) | (**'2' << 24**)))
2. Number of source joints (*int32*)
3. Header information for each joint: <details> <summary>View Data | Show</summary> - Name of the joint. It is a null-terminated *string* that contains: 1. The number of characters in the string including the null character (*[int](#c_int)*). 2. Joint name of the specified length (*char[length]*) - Parent of the joint. In case of the root joint without a parent, **-1** is used. (*short*) </details>
4. Shared skeleton file reference: <details> <summary>View Data | Show</summary> - Shared skeleton file GUID. It is a null-terminated *string* that contains: 1. The number of characters in the string including the null character (*int32*). 2. GUID string of the specified length (*char[length]*). - Shared skeleton file path. It is a null-terminated *string* that contains: 1. The number of characters in the string including the null character (*int32*). 2. Path string of the specified length (*char[length]*). </details>
5. Number of animated joints (*[int](#c_int)*)
6. Indices of the joints taking part in the animation (*short[num_animated_joints]*)
7. Animation frames per second (*int32*)
8. Root motion present flag (*bool*)
9. File format identifier (*int32* **"an12"**)
10. Number of animation frames (*[int](#c_int)*)
11. Transformation data for each animated joint in each frame: <details> <summary>View Data | Show</summary> - Flag (*char*), individual bits of which determine if the current transform stores position (bit **0**), rotation (bit **1**) or scale (bit **2**) components. If a component is not flagged, a default value is used: zero position, identity rotation, or unit scale. - If the corresponding flag bit is set, for each component of the joint: 1. Position of the joint along X, Y, Z axes (*float[3]*) 2. Rotation quaternion (*float[4]*) 3. Joint scaling along X, Y, Z axes (*float[3]*) </details>
12. File format identifier (*int32* **"an12"**)
