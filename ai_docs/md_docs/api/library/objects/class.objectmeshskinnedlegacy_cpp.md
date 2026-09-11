# ObjectMeshSkinnedLegacy Class (CPP)

**Header:** #include <UnigineObjects.h>

**Inherits from:** Object


This class is used to create and modify [skinned meshes](../../../objects/objects/mesh_skinned_legacy/index.md). Skinned Meshes are used to render characters with animation.


#### Applying Animation


Animation is applied to *ObjectMeshSkinnedLegacy* via its layers. Layers store skeletal poses, the pose is taken from the animation.


By default, when created, *ObjectMeshSkinnedLegacy* has only one active base layer, the pose of which is used for animation. More layers can be added to store various poses that may be blended or processed otherwise (through such functions as *[*lerpLayer*](#lerpLayer_int_int_int_float_void)*, *[*copyLayer*](#copyLayer_int_int_void)*, *[*importLayer*](#importLayer_int_void)*, *[*inverseLayer*](#inverseLayer_int_int_void)* and *[*mulLayer*](#mulLayer_int_int_int_float_void)*), with the resulting pose saved in the base layer for final render output.


**Automatic blending** of animations suitable for simple use cases is implemented internally in ObjectMeshSkinnedLegacy. For a layer to be included in the final blend, it must be enabled and have a non-zero weight. These values can be changed using **[setLayer()](../../...md#setLayer_int_int_float_void)**, **[setLayerEnabled()](../../...md#setLayerEnabled_int_int_void)** and **[setLayerWeight()](../../...md#setLayerWeight_int_float_void)**. When blending, an arithmetic weighted average is applied: all layer weights are first normalized, after which each component is multiplied by its corresponding weight and summed.


A similar approach is used for scaling and a slightly different one for rotations, but for working at the layer level this is not critical.


**Customized blending** of animations including partial bone blending, additive animation, and so on, is implemented via custom logic. You can control individual bones on layers using **[setLayerBoneTransform()](../../...md#setLayerBoneTransform_int_int_mat4_void)** / **[getLayerBoneTransform()](../../...md#getLayerBoneTransform_int_int_mat4)**, as well as their counterparts for individual components: position, rotation and scale. These functions allow you to create masks for bones and then work exclusively with those bones in a loop.


##### Creating and Playing Animation


To add the animation to the ObjectMeshSkinnedLegacy and play it, do the following:


1. Set the number of animation layers with **[setNumLayers()](../../...md#setNumLayers_int_void)**. There is only one layer by default, the pose of which is used for animation.
2. Enable each layer and set the animation weight for blending by calling the **[setLayer()](../../...md#setLayer_int_int_float_void)** function.
3. Add the animation `*.anim` file by using the **[setLayerAnimationFilePath()](../../...md#setLayerAnimationFilePath_int_cstr_void)** function.
4. Play the added animation by calling the **[setLayerFrame()](../../...md#setLayerFrame_int_float_int_int_float)** function for each animation layer.


Blending is performed between all layers. The contribution of each layer depends on its weight. Also, you can optionally define single bone transformations by hand, if needed, using either **[setBoneTransform()](../../...md#setBoneTransform_int_mat4_void)** or **[setBoneTransformWithChildren()](../../...md#setBoneTransformWithChildren_int_mat4_void)**.


###### Usage Example


The following example shows how to blend two different animations assigned to a mesh. You can use the mesh and animations from UNIGINE samples located in the following sample set folders:


- `<cpp_samples>/data/showcase_content/person`
- `<csharp_component_samples>/data/showcase_content/agent`


Animations are added by using the **[setLayerAnimationFilePath()](../../...md#setLayerAnimationFilePath_int_cstr_void)** function.


In this example, animation assets are accessed through the [Component System](../../../principles/component_system/index.md).


1. [Create a component](../../../code/usage/using_component_system/index.md) to control the animation loading, and generate a property for it.
2. Assign the property to the target controller node.
3. Assign the desired animation assets to the parameters of the property in UnigineEditor. ![](property_assets.png) *Assigning animation assets to property parameters via the Editor*
4. Implement logic of creating a skinned mesh with the specified animations. The complete source code: ```cpp #pragma once #include <UnigineComponentSystem.h> #include <UnigineObjects.h> class SkinnedMeshController: public Unigine::ComponentBase { public: COMPONENT(SkinnedMeshController, ComponentBase); COMPONENT_INIT(init); COMPONENT_UPDATE(update); COMPONENT_SHUTDOWN(shutdown); PROP_NAME("skinned_controller_property"); // property parameters for mesh and animation assets PROP_PARAM(File, mesh_asset); PROP_PARAM(File, anim_asset_1); PROP_PARAM(File, anim_asset_2); protected: void init(); void update(); void shutdown(); private: // the pointer to the skinned mesh object Unigine::ObjectMeshSkinnedLegacyPtr skinned_mesh; }; ``` ```cpp #include "SkinnedMeshController.h" #include <UnigineGame.h> // register the component REGISTER_COMPONENT(SkinnedMeshController); using namespace Unigine; void SkinnedMeshController::init() { // create the new ObjectMeshSkinnedLegacy mesh based on an existing mesh skinned_mesh = ObjectMeshSkinnedLegacy::create(mesh_asset); // we need two layers to get poses from two animations skinned_mesh->setNumLayers(2); // load animations from the files on separate layers skinned_mesh->setLayerAnimationFilePath(0, anim_asset_1); skinned_mesh->setLayerAnimationFilePath(1, anim_asset_2); // enable each layer and set an animation weight skinned_mesh->setLayer(0, true, 0.7f); skinned_mesh->setLayer(1, true, 0.3f); } void SkinnedMeshController::update() { // play each animation, getting new poses with each frame update skinned_mesh->setLayerFrame(0, Game::getTime() * 25.0f); skinned_mesh->setLayerFrame(1, Game::getTime() * 25.0f); } void SkinnedMeshController::shutdown() { } ```


#### Updating Bone Transformations


Some methods require to update the animation data before the renderer makes its update and actually draws the skinned mesh. Such update allows obtaining the correct result of blending between the frames and layers. This update is executed based on the state of the internal update flags that indicate if there have been any bone transformations.


The execution sequence of updating bone transformations is the following:


1. Call the method that sets the update flag. This flag shows that the instance should be updated.
2. Update the bone transformations by calling corresponding functions. These functions check the flag and if the flag is set, they calculate the transformations and set the flag to the default value.
3. During rendering, the engine performs animations and transformations which were calculated on the previous step or recalculates them, if the update flag has been set. If calculations have been performed, the flag is set to the default value.


If you try to update bone transformations before the flag is set to update, functions will not calculate new transformations and the engine won't perform them.


When you change the transformation of the bone, you should notify all skinned meshes that use this bone about these transformations to update the mesh. When you change transformations of a bone, skinned mesh instances get the flag to update. When you use the *[setLayerFrame()](#setLayerFrame_int_float_int_int_float)* function, you set necessary transformations for the specified skinned mesh.


#### Instancing


Surfaces of identical skinned meshes that have the same materials assigned to them and the same number of bones attached to their vertices are automatically instanced and drawn in one draw call.


The data buffers for instanced objects that store bone transformations are limited in size; therefore, if skinned meshes have many bones, only a few meshes can populate the instance data buffer to be drawn in one draw call.


> **Notice:** The higher the number of bones and the more bones are attached to one surface, the less robust instancing will be.


#### Procedural Mesh Modifications


Procedural mode for skinned meshes allows runtime modification of the object's geometry. This can be useful, for example, when generating character variations, dynamically adjusting armor or clothing to fit, or deforming a model in response to gameplay events.


In contrast to [procedural modes](../../../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE) available for static meshes, skinned meshes have **only one mode** - equivalent to *[PROCEDURAL_MODE_DYNAMIC](../../../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE_DYNAMIC)* (the procedural mesh remains in VRAM and will not be unloaded).


Procedural updates for skinned meshes are performed exclusively in the Engine's main thread using *[applyMeshProcedural()](../../...md#applyMeshProcedural_ConstMeshSkinned_int)*. If the source mesh contains compatible elements (e.g., bones, surfaces, skinning data) matching the original, then animations, morph targets, and other behaviors will continue to function without interruption. Otherwise, the mesh will remain static, with no animation or morphing applied.


#### Reusing Animations


Animations from one character can be used for another.


##### Animation Frame Masks


Masks are the simplest way of reusing animations, a couple of words about how they work. To each layer of an *ObjectMeshSkinnedLegacy* you can assign some animation and based on its frames it will change bone transformations on this layer. You can use **[masks](#ANIM_FRAME_USES_NONE)** to choose which components of the animation frame (position, rotation, scale, their combinations, or all of them) are to be used for each particular layer. In case any component is missing in the mask, the corresponding value will be taken from the T-pose.


As an example let's take eyes animation for these two skeletons:


![](anim_mask_1.jpg)


They have absolutely the same bone hierarchy as well as bone names, only the proportions differ. If we use animation for eyes from the left skeleton for the right one, we'll get the following result:


![](anim_mask_2.jpg)


The initial animation has completely changed the proportions of the second skeleton. We can fix it by setting **[ANIM_FRAME_USES_ROTATION](#ANIM_FRAME_USES_ROTATION)** mask to eye bones, and **[ANIM_FRAME_USES_NONE](#ANIM_FRAME_USES_NONE)** for the rest of the bones via the **[setLayerBoneFrameUses()](../../...md#setLayerBoneFrameUses_int_int_int_void)* / *[getLayerBoneFrameUses()](../../...md#getLayerBoneFrameUses_int_int_int)** methods. Thus, all values except for eyes rotation will be taken from the T-pose :


![](eyes_anim.gif)


If the skeletons have different bone names you should first apply retargeting and then use masks. In this case it is not that important to have similar skeletons.


##### Retargeting


To reuse animation entirely, both source and target skeletons must have similar bone hierarchy and their T-poses must not significantly differ.


This is acceptable and will work fine:


![](skeletons_good.jpg)


as we have similar bone hierarchies and all bones have similar bases in T-poses, only the proportions differ, but this proportion is almost uniform for all bones.


But we cannot use the following:


![](skeletons_bad.jpg)


Although the hierarchy looks similar, the T-poses differ and bones have different bases.


These limitations can be ignored if you need to retarget only some subset of the bones (e.g.: retarget bones having different names and then use only masks).


#### Inverse Kinematics (IK)


*ObjectMeshSkinnedLegacy* supports inverse kinematics (IK) for bone chains (**IK chains**). Inverse kinematics provide a way to handle joint rotation from the location of an **end-effector** rather than via direct joint rotation. You provide a location of the effector and the IK Solver attempts to find a rotation so that the final joint coincides with that location as best it can. This can be used to position a character's feet properly on uneven ground, and ensure believable interactions with the world. The **tolerance** value sets a threshold where the target is considered to have reached its destination position, and when the IK Solver stops iterating.


An IK chain can have an arbitrary length (contain an arbitrary number of bones), it has an auxiliary vector enabling you to control bending direction. You can also set rotation for the last joint of the chain.


Each IK chain has a **weight** value that can be used to control the impact of the target on the last joint of the chain. This enables you to make smooth transitions from the source animation to required target position of the limb.


To visualize IK chains you can use the following methods: **[addVisualizeIKChain()](../../...md#addVisualizeIKChain_int_void)*, *[removeVisualizeIKChain()](../../...md#removeVisualizeIKChain_int_void)**, and **[clearVisualizeIKChain()](../../...md#clearVisualizeIKChain_void)**.


![](ik_visualizer.gif)


### See Also


- *[Mesh](../../../api/library/rendering/class.mesh_cpp.md)* class
- Article on [Mesh File Formats](../../../code/formats/file_formats.md#mesh)
- Animation samples in *[C++](../../../sdk/api_samples/cpp/animation.md)* and *[C# Component Samples](../../../sdk/api_samples/cs/animation.md)* suites


## ObjectMeshSkinnedLegacy Class

### Enums

## BONE_SPACE

Defines which transformation of the bone is to be overridden by the bind node's transformation.
| Name | Description |
|---|---|
| **BONE_SPACE_WORLD** = 0 | World coordinates. |
| **BONE_SPACE_OBJECT** = 1 | Coordinates relative to the skinned mesh object. |
| **BONE_SPACE_LOCAL** = 2 | Coordinates relative to the parent bone. |

## NODE_SPACE

Defines the type of transformation of the bind node to be used to override the transformation of the specified bone.
| Name | Description |
|---|---|
| **NODE_SPACE_WORLD** = 0 | World transformation of the node. |
| **NODE_SPACE_LOCAL** = 1 | Local transformation of the node. |

## BIND_MODE

Type of blending of bind node's and bone's transformations.
| Name | Description |
|---|---|
| **BIND_MODE_OVERRIDE** = 0 | Replace bone's transformation with the transformation of the bind node. |
| **BIND_MODE_ADDITIVE** = 1 | Bind node's transformation is added to the current transformation of the bone. |

## ANIM_FRAME_USES

Frame components to be used for animation.
| Name | Description |
|---|---|
| **ANIM_FRAME_USES_NONE** = 0 | No frame components are to be used. |
| **ANIM_FRAME_USES_POSITION** = 1 << 0 | Only position is to be used. |
| **ANIM_FRAME_USES_ROTATION** = 1 << 1 | Only rotation is to be used. |
| **ANIM_FRAME_USES_SCALE** = 1 << 2 | Only scale is to be used. |
| **ANIM_FRAME_USES_ALL** = POSITION \| ROTATION \| SCALE | All frame components are to be used. |
| **ANIM_FRAME_USES_POSITION_AND_ROTATION** = POSITION \| ROTATION | Only position and rotation are to be used. |
| **ANIM_FRAME_USES_POSITION_AND_SCALE** = POSITION \| SCALE | Only position and scale are to be used. |
| **ANIM_FRAME_USES_ROTATION_AND_SCALE** = ROTATION \| SCALE | Only rotation and scale are to be used. |

## CHAIN_CONSTRAINT

| Name | Description |
|---|---|
| **CHAIN_CONSTRAINT_NONE** = 0 | No constraints applied to the IK/LookAt chain. The chain transforms are kept as is after applying the solver. |
| **CHAIN_CONSTRAINT_POLE_VECTOR** = 1 | The specified pole vector is applied for the IK/LookAt chain. For the IK chain, the pole vector defines the bend plane. For the LookAt chain, the pole vector defines the plane of the UP axis. This constraint is applied after applying the solver. |
| **CHAIN_CONSTRAINT_BONE_ROTATIONS** = 2 | At every solver application step, bone rotation constraints are applied to the chain if they have been previously configured. |

## INTERPOLATION_ACCURACY

| Name | Description |
|---|---|
| **INTERPOLATION_ACCURACY_LOW** = 0 | Linear interpolation with quaternion normalization (nlerp) is applied. |
| **INTERPOLATION_ACCURACY_MEDIUM** = 1 | Linear interpolation with quaternion normalization (nlerp) is applied to rotation, but the interpolation coefficient is adjusted to be approximated to the uniform angular rotation rate. |
| **INTERPOLATION_ACCURACY_HIGH** = 2 | The slerp function is used for rotations. |

### Members

## int getNumBones () const

Returns the current number of all bones taking part in animation.
### Return value

Current Number of bones of the skinned mesh.
## void setNumLayers ( int layers )

Sets a new number of animation layers for blending. For example, when two layers are blended, bone transformations in between the layers are interpolated, and vertex positions can be calculated using the interpolated results. For more details, see the article on [Skinned Mesh](../../../objects/objects/mesh_skinned_legacy/index.md).
### Arguments

- *int* **layers** - The number of animation layers (must be greater than 0).

## int getNumLayers () const

Returns the current number of animation layers for blending. For example, when two layers are blended, bone transformations in between the layers are interpolated, and vertex positions can be calculated using the interpolated results. For more details, see the article on [Skinned Mesh](../../../objects/objects/mesh_skinned_legacy/index.md).
### Return value

Current number of animation layers (must be greater than 0).
## bool isStopped () const

Returns the current stop status.
### Return value

**true** if animation is stopped; otherwise **false**.
## bool isPlaying () const

Returns the current playback status.
### Return value

**true** if animation is playing; otherwise **false**.
## void setSpeed ( float speed )

Sets a new multiplier value for the animation playback [time](#setTime_float_void).
### Arguments

- *float* **speed** - The playback speed multiplier value.

## float getSpeed () const

Returns the current multiplier value for the animation playback [time](#setTime_float_void).
### Return value

Current playback speed multiplier value.
## void setTime ( float time )

Sets a new animation time, in animation frames. The time count starts from the zero frame. If the time is set to be between frames, animation is blended. If the time is set outside the animation frame range, the animation is looped.
> **Notice:** *[setTime()](../../...md#setTime_float_void)* function corresponds to the [Play](../../../objects/objects/mesh_skinned_legacy/index.md#play) and [Stop](../../../objects/objects/mesh_skinned_legacy/index.md#stop) options in the editor. In all other cases use *[setLayerFrame()](../../...md#setLayerFrame_int_float_int_int_float)* to set the animation.


### Arguments

- *float* **time** - The animation time, in animation frames

## float getTime () const

Returns the current animation time, in animation frames. The time count starts from the zero frame. If the time is set to be between frames, animation is blended. If the time is set outside the animation frame range, the animation is looped.
> **Notice:** *[setTime()](../../...md#setTime_float_void)* function corresponds to the [Play](../../../objects/objects/mesh_skinned_legacy/index.md#play) and [Stop](../../../objects/objects/mesh_skinned_legacy/index.md#stop) options in the editor. In all other cases use *[setLayerFrame()](../../...md#setLayerFrame_int_float_int_int_float)* to set the animation.


### Return value

Current animation time, in animation frames
## void setLoop ( bool loop )

Sets a new value indicating if the animation is looped or played only once.
### Arguments

- *bool* **loop** - Set **true** to enable playing of the animation in a loop; **false** - to disable it.

## bool isLoop () const

Returns the current value indicating if the animation is looped or played only once.
### Return value

**true** if playing of the animation in a loop is enabled ; otherwise **false**.
## void setControlled ( bool controlled )

Sets a new value indicating if the animation is controlled by a parent ObjectMeshSkinnedLegacy.
### Arguments

- *bool* **controlled** - Set **true** to enable animation is controlled by a parent ObjectMeshSkinnedLegacy; **false** - to disable it.

## bool isControlled () const

Returns the current value indicating if the animation is controlled by a parent ObjectMeshSkinnedLegacy.
### Return value

**true** if animation is controlled by a parent ObjectMeshSkinnedLegacy; otherwise **false**.
## void setQuaternion ( bool quaternion )

Sets a new value indicating if the dual-quaternion skinning mode is used. The dual-quaternion model is an accurate, computationally efficient, robust, and flexible method of representing rigid transforms and it is used in skeletal animation. See [a Wikipedia article on dual quaternions](https://en.wikipedia.org/wiki/Dual_quaternion) and [a beginners guide to dual-quaternions](http://cs.gmu.edu/~jmlien/teaching/cs451/uploads/Main/dual-quaternion.pdf) for more information.
### Arguments

- *bool* **quaternion** - Set **true** to enable dual-quaternion skinning mode; **false** - to disable it.

## bool isQuaternion () const

Returns the current value indicating if the dual-quaternion skinning mode is used. The dual-quaternion model is an accurate, computationally efficient, robust, and flexible method of representing rigid transforms and it is used in skeletal animation. See [a Wikipedia article on dual quaternions](https://en.wikipedia.org/wiki/Dual_quaternion) and [a beginners guide to dual-quaternions](http://cs.gmu.edu/~jmlien/teaching/cs451/uploads/Main/dual-quaternion.pdf) for more information.
### Return value

**true** if dual-quaternion skinning mode is enabled ; otherwise **false**.
## void setUpdateDistanceLimit ( float limit = 200 )

Sets a new distance from the camera within which the object should be updated.
### Arguments

- *float* **limit** - The distance from the camera within which the object should be updated, in units.

## float getUpdateDistanceLimit () const

Returns the current distance from the camera within which the object should be updated.
### Return value

Current distance from the camera within which the object should be updated, in units.
## void setFPSInvisible ( int fpsinvisible = 0 )

Sets a new update rate value when the object is not rendered at all.
### Arguments

- *int* **fpsinvisible** - The update rate value when the object is not rendered at all.

## int getFPSInvisible () const

Returns the current update rate value when the object is not rendered at all.
### Return value

Current update rate value when the object is not rendered at all.
## void setFPSVisibleShadow ( int shadow = 30 )

Sets a new update rate value when only object shadows are rendered.
### Arguments

- *int* **shadow** - The update rate value when only object shadows are rendered.

## int getFPSVisibleShadow () const

Returns the current update rate value when only object shadows are rendered.
### Return value

Current update rate value when only object shadows are rendered.
## void setFPSVisibleCamera ( int camera = -1 )

Sets a new update rate value when the object is rendered to the viewport.
### Arguments

- *int* **camera** - The update rate value when the object is rendered to the viewport.

## int getFPSVisibleCamera () const

Returns the current update rate value when the object is rendered to the viewport.
### Return value

Current update rate value when the object is rendered to the viewport.
## void setVisualizeAllBones ( bool bones )

Sets a new value indicating if visualization for bones and their basis vectors is enabled. The visualizer can be used for debugging purposes showing positions of bones and their basis vectors for multiple meshes simultaneously.
### Arguments

- *bool* **bones** - Set **true** to enable visualization of bones and their basis vectors; **false** - to disable it.

## bool isVisualizeAllBones () const

Returns the current value indicating if visualization for bones and their basis vectors is enabled. The visualizer can be used for debugging purposes showing positions of bones and their basis vectors for multiple meshes simultaneously.
### Return value

**true** if visualization of bones and their basis vectors is enabled ; otherwise **false**.
## int getNumIKChains () const

Returns the current number of [IK chains](#ik_chains) of the skinned mesh.
### Return value

Current number of IK chains.
## Event<const Ptr < ObjectMeshSkinnedLegacy > &> getEventEndBoneConstraints () const

Event triggered after the bone rotation constraints are applied. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

<details>
<summary>See Example | Close</summary>

**Usage Example**


```cpp
// implement the EndBoneConstraints event handler
void endboneconstraints_event_handler(const Ptr<ObjectMeshSkinnedLegacy> & skinned)
{
	Log::message("\Handling EndBoneConstraints event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endboneconstraints_event_connections;

// link to this instance when subscribing for an event (subscription for various events can be linked)
objectmeshskinnedlegacy->getEventEndBoneConstraints().connect(endboneconstraints_event_connections, endboneconstraints_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
objectmeshskinnedlegacy->getEventEndBoneConstraints().connect(endboneconstraints_event_connections, [](const Ptr<ObjectMeshSkinnedLegacy> & skinned) {
		Log::message("\Handling EndBoneConstraints event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endboneconstraints_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endboneconstraints_event_connection;

// subscribe for the EndBoneConstraints event with a handler function keeping the connection
objectmeshskinnedlegacy->getEventEndBoneConstraints().connect(endboneconstraints_event_connection, endboneconstraints_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endboneconstraints_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endboneconstraints_event_connection.setEnabled(true);

// ...

// remove subscription for the EndBoneConstraints event via the connection
endboneconstraints_event_connection.disconnect();

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

	// A EndBoneConstraints event handler implemented as a class member
	void event_handler(const Ptr<ObjectMeshSkinnedLegacy> & skinned)
	{
		Log::message("\Handling EndBoneConstraints event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
objectmeshskinnedlegacy->getEventEndBoneConstraints().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//  4. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe for the EndBoneConstraints event with a handler function
objectmeshskinnedlegacy->getEventEndBoneConstraints().connect(endboneconstraints_event_handler);

// remove subscription for the EndBoneConstraints event later by the handler function
objectmeshskinnedlegacy->getEventEndBoneConstraints().disconnect(endboneconstraints_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   5. Subscribe to an event saving an ID and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////

// define a connection ID to be used to unsubscribe later
EventConnectionId endboneconstraints_handler_id;

// subscribe for the EndBoneConstraints event with a lambda handler function and keeping connection ID
endboneconstraints_handler_id = objectmeshskinnedlegacy->getEventEndBoneConstraints().connect([](const Ptr<ObjectMeshSkinnedLegacy> & skinned) {
		Log::message("\Handling EndBoneConstraints event (lambda).\n");
	}
);

// remove the subscription later using the ID
objectmeshskinnedlegacy->getEventEndBoneConstraints().disconnect(endboneconstraints_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   6. Ignoring all EndBoneConstraints events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
objectmeshskinnedlegacy->getEventEndBoneConstraints().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
objectmeshskinnedlegacy->getEventEndBoneConstraints().setEnabled(true);
```

</details>


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<ObjectMeshSkinnedLegacy> & **skinned**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndBoneConstraints event handler
void endboneconstraints_event_handler(const Ptr<ObjectMeshSkinnedLegacy> & skinned)
{
	Log::message("\Handling EndBoneConstraints event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endboneconstraints_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndBoneConstraints().connect(endboneconstraints_event_connections, endboneconstraints_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndBoneConstraints().connect(endboneconstraints_event_connections, [](const Ptr<ObjectMeshSkinnedLegacy> & skinned) {
		Log::message("\Handling EndBoneConstraints event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endboneconstraints_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endboneconstraints_event_connection;

// subscribe to the EndBoneConstraints event with a handler function keeping the connection
publisher->getEventEndBoneConstraints().connect(endboneconstraints_event_connection, endboneconstraints_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endboneconstraints_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endboneconstraints_event_connection.setEnabled(true);

// ...

// remove subscription to the EndBoneConstraints event via the connection
endboneconstraints_event_connection.disconnect();

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

	// A EndBoneConstraints event handler implemented as a class member
	void event_handler(const Ptr<ObjectMeshSkinnedLegacy> & skinned)
	{
		Log::message("\Handling EndBoneConstraints event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndBoneConstraints().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endboneconstraints_handler_id;

// subscribe to the EndBoneConstraints event with a lambda handler function and keeping connection ID
endboneconstraints_handler_id = publisher->getEventEndBoneConstraints().connect(e_connections, [](const Ptr<ObjectMeshSkinnedLegacy> & skinned) {
		Log::message("\Handling EndBoneConstraints event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndBoneConstraints().disconnect(endboneconstraints_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndBoneConstraints events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndBoneConstraints().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndBoneConstraints().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < ObjectMeshSkinnedLegacy > &> getEventBeginBoneConstraints () const

Event triggered before the bone rotation constraints are applied. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

<details>
<summary>See Example | Close</summary>

**Usage Example**


```cpp
// implement the BeginBoneConstraints event handler
void beginboneconstraints_event_handler(const Ptr<ObjectMeshSkinnedLegacy> & skinned)
{
	Log::message("\Handling BeginBoneConstraints event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginboneconstraints_event_connections;

// link to this instance when subscribing for an event (subscription for various events can be linked)
objectmeshskinnedlegacy->getEventBeginBoneConstraints().connect(beginboneconstraints_event_connections, beginboneconstraints_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
objectmeshskinnedlegacy->getEventBeginBoneConstraints().connect(beginboneconstraints_event_connections, [](const Ptr<ObjectMeshSkinnedLegacy> & skinned) {
		Log::message("\Handling BeginBoneConstraints event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginboneconstraints_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginboneconstraints_event_connection;

// subscribe for the BeginBoneConstraints event with a handler function keeping the connection
objectmeshskinnedlegacy->getEventBeginBoneConstraints().connect(beginboneconstraints_event_connection, beginboneconstraints_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginboneconstraints_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginboneconstraints_event_connection.setEnabled(true);

// ...

// remove subscription for the BeginBoneConstraints event via the connection
beginboneconstraints_event_connection.disconnect();

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

	// A BeginBoneConstraints event handler implemented as a class member
	void event_handler(const Ptr<ObjectMeshSkinnedLegacy> & skinned)
	{
		Log::message("\Handling BeginBoneConstraints event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
objectmeshskinnedlegacy->getEventBeginBoneConstraints().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//  4. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe for the BeginBoneConstraints event with a handler function
objectmeshskinnedlegacy->getEventBeginBoneConstraints().connect(beginboneconstraints_event_handler);

// remove subscription for the BeginBoneConstraints event later by the handler function
objectmeshskinnedlegacy->getEventBeginBoneConstraints().disconnect(beginboneconstraints_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   5. Subscribe to an event saving an ID and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////

// define a connection ID to be used to unsubscribe later
EventConnectionId beginboneconstraints_handler_id;

// subscribe for the BeginBoneConstraints event with a lambda handler function and keeping connection ID
beginboneconstraints_handler_id = objectmeshskinnedlegacy->getEventBeginBoneConstraints().connect([](const Ptr<ObjectMeshSkinnedLegacy> & skinned) {
		Log::message("\Handling BeginBoneConstraints event (lambda).\n");
	}
);

// remove the subscription later using the ID
objectmeshskinnedlegacy->getEventBeginBoneConstraints().disconnect(beginboneconstraints_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   6. Ignoring all BeginBoneConstraints events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
objectmeshskinnedlegacy->getEventBeginBoneConstraints().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
objectmeshskinnedlegacy->getEventBeginBoneConstraints().setEnabled(true);
```

</details>


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<ObjectMeshSkinnedLegacy> & **skinned**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginBoneConstraints event handler
void beginboneconstraints_event_handler(const Ptr<ObjectMeshSkinnedLegacy> & skinned)
{
	Log::message("\Handling BeginBoneConstraints event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginboneconstraints_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginBoneConstraints().connect(beginboneconstraints_event_connections, beginboneconstraints_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginBoneConstraints().connect(beginboneconstraints_event_connections, [](const Ptr<ObjectMeshSkinnedLegacy> & skinned) {
		Log::message("\Handling BeginBoneConstraints event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginboneconstraints_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginboneconstraints_event_connection;

// subscribe to the BeginBoneConstraints event with a handler function keeping the connection
publisher->getEventBeginBoneConstraints().connect(beginboneconstraints_event_connection, beginboneconstraints_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginboneconstraints_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginboneconstraints_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginBoneConstraints event via the connection
beginboneconstraints_event_connection.disconnect();

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

	// A BeginBoneConstraints event handler implemented as a class member
	void event_handler(const Ptr<ObjectMeshSkinnedLegacy> & skinned)
	{
		Log::message("\Handling BeginBoneConstraints event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginBoneConstraints().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginboneconstraints_handler_id;

// subscribe to the BeginBoneConstraints event with a lambda handler function and keeping connection ID
beginboneconstraints_handler_id = publisher->getEventBeginBoneConstraints().connect(e_connections, [](const Ptr<ObjectMeshSkinnedLegacy> & skinned) {
		Log::message("\Handling BeginBoneConstraints event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginBoneConstraints().disconnect(beginboneconstraints_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginBoneConstraints events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginBoneConstraints().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginBoneConstraints().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < ObjectMeshSkinnedLegacy > &> getEventEndIKSolvers () const

Event triggered after the IK solvers are applied. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

<details>
<summary>See Example | Close</summary>

**Usage Example**


```cpp
// implement the EndIKSolvers event handler
void endiksolvers_event_handler(const Ptr<ObjectMeshSkinnedLegacy> & skinned)
{
	Log::message("\Handling EndIKSolvers event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endiksolvers_event_connections;

// link to this instance when subscribing for an event (subscription for various events can be linked)
objectmeshskinnedlegacy->getEventEndIKSolvers().connect(endiksolvers_event_connections, endiksolvers_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
objectmeshskinnedlegacy->getEventEndIKSolvers().connect(endiksolvers_event_connections, [](const Ptr<ObjectMeshSkinnedLegacy> & skinned) {
		Log::message("\Handling EndIKSolvers event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endiksolvers_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endiksolvers_event_connection;

// subscribe for the EndIKSolvers event with a handler function keeping the connection
objectmeshskinnedlegacy->getEventEndIKSolvers().connect(endiksolvers_event_connection, endiksolvers_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endiksolvers_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endiksolvers_event_connection.setEnabled(true);

// ...

// remove subscription for the EndIKSolvers event via the connection
endiksolvers_event_connection.disconnect();

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

	// A EndIKSolvers event handler implemented as a class member
	void event_handler(const Ptr<ObjectMeshSkinnedLegacy> & skinned)
	{
		Log::message("\Handling EndIKSolvers event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
objectmeshskinnedlegacy->getEventEndIKSolvers().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//  4. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe for the EndIKSolvers event with a handler function
objectmeshskinnedlegacy->getEventEndIKSolvers().connect(endiksolvers_event_handler);

// remove subscription for the EndIKSolvers event later by the handler function
objectmeshskinnedlegacy->getEventEndIKSolvers().disconnect(endiksolvers_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   5. Subscribe to an event saving an ID and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////

// define a connection ID to be used to unsubscribe later
EventConnectionId endiksolvers_handler_id;

// subscribe for the EndIKSolvers event with a lambda handler function and keeping connection ID
endiksolvers_handler_id = objectmeshskinnedlegacy->getEventEndIKSolvers().connect([](const Ptr<ObjectMeshSkinnedLegacy> & skinned) {
		Log::message("\Handling EndIKSolvers event (lambda).\n");
	}
);

// remove the subscription later using the ID
objectmeshskinnedlegacy->getEventEndIKSolvers().disconnect(endiksolvers_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   6. Ignoring all EndIKSolvers events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
objectmeshskinnedlegacy->getEventEndIKSolvers().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
objectmeshskinnedlegacy->getEventEndIKSolvers().setEnabled(true);
```

</details>


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<ObjectMeshSkinnedLegacy> & **skinned**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndIKSolvers event handler
void endiksolvers_event_handler(const Ptr<ObjectMeshSkinnedLegacy> & skinned)
{
	Log::message("\Handling EndIKSolvers event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endiksolvers_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndIKSolvers().connect(endiksolvers_event_connections, endiksolvers_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndIKSolvers().connect(endiksolvers_event_connections, [](const Ptr<ObjectMeshSkinnedLegacy> & skinned) {
		Log::message("\Handling EndIKSolvers event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endiksolvers_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endiksolvers_event_connection;

// subscribe to the EndIKSolvers event with a handler function keeping the connection
publisher->getEventEndIKSolvers().connect(endiksolvers_event_connection, endiksolvers_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endiksolvers_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endiksolvers_event_connection.setEnabled(true);

// ...

// remove subscription to the EndIKSolvers event via the connection
endiksolvers_event_connection.disconnect();

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

	// A EndIKSolvers event handler implemented as a class member
	void event_handler(const Ptr<ObjectMeshSkinnedLegacy> & skinned)
	{
		Log::message("\Handling EndIKSolvers event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndIKSolvers().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endiksolvers_handler_id;

// subscribe to the EndIKSolvers event with a lambda handler function and keeping connection ID
endiksolvers_handler_id = publisher->getEventEndIKSolvers().connect(e_connections, [](const Ptr<ObjectMeshSkinnedLegacy> & skinned) {
		Log::message("\Handling EndIKSolvers event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndIKSolvers().disconnect(endiksolvers_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndIKSolvers events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndIKSolvers().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndIKSolvers().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < ObjectMeshSkinnedLegacy > &> getEventBeginIKSolvers () const

Event triggered before the IK solvers are applied. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

<details>
<summary>See Example | Close</summary>

**Usage Example**


```cpp
// implement the BeginIKSolvers event handler
void beginiksolvers_event_handler(const Ptr<ObjectMeshSkinnedLegacy> & skinned)
{
	Log::message("\Handling BeginIKSolvers event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginiksolvers_event_connections;

// link to this instance when subscribing for an event (subscription for various events can be linked)
objectmeshskinnedlegacy->getEventBeginIKSolvers().connect(beginiksolvers_event_connections, beginiksolvers_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
objectmeshskinnedlegacy->getEventBeginIKSolvers().connect(beginiksolvers_event_connections, [](const Ptr<ObjectMeshSkinnedLegacy> & skinned) {
		Log::message("\Handling BeginIKSolvers event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginiksolvers_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginiksolvers_event_connection;

// subscribe for the BeginIKSolvers event with a handler function keeping the connection
objectmeshskinnedlegacy->getEventBeginIKSolvers().connect(beginiksolvers_event_connection, beginiksolvers_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginiksolvers_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginiksolvers_event_connection.setEnabled(true);

// ...

// remove subscription for the BeginIKSolvers event via the connection
beginiksolvers_event_connection.disconnect();

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

	// A BeginIKSolvers event handler implemented as a class member
	void event_handler(const Ptr<ObjectMeshSkinnedLegacy> & skinned)
	{
		Log::message("\Handling BeginIKSolvers event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
objectmeshskinnedlegacy->getEventBeginIKSolvers().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//  4. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe for the BeginIKSolvers event with a handler function
objectmeshskinnedlegacy->getEventBeginIKSolvers().connect(beginiksolvers_event_handler);

// remove subscription for the BeginIKSolvers event later by the handler function
objectmeshskinnedlegacy->getEventBeginIKSolvers().disconnect(beginiksolvers_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   5. Subscribe to an event saving an ID and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////

// define a connection ID to be used to unsubscribe later
EventConnectionId beginiksolvers_handler_id;

// subscribe for the BeginIKSolvers event with a lambda handler function and keeping connection ID
beginiksolvers_handler_id = objectmeshskinnedlegacy->getEventBeginIKSolvers().connect([](const Ptr<ObjectMeshSkinnedLegacy> & skinned) {
		Log::message("\Handling BeginIKSolvers event (lambda).\n");
	}
);

// remove the subscription later using the ID
objectmeshskinnedlegacy->getEventBeginIKSolvers().disconnect(beginiksolvers_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   6. Ignoring all BeginIKSolvers events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
objectmeshskinnedlegacy->getEventBeginIKSolvers().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
objectmeshskinnedlegacy->getEventBeginIKSolvers().setEnabled(true);
```

</details>


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<ObjectMeshSkinnedLegacy> & **skinned**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginIKSolvers event handler
void beginiksolvers_event_handler(const Ptr<ObjectMeshSkinnedLegacy> & skinned)
{
	Log::message("\Handling BeginIKSolvers event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginiksolvers_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginIKSolvers().connect(beginiksolvers_event_connections, beginiksolvers_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginIKSolvers().connect(beginiksolvers_event_connections, [](const Ptr<ObjectMeshSkinnedLegacy> & skinned) {
		Log::message("\Handling BeginIKSolvers event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginiksolvers_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginiksolvers_event_connection;

// subscribe to the BeginIKSolvers event with a handler function keeping the connection
publisher->getEventBeginIKSolvers().connect(beginiksolvers_event_connection, beginiksolvers_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginiksolvers_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginiksolvers_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginIKSolvers event via the connection
beginiksolvers_event_connection.disconnect();

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

	// A BeginIKSolvers event handler implemented as a class member
	void event_handler(const Ptr<ObjectMeshSkinnedLegacy> & skinned)
	{
		Log::message("\Handling BeginIKSolvers event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginIKSolvers().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginiksolvers_handler_id;

// subscribe to the BeginIKSolvers event with a lambda handler function and keeping connection ID
beginiksolvers_handler_id = publisher->getEventBeginIKSolvers().connect(e_connections, [](const Ptr<ObjectMeshSkinnedLegacy> & skinned) {
		Log::message("\Handling BeginIKSolvers event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginIKSolvers().disconnect(beginiksolvers_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginIKSolvers events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginIKSolvers().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginIKSolvers().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < ObjectMeshSkinnedLegacy > &> getEventEndLookAtSolvers () const

Event triggered after the LookAtChain solvers are applied. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

<details>
<summary>See Example | Close</summary>

**Usage Example**


```cpp
// implement the EndLookAtSolvers event handler
void endlookatsolvers_event_handler(const Ptr<ObjectMeshSkinnedLegacy> & skinned)
{
	Log::message("\Handling EndLookAtSolvers event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endlookatsolvers_event_connections;

// link to this instance when subscribing for an event (subscription for various events can be linked)
objectmeshskinnedlegacy->getEventEndLookAtSolvers().connect(endlookatsolvers_event_connections, endlookatsolvers_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
objectmeshskinnedlegacy->getEventEndLookAtSolvers().connect(endlookatsolvers_event_connections, [](const Ptr<ObjectMeshSkinnedLegacy> & skinned) {
		Log::message("\Handling EndLookAtSolvers event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endlookatsolvers_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endlookatsolvers_event_connection;

// subscribe for the EndLookAtSolvers event with a handler function keeping the connection
objectmeshskinnedlegacy->getEventEndLookAtSolvers().connect(endlookatsolvers_event_connection, endlookatsolvers_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endlookatsolvers_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endlookatsolvers_event_connection.setEnabled(true);

// ...

// remove subscription for the EndLookAtSolvers event via the connection
endlookatsolvers_event_connection.disconnect();

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

	// A EndLookAtSolvers event handler implemented as a class member
	void event_handler(const Ptr<ObjectMeshSkinnedLegacy> & skinned)
	{
		Log::message("\Handling EndLookAtSolvers event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
objectmeshskinnedlegacy->getEventEndLookAtSolvers().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//  4. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe for the EndLookAtSolvers event with a handler function
objectmeshskinnedlegacy->getEventEndLookAtSolvers().connect(endlookatsolvers_event_handler);

// remove subscription for the EndLookAtSolvers event later by the handler function
objectmeshskinnedlegacy->getEventEndLookAtSolvers().disconnect(endlookatsolvers_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   5. Subscribe to an event saving an ID and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////

// define a connection ID to be used to unsubscribe later
EventConnectionId endlookatsolvers_handler_id;

// subscribe for the EndLookAtSolvers event with a lambda handler function and keeping connection ID
endlookatsolvers_handler_id = objectmeshskinnedlegacy->getEventEndLookAtSolvers().connect([](const Ptr<ObjectMeshSkinnedLegacy> & skinned) {
		Log::message("\Handling EndLookAtSolvers event (lambda).\n");
	}
);

// remove the subscription later using the ID
objectmeshskinnedlegacy->getEventEndLookAtSolvers().disconnect(endlookatsolvers_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   6. Ignoring all EndLookAtSolvers events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
objectmeshskinnedlegacy->getEventEndLookAtSolvers().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
objectmeshskinnedlegacy->getEventEndLookAtSolvers().setEnabled(true);
```

</details>


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<ObjectMeshSkinnedLegacy> & **skinned**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndLookAtSolvers event handler
void endlookatsolvers_event_handler(const Ptr<ObjectMeshSkinnedLegacy> & skinned)
{
	Log::message("\Handling EndLookAtSolvers event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endlookatsolvers_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndLookAtSolvers().connect(endlookatsolvers_event_connections, endlookatsolvers_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndLookAtSolvers().connect(endlookatsolvers_event_connections, [](const Ptr<ObjectMeshSkinnedLegacy> & skinned) {
		Log::message("\Handling EndLookAtSolvers event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endlookatsolvers_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endlookatsolvers_event_connection;

// subscribe to the EndLookAtSolvers event with a handler function keeping the connection
publisher->getEventEndLookAtSolvers().connect(endlookatsolvers_event_connection, endlookatsolvers_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endlookatsolvers_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endlookatsolvers_event_connection.setEnabled(true);

// ...

// remove subscription to the EndLookAtSolvers event via the connection
endlookatsolvers_event_connection.disconnect();

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

	// A EndLookAtSolvers event handler implemented as a class member
	void event_handler(const Ptr<ObjectMeshSkinnedLegacy> & skinned)
	{
		Log::message("\Handling EndLookAtSolvers event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndLookAtSolvers().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endlookatsolvers_handler_id;

// subscribe to the EndLookAtSolvers event with a lambda handler function and keeping connection ID
endlookatsolvers_handler_id = publisher->getEventEndLookAtSolvers().connect(e_connections, [](const Ptr<ObjectMeshSkinnedLegacy> & skinned) {
		Log::message("\Handling EndLookAtSolvers event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndLookAtSolvers().disconnect(endlookatsolvers_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndLookAtSolvers events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndLookAtSolvers().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndLookAtSolvers().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < ObjectMeshSkinnedLegacy > &> getEventBeginLookAtSolvers () const

Event triggered before the LookAtChain solvers are applied. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

<details>
<summary>See Example | Close</summary>

**Usage Example**


```cpp
// implement the BeginLookAtSolvers event handler
void beginlookatsolvers_event_handler(const Ptr<ObjectMeshSkinnedLegacy> & skinned)
{
	Log::message("\Handling BeginLookAtSolvers event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginlookatsolvers_event_connections;

// link to this instance when subscribing for an event (subscription for various events can be linked)
objectmeshskinnedlegacy->getEventBeginLookAtSolvers().connect(beginlookatsolvers_event_connections, beginlookatsolvers_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
objectmeshskinnedlegacy->getEventBeginLookAtSolvers().connect(beginlookatsolvers_event_connections, [](const Ptr<ObjectMeshSkinnedLegacy> & skinned) {
		Log::message("\Handling BeginLookAtSolvers event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginlookatsolvers_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginlookatsolvers_event_connection;

// subscribe for the BeginLookAtSolvers event with a handler function keeping the connection
objectmeshskinnedlegacy->getEventBeginLookAtSolvers().connect(beginlookatsolvers_event_connection, beginlookatsolvers_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginlookatsolvers_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginlookatsolvers_event_connection.setEnabled(true);

// ...

// remove subscription for the BeginLookAtSolvers event via the connection
beginlookatsolvers_event_connection.disconnect();

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

	// A BeginLookAtSolvers event handler implemented as a class member
	void event_handler(const Ptr<ObjectMeshSkinnedLegacy> & skinned)
	{
		Log::message("\Handling BeginLookAtSolvers event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
objectmeshskinnedlegacy->getEventBeginLookAtSolvers().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//  4. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe for the BeginLookAtSolvers event with a handler function
objectmeshskinnedlegacy->getEventBeginLookAtSolvers().connect(beginlookatsolvers_event_handler);

// remove subscription for the BeginLookAtSolvers event later by the handler function
objectmeshskinnedlegacy->getEventBeginLookAtSolvers().disconnect(beginlookatsolvers_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   5. Subscribe to an event saving an ID and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////

// define a connection ID to be used to unsubscribe later
EventConnectionId beginlookatsolvers_handler_id;

// subscribe for the BeginLookAtSolvers event with a lambda handler function and keeping connection ID
beginlookatsolvers_handler_id = objectmeshskinnedlegacy->getEventBeginLookAtSolvers().connect([](const Ptr<ObjectMeshSkinnedLegacy> & skinned) {
		Log::message("\Handling BeginLookAtSolvers event (lambda).\n");
	}
);

// remove the subscription later using the ID
objectmeshskinnedlegacy->getEventBeginLookAtSolvers().disconnect(beginlookatsolvers_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   6. Ignoring all BeginLookAtSolvers events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
objectmeshskinnedlegacy->getEventBeginLookAtSolvers().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
objectmeshskinnedlegacy->getEventBeginLookAtSolvers().setEnabled(true);
```

</details>


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<ObjectMeshSkinnedLegacy> & **skinned**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginLookAtSolvers event handler
void beginlookatsolvers_event_handler(const Ptr<ObjectMeshSkinnedLegacy> & skinned)
{
	Log::message("\Handling BeginLookAtSolvers event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginlookatsolvers_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginLookAtSolvers().connect(beginlookatsolvers_event_connections, beginlookatsolvers_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginLookAtSolvers().connect(beginlookatsolvers_event_connections, [](const Ptr<ObjectMeshSkinnedLegacy> & skinned) {
		Log::message("\Handling BeginLookAtSolvers event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginlookatsolvers_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginlookatsolvers_event_connection;

// subscribe to the BeginLookAtSolvers event with a handler function keeping the connection
publisher->getEventBeginLookAtSolvers().connect(beginlookatsolvers_event_connection, beginlookatsolvers_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginlookatsolvers_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginlookatsolvers_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginLookAtSolvers event via the connection
beginlookatsolvers_event_connection.disconnect();

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

	// A BeginLookAtSolvers event handler implemented as a class member
	void event_handler(const Ptr<ObjectMeshSkinnedLegacy> & skinned)
	{
		Log::message("\Handling BeginLookAtSolvers event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginLookAtSolvers().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginlookatsolvers_handler_id;

// subscribe to the BeginLookAtSolvers event with a lambda handler function and keeping connection ID
beginlookatsolvers_handler_id = publisher->getEventBeginLookAtSolvers().connect(e_connections, [](const Ptr<ObjectMeshSkinnedLegacy> & skinned) {
		Log::message("\Handling BeginLookAtSolvers event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginLookAtSolvers().disconnect(beginlookatsolvers_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginLookAtSolvers events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginLookAtSolvers().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginLookAtSolvers().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<float, const Ptr < ObjectMeshSkinnedLegacy > &> getEventUpdate () const

Event triggered when the Engine calls the object update. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

<details>
<summary>See Example | Close</summary>

**Usage Example**


```cpp
// implement the Update event handler
void update_event_handler(float ifps,  const Ptr<ObjectMeshSkinnedLegacy> & skinned)
{
	Log::message("\Handling Update event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections update_event_connections;

// link to this instance when subscribing for an event (subscription for various events can be linked)
objectmeshskinnedlegacy->getEventUpdate().connect(update_event_connections, update_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
objectmeshskinnedlegacy->getEventUpdate().connect(update_event_connections, [](float ifps,  const Ptr<ObjectMeshSkinnedLegacy> & skinned) {
		Log::message("\Handling Update event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
update_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection update_event_connection;

// subscribe for the Update event with a handler function keeping the connection
objectmeshskinnedlegacy->getEventUpdate().connect(update_event_connection, update_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
update_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
update_event_connection.setEnabled(true);

// ...

// remove subscription for the Update event via the connection
update_event_connection.disconnect();

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

	// A Update event handler implemented as a class member
	void event_handler(float ifps,  const Ptr<ObjectMeshSkinnedLegacy> & skinned)
	{
		Log::message("\Handling Update event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
objectmeshskinnedlegacy->getEventUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//  4. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe for the Update event with a handler function
objectmeshskinnedlegacy->getEventUpdate().connect(update_event_handler);

// remove subscription for the Update event later by the handler function
objectmeshskinnedlegacy->getEventUpdate().disconnect(update_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   5. Subscribe to an event saving an ID and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////

// define a connection ID to be used to unsubscribe later
EventConnectionId update_handler_id;

// subscribe for the Update event with a lambda handler function and keeping connection ID
update_handler_id = objectmeshskinnedlegacy->getEventUpdate().connect([](float ifps,  const Ptr<ObjectMeshSkinnedLegacy> & skinned) {
		Log::message("\Handling Update event (lambda).\n");
	}
);

// remove the subscription later using the ID
objectmeshskinnedlegacy->getEventUpdate().disconnect(update_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   6. Ignoring all Update events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
objectmeshskinnedlegacy->getEventUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
objectmeshskinnedlegacy->getEventUpdate().setEnabled(true);
```

</details>


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(float **ifps**, const Ptr<ObjectMeshSkinnedLegacy> & **skinned**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Update event handler
void update_event_handler(float ifps,  const Ptr<ObjectMeshSkinnedLegacy> & skinned)
{
	Log::message("\Handling Update event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections update_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventUpdate().connect(update_event_connections, update_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventUpdate().connect(update_event_connections, [](float ifps,  const Ptr<ObjectMeshSkinnedLegacy> & skinned) {
		Log::message("\Handling Update event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
update_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection update_event_connection;

// subscribe to the Update event with a handler function keeping the connection
publisher->getEventUpdate().connect(update_event_connection, update_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
update_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
update_event_connection.setEnabled(true);

// ...

// remove subscription to the Update event via the connection
update_event_connection.disconnect();

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

	// A Update event handler implemented as a class member
	void event_handler(float ifps,  const Ptr<ObjectMeshSkinnedLegacy> & skinned)
	{
		Log::message("\Handling Update event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId update_handler_id;

// subscribe to the Update event with a lambda handler function and keeping connection ID
update_handler_id = publisher->getEventUpdate().connect(e_connections, [](float ifps,  const Ptr<ObjectMeshSkinnedLegacy> & skinned) {
		Log::message("\Handling Update event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventUpdate().disconnect(update_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Update events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## int getNumBoneConstraints () const

Returns the current total number of bone rotation constraints.
### Return value

Current total number of constraints.
## void setInterpolationAccuracy ( ObjectMeshSkinnedLegacy::INTERPOLATION_ACCURACY accuracy )

Sets a new interpolation mode for the bone rotations. The value is set to HIGH by default.
### Arguments

- *[ObjectMeshSkinnedLegacy::INTERPOLATION_ACCURACY](../../../api/library/objects/class.objectmeshskinnedlegacy_cpp.md#INTERPOLATION_ACCURACY)* **accuracy** - The interpolation mode for the bone rotations. The default value is set to HIGH.

## ObjectMeshSkinnedLegacy::INTERPOLATION_ACCURACY getInterpolationAccuracy () const

Returns the current interpolation mode for the bone rotations. The value is set to HIGH by default.
### Return value

Current interpolation mode for the bone rotations. The default value is set to HIGH.
## void setAnimPath ( const char * path )

Sets a new path to a file containing the specified animation.
### Arguments

- *const char ** **path** - The path to a file containing the specified animation.

## const char * getAnimPath () const

Returns the current path to a file containing the specified animation.
### Return value

Current path to a file containing the specified animation.
## void setMeshProceduralMode ( bool mode )

Sets a new value indicating if the [procedural mesh usage mode](#procedural_modification) is enabled for the object. With the procedural mode enabled, geometry of the **ObjectMeshSkinnedLegacy** can be modified via *[applyMeshProcedural()](../../...md#applyMeshProcedural_ConstMeshSkinned_int)*. Disabling the procedural mode restores the object's initial geometry, removing any changes applied. For skinned meshes, procedural geometry editing is done only through the direct main-thread workflow, unlike static meshes that can use asynchronous generation or [other update strategies](../../../api/library/objects/class.objectmeshstatic_cpp.md#procedural_workflow).
### Arguments

- *bool* **mode** - value indicating if the procedural mesh usage mode is enabled for the object

## bool isMeshProceduralMode () const

Returns the current value indicating if the [procedural mesh usage mode](#procedural_modification) is enabled for the object. With the procedural mode enabled, geometry of the **ObjectMeshSkinnedLegacy** can be modified via *[applyMeshProcedural()](../../...md#applyMeshProcedural_ConstMeshSkinned_int)*. Disabling the procedural mode restores the object's initial geometry, removing any changes applied. For skinned meshes, procedural geometry editing is done only through the direct main-thread workflow, unlike static meshes that can use asynchronous generation or [other update strategies](../../../api/library/objects/class.objectmeshstatic_cpp.md#procedural_workflow).
### Return value

value indicating if the procedural mesh usage mode is enabled for the object
## bool isLoaded () const

Returns the current value indicating if the mesh is loaded (it is either a procedural one or has been loaded via the [setMeshPath()](#setMeshPath_cstr_void) method).
### Return value

**true** if the mesh is procedural or has been loaded from a mesh file; otherwise **false**.
## void setMeshPath ( const char * path )

Sets a new path to the mesh file. If the *Procedural* flag is enabled for the object, the mesh won't be loaded.
### Arguments

- *const char ** **path** - The path to the mesh file.

## const char * getMeshPath () const

Returns the current path to the mesh file. If the *Procedural* flag is enabled for the object, the mesh won't be loaded.
### Return value

Current path to the mesh file.
---

## static ObjectMeshSkinnedLegacyPtr create ( const char * path )

ObjectMeshSkinnedLegacy constructor.
### Arguments

- *const char ** **path** - Path to the skinned mesh file.

## static ObjectMeshSkinnedLegacyPtr create ( )

ObjectMeshSkinnedLegacy constructor.
## int getBoneChild ( int bone , int child ) const

Returns the number of a child of the given bone.
### Arguments

- *int* **bone** - Bone number.
- *int* **child** - Child number.

### Return value

Number of the child in the collection of all bones.
## void setBoneTransformWithChildren ( int bone , const Math:: mat4 & transform )

Sets transformation for the bone and all of its children (without considering node transformations).
> **Notice:** Bones can be scaled only uniformly.


### Arguments

- *int* **bone** - Bone number.
- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix.

## const char * getBoneName ( int bone ) const

Returns the name of the given bone.
### Arguments

- *int* **bone** - Bone number.

### Return value

Bone name.
## int getBoneParent ( int bone ) const

Returns the number of the parent bone for a given one.
### Arguments

- *int* **bone** - Number of the bone, for which the parent will be returned.

### Return value

Parent bone number, if the parent exists; otherwise, -1.
## void setBoneTransform ( int bone , const Math:: mat4 & transform )

Sets a transformation matrix for the given bone (without considering node transformations).
> **Notice:** Bones can be scaled only uniformly.


### Arguments

- *int* **bone** - Bone number.
- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix.

## Math:: mat4 getBoneTransform ( int bone ) const

Returns a transformation matrix of the given bone relatively to the parent object (not considering transformations of the Mesh Skinned node itself).
### Arguments

- *int* **bone** - Bone number.

### Return value

Transformation matrix.
## void setBoneTransforms ( const int * bones , const Math:: mat4 * transforms , int num_bones )

Sets a transformation matrix for given bones.
### Arguments

- *const int ** **bones** - Bone numbers.
- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) ** **transforms** - Transformation matrices.
- *int* **num_bones** - Number of bones.

## int getCIndex ( int num , int surface ) const

Returns the [coordinate index](../../../api/library/rendering/class.mesh_cpp.md#cindices) for the given vertex of the given surface.
### Arguments

- *int* **num** - Vertex number in the range from 0 to the total number of coordinate indices for the given surface. > **Notice:** To get the total number of coordinate indices for the given surface, use the [getNumCIndices()](#getNumCIndices_int_int) method.
- *int* **surface** - Mesh surface number.

### Return value

Coordinate index.
## Math:: vec4 getColor ( int num , int surface ) const

Returns the color of the given [triangle vertex](../../../api/library/rendering/class.mesh_cpp.md#tvertex) of the given surface.
### Arguments

- *int* **num** - [Triangle vertex](../../../api/library/rendering/class.mesh_cpp.md#tvertex) number in the range from 0 to the total number of vertex color entries of the given surface. > **Notice:** To get the total number of vertex color entries for the surface, call the [*getNumColors()*](#getNumColors_int_int) method.
- *int* **surface** - Mesh surface number.

### Return value

Vertex color.
## void setLayer ( int layer , bool enabled , float weight )

Enables or disables the given animation layer and sets the value of the weight parameter.
### Arguments

- *int* **layer** - Animation layer number.
- *bool* **enabled** - Enable flag. true to enable the layer, false to disable it.
- *float* **weight** - Animation layer weight.

## void setLayerEnabled ( int layer , bool enabled )

Enables or disables a given animation layer.
### Arguments

- *int* **layer** - Animation layer number.
- *bool* **enabled** - true to enable the animation layer, false to disable it.

## bool isLayerEnabled ( int layer ) const

Returns a value indicating if a given animation layer is enabled.
### Arguments

- *int* **layer** - Animation layer number.

### Return value

true if the layer is disabled; otherwise, false.
## void setLayerWeight ( int layer , float weight )

Sets a weight for the animation layer.
### Arguments

- *int* **layer** - Animation layer number.
- *float* **weight** - Animation layer weight.

## float getLayerWeight ( int layer ) const

Returns the weight of the animation layer.
### Arguments

- *int* **layer** - Animation layer number.

### Return value

Weight of the animation layer.
## bool getMesh ( Ptr < MeshSkinned > & mesh ) const

Copies the current mesh into the destination mesh.
```cpp
// a skinned mesh from which geometry will be obtained
ObjectMeshSkinnedLegacyPtr skinnedMesh = ObjectMeshSkinnedLegacy::create("skinned.mesh");
// create a new mesh
MeshSkinnedPtr mesh = MeshSkinned::create();
// copy geometry to the created mesh
if (skinnedMesh->getMesh(mesh)) {
	// do something with the obtained mesh
}
else {
	Log::error("Failed to copy a mesh\n");
}

```


### Arguments

- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[MeshSkinned](../../../api/library/rendering/class.meshskinned_cpp.md)> &* **mesh** - Destination mesh to copy into.

### Return value

**1** if the mesh is copied successfully; otherwise, **0**.
## bool getMeshSurface ( const Ptr < Mesh > & mesh , int surface , int target = -1 ) const

Copies the specified mesh surface to the destination mesh.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Mesh](../../../api/library/rendering/class.mesh_cpp.md)> &* **mesh** - Destination [Mesh](../../../api/library/rendering/class.mesh_cpp.md) to copy the surface to.
- *int* **surface** - Number of the mesh surface to be copied.
- *int* **target** - Number of the surface morph target to be copied. The default value is -1 (all morph targets).

### Return value

Number of the new added mesh surface.
## Math:: vec3 getNormal ( int num , int surface , int target = 0 ) const

Returns the normal for the given [triangle vertex](../../../api/library/rendering/class.mesh_cpp.md#tvertex) of the given surface target.
### Arguments

- *int* **num** - [Triangle vertex](../../../api/library/rendering/class.mesh_cpp.md#tvertex) number in the range from 0 to the total number of vertex tangent entries of the given surface target. > **Notice:** Vertex normals are calculated using vertex tangents. To get the total number of vertex tangent entries for the surface target, call the [*getNumTangents()*](#getNumTangents_int_int) method.
- *int* **surface** - Mesh surface number.
- *int* **target** - Surface target number. The default value is 0.

### Return value

Vertex normal.
## int getNumBoneChildren ( int bone ) const

Returns the number of children for the specified bone.
### Arguments

- *int* **bone** - Bone number.

### Return value

Number of child bones.
## int getNumCIndices ( int surface ) const

Returns the number of [coordinate indices](../../../api/library/rendering/class.mesh_cpp.md#cindices) for the given mesh surface.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Number of coordinate indices.
## int getNumColors ( int surface ) const

Returns the total number of vertex color entries for the given surface.
> **Notice:** Colors are specified for [triangle vertices](../../../api/library/rendering/class.mesh_cpp.md#tvertex).


### Arguments

- *int* **surface** - Surface number.

### Return value

Number of vertex color entries.
## int getNumSurfaceTargets ( int surface ) const

Returns the number of surface morph targets for the given mesh surface.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Number of surface morph targets.
## int getNumTangents ( int surface ) const

Returns the number of vertex tangent entries of the given mesh surface.
> **Notice:** Tangents are specified for [triangle vertices](../../../api/library/rendering/class.mesh_cpp.md#tvertex).


### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Number of surface tangent vectors.
## int getNumTexCoords0 ( int surface ) const

Returns the number of the first UV map texture coordinates for the given mesh surface.
> **Notice:** First UV map texture coordinates are specified for [triangle vertices](../../../api/library/rendering/class.mesh_cpp.md#tvertex).


### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Number of the first UV map texture coordinates.
## int getNumTexCoords1 ( int surface ) const

Returns the number of the second UV map texture coordinates for the given mesh surface.
> **Notice:** Second UV map texture coordinates are specified for [triangle vertices](../../../api/library/rendering/class.mesh_cpp.md#tvertex).


### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Number of the second UV map texture coordinates.
## int getNumTIndices ( int surface ) const

Returns the number of triangle indices for the given mesh surface.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Number of [triangle indices](../../../api/library/rendering/class.mesh_cpp.md#tindices).
## int getNumVertex ( int surface ) const

Returns the number of [coordinate vertices](../../../api/library/rendering/class.mesh_cpp.md#cvertex) for the given mesh surface.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Number of the surface vertices.
## Math:: vec3 getSkinnedNormal ( int num , int index , int surface ) const

Returns the skinned normal for the given [triangle vertex](../../../api/library/rendering/class.mesh_cpp.md#tvertex).
> **Notice:** A skinned normal is a recalculated normal for bones and morph targets used in skinning.


### Arguments

- *int* **num** - [Triangle vertex](../../../api/library/rendering/class.mesh_cpp.md#tvertex) number in the range from 0 to the total number of vertex tangent entries of the given surface target. > **Notice:** Vertex normals are calculated using vertex tangents. To get the total number of vertex tangent entries for the surface target, call the [*getNumTangents()*](#getNumTangents_int_int) method.
- *int* **index** - [Coordinate index](../../../api/library/rendering/class.mesh_cpp.md#cindices) of the vertex. > **Notice:** if -1 is passed, the coordinate index will be obtained for the first vertex having its [triangle index](../../../api/library/rendering/class.mesh_cpp.md#tindices) equal to the specified [triangle vertex](../../../api/library/rendering/class.mesh_cpp.md#tvertex) number.
- *int* **surface** - Mesh surface number.

### Return value

Skinned normal.
## Math:: quat getSkinnedTangent ( int num , int index , int surface ) const

Returns the skinned tangent vector for the given [triangle vertex](../../../api/library/rendering/class.mesh_cpp.md#tvertex).
> **Notice:** A skinned tangent vector is a recalculated tangent vector for bones and morph targets used in skinning.


### Arguments

- *int* **num** - [Triangle vertex](../../../api/library/rendering/class.mesh_cpp.md#tvertex) number in the range from 0 to the total number of vertex tangent entries of the given surface target. > **Notice:** To get the total number of vertex tangent entries for the surface target, call the [*getNumTangents()*](#getNumTangents_int_int) method.
- *int* **index** - [Coordinate index](../../../api/library/rendering/class.mesh_cpp.md#cindices) of the vertex. > **Notice:** if -1 is passed, the coordinate index will be obtained for the first vertex having its [triangle index](../../../api/library/rendering/class.mesh_cpp.md#tindices) equal to the specified [triangle vertex](../../../api/library/rendering/class.mesh_cpp.md#tvertex) number.
- *int* **surface** - Mesh surface number.

### Return value

Skinned tangent.
## Math:: vec3 getSkinnedVertex ( int num , int surface ) const

Returns skinned coordinates of the given [coordinate vertex](../../../api/library/rendering/class.mesh_cpp.md#cvertex).
> **Notice:** A skinned vertex is a recalculated vertex for bones and morph targets used in skinning.


### Arguments

- *int* **num** - [Coordinate vertex](../../../api/library/rendering/class.mesh_cpp.md#cvertex) number in the range from 0 to the total number of coordinate vertices for the given surface. > **Notice:** To get the total number of coordinate vertices for the given surface, use the [getNumVertex()](#getNumVertex_int_int) method.
- *int* **surface** - Mesh surface number.

### Return value

Vertex coordinates.
## bool isNeedUpdate ( ) const

Returns a value indicating if the *ObjectMeshSkinnedLegacy* needs to be updated (e.g. after adding new animations).
### Return value

true if the skinned mesh needs to be updated; otherwise, false.
## const char * getSurfaceTargetName ( int surface , int target ) const

Returns the name of the morph target for the given mesh surface.
### Arguments

- *int* **surface** - Mesh surface number.
- *int* **target** - Morph target number.

### Return value

Morph target name.
## Math:: quat getTangent ( int num , int surface , int target = 0 ) const

Returns the tangent for the given [triangle vertex](../../../api/library/rendering/class.mesh_cpp.md#tvertex) of the given surface target.
### Arguments

- *int* **num** - [Triangle vertex](../../../api/library/rendering/class.mesh_cpp.md#tvertex) number in the range from 0 to the total number of vertex tangent entries of the given surface. > **Notice:** To get the total number of vertex tangent entries for the surface, call the [getNumTangents()](#getNumTangents_int_int) method.
- *int* **surface** - Mesh surface number.
- *int* **target** - Surface target number. The default value is 0.

### Return value

Vertex tangent.
## Math:: vec2 getTexCoord0 ( int num , int surface ) const

Returns first UV map texture coordinates for the given [triangle vertex](../../../api/library/rendering/class.mesh_cpp.md#tvertex) of the given surface.
### Arguments

- *int* **num** - [Triangle vertex](../../../api/library/rendering/class.mesh_cpp.md#tvertex) number in the range from 0 to the total number of first UV map texture coordinate entries of the given surface. > **Notice:** To get the total number of first UV map texture coordinate entries for the surface, call the [getNumTexCoords0()](#getNumTexCoords0_int_int) method.
- *int* **surface** - Mesh surface number.

### Return value

First UV map texture coordinates.
## Math:: vec2 getTexCoord1 ( int num , int surface ) const

Returns second UV map texture coordinates for the given [triangle vertex](../../../api/library/rendering/class.mesh_cpp.md#tvertex) of the given surface.
### Arguments

- *int* **num** - [Triangle vertex](../../../api/library/rendering/class.mesh_cpp.md#tvertex) number in the range from 0 to the total number of second UV map texture coordinate entries of the given surface. > **Notice:** To get the total number of second UV map texture coordinate entries for the surface, call the [getNumTexCoords1()](#getNumTexCoords1_int_int) method.
- *int* **surface** - Mesh surface number.

### Return value

Second UV map texture coordinates.
## int getTIndex ( int num , int surface ) const

Returns the [triangle index](../../../api/library/rendering/class.mesh_cpp.md#tindices) for the given surface by using the index number.
### Arguments

- *int* **num** - Vertex number in the range from 0 to the total number of triangle indices for the given surface. > **Notice:** To get the total number of triangle indices for the given surface, use the [getNumTIndices()](#getNumTIndices_int_int) method.
- *int* **surface** - Mesh surface number.

### Return value

Triangle index.
## Math:: vec3 getVertex ( int num , int surface , int target = 0 ) const

Returns coordinates of the given [coordinate vertex](../../../api/library/rendering/class.mesh_cpp.md#cvertex) of the given surface target.
### Arguments

- *int* **num** - [Coordinate vertex](../../../api/library/rendering/class.mesh_cpp.md#cvertex) number in the range from 0 to the total number of coordinate vertices for the given surface. > **Notice:** To get the total number of coordinate vertices for the given surface, use the [getNumCVertex()](../../../api/library/rendering/class.mesh_cpp.md#getNumCVertex_int_int) method.
- *int* **surface** - Mesh surface number.
- *int* **target** - Surface target number. The default value is 0.

### Return value

Vertex coordinates.
## void setBoneWorldTransformWithChildren ( int bone , const Math:: Mat4 & transform )

Sets the transformation for the given bone and all of its children in the world coordinate space (considering node transformations).
> **Notice:** Bones can be scaled only uniformly.


### Arguments

- *int* **bone** - Bone number.
- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix in the world space.

## void setBoneWorldTransform ( int bone , const Math:: Mat4 & transform )

Sets the transformation for the given bone in the world coordinate space.
> **Notice:** Bones can be scaled only uniformly.


### Arguments

- *int* **bone** - Bone number.
- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix in the world space.

## Math:: Mat4 getBoneWorldTransform ( int bone ) const

Returns the current transformation matrix applied to the bone in the world coordinate space (considering node transformations).
### Arguments

- *int* **bone** - Bone number.

### Return value

Transformation matrix in the world space.
## void getObjectPose ( const Ptr < SkeletonPoseMatrix > & out_pose ) const

Writes the current object-space bone transforms (the result of blending all animation layers) into the specified [SkeletonPoseMatrix](../../../api/library/animations/skeletal/class.skeletonposematrix_cpp.md).
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[SkeletonPoseMatrix](../../../api/library/animations/skeletal/class.skeletonposematrix_cpp.md)> &* **out_pose** - Output pose to receive the object-space bone transforms.

## int addLayer ( )

Appends a new animation layer to the current mesh.
### Return value

Number of the new added animation layer.
## void clearLayer ( int layer )

Clears the given animation layer.
### Arguments

- *int* **layer** - Animation layer number.

## void copyLayer ( int dest , int src )


Copies source layer bones transformations to the destination layer. The copying conditions are the following:


- If the destination layer has more bones than the source one, it will keep its former transformations.
- If the source layer has more bones than destination one, those bones will be added to the destination layer.


### Arguments

- *int* **dest** - Number of the destination layer in the range from 0 to the total number of animation layers. > **Notice:** To get the total number of animation layers, use the [getNumLayers()](#getNumLayers_int) method.
- *int* **src** - Number of the source layer in range from 0 to the total number of animation layers. > **Notice:** To get the total number of animation layers, use the [getNumLayers()](#getNumLayers_int) method.

## int findBone ( const char * name ) const

Searches for a bone with a given name.
### Arguments

- *const char ** **name** - Bone name.

### Return value

Bone number if found; otherwise, -1.
## int findSurfaceTarget ( int surface , const char * name ) const

Searches for a surface morph target with a given name.
### Arguments

- *int* **surface** - Mesh surface number.
- *const char ** **name** - Name of the morph target.

### Return value

Number of the morph target, if exists; otherwise, **-1**.
## void importLayer ( int layer )

Copies the current bone state to the given animation layer.
### Arguments

- *int* **layer** - Animation layer number.

## void inverseLayer ( int dest , int src )

Copies inverse transformations of bones from the source layer to the destination layer.
> **Notice:** Destination layer is not cleared before transformations are written to it.


### Arguments

- *int* **dest** - Number of the destination layer in the range from 0 to the total number of animation layers. > **Notice:** To get the total number of animation layers, use the [getNumLayers()](#getNumLayers_int) method.
- *int* **src** - Number of the source layer in the range from 0 to the total number of animation layers. > **Notice:** To get the total number of animation layers, use the [getNumLayers()](#getNumLayers_int) method.

## void lerpLayer ( int dest , int layer0 , int layer1 , float weight )

Copies interpolated bone transformations from two source layers to a destination layer.
> **Notice:** If there is no bone in one of the source layers, the bone transformation from another one will be copied to the destination layer without interpolation.


### Arguments

- *int* **dest** - Number of the destination layer in the range from 0 to the total number of animation layers. > **Notice:** To get the total number of animation layers, use the [getNumLayers()](#getNumLayers_int) method.
- *int* **layer0** - Number of the first source layer in the range from 0 to the total number of animation layers. > **Notice:** To get the total number of animation layers, use the [getNumLayers()](#getNumLayers_int) method.
- *int* **layer1** - Number of the second source layer in range from 0 to the total number of animation layers. > **Notice:** To get the total number of animation layers, use the [getNumLayers()](#getNumLayers_int) method.
- *float* **weight** - Interpolation weight.

## void lerpLayerByMask ( int dest , int layer0 , int layer1 , int mask_index , float weight )

Copies interpolated bone transformations from two source layers to a destination layer, using the specified bone mask (by index) to control per-bone blending weights.
### Arguments

- *int* **dest** - Number of the destination layer.
- *int* **layer0** - Number of the first source layer.
- *int* **layer1** - Number of the second source layer.
- *int* **mask_index** - Index of the bone mask to use for per-bone blending weights.
- *float* **weight** - Interpolation weight.

## void lerpLayerByMask ( int dest , int layer0 , int layer1 , const char * mask_name , float weight )

Copies interpolated bone transformations from two source layers to a destination layer, using the specified bone mask (by name) to control per-bone blending weights.
### Arguments

- *int* **dest** - Number of the destination layer.
- *int* **layer0** - Number of the first source layer.
- *int* **layer1** - Number of the second source layer.
- *const char ** **mask_name** - Name of the bone mask to use for per-bone blending weights.
- *float* **weight** - Interpolation weight.

## void mulLayer ( int dest , int layer0 , int layer1 , float weight = 1.0f )

Copies multiplied bone transformations from two source layers to the destination layer.
### Arguments

- *int* **dest** - Number of the destination layer in the range from 0 to the total number of animation layers. > **Notice:** To get the total number of animation layers, use the [getNumLayers()](#getNumLayers_int) method.
- *int* **layer0** - Number of the first source layer in the range from 0 to the total number of animation layers. > **Notice:** To get the total number of animation layers, use the [getNumLayers()](#getNumLayers_int) method.
- *int* **layer1** - Number of the second source layer in the range from 0 to the total number of animation layers. > **Notice:** To get the total number of animation layers, use the [getNumLayers()](#getNumLayers_int) method.
- *float* **weight** - Interpolation weight.

## void play ( )

Continues playback of the animation, if it was paused, or starts playback if it was stopped.
## void removeLayer ( int layer )

Removes an animation layer.
### Arguments

- *int* **layer** - Layer number in the range from 0 to the total number of animation layers. > **Notice:** To get the total number of animation layers, use the [getNumLayers()](#getNumLayers_int) method.

## void stop ( )

Stops animation playback. This function saves the playback position so that playing of the animation can be resumed from the same point.
## void getBlendingLayersPose ( const Ptr < SkeletonPoseDecomposed > & pose ) const

Writes the final blended pose (the result of blending all enabled animation layers according to their weights) into the specified [SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_cpp.md). This provides the decomposed (position, rotation, scale) representation of the blended animation state.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_cpp.md)> &* **pose** - Output pose to receive the blended result.

## static int type ( )

Returns the type of the node.
### Return value

[Node](../../../api/library/nodes/class.node_cpp.md) type identifier.
## void updateSkinned ( )

Forces update of all bone transformations.
## void setBindNode ( int bone , const Ptr < Node > & node )

Sets a new node whose transformation is to be used to control the transformation of the bone with the specified number.
### Arguments

- *int* **bone** - Number of the bone to be controlled by the specified node, in the range from 0 to the [total number of bones](#getNumBones_int).
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **node** - Node whose transformation is used to control the transformation of the bone.

## void removeBindNodeByBone ( int bone )

Removes the assigned bind node from the bone with the specified number.
### Arguments

- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).

## void removeBindNodeByNode ( const Ptr < Node > & node )

Removes the specified bind node.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **node** - Bind node to be removed.

## void removeAllBindNode ( )

Removes all assigned bind nodes.
## Ptr < Node > getBindNode ( int bone ) const

Returns the bind node currently assigned to the bone with the specified number.
### Arguments

- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).

### Return value

Node whose transformation is used to control the transformation of the bone if it is assigned; otherwise - nullptr.
## void setBindNodeSpace ( int bone , ObjectMeshSkinnedLegacy::NODE_SPACE space )

Sets a new value indicating which transformation of the bind node (*World* or *Local*) is to be used to override the transformation of the specified bone.
### Arguments

- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).
- *[ObjectMeshSkinnedLegacy::NODE_SPACE](../../../api/library/objects/class.objectmeshskinnedlegacy_cpp.md#NODE_SPACE)* **space** - Type of transformation of the bind node to be used to override the transformation of the specified bone, one of the [*NODE_SPACE**](#NODE_SPACE_LOCAL) values.

## ObjectMeshSkinnedLegacy::NODE_SPACE getBindNodeSpace ( int bone ) const

Returns the current value indicating which transformation of the bind node (*World* or *Local*) is to be used to override the transformation of the specified bone.
### Arguments

- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).

### Return value

Type of transformation of the bind node to be used to override the transformation of the specified bone, one of the [*NODE_SPACE**](#NODE_SPACE_LOCAL) values.
## void setBindBoneSpace ( int bone , ObjectMeshSkinnedLegacy::BONE_SPACE space )

Sets a value indicating which transformation of the specified bone is to be overridden by the bind node's transformation.
### Arguments

- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).
- *[ObjectMeshSkinnedLegacy::BONE_SPACE](../../../api/library/objects/class.objectmeshskinnedlegacy_cpp.md#BONE_SPACE)* **space** - Type of transformation of the specified bone to be overridden by the bind node's transformation, one of the [*BONE_SPACE**](#BONE_SPACE_LOCAL) values.

## ObjectMeshSkinnedLegacy::BONE_SPACE getBindBoneSpace ( int bone ) const

Returns the current value indicating which transformation of the specified bone is to be overridden by the bind node's transformation.
### Arguments

- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).

### Return value

Current type of transformation of the specified bone overridden by the bind node's transformation, one of the [*BONE_SPACE**](#BONE_SPACE_LOCAL) values.
## void setBindMode ( int bone , ObjectMeshSkinnedLegacy::BIND_MODE mode )

Sets a new type of blending of bind node's and bone's transformations.
### Arguments

- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).
- *[ObjectMeshSkinnedLegacy::BIND_MODE](../../../api/library/objects/class.objectmeshskinnedlegacy_cpp.md#BIND_MODE)* **mode** - New type of blending of bind node's and bone's transformations:

  - **OVERRIDE** - replace bone's transformation with the transformation of the node.
  - **ADDITIVE** - node's transformation is added to the current transformation of the bone.

## ObjectMeshSkinnedLegacy::BIND_MODE getBindMode ( int bone ) const

Returns the current type of blending of bind node's and bone's transformations.
### Arguments

- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).

### Return value

Current type of blending of bind node's and bone's transformations:
- **OVERRIDE** - replace bone's transformation with the transformation of the node.
- **ADDITIVE** - node's transformation is added to the current transformation of the bone.


## void setBindNodeOffset ( int bone , const Math:: Mat4 & offset )

Sets a new transformation matrix to be applied to the node's transformation before applying it to bone's transformation. This parameter serves for the purpose of additional correction of the node's transform for the bone's basis.
### Arguments

- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).
- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **offset** - Transformation matrix applied to the node's transformation before applying it to bone's transformation.

## Math:: Mat4 getBindNodeOffset ( int bone ) const

Returns the current transformation matrix which is applied to the node's transformation before applying it to bone's transformation. This parameter serves for the purpose of additional correction of the node's transform for the bone's basis.
### Arguments

- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).

### Return value

Transformation matrix currently applied to the node's transformation before applying it to bone's transformation.
## void addVisualizeBone ( int bone )

Adds a bone with the specified number to the list of the bones for which the basis vectors are to be visualized.
### Arguments

- *int* **bone** - Number of the bone to be added to the visualizer, in the range from 0 to the [total number of bones](#getNumBones_int).

## void removeVisualizeBone ( int bone )

Removes a bone with the specified number from the list of the bones for which the basis vectors are to be visualized.
### Arguments

- *int* **bone** - Number of the bone to be removed from the visualizer, in the range from 0 to the [total number of bones](#getNumBones_int).

## void clearVisualizeBones ( )

Clears the list of the bones for which the basis vectors are to be visualized.
## void addVisualizeIKChain ( int chain_id )

Adds an [IK chain](#ik_chains) with the specified ID to the list of chains for which the basis vectors are to be visualized.
### Arguments

- *int* **chain_id** - IK chain ID.

## void removeVisualizeIKChain ( int chain_id )

Removes the [IK chain](#ik_chains) with the specified ID from the list of chains for which the basis vectors are to be visualized.
### Arguments

- *int* **chain_id** - IK chain ID.

## void clearVisualizeIKChain ( )

Clears the list of [IK chains](#ik_chains) for which the basis vectors are to be visualized.
## int addIKChain ( )

Adds a new [IK chain](#ik_chains) to the skinned mesh.
### Return value

ID of the added IK chain.
## void removeIKChain ( int chain_id )

Removes the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *int* **chain_id** - IK chain ID.

## void setIKChainEnabled ( bool enabled , int chain_id )

Sets a value indicating if the [IK chain](#ik_chains) with the specified ID is enabled.
### Arguments

- *bool* **enabled** - Set **true** to enable IK chain with the specified ID, or **false** - to disable it.
- *int* **chain_id** - IK chain ID.

## bool isIKChainEnabled ( int chain_id ) const

Returns a value indicating if the [IK chain](#ik_chains) with the specified ID is enabled.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

**true** if the IK chain with the specified ID is enabled; otherwise, **false**.
## void setIKChainWeight ( float weight , int chain_id )

Sets a new weight for the [IK chain](#ik_chains) with the specified ID. Weight value defines the impact of the target position on the last joint of the chain.
### Arguments

- *float* **weight** - New weight value to be set in the [0.0f, 1.0f] range. *Higher* values increase the impact.
- *int* **chain_id** - IK chain ID.

## float getIKChainWeight ( int chain_id ) const

Returns the current weight for the [IK chain](#ik_chains) with the specified ID. Weight value defines the impact of the target position on the last joint of the chain.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

Current weight value in the [0.0f, 1.0f] range. *Higher* values increase the impact.
## int addIKChainBone ( int bone , int chain_id )

Adds a bone with the specified number to the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *int* **bone** - Bone number.
- *int* **chain_id** - IK chain ID.

### Return value

Index of the last added bone in the chain.
## int getIKChainNumBones ( int chain_id ) const

Returns the number of bones in the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

Number of bones in the IK chain with the specified ID.
## void removeIKChainBone ( int bone_num , int chain_id )

Removes the bone with the specified number from the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *int* **bone_num** - Bone number.
- *int* **chain_id** - IK chain ID.

## int getIKChainBone ( int bone_num , int chain_id ) const

Returns the index of the bone with the specified number (within the chain) from the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *int* **bone_num** - Bone number.
- *int* **chain_id** - IK chain ID.

### Return value

Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).
## void setIKChainTargetPosition ( const Math:: Vec3 & position , int chain_id )

Sets new local coordinates of the target position of the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **position** - New local coordinates of the target position to be set for the IK chain with the specified ID.
- *int* **chain_id** - IK chain ID.

## Math:: Vec3 getIKChainTargetPosition ( int chain_id ) const

Returns the current local coordinates of the target position of the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

Local coordinates of the target position of the IK chain with the specified ID.
## void setIKChainTargetWorldPosition ( const Math:: Vec3 & position , int chain_id )

Sets new world coordinates of the target position of the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **position** - New world coordinates of the target position to be set for the IK chain with the specified ID.
- *int* **chain_id** - IK chain ID.

## Math:: Vec3 getIKChainTargetWorldPosition ( int chain_id ) const

Returns the current world coordinates of the target position of the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

World coordinates of the target position of the IK chain with the specified ID.
## void setIKChainPolePosition ( const Math:: Vec3 & position , int chain_id )

Sets a new pole position (in local coordinates) for the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **position** - New pole position (in local coordinates) to be set for the IK chain.
- *int* **chain_id** - IK chain ID.

## Math:: Vec3 getIKChainPolePosition ( int chain_id ) const

Returns the current pole position (in local coordinates) for the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

Pole position (in local coordinates) for the IK chain.
## void setIKChainPoleWorldPosition ( const Math:: Vec3 & position , int chain_id )

Sets a new pole position (in world coordinates) for the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **position** - New pole position (in world coordinates) to be set for the IK chain.
- *int* **chain_id** - IK chain ID.

## Math:: Vec3 getIKChainPoleWorldPosition ( int chain_id ) const

Returns the current pole position (in world coordinates) for the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

Pole position (in world coordinates) for the IK chain.
## void setIKChainUseEffectorRotation ( bool use , int chain_id )

Sets a value indicating if the effector rotation is to be used for the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *bool* **use** - **true** to use effector rotation for the IK chain with the specified ID; **false** - not to use.
- *int* **chain_id** - IK chain ID.

## bool isIKChainUseEffectorRotation ( int chain_id ) const

Returns a value indicating if the effector rotation is to be used for the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

**true** if the effector rotation is to be used for the IK chain with the specified ID; otherwise, **false**.
## void setIKChainEffectorRotation ( const Math:: quat & rotation , int chain_id )

Sets the rotation of the end-effector (in local coordinates) of the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *const  Math::[quat](../../../api/library/math/class.quat_cpp.md) &* **rotation** - Quaternion that defines rotation (local coordinates) of the end-effector of the chain.
- *int* **chain_id** - IK chain ID.

## Math:: quat getIKChainEffectorRotation ( int chain_id ) const

Returns the current rotation (in local coordinates) of the end-effector of the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

Quaternion that defines rotation (local coordinates) of the end-effector of the chain.
## void setIKChainEffectorWorldRotation ( const Math:: quat & rotation , int chain_id )

Sets the rotation of the end-effector (in world coordinates) of the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *const  Math::[quat](../../../api/library/math/class.quat_cpp.md) &* **rotation** - Quaternion that defines rotation (world coordinates) of the end-effector of the chain.
- *int* **chain_id** - IK chain ID.

## Math:: quat getIKChainEffectorWorldRotation ( int chain_id ) const

Returns the current rotation (in world coordinates) of the end-effector of the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

Quaternion that defines rotation (world coordinates) of the end-effector of the chain.
## void setIKChainNumIterations ( int num , int chain_id )

Sets the number of iterations to be used for solving the [IK chain](#ik_chains) with the specified ID (number of times the algorithm runs).
### Arguments

- *int* **num** - Number of iterations to be used for solving the IK chain with the specified ID.
- *int* **chain_id** - IK chain ID.

## int getIKChainNumIterations ( int chain_id ) const

Returns the number of iterations used for solving the [IK chain](#ik_chains) with the specified ID (number of times the algorithm runs).
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

Current number of iterations for the IK chain with the specified ID.
## void setIKChainTolerance ( float tolerance , int chain_id )

Sets a new tolerance value to be used for the [IK chain](#ik_chains) with the specified ID. This value sets a threshold where the target is considered to have reached its destination position, and when the IK Solver stops iterating.
### Arguments

- *float* **tolerance** - Tolerance value to be set for the IK chain.
- *int* **chain_id** - IK chain ID.

## float getIKChainTolerance ( int chain_id ) const

Returns the current tolerance value to be used for the [IK chain](#ik_chains) with the specified ID. This value sets a threshold where the target is considered to have reached its destination position, and when the IK Solver stops iterating.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

Current tolerance value for the IK chain.
## void copyBoneTransforms ( const Ptr < ObjectMeshSkinnedLegacy > & src )

Copies all bone transformations from the specified source skinned mesh.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ObjectMeshSkinnedLegacy](../../../api/library/objects/class.objectmeshskinnedlegacy_cpp.md)> &* **src** - Source skinned mesh from which bone transforms are to be copied.

## bool applyMeshProcedural ( Ptr <ConstMeshSkinned> mesh )

**[ Main Thread ]** Replaces the object's current geometry with the provided mesh and **uploads it to VRAM**. Can only be called if [procedural mode](#procedural_modification) is enabled via *[setMeshProceduralMode()](../../...md#setMeshProceduralMode_int_void)*. If the source mesh contains compatible elements (e.g., bones, surfaces, skinning data) matching the original, then animations, morph targets, and other behaviors will continue to function without interruption. Otherwise, the mesh will remain static, with no animation or morphing applied.
> **Notice:** The procedural mesh remains in memory and will not be unloaded automatically.


### Arguments

- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<ConstMeshSkinned>* **mesh** - Source mesh.

### Return value

true if the information from the mesh is successfully copied into the procedural mesh, otherwise false.
## void setSurfaceTargetEnabled ( int surface , int target , bool enabled )

Toggles the use of the morph target for the specified surface.
### Arguments

- *int* **surface** - Number of the surface, to which the morph target is to be appended.
- *int* **target** - Number of the morph target to be used.
- *bool* **enabled** - true to enable the use of the morph target for the surface, false to disable it.

## int isSurfaceTargetEnabled ( int surface , int target ) const

Returns the value indicating if the use of the morph target for the specified surface is enabled.
### Arguments

- *int* **surface** - Number of the surface, to which the morph target is appended.
- *int* **target** - Number of the morph target.

### Return value

trueif the use of the morph target for the surface is enabled, otherwise false.
## void setSurfaceTargetWeight ( int surface , int target , float weight )

Sets the weight of the morph target, i.e. the intensity of it affecting the surface vertices.
### Arguments

- *int* **surface** - Number of the surface, to which the morph target is appended.
- *int* **target** - Number of the morph target.
- *float* **weight** - Weight of the morph target.

## float getSurfaceTargetWeight ( int surface , int target ) const

Returns the weight of the morph target, i.e. the intensity of it affecting the surface vertices.
### Arguments

- *int* **surface** - Number of the surface, to which the morph target is appended.
- *int* **target** - Number of the morph target.

### Return value

Weight of the morph target.
## void setLayerBoneTransform ( int layer , int bone , const Math:: mat4 & transform )

Sets a transformation matrix for the given bone. The difference from the [setBoneTransform()](#setBoneTransform_int_mat4_void) function is that this method takes into account only the transformation in the specified animation layer (no blending is performed).
> **Notice:** The bone can be scaled only uniformly.


### Arguments

- *int* **layer** - Animation layer number.
- *int* **bone** - Bone number.
- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Bone transformation matrix.

## Math:: mat4 getLayerBoneTransform ( int layer , int bone ) const

Returns a transformation matrix of the given bone relatively to the parent object.
> **Notice:** The difference from [getBoneTransform()](#getBoneTransform_int_mat4) is that this method takes into account only the transformation in the animation layer (no blending is done).


### Arguments

- *int* **layer** - Animation layer number.
- *int* **bone** - Bone number.

### Return value

Bone transformation matrix.
## Math:: mat4 getBoneRestLocalTransform ( int bone ) const

Returns the rest (bind pose) transformation of the specified bone in its local space relative to the parent bone.
### Arguments

- *int* **bone** - Bone number.

### Return value

Rest (bind pose) transformation matrix in the local bone space.
## void setLayerBonePosition ( int layer , int bone , const Math:: vec3 & position )

Sets the position for the given bone.
### Arguments

- *int* **layer** - Animation layer number.
- *int* **bone** - Bone number.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **position** - Bone position.

## Math:: vec3 getLayerBonePosition ( int layer , int bone ) const

Returns the position for the given bone.
### Arguments

- *int* **layer** - Animation layer number.
- *int* **bone** - Bone number.

### Return value

Bone position.
## void setLayerBoneRotation ( int layer , int bone , const Math:: quat & rotation )

Sets the rotation for the given bone.
### Arguments

- *int* **layer** - Animation layer number.
- *int* **bone** - Bone number.
- *const  Math::[quat](../../../api/library/math/class.quat_cpp.md) &* **rotation** - Bone rotation.

## Math:: quat getLayerBoneRotation ( int layer , int bone ) const

Returns the rotation for the given bone.
### Arguments

- *int* **layer** - Animation layer number.
- *int* **bone** - Bone number.

### Return value

Bone rotation.
## void setLayerBoneScale ( int layer , int bone , const Math:: vec3 & scale )

Sets the scale for the given bone.
### Arguments

- *int* **layer** - Animation layer number.
- *int* **bone** - Bone number.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **scale** - Bone scale.

## Math:: vec3 getLayerBoneScale ( int layer , int bone ) const

Returns the scale for the given bone.
### Arguments

- *int* **layer** - Animation layer number.
- *int* **bone** - Bone number.

### Return value

Bone scale.
## void setLayerFrameUsesEnabled ( int layer , bool enabled )

Toggles the use of animation masks for bones in the specified layer.
### Arguments

- *int* **layer** - Animation layer number.
- *bool* **enabled** - true to enable the use of animation masks for bones in the specified layer, false to disable it.

## bool isLayerFrameUsesEnabled ( int layer ) const

Returns the value indicating if the use of animation masks for bones in the specified layer is enabled.
### Arguments

- *int* **layer** - Animation layer number.

### Return value

true if the use of animation masks for bones in the specified layer is enabled, otherwise false.
## void setLayerBoneFrameUses ( int layer , int bone , ObjectMeshSkinnedLegacy::ANIM_FRAME_USES uses )

Sets the value indicating which components of the frame are to be used to animate the specified bone of the given animation layer.
### Arguments

- *int* **layer** - Animation layer number.
- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).
- *[ObjectMeshSkinnedLegacy::ANIM_FRAME_USES](../../../api/library/objects/class.objectmeshskinnedlegacy_cpp.md#ANIM_FRAME_USES)* **uses** - Value indicating frame components to be used.

## ObjectMeshSkinnedLegacy::ANIM_FRAME_USES getLayerBoneFrameUses ( int layer , int bone ) const

Returns the value indicating which components of the frame are to be used to animate the specified bone of the given animation layer.
### Arguments

- *int* **layer** - Animation layer number.
- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).

### Return value

Value indicating frame components to be used.
## void setLayerPose ( int layer , const Ptr <ConstSkeletonPoseDecomposed> & pose )

Sets the bone transforms for the specified animation layer from the given [SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_cpp.md). This overwrites all bone transforms in the layer with the values from the pose.
### Arguments

- *int* **layer** - Animation layer number.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<ConstSkeletonPoseDecomposed> &* **pose** - Pose to apply to the layer.

## void getLayerPose ( int layer , const Ptr < SkeletonPoseDecomposed > & out_pose ) const

Writes the bone transforms of the specified animation layer into the given [SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_cpp.md).
### Arguments

- *int* **layer** - Animation layer number.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_cpp.md)> &* **out_pose** - Output pose to receive the layer bone transforms.

## int getLayerNumFrames ( int layer ) const

Returns the number of animation frames for a given layer.
### Arguments

- *int* **layer** - Animation layer number.

### Return value

Number of animation frames.
## float setLayerFrame ( int layer , float frame , int from = -1 , int to = -1 )

Sets a frame for the given animation layer.
### Arguments

- *int* **layer** - Animation layer number.
- *float* **frame** - Frame number in the "from-to" interval. If the float argument is passed, animation is interpolated between nearby frames. 0 means the from frame. For larger values, a residue of a modulo *(from-to)* is calculated. If a negative value is provided, interpolation will be done from the current frame to the *from* frame.
- *int* **from** - Start frame. -1 means the first frame of the animation.
- *int* **to** - End frame. -1 means the last frame of the animation.

### Return value

The number of the frame.
## float getLayerFrame ( int layer ) const

Returns the frame number passed as the time argument on the last [setLayerFrame()](#setLayerFrame_int_float_int_int_float) call.
### Arguments

- *int* **layer** - Animation layer number.

### Return value

Frame number.
## int getLayerFrameFrom ( int layer ) const

Returns the start frame passed as the from argument on the last [setLayerFrame()](#setLayerFrame_int_float_int_int_float) call.
### Arguments

- *int* **layer** - Animation layer number.

### Return value

Start frame.
## int getLayerFrameTo ( int layer ) const

Returns the end frame passed as the to argument on the last [setLayerFrame()](#setLayerFrame_int_float_int_int_float) call.
### Arguments

- *int* **layer** - Animation layer number.

### Return value

End frame.
## long long getAnimationResourceID ( const char * path ) const

Returns the unique animation ID using the path to it. This method also loads the animation if it hasn't been loaded yet.
### Arguments

- *const char ** **path** - Path to the animation file. The path can be represented by either a path to the file or its [GUID](../../../principles/filesystem/index_cpp.md#guids), which is the recommended approach. After loading the animation, its internal representation is identified by the path when using *[setLayerAnimationFilePath](#setLayerAnimationFilePath_int_cstr_void)* , etc. > **Notice:** When you [import](../../../editor2/fbx/index.md) your model with animations from an FBX container, the following path to your `*.anim` files should be used: `<path_to_your_fbx_file>/<file.fbx>/<your_anim_file.anim>` > For example: *object->setLayerAnimationFilePath(0,"models/soldier/soldier.fbx/run.anim");*

### Return value

The unique animation ID.
## void setLayerAnimationFilePath ( int layer , const char * path )

Sets the path to animation for the given animation layer.
### Arguments

- *int* **layer** - Layer number.
- *const char ** **path** - Path to the animation file. > **Notice:** When you [import](../../../editor2/fbx/index.md) your model with animations from an FBX container, the following path to your `*.anim` files should be used: **<path_to_your_fbx_file>/<file.fbx>/<your_anim_file.anim>** > For example: *object->setLayerAnimationFilePath(0,"models/soldier/soldier.fbx/run.anim");*

## String getLayerAnimationFilePath ( int layer ) const

Returns the path to animation for the given animation layer.
### Arguments

- *int* **layer** - Layer number.

### Return value

Path to the animation file.
## void setLayerAnimationResourceID ( int layer , long long resource_id ) const

Sets the animation for the layer using the unique animation ID.
### Arguments

- *int* **layer** - Layer number.
- *long long* **resource_id** - The unique animation ID.

## long long getLayerAnimationResourceID ( int layer ) const

Returns the unique ID of the animation used for the layer.
### Arguments

- *int* **layer** - Layer number.

### Return value

The unique animation ID.
## Math:: mat4 getBoneBindLocalTransform ( int bone ) const

Returns the bone transformation matrix of the bind pose relatively to the parent bone.
> **Notice:** To get the bind pose transformation matrix in the object space, use [getBoneBindObjectTransform()](#getBoneBindObjectTransform_int_mat4).


### Arguments

- *int* **bone** - Bone number.

### Return value

Bind pose transformation matrix.
## Math:: mat4 getBoneBindLocalITransform ( int bone ) const

Returns the inverse bone transformation matrix of the bind pose relatively to the parent bone.
> **Notice:** To get the bind pose transformation matrix in the object space, use [getBoneBindObjectITransform()](#getBoneBindObjectITransform_int_mat4).


### Arguments

- *int* **bone** - Bone number.

### Return value

Inverse bind pose transformation matrix.
## Math:: mat4 getBoneBindObjectTransform ( int bone ) const

Returns the bone transformation matrix of the bind pose in the object space.
> **Notice:** To get the bind pose transformation matrix relatively to the parent bone, use [getBoneBindLocalTransform()](#getBoneBindLocalTransform_int_mat4).


### Arguments

- *int* **bone** - Bone number.

### Return value

Bind pose transformation matrix.
## Math:: mat4 getBoneBindObjectITransform ( int bone ) const

Returns the inverse bone transformation matrix of the bind pose in the object space.
> **Notice:** To get the bind pose transformation matrix relatively to the parent bone, use [getBoneBindLocalITransform()](#getBoneBindLocalITransform_int_mat4).


### Arguments

- *int* **bone** - Bone number.

### Return value

Inverse bind pose transformation matrix.
## Math:: mat4 getBoneSkinningTransform ( int bone ) const

Returns the bone matrix based on which the bone affects the connected vertices, the result of the following multiplication: getBoneTransform(bone) * getBoneBindObjectITransform(bone).
### Arguments

- *int* **bone** - Bone number.

### Return value

Bone transformation matrix.
## void addVisualizeLookAtChain ( int chain_id )

Adds the specified LookAtChain to visualization.
### Arguments

- *int* **chain_id** - LookAtChain ID.

## void removeVisualizeLookAtChain ( int chain_id )

Removes the specified LookAtChain from visualization.
### Arguments

- *int* **chain_id** - LookAtChain ID.

## void clearVisualizeLookAtChain ( )

Removes all LookAtChains from visualization.
## void addVisualizeConstraint ( int constraint_index )

Adds the specified bone constraint to visualization.
### Arguments

- *int* **constraint_index** - Bone constraint index.

## void removeVisualizeConstraint ( int constraint_index )

Removes the specified bone constraint from visualization.
### Arguments

- *int* **constraint_index** - Bone constraint index.

## void clearVisualizeConstraint ( )

Removes all bone constraints from visualization.
## int addLookAtChain ( )

Adds a new LookAtChain and returns its ID.
### Return value

LookAtChain ID.
## void removeLookAtChain ( int chain_id )

Deletes the specified LookAtChain by its ID.
### Arguments

- *int* **chain_id** - LookAtChain ID.

## int getNumLookAtChains ( ) const

Returns the total number of LookAtChains.
### Return value

Total number of LookAtChains.
## int getLookAtChainID ( int num ) const

Returns the ID of LookAtChain by its index.
### Arguments

- *int* **num** - Index of LookAtChain.

### Return value

LookAtChain ID.
## void setLookAtChainEnabled ( bool enabled , int chain_id )

Toggles the use of LookAtChain.
### Arguments

- *bool* **enabled** - true to enable LookAtChain, false to disable it.
- *int* **chain_id** - LookAtChain ID.

## bool isLookAtChainEnabled ( int chain_id ) const

Checks if LookAtChain is enabled.
### Arguments

- *int* **chain_id** - LookAtChain ID.

### Return value

true if LookAtChain is enabled, otherwise false.
## void setLookAtChainConstraint ( ObjectMeshSkinnedLegacy::CHAIN_CONSTRAINT constraint , int chain_id )

Configures the type of bone constraint for the solver of the specified chain.
### Arguments

- *[ObjectMeshSkinnedLegacy::CHAIN_CONSTRAINT](../../../api/library/objects/class.objectmeshskinnedlegacy_cpp.md#CHAIN_CONSTRAINT)* **constraint** - The type of bone constraint for the solver.
- *int* **chain_id** - LookAtChain ID.

## ObjectMeshSkinnedLegacy::CHAIN_CONSTRAINT getLookAtChainConstraint ( int chain_id ) const

Returns the type of bone constraint for the solver of the specified chain.
### Arguments

- *int* **chain_id** - LookAtChain ID.

### Return value

The type of bone constraint for the solver.
## void setLookAtChainWeight ( float weight , int chain_id )

Sets the weight of LookAtChain, which affects the extent of the bone rotation to the target.
### Arguments

- *float* **weight** - Weight of the chain.
- *int* **chain_id** - LookAtChain ID.

## float getLookAtChainWeight ( int chain_id ) const

Returns the weight of LookAtChain, which affects the extent of the bone rotation to the target.
### Arguments

- *int* **chain_id** - LookAtChain ID.

### Return value

Weight of the chain.
## int addLookAtChainBone ( int bone , int chain_id )

Adds the bone to LookAtChain and returns its index.
### Arguments

- *int* **bone** - The bone to be added to the chain.
- *int* **chain_id** - LookAtChain ID.

### Return value

Bone index.
## int addLookAtChainBone ( const char * bone_name , int chain_id )

Adds the bone to LookAtChain and returns its index.
### Arguments

- *const char ** **bone_name** - The name of the bone to be added to the chain.
- *int* **chain_id** - LookAtChain ID.

### Return value

Bone index.
## int getLookAtChainNumBones ( int chain_id ) const

Returns the total number of bones in LookAtChain.
### Arguments

- *int* **chain_id** - LookAtChain ID.

### Return value

The total number of bones in LookAtChain.
## void removeLookAtChainBone ( int bone_num , int chain_id )

Removes the bone from LookAtChain by its index.
### Arguments

- *int* **bone_num** - The index of the bone to be removed from the chain.
- *int* **chain_id** - LookAtChain ID.

## int getLookAtChainBone ( int bone_num , int chain_id ) const

Returns the bone from LookAtChain by its index.
### Arguments

- *int* **bone_num** - The index of the bone in the chain.
- *int* **chain_id** - LookAtChain ID.

## void setLookAtChainBoneWeight ( float weight , int bone_num , int chain_id )

Set the additional local weight of the bone.
### Arguments

- *float* **weight** - The weight of the bone in the chain.
- *int* **bone_num** - The index of the bone in the chain.
- *int* **chain_id** - LookAtChain ID.

## float getLookAtChainBoneWeight ( int bone_num , int chain_id ) const

Returns the additional local weight of the bone.
### Arguments

- *int* **bone_num** - The index of the bone in the chain.
- *int* **chain_id** - LookAtChain ID.

### Return value

The weight of the bone in the chain.
## void setLookAtChainBoneUp ( const Math:: Vec3 & up , int bone_num , int chain_id )

Sets the UP axis for the bone.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **up** - The UP vector for the bone.
- *int* **bone_num** - The index of the bone in the chain.
- *int* **chain_id** - LookAtChain ID.

## Math:: Vec3 getLookAtChainBoneUp ( int bone_num , int chain_id ) const

Returns the UP axis for the bone.
### Arguments

- *int* **bone_num** - The index of the bone in the chain.
- *int* **chain_id** - LookAtChain ID.

### Return value

The UP vector for the bone.
## void setLookAtChainBoneAxis ( const Math:: Vec3 & axis , int bone_num , int chain_id )

Sets the axis that is directed at the target of LookAtChain.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **axis** - The axis that is directed at the target.
- *int* **bone_num** - The index of the bone in the chain.
- *int* **chain_id** - LookAtChain ID.

## Math:: Vec3 getLookAtChainBoneAxis ( int bone_num , int chain_id ) const

Returns the axis that is directed at the target of LookAtChain.
### Arguments

- *int* **bone_num** - The index of the bone in the chain.
- *int* **chain_id** - LookAtChain ID.

### Return value

The axis that is directed at the target.
## void setLookAtChainTargetPosition ( const Math:: Vec3 & position , int chain_id )

Sets the position for the rotation in the object space.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **position** - The position for the rotation in the object space.
- *int* **chain_id** - LookAtChain ID.

## Math:: Vec3 getLookAtChainTargetPosition ( int chain_id ) const

Returns the position for the rotation in the object space.
### Arguments

- *int* **chain_id** - LookAtChain ID.

### Return value

The position for the rotation in the object space.
## void setLookAtChainTargetWorldPosition ( const Math:: Vec3 & position , int chain_id )

Sets the position for the rotation in the world space.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **position** - The position for the rotation in the world space.
- *int* **chain_id** - LookAtChain ID.

## Math:: Vec3 getLookAtChainTargetWorldPosition ( int chain_id ) const

Returns the position for the rotation in the world space.
### Arguments

- *int* **chain_id** - LookAtChain ID.

### Return value

The position for the rotation in the world space.
## void setLookAtChainPolePosition ( const Math:: Vec3 & position , int chain_id )

Sets the position of the pole vector in the object space.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **position** - The position of the pole vector in the object space.
- *int* **chain_id** - LookAtChain ID.

## Math:: Vec3 getLookAtChainPolePosition ( int chain_id ) const

Returns the position of the pole vector in the object space.
### Arguments

- *int* **chain_id** - LookAtChain ID.

### Return value

The position of the pole vector in the object space.
## void setLookAtChainPoleWorldPosition ( const Math:: Vec3 & position , int chain_id )

Sets the position of the pole vector in the world space.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **position** - The position of the pole vector in the world space.
- *int* **chain_id** - LookAtChain ID.

## Math:: Vec3 getLookAtChainPoleWorldPosition ( int chain_id ) const

Returns the position of the pole vector in the world space.
### Arguments

- *int* **chain_id** - LookAtChain ID.

### Return value

The position of the pole vector in the world space.
## int getIKChainID ( int num ) const

Returns the IKChain ID by its index.
### Arguments

- *int* **num** - IKChain index.

### Return value

IKChain ID.
## void setIKChainConstraint ( ObjectMeshSkinnedLegacy::CHAIN_CONSTRAINT constraint , int chain_id )

Configures the type of bone constraint for the solver of the specified chain.
### Arguments

- *[ObjectMeshSkinnedLegacy::CHAIN_CONSTRAINT](../../../api/library/objects/class.objectmeshskinnedlegacy_cpp.md#CHAIN_CONSTRAINT)* **constraint** - The type of bone constraint for the solver.
- *int* **chain_id** - IK chain ID.

## ObjectMeshSkinnedLegacy::CHAIN_CONSTRAINT getIKChainConstraint ( int chain_id ) const

Returns the type of bone constraint for the solver of the specified chain.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

The type of bone constraint for the solver.
## int addIKChainBone ( const char * bone_name , int chain_id )

Adds the bone to IKChain and returns its index.
### Arguments

- *const char ** **bone_name** - The bone name.
- *int* **chain_id** - IKChain ID.

### Return value

Bone index.
## int addBoneConstraint ( int bone )

Adds the rotation constraint to the specified bone.
### Arguments

- *int* **bone** - The bone index in the mesh.

### Return value

The constraint index.
## int addBoneConstraint ( const char * bone_name )

Adds the rotation constraint to the specified bone.
### Arguments

- *const char ** **bone_name** - The bone name.

### Return value

The constraint index.
## void removeBoneConstraint ( int constraint_num )

Removes the specified bone rotation constraint.
### Arguments

- *int* **constraint_num** - The constraint index.

## int findBoneConstraint ( int bone ) const

Returns the rotation constraint index for the specified bone.
### Arguments

- *int* **bone** - The bone index in the mesh.

### Return value

The constraint index.
## int findBoneConstraint ( const char * bone_name ) const

Returns the rotation constraint index for the specified bone.
### Arguments

- *const char ** **bone_name** - The bone name.

### Return value

The constraint index.
## void setBoneConstraintEnabled ( bool enabled , int constraint_num )

Enables the use of the rotation constraint for the bone.
### Arguments

- *bool* **enabled** - true to enable the use of the rotation constraint for the bone, false to disable it.
- *int* **constraint_num** - The constraint index.

## bool isBoneConstraintEnabled ( int constraint_num ) const

Returns the value indicating if the use of the rotation constraint for the bone is enabled.
### Arguments

- *int* **constraint_num** - The constraint index.

### Return value

true if the use of the rotation constraint for the bone is enabled, otherwise false.
## int getBoneConstraintBoneIndex ( int constraint_num ) const

Returns the index of the bone for which the rotation constraint is set.
### Arguments

- *int* **constraint_num** - The constraint index.

### Return value

The bone index in the mesh.
## void setBoneConstraintYawAxis ( const Math:: vec3 & axis , int constraint_num )

Sets the yaw axis for the bone rotation constraint.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **axis** - The yaw axis.
- *int* **constraint_num** - The constraint index.

## Math:: vec3 getBoneConstraintYawAxis ( int constraint_num ) const

Returns the yaw axis for the bone rotation constraint.
### Arguments

- *int* **constraint_num** - The constraint index.

### Return value

The yaw axis.
## void setBoneConstraintPitchAxis ( const Math:: vec3 & axis , int constraint_num )

Sets the pitch axis for the bone rotation constraint.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **axis** - The pitch axis.
- *int* **constraint_num** - The constraint index.

## Math:: vec3 getBoneConstraintPitchAxis ( int constraint_num ) const

Returns the pitch axis for the bone rotation constraint.
### Arguments

- *int* **constraint_num** - The constraint index.

### Return value

The pitch axis.
## void setBoneConstraintRollAxis ( const Math:: vec3 & axis , int constraint_num )

Sets the roll axis for the bone rotation constraint.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **axis** - The roll axis.
- *int* **constraint_num** - The constraint index.

## Math:: vec3 getBoneConstraintRollAxis ( int constraint_num ) const

Returns the roll axis for the bone rotation constraint.
### Arguments

- *int* **constraint_num** - The constraint index.

### Return value

The roll axis.
## void setBoneConstraintYawAngles ( float min_angle , float max_angle , int constraint_num )

Sets the minimum and maximum angles restricting the bone rotation along the yaw axis.
### Arguments

- *float* **min_angle** - The minimum rotation angle.
- *float* **max_angle** - The maximum rotation angle.
- *int* **constraint_num** - The constraint index.

## float getBoneConstraintYawMinAngle ( int constraint_num ) const

Returns the minimum angle restricting the bone rotation along the yaw axis.
### Arguments

- *int* **constraint_num** - The constraint index.

### Return value

The minimum rotation angle.
## float getBoneConstraintYawMaxAngle ( int constraint_num ) const

Returns the maximum angle restricting the bone rotation along the yaw axis.
### Arguments

- *int* **constraint_num** - The constraint index.

### Return value

The maximum rotation angle.
## void setBoneConstraintPitchAngles ( float min_angle , float max_angle , int constraint_num )

Sets the minimum and maximum angles restricting the bone rotation along the pitch axis.
### Arguments

- *float* **min_angle** - The minimum rotation angle.
- *float* **max_angle** - The maximum rotation angle.
- *int* **constraint_num** - The constraint index.

## float getBoneConstraintPitchMinAngle ( int constraint_num ) const

Returns the minimum angle restricting the bone rotation along the pitch axis.
### Arguments

- *int* **constraint_num** - The constraint index.

### Return value

The minimum rotation angle.
## float getBoneConstraintPitchMaxAngle ( int constraint_num ) const

Returns the maximum angle restricting the bone rotation along the pitch axis.
### Arguments

- *int* **constraint_num** - The constraint index.

### Return value

The maximum rotation angle.
## void setBoneConstraintRollAngles ( float min_angle , float max_angle , int constraint_num )

Sets the minimum and maximum angles restricting the bone rotation along the roll axis.
### Arguments

- *float* **min_angle** - The minimum rotation angle.
- *float* **max_angle** - The maximum rotation angle.
- *int* **constraint_num** - The constraint index.

## float getBoneConstraintRollMinAngle ( int constraint_num ) const

Returns the minimum angle restricting the bone rotation along the roll axis.
### Arguments

- *int* **constraint_num** - The constraint index.

### Return value

The minimum rotation angle.
## float getBoneConstraintRollMaxAngle ( int constraint_num ) const

Returns the maximum angle restricting the bone rotation along the roll axis.
### Arguments

- *int* **constraint_num** - The constraint index.

### Return value

The maximum rotation angle.
## bool isLayerAnimationStreaming ( int layer ) const

Returns a value indicating if the animation on the specified layer is currently being loaded by the [data streaming](../../../principles/data_streaming/index.md) system. While the animation is streaming, the layer holds the first frame of this animation.
### Arguments

- *int* **layer** - Layer number.

### Return value

true if the animation assigned to the specified layer is still being streamed in; otherwise, false.
## void resetLayerToBindPose ( int layer )

Sets the skeleton's bind pose on the specified layer.
### Arguments

- *int* **layer** - Layer number.

## void resetLayerToRestPose ( int layer )

Sets the mesh's rest pose on the specified layer.
### Arguments

- *int* **layer** - Layer number.

## bool loadAsyncRender ( )

Requests asynchronous loading of the mesh for rendering. The mesh becomes available in one of the following frames, so the object keeps rendering whatever it already has until then.
### Return value

true if the request has been queued; otherwise, false.
## bool loadForceRender ( )

Loads the mesh for rendering immediately, blocking until it is done.
### Return value

true if the mesh has been loaded; otherwise, false.
