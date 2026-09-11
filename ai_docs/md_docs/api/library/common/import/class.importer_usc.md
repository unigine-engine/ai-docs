# Unigine::Importer Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to manage a file importer. File importers are used by the Engine's [import system](../../../../api/library/common/import/index.md) to bring the data stored in various non-native formats to UNIGINE. Each importer can be used to import multiple file formats, but there shouldn't be two or more importers registered for a single file format.


## Importer Class

### Members

## void setAnimationsProcessor ( string processor )

Sets a new import [processor](../../../../api/library/common/import/class.importprocessor_usc.md) to be used for importing animations.
### Arguments

- *string* **processor** - The animations import [processor](../../../../api/library/common/import/class.importprocessor_usc.md).

## const char * getAnimationsProcessor () const

Returns the current import [processor](../../../../api/library/common/import/class.importprocessor_usc.md) to be used for importing animations.
### Return value

Current animations import [processor](../../../../api/library/common/import/class.importprocessor_usc.md).
## void setSkeletonsProcessor ( string processor )

Sets a new import [processor](../../../../api/library/common/import/class.importprocessor_usc.md) to be used for importing skeletons.
### Arguments

- *string* **processor** - The skeletons import [processor](../../../../api/library/common/import/class.importprocessor_usc.md).

## const char * getSkeletonsProcessor () const

Returns the current import [processor](../../../../api/library/common/import/class.importprocessor_usc.md) to be used for importing skeletons.
### Return value

Current skeletons import [processor](../../../../api/library/common/import/class.importprocessor_usc.md).
## void setLightsProcessor ( string processor )

Sets a new import [processor](../../../../api/library/common/import/class.importprocessor_usc.md) to be used for importing light sources.
### Arguments

- *string* **processor** - The lights import [processor](../../../../api/library/common/import/class.importprocessor_usc.md).

## const char * getLightsProcessor () const

Returns the current import [processor](../../../../api/library/common/import/class.importprocessor_usc.md) to be used for importing light sources.
### Return value

Current lights import [processor](../../../../api/library/common/import/class.importprocessor_usc.md).
## void setMeshesProcessor ( string processor )

Sets a new import [processor](../../../../api/library/common/import/class.importprocessor_usc.md) to be used for importing meshes.
### Arguments

- *string* **processor** - The meshes import [processor](../../../../api/library/common/import/class.importprocessor_usc.md).

## const char * getMeshesProcessor () const

Returns the current import [processor](../../../../api/library/common/import/class.importprocessor_usc.md) to be used for importing meshes.
### Return value

Current meshes import [processor](../../../../api/library/common/import/class.importprocessor_usc.md).
## void setMeshSkinnedsProcessor ( string processor )

Sets a new import [processor](../../../../api/library/common/import/class.importprocessor_usc.md) to be used for importing skinned meshes.
### Arguments

- *string* **processor** - The skinned meshes import [processor](../../../../api/library/common/import/class.importprocessor_usc.md).

## const char * getMeshSkinnedsProcessor () const

Returns the current import [processor](../../../../api/library/common/import/class.importprocessor_usc.md) to be used for importing skinned meshes.
### Return value

Current skinned meshes import [processor](../../../../api/library/common/import/class.importprocessor_usc.md).
## void setNodesProcessor ( string processor )

Sets a new import [processor](../../../../api/library/common/import/class.importprocessor_usc.md) to be used for importing nodes.
### Arguments

- *string* **processor** - The nodes import [processor](../../../../api/library/common/import/class.importprocessor_usc.md).

## const char * getNodesProcessor () const

Returns the current import [processor](../../../../api/library/common/import/class.importprocessor_usc.md) to be used for importing nodes.
### Return value

Current nodes import [processor](../../../../api/library/common/import/class.importprocessor_usc.md).
## void setCamerasProcessor ( string processor )

Sets a new import [processor](../../../../api/library/common/import/class.importprocessor_usc.md) to be used for importing cameras.
### Arguments

- *string* **processor** - The cameras import [processor](../../../../api/library/common/import/class.importprocessor_usc.md).

## const char * getCamerasProcessor () const

Returns the current import [processor](../../../../api/library/common/import/class.importprocessor_usc.md) to be used for importing cameras.
### Return value

Current cameras import [processor](../../../../api/library/common/import/class.importprocessor_usc.md).
## void setMaterialsProcessor ( string processor )

