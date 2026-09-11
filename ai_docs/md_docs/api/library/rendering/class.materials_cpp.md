# Unigine.Materials Class (CPP)

**Header:** #include <UnigineMaterials.h>

> **Notice:** This class is a singleton.


Interface for managing loaded [materials](../../../principles/world_structure/index.md#materials) via the code.


All materials existing in the project are preloaded at Engine initialization depending on the materials preload mode specified by the [`materials_preload`](../../../code/console/index.md#materials_preload) console command (enabled by default) and saved on world's saving or on calling the *[materials_save](../../../code/console/index.md#materials_save)* console command.


### See Also


- C++ API sample located in the folder **<UnigineSDK>/source/samples/Api/Systems/Materials**


## Materials Class

### Members

## void setPrecompileAllShaders ( bool shaders )

Sets a new value indicating if shader precompilation is enabled.
### Arguments

- *bool* **shaders** - Set **true** to enable shader precompilation; **false** - to disable it.

## bool isPrecompileAllShaders () const

Returns the current value indicating if shader precompilation is enabled.
### Return value

**true** if shader precompilation is enabled ; otherwise **false**.
## int getNumMaterials () const

Returns the current number of materials loaded for the current project.
### Return value

Current number of materials.
## static Event<> getEventEndReload () const

event triggered after all materials are reloaded (i. e. execution of [reloadMaterials()](#reloadMaterials_void) is finished), if the `materials_reload_event` console variable is enabled. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndReload event handler
void endreload_event_handler()
{
	Log::message("\Handling EndReload event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endreload_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Materials::getEventEndReload().connect(endreload_event_connections, endreload_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Materials::getEventEndReload().connect(endreload_event_connections, []() {
		Log::message("\Handling EndReload event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endreload_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endreload_event_connection;

// subscribe to the EndReload event with a handler function keeping the connection
Materials::getEventEndReload().connect(endreload_event_connection, endreload_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endreload_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endreload_event_connection.setEnabled(true);

// ...

// remove subscription to the EndReload event via the connection
endreload_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A EndReload event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndReload event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Materials::getEventEndReload().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId endreload_handler_id;

// subscribe to the EndReload event with a lambda handler function and keeping connection ID
endreload_handler_id = Materials::getEventEndReload().connect(e_connections, []() {
		Log::message("\Handling EndReload event (lambda).\n");
	}
);

// remove the subscription later using the ID
Materials::getEventEndReload().disconnect(endreload_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndReload events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Materials::getEventEndReload().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Materials::getEventEndReload().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<> getEventBeginReload () const

event triggered before reloading all loaded materials (i. e. when [reloadMaterials()](#reloadMaterials_void) is called), if the `materials_reload_event` console variable is enabled. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginReload event handler
void beginreload_event_handler()
{
	Log::message("\Handling BeginReload event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginreload_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Materials::getEventBeginReload().connect(beginreload_event_connections, beginreload_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Materials::getEventBeginReload().connect(beginreload_event_connections, []() {
		Log::message("\Handling BeginReload event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginreload_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginreload_event_connection;

// subscribe to the BeginReload event with a handler function keeping the connection
Materials::getEventBeginReload().connect(beginreload_event_connection, beginreload_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginreload_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginreload_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginReload event via the connection
beginreload_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A BeginReload event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginReload event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Materials::getEventBeginReload().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId beginreload_handler_id;

// subscribe to the BeginReload event with a lambda handler function and keeping connection ID
beginreload_handler_id = Materials::getEventBeginReload().connect(e_connections, []() {
		Log::message("\Handling BeginReload event (lambda).\n");
	}
);

// remove the subscription later using the ID
Materials::getEventBeginReload().disconnect(beginreload_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginReload events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Materials::getEventBeginReload().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Materials::getEventBeginReload().setEnabled(true);

```

</details>

### Return value

Event instance.
## bool isShadersCompiling () const

Returns the current value indicating if asynchronous compilation is being performed.
### Return value

**true** if asynchronous compilation is being performed; otherwise **false**.
## Ptr < CustomParameterLayout > getMaterialParameters () const

Returns the current layout of custom material parameters (the *[CustomParameterLayout](../../../api/library/common/class.customparameterlayout_cpp.md)* instance shared by all materials). Each parameter defined in this layout exists on every material.
### Return value

Current layout of custom material parameters
---

## Ptr < Material > loadMaterial ( const char * path )

Loads a material stored by the given path. The function can be used to load materials created during application execution or stored outside the `data` directory.
### Arguments

- *const char ** **path** - A path to the material (including its name).

### Return value

A loaded material.
## bool isMaterialGUID ( const UGUID & guid ) const

Returns a value indicating if a material with the specified GUID exists.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - A material [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

### Return value

true if the material with the specified GUID exists; otherwise, false.
## Ptr < Material > getMaterial ( int num ) const

Returns the material by its number.
### Arguments

- *int* **num** - Material number.

### Return value

A material.
## Ptr < Material > findManualMaterial ( const char * name ) const

Searches for a manual material by the given name.
### Arguments

- *const char ** **name** - A manual material name.

### Return value

A manual material smart pointer.
## Ptr < Material > findMaterialByGUID ( const UGUID & guid ) const

Searches for a material with the given GUID.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - A material [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

### Return value

A material smart pointer.
## Ptr < Material > findMaterialByFileGUID ( const UGUID & guid ) const

Searches for a material with the given GUID of a material file.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - A [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of a material file.

### Return value

A material smart pointer.
## Ptr < Material > findMaterialByPath ( const char * path ) const

Searches for a material stored by the specified path.
### Arguments

- *const char ** **path** - A loading path of the material (including a material's name).

### Return value

A material smart pointer.
## void setCachedMaterial ( const Ptr < Material > & mat )

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

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)> &* **mat** - The material to be modified in runtime.

## Ptr < Material > getCachedMaterial ( )

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
## void setCachedState ( const char * name , int value )

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

- *const char ** **name** - The name of the state to be changed.
- *int* **value** - The target state value.

## bool removeMaterial ( const UGUID & guid , bool remove_file = 0 , bool remove_children = 1 )

Deletes a material. If the *remove_file* flag is enabled, the material file will be deleted as well. If the flag is disabled, the deleted material will be loaded again on the next application start-up. If the *remove_children* flag is enabled, all the children of the material will be deleted as well.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - GUID of the material to be removed.
- *bool* **remove_file** - Flag indicating if the material file will be deleted.
- *bool* **remove_children** - Flag indicating if all the children of the material will be also deleted.

### Return value

true if the material is deleted successfully; otherwise, false.
## bool replaceMaterial ( const Ptr < Material > & material , const Ptr < Material > & new_material )

Replaces the material with the given one.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)> &* **material** - A material to be replaced.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)> &* **new_material** - A replacing material.

### Return value

true if the material is replaced successfully; otherwise, false.
## bool saveMaterials ( ) const

Saves changes made for all loaded materials.
### Return value

true if materials are saved successfully; otherwise, false.
## void reloadMaterials ( )

Reloads all loaded materials.
## void destroyShaders ( )

Deletes all shaders used for the loaded materials.
## void destroyTextures ( )

Deletes all textures used by the loaded materials.
## void createShaders ( )

Creates all shaders for all loaded materials.
## void createRenderMaterials ( )

Creates render materials (internal materials required for rendering). For example, you can create all necessary render materials during initialization to avoid spikes that may occur later.
## void createShaderCacheAsync ( )

Creates the shader cache for all loaded materials in asynchronous mode: missing shader permutations are queued for background compilation. A loading screen with progress is displayed while the materials are iterated.
## void createShaderCacheForce ( )

Creates the shader cache for all loaded materials immediately: every missing shader permutation is compiled in a blocking multithreaded batch while a loading screen with progress is displayed.
## void createShadersFromCache ( )

Compiles the shaders available in the shader cache.
## void flushShadersCompiling ( )

Force-compiles all shaders that are queued for the asynchronous compilation.
## unsigned int getMaterialFeatureBits ( unsigned int material_id ) const

Returns the screen-space effect feature bits of the material with the given runtime ID. This makes it possible to query the flags by a material ID obtained from the GPU buffers without having the material itself.
### Arguments

- *unsigned int* **material_id** - Runtime material ID.

### Return value

Material feature bits, or 0 if no material with this ID exists.
## unsigned int getMaterialMask ( unsigned int material_id ) const

Returns the material mask of the material with the given runtime ID.
### Arguments

- *unsigned int* **material_id** - Runtime material ID.

### Return value

Material mask, or 0 if no material with this ID exists.
