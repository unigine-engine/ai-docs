# Adding Morph Targets (CPP)


This article describes how to work with the *morph target* animation also known as *blend shapes* in UNIGINE. Usually, morph targets are used to change facial expressions of characters.


The article shows how to export the mesh with morph targets from *Autodesk Maya* and then add it to UNIGINE.


The model used in this tutorial is *Spot* by [Keenan Crane](https://www.cs.cmu.edu/~kmcrane/Projects/ModelRepository/) distributed under [CC0 1.0 Universal](https://creativecommons.org/publicdomain/zero/1.0/).


### Requirements


- It is supposed that you already have a 3D model with blend shapes ready to be exported, and this model is within the [limitations](../../../objects/objects/mesh_skinned/index.md#mesh_limitations) set in UNIGINE.
- It is supposed that you already have a world created.


### See Also


- Description of the *[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cpp.md)* class functions


## Step 1. Export a Mesh with Blend Shapes from Maya


This section shows the way of exporting meshes with blend shapes in the `FBX` format from *Autodesk Maya*. It contains an example mesh of a calf, which has 2 blend shapes (morph targets).


To export the mesh with blend shapes, do the following:


1. In *Autodesk Maya*, select the mesh with blend shapes to be exported. ![](1_select.png)
2. In the main menu, click *File -> Export Selection...* ![](1_export_selection.png)
3. In the *Export Selection* window, choose a folder to save the mesh and specify a name for the FBX file. In the *Files of type* drop-down list, choose FBX export.
4. In the *File Type Specific Options* tab with export options, specify parameters to export the mesh.
5. In the *Deformed Models* tab, check the *Blend Shapes* checkbox to export blend shapes.
6. Click *Export Selection*.


Now you have the mesh in the `FBX` format that can be easily added to your project.


## Step 2. Add a Mesh into the World


This section shows how to add the exported mesh to the world and set up morph target animation.


To add the exported mesh to the world:


1. [Import the `*.fbx`](../../../editor2/fbx/index.md#import_fbx) file with the **[Import Morph Targets](../../../editor2/fbx/index.md#animation)** option enabled. ![](import_options.png)
2. [Add](../../../editor2/fbx/index.md#add_fbx) the imported file to the scene.
3. [Save](../../../editor2/worlds/index.md#save_world) the world.


Each blend shape of the mesh is a target. You need to enable morph targets for the mesh surface and set parameters to these targets to control the morph target animation. The following example shows how to create morph targets and set parameters via code:


> **Notice:** The code is implemented as a component that should be assigned to the node via UnigineEditor. Check the article on [Component System](../../../principles/component_system/index.md) for more detail.


```cpp
#pragma once
#include <UnigineComponentSystem.h>
#include <UnigineWorld.h>
#include <UnigineGame.h>

class Morph :
	public Unigine::ComponentBase
{
public:
	// declare constructor and destructor for the Morph class
	COMPONENT_DEFINE(Morph, Unigine::ComponentBase);

	// declare methods to be called at the corresponding stages of the execution sequence
	COMPONENT_INIT(init);
	COMPONENT_UPDATE(update);

private:
	Unigine::ObjectMeshSkinnedPtr mesh;

protected:
	// world main loop
	void init();
	void update();
};

```


```cpp
#include "Morph.h"

REGISTER_COMPONENT(Morph);		// macro for component registration by the Component System
using namespace Unigine;
using namespace Math;

void Morph::init()
{
	// get the node and cast it to a skinned mesh
	mesh = static_ptr_cast<ObjectMeshSkinned>(node);

	// enable targets of the surface
	mesh->setSurfaceTargetEnabled(0, 1, true);
	mesh->setSurfaceTargetEnabled(0, 2, true);
}

void Morph::update()
{
	float time = Game::getTime() * 2.0f;
	// calculate weights of targets
	float k0 = Unigine::Math::sin(time * 3.0f) + 0.75f;
	float k1 = Unigine::Math::cos(time * 3.0f) + 0.75f;

	// set targets with parameters
	mesh->setSurfaceTargetWeight(0, 0, 1.0f - k0 - k1);
	mesh->setSurfaceTargetWeight(0, 1, k0);
	mesh->setSurfaceTargetWeight(0, 2, k1);
}

```


The code given above gets the node that refers to the FBX file and sets parameters to morph targets. Let's clarify the essential things:


- The mesh was obtained by casting the node that refers to the FBX asset to *[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cpp.md)*. The node to be cast is the one to which the component is assigned. Prior to casting this node, you may also want to add a check if it is *ObjectMeshSkinned*: ```cpp //check if the node to which the component is assigned is MeshSkinned if (node->getType() != Node::OBJECT_MESH_SKINNED) return; // get the node and cast it to a skinned mesh mesh = static_ptr_cast<ObjectMeshSkinned>(node); ```
- The *[setSurfaceTargetEnabled()](../../../api/library/objects/class.objectmeshskinned_cpp.md#setSurfaceTargetEnabled_int_int_int_void)* function sets the target for the specified mesh surface.
- By using *[setSurfaceTargetWeight()](../../../api/library/objects/class.objectmeshskinned_cpp.md#setSurfaceTargetWeight_int_int_float_void)*, weights for morph targets are set. Each target has its target weight. Weights affect coordinates of the mesh: coordinates are multiplied by their weights. Thus, all enabled targets are multiplied by their weights and the new mesh is created: final_xyz = target_0_xyz * weight_0 + target_1_xyz * weight_1 + ...
- Three targets are enabled for the object and *sin()* and *cos()* functions are used for animation blending of these targets in the following way:

  - Subtract the impact of the other two morph targets from the *bind pose* to receive a normalized weight for blending. ```cpp mesh->setSurfaceTargetWeight(0, 0, 1.0f - k0 - k1); ```
  - The first target weight is modified using the *sin()* function. ```cpp mesh->setSurfaceTargetWeight(0, 1, k0); ```
  - The second target weight is modified using the *cos()* function. ```cpp mesh->setSurfaceTargetWeight(0, 2, k1); ```


After assigning the component to the mesh, the result looks as follows:


![](calf_5.gif)
