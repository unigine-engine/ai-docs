# Unigine::ImportScene Class (CS)


This class is the top-level container for all data extracted from a source file during import. It manages the scene graph (a hierarchy of *[ImportNode](../../../../api/library/common/import/class.importnode_cs.md)* elements) and parallel collections of scene components. During import, an *[Importer](../../../../api/library/common/import/class.importer_cs.md)* populates the *ImportScene*, and then an *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_cs.md)* converts its contents into UNIGINE assets.


A scene can include the following components:


- [animations](../../../../api/library/common/import/class.importanimation_cs.md)
- [cameras](../../../../api/library/common/import/class.importcamera_cs.md)
- [lights](../../../../api/library/common/import/class.importlight_cs.md)
- [meshes](../../../../api/library/common/import/class.importmesh_cs.md)
- [skinned meshes](../../../../api/library/common/import/class.importmeshskinned_cs.md)
- [nodes](../../../../api/library/common/import/class.importnode_cs.md)
- [skeletons](../../../../api/library/common/import/class.importskeleton_cs.md)
- [materials](../../../../api/library/common/import/class.importmaterial_cs.md)
- [textures](../../../../api/library/common/import/class.importtexture_cs.md)


## ImportScene Class

### Members

---

## ImportScene ( )

Constructor. Creates an empty import scene instance.
## int GetNumNodes ( )

Returns the total number of nodes in the imported scene.
### Return value

Number of nodes in the imported scene.
## ImportNode GetNode ( int i )

Returns a node contained in the imported scene by its index.
### Arguments

