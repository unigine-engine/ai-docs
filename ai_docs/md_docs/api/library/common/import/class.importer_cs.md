# Unigine::Importer Class (CS)


This class is used to manage a file importer. File importers are used by the Engine's [import system](../../../../api/library/common/import/index.md) to bring the data stored in various non-native formats to UNIGINE. Each importer can be used to import multiple file formats, but there shouldn't be two or more importers [registered](../../../../api/library/common/import/class.import_cs.md#registerImporter_ImporterID_cstr_ImporterCreationFunction_ImporterDeletionFunction_vptr_int_vptr) for a single file format.


Importer has a [set of flags](#IMPORT_LIGHTS) defining which scene components are to be extracted and imported. So, the importer should be [initialized](#init_cstr_int_bool) before use.


Each importer generates UNIGINE objects on the basis of metadata extracted from the imported files and uses a set of [processors](../../../../api/library/common/import/class.importprocessor_cs.md) to perform all necessary auxiliary operations (data preparation, file saving, file management, etc.). Importer allows you to add any number of pre- and post-processors. However, you can set only one processor for each scene component.


> **Notice:** This is a base class for all importers. Your custom importer class must be inherited from it.


You can customize actions to be performed when importing the whole scene as well as when importing textures, materials, meshes, animations, lights, cameras by overriding the corresponding event handler functions for your custom importer


```cpp
class MyCustomImporter : public Unigine::Importer
{
public:
	MyCustomImporter();
	virtual ~MyCustomImporter();

/*...*/

// overrides of event functions
protected:
	virtual bool onInit(const ImportScenePtr &scene, const char *filepath) override;
	virtual bool onImport(const char *output_path) override;
	virtual bool onImportTexture(const Unigine::ImportProcessor &processor, const Unigine::ImportTexturePtr &import_texture) override;
	virtual bool onImportMaterial(const Unigine::ImportProcessor &processor, const Unigine::MaterialPtr &material, const Unigine::ImportMaterial &import_material) override;
	virtual bool onImportMesh(const Unigine::ImportProcessor &processor, const Unigine::MeshPtr &mesh, const Unigine::ImportMesh &import_mesh) override;
	virtual bool onImportMeshSkinned(const Unigine::ImportProcessor &processor, const Unigine::MeshSkinnedPtr &mesh_skinned, const Unigine::ImportMeshSkinned &import_mesh_skinned) override;
	virtual bool onImportLight(const Unigine::ImportProcessor &processor, const Unigine::LightPtr &light, const Unigine::ImportLight &import_light) override;
	virtual bool onImportCamera(const Unigine::ImportProcessor &processor, const Unigine::PlayerPtr &camera, const Unigine::ImportCamera &import_camera);
	virtual bool onImportNode(const Unigine::ImportProcessor &processor, const Unigine::NodePtr &node, const Unigine::ImportNode &import_node) override;
	virtual bool onImportNodeChild(const ImportProcessorPtr &processor, const Unigine::NodePtr &node_parent, const ImportNodePtr &import_node_parent, const Unigine::NodePtr &node_child, const ImportNodePtr &import_node_child) override;
	virtual bool onImportAnimation(const Unigine::ImportProcessor &processor, const Unigine::MeshSkinnedAnimationPtr &animation, const Unigine::ImportMeshSkinned &import_mesh_skinned, const Unigine::ImportAnimation &import_animation) override;
	virtual bool onImportSkeleton(const Unigine::ImportProcessor &processor, const Unigine::SkeletonPtr &skeleton, const Unigine::ImportSkeleton &import_skeleton) override;
	virtual bool onCheckSupportedAnimation(const Unigine::ImportMeshSkinnedPtr &import_mesh_skinned, const Unigine::ImportAnimationPtr &import_animation) override;
	virtual bool onCheckDefaultAnimation(const Unigine::ImportMeshSkinnedPtr &import_mesh_skinned, const Unigine::ImportAnimationPtr &import_animation) override;

private:
	ImportScene *import_scene();
	void import_textures(const Unigine::ImportScene &scene);
	void import_materials(const Unigine::ImportScene &scene);
	void import_animations(const Unigine::ImportScene &scene);

	void process_node(const Unigine::ImportScene &import_scene, const Unigine::ImportNode &parent, fbx::FbxNode *fbx_node);
	void process_mesh(const Unigine::ImportScene &import_scene, const Unigine::ImportNode &node, fbx::FbxNode *fbx_node, fbx::FbxMesh *fbx_mesh);
	void process_light(const Unigine::ImportScene &import_scene, const Unigine::ImportNode &node, fbx::FbxNode *fbx_node, fbx::FbxLight *fbx_light);
	void process_camera(const Unigine::ImportScene &import_scene, const Unigine::ImportNode &node, fbx::FbxNode *fbx_node, fbx::FbxCamera *fbx_camera);

/*...*/

};

```


## Importer Class

### Enums

## Axis

Axis.
| Name | Description |
|---|---|
| **None** = -1 | Axis none. |
| **X** = None + 1 | X axis. |
| **NX** = X + 1 | Negative X axis. |
| **Y** = NX + 1 | Y axis. |
| **NY** = Y + 1 | Negative Y axis. |
| **Z** = NY + 1 | Z axis. |
| **NZ** = Z + 1 | Negative Z axis. |

### Properties

## string AnimationsProcessor

The import [processor](../../../../api/library/common/import/class.importprocessor_cs.md) to be used for importing animations.
## string SkeletonsProcessor

The import [processor](../../../../api/library/common/import/class.importprocessor_cs.md) to be used for importing skeletons.
## string LightsProcessor

The import [processor](../../../../api/library/common/import/class.importprocessor_cs.md) to be used for importing light sources.
## string MeshesProcessor

The import [processor](../../../../api/library/common/import/class.importprocessor_cs.md) to be used for importing meshes.
## string MeshSkinnedsProcessor

The import [processor](../../../../api/library/common/import/class.importprocessor_cs.md) to be used for importing skinned meshes.
## string NodesProcessor

The import [processor](../../../../api/library/common/import/class.importprocessor_cs.md) to be used for importing nodes.
## string CamerasProcessor

The import [processor](../../../../api/library/common/import/class.importprocessor_cs.md) to be used for importing cameras.
## string MaterialsProcessor

The import [processor](../../../../api/library/common/import/class.importprocessor_cs.md) to be used for importing materials.
## string OutputFilepath

The resulting output file path for imported scene component(s). In case a set of files is generated, the path to resulting `*.node` file will be returned.
## string TexturesProcessor

The import [processor](../../../../api/library/common/import/class.importprocessor_cs.md) to be used for importing textures.
### Members

---

## Importer ( )

Constructor. Creates an empty importer.
## Importer GetImporter ( )

Returns the [importer](../../../../api/library/common/import/class.importer_cs.md) itself.
### Return value

Importer itself.
## bool ContainsParameter ( string name )

Returns a value indicating whether the list of import parameters includes a parameter with a given name.
### Arguments

- *string* **name** - Parameter name.

### Return value

true if the list of import parameters includes a parameter with a given name; otherwise, false.
## void SetParameterInt ( string name , int v )

Sets a new value for the specified *integer* parameter. There are [built-in parameters](../../../../principles/import_system/index_cs.md#param_int) that can also be used in custom importers.
### Arguments

- *string* **name** - Name of the *integer* parameter.
- *int* **v** - New value to be set.

## int GetParameterInt ( string name )

Returns the current value of the specified *integer* parameter. There are [built-in parameters](../../../../principles/import_system/index_cs.md#param_int) that can also be used in custom importers.
### Arguments

- *string* **name** - Name of the *integer* parameter.

### Return value

Value of the *integer* parameter.
## void SetParameterFloat ( string name , float v )

Sets a new value for the specified *float* parameter. There are [built-in parameters](../../../../principles/import_system/index_cs.md#param_int) that can also be used in custom importers.
### Arguments

- *string* **name** - Name of the *float* parameter.
- *float* **v** - New value to be set.

## float GetParameterFloat ( string name )

Returns the current value of the specified *float* parameter. There are [built-in parameters](../../../../principles/import_system/index_cs.md#param_int) that can also be used in custom importers.
### Arguments

- *string* **name** - Name of the *float* parameter.

### Return value

Value of the *float* parameter.
## void SetParameterDouble ( string name , double v )

Sets a new value for the specified *double* parameter. There are [built-in parameters](../../../../principles/import_system/index_cs.md#param_int) that can also be used in custom importers.
### Arguments

- *string* **name** - Name of the *double* parameter.
- *double* **v** - New value to be set.

## double GetParameterDouble ( string name )

Returns the current value of the specified *double* parameter. There are [built-in parameters](../../../../principles/import_system/index_cs.md#param_int) that can also be used in custom importers.
### Arguments

- *string* **name** - Name of the *double* parameter.

### Return value

Value of the *double* parameter.
## void SetParameterString ( string name , string v )

Sets a new value for the specified string parameter. There are [built-in parameters](../../../../principles/import_system/index_cs.md#param_int) that can also be used in custom importers.
### Arguments

- *string* **name** - Name of the string parameter.
- *string* **v** - New value to be set.

## string GetParameterString ( string name )

Returns the current value of the specified string parameter. There are [built-in parameters](../../../../principles/import_system/index_cs.md#param_int) that can also be used in custom importers.
### Arguments

- *string* **name** - Name of the string parameter.

### Return value

Value of the string parameter.
## bool AddPreProcessor ( string type_name )

Adds an import [pre-processor](../../../../api/library/common/import/class.importprocessor_cs.md) with a given type name. There are [built-in pre-processors](../../../../principles/import_system/index_cs.md#preprocessors) that can also be added to custom importers.
### Arguments

- *string* **type_name** - Pre-processor type name.

### Return value

true if the specified import pre-processor is successfully added; otherwise, false.
## void RemovePreProcessor ( string type_name )

Removes an import [pre-processor](../../../../api/library/common/import/class.importprocessor_cs.md) with a given type name. There are [built-in pre-processors](../../../../principles/import_system/index_cs.md#preprocessors) that can also be added to custom importers.
### Arguments

- *string* **type_name** - Pre-processor type name.

## bool HasPreProcessor ( string type_name )

Returns a value indicating if an import [pre-processor](../../../../api/library/common/import/class.importprocessor_cs.md) with a given type name is used by the importer. There are [built-in pre-processors](../../../../principles/import_system/index_cs.md#preprocessors) that can also be added to custom importers.
### Arguments

- *string* **type_name** - Pre-processor type name.

### Return value

true if an import pre-processor with a given type name is used by the importer; otherwise, false.
## bool AddPostProcessor ( string type_name )

Adds an import [post-processor](../../../../api/library/common/import/class.importprocessor_cs.md) with a given type name. There are [built-in post-processors](../../../../principles/import_system/index_cs.md#postprocessors) that can also be added to custom importers.
### Arguments

- *string* **type_name** - Post-processor type name to check.

## void RemovePostProcessor ( string type_name )

Removes an import [post-processor](../../../../api/library/common/import/class.importprocessor_cs.md) with a given type name. There are [built-in post-processors](../../../../principles/import_system/index_cs.md#postprocessors) that can also be added to custom importers.
### Arguments

- *string* **type_name** - Post-processor type name.

## bool HasPostProcessor ( string type_name )

Returns a value indicating if an import [post-processor](../../../../api/library/common/import/class.importprocessor_cs.md) with a given type name is used by the importer. There are [built-in post-processors](../../../../principles/import_system/index_cs.md#postprocessors) that can also be added to custom importers.
### Arguments

- *string* **type_name** - Post-processor type name to check.

### Return value

true if an import post-processor with a given type name is used by the importer; otherwise, false.
## ImportScene GetScene ( )

Returns the imported scene.
### Return value

Instance of the *[ImportScene](../../../../api/library/common/import/class.importscene_cs.md)* class.
## bool Init ( string filepath , int flags = ~0 )

Initializes the importer for the specified file using the given flags. Import flags specify which scene components are to be imported.
### Arguments

- *string* **filepath** - Path to a file to be imported.
- *int* **flags** - Set of import flags. Any combination of [IMPORT_*](#IMPORT_LIGHTS) flags, or ~0 to set all of them.

### Return value

true if the importer was initialized successfully; otherwise, 0.
## bool Import ( string output_path )

Imports the contents of the input file to the specified output path.
### Arguments

- *string* **output_path** - Output path.

### Return value

true if the contents of the input file are successfully imported to the specified output path; otherwise, false.
## string GetSourceFilepath ( )

Returns the path to the source file.
### Return value

Source file path.
## int GetFlags ( )

Returns the current set of import flags (*[IMPORT_*](#IMPORT_LIGHTS)*) that were set at initialization.
## bool ComputeBoundBox ( ImportMesh import_mesh )

Computes a bound box for the specified mesh.
### Arguments

- *[ImportMesh](../../../../api/library/common/import/class.importmesh_cs.md)* **import_mesh** - Imported mesh for which a bound box is to be calculated.

### Return value

true if a bound box for the specified mesh is successfully calculated; otherwise, false.
## bool Preprocess ( )

Starts execution of all [added](#addPreProcessor_cstr_bool) pre-processors.
### Return value

true if the pre-processing is completed successfully.
## Node ConvertNode ( ImportProcessor processor , ImportNode root_node )

Converts metadata stored in an instance of the *[ImportNode](../../../../api/library/common/import/class.importnode_cs.md)* class to UNIGINE's node (node hierarchy).
### Arguments

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_cs.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_cs.md) to be used for this import operation.
- *[ImportNode](../../../../api/library/common/import/class.importnode_cs.md)* **root_node** - Instance of the *[ImportNode](../../../../api/library/common/import/class.importnode_cs.md)* class representing the root node of the imported hierarchy.

### Return value

Resulting [UNIGINE's node instance](../../../../api/library/nodes/class.node_cs.md) that stores the specified imported node (node hierarchy).
## bool ImportTexture ( ImportProcessor processor , ImportTexture import_texture )


Imports the specified texture and uses the specified [processor](../../../../api/library/common/import/class.importprocessor_cs.md) to process and save the generated texture to a corresponding file in the output directory specified in the **[Import()](../../../...md#import_cstr_bool)** method.


> **Notice:** To customize actions to be performed on importing textures, when implementing a custom importer, you can override the **[OnImportTexture()](../../../...md#onImportTexture_ImportProcessor_ImportTexture_bool)** method.

### Arguments

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_cs.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_cs.md) to be used for this import operation.
- *[ImportTexture](../../../../api/library/common/import/class.importtexture_cs.md)* **import_texture** - Instance of the *[ImportTexture](../../../../api/library/common/import/class.importtexture_cs.md)* class.

### Return value

true if the specified texture was successfully imported; otherwise, false.
## bool ImportMaterial ( ImportProcessor processor , Material material , ImportMaterial import_material )


Imports the specified material and uses the specified [processor](../../../../api/library/common/import/class.importprocessor_cs.md) to process and save the generated material to a corresponding file in the output directory specified in the **[Import()](../../../...md#import_cstr_bool)** method.


> **Notice:** To customize actions to be performed on importing materials, when implementing a custom importer, you can override the **[OnImportMaterial()](../../../...md#onImportMaterial_ImportProcessor_Material_ImportMaterial_bool)** method.


### Arguments

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_cs.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_cs.md) to be used for this import operation.
- *[Material](../../../../api/library/rendering/class.material_cs.md)* **material** - Target [UNIGINE's material instance](../../../../api/library/rendering/class.material_cs.md) to store the specified imported material.
- *[ImportMaterial](../../../../api/library/common/import/class.importmaterial_cs.md)* **import_material** - Instance of the *[ImportMaterial](../../../../api/library/common/import/class.importmaterial_cs.md)* class.

### Return value

true if the specified material was successfully imported; otherwise, false.
## bool ImportMesh ( ImportProcessor processor , Mesh mesh , ImportMesh import_mesh )


Imports the specified mesh and uses the specified [processor](../../../../api/library/common/import/class.importprocessor_cs.md) to process and save the generated mesh to a corresponding file in the output directory specified in the **[Import()](../../../...md#import_cstr_bool)** method.


> **Notice:** To customize actions to be performed on importing meshes, when implementing a custom importer, you can override the **[OnImportMesh()](../../../...md#onImportMesh_ImportProcessor_Mesh_ImportMesh_bool)** method.


### Arguments

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_cs.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_cs.md) to be used for this import operation.
- *[Mesh](../../../../api/library/rendering/class.mesh_cs.md)* **mesh** - Target [UNIGINE's mesh instance](../../../../api/library/rendering/class.mesh_cs.md) to store the specified imported mesh.
- *[ImportMesh](../../../../api/library/common/import/class.importmesh_cs.md)* **import_mesh** - Instance of the *[ImportMesh](../../../../api/library/common/import/class.importmesh_cs.md)* class.

### Return value

true if the specified mesh was successfully imported; otherwise, false.
## bool ImportMeshSkinned ( ImportProcessor processor , MeshSkinned mesh_skinned , ImportMeshSkinned import_mesh_skinned )


Imports the specified skinned mesh and uses the specified [processor](../../../../api/library/common/import/class.importprocessor_cs.md) to process and save the generated skinned mesh to a corresponding file in the output directory specified in the **[Import()](../../../...md#import_cstr_bool)** method.


> **Notice:** To customize actions to be performed on importing skinned meshes, when implementing a custom importer, you can override the **[OnImportMeshSkinned()](../../../...md#onImportMeshSkinned_ImportProcessor_MeshSkinned_ImportMeshSkinned_bool)** method.


### Arguments

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_cs.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_cs.md) to be used for this import operation.
- *[MeshSkinned](../../../../api/library/rendering/class.meshskinned_cs.md)* **mesh_skinned** - Target [UNIGINE's skinned mesh instance](../../../../api/library/rendering/class.meshskinned_cs.md) to store the specified imported skinned mesh.
- *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cs.md)* **import_mesh_skinned** - Instance of the *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cs.md)* class.

### Return value

true if the specified skinned mesh was successfully imported; otherwise, false.
## Light ImportLight ( ImportProcessor processor , ImportLight import_light )

 Imports the specified light and uses the specified [processor](../../../../api/library/common/import/class.importprocessor_cs.md) to process and save the generated light to a corresponding `*.node` file in the output directory specified in the **[Import()](../../../...md#import_cstr_bool)** method.
> **Notice:** To customize actions to be performed on importing lights, when implementing a custom importer, you can override the **[OnImportLight()](../../../...md#onImportLight_ImportProcessor_ImportLight_Light)** method.


### Arguments

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_cs.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_cs.md) to be used for this import operation.
- *[ImportLight](../../../../api/library/common/import/class.importlight_cs.md)* **import_light** - Instance of the *[ImportLight](../../../../api/library/common/import/class.importlight_cs.md)* class.

### Return value

[UNIGINE's light instance](../../../../api/library/lights/class.light_cs.md) that stores the specified imported light source.
## Player ImportCamera ( ImportProcessor processor , ImportCamera import_camera )

 Imports the specified camera and uses the specified [processor](../../../../api/library/common/import/class.importprocessor_cs.md) to process and save the generated player to a corresponding `*.node` file in the output directory specified in the **[Import()](../../../...md#import_cstr_bool)** method.
> **Notice:** To customize actions to be performed on importing cameras, when implementing a custom importer, you can override the **[OnImportCamera()](../../../...md#onImportCamera_ImportProcessor_ImportCamera_Player)** method.


### Arguments

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_cs.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_cs.md) to be used for this import operation.
- *[ImportCamera](../../../../api/library/common/import/class.importcamera_cs.md)* **import_camera** - Instance of the *[ImportCamera](../../../../api/library/common/import/class.importcamera_cs.md)* class.

### Return value

[UNIGINE's player instance](../../../../api/library/players/class.player_cs.md) that stores the specified imported camera.
## bool ImportAnimation ( ImportProcessor processor , MeshSkinnedAnimation animation , ImportAnimation import_animation )


Imports the specified mesh animation and uses the specified [processor](../../../../api/library/common/import/class.importprocessor_cs.md) to process and save the generated mesh animation to a corresponding file in the output directory specified in the **[Import()](../../../...md#import_cstr_bool)** method.


> **Notice:** To customize actions to be performed on importing mesh animations, when implementing a custom importer, you can override the **[OnImportAnimation()](../../../...md#onImportAnimation_ImportProcessor_MeshSkinnedAnimation_ImportAnimation_bool)** method.

### Arguments

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_cs.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_cs.md) to be used for this import operation.
- *[MeshSkinnedAnimation](../../../../api/library/rendering/class.meshskinnedanimation_cs.md)* **animation** - Target [UNIGINE's mesh animation instance](../../../../api/library/rendering/class.meshskinnedanimation_cs.md) to store the specified imported mesh animation.
- *[ImportAnimation](../../../../api/library/common/import/class.importanimation_cs.md)* **import_animation** - Instance of the *[ImportAnimation](../../../../api/library/common/import/class.importanimation_cs.md)* class.

### Return value

true if the specified animation was successfully imported; otherwise, false.
## bool ImportAnimation ( ImportProcessor processor , MeshSkinnedAnimation animation , ImportMeshSkinned import_mesh_skinned , ImportAnimation import_animation )


Imports the specified mesh animation and uses the specified [processor](../../../../api/library/common/import/class.importprocessor_cs.md) to process and save the generated mesh animation to a corresponding file in the output directory specified in the **[Import()](../../../...md#import_cstr_bool)** method.


> **Notice:** To customize actions to be performed on importing mesh animations, when implementing a custom importer, you can override the **[OnImportAnimation()](../../../...md#onImportAnimation_ImportProcessor_MeshSkinnedAnimation_ImportMeshSkinned_ImportAnimation_bool)** method.

### Arguments

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_cs.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_cs.md) to be used for this import operation.
- *[MeshSkinnedAnimation](../../../../api/library/rendering/class.meshskinnedanimation_cs.md)* **animation** - Target [UNIGINE's mesh animation instance](../../../../api/library/rendering/class.meshskinnedanimation_cs.md) to store the specified imported mesh animation.
- *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cs.md)* **import_mesh_skinned** - Instance of the *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cs.md)* class.
- *[ImportAnimation](../../../../api/library/common/import/class.importanimation_cs.md)* **import_animation** - Instance of the *[ImportAnimation](../../../../api/library/common/import/class.importanimation_cs.md)* class.

### Return value

true if the specified animation was successfully imported; otherwise, false.
## bool ImportSkeleton ( ImportProcessor processor , Skeleton skeleton , ImportSkeleton import_skeleton )


Imports the specified skeleton and uses the specified [processor](../../../../api/library/common/import/class.importprocessor_cs.md) to process and save the generated skeleton to a corresponding file in the output directory specified in the **[Import()](../../../...md#import_cstr_bool)** method.


> **Notice:** To customize actions to be performed on importing skeletons, when implementing a custom importer, you can override the **[OnImportSkeleton()](../../../...md#onImportSkeleton_ImportProcessor_Skeleton_ImportSkeleton_bool)** method.

### Arguments

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_cs.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_cs.md) to be used for this import operation.
- *[Skeleton](../../../../api/library/animations/skeletal/class.skeleton_cs.md)* **skeleton** - Target [UNIGINE's skeleton instance](../../../../api/library/animations/skeletal/class.skeleton_cs.md) to store the specified imported skeleton.
- *[ImportSkeleton](../../../../api/library/common/import/class.importskeleton_cs.md)* **import_skeleton** - Instance of the *[ImportSkeleton](../../../../api/library/common/import/class.importskeleton_cs.md)* class.

### Return value

true if the specified skeleton was successfully imported; otherwise, false.
## bool CheckSupportedAnimation ( ImportMeshSkinned import_mesh_skinned , ImportAnimation import_animation )

Returns a value indicating if importing of the specified animation of the specified imported mesh is supported.
### Arguments

- *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cs.md)* **import_mesh_skinned** - Instance of the *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cs.md)* class.
- *[ImportAnimation](../../../../api/library/common/import/class.importanimation_cs.md)* **import_animation** - Instance of the *[ImportAnimation](../../../../api/library/common/import/class.importanimation_cs.md)* class.

### Return value

true if importing of the specified animation of the specified imported mesh is supported; otherwise, false.
## bool CheckDefaultAnimation ( ImportMeshSkinned import_mesh_skinned , ImportAnimation import_animation )

Returns a value indicating if the specified animation is the default one for the specified imported mesh.
### Arguments

- *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cs.md)* **import_mesh_skinned** - Instance of the *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cs.md)* class.
- *[ImportAnimation](../../../../api/library/common/import/class.importanimation_cs.md)* **import_animation** - Instance of the *[ImportAnimation](../../../../api/library/common/import/class.importanimation_cs.md)* class.

### Return value

true if the specified animation is the default one for the specified imported mesh; otherwise, false.
## Node ImportNode ( ImportProcessor processor , ImportNode import_node )


Imports the specified node and uses the specified [processor](../../../../api/library/common/import/class.importprocessor_cs.md) to process and save the generated node to a corresponding file in the output directory specified in the **[Import()](../../../...md#import_cstr_bool)** method.


> **Notice:** To customize actions to be performed on importing nodes, when implementing a custom importer, you can override the **[OnImportNode()](../../../...md#onImportNode_ImportProcessor_ImportNode_Node)** method.


### Arguments

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_cs.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_cs.md) to be used for this import operation.
- *[ImportNode](../../../../api/library/common/import/class.importnode_cs.md)* **import_node** - Instance of the *[ImportNode](../../../../api/library/common/import/class.importnode_cs.md)* class.

### Return value

Target [UNIGINE's node instance](../../../../api/library/nodes/class.node_cs.md) to store the specified imported node.
## bool ImportNodeChild ( ImportProcessor processor , Node node_parent , ImportNode import_node_parent , Node node_child , ImportNode import_node_child )


Imports the specified parent node with the specified child node and uses the specified [processor](../../../../api/library/common/import/class.importprocessor_cs.md) to process and save generated nodes to a corresponding file in the output directory specified in the **[Import()](../../../...md#import_cstr_bool)** method.


> **Notice:** To customize actions to be performed on importing nodes, when implementing a custom importer, you can override the **[OnImportNodeChild()](../../../...md#onImportNodeChild_ImportProcessor_Node_ImportNode_Node_ImportNode_bool)** method.


### Arguments

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_cs.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_cs.md) to be used for this import operation.
- *[Node](../../../../api/library/nodes/class.node_cs.md)* **node_parent** - Target [UNIGINE's node instance](../../../../api/library/nodes/class.node_cs.md) to store the specified imported parent node.
- *[ImportNode](../../../../api/library/common/import/class.importnode_cs.md)* **import_node_parent** - Instance of the [ImportNode](../../../../api/library/common/import/class.importnode_cs.md) class for the parent node.
- *[Node](../../../../api/library/nodes/class.node_cs.md)* **node_child** - Target [UNIGINE's node instance](../../../../api/library/nodes/class.node_cs.md) to store the specified imported child node.
- *[ImportNode](../../../../api/library/common/import/class.importnode_cs.md)* **import_node_child** - Instance of the [ImportNode](../../../../api/library/common/import/class.importnode_cs.md) class for the child node.

### Return value

true if the specified parent node along with the specified child node were successfully imported; otherwise, false.
## bool Postprocess ( )

Starts execution of all [added](#addPostProcessor_cstr_bool) post-processors. Post-processors can be used to manage files generated in the process of import.
### Return value

true if the post-processing is completed successfully.
## bool GetBasis ( Importer.Axis up_axis , Importer.Axis front_axis , out dmat4 ret )

Returns the transformation matrix for the basis specified by axes.
### Arguments

- *[Importer.Axis](../../../../api/library/common/import/class.importer_cs.md#Axis)* **up_axis** - Up axis of the basis.
- *[Importer.Axis](../../../../api/library/common/import/class.importer_cs.md#Axis)* **front_axis** - Front axis of the basis.
- *out dmat4* **ret** - Transformation matrix for the basis specified by axes.

### Return value

true the transformation matrix for the basis was successfully calculated; otherwise, false.
## bool OnComputeBoundBox ( ImportMesh import_mesh )

Extendable method for custom bound box computation.
### Arguments

- *[ImportMesh](../../../../api/library/common/import/class.importmesh_cs.md)* **import_mesh** - Imported mesh for which a bound box is to be calculated.

### Return value

true if a bound box for the specified mesh was successfully calculated; otherwise, false.
## bool OnInit ( ImportScene import_scene , string filepath )

Builds and initializes the imported [scene](../../../../api/library/common/import/class.importscene_cs.md) based on the data contained in the specified input file.
### Arguments

- *[ImportScene](../../../../api/library/common/import/class.importscene_cs.md)* **import_scene** - Imported scene (built from the data contained in the specified input file).
- *string* **filepath** - Path to an input file to be imported.

### Return value

true if the scene is successfully initialized using the data from the specified input file; otherwise, false.
## bool OnImport ( string output_path )


Import event handler function. This function is called each time when the *[Import()](../../../...md#import_cstr_bool)* function is called. You can specify your custom actions to be performed on scene import.


```cpp
class MyCustomImporter : public Unigine::Importer
{
public:
	MyCustomImporter();
	virtual ~MyCustomImporter();

/*...*/

// overrides of event functions
protected:
	bool onImport(const char *output_path) override;

/*...*/

};

/*...*/

bool MyCustomImporter::onImport(const char *output_path)
{
	bool result = false;

	// your custom actions

	return result;
}

```


### Arguments

- *string* **output_path** - Output path to be used to store generated file(s) with imported data.

### Return value

true if import operation for the specified output path was successful; otherwise, false.
## bool OnImportTexture ( ImportProcessor processor , ImportTexture import_texture )


Texture import event handler function. This function is called each time when the *[ImportTexture()](../../../...md#importTexture_ImportProcessor_ImportTexture_bool)* function is called. You can specify your custom actions to be performed on texture import.


```cpp
class MyCustomImporter : public Unigine::Importer
{
public:
	MyCustomImporter();
	virtual ~MyCustomImporter();

/*...*/

// overrides of event functions
protected:
	bool onImportTexture(const ImportProcessorPtr &processor, const ImportTexturePtr &import_texture) override;

/*...*/

};

/*...*/

bool MyCustomImporter::onImportTexture(const ImportProcessorPtr &processor, const ImportTexturePtr &import_texture)
{
	bool result = false;

	// your custom actions

	return result;
}

```


### Arguments

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_cs.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_cs.md) used for this import operation.
- *[ImportTexture](../../../../api/library/common/import/class.importtexture_cs.md)* **import_texture** - Instance of the *[ImportTexture](../../../../api/library/common/import/class.importtexture_cs.md)* class.

### Return value

true if the specified texture was successfully imported; otherwise, false.
## bool OnImportMaterial ( ImportProcessor processor , Material material , ImportMaterial import_material )


Material import event handler function. This function is called each time when the **[ImportMaterial()](../../../...md#importMaterial_ImportProcessor_Material_ImportMaterial_bool)** function is called. You can specify your custom actions to be performed on material import.


```cpp
class MyCustomImporter : public Unigine::Importer
{
public:
	MyCustomImporter();
	virtual ~MyCustomImporter();

/*...*/

// overrides of event functions
protected:
	bool onImportMaterial(const ImportProcessorPtr &processor, const Unigine::MaterialPtr &material, const ImportMaterialPtr &import_material) override;

/*...*/

};

/*...*/

bool MyCustomImporter::onImportMaterial(const ImportProcessorPtr &processor, const Unigine::MaterialPtr &material, const ImportMaterialPtr &import_material)
{
	bool result = false;

	// your custom actions

	return result;
}

```


### Arguments

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_cs.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_cs.md) used for this import operation.
- *[Material](../../../../api/library/rendering/class.material_cs.md)* **material** - Target [UNIGINE's material instance](../../../../api/library/rendering/class.material_cs.md) to store the specified imported material.
- *[ImportMaterial](../../../../api/library/common/import/class.importmaterial_cs.md)* **import_material** - Instance of the [ImportMaterial](../../../../api/library/common/import/class.importmaterial_cs.md) class.

### Return value

true if the specified material was successfully imported; otherwise, false.
## Light OnImportLight ( ImportProcessor processor , ImportLight import_light )


Light import event handler function. This function is called each time when the **[ImportLight()](../../../...md#importLight_ImportProcessor_ImportLight_Light)** function is called. You can specify your custom actions to be performed on light import.


```cpp
class MyCustomImporter : public Unigine::Importer
{
public:
	MyCustomImporter();
	virtual ~MyCustomImporter();

/*...*/

// overrides of event functions
protected:
	Unigine::LightPtr onImportLight(const ImportProcessorPtr &processor, const ImportLightPtr &import_light) override;

/*...*/

};

/*...*/

Unigine::LightPtr MyCustomImporter::onImportLight(const ImportProcessorPtr &processor, const ImportLightPtr &import_light)
{
	bool result = false;

	// your custom actions

	return result;
}

```


### Arguments

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_cs.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_cs.md) used for this import operation.
- *[ImportLight](../../../../api/library/common/import/class.importlight_cs.md)* **import_light** - Instance of the [ImportLight](../../../../api/library/common/import/class.importlight_cs.md) class.

### Return value

[UNIGINE's light instance](../../../../api/library/lights/class.light_cs.md) that stores the specified imported light.
## Player OnImportCamera ( ImportProcessor processor , ImportCamera import_camera )


Camera import event handler function. This function is called each time when the **[ImportCamera()](../../../...md#importCamera_ImportProcessor_ImportCamera_Player)** function is called. You can specify your custom actions to be performed on camera import.


```cpp
class MyCustomImporter : public Unigine::Importer
{
public:
	MyCustomImporter();
	virtual ~MyCustomImporter();

/*...*/

// overrides of event functions
protected:
	Unigine::PlayerPtr onImportCamera(const ImportProcessorPtr &processor, const ImportCameraPtr &import_camera) override;

/*...*/

};

/*...*/

Unigine::PlayerPtr MyCustomImporter::onImportCamera(const ImportProcessorPtr &processor, const ImportCameraPtr &import_camera)
{
	bool result = false;

	// your custom actions

	return result;
}

```


### Arguments

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_cs.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_cs.md) used for this import operation.
- *[ImportCamera](../../../../api/library/common/import/class.importcamera_cs.md)* **import_camera** - Instance of the [ImportCamera](../../../../api/library/common/import/class.importcamera_cs.md) class.

### Return value

[UNIGINE's player instance](../../../../api/library/players/class.player_cs.md) that stores the specified imported camera.
## bool OnImportMesh ( ImportProcessor processor , Mesh mesh , ImportMesh import_mesh )


Mesh import event handler function. This function is called each time when the **[ImportMesh()](../../../...md#importMesh_ImportProcessor_Mesh_ImportMesh_bool)** function is called. You can specify your custom actions to be performed on mesh import.


```cpp
class MyCustomImporter : public Unigine::Importer
{
public:
	MyCustomImporter();
	virtual ~MyCustomImporter();

/*...*/

// overrides of event functions
protected:
	bool onImportMesh(const ImportProcessorPtr &processor, const Unigine::MeshPtr &mesh, const ImportMeshPtr &import_mesh) override;

/*...*/

};

/*...*/

bool MyCustomImporter::onImportMesh(const ImportProcessorPtr &, const Unigine::MeshPtr &mesh, const ImportMeshPtr &import_mesh)
{
	bool result = false;

	// your custom actions

	return result;
}

```


### Arguments

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_cs.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_cs.md) used for this import operation.
- *[Mesh](../../../../api/library/rendering/class.mesh_cs.md)* **mesh** - Target [UNIGINE's mesh instance](../../../../api/library/rendering/class.mesh_cs.md) to store the specified imported mesh.
- *[ImportMesh](../../../../api/library/common/import/class.importmesh_cs.md)* **import_mesh** - Instance of the [ImportMesh](../../../../api/library/common/import/class.importmesh_cs.md) class.

### Return value

true if the specified mesh was successfully imported; otherwise, false.
## bool OnImportMeshSkinned ( ImportProcessor processor , MeshSkinned mesh_skinned , ImportMeshSkinned import_mesh_skinned )


Skinned mesh import event handler function. This function is called each time when the **[ImportMeshSkinned()](../../../...md#importMeshSkinned_ImportProcessor_MeshSkinned_ImportMeshSkinned_bool)** function is called. You can specify your custom actions to be performed on skinned mesh import.


```cpp
class MyCustomImporter : public Unigine::Importer
{
public:
	MyCustomImporter();
	virtual ~MyCustomImporter();

/*...*/

// overrides of event functions
protected:
	bool onImportMeshSkinned(const ImportProcessorPtr &processor, const Unigine::MeshSkinnedPtr &mesh_skinned, const ImportMeshSkinnedPtr &import_mesh_skinned) override;

/*...*/

};

/*...*/

bool MyCustomImporter::onImportMeshSkinned(const ImportProcessorPtr &processor, const Unigine::MeshSkinnedPtr &mesh_skinned, const ImportMeshSkinnedPtr &import_mesh_skinned)
{
	bool result = false;

	// your custom actions

	return result;
}

```


### Arguments

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_cs.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_cs.md) used for this import operation.
- *[MeshSkinned](../../../../api/library/rendering/class.meshskinned_cs.md)* **mesh_skinned** - Target [UNIGINE's skinned mesh instance](../../../../api/library/rendering/class.meshskinned_cs.md) to store the specified imported skinned mesh.
- *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cs.md)* **import_mesh_skinned** - Instance of the [ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cs.md) class.

### Return value

true if the specified skinned mesh was successfully imported; otherwise, false.
## Node OnImportNode ( ImportProcessor processor , ImportNode import_node )


Node import event handler function. This function is called each time when the **[ImportNode()](../../../...md#importNode_ImportProcessor_ImportNode_Node)** function is called. You can specify your custom actions to be performed on node import.


```cpp
class MyCustomImporter : public Unigine::Importer
{
public:
	MyCustomImporter();
	virtual ~MyCustomImporter();

/*...*/

// overrides of event functions
protected:
	Unigine::NodePtr onImportNode(const ImportProcessorPtr &processor, const ImportNodePtr &import_node) override;

/*...*/

};

/*...*/

Unigine::NodePtr MyCustomImporter::onImportNode(const ImportProcessorPtr &processor, const ImportNodePtr &import_node)
{
	bool result = false;

	// your custom actions

	return result;
}

```


### Arguments

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_cs.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_cs.md) used for this import operation.
- *[ImportNode](../../../../api/library/common/import/class.importnode_cs.md)* **import_node** - Instance of the [ImportNode](../../../../api/library/common/import/class.importnode_cs.md) class.

### Return value

[UNIGINE's node instance](../../../../api/library/nodes/class.node_cs.md) that stores the specified imported node.
## bool OnImportNodeChild ( ImportProcessor processor , Node node_parent , ImportNode import_node_parent , Node node_child , ImportNode import_node_child )


Node import event handler function. This function is called each time when the **[ImportNodeChild()](../../../...md#importNodeChild_ImportProcessor_Node_ImportNode_Node_ImportNode_bool)** function is called. You can specify your custom actions to be performed on importing and processing node hierarchies (e.g. assigning properties to node children).


```cpp
class MyCustomImporter : public Unigine::Importer
{
public:
	MyCustomImporter();
	virtual ~MyCustomImporter();

/*...*/

// overrides of event functions
protected:
	bool onImportNodeChild(const ImportProcessorPtr &processor, const Unigine::NodePtr &node_parent, const ImportNodePtr &import_node_parent, const Unigine::NodePtr &node_child, const ImportNodePtr &import_node_child) override;

/*...*/

};

/*...*/

bool MyCustomImporter::onImportNodeChild(const ImportProcessorPtr &processor, const Unigine::NodePtr &node_parent, const ImportNodePtr &import_node_parent, const Unigine::NodePtr &node_child, const ImportNodePtr &import_node_child)
{
	bool result = false;

	// your custom actions

	return result;
}

```


### Arguments

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_cs.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_cs.md) used for this import operation.
- *[Node](../../../../api/library/nodes/class.node_cs.md)* **node_parent** - Target [UNIGINE's node instance](../../../../api/library/nodes/class.node_cs.md) to store the specified imported parent node.
- *[ImportNode](../../../../api/library/common/import/class.importnode_cs.md)* **import_node_parent** - Instance of the [ImportNode](../../../../api/library/common/import/class.importnode_cs.md) class for the parent node.
- *[Node](../../../../api/library/nodes/class.node_cs.md)* **node_child** - Target [UNIGINE's node instance](../../../../api/library/nodes/class.node_cs.md) to store the specified imported child node.
- *[ImportNode](../../../../api/library/common/import/class.importnode_cs.md)* **import_node_child** - Instance of the [ImportNode](../../../../api/library/common/import/class.importnode_cs.md) class for the child node.

### Return value

true if the specified parent node and its child node animation were successfully imported; otherwise, false.
## bool OnImportAnimation ( ImportProcessor processor , MeshSkinnedAnimation animation , ImportAnimation import_animation )

Animation import event handler function. This function is called each time when the *[ImportAnimation()](../../../...md#importAnimation_ImportProcessor_MeshSkinnedAnimation_ImportAnimation_bool)* function is called. You can specify your custom actions to be performed on animation import.
### Arguments

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_cs.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_cs.md) used for this import operation.
- *[MeshSkinnedAnimation](../../../../api/library/rendering/class.meshskinnedanimation_cs.md)* **animation** - Target [UNIGINE's mesh animation instance](../../../../api/library/rendering/class.meshskinnedanimation_cs.md) to store the specified imported mesh animation.
- *[ImportAnimation](../../../../api/library/common/import/class.importanimation_cs.md)* **import_animation** - [ImportAnimation structure](../../../../api/library/common/import/class.importanimation_cs.md) pointer. The metadata for the animation that needs to be imported.

### Return value

true if the specified mesh animation was successfully imported; otherwise, false.
## bool OnImportAnimation ( ImportProcessor processor , MeshSkinnedAnimation animation , ImportMeshSkinned import_mesh_skinned , ImportAnimation import_animation )

Animation import event handler function. This function is called each time when the *[ImportAnimation()](../../../...md#importAnimation_ImportProcessor_MeshSkinnedAnimation_ImportMeshSkinned_ImportAnimation_bool)* function is called. You can specify your custom actions to be performed on animation import.
### Arguments

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_cs.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_cs.md) used for this import operation.
- *[MeshSkinnedAnimation](../../../../api/library/rendering/class.meshskinnedanimation_cs.md)* **animation** - Target [UNIGINE's mesh animation instance](../../../../api/library/rendering/class.meshskinnedanimation_cs.md) to store the specified imported mesh animation.
- *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cs.md)* **import_mesh_skinned** - [ImportMeshSkinned structure](../../../../api/library/common/import/class.importmeshskinned_cs.md) pointer. The metadata for the skinned mesh that needs to be imported.
- *[ImportAnimation](../../../../api/library/common/import/class.importanimation_cs.md)* **import_animation** - [ImportAnimation structure](../../../../api/library/common/import/class.importanimation_cs.md) pointer. The metadata for the animation that needs to be imported.

### Return value

true if the specified mesh animation was successfully imported; otherwise, false.
## bool OnImportSkeleton ( ImportProcessor processor , Skeleton skeleton , ImportSkeleton import_skeleton )


Skeleton import event handler function. This function is called each time when the **[ImportSkeleton()](../../../...md#importSkeleton_ImportProcessor_Skeleton_ImportSkeleton_bool)** function is called. You can specify your custom actions to be performed on skeleton import.


```cpp
class MyCustomImporter : public Unigine::Importer
{
public:
	MyCustomImporter();
	virtual ~MyCustomImporter();

/*...*/

// overrides of event functions
protected:
	bool onImportSkeleton(const ImportProcessorPtr &processor, const Unigine::SkeletonPtr &skeleton, const ImportSkeletonPtr &import_skeleton) override;

/*...*/

};

/*...*/

bool MyCustomImporter::onImportSkeleton(const ImportProcessorPtr &processor, const Unigine::SkeletonPtr &skeleton, const ImportSkeletonPtr &import_skeleton)
{
	bool result = false;

	// your custom actions

	return result;
}

```


### Arguments

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_cs.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_cs.md) used for this import operation.
- *[Skeleton](../../../../api/library/animations/skeletal/class.skeleton_cs.md)* **skeleton** - Target [UNIGINE's skeleton instance](../../../../api/library/animations/skeletal/class.skeleton_cs.md) to store the specified imported skeleton.
- *[ImportSkeleton](../../../../api/library/common/import/class.importskeleton_cs.md)* **import_skeleton** - Instance of the [ImportSkeleton](../../../../api/library/common/import/class.importskeleton_cs.md) class.

### Return value

true if the specified skeleton was successfully imported; otherwise, false.
## bool OnCheckSupportedAnimation ( ImportMeshSkinned import_mesh_skinned , ImportAnimation import_animation )

Animation import support check event handler function. This function is called each time when the *[CheckSupportedAnimation()](../../../...md#checkSupportedAnimation_ImportMeshSkinned_ImportAnimation_bool)* function is called. You can specify your custom actions to be performed on animation import.
### Arguments

- *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cs.md)* **import_mesh_skinned** - [ImportMeshSkinned structure](../../../../api/library/common/import/class.importmeshskinned_cs.md) pointer. The metadata for the imported skinned mesh.
- *[ImportAnimation](../../../../api/library/common/import/class.importanimation_cs.md)* **import_animation** - [ImportAnimation structure](../../../../api/library/common/import/class.importanimation_cs.md) pointer. The metadata for the imported animation.

### Return value

true if importing of the specified mesh animation is supported; otherwise, false.
## bool OnCheckDefaultAnimation ( ImportMeshSkinned import_mesh_skinned , ImportAnimation import_animation )

Default animation import check event handler function. This function is called each time when the *[CheckDefaultAnimation()](../../../...md#checkDefaultAnimation_ImportMeshSkinned_ImportAnimation_bool)* function is called. You can specify your custom actions to be performed on animation import.
### Arguments

- *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cs.md)* **import_mesh_skinned** - [ImportMeshSkinned structure](../../../../api/library/common/import/class.importmeshskinned_cs.md) pointer. The metadata for the imported skinned mesh.
- *[ImportAnimation](../../../../api/library/common/import/class.importanimation_cs.md)* **import_animation** - [ImportAnimation structure](../../../../api/library/common/import/class.importanimation_cs.md) pointer. The metadata for the imported animation.

### Return value

true if the specified mesh animation is the default one for the imported mesh; otherwise, false.
