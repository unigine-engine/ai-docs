# Unigine::ImportScene Class (CPP)

**Header:** #include <UnigineImport.h>


This class is the top-level container for all data extracted from a source file during import. It manages the scene graph (a hierarchy of *[ImportNode](../../../../api/library/common/import/class.importnode_cpp.md)* elements) and parallel collections of scene components. During import, an *[Importer](../../../../api/library/common/import/class.importer_cpp.md)* populates the *ImportScene*, and then an *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_cpp.md)* converts its contents into UNIGINE assets.


A scene can include the following components:


- [animations](../../../../api/library/common/import/class.importanimation_cpp.md)
- [cameras](../../../../api/library/common/import/class.importcamera_cpp.md)
- [lights](../../../../api/library/common/import/class.importlight_cpp.md)
- [meshes](../../../../api/library/common/import/class.importmesh_cpp.md)
- [skinned meshes](../../../../api/library/common/import/class.importmeshskinned_cpp.md)
- [nodes](../../../../api/library/common/import/class.importnode_cpp.md)
- [skeletons](../../../../api/library/common/import/class.importskeleton_cpp.md)
- [materials](../../../../api/library/common/import/class.importmaterial_cpp.md)
- [textures](../../../../api/library/common/import/class.importtexture_cpp.md)


## ImportScene Class

---

## static ImportScenePtr create ( )

Constructor. Creates an empty import scene instance.
## int getNumNodes ( ) const

Returns the total number of nodes in the imported scene.
### Return value

Number of nodes in the imported scene.
## Ptr < ImportNode > getNode ( int i ) const

Returns a node contained in the imported scene by its index.
### Arguments

- *int* **i** - Scene node index, in the range from 0 to ([total number of nodes in the scene](#getNumNodes_int) - 1).

### Return value

Scene node with the specified index (*[ImportNode](../../../../api/library/common/import/class.importnode_cpp.md)* class instance if it exists).
## Ptr < ImportNode > addNode ( const Ptr < ImportNode > & parent )

Adds a new node as an attribute to the specified scene graph node and returns the corresponding *[ImportNode](../../../../api/library/common/import/class.importnode_cpp.md)* instance.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportNode](../../../../api/library/common/import/class.importnode_cpp.md)> &* **parent** - Scene graph node to add a new node to.

### Return value

New added *[ImportNode](../../../../api/library/common/import/class.importnode_cpp.md)* class instance.
## bool removeNode ( const Ptr < ImportNode > & node )

Removes the specified scene graph node.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportNode](../../../../api/library/common/import/class.importnode_cpp.md)> &* **node** - Scene graph node to be removed.

### Return value

true if the specified scene graph node was successfully removed from the scene; otherwise false.
## int getNumMeshes ( ) const

Returns the total number of meshes in the imported scene.
### Return value

Number of meshes in the imported scene.
## Ptr < ImportMesh > getMesh ( int i ) const

Returns a mesh contained in the imported scene by its index.
### Arguments

- *int* **i** - Mesh index, in the range from 0 to ([total number of meshes in the scene](#getNumMeshes_int) - 1).

### Return value

Mesh with the specified index (*[ImportMesh](../../../../api/library/common/import/class.importmesh_cpp.md)* class instance if it exists).
## Ptr < ImportMesh > addMesh ( const Ptr < ImportNode > & node )

Adds a new mesh as an attribute to the specified imported node and returns the corresponding *[ImportMesh](../../../../api/library/common/import/class.importmesh_cpp.md)* instance.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportNode](../../../../api/library/common/import/class.importnode_cpp.md)> &* **node** - Scene graph node to add a new mesh to.

### Return value

New added *[ImportMesh](../../../../api/library/common/import/class.importmesh_cpp.md)* class instance.
## void removeMesh ( const Ptr < ImportMesh > & mesh )

Removes the specified mesh from the list of meshes of the imported scene.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportMesh](../../../../api/library/common/import/class.importmesh_cpp.md)> &* **mesh** - Mesh to be removed.

## int getNumMeshSkinneds ( ) const

Returns the total number of skinned meshes in the imported scene.
### Return value

Number of skinned meshes in the imported scene.
## Ptr < ImportMeshSkinned > getMeshSkinned ( int i ) const