Sets a new import [processor](../../../../api/library/common/import/class.importprocessor_usc.md) to be used for importing materials.
### Arguments

- *string* **processor** - The materials import [processor](../../../../api/library/common/import/class.importprocessor_usc.md).

## const char * getMaterialsProcessor () const

Returns the current import [processor](../../../../api/library/common/import/class.importprocessor_usc.md) to be used for importing materials.
### Return value

Current materials import [processor](../../../../api/library/common/import/class.importprocessor_usc.md).
## void setOutputFilepath ( string filepath )

Sets a new resulting output file path for imported scene component(s). In case a set of files is generated, the path to resulting `*.node` file will be returned.
### Arguments

- *string* **filepath** - The output file path.

## const char * getOutputFilepath () const

Returns the current resulting output file path for imported scene component(s). In case a set of files is generated, the path to resulting `*.node` file will be returned.
### Return value

Current output file path.
## void setTexturesProcessor ( string processor )

Sets a new import [processor](../../../../api/library/common/import/class.importprocessor_usc.md) to be used for importing textures.
### Arguments

- *string* **processor** - The textures import [processor](../../../../api/library/common/import/class.importprocessor_usc.md).

## const char * getTexturesProcessor () const

Returns the current import [processor](../../../../api/library/common/import/class.importprocessor_usc.md) to be used for importing textures.
### Return value

Current textures import [processor](../../../../api/library/common/import/class.importprocessor_usc.md).
---

## static Importer ( )

Constructor. Creates an empty importer.
## Importer getImporter ( )

Returns the [importer](../../../../api/library/common/import/class.importer_usc.md) itself.
### Return value

Importer itself.
## bool containsParameter ( string name )

Returns a value indicating whether the list of import parameters includes a parameter with a given name.
### Arguments

- *string* **name** - Parameter name.

### Return value

true if the list of import parameters includes a parameter with a given name; otherwise, false.
## void setParameterInt ( string name , int v )

