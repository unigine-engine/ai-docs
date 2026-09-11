# ObjectMeshSkinnedLegacy Class (CS)

**Inherits from:** Object


This class is used to create and modify [skinned meshes](../../../objects/objects/mesh_skinned_legacy/index.md). Skinned Meshes are used to render characters with animation.


#### Applying Animation


Animation is applied to *ObjectMeshSkinnedLegacy* via its layers. Layers store skeletal poses, the pose is taken from the animation.


By default, when created, *ObjectMeshSkinnedLegacy* has only one active base layer, the pose of which is used for animation. More layers can be added to store various poses that may be blended or processed otherwise (through such functions as *[*LerpLayer*](#lerpLayer_int_int_int_float_void)*, *[*CopyLayer*](#copyLayer_int_int_void)*, *[*ImportLayer*](#importLayer_int_void)*, *[*InverseLayer*](#inverseLayer_int_int_void)* and *[*MulLayer*](#mulLayer_int_int_int_float_void)*), with the resulting pose saved in the base layer for final render output.


**Automatic blending** of animations suitable for simple use cases is implemented internally in ObjectMeshSkinnedLegacy. For a layer to be included in the final blend, it must be enabled and have a non-zero weight. These values can be changed using **[SetLayer()](../../...md#setLayer_int_int_float_void)**, **[SetLayerEnabled()](../../...md#setLayerEnabled_int_int_void)** and **[SetLayerWeight()](../../...md#setLayerWeight_int_float_void)**. When blending, an arithmetic weighted average is applied: all layer weights are first normalized, after which each component is multiplied by its corresponding weight and summed.


A similar approach is used for scaling and a slightly different one for rotations, but for working at the layer level this is not critical.


**Customized blending** of animations including partial bone blending, additive animation, and so on, is implemented via custom logic. You can control individual bones on layers using **[SetLayerBoneTransform()](../../...md#setLayerBoneTransform_int_int_mat4_void)** / **[GetLayerBoneTransform()](../../...md#getLayerBoneTransform_int_int_mat4)**, as well as their counterparts for individual components: position, rotation and scale. These functions allow you to create masks for bones and then work exclusively with those bones in a loop.


##### Creating and Playing Animation


To add the animation to the ObjectMeshSkinnedLegacy and play it, do the following:


1. Set the number of animation layers with **[NumLayers](../../...md#setNumLayers_int_void)**. There is only one layer by default, the pose of which is used for animation.
2. Enable each layer and set the animation weight for blending by calling the **[SetLayer()](../../...md#setLayer_int_int_float_void)** function.
3. Add the animation `*.anim` file by using the **[SetLayerAnimationFilePath()](../../...md#setLayerAnimationFilePath_int_cstr_void)** function.
4. Play the added animation by calling the **[SetLayerFrame()](../../...md#setLayerFrame_int_float_int_int_float)** function for each animation layer.


Blending is performed between all layers. The contribution of each layer depends on its weight. Also, you can optionally define single bone transformations by hand, if needed, using either **[SetBoneTransform()](../../...md#setBoneTransform_int_mat4_void)** or **[SetBoneTransformWithChildren()](../../...md#setBoneTransformWithChildren_int_mat4_void)**.


###### Usage Example


The following example shows how to blend two different animations assigned to a mesh. You can use the mesh and animations from UNIGINE samples located in the following sample set folders:


- `<cpp_samples>/data/showcase_content/person`
- `<csharp_component_samples>/data/showcase_content/agent`


Animations are added by using the **[SetLayerAnimationFilePath()](../../...md#setLayerAnimationFilePath_int_cstr_void)** function.


```csharp
using Unigine;

public partial class SkinnedMeshController : Component
{
	public AssetLink meshAsset;
	public AssetLink animAsset1;
	public AssetLink animAsset2;

	private ObjectMeshSkinnedLegacy skinnedMesh;

	void Init()
	{
		// create the new ObjectMeshSkinnedLegacy mesh based on an existing mesh
		skinnedMesh = new ObjectMeshSkinnedLegacy(meshAsset.Path);

		// we need two layers to get poses from two animations
		skinnedMesh.NumLayers = 2;

		// load animations from the files on separate layers
		skinnedMesh.SetLayerAnimationFilePath(0, animAsset1.Path);
		skinnedMesh.SetLayerAnimationFilePath(1, animAsset2.Path);

		// enable each layer and set an animation weight
		skinnedMesh.SetLayer(0, true, 0.7f);
		skinnedMesh.SetLayer(1, true, 0.3f);
	}

	void Update()
	{
		// play each animation, getting new poses with each frame update
		skinnedMesh.SetLayerFrame(0, Game.Time * 25.0f);
		skinnedMesh.SetLayerFrame(1, Game.Time * 25.0f);
	}
}

```


###### Usage Example


This example demonstrates how to blend animations using the gradient band interpolation. You can add all animations for *ObjectMeshSkinnedLegacy* on separate layers and then update their weights.


This is a [C# Component System](../../../principles/component_system/component_system_cs/index.md) component. [Assign](../../../principles/component_system/component_system_cs/index.md#apply) this component to your *ObjectMeshSkinnedLegacy* and add the necessary animation files.


The complete source code:


<details>
<summary>Blend2D.cs | Close</summary>

```csharp
using System.Collections;
using System.Collections.Generic;
using Unigine;

public class Blend2D : Component
{
	private ObjectMeshSkinnedLegacy meshSkinned = null;

	public struct Animation
	{
		public string name;

		[ParameterAsset(Filter = "anim")]
		public AssetLink asset;

		public vec2 point;
	}

	[ShowInEditor]
	[ParameterSlider(Min = MathLib.EPSILON)]
	private float targetDuration = 2.0f;

	[ShowInEditor]
	private List<Animation> animations = new List<Animation>()
	{
		new Animation() { name = "Idle", point = new vec2(0, 0) },
		new Animation() { name = "Forward", point = new vec2(0, 1) },
		new Animation() { name = "Backward", point = new vec2(0, -1) },
		new Animation() { name = "Right", point = new vec2(1, 0) },
		new Animation() { name = "Left", point = new vec2(-1, 0) },
	};

	// for playback
	private float time = 0.0f;
	private List<float> speeds = new List<float>();

	// for blending
	private List<vec2> points = new List<vec2>();
	private List<float> weights = new List<float>();
	private vec2 targetPoint = new vec2(0, 0);

	private void Init()
	{
		meshSkinned = node as ObjectMeshSkinnedLegacy;
		if (!meshSkinned)
			return;

		// remove default layer
		meshSkinned.RemoveLayer(0);

		for (int i = 0; i < animations.Count; i++)
		{
			if (animations[i].asset.IsNull || !animations[i].asset.IsFileExist)
				continue;

			// create layer for each animation
			meshSkinned.AddLayer();
			meshSkinned.SetLayerAnimationFilePath(meshSkinned.NumLayers - 1, animations[i].asset.Path);

			// enable new layer and set default weight to 1.0
			meshSkinned.SetLayer(meshSkinned.NumLayers - 1, true, 1.0f);

			// calculate animation speed to play with fixed duration
			int numFrames = meshSkinned.GetLayerNumFrames(meshSkinned.NumLayers - 1);
			float speed = numFrames / targetDuration;
			speeds.Add(speed);

			// add point and weight for blending
			points.Add(animations[i].point);
			weights.Add(1.0f);
		}
	}

	private void Update()
	{
		if (!meshSkinned)
			return;

		// update weight for each layer
		UpdateWeights();

		// update layer frames and layer weights
		for (int i = 0; i < meshSkinned.NumLayers; i++)
		{
			float frame = time * speeds[i];
			meshSkinned.SetLayerFrame(i, frame);
			meshSkinned.SetLayerWeight(i, weights[i]);
		}

		time += Game.IFps;
		if (time > targetDuration)
			time -= targetDuration;

		// update target point for blending
		ivec2 movement = new ivec2();
		if (Input.IsKeyPressed(Input.KEY.T))
			movement += new ivec2(0, 1);

		if (Input.IsKeyPressed(Input.KEY.G))
			movement -= new ivec2(0, 1);

		if (Input.IsKeyPressed(Input.KEY.H))
			movement += new ivec2(1, 0);

		if (Input.IsKeyPressed(Input.KEY.F))
			movement -= new ivec2(1, 0);

		if (movement.x != 0)
			targetPoint.x += movement.x * Game.IFps * 2.0f;
		else
			targetPoint.x *= MathLib.Exp(-Game.IFps * 3.0f);

		if (movement.y != 0)
			targetPoint.y += movement.y * Game.IFps * 2.0f;
		else
			targetPoint.y *= MathLib.Exp(-Game.IFps * 3.0f);

		targetPoint = MathLib.Clamp(targetPoint, new vec2(-1, -1), new vec2(1, 1));
	}

	private void UpdateWeights()
	{
		// gradient band interpolation

		float totalWeight = 0.0f;
		for (int i = 0; i < points.Count; i++)
		{
			vec2 pi = points[i];
			vec2 targetVector = targetPoint - pi;

			float weight = 1.0f;
			for (int j = 0; j < points.Count; j++)
			{
				if (j == i)
					continue;

				vec2 jVector = points[j] - pi;

				float newWeight = 1.0f - MathLib.Dot(targetVector, jVector) / jVector.Length2;
				newWeight = MathLib.Clamp(newWeight, 0.0f, 1.0f);

				weight = MathLib.Min(weight, newWeight);
			}

			weights[i] = weight;
			totalWeight += weight;
		}

		for (int i = 0; i < weights.Count; i++)
			weights[i] = weights[i] / totalWeight;
	}
}

```

</details>


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


In contrast to [procedural modes](../../../api/library/objects/class.objectmeshstatic_cs.md#PROCEDURAL_MODE) available for static meshes, skinned meshes have **only one mode** - equivalent to *[PROCEDURAL_MODE_DYNAMIC](../../../api/library/objects/class.objectmeshstatic_cs.md#PROCEDURAL_MODE_DYNAMIC)* (the procedural mesh remains in VRAM and will not be unloaded).


Procedural updates for skinned meshes are performed exclusively in the Engine's main thread using *[ApplyMeshProcedural()](../../...md#applyMeshProcedural_ConstMeshSkinned_int)*. If the source mesh contains compatible elements (e.g., bones, surfaces, skinning data) matching the original, then animations, morph targets, and other behaviors will continue to function without interruption. Otherwise, the mesh will remain static, with no animation or morphing applied.


#### Reusing Animations


Animations from one character can be used for another.


##### Animation Frame Masks


Masks are the simplest way of reusing animations, a couple of words about how they work. To each layer of an *ObjectMeshSkinnedLegacy* you can assign some animation and based on its frames it will change bone transformations on this layer. You can use **[masks](#ANIM_FRAME_USES_NONE)** to choose which components of the animation frame (position, rotation, scale, their combinations, or all of them) are to be used for each particular layer. In case any component is missing in the mask, the corresponding value will be taken from the T-pose.


As an example let's take eyes animation for these two skeletons:


![](anim_mask_1.jpg)


They have absolutely the same bone hierarchy as well as bone names, only the proportions differ. If we use animation for eyes from the left skeleton for the right one, we'll get the following result:


![](anim_mask_2.jpg)


The initial animation has completely changed the proportions of the second skeleton. We can fix it by setting **[ANIM_FRAME_USES_ROTATION](#ANIM_FRAME_USES_ROTATION)** mask to eye bones, and **[ANIM_FRAME_USES_NONE](#ANIM_FRAME_USES_NONE)** for the rest of the bones via the **[SetLayerBoneFrameUses()](../../...md#setLayerBoneFrameUses_int_int_int_void)* / *[GetLayerBoneFrameUses()](../../...md#getLayerBoneFrameUses_int_int_int)** methods. Thus, all values except for eyes rotation will be taken from the T-pose :


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


To visualize IK chains you can use the following methods: **[AddVisualizeIKChain()](../../...md#addVisualizeIKChain_int_void)*, *[RemoveVisualizeIKChain()](../../...md#removeVisualizeIKChain_int_void)**, and **[ClearVisualizeIKChain()](../../...md#clearVisualizeIKChain_void)**.


![](ik_visualizer.gif)


### See Also


- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* class
- Article on [Mesh File Formats](../../../code/formats/file_formats.md#mesh)
- Animation samples in *[C++](../../../sdk/api_samples/cpp/animation.md)* and *[C# Component Samples](../../../sdk/api_samples/cs/animation.md)* suites


## ObjectMeshSkinnedLegacy Class

### Enums

## BONE_SPACE

Defines which transformation of the bone is to be overridden by the bind node's transformation.
| Name | Description |
|---|---|
| **WORLD** = 0 | World coordinates. |
| **OBJECT** = 1 | Coordinates relative to the skinned mesh object. |
| **LOCAL** = 2 | Coordinates relative to the parent bone. |

## NODE_SPACE

Defines the type of transformation of the bind node to be used to override the transformation of the specified bone.
| Name | Description |
|---|---|
| **WORLD** = 0 | World transformation of the node. |
| **LOCAL** = 1 | Local transformation of the node. |

## BIND_MODE

Type of blending of bind node's and bone's transformations.
| Name | Description |
|---|---|
| **OVERRIDE** = 0 | Replace bone's transformation with the transformation of the bind node. |
| **ADDITIVE** = 1 | Bind node's transformation is added to the current transformation of the bone. |

## ANIM_FRAME_USES

Frame components to be used for animation.
| Name | Description |
|---|---|
| **NONE** = 0 | No frame components are to be used. |
| **POSITION** = 1 << 0 | Only position is to be used. |
| **ROTATION** = 1 << 1 | Only rotation is to be used. |
| **SCALE** = 1 << 2 | Only scale is to be used. |
| **ALL** = POSITION \| ROTATION \| SCALE | All frame components are to be used. |
| **POSITION_AND_ROTATION** = POSITION \| ROTATION | Only position and rotation are to be used. |
| **POSITION_AND_SCALE** = POSITION \| SCALE | Only position and scale are to be used. |
| **ROTATION_AND_SCALE** = ROTATION \| SCALE | Only rotation and scale are to be used. |

## CHAIN_CONSTRAINT

| Name | Description |
|---|---|
| **NONE** = 0 | No constraints applied to the IK/LookAt chain. The chain transforms are kept as is after applying the solver. |
| **POLE_VECTOR** = 1 | The specified pole vector is applied for the IK/LookAt chain. For the IK chain, the pole vector defines the bend plane. For the LookAt chain, the pole vector defines the plane of the UP axis. This constraint is applied after applying the solver. |
| **BONE_ROTATIONS** = 2 | At every solver application step, bone rotation constraints are applied to the chain if they have been previously configured. |

## INTERPOLATION_ACCURACY

| Name | Description |
|---|---|
| **LOW** = 0 | Linear interpolation with quaternion normalization (nlerp) is applied. |
| **MEDIUM** = 1 | Linear interpolation with quaternion normalization (nlerp) is applied to rotation, but the interpolation coefficient is adjusted to be approximated to the uniform angular rotation rate. |
| **HIGH** = 2 | The slerp function is used for rotations. |

### Properties

## 🔒︎ int NumBones

The number of all bones taking part in animation.
## int NumLayers

The number of animation layers for blending. For example, when two layers are blended, bone transformations in between the layers are interpolated, and vertex positions can be calculated using the interpolated results. For more details, see the article on [Skinned Mesh](../../../objects/objects/mesh_skinned_legacy/index.md).
## 🔒︎ bool IsStopped

The stop status.
## 🔒︎ bool IsPlaying

The playback status.
## float Speed

The multiplier value for the animation playback [time](#setTime_float_void).
## float Time

The animation time, in animation frames. The time count starts from the zero frame. If the time is set to be between frames, animation is blended. If the time is set outside the animation frame range, the animation is looped.
> **Notice:** *[SetTime()](../../...md#setTime_float_void)* function corresponds to the [Play](../../../objects/objects/mesh_skinned_legacy/index.md#play) and [Stop](../../../objects/objects/mesh_skinned_legacy/index.md#stop) options in the editor. In all other cases use *[SetLayerFrame()](../../...md#setLayerFrame_int_float_int_int_float)* to set the animation.


## bool Loop

The value indicating if the animation is looped or played only once.
## bool Controlled

The value indicating if the animation is controlled by a parent ObjectMeshSkinnedLegacy.
## bool Quaternion

The value indicating if the dual-quaternion skinning mode is used. The dual-quaternion model is an accurate, computationally efficient, robust, and flexible method of representing rigid transforms and it is used in skeletal animation. See [a Wikipedia article on dual quaternions](https://en.wikipedia.org/wiki/Dual_quaternion) and [a beginners guide to dual-quaternions](http://cs.gmu.edu/~jmlien/teaching/cs451/uploads/Main/dual-quaternion.pdf) for more information.
## float UpdateDistanceLimit

The distance from the camera within which the object should be updated.
## int FPSInvisible

The update rate value when the object is not rendered at all.
## int FPSVisibleShadow

The update rate value when only object shadows are rendered.
## int FPSVisibleCamera

The update rate value when the object is rendered to the viewport.
## bool VisualizeAllBones

The value indicating if visualization for bones and their basis vectors is enabled. The visualizer can be used for debugging purposes showing positions of bones and their basis vectors for multiple meshes simultaneously.
## 🔒︎ int NumIKChains

The number of [IK chains](#ik_chains) of the skinned mesh.
## 🔒︎ Event< ObjectMeshSkinnedLegacy > EventEndBoneConstraints

The Event triggered after the bone rotation constraints are applied. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

<details>
<summary>See Example | Close</summary>

**Usage Example**


```csharp
// implement the EndBoneConstraints event handler
void endboneconstraints_handler(ObjectMeshSkinnedLegacy skinned)
{
	Log.Message("\Handling EndBoneConstraints event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endboneconstraints_event_connections = new EventConnections();

// link to this instance when subscribing for an event (subscription for various events can be linked)
objectmeshskinnedlegacy.EventEndBoneConstraints.Connect(endboneconstraints_event_connections, endboneconstraints_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
objectmeshskinnedlegacy.EventEndBoneConstraints.Connect(endboneconstraints_event_connections, (ObjectMeshSkinnedLegacy skinned) => {
		Log.Message("Handling EndBoneConstraints event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endboneconstraints_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe for the EndBoneConstraints event with a handler function
objectmeshskinnedlegacy.EventEndBoneConstraints.Connect(endboneconstraints_event_handler);

// remove subscription for the EndBoneConstraints event later by the handler function
objectmeshskinnedlegacy.EventEndBoneConstraints.Disconnect(endboneconstraints_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endboneconstraints_event_connection;

// subscribe for the EndBoneConstraints event with a lambda handler function and keeping the connection
endboneconstraints_event_connection = objectmeshskinnedlegacy.EventEndBoneConstraints.Connect((ObjectMeshSkinnedLegacy skinned) => {
		Log.Message("Handling EndBoneConstraints event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endboneconstraints_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
leave_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endboneconstraints_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndBoneConstraints events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
objectmeshskinnedlegacy.EventEndBoneConstraints.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
objectmeshskinnedlegacy.EventEndBoneConstraints.Enabled = true;
```

</details>


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(ObjectMeshSkinnedLegacy **skinned**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndBoneConstraints event handler
void endboneconstraints_event_handler(ObjectMeshSkinnedLegacy skinned)
{
	Log.Message("\Handling EndBoneConstraints event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endboneconstraints_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndBoneConstraints.Connect(endboneconstraints_event_connections, endboneconstraints_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndBoneConstraints.Connect(endboneconstraints_event_connections, (ObjectMeshSkinnedLegacy skinned) => {
		Log.Message("Handling EndBoneConstraints event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endboneconstraints_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndBoneConstraints event with a handler function
publisher.EventEndBoneConstraints.Connect(endboneconstraints_event_handler);

// remove subscription to the EndBoneConstraints event later by the handler function
publisher.EventEndBoneConstraints.Disconnect(endboneconstraints_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endboneconstraints_event_connection;

// subscribe to the EndBoneConstraints event with a lambda handler function and keeping the connection
endboneconstraints_event_connection = publisher.EventEndBoneConstraints.Connect((ObjectMeshSkinnedLegacy skinned) => {
		Log.Message("Handling EndBoneConstraints event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endboneconstraints_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endboneconstraints_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endboneconstraints_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndBoneConstraints events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndBoneConstraints.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndBoneConstraints.Enabled = true;

```

</details>

## 🔒︎ Event< ObjectMeshSkinnedLegacy > EventBeginBoneConstraints

The Event triggered before the bone rotation constraints are applied. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

<details>
<summary>See Example | Close</summary>

**Usage Example**


```csharp
// implement the BeginBoneConstraints event handler
void beginboneconstraints_handler(ObjectMeshSkinnedLegacy skinned)
{
	Log.Message("\Handling BeginBoneConstraints event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginboneconstraints_event_connections = new EventConnections();

// link to this instance when subscribing for an event (subscription for various events can be linked)
objectmeshskinnedlegacy.EventBeginBoneConstraints.Connect(beginboneconstraints_event_connections, beginboneconstraints_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
objectmeshskinnedlegacy.EventBeginBoneConstraints.Connect(beginboneconstraints_event_connections, (ObjectMeshSkinnedLegacy skinned) => {
		Log.Message("Handling BeginBoneConstraints event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginboneconstraints_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe for the BeginBoneConstraints event with a handler function
objectmeshskinnedlegacy.EventBeginBoneConstraints.Connect(beginboneconstraints_event_handler);

// remove subscription for the BeginBoneConstraints event later by the handler function
objectmeshskinnedlegacy.EventBeginBoneConstraints.Disconnect(beginboneconstraints_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginboneconstraints_event_connection;

// subscribe for the BeginBoneConstraints event with a lambda handler function and keeping the connection
beginboneconstraints_event_connection = objectmeshskinnedlegacy.EventBeginBoneConstraints.Connect((ObjectMeshSkinnedLegacy skinned) => {
		Log.Message("Handling BeginBoneConstraints event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginboneconstraints_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
leave_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginboneconstraints_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginBoneConstraints events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
objectmeshskinnedlegacy.EventBeginBoneConstraints.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
objectmeshskinnedlegacy.EventBeginBoneConstraints.Enabled = true;
```

</details>


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(ObjectMeshSkinnedLegacy **skinned**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginBoneConstraints event handler
void beginboneconstraints_event_handler(ObjectMeshSkinnedLegacy skinned)
{
	Log.Message("\Handling BeginBoneConstraints event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginboneconstraints_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginBoneConstraints.Connect(beginboneconstraints_event_connections, beginboneconstraints_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginBoneConstraints.Connect(beginboneconstraints_event_connections, (ObjectMeshSkinnedLegacy skinned) => {
		Log.Message("Handling BeginBoneConstraints event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginboneconstraints_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginBoneConstraints event with a handler function
publisher.EventBeginBoneConstraints.Connect(beginboneconstraints_event_handler);

// remove subscription to the BeginBoneConstraints event later by the handler function
publisher.EventBeginBoneConstraints.Disconnect(beginboneconstraints_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginboneconstraints_event_connection;

// subscribe to the BeginBoneConstraints event with a lambda handler function and keeping the connection
beginboneconstraints_event_connection = publisher.EventBeginBoneConstraints.Connect((ObjectMeshSkinnedLegacy skinned) => {
		Log.Message("Handling BeginBoneConstraints event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginboneconstraints_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginboneconstraints_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginboneconstraints_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginBoneConstraints events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginBoneConstraints.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginBoneConstraints.Enabled = true;

```

</details>

## 🔒︎ Event< ObjectMeshSkinnedLegacy > EventEndIKSolvers

The Event triggered after the IK solvers are applied. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

<details>
<summary>See Example | Close</summary>

**Usage Example**


```csharp
// implement the EndIKSolvers event handler
void endiksolvers_handler(ObjectMeshSkinnedLegacy skinned)
{
	Log.Message("\Handling EndIKSolvers event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endiksolvers_event_connections = new EventConnections();

// link to this instance when subscribing for an event (subscription for various events can be linked)
objectmeshskinnedlegacy.EventEndIKSolvers.Connect(endiksolvers_event_connections, endiksolvers_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
objectmeshskinnedlegacy.EventEndIKSolvers.Connect(endiksolvers_event_connections, (ObjectMeshSkinnedLegacy skinned) => {
		Log.Message("Handling EndIKSolvers event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endiksolvers_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe for the EndIKSolvers event with a handler function
objectmeshskinnedlegacy.EventEndIKSolvers.Connect(endiksolvers_event_handler);

// remove subscription for the EndIKSolvers event later by the handler function
objectmeshskinnedlegacy.EventEndIKSolvers.Disconnect(endiksolvers_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endiksolvers_event_connection;

// subscribe for the EndIKSolvers event with a lambda handler function and keeping the connection
endiksolvers_event_connection = objectmeshskinnedlegacy.EventEndIKSolvers.Connect((ObjectMeshSkinnedLegacy skinned) => {
		Log.Message("Handling EndIKSolvers event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endiksolvers_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
leave_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endiksolvers_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndIKSolvers events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
objectmeshskinnedlegacy.EventEndIKSolvers.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
objectmeshskinnedlegacy.EventEndIKSolvers.Enabled = true;
```

</details>


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(ObjectMeshSkinnedLegacy **skinned**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndIKSolvers event handler
void endiksolvers_event_handler(ObjectMeshSkinnedLegacy skinned)
{
	Log.Message("\Handling EndIKSolvers event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endiksolvers_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndIKSolvers.Connect(endiksolvers_event_connections, endiksolvers_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndIKSolvers.Connect(endiksolvers_event_connections, (ObjectMeshSkinnedLegacy skinned) => {
		Log.Message("Handling EndIKSolvers event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endiksolvers_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndIKSolvers event with a handler function
publisher.EventEndIKSolvers.Connect(endiksolvers_event_handler);

// remove subscription to the EndIKSolvers event later by the handler function
publisher.EventEndIKSolvers.Disconnect(endiksolvers_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endiksolvers_event_connection;

// subscribe to the EndIKSolvers event with a lambda handler function and keeping the connection
endiksolvers_event_connection = publisher.EventEndIKSolvers.Connect((ObjectMeshSkinnedLegacy skinned) => {
		Log.Message("Handling EndIKSolvers event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endiksolvers_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endiksolvers_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endiksolvers_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndIKSolvers events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndIKSolvers.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndIKSolvers.Enabled = true;

```

</details>

## 🔒︎ Event< ObjectMeshSkinnedLegacy > EventBeginIKSolvers

The Event triggered before the IK solvers are applied. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

<details>
<summary>See Example | Close</summary>

**Usage Example**


```csharp
// implement the BeginIKSolvers event handler
void beginiksolvers_handler(ObjectMeshSkinnedLegacy skinned)
{
	Log.Message("\Handling BeginIKSolvers event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginiksolvers_event_connections = new EventConnections();

// link to this instance when subscribing for an event (subscription for various events can be linked)
objectmeshskinnedlegacy.EventBeginIKSolvers.Connect(beginiksolvers_event_connections, beginiksolvers_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
objectmeshskinnedlegacy.EventBeginIKSolvers.Connect(beginiksolvers_event_connections, (ObjectMeshSkinnedLegacy skinned) => {
		Log.Message("Handling BeginIKSolvers event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginiksolvers_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe for the BeginIKSolvers event with a handler function
objectmeshskinnedlegacy.EventBeginIKSolvers.Connect(beginiksolvers_event_handler);

// remove subscription for the BeginIKSolvers event later by the handler function
objectmeshskinnedlegacy.EventBeginIKSolvers.Disconnect(beginiksolvers_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginiksolvers_event_connection;

// subscribe for the BeginIKSolvers event with a lambda handler function and keeping the connection
beginiksolvers_event_connection = objectmeshskinnedlegacy.EventBeginIKSolvers.Connect((ObjectMeshSkinnedLegacy skinned) => {
		Log.Message("Handling BeginIKSolvers event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginiksolvers_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
leave_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginiksolvers_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginIKSolvers events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
objectmeshskinnedlegacy.EventBeginIKSolvers.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
objectmeshskinnedlegacy.EventBeginIKSolvers.Enabled = true;
```

</details>


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(ObjectMeshSkinnedLegacy **skinned**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginIKSolvers event handler
void beginiksolvers_event_handler(ObjectMeshSkinnedLegacy skinned)
{
	Log.Message("\Handling BeginIKSolvers event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginiksolvers_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginIKSolvers.Connect(beginiksolvers_event_connections, beginiksolvers_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginIKSolvers.Connect(beginiksolvers_event_connections, (ObjectMeshSkinnedLegacy skinned) => {
		Log.Message("Handling BeginIKSolvers event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginiksolvers_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginIKSolvers event with a handler function
publisher.EventBeginIKSolvers.Connect(beginiksolvers_event_handler);

// remove subscription to the BeginIKSolvers event later by the handler function
publisher.EventBeginIKSolvers.Disconnect(beginiksolvers_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginiksolvers_event_connection;

// subscribe to the BeginIKSolvers event with a lambda handler function and keeping the connection
beginiksolvers_event_connection = publisher.EventBeginIKSolvers.Connect((ObjectMeshSkinnedLegacy skinned) => {
		Log.Message("Handling BeginIKSolvers event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginiksolvers_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginiksolvers_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginiksolvers_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginIKSolvers events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginIKSolvers.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginIKSolvers.Enabled = true;

```

</details>

## 🔒︎ Event< ObjectMeshSkinnedLegacy > EventEndLookAtSolvers

The Event triggered after the LookAtChain solvers are applied. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

<details>
<summary>See Example | Close</summary>

**Usage Example**


```csharp
// implement the EndLookAtSolvers event handler
void endlookatsolvers_handler(ObjectMeshSkinnedLegacy skinned)
{
	Log.Message("\Handling EndLookAtSolvers event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endlookatsolvers_event_connections = new EventConnections();

// link to this instance when subscribing for an event (subscription for various events can be linked)
objectmeshskinnedlegacy.EventEndLookAtSolvers.Connect(endlookatsolvers_event_connections, endlookatsolvers_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
objectmeshskinnedlegacy.EventEndLookAtSolvers.Connect(endlookatsolvers_event_connections, (ObjectMeshSkinnedLegacy skinned) => {
		Log.Message("Handling EndLookAtSolvers event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endlookatsolvers_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe for the EndLookAtSolvers event with a handler function
objectmeshskinnedlegacy.EventEndLookAtSolvers.Connect(endlookatsolvers_event_handler);

// remove subscription for the EndLookAtSolvers event later by the handler function
objectmeshskinnedlegacy.EventEndLookAtSolvers.Disconnect(endlookatsolvers_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endlookatsolvers_event_connection;

// subscribe for the EndLookAtSolvers event with a lambda handler function and keeping the connection
endlookatsolvers_event_connection = objectmeshskinnedlegacy.EventEndLookAtSolvers.Connect((ObjectMeshSkinnedLegacy skinned) => {
		Log.Message("Handling EndLookAtSolvers event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endlookatsolvers_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
leave_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endlookatsolvers_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndLookAtSolvers events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
objectmeshskinnedlegacy.EventEndLookAtSolvers.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
objectmeshskinnedlegacy.EventEndLookAtSolvers.Enabled = true;
```

</details>


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(ObjectMeshSkinnedLegacy **skinned**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndLookAtSolvers event handler
void endlookatsolvers_event_handler(ObjectMeshSkinnedLegacy skinned)
{
	Log.Message("\Handling EndLookAtSolvers event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endlookatsolvers_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndLookAtSolvers.Connect(endlookatsolvers_event_connections, endlookatsolvers_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndLookAtSolvers.Connect(endlookatsolvers_event_connections, (ObjectMeshSkinnedLegacy skinned) => {
		Log.Message("Handling EndLookAtSolvers event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endlookatsolvers_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndLookAtSolvers event with a handler function
publisher.EventEndLookAtSolvers.Connect(endlookatsolvers_event_handler);

// remove subscription to the EndLookAtSolvers event later by the handler function
publisher.EventEndLookAtSolvers.Disconnect(endlookatsolvers_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endlookatsolvers_event_connection;

// subscribe to the EndLookAtSolvers event with a lambda handler function and keeping the connection
endlookatsolvers_event_connection = publisher.EventEndLookAtSolvers.Connect((ObjectMeshSkinnedLegacy skinned) => {
		Log.Message("Handling EndLookAtSolvers event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endlookatsolvers_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endlookatsolvers_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endlookatsolvers_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndLookAtSolvers events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndLookAtSolvers.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndLookAtSolvers.Enabled = true;

```

</details>

## 🔒︎ Event< ObjectMeshSkinnedLegacy > EventBeginLookAtSolvers

The Event triggered before the LookAtChain solvers are applied. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

<details>
<summary>See Example | Close</summary>

**Usage Example**


```csharp
// implement the BeginLookAtSolvers event handler
void beginlookatsolvers_handler(ObjectMeshSkinnedLegacy skinned)
{
	Log.Message("\Handling BeginLookAtSolvers event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginlookatsolvers_event_connections = new EventConnections();

// link to this instance when subscribing for an event (subscription for various events can be linked)
objectmeshskinnedlegacy.EventBeginLookAtSolvers.Connect(beginlookatsolvers_event_connections, beginlookatsolvers_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
objectmeshskinnedlegacy.EventBeginLookAtSolvers.Connect(beginlookatsolvers_event_connections, (ObjectMeshSkinnedLegacy skinned) => {
		Log.Message("Handling BeginLookAtSolvers event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginlookatsolvers_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe for the BeginLookAtSolvers event with a handler function
objectmeshskinnedlegacy.EventBeginLookAtSolvers.Connect(beginlookatsolvers_event_handler);

// remove subscription for the BeginLookAtSolvers event later by the handler function
objectmeshskinnedlegacy.EventBeginLookAtSolvers.Disconnect(beginlookatsolvers_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginlookatsolvers_event_connection;

// subscribe for the BeginLookAtSolvers event with a lambda handler function and keeping the connection
beginlookatsolvers_event_connection = objectmeshskinnedlegacy.EventBeginLookAtSolvers.Connect((ObjectMeshSkinnedLegacy skinned) => {
		Log.Message("Handling BeginLookAtSolvers event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginlookatsolvers_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
leave_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginlookatsolvers_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginLookAtSolvers events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
objectmeshskinnedlegacy.EventBeginLookAtSolvers.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
objectmeshskinnedlegacy.EventBeginLookAtSolvers.Enabled = true;
```

</details>


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(ObjectMeshSkinnedLegacy **skinned**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginLookAtSolvers event handler
void beginlookatsolvers_event_handler(ObjectMeshSkinnedLegacy skinned)
{
	Log.Message("\Handling BeginLookAtSolvers event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginlookatsolvers_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginLookAtSolvers.Connect(beginlookatsolvers_event_connections, beginlookatsolvers_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginLookAtSolvers.Connect(beginlookatsolvers_event_connections, (ObjectMeshSkinnedLegacy skinned) => {
		Log.Message("Handling BeginLookAtSolvers event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginlookatsolvers_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginLookAtSolvers event with a handler function
publisher.EventBeginLookAtSolvers.Connect(beginlookatsolvers_event_handler);

// remove subscription to the BeginLookAtSolvers event later by the handler function
publisher.EventBeginLookAtSolvers.Disconnect(beginlookatsolvers_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginlookatsolvers_event_connection;

// subscribe to the BeginLookAtSolvers event with a lambda handler function and keeping the connection
beginlookatsolvers_event_connection = publisher.EventBeginLookAtSolvers.Connect((ObjectMeshSkinnedLegacy skinned) => {
		Log.Message("Handling BeginLookAtSolvers event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginlookatsolvers_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginlookatsolvers_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginlookatsolvers_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginLookAtSolvers events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginLookAtSolvers.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginLookAtSolvers.Enabled = true;

```

</details>

## 🔒︎ Event<float, ObjectMeshSkinnedLegacy > EventUpdate

The Event triggered when the Engine calls the object update. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

<details>
<summary>See Example | Close</summary>

**Usage Example**


```csharp
// implement the Update event handler
void update_handler(float ifps,  ObjectMeshSkinnedLegacy skinned)
{
	Log.Message("\Handling Update event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections update_event_connections = new EventConnections();

// link to this instance when subscribing for an event (subscription for various events can be linked)
objectmeshskinnedlegacy.EventUpdate.Connect(update_event_connections, update_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
objectmeshskinnedlegacy.EventUpdate.Connect(update_event_connections, (float ifps,  ObjectMeshSkinnedLegacy skinned) => {
		Log.Message("Handling Update event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
update_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe for the Update event with a handler function
objectmeshskinnedlegacy.EventUpdate.Connect(update_event_handler);

// remove subscription for the Update event later by the handler function
objectmeshskinnedlegacy.EventUpdate.Disconnect(update_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection update_event_connection;

// subscribe for the Update event with a lambda handler function and keeping the connection
update_event_connection = objectmeshskinnedlegacy.EventUpdate.Connect((float ifps,  ObjectMeshSkinnedLegacy skinned) => {
		Log.Message("Handling Update event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
update_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
leave_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
update_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Update events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
objectmeshskinnedlegacy.EventUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
objectmeshskinnedlegacy.EventUpdate.Enabled = true;
```

</details>


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(float **ifps**, ObjectMeshSkinnedLegacy **skinned**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Update event handler
void update_event_handler(float ifps,  ObjectMeshSkinnedLegacy skinned)
{
	Log.Message("\Handling Update event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections update_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventUpdate.Connect(update_event_connections, update_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventUpdate.Connect(update_event_connections, (float ifps,  ObjectMeshSkinnedLegacy skinned) => {
		Log.Message("Handling Update event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
update_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Update event with a handler function
publisher.EventUpdate.Connect(update_event_handler);

// remove subscription to the Update event later by the handler function
publisher.EventUpdate.Disconnect(update_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection update_event_connection;

// subscribe to the Update event with a lambda handler function and keeping the connection
update_event_connection = publisher.EventUpdate.Connect((float ifps,  ObjectMeshSkinnedLegacy skinned) => {
		Log.Message("Handling Update event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
update_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
update_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
update_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Update events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventUpdate.Enabled = true;

```

</details>

## 🔒︎ int NumBoneConstraints

The total number of bone rotation constraints.
## ObjectMeshSkinnedLegacy.INTERPOLATION_ACCURACY InterpolationAccuracy

The interpolation mode for the bone rotations. The value is set to HIGH by default.
## string AnimPath

The path to a file containing the specified animation.
## bool MeshProceduralMode

The value indicating if the [procedural mesh usage mode](#procedural_modification) is enabled for the object. With the procedural mode enabled, geometry of the **ObjectMeshSkinnedLegacy** can be modified via *[ApplyMeshProcedural()](../../...md#applyMeshProcedural_ConstMeshSkinned_int)*. Disabling the procedural mode restores the object's initial geometry, removing any changes applied. For skinned meshes, procedural geometry editing is done only through the direct main-thread workflow, unlike static meshes that can use asynchronous generation or [other update strategies](../../../api/library/objects/class.objectmeshstatic_cs.md#procedural_workflow).
## 🔒︎ bool IsLoaded

The value indicating if the mesh is loaded (it is either a procedural one or has been loaded via the [setMeshPath()](#setMeshPath_cstr_void) method).
## string MeshPath

The path to the mesh file. If the *Procedural* flag is enabled for the object, the mesh won't be loaded.
### Members

---

## ObjectMeshSkinnedLegacy ( string path )

ObjectMeshSkinnedLegacy constructor.
### Arguments

- *string* **path** - Path to the skinned mesh file.

## ObjectMeshSkinnedLegacy ( )

ObjectMeshSkinnedLegacy constructor.
## int GetBoneChild ( int bone , int child )

Returns the number of a child of the given bone.
### Arguments

- *int* **bone** - Bone number.
- *int* **child** - Child number.

### Return value

Number of the child in the collection of all bones.
## void SetBoneTransformWithChildren ( int bone , mat4 transform )

Sets transformation for the bone and all of its children (without considering node transformations).
> **Notice:** Bones can be scaled only uniformly.


### Arguments

- *int* **bone** - Bone number.
- *mat4* **transform** - Transformation matrix.

## string GetBoneName ( int bone )

Returns the name of the given bone.
### Arguments

- *int* **bone** - Bone number.

### Return value

Bone name.
## int GetBoneParent ( int bone )

Returns the number of the parent bone for a given one.
### Arguments

- *int* **bone** - Number of the bone, for which the parent will be returned.

### Return value

Parent bone number, if the parent exists; otherwise, -1.
## void SetBoneTransform ( int bone , mat4 transform )

Sets a transformation matrix for the given bone (without considering node transformations).
> **Notice:** Bones can be scaled only uniformly.


### Arguments

- *int* **bone** - Bone number.
- *mat4* **transform** - Transformation matrix.

## mat4 GetBoneTransform ( int bone )

Returns a transformation matrix of the given bone relatively to the parent object (not considering transformations of the Mesh Skinned node itself).
### Arguments

- *int* **bone** - Bone number.

### Return value

Transformation matrix.
## void SetBoneTransforms ( int[] bones , mat4[] transforms , int num_bones )

Sets a transformation matrix for given bones.
### Arguments

- *int[]* **bones** - Bone numbers.
- *mat4[]* **transforms** - Transformation matrices.
- *int* **num_bones** - Number of bones.

## int GetCIndex ( int num , int surface )

Returns the [coordinate index](../../../api/library/rendering/class.mesh_cs.md#cindices) for the given vertex of the given surface.
### Arguments

- *int* **num** - Vertex number in the range from 0 to the total number of coordinate indices for the given surface. > **Notice:** To get the total number of coordinate indices for the given surface, use the [getNumCIndices()](#getNumCIndices_int_int) method.
- *int* **surface** - Mesh surface number.

### Return value

Coordinate index.
## vec4 GetColor ( int num , int surface )

Returns the color of the given [triangle vertex](../../../api/library/rendering/class.mesh_cs.md#tvertex) of the given surface.
### Arguments

- *int* **num** - [Triangle vertex](../../../api/library/rendering/class.mesh_cs.md#tvertex) number in the range from 0 to the total number of vertex color entries of the given surface. > **Notice:** To get the total number of vertex color entries for the surface, call the [*getNumColors()*](#getNumColors_int_int) method.
- *int* **surface** - Mesh surface number.

### Return value

Vertex color.
## void SetLayer ( int layer , bool enabled , float weight )

Enables or disables the given animation layer and sets the value of the weight parameter.
### Arguments

- *int* **layer** - Animation layer number.
- *bool* **enabled** - Enable flag. true to enable the layer, false to disable it.
- *float* **weight** - Animation layer weight.

## void SetLayerEnabled ( int layer , bool enabled )

Enables or disables a given animation layer.
### Arguments

- *int* **layer** - Animation layer number.
- *bool* **enabled** - true to enable the animation layer, false to disable it.

## bool IsLayerEnabled ( int layer )

Returns a value indicating if a given animation layer is enabled.
### Arguments

- *int* **layer** - Animation layer number.

### Return value

true if the layer is disabled; otherwise, false.
## void SetLayerWeight ( int layer , float weight )

Sets a weight for the animation layer.
### Arguments

- *int* **layer** - Animation layer number.
- *float* **weight** - Animation layer weight.

## float GetLayerWeight ( int layer )

Returns the weight of the animation layer.
### Arguments

- *int* **layer** - Animation layer number.

### Return value

Weight of the animation layer.
## bool GetMesh ( MeshSkinned mesh )

Copies the current mesh into the destination mesh.
```csharp
// a skinned mesh from which geometry will be obtained
ObjectMeshSkinnedLegacy skinnedMesh = new ObjectMeshSkinnedLegacy("skinned.mesh");
// create a new mesh
MeshSkinned mesh = new MeshSkinned();
// copy geometry to the created mesh
if (skinnedMesh.GetMesh(mesh)) {
	// do something with the obtained mesh
}
else {
	Log.Error("Failed to copy a mesh\n");
}

```


### Arguments

- *[MeshSkinned](../../../api/library/rendering/class.meshskinned_cs.md)* **mesh** - Destination mesh to copy into.

### Return value

**1** if the mesh is copied successfully; otherwise, **0**.
## bool GetMeshSurface ( Mesh mesh , int surface , int target = -1 )

Copies the specified mesh surface to the destination mesh.
### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* **mesh** - Destination [Mesh](../../../api/library/rendering/class.mesh_cs.md) to copy the surface to.
- *int* **surface** - Number of the mesh surface to be copied.
- *int* **target** - Number of the surface morph target to be copied. The default value is -1 (all morph targets).

### Return value

Number of the new added mesh surface.
## vec3 GetNormal ( int num , int surface , int target = 0 )

Returns the normal for the given [triangle vertex](../../../api/library/rendering/class.mesh_cs.md#tvertex) of the given surface target.
### Arguments

- *int* **num** - [Triangle vertex](../../../api/library/rendering/class.mesh_cs.md#tvertex) number in the range from 0 to the total number of vertex tangent entries of the given surface target. > **Notice:** Vertex normals are calculated using vertex tangents. To get the total number of vertex tangent entries for the surface target, call the [*getNumTangents()*](#getNumTangents_int_int) method.
- *int* **surface** - Mesh surface number.
- *int* **target** - Surface target number. The default value is 0.

### Return value

Vertex normal.
## int GetNumBoneChildren ( int bone )

Returns the number of children for the specified bone.
### Arguments

- *int* **bone** - Bone number.

### Return value

Number of child bones.
## int GetNumCIndices ( int surface )

Returns the number of [coordinate indices](../../../api/library/rendering/class.mesh_cs.md#cindices) for the given mesh surface.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Number of coordinate indices.
## int GetNumColors ( int surface )

Returns the total number of vertex color entries for the given surface.
> **Notice:** Colors are specified for [triangle vertices](../../../api/library/rendering/class.mesh_cs.md#tvertex).


### Arguments

- *int* **surface** - Surface number.

### Return value

Number of vertex color entries.
## int GetNumSurfaceTargets ( int surface )

Returns the number of surface morph targets for the given mesh surface.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Number of surface morph targets.
## int GetNumTangents ( int surface )

Returns the number of vertex tangent entries of the given mesh surface.
> **Notice:** Tangents are specified for [triangle vertices](../../../api/library/rendering/class.mesh_cs.md#tvertex).


### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Number of surface tangent vectors.
## int GetNumTexCoords0 ( int surface )

Returns the number of the first UV map texture coordinates for the given mesh surface.
> **Notice:** First UV map texture coordinates are specified for [triangle vertices](../../../api/library/rendering/class.mesh_cs.md#tvertex).


### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Number of the first UV map texture coordinates.
## int GetNumTexCoords1 ( int surface )

Returns the number of the second UV map texture coordinates for the given mesh surface.
> **Notice:** Second UV map texture coordinates are specified for [triangle vertices](../../../api/library/rendering/class.mesh_cs.md#tvertex).


### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Number of the second UV map texture coordinates.
## int GetNumTIndices ( int surface )

Returns the number of triangle indices for the given mesh surface.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Number of [triangle indices](../../../api/library/rendering/class.mesh_cs.md#tindices).
## int GetNumVertex ( int surface )

Returns the number of [coordinate vertices](../../../api/library/rendering/class.mesh_cs.md#cvertex) for the given mesh surface.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Number of the surface vertices.
## vec3 GetSkinnedNormal ( int num , int index , int surface )

Returns the skinned normal for the given [triangle vertex](../../../api/library/rendering/class.mesh_cs.md#tvertex).
> **Notice:** A skinned normal is a recalculated normal for bones and morph targets used in skinning.


### Arguments

- *int* **num** - [Triangle vertex](../../../api/library/rendering/class.mesh_cs.md#tvertex) number in the range from 0 to the total number of vertex tangent entries of the given surface target. > **Notice:** Vertex normals are calculated using vertex tangents. To get the total number of vertex tangent entries for the surface target, call the [*getNumTangents()*](#getNumTangents_int_int) method.
- *int* **index** - [Coordinate index](../../../api/library/rendering/class.mesh_cs.md#cindices) of the vertex. > **Notice:** if -1 is passed, the coordinate index will be obtained for the first vertex having its [triangle index](../../../api/library/rendering/class.mesh_cs.md#tindices) equal to the specified [triangle vertex](../../../api/library/rendering/class.mesh_cs.md#tvertex) number.
- *int* **surface** - Mesh surface number.

### Return value

Skinned normal.
## quat GetSkinnedTangent ( int num , int index , int surface )

Returns the skinned tangent vector for the given [triangle vertex](../../../api/library/rendering/class.mesh_cs.md#tvertex).
> **Notice:** A skinned tangent vector is a recalculated tangent vector for bones and morph targets used in skinning.


### Arguments

- *int* **num** - [Triangle vertex](../../../api/library/rendering/class.mesh_cs.md#tvertex) number in the range from 0 to the total number of vertex tangent entries of the given surface target. > **Notice:** To get the total number of vertex tangent entries for the surface target, call the [*getNumTangents()*](#getNumTangents_int_int) method.
- *int* **index** - [Coordinate index](../../../api/library/rendering/class.mesh_cs.md#cindices) of the vertex. > **Notice:** if -1 is passed, the coordinate index will be obtained for the first vertex having its [triangle index](../../../api/library/rendering/class.mesh_cs.md#tindices) equal to the specified [triangle vertex](../../../api/library/rendering/class.mesh_cs.md#tvertex) number.
- *int* **surface** - Mesh surface number.

### Return value

Skinned tangent.
## vec3 GetSkinnedVertex ( int num , int surface )

Returns skinned coordinates of the given [coordinate vertex](../../../api/library/rendering/class.mesh_cs.md#cvertex).
> **Notice:** A skinned vertex is a recalculated vertex for bones and morph targets used in skinning.


### Arguments

- *int* **num** - [Coordinate vertex](../../../api/library/rendering/class.mesh_cs.md#cvertex) number in the range from 0 to the total number of coordinate vertices for the given surface. > **Notice:** To get the total number of coordinate vertices for the given surface, use the [getNumVertex()](#getNumVertex_int_int) method.
- *int* **surface** - Mesh surface number.

### Return value

Vertex coordinates.
## bool IsNeedUpdate ( )

Returns a value indicating if the *ObjectMeshSkinnedLegacy* needs to be updated (e.g. after adding new animations).
### Return value

true if the skinned mesh needs to be updated; otherwise, false.
## string GetSurfaceTargetName ( int surface , int target )

Returns the name of the morph target for the given mesh surface.
### Arguments

- *int* **surface** - Mesh surface number.
- *int* **target** - Morph target number.

### Return value

Morph target name.
## quat GetTangent ( int num , int surface , int target = 0 )

Returns the tangent for the given [triangle vertex](../../../api/library/rendering/class.mesh_cs.md#tvertex) of the given surface target.
### Arguments

- *int* **num** - [Triangle vertex](../../../api/library/rendering/class.mesh_cs.md#tvertex) number in the range from 0 to the total number of vertex tangent entries of the given surface. > **Notice:** To get the total number of vertex tangent entries for the surface, call the [getNumTangents()](#getNumTangents_int_int) method.
- *int* **surface** - Mesh surface number.
- *int* **target** - Surface target number. The default value is 0.

### Return value

Vertex tangent.
## vec2 GetTexCoord0 ( int num , int surface )

Returns first UV map texture coordinates for the given [triangle vertex](../../../api/library/rendering/class.mesh_cs.md#tvertex) of the given surface.
### Arguments

- *int* **num** - [Triangle vertex](../../../api/library/rendering/class.mesh_cs.md#tvertex) number in the range from 0 to the total number of first UV map texture coordinate entries of the given surface. > **Notice:** To get the total number of first UV map texture coordinate entries for the surface, call the [getNumTexCoords0()](#getNumTexCoords0_int_int) method.
- *int* **surface** - Mesh surface number.

### Return value

First UV map texture coordinates.
## vec2 GetTexCoord1 ( int num , int surface )

Returns second UV map texture coordinates for the given [triangle vertex](../../../api/library/rendering/class.mesh_cs.md#tvertex) of the given surface.
### Arguments

- *int* **num** - [Triangle vertex](../../../api/library/rendering/class.mesh_cs.md#tvertex) number in the range from 0 to the total number of second UV map texture coordinate entries of the given surface. > **Notice:** To get the total number of second UV map texture coordinate entries for the surface, call the [getNumTexCoords1()](#getNumTexCoords1_int_int) method.
- *int* **surface** - Mesh surface number.

### Return value

Second UV map texture coordinates.
## int GetTIndex ( int num , int surface )

Returns the [triangle index](../../../api/library/rendering/class.mesh_cs.md#tindices) for the given surface by using the index number.
### Arguments

- *int* **num** - Vertex number in the range from 0 to the total number of triangle indices for the given surface. > **Notice:** To get the total number of triangle indices for the given surface, use the [getNumTIndices()](#getNumTIndices_int_int) method.
- *int* **surface** - Mesh surface number.

### Return value

Triangle index.
## vec3 GetVertex ( int num , int surface , int target = 0 )

Returns coordinates of the given [coordinate vertex](../../../api/library/rendering/class.mesh_cs.md#cvertex) of the given surface target.
### Arguments

- *int* **num** - [Coordinate vertex](../../../api/library/rendering/class.mesh_cs.md#cvertex) number in the range from 0 to the total number of coordinate vertices for the given surface. > **Notice:** To get the total number of coordinate vertices for the given surface, use the [getNumCVertex()](../../../api/library/rendering/class.mesh_cs.md#getNumCVertex_int_int) method.
- *int* **surface** - Mesh surface number.
- *int* **target** - Surface target number. The default value is 0.

### Return value

Vertex coordinates.
## void SetBoneWorldTransformWithChildren ( int bone , mat4 transform )

Sets the transformation for the given bone and all of its children in the world coordinate space (considering node transformations).
> **Notice:** Bones can be scaled only uniformly.


### Arguments

- *int* **bone** - Bone number.
- *mat4* **transform** - Transformation matrix in the world space.

## void SetBoneWorldTransform ( int bone , mat4 transform )

Sets the transformation for the given bone in the world coordinate space.
> **Notice:** Bones can be scaled only uniformly.


### Arguments

- *int* **bone** - Bone number.
- *mat4* **transform** - Transformation matrix in the world space.

## mat4 GetBoneWorldTransform ( int bone )

Returns the current transformation matrix applied to the bone in the world coordinate space (considering node transformations).
### Arguments

- *int* **bone** - Bone number.

### Return value

Transformation matrix in the world space.
## void GetObjectPose ( SkeletonPoseMatrix out_pose )

Writes the current object-space bone transforms (the result of blending all animation layers) into the specified [SkeletonPoseMatrix](../../../api/library/animations/skeletal/class.skeletonposematrix_cs.md).
### Arguments

- *[SkeletonPoseMatrix](../../../api/library/animations/skeletal/class.skeletonposematrix_cs.md)* **out_pose** - Output pose to receive the object-space bone transforms.

## int AddLayer ( )

Appends a new animation layer to the current mesh.
### Return value

Number of the new added animation layer.
## void ClearLayer ( int layer )

Clears the given animation layer.
### Arguments

- *int* **layer** - Animation layer number.

## void CopyLayer ( int dest , int src )


Copies source layer bones transformations to the destination layer. The copying conditions are the following:


- If the destination layer has more bones than the source one, it will keep its former transformations.
- If the source layer has more bones than destination one, those bones will be added to the destination layer.


### Arguments

- *int* **dest** - Number of the destination layer in the range from 0 to the total number of animation layers. > **Notice:** To get the total number of animation layers, use the [getNumLayers()](#getNumLayers_int) method.
- *int* **src** - Number of the source layer in range from 0 to the total number of animation layers. > **Notice:** To get the total number of animation layers, use the [getNumLayers()](#getNumLayers_int) method.

## int FindBone ( string name )

Searches for a bone with a given name.
### Arguments

- *string* **name** - Bone name.

### Return value

Bone number if found; otherwise, -1.
## int FindSurfaceTarget ( int surface , string name )

Searches for a surface morph target with a given name.
### Arguments

- *int* **surface** - Mesh surface number.
- *string* **name** - Name of the morph target.

### Return value

Number of the morph target, if exists; otherwise, **-1**.
## void ImportLayer ( int layer )

Copies the current bone state to the given animation layer.
### Arguments

- *int* **layer** - Animation layer number.

## void InverseLayer ( int dest , int src )

Copies inverse transformations of bones from the source layer to the destination layer.
> **Notice:** Destination layer is not cleared before transformations are written to it.


### Arguments

- *int* **dest** - Number of the destination layer in the range from 0 to the total number of animation layers. > **Notice:** To get the total number of animation layers, use the [getNumLayers()](#getNumLayers_int) method.
- *int* **src** - Number of the source layer in the range from 0 to the total number of animation layers. > **Notice:** To get the total number of animation layers, use the [getNumLayers()](#getNumLayers_int) method.

## void LerpLayer ( int dest , int layer0 , int layer1 , float weight )

Copies interpolated bone transformations from two source layers to a destination layer.
> **Notice:** If there is no bone in one of the source layers, the bone transformation from another one will be copied to the destination layer without interpolation.


### Arguments

- *int* **dest** - Number of the destination layer in the range from 0 to the total number of animation layers. > **Notice:** To get the total number of animation layers, use the [getNumLayers()](#getNumLayers_int) method.
- *int* **layer0** - Number of the first source layer in the range from 0 to the total number of animation layers. > **Notice:** To get the total number of animation layers, use the [getNumLayers()](#getNumLayers_int) method.
- *int* **layer1** - Number of the second source layer in range from 0 to the total number of animation layers. > **Notice:** To get the total number of animation layers, use the [getNumLayers()](#getNumLayers_int) method.
- *float* **weight** - Interpolation weight.

## void LerpLayerByMask ( int dest , int layer0 , int layer1 , int mask_index , float weight )

Copies interpolated bone transformations from two source layers to a destination layer, using the specified bone mask (by index) to control per-bone blending weights.
### Arguments

- *int* **dest** - Number of the destination layer.
- *int* **layer0** - Number of the first source layer.
- *int* **layer1** - Number of the second source layer.
- *int* **mask_index** - Index of the bone mask to use for per-bone blending weights.
- *float* **weight** - Interpolation weight.

## void LerpLayerByMask ( int dest , int layer0 , int layer1 , string mask_name , float weight )

Copies interpolated bone transformations from two source layers to a destination layer, using the specified bone mask (by name) to control per-bone blending weights.
### Arguments

- *int* **dest** - Number of the destination layer.
- *int* **layer0** - Number of the first source layer.
- *int* **layer1** - Number of the second source layer.
- *string* **mask_name** - Name of the bone mask to use for per-bone blending weights.
- *float* **weight** - Interpolation weight.

## void MulLayer ( int dest , int layer0 , int layer1 , float weight = 1.0f )

Copies multiplied bone transformations from two source layers to the destination layer.
### Arguments

- *int* **dest** - Number of the destination layer in the range from 0 to the total number of animation layers. > **Notice:** To get the total number of animation layers, use the [getNumLayers()](#getNumLayers_int) method.
- *int* **layer0** - Number of the first source layer in the range from 0 to the total number of animation layers. > **Notice:** To get the total number of animation layers, use the [getNumLayers()](#getNumLayers_int) method.
- *int* **layer1** - Number of the second source layer in the range from 0 to the total number of animation layers. > **Notice:** To get the total number of animation layers, use the [getNumLayers()](#getNumLayers_int) method.
- *float* **weight** - Interpolation weight.

## void Play ( )

Continues playback of the animation, if it was paused, or starts playback if it was stopped.
## void RemoveLayer ( int layer )

Removes an animation layer.
### Arguments

- *int* **layer** - Layer number in the range from 0 to the total number of animation layers. > **Notice:** To get the total number of animation layers, use the [getNumLayers()](#getNumLayers_int) method.

## void Stop ( )

Stops animation playback. This function saves the playback position so that playing of the animation can be resumed from the same point.
## void GetBlendingLayersPose ( SkeletonPoseDecomposed pose )

Writes the final blended pose (the result of blending all enabled animation layers according to their weights) into the specified [SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_cs.md). This provides the decomposed (position, rotation, scale) representation of the blended animation state.
### Arguments

- *[SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_cs.md)* **pose** - Output pose to receive the blended result.

## static int type ( )

Returns the type of the node.
### Return value

[Node](../../../api/library/nodes/class.node_cs.md) type identifier.
## void UpdateSkinned ( )

Forces update of all bone transformations.
## void SetBindNode ( int bone , Node node )

Sets a new node whose transformation is to be used to control the transformation of the bone with the specified number.
### Arguments

- *int* **bone** - Number of the bone to be controlled by the specified node, in the range from 0 to the [total number of bones](#getNumBones_int).
- *[Node](../../../api/library/nodes/class.node_cs.md)* **node** - Node whose transformation is used to control the transformation of the bone.

## void RemoveBindNodeByBone ( int bone )

Removes the assigned bind node from the bone with the specified number.
### Arguments

- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).

## void RemoveBindNodeByNode ( Node node )

Removes the specified bind node.
### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)* **node** - Bind node to be removed.

## void RemoveAllBindNode ( )

Removes all assigned bind nodes.
## Node GetBindNode ( int bone )

Returns the bind node currently assigned to the bone with the specified number.
### Arguments

- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).

### Return value

Node whose transformation is used to control the transformation of the bone if it is assigned; otherwise - nullptr.
## void SetBindNodeSpace ( int bone , ObjectMeshSkinnedLegacy.NODE_SPACE space )

Sets a new value indicating which transformation of the bind node (*World* or *Local*) is to be used to override the transformation of the specified bone.
### Arguments

- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).
- *[ObjectMeshSkinnedLegacy.NODE_SPACE](../../../api/library/objects/class.objectmeshskinnedlegacy_cs.md#NODE_SPACE)* **space** - Type of transformation of the bind node to be used to override the transformation of the specified bone, one of the [*NODE_SPACE**](#NODE_SPACE_LOCAL) values.

## ObjectMeshSkinnedLegacy.NODE_SPACE GetBindNodeSpace ( int bone )

Returns the current value indicating which transformation of the bind node (*World* or *Local*) is to be used to override the transformation of the specified bone.
### Arguments

- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).

### Return value

Type of transformation of the bind node to be used to override the transformation of the specified bone, one of the [*NODE_SPACE**](#NODE_SPACE_LOCAL) values.
## void SetBindBoneSpace ( int bone , ObjectMeshSkinnedLegacy.BONE_SPACE space )

Sets a value indicating which transformation of the specified bone is to be overridden by the bind node's transformation.
### Arguments

- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).
- *[ObjectMeshSkinnedLegacy.BONE_SPACE](../../../api/library/objects/class.objectmeshskinnedlegacy_cs.md#BONE_SPACE)* **space** - Type of transformation of the specified bone to be overridden by the bind node's transformation, one of the [*BONE_SPACE**](#BONE_SPACE_LOCAL) values.

## ObjectMeshSkinnedLegacy.BONE_SPACE GetBindBoneSpace ( int bone )

Returns the current value indicating which transformation of the specified bone is to be overridden by the bind node's transformation.
### Arguments

- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).

### Return value

Current type of transformation of the specified bone overridden by the bind node's transformation, one of the [*BONE_SPACE**](#BONE_SPACE_LOCAL) values.
## void SetBindMode ( int bone , ObjectMeshSkinnedLegacy.BIND_MODE mode )

Sets a new type of blending of bind node's and bone's transformations.
### Arguments

- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).
- *[ObjectMeshSkinnedLegacy.BIND_MODE](../../../api/library/objects/class.objectmeshskinnedlegacy_cs.md#BIND_MODE)* **mode** - New type of blending of bind node's and bone's transformations:

  - **OVERRIDE** - replace bone's transformation with the transformation of the node.
  - **ADDITIVE** - node's transformation is added to the current transformation of the bone.

## ObjectMeshSkinnedLegacy.BIND_MODE GetBindMode ( int bone )

Returns the current type of blending of bind node's and bone's transformations.
### Arguments

- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).

### Return value

Current type of blending of bind node's and bone's transformations:
- **OVERRIDE** - replace bone's transformation with the transformation of the node.
- **ADDITIVE** - node's transformation is added to the current transformation of the bone.


## void SetBindNodeOffset ( int bone , mat4 offset )

Sets a new transformation matrix to be applied to the node's transformation before applying it to bone's transformation. This parameter serves for the purpose of additional correction of the node's transform for the bone's basis.
### Arguments

- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).
- *mat4* **offset** - Transformation matrix applied to the node's transformation before applying it to bone's transformation.

## mat4 GetBindNodeOffset ( int bone )

Returns the current transformation matrix which is applied to the node's transformation before applying it to bone's transformation. This parameter serves for the purpose of additional correction of the node's transform for the bone's basis.
### Arguments

- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).

### Return value

Transformation matrix currently applied to the node's transformation before applying it to bone's transformation.
## void AddVisualizeBone ( int bone )

Adds a bone with the specified number to the list of the bones for which the basis vectors are to be visualized.
### Arguments

- *int* **bone** - Number of the bone to be added to the visualizer, in the range from 0 to the [total number of bones](#getNumBones_int).

## void RemoveVisualizeBone ( int bone )

Removes a bone with the specified number from the list of the bones for which the basis vectors are to be visualized.
### Arguments

- *int* **bone** - Number of the bone to be removed from the visualizer, in the range from 0 to the [total number of bones](#getNumBones_int).

## void ClearVisualizeBones ( )

Clears the list of the bones for which the basis vectors are to be visualized.
## void AddVisualizeIKChain ( int chain_id )

Adds an [IK chain](#ik_chains) with the specified ID to the list of chains for which the basis vectors are to be visualized.
### Arguments

- *int* **chain_id** - IK chain ID.

## void RemoveVisualizeIKChain ( int chain_id )

Removes the [IK chain](#ik_chains) with the specified ID from the list of chains for which the basis vectors are to be visualized.
### Arguments

- *int* **chain_id** - IK chain ID.

## void ClearVisualizeIKChain ( )

Clears the list of [IK chains](#ik_chains) for which the basis vectors are to be visualized.
## int AddIKChain ( )

Adds a new [IK chain](#ik_chains) to the skinned mesh.
### Return value

ID of the added IK chain.
## void RemoveIKChain ( int chain_id )

Removes the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *int* **chain_id** - IK chain ID.

## void SetIKChainEnabled ( bool enabled , int chain_id )

Sets a value indicating if the [IK chain](#ik_chains) with the specified ID is enabled.
### Arguments

- *bool* **enabled** - Set **true** to enable IK chain with the specified ID, or **false** - to disable it.
- *int* **chain_id** - IK chain ID.

## bool IsIKChainEnabled ( int chain_id )

Returns a value indicating if the [IK chain](#ik_chains) with the specified ID is enabled.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

**true** if the IK chain with the specified ID is enabled; otherwise, **false**.
## void SetIKChainWeight ( float weight , int chain_id )

Sets a new weight for the [IK chain](#ik_chains) with the specified ID. Weight value defines the impact of the target position on the last joint of the chain.
### Arguments

- *float* **weight** - New weight value to be set in the [0.0f, 1.0f] range. *Higher* values increase the impact.
- *int* **chain_id** - IK chain ID.

## float GetIKChainWeight ( int chain_id )

Returns the current weight for the [IK chain](#ik_chains) with the specified ID. Weight value defines the impact of the target position on the last joint of the chain.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

Current weight value in the [0.0f, 1.0f] range. *Higher* values increase the impact.
## int AddIKChainBone ( int bone , int chain_id )

Adds a bone with the specified number to the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *int* **bone** - Bone number.
- *int* **chain_id** - IK chain ID.

### Return value

Index of the last added bone in the chain.
## int GetIKChainNumBones ( int chain_id )

Returns the number of bones in the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

Number of bones in the IK chain with the specified ID.
## void RemoveIKChainBone ( int bone_num , int chain_id )

Removes the bone with the specified number from the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *int* **bone_num** - Bone number.
- *int* **chain_id** - IK chain ID.

## int GetIKChainBone ( int bone_num , int chain_id )

Returns the index of the bone with the specified number (within the chain) from the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *int* **bone_num** - Bone number.
- *int* **chain_id** - IK chain ID.

### Return value

Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).
## void SetIKChainTargetPosition ( vec3 position , int chain_id )

Sets new local coordinates of the target position of the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *vec3* **position** - New local coordinates of the target position to be set for the IK chain with the specified ID.
- *int* **chain_id** - IK chain ID.

## vec3 GetIKChainTargetPosition ( int chain_id )

Returns the current local coordinates of the target position of the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

Local coordinates of the target position of the IK chain with the specified ID.
## void SetIKChainTargetWorldPosition ( vec3 position , int chain_id )

Sets new world coordinates of the target position of the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *vec3* **position** - New world coordinates of the target position to be set for the IK chain with the specified ID.
- *int* **chain_id** - IK chain ID.

## vec3 GetIKChainTargetWorldPosition ( int chain_id )

Returns the current world coordinates of the target position of the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

World coordinates of the target position of the IK chain with the specified ID.
## void SetIKChainPolePosition ( vec3 position , int chain_id )

Sets a new pole position (in local coordinates) for the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *vec3* **position** - New pole position (in local coordinates) to be set for the IK chain.
- *int* **chain_id** - IK chain ID.

## vec3 GetIKChainPolePosition ( int chain_id )

Returns the current pole position (in local coordinates) for the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

Pole position (in local coordinates) for the IK chain.
## void SetIKChainPoleWorldPosition ( vec3 position , int chain_id )

Sets a new pole position (in world coordinates) for the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *vec3* **position** - New pole position (in world coordinates) to be set for the IK chain.
- *int* **chain_id** - IK chain ID.

## vec3 GetIKChainPoleWorldPosition ( int chain_id )

Returns the current pole position (in world coordinates) for the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

Pole position (in world coordinates) for the IK chain.
## void SetIKChainUseEffectorRotation ( bool use , int chain_id )

Sets a value indicating if the effector rotation is to be used for the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *bool* **use** - **true** to use effector rotation for the IK chain with the specified ID; **false** - not to use.
- *int* **chain_id** - IK chain ID.

## bool IsIKChainUseEffectorRotation ( int chain_id )

Returns a value indicating if the effector rotation is to be used for the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

**true** if the effector rotation is to be used for the IK chain with the specified ID; otherwise, **false**.
## void SetIKChainEffectorRotation ( quat rotation , int chain_id )

Sets the rotation of the end-effector (in local coordinates) of the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *quat* **rotation** - Quaternion that defines rotation (local coordinates) of the end-effector of the chain.
- *int* **chain_id** - IK chain ID.

## quat GetIKChainEffectorRotation ( int chain_id )

Returns the current rotation (in local coordinates) of the end-effector of the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

Quaternion that defines rotation (local coordinates) of the end-effector of the chain.
## void SetIKChainEffectorWorldRotation ( quat rotation , int chain_id )

Sets the rotation of the end-effector (in world coordinates) of the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *quat* **rotation** - Quaternion that defines rotation (world coordinates) of the end-effector of the chain.
- *int* **chain_id** - IK chain ID.

## quat GetIKChainEffectorWorldRotation ( int chain_id )

Returns the current rotation (in world coordinates) of the end-effector of the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

Quaternion that defines rotation (world coordinates) of the end-effector of the chain.
## void SetIKChainNumIterations ( int num , int chain_id )

Sets the number of iterations to be used for solving the [IK chain](#ik_chains) with the specified ID (number of times the algorithm runs).
### Arguments

- *int* **num** - Number of iterations to be used for solving the IK chain with the specified ID.
- *int* **chain_id** - IK chain ID.

## int GetIKChainNumIterations ( int chain_id )

Returns the number of iterations used for solving the [IK chain](#ik_chains) with the specified ID (number of times the algorithm runs).
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

Current number of iterations for the IK chain with the specified ID.
## void SetIKChainTolerance ( float tolerance , int chain_id )

Sets a new tolerance value to be used for the [IK chain](#ik_chains) with the specified ID. This value sets a threshold where the target is considered to have reached its destination position, and when the IK Solver stops iterating.
### Arguments

- *float* **tolerance** - Tolerance value to be set for the IK chain.
- *int* **chain_id** - IK chain ID.

## float GetIKChainTolerance ( int chain_id )

Returns the current tolerance value to be used for the [IK chain](#ik_chains) with the specified ID. This value sets a threshold where the target is considered to have reached its destination position, and when the IK Solver stops iterating.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

Current tolerance value for the IK chain.
## void CopyBoneTransforms ( ObjectMeshSkinnedLegacy src )

Copies all bone transformations from the specified source skinned mesh.
### Arguments

- *[ObjectMeshSkinnedLegacy](../../../api/library/objects/class.objectmeshskinnedlegacy_cs.md)* **src** - Source skinned mesh from which bone transforms are to be copied.

## bool ApplyMeshProcedural ( MeshSkinned mesh )

**[ Main Thread ]** Replaces the object's current geometry with the provided mesh and **uploads it to VRAM**. Can only be called if [procedural mode](#procedural_modification) is enabled via *[MeshProceduralMode](../../...md#setMeshProceduralMode_int_void)*. If the source mesh contains compatible elements (e.g., bones, surfaces, skinning data) matching the original, then animations, morph targets, and other behaviors will continue to function without interruption. Otherwise, the mesh will remain static, with no animation or morphing applied.
> **Notice:** The procedural mesh remains in memory and will not be unloaded automatically.


### Arguments

- *[MeshSkinned](../../../api/library/rendering/class.meshskinned_cs.md)* **mesh** - Source mesh.

### Return value

true if the information from the mesh is successfully copied into the procedural mesh, otherwise false.
## void SetSurfaceTargetEnabled ( int surface , int target , bool enabled )

Toggles the use of the morph target for the specified surface.
### Arguments

- *int* **surface** - Number of the surface, to which the morph target is to be appended.
- *int* **target** - Number of the morph target to be used.
- *bool* **enabled** - true to enable the use of the morph target for the surface, false to disable it.

## int IsSurfaceTargetEnabled ( int surface , int target )

Returns the value indicating if the use of the morph target for the specified surface is enabled.
### Arguments

- *int* **surface** - Number of the surface, to which the morph target is appended.
- *int* **target** - Number of the morph target.

### Return value

trueif the use of the morph target for the surface is enabled, otherwise false.
## void SetSurfaceTargetWeight ( int surface , int target , float weight )

Sets the weight of the morph target, i.e. the intensity of it affecting the surface vertices.
### Arguments

- *int* **surface** - Number of the surface, to which the morph target is appended.
- *int* **target** - Number of the morph target.
- *float* **weight** - Weight of the morph target.

## float GetSurfaceTargetWeight ( int surface , int target )

Returns the weight of the morph target, i.e. the intensity of it affecting the surface vertices.
### Arguments

- *int* **surface** - Number of the surface, to which the morph target is appended.
- *int* **target** - Number of the morph target.

### Return value

Weight of the morph target.
## void SetLayerBoneTransform ( int layer , int bone , mat4 transform )

Sets a transformation matrix for the given bone. The difference from the [setBoneTransform()](#setBoneTransform_int_mat4_void) function is that this method takes into account only the transformation in the specified animation layer (no blending is performed).
> **Notice:** The bone can be scaled only uniformly.


### Arguments

- *int* **layer** - Animation layer number.
- *int* **bone** - Bone number.
- *mat4* **transform** - Bone transformation matrix.

## mat4 GetLayerBoneTransform ( int layer , int bone )

Returns a transformation matrix of the given bone relatively to the parent object.
> **Notice:** The difference from [getBoneTransform()](#getBoneTransform_int_mat4) is that this method takes into account only the transformation in the animation layer (no blending is done).


### Arguments

- *int* **layer** - Animation layer number.
- *int* **bone** - Bone number.

### Return value

Bone transformation matrix.
## mat4 GetBoneRestLocalTransform ( int bone )

Returns the rest (bind pose) transformation of the specified bone in its local space relative to the parent bone.
### Arguments

- *int* **bone** - Bone number.

### Return value

Rest (bind pose) transformation matrix in the local bone space.
## void SetLayerBonePosition ( int layer , int bone , vec3 position )

Sets the position for the given bone.
### Arguments

- *int* **layer** - Animation layer number.
- *int* **bone** - Bone number.
- *vec3* **position** - Bone position.

## vec3 GetLayerBonePosition ( int layer , int bone )

Returns the position for the given bone.
### Arguments

- *int* **layer** - Animation layer number.
- *int* **bone** - Bone number.

### Return value

Bone position.
## void SetLayerBoneRotation ( int layer , int bone , quat rotation )

Sets the rotation for the given bone.
### Arguments

- *int* **layer** - Animation layer number.
- *int* **bone** - Bone number.
- *quat* **rotation** - Bone rotation.

## quat GetLayerBoneRotation ( int layer , int bone )

Returns the rotation for the given bone.
### Arguments

- *int* **layer** - Animation layer number.
- *int* **bone** - Bone number.

### Return value

Bone rotation.
## void SetLayerBoneScale ( int layer , int bone , vec3 scale )

Sets the scale for the given bone.
### Arguments

- *int* **layer** - Animation layer number.
- *int* **bone** - Bone number.
- *vec3* **scale** - Bone scale.

## vec3 GetLayerBoneScale ( int layer , int bone )

Returns the scale for the given bone.
### Arguments

- *int* **layer** - Animation layer number.
- *int* **bone** - Bone number.

### Return value

Bone scale.
## void SetLayerFrameUsesEnabled ( int layer , bool enabled )

Toggles the use of animation masks for bones in the specified layer.
### Arguments

- *int* **layer** - Animation layer number.
- *bool* **enabled** - true to enable the use of animation masks for bones in the specified layer, false to disable it.

## bool IsLayerFrameUsesEnabled ( int layer )

Returns the value indicating if the use of animation masks for bones in the specified layer is enabled.
### Arguments

- *int* **layer** - Animation layer number.

### Return value

true if the use of animation masks for bones in the specified layer is enabled, otherwise false.
## void SetLayerBoneFrameUses ( int layer , int bone , ObjectMeshSkinnedLegacy.ANIM_FRAME_USES uses )

Sets the value indicating which components of the frame are to be used to animate the specified bone of the given animation layer.
### Arguments

- *int* **layer** - Animation layer number.
- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).
- *[ObjectMeshSkinnedLegacy.ANIM_FRAME_USES](../../../api/library/objects/class.objectmeshskinnedlegacy_cs.md#ANIM_FRAME_USES)* **uses** - Value indicating frame components to be used.

## ObjectMeshSkinnedLegacy.ANIM_FRAME_USES GetLayerBoneFrameUses ( int layer , int bone )

Returns the value indicating which components of the frame are to be used to animate the specified bone of the given animation layer.
### Arguments

- *int* **layer** - Animation layer number.
- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).

### Return value

Value indicating frame components to be used.
## void SetLayerPose ( int layer , SkeletonPoseDecomposed pose )

Sets the bone transforms for the specified animation layer from the given [SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_cs.md). This overwrites all bone transforms in the layer with the values from the pose.
### Arguments

- *int* **layer** - Animation layer number.
- *[SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_cs.md)* **pose** - Pose to apply to the layer.

## void GetLayerPose ( int layer , SkeletonPoseDecomposed out_pose )

Writes the bone transforms of the specified animation layer into the given [SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_cs.md).
### Arguments

- *int* **layer** - Animation layer number.
- *[SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_cs.md)* **out_pose** - Output pose to receive the layer bone transforms.

## int GetLayerNumFrames ( int layer )

Returns the number of animation frames for a given layer.
### Arguments

- *int* **layer** - Animation layer number.

### Return value

Number of animation frames.
## float SetLayerFrame ( int layer , float frame , int from = -1 , int to = -1 )

Sets a frame for the given animation layer.
### Arguments

- *int* **layer** - Animation layer number.
- *float* **frame** - Frame number in the "from-to" interval. If the float argument is passed, animation is interpolated between nearby frames. 0 means the from frame. For larger values, a residue of a modulo *(from-to)* is calculated. If a negative value is provided, interpolation will be done from the current frame to the *from* frame.
- *int* **from** - Start frame. -1 means the first frame of the animation.
- *int* **to** - End frame. -1 means the last frame of the animation.

### Return value

The number of the frame.
## float GetLayerFrame ( int layer )

Returns the frame number passed as the time argument on the last [setLayerFrame()](#setLayerFrame_int_float_int_int_float) call.
### Arguments

- *int* **layer** - Animation layer number.

### Return value

Frame number.
## int GetLayerFrameFrom ( int layer )

Returns the start frame passed as the from argument on the last [setLayerFrame()](#setLayerFrame_int_float_int_int_float) call.
### Arguments

- *int* **layer** - Animation layer number.

### Return value

Start frame.
## int GetLayerFrameTo ( int layer )

Returns the end frame passed as the to argument on the last [setLayerFrame()](#setLayerFrame_int_float_int_int_float) call.
### Arguments

- *int* **layer** - Animation layer number.

### Return value

End frame.
## long GetAnimationResourceID ( string path )

Returns the unique animation ID using the path to it. This method also loads the animation if it hasn't been loaded yet.
### Arguments

- *string* **path** - Path to the animation file. The path can be represented by either a path to the file or its [GUID](../../../principles/filesystem/index_cs.md#guids), which is the recommended approach. After loading the animation, its internal representation is identified by the path when using *[setLayerAnimationFilePath](#setLayerAnimationFilePath_int_cstr_void)* , etc. > **Notice:** When you [import](../../../editor2/fbx/index.md) your model with animations from an FBX container, the following path to your `*.anim` files should be used: `<path_to_your_fbx_file>/<file.fbx>/<your_anim_file.anim>` > For example: *object->setLayerAnimationFilePath(0,"models/soldier/soldier.fbx/run.anim");*

### Return value

The unique animation ID.
## void SetLayerAnimationFilePath ( int layer , string path )

Sets the path to animation for the given animation layer.
### Arguments

- *int* **layer** - Layer number.
- *string* **path** - Path to the animation file. > **Notice:** When you [import](../../../editor2/fbx/index.md) your model with animations from an FBX container, the following path to your `*.anim` files should be used: **<path_to_your_fbx_file>/<file.fbx>/<your_anim_file.anim>** > For example: *object->setLayerAnimationFilePath(0,"models/soldier/soldier.fbx/run.anim");*

## string GetLayerAnimationFilePath ( int layer )

Returns the path to animation for the given animation layer.
### Arguments

- *int* **layer** - Layer number.

### Return value

Path to the animation file.
## void SetLayerAnimationResourceID ( int layer , long resource_id )

Sets the animation for the layer using the unique animation ID.
### Arguments

- *int* **layer** - Layer number.
- *long* **resource_id** - The unique animation ID.

## long GetLayerAnimationResourceID ( int layer )

Returns the unique ID of the animation used for the layer.
### Arguments

- *int* **layer** - Layer number.

### Return value

The unique animation ID.
## mat4 GetBoneBindLocalTransform ( int bone )

Returns the bone transformation matrix of the bind pose relatively to the parent bone.
> **Notice:** To get the bind pose transformation matrix in the object space, use [getBoneBindObjectTransform()](#getBoneBindObjectTransform_int_mat4).


### Arguments

- *int* **bone** - Bone number.

### Return value

Bind pose transformation matrix.
## mat4 GetBoneBindLocalITransform ( int bone )

Returns the inverse bone transformation matrix of the bind pose relatively to the parent bone.
> **Notice:** To get the bind pose transformation matrix in the object space, use [getBoneBindObjectITransform()](#getBoneBindObjectITransform_int_mat4).


### Arguments

- *int* **bone** - Bone number.

### Return value

Inverse bind pose transformation matrix.
## mat4 GetBoneBindObjectTransform ( int bone )

Returns the bone transformation matrix of the bind pose in the object space.
> **Notice:** To get the bind pose transformation matrix relatively to the parent bone, use [getBoneBindLocalTransform()](#getBoneBindLocalTransform_int_mat4).


### Arguments

- *int* **bone** - Bone number.

### Return value

Bind pose transformation matrix.
## mat4 GetBoneBindObjectITransform ( int bone )

Returns the inverse bone transformation matrix of the bind pose in the object space.
> **Notice:** To get the bind pose transformation matrix relatively to the parent bone, use [getBoneBindLocalITransform()](#getBoneBindLocalITransform_int_mat4).


### Arguments

- *int* **bone** - Bone number.

### Return value

Inverse bind pose transformation matrix.
## mat4 GetBoneSkinningTransform ( int bone )

Returns the bone matrix based on which the bone affects the connected vertices, the result of the following multiplication: getBoneTransform(bone) * getBoneBindObjectITransform(bone).
### Arguments

- *int* **bone** - Bone number.

### Return value

Bone transformation matrix.
## void AddVisualizeLookAtChain ( int chain_id )

Adds the specified LookAtChain to visualization.
### Arguments

- *int* **chain_id** - LookAtChain ID.

## void RemoveVisualizeLookAtChain ( int chain_id )

Removes the specified LookAtChain from visualization.
### Arguments

- *int* **chain_id** - LookAtChain ID.

## void ClearVisualizeLookAtChain ( )

Removes all LookAtChains from visualization.
## void AddVisualizeConstraint ( int constraint_index )

Adds the specified bone constraint to visualization.
### Arguments

- *int* **constraint_index** - Bone constraint index.

## void RemoveVisualizeConstraint ( int constraint_index )

Removes the specified bone constraint from visualization.
### Arguments

- *int* **constraint_index** - Bone constraint index.

## void ClearVisualizeConstraint ( )

Removes all bone constraints from visualization.
## int AddLookAtChain ( )

Adds a new LookAtChain and returns its ID.
### Return value

LookAtChain ID.
## void RemoveLookAtChain ( int chain_id )

Deletes the specified LookAtChain by its ID.
### Arguments

- *int* **chain_id** - LookAtChain ID.

## int GetNumLookAtChains ( )

Returns the total number of LookAtChains.
### Return value

Total number of LookAtChains.
## int GetLookAtChainID ( int num )

Returns the ID of LookAtChain by its index.
### Arguments

- *int* **num** - Index of LookAtChain.

### Return value

LookAtChain ID.
## void SetLookAtChainEnabled ( bool enabled , int chain_id )

Toggles the use of LookAtChain.
### Arguments

- *bool* **enabled** - true to enable LookAtChain, false to disable it.
- *int* **chain_id** - LookAtChain ID.

## bool IsLookAtChainEnabled ( int chain_id )

Checks if LookAtChain is enabled.
### Arguments

- *int* **chain_id** - LookAtChain ID.

### Return value

true if LookAtChain is enabled, otherwise false.
## void SetLookAtChainConstraint ( ObjectMeshSkinnedLegacy.CHAIN_CONSTRAINT constraint , int chain_id )

Configures the type of bone constraint for the solver of the specified chain.
### Arguments

- *[ObjectMeshSkinnedLegacy.CHAIN_CONSTRAINT](../../../api/library/objects/class.objectmeshskinnedlegacy_cs.md#CHAIN_CONSTRAINT)* **constraint** - The type of bone constraint for the solver.
- *int* **chain_id** - LookAtChain ID.

## ObjectMeshSkinnedLegacy.CHAIN_CONSTRAINT GetLookAtChainConstraint ( int chain_id )

Returns the type of bone constraint for the solver of the specified chain.
### Arguments

- *int* **chain_id** - LookAtChain ID.

### Return value

The type of bone constraint for the solver.
## void SetLookAtChainWeight ( float weight , int chain_id )

Sets the weight of LookAtChain, which affects the extent of the bone rotation to the target.
### Arguments

- *float* **weight** - Weight of the chain.
- *int* **chain_id** - LookAtChain ID.

## float GetLookAtChainWeight ( int chain_id )

Returns the weight of LookAtChain, which affects the extent of the bone rotation to the target.
### Arguments

- *int* **chain_id** - LookAtChain ID.

### Return value

Weight of the chain.
## int AddLookAtChainBone ( int bone , int chain_id )

Adds the bone to LookAtChain and returns its index.
### Arguments

- *int* **bone** - The bone to be added to the chain.
- *int* **chain_id** - LookAtChain ID.

### Return value

Bone index.
## int AddLookAtChainBone ( string bone_name , int chain_id )

Adds the bone to LookAtChain and returns its index.
### Arguments

- *string* **bone_name** - The name of the bone to be added to the chain.
- *int* **chain_id** - LookAtChain ID.

### Return value

Bone index.
## int GetLookAtChainNumBones ( int chain_id )

Returns the total number of bones in LookAtChain.
### Arguments

- *int* **chain_id** - LookAtChain ID.

### Return value

The total number of bones in LookAtChain.
## void RemoveLookAtChainBone ( int bone_num , int chain_id )

Removes the bone from LookAtChain by its index.
### Arguments

- *int* **bone_num** - The index of the bone to be removed from the chain.
- *int* **chain_id** - LookAtChain ID.

## int GetLookAtChainBone ( int bone_num , int chain_id )

Returns the bone from LookAtChain by its index.
### Arguments

- *int* **bone_num** - The index of the bone in the chain.
- *int* **chain_id** - LookAtChain ID.

## void SetLookAtChainBoneWeight ( float weight , int bone_num , int chain_id )

Set the additional local weight of the bone.
### Arguments

- *float* **weight** - The weight of the bone in the chain.
- *int* **bone_num** - The index of the bone in the chain.
- *int* **chain_id** - LookAtChain ID.

## float GetLookAtChainBoneWeight ( int bone_num , int chain_id )

Returns the additional local weight of the bone.
### Arguments

- *int* **bone_num** - The index of the bone in the chain.
- *int* **chain_id** - LookAtChain ID.

### Return value

The weight of the bone in the chain.
## void SetLookAtChainBoneUp ( vec3 up , int bone_num , int chain_id )

Sets the UP axis for the bone.
### Arguments

- *vec3* **up** - The UP vector for the bone.
- *int* **bone_num** - The index of the bone in the chain.
- *int* **chain_id** - LookAtChain ID.

## vec3 GetLookAtChainBoneUp ( int bone_num , int chain_id )

Returns the UP axis for the bone.
### Arguments

- *int* **bone_num** - The index of the bone in the chain.
- *int* **chain_id** - LookAtChain ID.

### Return value

The UP vector for the bone.
## void SetLookAtChainBoneAxis ( vec3 axis , int bone_num , int chain_id )

Sets the axis that is directed at the target of LookAtChain.
### Arguments

- *vec3* **axis** - The axis that is directed at the target.
- *int* **bone_num** - The index of the bone in the chain.
- *int* **chain_id** - LookAtChain ID.

## vec3 GetLookAtChainBoneAxis ( int bone_num , int chain_id )

Returns the axis that is directed at the target of LookAtChain.
### Arguments

- *int* **bone_num** - The index of the bone in the chain.
- *int* **chain_id** - LookAtChain ID.

### Return value

The axis that is directed at the target.
## void SetLookAtChainTargetPosition ( vec3 position , int chain_id )

Sets the position for the rotation in the object space.
### Arguments

- *vec3* **position** - The position for the rotation in the object space.
- *int* **chain_id** - LookAtChain ID.

## vec3 GetLookAtChainTargetPosition ( int chain_id )

Returns the position for the rotation in the object space.
### Arguments

- *int* **chain_id** - LookAtChain ID.

### Return value

The position for the rotation in the object space.
## void SetLookAtChainTargetWorldPosition ( vec3 position , int chain_id )

Sets the position for the rotation in the world space.
### Arguments

- *vec3* **position** - The position for the rotation in the world space.
- *int* **chain_id** - LookAtChain ID.

## vec3 GetLookAtChainTargetWorldPosition ( int chain_id )

Returns the position for the rotation in the world space.
### Arguments

- *int* **chain_id** - LookAtChain ID.

### Return value

The position for the rotation in the world space.
## void SetLookAtChainPolePosition ( vec3 position , int chain_id )

Sets the position of the pole vector in the object space.
### Arguments

- *vec3* **position** - The position of the pole vector in the object space.
- *int* **chain_id** - LookAtChain ID.

## vec3 GetLookAtChainPolePosition ( int chain_id )

Returns the position of the pole vector in the object space.
### Arguments

- *int* **chain_id** - LookAtChain ID.

### Return value

The position of the pole vector in the object space.
## void SetLookAtChainPoleWorldPosition ( vec3 position , int chain_id )

Sets the position of the pole vector in the world space.
### Arguments

- *vec3* **position** - The position of the pole vector in the world space.
- *int* **chain_id** - LookAtChain ID.

## vec3 GetLookAtChainPoleWorldPosition ( int chain_id )

Returns the position of the pole vector in the world space.
### Arguments

- *int* **chain_id** - LookAtChain ID.

### Return value

The position of the pole vector in the world space.
## int GetIKChainID ( int num )

Returns the IKChain ID by its index.
### Arguments

- *int* **num** - IKChain index.

### Return value

IKChain ID.
## void SetIKChainConstraint ( ObjectMeshSkinnedLegacy.CHAIN_CONSTRAINT constraint , int chain_id )

Configures the type of bone constraint for the solver of the specified chain.
### Arguments

- *[ObjectMeshSkinnedLegacy.CHAIN_CONSTRAINT](../../../api/library/objects/class.objectmeshskinnedlegacy_cs.md#CHAIN_CONSTRAINT)* **constraint** - The type of bone constraint for the solver.
- *int* **chain_id** - IK chain ID.

## ObjectMeshSkinnedLegacy.CHAIN_CONSTRAINT GetIKChainConstraint ( int chain_id )

Returns the type of bone constraint for the solver of the specified chain.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

The type of bone constraint for the solver.
## int AddIKChainBone ( string bone_name , int chain_id )

Adds the bone to IKChain and returns its index.
### Arguments

- *string* **bone_name** - The bone name.
- *int* **chain_id** - IKChain ID.

### Return value

Bone index.
## int AddBoneConstraint ( int bone )

Adds the rotation constraint to the specified bone.
### Arguments

- *int* **bone** - The bone index in the mesh.

### Return value

The constraint index.
## int AddBoneConstraint ( string bone_name )

Adds the rotation constraint to the specified bone.
### Arguments

- *string* **bone_name** - The bone name.

### Return value

The constraint index.
## void RemoveBoneConstraint ( int constraint_num )

Removes the specified bone rotation constraint.
### Arguments

- *int* **constraint_num** - The constraint index.

## int FindBoneConstraint ( int bone )

Returns the rotation constraint index for the specified bone.
### Arguments

- *int* **bone** - The bone index in the mesh.

### Return value

The constraint index.
## int FindBoneConstraint ( string bone_name )

Returns the rotation constraint index for the specified bone.
### Arguments

- *string* **bone_name** - The bone name.

### Return value

The constraint index.
## void SetBoneConstraintEnabled ( bool enabled , int constraint_num )

Enables the use of the rotation constraint for the bone.
### Arguments

- *bool* **enabled** - true to enable the use of the rotation constraint for the bone, false to disable it.
- *int* **constraint_num** - The constraint index.

## bool IsBoneConstraintEnabled ( int constraint_num )

Returns the value indicating if the use of the rotation constraint for the bone is enabled.
### Arguments

- *int* **constraint_num** - The constraint index.

### Return value

true if the use of the rotation constraint for the bone is enabled, otherwise false.
## int GetBoneConstraintBoneIndex ( int constraint_num )

Returns the index of the bone for which the rotation constraint is set.
### Arguments

- *int* **constraint_num** - The constraint index.

### Return value

The bone index in the mesh.
## void SetBoneConstraintYawAxis ( vec3 axis , int constraint_num )

Sets the yaw axis for the bone rotation constraint.
### Arguments

- *vec3* **axis** - The yaw axis.
- *int* **constraint_num** - The constraint index.

## vec3 GetBoneConstraintYawAxis ( int constraint_num )

Returns the yaw axis for the bone rotation constraint.
### Arguments

- *int* **constraint_num** - The constraint index.

### Return value

The yaw axis.
## void SetBoneConstraintPitchAxis ( vec3 axis , int constraint_num )

Sets the pitch axis for the bone rotation constraint.
### Arguments

- *vec3* **axis** - The pitch axis.
- *int* **constraint_num** - The constraint index.

## vec3 GetBoneConstraintPitchAxis ( int constraint_num )

Returns the pitch axis for the bone rotation constraint.
### Arguments

- *int* **constraint_num** - The constraint index.

### Return value

The pitch axis.
## void SetBoneConstraintRollAxis ( vec3 axis , int constraint_num )

Sets the roll axis for the bone rotation constraint.
### Arguments

- *vec3* **axis** - The roll axis.
- *int* **constraint_num** - The constraint index.

## vec3 GetBoneConstraintRollAxis ( int constraint_num )

Returns the roll axis for the bone rotation constraint.
### Arguments

- *int* **constraint_num** - The constraint index.

### Return value

The roll axis.
## void SetBoneConstraintYawAngles ( float min_angle , float max_angle , int constraint_num )

Sets the minimum and maximum angles restricting the bone rotation along the yaw axis.
### Arguments

- *float* **min_angle** - The minimum rotation angle.
- *float* **max_angle** - The maximum rotation angle.
- *int* **constraint_num** - The constraint index.

## float GetBoneConstraintYawMinAngle ( int constraint_num )

Returns the minimum angle restricting the bone rotation along the yaw axis.
### Arguments

- *int* **constraint_num** - The constraint index.

### Return value

The minimum rotation angle.
## float GetBoneConstraintYawMaxAngle ( int constraint_num )

Returns the maximum angle restricting the bone rotation along the yaw axis.
### Arguments

- *int* **constraint_num** - The constraint index.

### Return value

The maximum rotation angle.
## void SetBoneConstraintPitchAngles ( float min_angle , float max_angle , int constraint_num )

Sets the minimum and maximum angles restricting the bone rotation along the pitch axis.
### Arguments

- *float* **min_angle** - The minimum rotation angle.
- *float* **max_angle** - The maximum rotation angle.
- *int* **constraint_num** - The constraint index.

## float GetBoneConstraintPitchMinAngle ( int constraint_num )

Returns the minimum angle restricting the bone rotation along the pitch axis.
### Arguments

- *int* **constraint_num** - The constraint index.

### Return value

The minimum rotation angle.
## float GetBoneConstraintPitchMaxAngle ( int constraint_num )

Returns the maximum angle restricting the bone rotation along the pitch axis.
### Arguments

- *int* **constraint_num** - The constraint index.

### Return value

The maximum rotation angle.
## void SetBoneConstraintRollAngles ( float min_angle , float max_angle , int constraint_num )

Sets the minimum and maximum angles restricting the bone rotation along the roll axis.
### Arguments

- *float* **min_angle** - The minimum rotation angle.
- *float* **max_angle** - The maximum rotation angle.
- *int* **constraint_num** - The constraint index.

## float GetBoneConstraintRollMinAngle ( int constraint_num )

Returns the minimum angle restricting the bone rotation along the roll axis.
### Arguments

- *int* **constraint_num** - The constraint index.

### Return value

The minimum rotation angle.
## float GetBoneConstraintRollMaxAngle ( int constraint_num )

Returns the maximum angle restricting the bone rotation along the roll axis.
### Arguments

- *int* **constraint_num** - The constraint index.

### Return value

The maximum rotation angle.
## bool IsLayerAnimationStreaming ( int layer )

Returns a value indicating if the animation on the specified layer is currently being loaded by the [data streaming](../../../principles/data_streaming/index.md) system. While the animation is streaming, the layer holds the first frame of this animation.
### Arguments

- *int* **layer** - Layer number.

### Return value

true if the animation assigned to the specified layer is still being streamed in; otherwise, false.
## void ResetLayerToBindPose ( int layer )

Sets the skeleton's bind pose on the specified layer.
### Arguments

- *int* **layer** - Layer number.

## void ResetLayerToRestPose ( int layer )

Sets the mesh's rest pose on the specified layer.
### Arguments

- *int* **layer** - Layer number.

## bool LoadAsyncRender ( )

Requests asynchronous loading of the mesh for rendering. The mesh becomes available in one of the following frames, so the object keeps rendering whatever it already has until then.
### Return value

true if the request has been queued; otherwise, false.
## bool LoadForceRender ( )

Loads the mesh for rendering immediately, blocking until it is done.
### Return value

true if the mesh has been loaded; otherwise, false.