Returns a skinned mesh contained in the imported scene by its index.
### Arguments

- *int* **i** - Skinned mesh index, in the range from 0 to ([total number of skinned meshes in the scene](#getNumMeshSkinneds_int) - 1).

### Return value

Skinned mesh with the specified index (*[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cpp.md)* class instance if it exists).
## Ptr < ImportMeshSkinned > addMeshSkinned ( const Ptr < ImportNode > & node )

Adds a new skinned mesh as an attribute to the specified imported node and returns the corresponding *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cpp.md)* instance.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportNode](../../../../api/library/common/import/class.importnode_cpp.md)> &* **node** - Scene graph node to add a new skinned mesh to.

### Return value

New added *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cpp.md)* class instance.
## void removeMeshSkinned ( const Ptr < ImportMeshSkinned > & mesh_skinned )

Removes the specified skinned mesh from the list of skinned meshes of the imported scene.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cpp.md)> &* **mesh_skinned** - Skinned mesh to be removed.

## int getNumLights ( ) const

Returns the total number of lights in the imported scene.
### Return value

Number of lights in the imported scene.
## Ptr < ImportLight > getLight ( int i ) const

Returns a light source contained in the imported scene by its index.
### Arguments

- *int* **i** - Light source index, in the range from 0 to ([total number of lights in the scene](#getNumLights_int) - 1).

### Return value

Light source with the specified index (*[ImportLight](../../../../api/library/common/import/class.importlight_cpp.md)* class instance if it exists).
## Ptr < ImportLight > addLight ( const Ptr < ImportNode > & node )

Adds a new light as an attribute to the specified imported node and returns the corresponding *[ImportLight](../../../../api/library/common/import/class.importlight_cpp.md)* instance.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportNode](../../../../api/library/common/import/class.importnode_cpp.md)> &* **node** - Scene graph node to add a light source to.

### Return value

New added *[ImportLight](../../../../api/library/common/import/class.importlight_cpp.md)* class instance.
## void removeLight ( const Ptr < ImportLight > & light )

Removes the specified light source from the list of light sources of the imported scene.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportLight](../../../../api/library/common/import/class.importlight_cpp.md)> &* **light** - Lights source to be removed.

## int getNumCameras ( ) const

Returns the total number of cameras in the imported scene.
### Return value

Number of cameras in the imported scene.
## Ptr < ImportCamera > getCamera ( int i ) const

Returns a camera contained in the imported scene by its index.
### Arguments

- *int* **i** - Camera index, in the range from 0 to ([total number of cameras in the scene](#getNumCameras_int) - 1).

### Return value

Camera with the specified index (*[ImportCamera](../../../../api/library/common/import/class.importcamera_cpp.md)* class instance if it exists).
## Ptr < ImportCamera > addCamera ( const Ptr < ImportNode > & node )

Adds a new camera as an attribute to the specified imported node and returns the corresponding *[ImportCamera](../../../../api/library/common/import/class.importcamera_cpp.md)* instance.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportNode](../../../../api/library/common/import/class.importnode_cpp.md)> &* **node** - Scene graph node to add a new camera to.

### Return value

New added *[ImportCamera](../../../../api/library/common/import/class.importcamera_cpp.md)* class instance.
## void removeCamera ( const Ptr < ImportCamera > & camera )

Removes the specified camera from the scene.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportCamera](../../../../api/library/common/import/class.importcamera_cpp.md)> &* **camera** - Camera to be removed.

## int getNumAnimations ( ) const

Returns the total number of animations in the imported scene.
### Return value

Number of animations in the imported scene.
## Ptr < ImportAnimation > getAnimation ( int i ) const

Returns an animation contained in the imported scene by its index.
### Arguments

