# Accessing Nodes and Files via Properties


> **Notice:** The approach described in is article is not intended for projects using C# Component System, where assets are managed via [components](../../../api/library/common/logic/component_system/cs/class.component.md#parameters).


Every resource ([asset](../../../editor2/assets_workflow/index.md)) used in your project, be it a node, a mesh, a material, a texture, or any other, has a unique identifier (GUID). A **GUID** identifies a path to the asset (i.e., location of the asset in the project). GUIDs are used to keep all links and dependencies between the assets, **regardless of their name and location within the project** (when you change asset's name or location within the project, its GUID does not change).


Using GUIDs to link your assets is safer than using file names, as you don't have to worry that your material will lose a texture when you change its name. However, managing GUIDs directly is rather confusing.


[Property](../../../principles/properties/index.md) allows linking certain assets to a [node](../../../start/index.md#node) via GUIDs without even thinking about them, giving you easy access to these assets. There is a number of property parameter types making that possible:


- **material** - for materials
- **property** - for properties
- **file** - for all other files (textures, meshes, sounds, etc.)


The *node* property parameter type allows linking a node to another node in a similar way using the ID.


Artists and programmers developing a project should be able to work independently: artists prepare content (textures, materials, models etc.), while programmers write code implementing logic that performs certain operations with the content.


Using properties makes the whole process simpler:


- Artists can safely move or rename files and nodes. Programmers always work with properties: create them, set and read parameter values (which can represent links to various assets). Artists can set property parameters too, they do it [via the Editor](../../../editor2/properties_settings/organizing_properties/index.md#assign_property).
- Neither artists nor programmers should work with node IDs or GUIDs and remember them. A programmer always has at hand a variable (property parameter) that gives access to any necessary node or a file.


General property-based workflow is clear and simple. There are two basic cases, depending on the logic of your project:


- [For projects implemented without the Component System](#no_cs)
- [For C++ projects implemented using the Component System](#using_cs)


## General Workflow


The general workflow for all projects that don't use the [C++ Component System](../../../principles/component_system/component_system_cpp/index.md) should be as follows:


1. First, we create a property to store links to all nodes and assets that we need and save it to our project's `data` folder. For example, the property can be like this: ```xml <?xml version="1.0" encoding="utf-8"?> <property version="2.16.0.2" name="my_property" parent_name="node_base" manual="1" editable="1"> <parameter name="some_float" type="float">30.5</parameter> <parameter name="some_string" type="string">Hello from my_property!</parameter> <parameter name="some_node" type="node">0</parameter> <parameter name="some_material" type="material"></parameter> <parameter name="some_mesh" type="file"></parameter> <parameter name="some_file" type="file"></parameter> </property> ```
2. Then open the UnigineEditor, select the desired node, click *Add new property* and drag the property file to the new property field, then drag all necessary assets and nodes to the corresponding fields of the property (see the video below). ![](assign_prop_params.gif) *Linking nodes and assets to the property*
3. As we don't use components, we'll have to be bound to names of nodes to which the properties with links to assets are assigned. So, in the *[init()](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic_init)* method of the *WorldLogic* class we get a node by its name: ```cpp int AppWorldLogic::init() { /* ... */ NodePtr node = World::getNodeByName("node_name"); /* ... */ return 1; } ```
4. Then we get a property assigned to it: ```cpp PropertyPtr property = node->getProperty(); ```
5. Now we can use the property to get access to nodes and files:

  - **to get a material** we can simply use the corresponding node parameter: ```cpp property->getParameterPtr("node_param_name")->getValueMaterial(); ```
  - **to get a path to file**, we can simply use: ```cpp const char *path = property->getParameterPtr("file_param_name")->getValueFile(); ``` As we have a path to our file, we can use it, for example: ```cpp // to create a node reference NodeReferencePtr node_ref = NodeReference::create(path_to_node_file); // to load a sound source SoundSourcePtr sound = SoundSource::create(path_to_sound_file); ```


Let us use an example to illustrate this workflow.


### Usage Example


In this example we are going to manipulate nodes and assets linked to certain node using a property via C++ and C#.


Let us create a simple MeshStatic object named *my_object*, inherit a material from the **[mesh_base](../../../content/materials/library/mesh_base/index.md)** to assign to the surfaces of our object, and add some audio file (`*.mp3` or `*.oga`) to our project.


So, we link a `*.mesh` file, a material, the **material_ball** node from the default world and an audio file using the [property file described above](#property).


In our code we will:


- Rotate the linked node.
- Modify linked material and save changes.
- Generate a new object using a linked mesh.
- Play a linked audio file.


#### C++ Implementation


Below you'll find the C++ implementation of the example [described above](#example_description). You can copy and paste it to the `AppWorldLogic.cpp` file of your project.


<details>
<summary>AppWorldLogic.cpp | Close</summary>

**AppWorldLogic.cpp**


```cpp
#include "AppWorldLogic.h"
#include <UnigineMaterials.h>
#include <UnigineSounds.h>
#include <UnigineGame.h>
#include <UnigineWorld.h>
#include <UnigineFileSystem.h>

using namespace Unigine;
using namespace Math;
NodePtr my_node;                   // node to which a property with links is assigned
PropertyPtr property;              // property with all necessary links
MaterialPtr material;              // linked material
NodePtr param_node;                // linked node
SoundSourcePtr sound;	      	   // sound source to be played
ObjectMeshStaticPtr generated_obj; // object to be generated using the mesh

AppWorldLogic::AppWorldLogic() {

}

AppWorldLogic::~AppWorldLogic() {

}

int AppWorldLogic::init() {
	// getting the node to which a property with links to assets is assigned
	my_node = World::getNodeByName("my_object");

	// getting the property, that will be used to access all necessary files
	property = my_node->getProperty();
	// using access to property parameters to perform desired actions
	if (property) {
		// getting a material from the corresponding property parameter
		material = property->getParameterPtr("some_material")->getValueMaterial();

		// getting the path to the mesh file from the corresponding property parameter
		const char *mesh_file_name = property->getParameterPtr("some_mesh")->getValueFile();

		// creating the object by using the mesh
		generated_obj = ObjectMeshStatic::create(mesh_file_name);

		// setting the object position relative to another node position
		generated_obj->setWorldPosition(my_node->getWorldPosition());
		generated_obj->translate(vec3(-1.0f, 0.0f, 0.0f));

		// getting the path to the sound file from the corresponding property parameter
		const char *sound_file_name = property->getParameterPtr("some_file")->getValueFile();

		// getting a node from the corresponding property parameter
		param_node = property->getParameterPtr("some_node")->getValueNode();

		// creating and playing a sound from the file
		sound = SoundSource::create(sound_file_name);
		sound->setMaxDistance(100.0f);
		sound->setLoop(1);
		sound->play();

		// reporting results to the console
		Log::message("Path to mesh file: %s\nPath to sound file: %s\nNode ID: %d\n", mesh_file_name, sound_file_name, param_node->getID());
	}
	return 1;
}

// start of the main loop
int AppWorldLogic::update() {
	// Write here code to be called before updating each render frame: specify all graphics-related functions you want to be called every frame while your application executes.

	float ifps = Game::getIFps();

	// changing the material
	material->setParameterFloat4("albedo_color", vec4(Game::getRandomFloat(0.0f, 1.0f), Game::getRandomFloat(0.0f, 1.0f), Game::getRandomFloat(0.0f, 1.0f), 1.0f));

	// rotate linked node
	param_node->setRotation(param_node->getRotation() * quat(0, 0, 30.0f * ifps));

	return 1;
}

int AppWorldLogic::postUpdate() {
	// The engine calls this function before rendering each render frame: correct behavior after the state of the node has been updated.

	return 1;
}

int AppWorldLogic::updatePhysics() {
	// Write here code to be called before updating each physics frame: control physics in your application and put non-rendering calculations.
	// The engine calls updatePhysics() with the fixed rate (60 times per second by default) regardless of the FPS value.
	// WARNING: do not create, delete or change transformations of nodes here, because rendering is already in progress.

	return 1;
}
// end of the main loop

int AppWorldLogic::shutdown() {
	// Write here code to be called on world shutdown: delete resources that were created during world script execution to avoid memory leaks.
	// saving current material color (check it in the UnigineEditor to see that it was modified)
	material->save();
	return 1;
}

int AppWorldLogic::save(const Unigine::StreamPtr &stream) {
	// Write here code to be called when the world is saving its state: save custom user data to a file.

	UNIGINE_UNUSED(stream);
	return 1;
}

int AppWorldLogic::restore(const Unigine::StreamPtr &stream) {
	// Write here code to be called when the world is restoring its state: restore custom user data to a file here.

	UNIGINE_UNUSED(stream);
	return 1;
}

```

</details>


#### C# Implementation


> **Notice:** In C# projects using [C# Component System](../../../principles/component_system/component_system_cs/index.md), access to files and nodes is commonly [implemented via components](../../../code/csharp/usage/using_cs_component_system/index.md).


Below you'll find the C# implementation of the example [described above](#example_description). You can copy and paste it to the `AppWorldLogic.cs` file of your project.


<details>
<summary>AppWorldLogic.cs | Close</summary>

**AppWorldLogic.cs**


```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Unigine;

namespace UnigineApp
{
	class AppWorldLogic : WorldLogic
	{
		// World logic, it takes effect only when the world is loaded.
		// These methods are called right after corresponding world script's (UnigineScript) methods.
		Node my_node;						// node to which a property with links is assigned
		Property property;					// property with all necessary links
		Material material;					// linked material
		Node param_node;					// linked node
		SoundSource sound;					// sound source to be played
		ObjectMeshStatic generated_obj;		// object to be generated using the mesh

		public AppWorldLogic()
		{
		}

		public override bool Init()
		{
			// getting the node to which a property with links to assets is assigned
			my_node = World.GetNodeByName("my_object");

			// getting the property, that will be used to access all necessary files
			property = my_node.GetProperty();
			// using access to property parameters to perform desired actions
			if (property) {
				// getting a material from the corresponding property parameter
				material = property.GetParameterPtr("some_material").ValueMaterial;

				// getting the path to the mesh file from the corresponding property parameter
				String mesh_file_name = property.GetParameterPtr("some_mesh").ValueFile;

				// creating the object by using the mesh
				generated_obj = new ObjectMeshStatic(mesh_file_name);

				// setting the object position relative to another node position
				generated_obj.WorldPosition = my_node.WorldPosition;
				generated_obj.Translate(-1.0f, 0.0f, 0.0f);

				// getting the path to the sound file from the corresponding property parameter
				String sound_file_name = property.GetParameterPtr("some_file").ValueFile;

				// getting a node from the corresponding property parameter
				param_node = property.GetParameterPtr("some_node").ValueNode;

				// creating and playing a sound from the file
				sound = new SoundSource(sound_file_name);
				sound.MaxDistance = 100.0f;
				sound.Loop = 1;
				sound.Play();

				// reporting results to the console
				Log.Message("Path to mesh file: {0}\nPath to sound file: {1}\nNode ID: {2}\n", mesh_file_name, sound_file_name, param_node.ID);
			}
			return true;
		}

		// start of the main loop
		public override bool Update()
		{
			// Write here code to be called before updating each render frame: specify all graphics-related functions you want to be called every frame while your application executes.
			float ifps = Game.IFps;

			// changing the material
			 material.SetParameterFloat4("albedo_color", new vec4(Game.GetRandomFloat(0.0f, 1.0f), Game.GetRandomFloat(0.0f, 1.0f), Game.GetRandomFloat(0.0f, 1.0f), 1.0f));

			// rotate linked node
			param_node.SetRotation(param_node.GetRotation() * new quat(0, 0, 30.0f * ifps));

			return true;
		}

		public override bool PostUpdate()
		{
			// The engine calls this function before rendering each render frame: correct behavior after the state of the node has been updated.
			return true;
		}

		// end of the main loop

		public override bool Shutdown()
		{
			// Write here code to be called on world shutdown: delete resources that were created during world script execution to avoid memory leaks.
			// saving current material color (check it in the UnigineEditor to see that it was modified)
			material.Save();

			return true;
		}

		public override bool Save(Stream stream)
		{
			// Write here code to be called when the world is saving its state: save custom user data to a file.
			return true;
		}

		public override bool Restore(Stream stream)
		{
			// Write here code to be called when the world is restoring its state: restore custom user data to a file here.
			return true;
		}
	}
}

```

</details>


## C++ Component System Workflow


If you use [C++ Component System](../../../principles/component_system/component_system_cpp/index.md) in your project, the following workflow is recommended:


1. Create a component by inheriting a class from the *[ComponentBase](../../../api/library/common/logic/component_system/cpp/class.componentbase_cpp.md)*. The template of this class is available in the *UnigineComponentSystem.h* header.
2. Add fields to store links to all necessary nodes and files, materials, meshes, etc. (by using the *PROP_PARAM* macros).
3. Generate a `*.prop` file for this class (by compiling and running the application).
4. Open your world in the UnigineEditor and assign the generated component's property to the desired nodes.
5. Specify all links to nodes, materials, textures, meshes, other files to be used, by dragging them from the *[Asset Browser](../../../editor2/assets_workflow/index.md#asset_browser)* directly to the corresponding field of the property in the *[Parameters](../../../editor2/interface/index.md#parameters)* window. ![](assign_prop_params.gif) *Linking nodes and assets to the property.*
6. An instance of the component is created when you launch your application. This instance has variables providing access to all used assets.


For more detailed information on using C++ Component System, see the [C++ Component System Usage Example](../../../code/usage/using_component_system/index.md).


## Global Properties for Multiple Worlds


Sometimes you may need to have a property with links to assets (like [described above](#example_description)), that you want to be used in multiple worlds, a sort of **global self-sufficient property, not assigned to any node**. Such a property can be used, for example, to store settings for a particular type of weapon (FBX-model, shooting sounds, nodes with particle systems for VFX, etc. ) to be used globally in various levels of the game.


The workflow here is as follows:


1. First, we create a property to store links to all nodes and assets that we need and save it to our project's `data` folder. For example, the property can be like this: ```xml <?xml version="1.0" encoding="utf-8"?> <property version="2.16.0.2" name="my_property" parent_name="node_base" manual="1" editable="1"> <parameter name="some_float" type="float">30.5</parameter> <parameter name="some_string" type="string">Hello from my_property!</parameter> <parameter name="some_node" type="node">0</parameter> <parameter name="some_material" type="material"></parameter> <parameter name="some_mesh" type="file"></parameter> <parameter name="some_file" type="file"></parameter> </property> ```
2. Then open the UnigineEditor, find the created property in the *Properties* window, right-click on it and select *Create Child*. The property named `my_property_0` shall be created (you can rename it if you want). ![](inherit_property.png) *Create a child property*
3. Level designers make adjustments by dragging all necessary assets and nodes to the corresponding fields of the child property `my_property_0`, as well as by setting other parameters (if any). ![](assign_gprop_params.gif) *Linking nodes and assets to the property*
4. Programmers can **access any of these assets via this global property from any world**. As we don't use components, we'll have to find the property with links to assets by its name (*my_property_0*). So, in the *[init()](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic_init)* method of the *WorldLogic* class we do the following: ```cpp int AppWorldLogic::init() { /* ... */ PropertyPtr property = Properties::findManualProperty("my_property_0"); /* ... */ return 1; } ```
5. Now we can use the property to get access to nodes and files:

  - **to get a material** we can simply use the corresponding node parameter: ```cpp property->getParameterPtr("node_param_name")->getValueMaterial(); ```
  - **to get a path to file**, we can simply use: ```cpp const char *path = property->getParameterPtr("file_param_name")->getValueFile(); ``` As we have a path to our file, we can use it, for example: ```cpp // to create a node reference NodeReferencePtr node_ref = NodeReference::create(path_to_node_file); // to load a sound source SoundSourcePtr sound = SoundSource::create(path_to_sound_file); ```


### C++ Implementation


So, C++ implementation of the example ([described above](#example)) for a global property will be rewritten as shown below. You can copy and paste the code to the `AppWorldLogic.cpp` file of your project.


<details>
<summary>AppWorldLogic.cpp | Close</summary>

**AppWorldLogic.cpp**


```cpp
#include "AppWorldLogic.h"
#include <UnigineMaterials.h>
#include <UnigineSounds.h>
#include <UnigineGame.h>
#include <UnigineWorld.h>
#include <UnigineFileSystem.h>

using namespace Unigine;
using namespace Math;
PropertyPtr property;              // property with all necessary links
MaterialPtr material;              // linked material
NodePtr param_node;                // linked node
SoundSourcePtr sound;	      	   // sound source to be played
ObjectMeshStaticPtr generated_obj; // object to be generated using the mesh

AppWorldLogic::AppWorldLogic() {

}

AppWorldLogic::~AppWorldLogic() {

}

int AppWorldLogic::init() {
	// getting the property that will be used to access all necessary files using its name
	property = Properties::findManualProperty("my_property_0");
	// using access to property parameters to perform desired actions
	if (property) {
		// getting a material from the corresponding property parameter
		material = property->getParameterPtr("some_material")->getValueMaterial();

		// getting the path to the mesh file from the corresponding property parameter
		const char *mesh_file_name = property->getParameterPtr("some_mesh")->getValueFile();

		// creating the object by using the mesh
		generated_obj = ObjectMeshStatic::create(mesh_file_name);

		// setting the object position relative to another node position
		generated_obj->setWorldPosition(my_node->getWorldPosition());
		generated_obj->translate(vec3(-1.0f, 0.0f, 0.0f));

		// getting the path to the sound file from the corresponding property parameter
		const char *sound_file_name = property->getParameterPtr("some_file")->getValueFile();

		// getting a node from the corresponding property parameter
		param_node = property->getParameterPtr("some_node")->getValueNode();

		// creating and playing a sound from the file
		sound = SoundSource::create(sound_file_name);
		sound->setMaxDistance(100.0f);
		sound->setLoop(1);
		sound->play();

		// reporting results to the console
		Log::message("Path to mesh file: %s\nPath to sound file: %s\nNode ID: %d\n", mesh_file_name, sound_file_name, param_node->getID());
	}
	return 1;
}

// start of the main loop
int AppWorldLogic::update() {
	// Write here code to be called before updating each render frame: specify all graphics-related functions you want to be called every frame while your application executes.

	float ifps = Game::getIFps();

	// changing the material
	material->setParameterFloat4("albedo_color", vec4(Game::getRandomFloat(0.0f, 1.0f), Game::getRandomFloat(0.0f, 1.0f), Game::getRandomFloat(0.0f, 1.0f), 1.0f));

	// rotate linked node
	param_node->setRotation(param_node->getRotation() * quat(0, 0, 30.0f * ifps));

	return 1;
}

int AppWorldLogic::postUpdate() {
	// The engine calls this function before rendering each render frame: correct behavior after the state of the node has been updated.

	return 1;
}

int AppWorldLogic::updatePhysics() {
	// Write here code to be called before updating each physics frame: control physics in your application and put non-rendering calculations.
	// The engine calls updatePhysics() with the fixed rate (60 times per second by default) regardless of the FPS value.
	// WARNING: do not create, delete or change transformations of nodes here, because rendering is already in progress.

	return 1;
}
// end of the main loop

int AppWorldLogic::shutdown() {
	// Write here code to be called on world shutdown: delete resources that were created during world script execution to avoid memory leaks.
	// saving current material color (check it in the UnigineEditor to see that it was modified)
	material->save();
	return 1;
}

int AppWorldLogic::save(const Unigine::StreamPtr &stream) {
	// Write here code to be called when the world is saving its state: save custom user data to a file.

	UNIGINE_UNUSED(stream);
	return 1;
}

int AppWorldLogic::restore(const Unigine::StreamPtr &stream) {
	// Write here code to be called when the world is restoring its state: restore custom user data to a file here.

	UNIGINE_UNUSED(stream);
	return 1;
}

```

</details>


### C# Implementation


The C# implementation of the example ([described above](#example)) for a global property will be rewritten as shown below. You can copy and paste the code to the `AppWorldLogic.cs` file of your project.


<details>
<summary>AppWorldLogic.cs | Close</summary>

**AppWorldLogic.cs**


```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Unigine;

namespace UnigineApp
{
	class AppWorldLogic : WorldLogic
	{
		// World logic, it takes effect only when the world is loaded.
		// These methods are called right after corresponding world script's (UnigineScript) methods.
		Property property;					// property with all necessary links
		Material material;					// linked material
		Node param_node;					// linked node
		SoundSource sound;					// sound source to be played
		ObjectMeshStatic generated_obj;		// object to be generated using the mesh

		public AppWorldLogic()
		{
		}

		public override bool Init()
		{
			// getting the property that will be used to access all necessary files using its name
			property = Properties.FindManualProperty("my_property_0");
			// using access to property parameters to perform desired actions
			if (property) {
				// getting a material from the corresponding property parameter
				material = property.GetParameterPtr("some_material").ValueMaterial;

				// getting the path to the mesh file from the corresponding property parameter
				String mesh_file_name = property.GetParameterPtr("some_mesh").ValueFile;

				// creating the object by using the mesh
				generated_obj = new ObjectMeshStatic(mesh_file_name);

				// setting the object position relative to another node position
				generated_obj.WorldPosition = my_node.WorldPosition;
				generated_obj.Translate(-1.0f, 0.0f, 0.0f);

				// getting the path to the sound file from the corresponding property parameter
				String sound_file_name = property.GetParameterPtr("some_file").ValueFile;

				// getting a node from the corresponding property parameter
				param_node = property.GetParameterPtr("some_node").ValueNode;

				// creating and playing a sound from the file
				sound = new SoundSource(sound_file_name);
				sound.MaxDistance = 100.0f;
				sound.Loop = 1;
				sound.Play();

				// reporting results to the console
				Log.Message("Path to mesh file: {0}\nPath to sound file: {1}\nNode ID: {2}\n", mesh_file_name, sound_file_name, param_node.ID);
			}
			return true;
		}

		// start of the main loop
		public override bool Update()
		{
			// Write here code to be called before updating each render frame: specify all graphics-related functions you want to be called every frame while your application executes.
			float ifps = Game.IFps;

			// changing the material
			 material.SetParameterFloat4("albedo_color", new vec4(Game.GetRandomFloat(0.0f, 1.0f), Game.GetRandomFloat(0.0f, 1.0f), Game.GetRandomFloat(0.0f, 1.0f), 1.0f));

			// rotate linked node
			param_node.SetRotation(param_node.GetRotation() * new quat(0, 0, 30.0f * ifps));

			return true;
		}

		public override bool PostUpdate()
		{
			// The engine calls this function before rendering each render frame: correct behavior after the state of the node has been updated.
			return true;
		}

		// end of the main loop

		public override bool Shutdown()
		{
			// Write here code to be called on world shutdown: delete resources that were created during world script execution to avoid memory leaks.
			// saving current material color (check it in the UnigineEditor to see that it was modified)
			material.Save();

			return true;
		}

		public override bool Save(Stream stream)
		{
			// Write here code to be called when the world is saving its state: save custom user data to a file.
			return true;
		}

		public override bool Restore(Stream stream)
		{
			// Write here code to be called when the world is restoring its state: restore custom user data to a file here.
			return true;
		}
	}
}

```

</details>
