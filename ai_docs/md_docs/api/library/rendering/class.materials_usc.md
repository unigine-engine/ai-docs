# Unigine.Materials Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


Interface for managing loaded [materials](../../../principles/world_structure/index.md#materials) via the code.


All materials existing in the project are preloaded at Engine initialization depending on the materials preload mode specified by the [`materials_preload`](../../../code/console/index.md#materials_preload) console command (enabled by default) and saved on world's saving or on calling the *[materials_save](../../../code/console/index.md#materials_save)* console command.


### See Also


- C++ API sample located in the folder **<UnigineSDK>/source/samples/Api/Systems/Materials**


## Materials Class

### Members

## void setPrecompileAllShaders ( int shaders )

Sets a new value indicating if shader precompilation is enabled.
### Arguments

- *int* **shaders** - The shader precompilation

## int isPrecompileAllShaders () const

Returns the current value indicating if shader precompilation is enabled.
### Return value

Current shader precompilation
## int getNumMaterials () const

Returns the current number of materials loaded for the current project.
### Return value

Current number of materials.
## static getEventEndReload () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventBeginReload () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## int isShadersCompiling () const

Returns the current value indicating if asynchronous compilation is being performed.
### Return value

Current asynchronous compilation is being performed
## CustomParameterLayout getMaterialParameters () const

Returns the current layout of custom material parameters (the *[CustomParameterLayout](../../../api/library/common/class.customparameterlayout_usc.md)* instance shared by all materials). Each parameter defined in this layout exists on every material.
### Return value

Current layout of custom material parameters
---

## Material engine.materials. loadMaterial ( string path )

Loads a material stored by the given path. The function can be used to load materials created during application execution or stored outside the `data` directory.
### Arguments

- *string* **path** - A path to the material (including its name).

### Return value

A loaded material.
## int engine.materials. isMaterialGUID ( UGUID guid )

Returns a value indicating if a material with the specified GUID exists.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - A material [GUID](../../../api/library/filesystem/class.uguid_usc.md).

### Return value

**1** if the material with the specified GUID exists; otherwise, **0**.
## Material engine.materials. getMaterial ( int num )

Returns the material by its number.
### Arguments

- *int* **num** - Material number.

### Return value

A material.
## Material engine.materials. findManualMaterial ( string name )

Searches for a manual material by the given name.
### Arguments

- *string* **name** - A manual material name.

### Return value

A manual material instance.
## Material engine.materials. findMaterialByGUID ( UGUID guid )

Searches for a material with the given GUID.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - A material [GUID](../../../api/library/filesystem/class.uguid_usc.md).

### Return value

A material instance.
## Material engine.materials. findMaterialByFileGUID ( UGUID guid )

Searches for a material with the given GUID of a material file.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - A [GUID](../../../api/library/filesystem/class.uguid_usc.md) of a material file.

### Return value

A material instance.
## Material engine.materials. findMaterialByPath ( string path )

Searches for a material stored by the specified path.
### Arguments

- *string* **path** - A loading path of the material (including a material's name).

### Return value

A material instance.
## void engine.materials. setCachedMaterial ( Material mat )

 Sets the material to be modified in runtime. This method is used together with [setCachedState](#setCachedState_cstr_int_void) and [getCachedMaterial()](#getCachedMaterial_Material) to change the material state in runtime without the necessity to recalculate the materials every frame and recompile the shaders. Using these methods is highly recommended if the material states are changed almost every frame or several times per frame.
Let's review an example use case that can make use of these methods. Assume that you have a performance-consuming material and you want to reduce its quality when it's rendered in reflections. The following pseudo code demonstrates the approach to using these methods:


```text
MaterialPtr get_effect_material(bool quality)
	{
		Materials::setCachedMaterial(my_effect);

		Materials::setCachedState("quality", quality);

		return Material::getCachedMaterial();
	}

// switching quality of material depending on where it's rendered
void event()
	{
		bool quality = true;
		if (Renderer::isReflection())
			quality = false;

		MaterialPtr mat = get_effect_material(quality);
	}

```


### Arguments

- *[Material](../../../api/library/rendering/class.material_usc.md)* **mat** - The material to be modified in runtime.

## Material engine.materials. getCachedMaterial ( )

 Returns the material modified in runtime. This method is used together with [setCachedMaterial()](#setCachedMaterial_Material_void) and [setCachedState](#setCachedState_cstr_int_void) to change the material state in runtime without the necessity to recalculate the materials every frame and recompile the shaders. Using these methods is highly recommended if the material states are changed almost every frame or several times per frame.
Let's review an example use case that can make use of these methods. Assume that you have a performance-consuming material and you want to reduce its quality when it's rendered in reflections. The following pseudo code demonstrates the approach to using these methods:


```text
MaterialPtr get_effect_material(bool quality)
	{
		Materials::setCachedMaterial(my_effect);

		Materials::setCachedState("quality", quality);

		return Material::getCachedMaterial();
	}

// switching quality of material depending on where it's rendered
void event()
	{
		bool quality = true;
		if (Renderer::isReflection())
			quality = false;

		MaterialPtr mat = get_effect_material(quality);
	}

```


### Return value

The material modified in runtime.
## void engine.materials. setCachedState ( string name , int value )

 Sets the target state for the material to modify it in runtime. This method is used together with [setCachedMaterial()](#setCachedMaterial_Material_void) and [getCachedMaterial()](#getCachedMaterial_Material) to change the material state in runtime without the necessity to recalculate the materials every frame and recompile the shaders. Using these methods is highly recommended if the material states are changed almost every frame or several times per frame.
Let's review an example use case that can make use of these methods. Assume that you have a performance-consuming material and you want to reduce its quality when it's rendered in reflections. The following pseudo code demonstrates the approach to using these methods:


```text
MaterialPtr get_effect_material(bool quality)
	{
		Materials::setCachedMaterial(my_effect);

		Materials::setCachedState("quality", quality);

		return Material::getCachedMaterial();
	}

// switching quality of material depending on where it's rendered
void event()
	{
		bool quality = true;
		if (Renderer::isReflection())
			quality = false;

		MaterialPtr mat = get_effect_material(quality);
	}

```


### Arguments

- *string* **name** - The name of the state to be changed.
- *int* **value** - The target state value.

## int engine.materials. removeMaterial ( UGUID guid , int remove_file = 0 , int remove_children = 1 )

Deletes a material. If the *remove_file* flag is enabled, the material file will be deleted as well. If the flag is disabled, the deleted material will be loaded again on the next application start-up. If the *remove_children* flag is enabled, all the children of the material will be deleted as well.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - GUID of the material to be removed.
- *int* **remove_file** - Flag indicating if the material file will be deleted.
- *int* **remove_children** - Flag indicating if all the children of the material will be also deleted.

### Return value

**1** if the material is deleted successfully; otherwise, **0**.
## int engine.materials. replaceMaterial ( Material material , Material new_material )

Replaces the material with the given one.
### Arguments

- *[Material](../../../api/library/rendering/class.material_usc.md)* **material** - A material to be replaced.
- *[Material](../../../api/library/rendering/class.material_usc.md)* **new_material** - A replacing material.

### Return value

**1** if the material is replaced successfully; otherwise, **0**.
## int engine.materials. saveMaterials ( )

Saves changes made for all loaded materials.
### Return value

**1** if materials are saved successfully; otherwise, **0**.
## void engine.materials. reloadMaterials ( )

Reloads all loaded materials.
## void engine.materials. destroyShaders ( )

Deletes all shaders used for the loaded materials.
## void engine.materials. destroyTextures ( )

Deletes all textures used by the loaded materials.
## void engine.materials. createShaders ( )

Creates all shaders for all loaded materials.
## void engine.materials. createRenderMaterials ( )

Creates render materials (internal materials required for rendering). For example, you can create all necessary render materials during initialization to avoid spikes that may occur later.
## void engine.materials. createShaderCacheAsync ( )

Creates the shader cache for all loaded materials in asynchronous mode: missing shader permutations are queued for background compilation. A loading screen with progress is displayed while the materials are iterated.
## void engine.materials. createShaderCacheForce ( )

Creates the shader cache for all loaded materials immediately: every missing shader permutation is compiled in a blocking multithreaded batch while a loading screen with progress is displayed.
## void engine.materials. createShadersFromCache ( )

Compiles the shaders available in the shader cache.
## void engine.materials. flushShadersCompiling ( )

Force-compiles all shaders that are queued for the asynchronous compilation.
## unsigned int engine.materials. getMaterialFeatureBits ( unsigned int material_id )

Returns the screen-space effect feature bits of the material with the given runtime ID. This makes it possible to query the flags by a material ID obtained from the GPU buffers without having the material itself.
### Arguments

- *unsigned int* **material_id** - Runtime material ID.

### Return value

Material feature bits, or 0 if no material with this ID exists.
## unsigned int engine.materials. getMaterialMask ( unsigned int material_id )

Returns the material mask of the material with the given runtime ID.
### Arguments

- *unsigned int* **material_id** - Runtime material ID.

### Return value

Material mask, or 0 if no material with this ID exists.