- *int* **i** - Animation index, in the range from 0 to ([total number of animations in the scene](#getNumAnimations_int) - 1).

### Return value

Animation with the specified index (*[ImportAnimation](../../../../api/library/common/import/class.importanimation_cpp.md)* class instance if it exists).
## Ptr < ImportAnimation > addAnimation ( )

Adds a given animation to the scene and returns an instance of the added animation.
### Return value

New added *[ImportAnimation](../../../../api/library/common/import/class.importanimation_cpp.md)* class instance.
## void removeAnimation ( const Ptr < ImportAnimation > & animation )

Removes the specified animation from the scene.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportAnimation](../../../../api/library/common/import/class.importanimation_cpp.md)> &* **animation** - Animation to be removed.

## int getNumSkeletons ( ) const

Returns the total number of skeletons in the imported scene.
### Return value

Number of skeletons in the imported scene.
## Ptr < ImportSkeleton > getSkeleton ( int i ) const

Returns a skeleton contained in the imported scene by its index.
### Arguments

- *int* **i** - Skeleton index, in the range from 0 to ([total number of skeletons in the scene](#getNumSkeletons_int) - 1).

### Return value

Skeleton with the specified index (*[ImportSkeleton](../../../../api/library/common/import/class.importskeleton_cpp.md)* class instance if it exists).
## Ptr < ImportSkeleton > addSkeleton ( )

Adds a new skeleton to the scene and returns the corresponding *[ImportSkeleton](../../../../api/library/common/import/class.importskeleton_cpp.md)* instance.
### Return value

New added *[ImportSkeleton](../../../../api/library/common/import/class.importskeleton_cpp.md)* class instance.
## void removeSkeleton ( const Ptr < ImportSkeleton > & skeleton )

Removes the specified skeleton from the scene.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportSkeleton](../../../../api/library/common/import/class.importskeleton_cpp.md)> &* **skeleton** - Skeleton to be removed.

## int getNumMaterials ( ) const

Returns the total number of materials in the imported scene.
### Return value

Number of materials in the imported scene.
## Ptr < ImportMaterial > getMaterial ( int i ) const

Returns a material contained in the imported scene by its index.
### Arguments

- *int* **i** - Material index, in the range from 0 to ([total number of materials in the scene](#getNumMaterials_int) - 1).

### Return value

Material with the specified index (*[ImportMaterial](../../../../api/library/common/import/class.importmaterial_cpp.md)* class instance if it exists).
## Ptr < ImportMaterial > addMaterial ( )

Adds a given material to the scene and returns an instance of the added material.
### Return value

New added *[ImportMaterial](../../../../api/library/common/import/class.importmaterial_cpp.md)* class instance.
## Ptr < ImportMaterial > getMaterial ( const char * name ) const

Returns a material contained in the imported scene by its name.
### Arguments

- *const char ** **name** - Material name.

### Return value

Material with the specified name (*[ImportMaterial](../../../../api/library/common/import/class.importmaterial_cpp.md)* class instance if it exists).
## void replaceMaterial ( const Ptr < ImportMaterial > & old_material , const Ptr < ImportMaterial > & new_material )

Replaces the specified material contained in the imported scene with another one.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportMaterial](../../../../api/library/common/import/class.importmaterial_cpp.md)> &* **old_material** - Material to be replaced.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportMaterial](../../../../api/library/common/import/class.importmaterial_cpp.md)> &* **new_material** - New material to replace the initial one.

## void removeMaterial ( const Ptr < ImportMaterial > & material )

Removes the specified material from the scene.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportMaterial](../../../../api/library/common/import/class.importmaterial_cpp.md)> &* **material** - Material to be removed.

## int getNumTextures ( ) const

Returns the total number of textures in the imported scene.
### Return value

Number of textures in the imported scene.
## Ptr < ImportTexture > getTexture ( int i ) const

Returns a texture contained in the imported scene by its index.
### Arguments

- *int* **i** - Texture index, in the range from 0 to ([total number of textures in the scene](#getNumTextures_int) - 1).

### Return value

Texture with the specified index (*[ImportTexture](../../../../api/library/common/import/class.importtexture_cpp.md)* class instance if it exists).
## Ptr < ImportTexture > getTexture ( const char * filepath )

Returns a texture contained in the imported scene by its file path.
### Arguments

- *const char ** **filepath** - Texture file path.

### Return value

Texture with the specified file path (*[ImportTexture](../../../../api/library/common/import/class.importtexture_cpp.md)* class instance if it exists).
## Ptr < ImportTexture > findTexture ( const char * filepath ) const

Returns a texture contained in the imported scene by its file path.
### Arguments

- *const char ** **filepath** - Texture file path.

### Return value

Texture with the specified file path (*[ImportTexture](../../../../api/library/common/import/class.importtexture_cpp.md)* class instance if it exists).
