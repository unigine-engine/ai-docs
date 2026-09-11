# Unigine.Materials Class (CS)

> **Notice:** This class is a singleton.


Interface for managing loaded [materials](../../../principles/world_structure/index.md#materials) via the code.


All materials existing in the project are preloaded at Engine initialization depending on the materials preload mode specified by the [`materials_preload`](../../../code/console/index.md#materials_preload) console command (enabled by default) and saved on world's saving or on calling the *[materials_save](../../../code/console/index.md#materials_save)* console command.


### See Also


- C++ API sample located in the folder **<UnigineSDK>/source/samples/Api/Systems/Materials**


## Materials Class

### Properties

## bool PrecompileAllShaders

The value indicating if shader precompilation is enabled.
## 🔒︎ int NumMaterials

The number of materials loaded for the current project.
## 🔒︎ Event EventEndReload

The event triggered after all materials are reloaded (i. e. execution of [ReloadMaterials()](#reloadMaterials_void) is finished), if the `materials_reload_event` console variable is enabled. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndReload event handler
void endreload_event_handler()
{
	Log.Message("\Handling EndReload event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endreload_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Materials.EventEndReload.Connect(endreload_event_connections, endreload_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Materials.EventEndReload.Connect(endreload_event_connections, () => {
		Log.Message("Handling EndReload event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endreload_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndReload event with a handler function
Materials.EventEndReload.Connect(endreload_event_handler);

// remove subscription to the EndReload event later by the handler function
Materials.EventEndReload.Disconnect(endreload_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endreload_event_connection;

// subscribe to the EndReload event with a lambda handler function and keeping the connection
endreload_event_connection = Materials.EventEndReload.Connect(() => {
		Log.Message("Handling EndReload event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endreload_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endreload_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endreload_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndReload events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Materials.EventEndReload.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Materials.EventEndReload.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginReload

The event triggered before reloading all loaded materials (i. e. when [ReloadMaterials()](#reloadMaterials_void) is called), if the `materials_reload_event` console variable is enabled. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginReload event handler
void beginreload_event_handler()
{
	Log.Message("\Handling BeginReload event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginreload_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Materials.EventBeginReload.Connect(beginreload_event_connections, beginreload_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Materials.EventBeginReload.Connect(beginreload_event_connections, () => {
		Log.Message("Handling BeginReload event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginreload_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginReload event with a handler function
Materials.EventBeginReload.Connect(beginreload_event_handler);

// remove subscription to the BeginReload event later by the handler function
Materials.EventBeginReload.Disconnect(beginreload_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginreload_event_connection;

// subscribe to the BeginReload event with a lambda handler function and keeping the connection
beginreload_event_connection = Materials.EventBeginReload.Connect(() => {
		Log.Message("Handling BeginReload event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginreload_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginreload_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginreload_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginReload events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Materials.EventBeginReload.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Materials.EventBeginReload.Enabled = true;

```

</details>

## 🔒︎ bool IsShadersCompiling

The value indicating if asynchronous compilation is being performed.
## 🔒︎ CustomParameterLayout MaterialParameters

The layout of custom material parameters (the *[CustomParameterLayout](../../../api/library/common/class.customparameterlayout_cs.md)* instance shared by all materials). Each parameter defined in this layout exists on every material.
### Members

---

## Material LoadMaterial ( string path )

Loads a material stored by the given path. The function can be used to load materials created during application execution or stored outside the `data` directory.
### Arguments

- *string* **path** - A path to the material (including its name).

### Return value

A loaded material.
## bool IsMaterialGUID ( UGUID guid )

Returns a value indicating if a material with the specified GUID exists.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - A material [GUID](../../../api/library/filesystem/class.uguid_cs.md).

### Return value

true if the material with the specified GUID exists; otherwise, false.
## Material GetMaterial ( int num )

Returns the material by its number.
### Arguments

- *int* **num** - Material number.

### Return value

A material.
## Material FindManualMaterial ( string name )

Searches for a manual material by the given name.
### Arguments

- *string* **name** - A manual material name.

### Return value

A manual material instance.
## Material FindMaterialByGUID ( UGUID guid )

Searches for a material with the given GUID.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - A material [GUID](../../../api/library/filesystem/class.uguid_cs.md).

### Return value

A material instance.
## Material FindMaterialByFileGUID ( UGUID guid )

Searches for a material with the given GUID of a material file.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - A [GUID](../../../api/library/filesystem/class.uguid_cs.md) of a material file.

### Return value

A material instance.
## Material FindMaterialByPath ( string path )

Searches for a material stored by the specified path.
### Arguments

- *string* **path** - A loading path of the material (including a material's name).

### Return value

A material instance.
## void SetCachedMaterial ( Material mat )

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

- *[Material](../../../api/library/rendering/class.material_cs.md)* **mat** - The material to be modified in runtime.

## Material GetCachedMaterial ( )

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
## void SetCachedState ( string name , int value )

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

## bool RemoveMaterial ( UGUID guid , bool remove_file = 0 , bool remove_children = 1 )

Deletes a material. If the *remove_file* flag is enabled, the material file will be deleted as well. If the flag is disabled, the deleted material will be loaded again on the next application start-up. If the *remove_children* flag is enabled, all the children of the material will be deleted as well.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - GUID of the material to be removed.
- *bool* **remove_file** - Flag indicating if the material file will be deleted.
- *bool* **remove_children** - Flag indicating if all the children of the material will be also deleted.

### Return value

true if the material is deleted successfully; otherwise, false.
## bool ReplaceMaterial ( Material material , Material new_material )

Replaces the material with the given one.
### Arguments

- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - A material to be replaced.
- *[Material](../../../api/library/rendering/class.material_cs.md)* **new_material** - A replacing material.

### Return value

true if the material is replaced successfully; otherwise, false.
## bool SaveMaterials ( )

Saves changes made for all loaded materials.
### Return value

true if materials are saved successfully; otherwise, false.
## void ReloadMaterials ( )

Reloads all loaded materials.
## void DestroyShaders ( )

Deletes all shaders used for the loaded materials.
## void DestroyTextures ( )

Deletes all textures used by the loaded materials.
## void CreateShaders ( )

Creates all shaders for all loaded materials.
## void CreateRenderMaterials ( )

Creates render materials (internal materials required for rendering). For example, you can create all necessary render materials during initialization to avoid spikes that may occur later.
## void CreateShaderCacheAsync ( )

Creates the shader cache for all loaded materials in asynchronous mode: missing shader permutations are queued for background compilation. A loading screen with progress is displayed while the materials are iterated.
## void CreateShaderCacheForce ( )

Creates the shader cache for all loaded materials immediately: every missing shader permutation is compiled in a blocking multithreaded batch while a loading screen with progress is displayed.
## void CreateShadersFromCache ( )

Compiles the shaders available in the shader cache.
## void FlushShadersCompiling ( )

Force-compiles all shaders that are queued for the asynchronous compilation.
## uint GetMaterialFeatureBits ( uint material_id )

Returns the screen-space effect feature bits of the material with the given runtime ID. This makes it possible to query the flags by a material ID obtained from the GPU buffers without having the material itself.
### Arguments

- *uint* **material_id** - Runtime material ID.

### Return value

Material feature bits, or 0 if no material with this ID exists.
## uint GetMaterialMask ( uint material_id )

Returns the material mask of the material with the given runtime ID.
### Arguments

- *uint* **material_id** - Runtime material ID.

### Return value

Material mask, or 0 if no material with this ID exists.