Sets a new value for the specified *integer* parameter. There are [built-in parameters](../../../../principles/import_system/index.md#param_int) that can also be used in custom importers.
### Arguments

- *string* **name** - Name of the *integer* parameter.
- *int* **v** - New value to be set.

## int getParameterInt ( string name )

Returns the current value of the specified *integer* parameter. There are [built-in parameters](../../../../principles/import_system/index.md#param_int) that can also be used in custom importers.
### Arguments

- *string* **name** - Name of the *integer* parameter.

### Return value

Value of the *integer* parameter.
## void setParameterFloat ( string name , float v )

Sets a new value for the specified *float* parameter. There are [built-in parameters](../../../../principles/import_system/index.md#param_int) that can also be used in custom importers.
### Arguments

- *string* **name** - Name of the *float* parameter.
- *float* **v** - New value to be set.

## float getParameterFloat ( string name )

Returns the current value of the specified *float* parameter. There are [built-in parameters](../../../../principles/import_system/index.md#param_int) that can also be used in custom importers.
### Arguments

- *string* **name** - Name of the *float* parameter.

### Return value

Value of the *float* parameter.
## void setParameterDouble ( string name , double v )

Sets a new value for the specified *double* parameter. There are [built-in parameters](../../../../principles/import_system/index.md#param_int) that can also be used in custom importers.
### Arguments

- *string* **name** - Name of the *double* parameter.
- *double* **v** - New value to be set.

## double getParameterDouble ( string name )

Returns the current value of the specified *double* parameter. There are [built-in parameters](../../../../principles/import_system/index.md#param_int) that can also be used in custom importers.
### Arguments

- *string* **name** - Name of the *double* parameter.

### Return value

Value of the *double* parameter.
## void setParameterString ( string name , string v )

Sets a new value for the specified string parameter. There are [built-in parameters](../../../../principles/import_system/index.md#param_int) that can also be used in custom importers.
### Arguments

- *string* **name** - Name of the string parameter.
- *string* **v** - New value to be set.

## string getParameterString ( string name )

Returns the current value of the specified string parameter. There are [built-in parameters](../../../../principles/import_system/index.md#param_int) that can also be used in custom importers.
### Arguments

- *string* **name** - Name of the string parameter.

### Return value

Value of the string parameter.
## bool addPreProcessor ( string type_name )

Adds an import [pre-processor](../../../../api/library/common/import/class.importprocessor_usc.md) with a given type name. There are [built-in pre-processors](../../../../principles/import_system/index.md#preprocessors) that can also be added to custom importers.
### Arguments

- *string* **type_name** - Pre-processor type name.

### Return value

true if the specified import pre-processor is successfully added; otherwise, false.
## void removePreProcessor ( string type_name )

Removes an import [pre-processor](../../../../api/library/common/import/class.importprocessor_usc.md) with a given type name. There are [built-in pre-processors](../../../../principles/import_system/index.md#preprocessors) that can also be added to custom importers.
### Arguments

- *string* **type_name** - Pre-processor type name.

## bool hasPreProcessor ( string type_name )

Returns a value indicating if an import [pre-processor](../../../../api/library/common/import/class.importprocessor_usc.md) with a given type name is used by the importer. There are [built-in pre-processors](../../../../principles/import_system/index.md#preprocessors) that can also be added to custom importers.
### Arguments

- *string* **type_name** - Pre-processor type name.

### Return value

true if an import pre-processor with a given type name is used by the importer; otherwise, false.
## bool addPostProcessor ( string type_name )

Adds an import [post-processor](../../../../api/library/common/import/class.importprocessor_usc.md) with a given type name. There are [built-in post-processors](../../../../principles/import_system/index.md#postprocessors) that can also be added to custom importers.
### Arguments

- *string* **type_name** - Post-processor type name to check.

## void removePostProcessor ( string type_name )

Removes an import [post-processor](../../../../api/library/common/import/class.importprocessor_usc.md) with a given type name. There are [built-in post-processors](../../../../principles/import_system/index.md#postprocessors) that can also be added to custom importers.
### Arguments

- *string* **type_name** - Post-processor type name.

## bool hasPostProcessor ( string type_name )

Returns a value indicating if an import [post-processor](../../../../api/library/common/import/class.importprocessor_usc.md) with a given type name is used by the importer. There are [built-in post-processors](../../../../principles/import_system/index.md#postprocessors) that can also be added to custom importers.
### Arguments

- *string* **type_name** - Post-processor type name to check.

### Return value

true if an import post-processor with a given type name is used by the importer; otherwise, false.
## ImportScene getScene ( )

Returns the imported scene.
### Return value

Instance of the *[ImportScene](../../../../api/library/common/import/class.importscene_usc.md)* class.
## bool init ( string filepath , int flags = ~0 )

Initializes the importer for the specified file using the given flags. Import flags specify which scene components are to be imported.
### Arguments

- *string* **filepath** - Path to a file to be imported.
- *int* **flags** - Set of import flags. Any combination of [IMPORT_*](#IMPORT_LIGHTS) flags, or ~0 to set all of them.

### Return value

true if the importer was initialized successfully; otherwise, 0.
## bool import ( string output_path )

Imports the contents of the input file to the specified output path.
### Arguments

- *string* **output_path** - Output path.

### Return value

true if the contents of the input file are successfully imported to the specified output path; otherwise, false.
## string getSourceFilepath ( )

Returns the path to the source file.
### Return value

Source file path.
## int getFlags ( )

Returns the current set of import flags (*[IMPORT_*](#IMPORT_LIGHTS)*) that were set at initialization.
## bool computeBoundBox ( ImportMesh import_mesh )

Computes a bound box for the specified mesh.
### Arguments

- *[ImportMesh](../../../../api/library/common/import/class.importmesh_usc.md)* **import_mesh** - Imported mesh for which a bound box is to be calculated.

### Return value

true if a bound box for the specified mesh is successfully calculated; otherwise, false.
## bool preprocess ( )

Starts execution of all [added](#addPreProcessor_cstr_bool) pre-processors.
### Return value

true if the pre-processing is completed successfully.
## bool postprocess ( )

Starts execution of all [added](#addPostProcessor_cstr_bool) post-processors. Post-processors can be used to manage files generated in the process of import.
### Return value

true if the post-processing is completed successfully.
## bool getBasis ( int up_axis , int front_axis , dmat4 & ret )

Returns the transformation matrix for the basis specified by axes.
### Arguments

- *int* **up_axis** - Up axis of the basis.
- *int* **front_axis** - Front axis of the basis.
- *dmat4 &* **ret** - Transformation matrix for the basis specified by axes.

### Return value

true the transformation matrix for the basis was successfully calculated; otherwise, false.
## bool onComputeBoundBox ( ImportMesh import_mesh )

Extendable method for custom bound box computation.
### Arguments

- *[ImportMesh](../../../../api/library/common/import/class.importmesh_usc.md)* **import_mesh** - Imported mesh for which a bound box is to be calculated.

### Return value

true if a bound box for the specified mesh was successfully calculated; otherwise, false.
## bool onInit ( ImportScene import_scene , string filepath )

Builds and initializes the imported [scene](../../../../api/library/common/import/class.importscene_usc.md) based on the data contained in the specified input file.
### Arguments

- *[ImportScene](../../../../api/library/common/import/class.importscene_usc.md)* **import_scene** - Imported scene (built from the data contained in the specified input file).
- *string* **filepath** - Path to an input file to be imported.

### Return value

true if the scene is successfully initialized using the data from the specified input file; otherwise, false.
## bool onImport ( string output_path )


Import event handler function. This function is called each time when the *[import()()](../../../...md#import_cstr_bool)* function is called. You can specify your custom actions to be performed on scene import.


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
## bool onImportTexture ( ImportProcessor processor , ImportTexture import_texture )


Texture import event handler function. This function is called each time when the *[importTexture()()](../../../...md#importTexture_ImportProcessor_ImportTexture_bool)* function is called. You can specify your custom actions to be performed on texture import.


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

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_usc.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_usc.md) used for this import operation.
- *[ImportTexture](../../../../api/library/common/import/class.importtexture_usc.md)* **import_texture** - Instance of the *[ImportTexture](../../../../api/library/common/import/class.importtexture_usc.md)* class.

### Return value

true if the specified texture was successfully imported; otherwise, false.
## bool onImportMaterial ( ImportProcessor processor , Material material , ImportMaterial import_material )


Material import event handler function. This function is called each time when the **[importMaterial()()](../../../...md#importMaterial_ImportProcessor_Material_ImportMaterial_bool)** function is called. You can specify your custom actions to be performed on material import.


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

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_usc.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_usc.md) used for this import operation.
- *[Material](../../../../api/library/rendering/class.material_usc.md)* **material** - Target [UNIGINE's material instance](../../../../api/library/rendering/class.material_usc.md) to store the specified imported material.
- *[ImportMaterial](../../../../api/library/common/import/class.importmaterial_usc.md)* **import_material** - Instance of the [ImportMaterial](../../../../api/library/common/import/class.importmaterial_usc.md) class.

### Return value

true if the specified material was successfully imported; otherwise, false.
## Light onImportLight ( ImportProcessor processor , ImportLight import_light )


Light import event handler function. This function is called each time when the **[importLight()()](../../../...md#importLight_ImportProcessor_ImportLight_Light)** function is called. You can specify your custom actions to be performed on light import.


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

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_usc.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_usc.md) used for this import operation.
- *[ImportLight](../../../../api/library/common/import/class.importlight_usc.md)* **import_light** - Instance of the [ImportLight](../../../../api/library/common/import/class.importlight_usc.md) class.

### Return value

[UNIGINE's light instance](../../../../api/library/lights/class.light_usc.md) that stores the specified imported light.
## Player onImportCamera ( ImportProcessor processor , ImportCamera import_camera )


Camera import event handler function. This function is called each time when the **[importCamera()()](../../../...md#importCamera_ImportProcessor_ImportCamera_Player)** function is called. You can specify your custom actions to be performed on camera import.


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

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_usc.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_usc.md) used for this import operation.
- *[ImportCamera](../../../../api/library/common/import/class.importcamera_usc.md)* **import_camera** - Instance of the [ImportCamera](../../../../api/library/common/import/class.importcamera_usc.md) class.

### Return value

[UNIGINE's player instance](../../../../api/library/players/class.player_usc.md) that stores the specified imported camera.
## bool onImportMesh ( ImportProcessor processor , Mesh mesh , ImportMesh import_mesh )


Mesh import event handler function. This function is called each time when the **[importMesh()()](../../../...md#importMesh_ImportProcessor_Mesh_ImportMesh_bool)** function is called. You can specify your custom actions to be performed on mesh import.


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

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_usc.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_usc.md) used for this import operation.
- *[Mesh](../../../../api/library/rendering/class.mesh_usc.md)* **mesh** - Target [UNIGINE's mesh instance](../../../../api/library/rendering/class.mesh_usc.md) to store the specified imported mesh.
- *[ImportMesh](../../../../api/library/common/import/class.importmesh_usc.md)* **import_mesh** - Instance of the [ImportMesh](../../../../api/library/common/import/class.importmesh_usc.md) class.

### Return value

true if the specified mesh was successfully imported; otherwise, false.
## bool onImportMeshSkinned ( ImportProcessor processor , MeshSkinned mesh_skinned , ImportMeshSkinned import_mesh_skinned )


Skinned mesh import event handler function. This function is called each time when the **[importMeshSkinned()()](../../../...md#importMeshSkinned_ImportProcessor_MeshSkinned_ImportMeshSkinned_bool)** function is called. You can specify your custom actions to be performed on skinned mesh import.


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

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_usc.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_usc.md) used for this import operation.
- *[MeshSkinned](../../../../api/library/rendering/class.meshskinned_usc.md)* **mesh_skinned** - Target [UNIGINE's skinned mesh instance](../../../../api/library/rendering/class.meshskinned_usc.md) to store the specified imported skinned mesh.
- *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_usc.md)* **import_mesh_skinned** - Instance of the [ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_usc.md) class.

### Return value

true if the specified skinned mesh was successfully imported; otherwise, false.
## Node onImportNode ( ImportProcessor processor , ImportNode import_node )


Node import event handler function. This function is called each time when the **[importNode()()](../../../...md#importNode_ImportProcessor_ImportNode_Node)** function is called. You can specify your custom actions to be performed on node import.


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

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_usc.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_usc.md) used for this import operation.
- *[ImportNode](../../../../api/library/common/import/class.importnode_usc.md)* **import_node** - Instance of the [ImportNode](../../../../api/library/common/import/class.importnode_usc.md) class.

### Return value

[UNIGINE's node instance](../../../../api/library/nodes/class.node_usc.md) that stores the specified imported node.
## bool onImportNodeChild ( ImportProcessor processor , Node node_parent , ImportNode import_node_parent , Node node_child , ImportNode import_node_child )


Node import event handler function. This function is called each time when the **[importNodeChild()()](../../../...md#importNodeChild_ImportProcessor_Node_ImportNode_Node_ImportNode_bool)** function is called. You can specify your custom actions to be performed on importing and processing node hierarchies (e.g. assigning properties to node children).


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

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_usc.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_usc.md) used for this import operation.
- *[Node](../../../../api/library/nodes/class.node_usc.md)* **node_parent** - Target [UNIGINE's node instance](../../../../api/library/nodes/class.node_usc.md) to store the specified imported parent node.
- *[ImportNode](../../../../api/library/common/import/class.importnode_usc.md)* **import_node_parent** - Instance of the [ImportNode](../../../../api/library/common/import/class.importnode_usc.md) class for the parent node.
- *[Node](../../../../api/library/nodes/class.node_usc.md)* **node_child** - Target [UNIGINE's node instance](../../../../api/library/nodes/class.node_usc.md) to store the specified imported child node.
- *[ImportNode](../../../../api/library/common/import/class.importnode_usc.md)* **import_node_child** - Instance of the [ImportNode](../../../../api/library/common/import/class.importnode_usc.md) class for the child node.

### Return value

true if the specified parent node and its child node animation were successfully imported; otherwise, false.
## bool onImportAnimation ( ImportProcessor processor , MeshSkinnedAnimation animation , ImportAnimation import_animation )

Animation import event handler function. This function is called each time when the *[importAnimation()()](../../../...md#importAnimation_ImportProcessor_MeshSkinnedAnimation_ImportAnimation_bool)* function is called. You can specify your custom actions to be performed on animation import.
### Arguments

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_usc.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_usc.md) used for this import operation.
- *[MeshSkinnedAnimation](../../../../api/library/rendering/class.meshskinnedanimation_usc.md)* **animation** - Target [UNIGINE's mesh animation instance](../../../../api/library/rendering/class.meshskinnedanimation_usc.md) to store the specified imported mesh animation.
- *[ImportAnimation](../../../../api/library/common/import/class.importanimation_usc.md)* **import_animation** - [ImportAnimation structure](../../../../api/library/common/import/class.importanimation_usc.md) pointer. The metadata for the animation that needs to be imported.

### Return value

true if the specified mesh animation was successfully imported; otherwise, false.
## bool onImportAnimation ( ImportProcessor processor , MeshSkinnedAnimation animation , ImportMeshSkinned import_mesh_skinned , ImportAnimation import_animation )

Animation import event handler function. This function is called each time when the *[importAnimation()()](../../../...md#importAnimation_ImportProcessor_MeshSkinnedAnimation_ImportMeshSkinned_ImportAnimation_bool)* function is called. You can specify your custom actions to be performed on animation import.
### Arguments

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_usc.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_usc.md) used for this import operation.
- *[MeshSkinnedAnimation](../../../../api/library/rendering/class.meshskinnedanimation_usc.md)* **animation** - Target [UNIGINE's mesh animation instance](../../../../api/library/rendering/class.meshskinnedanimation_usc.md) to store the specified imported mesh animation.
- *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_usc.md)* **import_mesh_skinned** - [ImportMeshSkinned structure](../../../../api/library/common/import/class.importmeshskinned_usc.md) pointer. The metadata for the skinned mesh that needs to be imported.
- *[ImportAnimation](../../../../api/library/common/import/class.importanimation_usc.md)* **import_animation** - [ImportAnimation structure](../../../../api/library/common/import/class.importanimation_usc.md) pointer. The metadata for the animation that needs to be imported.

### Return value

true if the specified mesh animation was successfully imported; otherwise, false.
## bool onImportSkeleton ( ImportProcessor processor , Skeleton skeleton , ImportSkeleton import_skeleton )


Skeleton import event handler function. This function is called each time when the **[importSkeleton()()](../../../...md#importSkeleton_ImportProcessor_Skeleton_ImportSkeleton_bool)** function is called. You can specify your custom actions to be performed on skeleton import.


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

- *[ImportProcessor](../../../../api/library/common/import/class.importprocessor_usc.md)* **processor** - [Import processor](../../../../api/library/common/import/class.importprocessor_usc.md) used for this import operation.
- *[Skeleton](../../../../api/library/animations/skeletal/class.skeleton_usc.md)* **skeleton** - Target [UNIGINE's skeleton instance](../../../../api/library/animations/skeletal/class.skeleton_usc.md) to store the specified imported skeleton.
- *[ImportSkeleton](../../../../api/library/common/import/class.importskeleton_usc.md)* **import_skeleton** - Instance of the [ImportSkeleton](../../../../api/library/common/import/class.importskeleton_usc.md) class.

### Return value

true if the specified skeleton was successfully imported; otherwise, false.
## bool onCheckSupportedAnimation ( ImportMeshSkinned import_mesh_skinned , ImportAnimation import_animation )

Animation import support check event handler function. This function is called each time when the *[checkSupportedAnimation()()](../../../...md#checkSupportedAnimation_ImportMeshSkinned_ImportAnimation_bool)* function is called. You can specify your custom actions to be performed on animation import.
### Arguments

- *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_usc.md)* **import_mesh_skinned** - [ImportMeshSkinned structure](../../../../api/library/common/import/class.importmeshskinned_usc.md) pointer. The metadata for the imported skinned mesh.
- *[ImportAnimation](../../../../api/library/common/import/class.importanimation_usc.md)* **import_animation** - [ImportAnimation structure](../../../../api/library/common/import/class.importanimation_usc.md) pointer. The metadata for the imported animation.

### Return value

true if importing of the specified mesh animation is supported; otherwise, false.
## bool onCheckDefaultAnimation ( ImportMeshSkinned import_mesh_skinned , ImportAnimation import_animation )

Default animation import check event handler function. This function is called each time when the *[checkDefaultAnimation()()](../../../...md#checkDefaultAnimation_ImportMeshSkinned_ImportAnimation_bool)* function is called. You can specify your custom actions to be performed on animation import.
### Arguments

- *[ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_usc.md)* **import_mesh_skinned** - [ImportMeshSkinned structure](../../../../api/library/common/import/class.importmeshskinned_usc.md) pointer. The metadata for the imported skinned mesh.
- *[ImportAnimation](../../../../api/library/common/import/class.importanimation_usc.md)* **import_animation** - [ImportAnimation structure](../../../../api/library/common/import/class.importanimation_usc.md) pointer. The metadata for the imported animation.

### Return value

true if the specified mesh animation is the default one for the imported mesh; otherwise, false.