- *int* **i** - Scene node index, in the range from 0 to ([total number of nodes in the scene](#getNumNodes_int) - 1).

### Return value

Scene node with the specified index (*[ImportNode](../../../../api/library/common/import/class.importnode_cs.md)* class instance if it exists).
## ImportNode AddNode ( ImportNode parent )

Adds a new node as an attribute to the specified scene graph node and returns the corresponding *[ImportNode](../../../../api/library/common/import/class.importnode_cs.md)* instance.
### Arguments

- *[ImportNode](../../../../api/library/common/import/class.importnode_cs.md)* **parent** - Scene graph node to add a new node to.

### Return value

New added *[ImportNode](../../../../api/library/common/import/class.importnode_cs.md)* class instance.
## bool RemoveNode ( ImportNode node )

Removes the specified scene graph node.
### Arguments

- *[ImportNode](../../../../api/library/common/import/class.importnode_cs.md)* **node** - Scene graph node to be removed.

### Return value

true if the specified scene graph node was successfully removed from the scene; otherwise false.
## int GetNumMeshes ( )

Returns the total number of meshes in the imported scene.
### Return value

Number of meshes in the imported scene.
## ImportMesh GetMesh ( int i )

Returns a mesh contained in the imported scene by its index.
### Arguments

- *int* **i** - Mesh index, in the range from 0 to ([total number of meshes in the scene](#getNumMeshes_int) - 1).

### Return value

Mesh with the specified index (*[ImportMesh](../../../../api/library/common/import/class.importmesh_cs.md)* class instance if it exists).
## ImportMesh AddMesh ( ImportNode node )

Adds a new mesh as an attribute to the specified imported node and returns the corresponding *[ImportMesh](../../../../api/library/common/import/class.importmesh_cs.md)* instance.
### Arguments

- *[ImportNode](../../../../api/library/common/import/class.importnode_cs.md)* **node** - Scene graph node to add a new mesh to.

### Return value

New added *[ImportMesh](../../../../api/library/common/import/class.importmesh_cs.md)* class instance.
## void RemoveMesh ( ImportMesh mesh )

Removes the specified mesh from the list of meshes of the imported scene.
### Arguments

- *[ImportMesh](../../../../api/library/common/import/class.importmesh_cs.md)* **mesh** - Mesh to be removed.

## int GetNumMeshSkinneds ( )

Returns the total number of skinned meshes in the imported scene.
### Return value

Number of skinned meshes in the imported scene.
## ImportMeshSkinned GetMeshSkinned ( int i )

Returns a skinned mesh contained in the imported scene by its index.
### Arguments

- *int* **i** - Skinned mesh index, in the range from 0 to ([total number of skinned meshes in the scene](#getNumMeshSkinneds_int) - 1).

### Return value

Skinned mesh with the specified index (*[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cs.md)* class instance if it exists).
## ImportMeshSkinned AddMeshSkinned ( ImportNode node )

Adds a new skinned mesh as an attribute to the specified imported node and returns the corresponding *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cs.md)* instance.
### Arguments

- *[ImportNode](../../../../api/library/common/import/class.importnode_cs.md)* **node** - Scene graph node to add a new skinned mesh to.

### Return value

New added *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cs.md)* class instance.
## void RemoveMeshSkinned ( ImportMeshSkinned mesh_skinned )

Removes the specified skinned mesh from the list of skinned meshes of the imported scene.
### Arguments

- *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cs.md)* **mesh_skinned** - Skinned mesh to be removed.

## int GetNumLights ( )

Returns the total number of lights in the imported scene.
### Return value

Number of lights in the imported scene.
## ImportLight GetLight ( int i )

Returns a light source contained in the imported scene by its index.
### Arguments

- *int* **i** - Light source index, in the range from 0 to ([total number of lights in the scene](#getNumLights_int) - 1).

### Return value

Light source with the specified index (*[ImportLight](../../../../api/library/common/import/class.importlight_cs.md)* class instance if it exists).
## ImportLight AddLight ( ImportNode node )

Adds a new light as an attribute to the specified imported node and returns the corresponding *[ImportLight](../../../../api/library/common/import/class.importlight_cs.md)* instance.
### Arguments

- *[ImportNode](../../../../api/library/common/import/class.importnode_cs.md)* **node** - Scene graph node to add a light source to.

### Return value

New added *[ImportLight](../../../../api/library/common/import/class.importlight_cs.md)* class instance.
## void RemoveLight ( ImportLight light )

Removes the specified light source from the list of light sources of the imported scene.
### Arguments

- *[ImportLight](../../../../api/library/common/import/class.importlight_cs.md)* **light** - Lights source to be removed.

## int GetNumCameras ( )

Returns the total number of cameras in the imported scene.
### Return value

Number of cameras in the imported scene.
## ImportCamera GetCamera ( int i )

Returns a camera contained in the imported scene by its index.
### Arguments

- *int* **i** - Camera index, in the range from 0 to ([total number of cameras in the scene](#getNumCameras_int) - 1).

### Return value

Camera with the specified index (*[ImportCamera](../../../../api/library/common/import/class.importcamera_cs.md)* class instance if it exists).
## ImportCamera AddCamera ( ImportNode node )

Adds a new camera as an attribute to the specified imported node and returns the corresponding *[ImportCamera](../../../../api/library/common/import/class.importcamera_cs.md)* instance.
### Arguments

- *[ImportNode](../../../../api/library/common/import/class.importnode_cs.md)* **node** - Scene graph node to add a new camera to.

### Return value

New added *[ImportCamera](../../../../api/library/common/import/class.importcamera_cs.md)* class instance.
## void RemoveCamera ( ImportCamera camera )

Removes the specified camera from the scene.
### Arguments

- *[ImportCamera](../../../../api/library/common/import/class.importcamera_cs.md)* **camera** - Camera to be removed.

## int GetNumAnimations ( )

Returns the total number of animations in the imported scene.
### Return value

Number of animations in the imported scene.
## ImportAnimation GetAnimation ( int i )

Returns an animation contained in the imported scene by its index.
### Arguments

- *int* **i** - Animation index, in the range from 0 to ([total number of animations in the scene](#getNumAnimations_int) - 1).

### Return value

Animation with the specified index (*[ImportAnimation](../../../../api/library/common/import/class.importanimation_cs.md)* class instance if it exists).
## ImportAnimation AddAnimation ( )

Adds a given animation to the scene and returns an instance of the added animation.
### Return value

New added *[ImportAnimation](../../../../api/library/common/import/class.importanimation_cs.md)* class instance.
## void RemoveAnimation ( ImportAnimation animation )

Removes the specified animation from the scene.
### Arguments

- *[ImportAnimation](../../../../api/library/common/import/class.importanimation_cs.md)* **animation** - Animation to be removed.

## int GetNumSkeletons ( )

Returns the total number of skeletons in the imported scene.
### Return value

Number of skeletons in the imported scene.
## ImportSkeleton GetSkeleton ( int i )

Returns a skeleton contained in the imported scene by its index.
### Arguments

- *int* **i** - Skeleton index, in the range from 0 to ([total number of skeletons in the scene](#getNumSkeletons_int) - 1).

### Return value

Skeleton with the specified index (*[ImportSkeleton](../../../../api/library/common/import/class.importskeleton_cs.md)* class instance if it exists).
## ImportSkeleton AddSkeleton ( )

Adds a new skeleton to the scene and returns the corresponding *[ImportSkeleton](../../../../api/library/common/import/class.importskeleton_cs.md)* instance.
### Return value

New added *[ImportSkeleton](../../../../api/library/common/import/class.importskeleton_cs.md)* class instance.
## void RemoveSkeleton ( ImportSkeleton skeleton )

Removes the specified skeleton from the scene.
### Arguments

- *[ImportSkeleton](../../../../api/library/common/import/class.importskeleton_cs.md)* **skeleton** - Skeleton to be removed.

## int GetNumMaterials ( )

Returns the total number of materials in the imported scene.
### Return value

Number of materials in the imported scene.
## ImportMaterial GetMaterial ( int i )

Returns a material contained in the imported scene by its index.
### Arguments

- *int* **i** - Material index, in the range from 0 to ([total number of materials in the scene](#getNumMaterials_int) - 1).

### Return value

Material with the specified index (*[ImportMaterial](../../../../api/library/common/import/class.importmaterial_cs.md)* class instance if it exists).
## ImportMaterial AddMaterial ( )

Adds a given material to the scene and returns an instance of the added material.
### Return value

New added *[ImportMaterial](../../../../api/library/common/import/class.importmaterial_cs.md)* class instance.
## ImportMaterial GetMaterial ( string name )

Returns a material contained in the imported scene by its name.
### Arguments

- *string* **name** - Material name.

### Return value

Material with the specified name (*[ImportMaterial](../../../../api/library/common/import/class.importmaterial_cs.md)* class instance if it exists).
## void ReplaceMaterial ( ImportMaterial old_material , ImportMaterial new_material )

Replaces the specified material contained in the imported scene with another one.
### Arguments

- *[ImportMaterial](../../../../api/library/common/import/class.importmaterial_cs.md)* **old_material** - Material to be replaced.
- *[ImportMaterial](../../../../api/library/common/import/class.importmaterial_cs.md)* **new_material** - New material to replace the initial one.

## void RemoveMaterial ( ImportMaterial material )

Removes the specified material from the scene.
### Arguments

- *[ImportMaterial](../../../../api/library/common/import/class.importmaterial_cs.md)* **material** - Material to be removed.

## int GetNumTextures ( )

Returns the total number of textures in the imported scene.
### Return value

Number of textures in the imported scene.
## ImportTexture GetTexture ( int i )

Returns a texture contained in the imported scene by its index.
### Arguments

- *int* **i** - Texture index, in the range from 0 to ([total number of textures in the scene](#getNumTextures_int) - 1).

### Return value

Texture with the specified index (*[ImportTexture](../../../../api/library/common/import/class.importtexture_cs.md)* class instance if it exists).
## ImportTexture GetTexture ( string filepath )

Returns a texture contained in the imported scene by its file path.
### Arguments

- *string* **filepath** - Texture file path.

### Return value

Texture with the specified file path (*[ImportTexture](../../../../api/library/common/import/class.importtexture_cs.md)* class instance if it exists).
## ImportTexture FindTexture ( string filepath )

Returns a texture contained in the imported scene by its file path.
### Arguments

- *string* **filepath** - Texture file path.

### Return value

Texture with the specified file path (*[ImportTexture](../../../../api/library/common/import/class.importtexture_cs.md)* class instance if it exists).
