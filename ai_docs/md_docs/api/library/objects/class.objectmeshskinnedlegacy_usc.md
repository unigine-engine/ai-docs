# ObjectMeshSkinnedLegacy Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Object


This class is used to create and modify [skinned meshes](../../../objects/objects/mesh_skinned_legacy/index.md). Skinned Meshes are used to render characters with animation.


#### Applying Animation


Animation is applied to *ObjectMeshSkinnedLegacy* via its layers. Layers store skeletal poses, the pose is taken from the animation.


By default, when created, *ObjectMeshSkinnedLegacy* has only one active base layer, the pose of which is used for animation. More layers can be added to store various poses that may be blended or processed otherwise (through such functions as *[*lerpLayer*](#lerpLayer_int_int_int_float_void)*, *[*copyLayer*](#copyLayer_int_int_void)*, *[*importLayer*](#importLayer_int_void)*, *[*inverseLayer*](#inverseLayer_int_int_void)* and *[*mulLayer*](#mulLayer_int_int_int_float_void)*), with the resulting pose saved in the base layer for final render output.


**Automatic blending** of animations suitable for simple use cases is implemented internally in ObjectMeshSkinnedLegacy. For a layer to be included in the final blend, it must be enabled and have a non-zero weight. These values can be changed using **[setLayer()()](../../...md#setLayer_int_int_float_void)**, **[setLayerEnabled()()](../../...md#setLayerEnabled_int_int_void)** and **[setLayerWeight()()](../../...md#setLayerWeight_int_float_void)**. When blending, an arithmetic weighted average is applied: all layer weights are first normalized, after which each component is multiplied by its corresponding weight and summed.


A similar approach is used for scaling and a slightly different one for rotations, but for working at the layer level this is not critical.


**Customized blending** of animations including partial bone blending, additive animation, and so on, is implemented via custom logic. You can control individual bones on layers using **[setLayerBoneTransform()()](../../...md#setLayerBoneTransform_int_int_mat4_void)** / **[getLayerBoneTransform()()](../../...md#getLayerBoneTransform_int_int_mat4)**, as well as their counterparts for individual components: position, rotation and scale. These functions allow you to create masks for bones and then work exclusively with those bones in a loop.


##### Creating and Playing Animation


To add the animation to the ObjectMeshSkinnedLegacy and play it, do the following:


1. Set the number of animation layers with **[clearVisualizeIKChain()()](../../...md#setNumLayers_int_void)**. There is only one layer by default, the pose of which is used for animation.
2. Enable each layer and set the animation weight for blending by calling the **[setLayer()()](../../...md#setLayer_int_int_float_void)** function.
3. Add the animation `*.anim` file by using the **[setLayerAnimationFilePath()()](../../...md#setLayerAnimationFilePath_int_cstr_void)** function.
4. Play the added animation by calling the **[setLayerFrame()()](../../...md#setLayerFrame_int_float_int_int_float)** function for each animation layer.


Blending is performed between all layers. The contribution of each layer depends on its weight. Also, you can optionally define single bone transformations by hand, if needed, using either **[setBoneTransform()()](../../...md#setBoneTransform_int_mat4_void)** or **[setBoneTransformWithChildren()()](../../...md#setBoneTransformWithChildren_int_mat4_void)**.


###### Usage Example


The following example shows how to blend two different animations assigned to a mesh. You can use the mesh and animations from UNIGINE samples located in the following sample set folders:


- `<cpp_samples>/data/showcase_content/person`
- `<csharp_component_samples>/data/showcase_content/agent`


Animations are added by using the **[setLayerAnimationFilePath()()](../../...md#setLayerAnimationFilePath_int_cstr_void)** function.


```cpp
// define the new ObjectMeshSkinnedLegacy class instance
					ObjectMeshSkinnedLegacy skinned_mesh;

					int init() {
						/* ... */
						// create the new ObjectMeshSkinnedLegacy mesh based on an existing mesh
						skinned_mesh = new ObjectMeshSkinnedLegacy("samples/animation/meshes/agent.mesh");

						// we need two layers to get poses from two animations
						skinned_mesh.setNumLayers(2);

						// load animations from the files
						int animation_1 = skinned_mesh.addAnimation("samples/animation/animations/agent_run.anim");
						int animation_2 = skinned_mesh.addAnimation("samples/animation/animations/agent_punch.anim");

						// enable each layer and set an animation weight
						skinned_mesh.setLayer(0,1,0.7);
						skinned_mesh.setLayer(1,1,0.3);

						// set animations to layers
						skinned_mesh.setAnimation(0, animation_1);
						skinned_mesh.setAnimation(1, animation_2);

						/* ... */
					}

					int update() {
						/* ... */
						// get the current time spent in the game
						float time = engine.game.getTime();

						// start each animation playing
						skinned_mesh.setLayerFrame(0,time * 25.0f);
						skinned_mesh.setLayerFrame(1,time * 25.0f);
						/* ... */
					}

```


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


In contrast to [procedural modes](../../../api/library/objects/class.objectmeshstatic_usc.md#PROCEDURAL_MODE) available for static meshes, skinned meshes have **only one mode** - equivalent to *[PROCEDURAL_MODE_DYNAMIC](../../../api/library/objects/class.objectmeshstatic_usc.md#PROCEDURAL_MODE_DYNAMIC)* (the procedural mesh remains in VRAM and will not be unloaded).


Procedural updates for skinned meshes are performed exclusively in the Engine's main thread using *[applyMeshProcedural()()](../../...md#applyMeshProcedural_ConstMeshSkinned_int)*. If the source mesh contains compatible elements (e.g., bones, surfaces, skinning data) matching the original, then animations, morph targets, and other behaviors will continue to function without interruption. Otherwise, the mesh will remain static, with no animation or morphing applied.


#### Reusing Animations


Animations from one character can be used for another.


##### Animation Frame Masks


Masks are the simplest way of reusing animations, a couple of words about how they work. To each layer of an *ObjectMeshSkinnedLegacy* you can assign some animation and based on its frames it will change bone transformations on this layer. You can use **[masks](#ANIM_FRAME_USES_NONE)** to choose which components of the animation frame (position, rotation, scale, their combinations, or all of them) are to be used for each particular layer. In case any component is missing in the mask, the corresponding value will be taken from the T-pose.


As an example let's take eyes animation for these two skeletons:


![](anim_mask_1.jpg)


They have absolutely the same bone hierarchy as well as bone names, only the proportions differ. If we use animation for eyes from the left skeleton for the right one, we'll get the following result:


![](anim_mask_2.jpg)


The initial animation has completely changed the proportions of the second skeleton. We can fix it by setting **[ANIM_FRAME_USES_ROTATION](#ANIM_FRAME_USES_ROTATION)** mask to eye bones, and **[ANIM_FRAME_USES_NONE](#ANIM_FRAME_USES_NONE)** for the rest of the bones via the **[setLayerBoneFrameUses()()](../../...md#setLayerBoneFrameUses_int_int_int_void)* / *[getLayerBoneFrameUses()()](../../...md#getLayerBoneFrameUses_int_int_int)** methods. Thus, all values except for eyes rotation will be taken from the T-pose :


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


To visualize IK chains you can use the following methods: **[addVisualizeIKChain()()](../../...md#addVisualizeIKChain_int_void)*, *[removeVisualizeIKChain()()](../../...md#removeVisualizeIKChain_int_void)**, and **[clearVisualizeIKChain()()](../../...md#clearVisualizeIKChain_void)**.


![](ik_visualizer.gif)


### See Also


- *[Mesh](../../../api/library/rendering/class.mesh_usc.md)* class
- Article on [Mesh File Formats](../../../code/formats/file_formats.md#mesh)
- Animation samples in *[C++](../../../sdk/api_samples/cpp/animation.md)* and *[C# Component Samples](../../../sdk/api_samples/cs/animation.md)* suites


## ObjectMeshSkinnedLegacy Class

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
## int isStopped () const

Returns the current stop status.
### Return value

Current animation is stopped
## int isPlaying () const

Returns the current playback status.
### Return value

Current animation is playing
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
> **Notice:** *[setTime()()](../../...md#setTime_float_void)* function corresponds to the [Play](../../../objects/objects/mesh_skinned_legacy/index.md#play) and [Stop](../../../objects/objects/mesh_skinned_legacy/index.md#stop) options in the editor. In all other cases use *[setLayerFrame()()](../../...md#setLayerFrame_int_float_int_int_float)* to set the animation.


### Arguments

- *float* **time** - The animation time, in animation frames

## float getTime () const

Returns the current animation time, in animation frames. The time count starts from the zero frame. If the time is set to be between frames, animation is blended. If the time is set outside the animation frame range, the animation is looped.
> **Notice:** *[setTime()()](../../...md#setTime_float_void)* function corresponds to the [Play](../../../objects/objects/mesh_skinned_legacy/index.md#play) and [Stop](../../../objects/objects/mesh_skinned_legacy/index.md#stop) options in the editor. In all other cases use *[setLayerFrame()()](../../...md#setLayerFrame_int_float_int_int_float)* to set the animation.


### Return value

Current animation time, in animation frames
## void setLoop ( int loop )

Sets a new value indicating if the animation is looped or played only once.
### Arguments

- *int* **loop** - The playing of the animation in a loop

## int isLoop () const

Returns the current value indicating if the animation is looped or played only once.
### Return value

Current playing of the animation in a loop
## void setControlled ( int controlled )

Sets a new value indicating if the animation is controlled by a parent ObjectMeshSkinnedLegacy.
### Arguments

- *int* **controlled** - The animation is controlled by a parent ObjectMeshSkinnedLegacy

## int isControlled () const

Returns the current value indicating if the animation is controlled by a parent ObjectMeshSkinnedLegacy.
### Return value

Current animation is controlled by a parent ObjectMeshSkinnedLegacy
## void setQuaternion ( int quaternion )

Sets a new value indicating if the dual-quaternion skinning mode is used. The dual-quaternion model is an accurate, computationally efficient, robust, and flexible method of representing rigid transforms and it is used in skeletal animation. See [a Wikipedia article on dual quaternions](https://en.wikipedia.org/wiki/Dual_quaternion) and [a beginners guide to dual-quaternions](http://cs.gmu.edu/~jmlien/teaching/cs451/uploads/Main/dual-quaternion.pdf) for more information.
### Arguments

- *int* **quaternion** - The dual-quaternion skinning mode

## int isQuaternion () const

Returns the current value indicating if the dual-quaternion skinning mode is used. The dual-quaternion model is an accurate, computationally efficient, robust, and flexible method of representing rigid transforms and it is used in skeletal animation. See [a Wikipedia article on dual quaternions](https://en.wikipedia.org/wiki/Dual_quaternion) and [a beginners guide to dual-quaternions](http://cs.gmu.edu/~jmlien/teaching/cs451/uploads/Main/dual-quaternion.pdf) for more information.
### Return value

Current dual-quaternion skinning mode
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
## void setVisualizeAllBones ( int bones )

Sets a new value indicating if visualization for bones and their basis vectors is enabled. The visualizer can be used for debugging purposes showing positions of bones and their basis vectors for multiple meshes simultaneously.
### Arguments

- *int* **bones** - The visualization of bones and their basis vectors

## int isVisualizeAllBones () const

Returns the current value indicating if visualization for bones and their basis vectors is enabled. The visualizer can be used for debugging purposes showing positions of bones and their basis vectors for multiple meshes simultaneously.
### Return value

Current visualization of bones and their basis vectors
## int getNumIKChains () const

Returns the current number of [IK chains](#ik_chains) of the skinned mesh.
### Return value

Current number of IK chains.
## getEventEndBoneConstraints () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginBoneConstraints () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndIKSolvers () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginIKSolvers () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndLookAtSolvers () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginLookAtSolvers () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## int getNumBoneConstraints () const

Returns the current total number of bone rotation constraints.
### Return value

Current total number of constraints.
## void setInterpolationAccuracy ( )

Sets a new interpolation mode for the bone rotations. The value is set to HIGH by default.
### Arguments

- **accuracy** - The interpolation mode for the bone rotations. The default value is set to HIGH.

## getInterpolationAccuracy () const

Returns the current interpolation mode for the bone rotations. The value is set to HIGH by default.
### Return value

Current interpolation mode for the bone rotations. The default value is set to HIGH.
## void setAnimPath ( )

Sets a new path to a file containing the specified animation.
### Arguments

- **path** - The path to a file containing the specified animation.

## const char * getAnimPath () const

Returns the current path to a file containing the specified animation.
### Return value

Current path to a file containing the specified animation.
## void setMeshProceduralMode ( int mode )

Sets a new value indicating if the [procedural mesh usage mode](#procedural_modification) is enabled for the object. With the procedural mode enabled, geometry of the **ObjectMeshSkinnedLegacy** can be modified via *[applyMeshProcedural()()](../../...md#applyMeshProcedural_ConstMeshSkinned_int)*. Disabling the procedural mode restores the object's initial geometry, removing any changes applied. For skinned meshes, procedural geometry editing is done only through the direct main-thread workflow, unlike static meshes that can use asynchronous generation or [other update strategies](../../../api/library/objects/class.objectmeshstatic_usc.md#procedural_workflow).
### Arguments

- *int* **mode** - The value indicating if the procedural mesh usage mode is enabled for the object

## int isMeshProceduralMode () const

Returns the current value indicating if the [procedural mesh usage mode](#procedural_modification) is enabled for the object. With the procedural mode enabled, geometry of the **ObjectMeshSkinnedLegacy** can be modified via *[applyMeshProcedural()()](../../...md#applyMeshProcedural_ConstMeshSkinned_int)*. Disabling the procedural mode restores the object's initial geometry, removing any changes applied. For skinned meshes, procedural geometry editing is done only through the direct main-thread workflow, unlike static meshes that can use asynchronous generation or [other update strategies](../../../api/library/objects/class.objectmeshstatic_usc.md#procedural_workflow).
### Return value

Current value indicating if the procedural mesh usage mode is enabled for the object
## int isLoaded () const

Returns the current value indicating if the mesh is loaded (it is either a procedural one or has been loaded via the [setMeshPath()](#setMeshPath_cstr_void) method).
### Return value

Current the mesh is procedural or has been loaded from a mesh file
## void setMeshPath ( )

Sets a new path to the mesh file. If the *Procedural* flag is enabled for the object, the mesh won't be loaded.
### Arguments

- **path** - The path to the mesh file.

## const char * getMeshPath () const

Returns the current path to the mesh file. If the *Procedural* flag is enabled for the object, the mesh won't be loaded.
### Return value

Current path to the mesh file.
---

## static ObjectMeshSkinnedLegacy ( string path )

ObjectMeshSkinnedLegacy constructor.
### Arguments

- *string* **path** - Path to the skinned mesh file.

## static ObjectMeshSkinnedLegacy ( )

ObjectMeshSkinnedLegacy constructor.
## int getBoneChild ( int bone , int child )

Returns the number of a child of the given bone.
### Arguments

- *int* **bone** - Bone number.
- *int* **child** - Child number.

### Return value

Number of the child in the collection of all bones.
## void setBoneTransformWithChildren ( int bone , mat4 transform )

Sets transformation for the bone and all of its children (without considering node transformations).
> **Notice:** Bones can be scaled only uniformly.


### Arguments

- *int* **bone** - Bone number.
- *mat4* **transform** - Transformation matrix.

## string getBoneName ( int bone )

Returns the name of the given bone.
### Arguments

- *int* **bone** - Bone number.

### Return value

Bone name.
## int getBoneParent ( int bone )

Returns the number of the parent bone for a given one.
### Arguments

- *int* **bone** - Number of the bone, for which the parent will be returned.

### Return value

Parent bone number, if the parent exists; otherwise, -1.
## void setBoneTransform ( int bone , mat4 transform )

Sets a transformation matrix for the given bone (without considering node transformations).
> **Notice:** Bones can be scaled only uniformly.


### Arguments

- *int* **bone** - Bone number.
- *mat4* **transform** - Transformation matrix.

## mat4 getBoneTransform ( int bone )

Returns a transformation matrix of the given bone relatively to the parent object (not considering transformations of the Mesh Skinned node itself).
### Arguments

- *int* **bone** - Bone number.

### Return value

Transformation matrix.
## void setBoneTransforms ( int[] bones , mat4[] transforms , int num_bones )

Sets a transformation matrix for given bones.
### Arguments

- *int[]* **bones** - Bone numbers.
- *mat4[]* **transforms** - Transformation matrices.
- *int* **num_bones** - Number of bones.

## int getCIndex ( int num , int surface )

Returns the [coordinate index](../../../api/library/rendering/class.mesh_usc.md#cindices) for the given vertex of the given surface.
### Arguments

- *int* **num** - Vertex number in the range from 0 to the total number of coordinate indices for the given surface. > **Notice:** To get the total number of coordinate indices for the given surface, use the [getNumCIndices()](#getNumCIndices_int_int) method.
- *int* **surface** - Mesh surface number.

### Return value

Coordinate index.
## vec4 getColor ( int num , int surface )

Returns the color of the given [triangle vertex](../../../api/library/rendering/class.mesh_usc.md#tvertex) of the given surface.
### Arguments

- *int* **num** - [Triangle vertex](../../../api/library/rendering/class.mesh_usc.md#tvertex) number in the range from 0 to the total number of vertex color entries of the given surface. > **Notice:** To get the total number of vertex color entries for the surface, call the [*getNumColors()*](#getNumColors_int_int) method.
- *int* **surface** - Mesh surface number.

### Return value

Vertex color.
## void setLayer ( int layer , int enabled , float weight )

Enables or disables the given animation layer and sets the value of the weight parameter.
### Arguments

- *int* **layer** - Animation layer number.
- *int* **enabled** - Enable flag. 1 to enable the layer, 0 to disable it.
- *float* **weight** - Animation layer weight.

## void setLayerEnabled ( int layer , int enabled )

Enables or disables a given animation layer.
### Arguments

- *int* **layer** - Animation layer number.
- *int* **enabled** - **1** to enable the animation layer, **0** to disable it.

## int isLayerEnabled ( int layer )

Returns a value indicating if a given animation layer is enabled.
### Arguments

- *int* **layer** - Animation layer number.

### Return value

**1** if the layer is disabled; otherwise, **0**.
## void setLayerWeight ( int layer , float weight )

Sets a weight for the animation layer.
### Arguments

- *int* **layer** - Animation layer number.
- *float* **weight** - Animation layer weight.

## float getLayerWeight ( int layer )

Returns the weight of the animation layer.
### Arguments

- *int* **layer** - Animation layer number.

### Return value

Weight of the animation layer.
## int getMesh ( MeshSkinned & mesh )

Copies the current mesh into the destination mesh.
```cpp
// a skinned mesh from which geometry will be obtained
ObjectMeshSkinnedLegacy skinnedMesh = new ObjectMeshSkinnedLegacy("skinned.mesh");
// create a new mesh
MeshSkinned mesh = new MeshSkinned();
// copy geometry to the created mesh
if (skinnedMesh.getMesh(mesh)) {
	// do something with the obtained mesh
}
else {
	log.error("Failed to copy a mesh\n");
}

```


### Arguments

- *[MeshSkinned](../../../api/library/rendering/class.meshskinned_usc.md) &* **mesh** - Destination mesh to copy into.

### Return value

**1** if the mesh is copied successfully.
## int getMeshSurface ( Mesh mesh , int surface , int target = -1 )

Copies the specified mesh surface to the destination mesh.
### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_usc.md)* **mesh** - Destination [Mesh](../../../api/library/rendering/class.mesh_usc.md) to copy the surface to.
- *int* **surface** - Number of the mesh surface to be copied.
- *int* **target** - Number of the surface morph target to be copied. The default value is -1 (all morph targets).

### Return value

Number of the new added mesh surface.
## vec3 getNormal ( int num , int surface , int target = 0 )

Returns the normal for the given [triangle vertex](../../../api/library/rendering/class.mesh_usc.md#tvertex) of the given surface target.
### Arguments

- *int* **num** - [Triangle vertex](../../../api/library/rendering/class.mesh_usc.md#tvertex) number in the range from 0 to the total number of vertex tangent entries of the given surface target. > **Notice:** Vertex normals are calculated using vertex tangents. To get the total number of vertex tangent entries for the surface target, call the [*getNumTangents()*](#getNumTangents_int_int) method.
- *int* **surface** - Mesh surface number.
- *int* **target** - Surface target number. The default value is 0.

### Return value

Vertex normal.
## int getNumBoneChildren ( int bone )

Returns the number of children for the specified bone.
### Arguments

- *int* **bone** - Bone number.

### Return value

Number of child bones.
## int getNumCIndices ( int surface )

Returns the number of [coordinate indices](../../../api/library/rendering/class.mesh_usc.md#cindices) for the given mesh surface.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Number of coordinate indices.
## int getNumColors ( int surface )

Returns the total number of vertex color entries for the given surface.
> **Notice:** Colors are specified for [triangle vertices](../../../api/library/rendering/class.mesh_usc.md#tvertex).


### Arguments

- *int* **surface** - Surface number.

### Return value

Number of vertex color entries.
## int getNumSurfaceTargets ( int surface )

Returns the number of surface morph targets for the given mesh surface.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Number of surface morph targets.
## int getNumTangents ( int surface )

Returns the number of vertex tangent entries of the given mesh surface.
> **Notice:** Tangents are specified for [triangle vertices](../../../api/library/rendering/class.mesh_usc.md#tvertex).


### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Number of surface tangent vectors.
## int getNumTexCoords0 ( int surface )

Returns the number of the first UV map texture coordinates for the given mesh surface.
> **Notice:** First UV map texture coordinates are specified for [triangle vertices](../../../api/library/rendering/class.mesh_usc.md#tvertex).


### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Number of the first UV map texture coordinates.
## int getNumTexCoords1 ( int surface )

Returns the number of the second UV map texture coordinates for the given mesh surface.
> **Notice:** Second UV map texture coordinates are specified for [triangle vertices](../../../api/library/rendering/class.mesh_usc.md#tvertex).


### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Number of the second UV map texture coordinates.
## int getNumTIndices ( int surface )

Returns the number of triangle indices for the given mesh surface.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Number of [triangle indices](../../../api/library/rendering/class.mesh_usc.md#tindices).
## int getNumVertex ( int surface )

Returns the number of [coordinate vertices](../../../api/library/rendering/class.mesh_usc.md#cvertex) for the given mesh surface.
### Arguments

- *int* **surface** - Mesh surface number.

### Return value

Number of the surface vertices.
## vec3 getSkinnedNormal ( int num , int index , int surface )

Returns the skinned normal for the given [triangle vertex](../../../api/library/rendering/class.mesh_usc.md#tvertex).
> **Notice:** A skinned normal is a recalculated normal for bones and morph targets used in skinning.


### Arguments

- *int* **num** - [Triangle vertex](../../../api/library/rendering/class.mesh_usc.md#tvertex) number in the range from 0 to the total number of vertex tangent entries of the given surface target. > **Notice:** Vertex normals are calculated using vertex tangents. To get the total number of vertex tangent entries for the surface target, call the [*getNumTangents()*](#getNumTangents_int_int) method.
- *int* **index** - [Coordinate index](../../../api/library/rendering/class.mesh_usc.md#cindices) of the vertex. > **Notice:** if -1 is passed, the coordinate index will be obtained for the first vertex having its [triangle index](../../../api/library/rendering/class.mesh_usc.md#tindices) equal to the specified [triangle vertex](../../../api/library/rendering/class.mesh_usc.md#tvertex) number.
- *int* **surface** - Mesh surface number.

### Return value

Skinned normal.
## quat getSkinnedTangent ( int num , int index , int surface )

Returns the skinned tangent vector for the given [triangle vertex](../../../api/library/rendering/class.mesh_usc.md#tvertex).
> **Notice:** A skinned tangent vector is a recalculated tangent vector for bones and morph targets used in skinning.


### Arguments

- *int* **num** - [Triangle vertex](../../../api/library/rendering/class.mesh_usc.md#tvertex) number in the range from 0 to the total number of vertex tangent entries of the given surface target. > **Notice:** To get the total number of vertex tangent entries for the surface target, call the [*getNumTangents()*](#getNumTangents_int_int) method.
- *int* **index** - [Coordinate index](../../../api/library/rendering/class.mesh_usc.md#cindices) of the vertex. > **Notice:** if -1 is passed, the coordinate index will be obtained for the first vertex having its [triangle index](../../../api/library/rendering/class.mesh_usc.md#tindices) equal to the specified [triangle vertex](../../../api/library/rendering/class.mesh_usc.md#tvertex) number.
- *int* **surface** - Mesh surface number.

### Return value

Skinned tangent.
## vec3 getSkinnedVertex ( int num , int surface )

Returns skinned coordinates of the given [coordinate vertex](../../../api/library/rendering/class.mesh_usc.md#cvertex).
> **Notice:** A skinned vertex is a recalculated vertex for bones and morph targets used in skinning.


### Arguments

- *int* **num** - [Coordinate vertex](../../../api/library/rendering/class.mesh_usc.md#cvertex) number in the range from 0 to the total number of coordinate vertices for the given surface. > **Notice:** To get the total number of coordinate vertices for the given surface, use the [getNumVertex()](#getNumVertex_int_int) method.
- *int* **surface** - Mesh surface number.

### Return value

Vertex coordinates.
## int isNeedUpdate ( )

Returns a value indicating if the *ObjectMeshSkinnedLegacy* needs to be updated (e.g. after adding new animations).
### Return value

**1** if the skinned mesh needs to be updated; otherwise, **0**.
## string getSurfaceTargetName ( int surface , int target )

Returns the name of the morph target for the given mesh surface.
### Arguments

- *int* **surface** - Mesh surface number.
- *int* **target** - Morph target number.

### Return value

Morph target name.
## quat getTangent ( int num , int surface , int target = 0 )

Returns the tangent for the given [triangle vertex](../../../api/library/rendering/class.mesh_usc.md#tvertex) of the given surface target.
### Arguments

- *int* **num** - [Triangle vertex](../../../api/library/rendering/class.mesh_usc.md#tvertex) number in the range from 0 to the total number of vertex tangent entries of the given surface. > **Notice:** To get the total number of vertex tangent entries for the surface, call the [getNumTangents()](#getNumTangents_int_int) method.
- *int* **surface** - Mesh surface number.
- *int* **target** - Surface target number. The default value is 0.

### Return value

Vertex tangent.
## vec2 getTexCoord0 ( int num , int surface )

Returns first UV map texture coordinates for the given [triangle vertex](../../../api/library/rendering/class.mesh_usc.md#tvertex) of the given surface.
### Arguments

- *int* **num** - [Triangle vertex](../../../api/library/rendering/class.mesh_usc.md#tvertex) number in the range from 0 to the total number of first UV map texture coordinate entries of the given surface. > **Notice:** To get the total number of first UV map texture coordinate entries for the surface, call the [getNumTexCoords0()](#getNumTexCoords0_int_int) method.
- *int* **surface** - Mesh surface number.

### Return value

First UV map texture coordinates.
## vec2 getTexCoord1 ( int num , int surface )

Returns second UV map texture coordinates for the given [triangle vertex](../../../api/library/rendering/class.mesh_usc.md#tvertex) of the given surface.
### Arguments

- *int* **num** - [Triangle vertex](../../../api/library/rendering/class.mesh_usc.md#tvertex) number in the range from 0 to the total number of second UV map texture coordinate entries of the given surface. > **Notice:** To get the total number of second UV map texture coordinate entries for the surface, call the [getNumTexCoords1()](#getNumTexCoords1_int_int) method.
- *int* **surface** - Mesh surface number.

### Return value

Second UV map texture coordinates.
## int getTIndex ( int num , int surface )

Returns the [triangle index](../../../api/library/rendering/class.mesh_usc.md#tindices) for the given surface by using the index number.
### Arguments

- *int* **num** - Vertex number in the range from 0 to the total number of triangle indices for the given surface. > **Notice:** To get the total number of triangle indices for the given surface, use the [getNumTIndices()](#getNumTIndices_int_int) method.
- *int* **surface** - Mesh surface number.

### Return value

Triangle index.
## vec3 getVertex ( int num , int surface , int target = 0 )

Returns coordinates of the given [coordinate vertex](../../../api/library/rendering/class.mesh_usc.md#cvertex) of the given surface target.
### Arguments

- *int* **num** - [Coordinate vertex](../../../api/library/rendering/class.mesh_usc.md#cvertex) number in the range from 0 to the total number of coordinate vertices for the given surface. > **Notice:** To get the total number of coordinate vertices for the given surface, use the [getNumCVertex()](../../../api/library/rendering/class.mesh_usc.md#getNumCVertex_int_int) method.
- *int* **surface** - Mesh surface number.
- *int* **target** - Surface target number. The default value is 0.

### Return value

Vertex coordinates.
## void setBoneWorldTransformWithChildren ( int bone , Mat4 transform )

Sets the transformation for the given bone and all of its children in the world coordinate space (considering node transformations).
> **Notice:** Bones can be scaled only uniformly.


### Arguments

- *int* **bone** - Bone number.
- *Mat4* **transform** - Transformation matrix in the world space.

## void setBoneWorldTransform ( int bone , Mat4 transform )

Sets the transformation for the given bone in the world coordinate space.
> **Notice:** Bones can be scaled only uniformly.


### Arguments

- *int* **bone** - Bone number.
- *Mat4* **transform** - Transformation matrix in the world space.

## Mat4 getBoneWorldTransform ( int bone )

Returns the current transformation matrix applied to the bone in the world coordinate space (considering node transformations).
### Arguments

- *int* **bone** - Bone number.

### Return value

Transformation matrix in the world space.
## void getObjectPose ( SkeletonPoseMatrix out_pose )

Writes the current object-space bone transforms (the result of blending all animation layers) into the specified [SkeletonPoseMatrix](../../../api/library/animations/skeletal/class.skeletonposematrix_usc.md).
### Arguments

- *[SkeletonPoseMatrix](../../../api/library/animations/skeletal/class.skeletonposematrix_usc.md)* **out_pose** - Output pose to receive the object-space bone transforms.

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

## int findBone ( string name )

Searches for a bone with a given name.
### Arguments

- *string* **name** - Bone name.

### Return value

Bone number if found; otherwise, -1.
## int findSurfaceTarget ( int surface , string name )

Searches for a surface morph target with a given name.
### Arguments

- *int* **surface** - Mesh surface number.
- *string* **name** - Name of the morph target.

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
## void getBlendingLayersPose ( SkeletonPoseDecomposed pose )

Writes the final blended pose (the result of blending all enabled animation layers according to their weights) into the specified [SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_usc.md). This provides the decomposed (position, rotation, scale) representation of the blended animation state.
### Arguments

- *[SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_usc.md)* **pose** - Output pose to receive the blended result.

## static int type ( )

Returns the type of the node.
### Return value

[Node](../../../api/library/nodes/class.node_usc.md) type identifier.
## void updateSkinned ( )

Forces update of all bone transformations.
## void setBindNode ( int bone , Node node )

Sets a new node whose transformation is to be used to control the transformation of the bone with the specified number.
### Arguments

- *int* **bone** - Number of the bone to be controlled by the specified node, in the range from 0 to the [total number of bones](#getNumBones_int).
- *[Node](../../../api/library/nodes/class.node_usc.md)* **node** - Node whose transformation is used to control the transformation of the bone.

## void removeBindNodeByBone ( int bone )

Removes the assigned bind node from the bone with the specified number.
### Arguments

- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).

## void removeBindNodeByNode ( Node node )

Removes the specified bind node.
### Arguments

- *[Node](../../../api/library/nodes/class.node_usc.md)* **node** - Bind node to be removed.

## void removeAllBindNode ( )

Removes all assigned bind nodes.
## Node getBindNode ( int bone )

Returns the bind node currently assigned to the bone with the specified number.
### Arguments

- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).

### Return value

Node whose transformation is used to control the transformation of the bone if it is assigned; otherwise - nullptr.
## void setBindNodeSpace ( int bone , int space )

Sets a new value indicating which transformation of the bind node (*World* or *Local*) is to be used to override the transformation of the specified bone.
### Arguments

- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).
- *int* **space** - Type of transformation of the bind node to be used to override the transformation of the specified bone, one of the [*NODE_SPACE**](#NODE_SPACE_LOCAL) values.

## int getBindNodeSpace ( int bone )

Returns the current value indicating which transformation of the bind node (*World* or *Local*) is to be used to override the transformation of the specified bone.
### Arguments

- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).

### Return value

Type of transformation of the bind node to be used to override the transformation of the specified bone, one of the [*NODE_SPACE**](#NODE_SPACE_LOCAL) values.
## void setBindBoneSpace ( int bone , int space )

Sets a value indicating which transformation of the specified bone is to be overridden by the bind node's transformation.
### Arguments

- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).
- *int* **space** - Type of transformation of the specified bone to be overridden by the bind node's transformation, one of the [*BONE_SPACE**](#BONE_SPACE_LOCAL) values.

## int getBindBoneSpace ( int bone )

Returns the current value indicating which transformation of the specified bone is to be overridden by the bind node's transformation.
### Arguments

- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).

### Return value

Current type of transformation of the specified bone overridden by the bind node's transformation, one of the [*BONE_SPACE**](#BONE_SPACE_LOCAL) values.
## void setBindMode ( int bone , int mode )

Sets a new type of blending of bind node's and bone's transformations.
### Arguments

- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).
- *int* **mode** - New type of blending of bind node's and bone's transformations:

  - **OVERRIDE** - replace bone's transformation with the transformation of the node.
  - **ADDITIVE** - node's transformation is added to the current transformation of the bone.

## int getBindMode ( int bone )

Returns the current type of blending of bind node's and bone's transformations.
### Arguments

- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).

### Return value

Current type of blending of bind node's and bone's transformations:
- **OVERRIDE** - replace bone's transformation with the transformation of the node.
- **ADDITIVE** - node's transformation is added to the current transformation of the bone.


## void setBindNodeOffset ( int bone , Mat4 offset )

Sets a new transformation matrix to be applied to the node's transformation before applying it to bone's transformation. This parameter serves for the purpose of additional correction of the node's transform for the bone's basis.
### Arguments

- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).
- *Mat4* **offset** - Transformation matrix applied to the node's transformation before applying it to bone's transformation.

## Mat4 getBindNodeOffset ( int bone )

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

## void setIKChainEnabled ( int enabled , int chain_id )

Sets a value indicating if the [IK chain](#ik_chains) with the specified ID is enabled.
### Arguments

- *int* **enabled** - Set **1** to enable IK chain with the specified ID, or **0** - to disable it.
- *int* **chain_id** - IK chain ID.

## int isIKChainEnabled ( int chain_id )

Returns a value indicating if the [IK chain](#ik_chains) with the specified ID is enabled.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

**1** if the IK chain with the specified ID is enabled; otherwise, **0**.
## void setIKChainWeight ( float weight , int chain_id )

Sets a new weight for the [IK chain](#ik_chains) with the specified ID. Weight value defines the impact of the target position on the last joint of the chain.
### Arguments

- *float* **weight** - New weight value to be set in the [0.0f, 1.0f] range. *Higher* values increase the impact.
- *int* **chain_id** - IK chain ID.

## float getIKChainWeight ( int chain_id )

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
## int getIKChainNumBones ( int chain_id )

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

## int getIKChainBone ( int bone_num , int chain_id )

Returns the index of the bone with the specified number (within the chain) from the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *int* **bone_num** - Bone number.
- *int* **chain_id** - IK chain ID.

### Return value

Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).
## void setIKChainTargetPosition ( Vec3 position , int chain_id )

Sets new local coordinates of the target position of the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *Vec3* **position** - New local coordinates of the target position to be set for the IK chain with the specified ID.
- *int* **chain_id** - IK chain ID.

## Vec3 getIKChainTargetPosition ( int chain_id )

Returns the current local coordinates of the target position of the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

Local coordinates of the target position of the IK chain with the specified ID.
## void setIKChainTargetWorldPosition ( Vec3 position , int chain_id )

Sets new world coordinates of the target position of the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *Vec3* **position** - New world coordinates of the target position to be set for the IK chain with the specified ID.
- *int* **chain_id** - IK chain ID.

## Vec3 getIKChainTargetWorldPosition ( int chain_id )

Returns the current world coordinates of the target position of the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

World coordinates of the target position of the IK chain with the specified ID.
## void setIKChainPolePosition ( Vec3 position , int chain_id )

Sets a new pole position (in local coordinates) for the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *Vec3* **position** - New pole position (in local coordinates) to be set for the IK chain.
- *int* **chain_id** - IK chain ID.

## Vec3 getIKChainPolePosition ( int chain_id )

Returns the current pole position (in local coordinates) for the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

Pole position (in local coordinates) for the IK chain.
## void setIKChainPoleWorldPosition ( Vec3 position , int chain_id )

Sets a new pole position (in world coordinates) for the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *Vec3* **position** - New pole position (in world coordinates) to be set for the IK chain.
- *int* **chain_id** - IK chain ID.

## Vec3 getIKChainPoleWorldPosition ( int chain_id )

Returns the current pole position (in world coordinates) for the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

Pole position (in world coordinates) for the IK chain.
## void setIKChainUseEffectorRotation ( int use , int chain_id )

Sets a value indicating if the effector rotation is to be used for the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *int* **use** - **1** to use effector rotation for the IK chain with the specified ID; **0** - not to use.
- *int* **chain_id** - IK chain ID.

## int isIKChainUseEffectorRotation ( int chain_id )

Returns a value indicating if the effector rotation is to be used for the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

**1** if the effector rotation is to be used for the IK chain with the specified ID; otherwise, **0**.
## void setIKChainEffectorRotation ( quat rotation , int chain_id )

Sets the rotation of the end-effector (in local coordinates) of the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *quat* **rotation** - Quaternion that defines rotation (local coordinates) of the end-effector of the chain.
- *int* **chain_id** - IK chain ID.

## quat getIKChainEffectorRotation ( int chain_id )

Returns the current rotation (in local coordinates) of the end-effector of the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

Quaternion that defines rotation (local coordinates) of the end-effector of the chain.
## void setIKChainEffectorWorldRotation ( quat rotation , int chain_id )

Sets the rotation of the end-effector (in world coordinates) of the [IK chain](#ik_chains) with the specified ID.
### Arguments

- *quat* **rotation** - Quaternion that defines rotation (world coordinates) of the end-effector of the chain.
- *int* **chain_id** - IK chain ID.

## quat getIKChainEffectorWorldRotation ( int chain_id )

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

## int getIKChainNumIterations ( int chain_id )

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

## float getIKChainTolerance ( int chain_id )

Returns the current tolerance value to be used for the [IK chain](#ik_chains) with the specified ID. This value sets a threshold where the target is considered to have reached its destination position, and when the IK Solver stops iterating.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

Current tolerance value for the IK chain.
## void copyBoneTransforms ( const ObjectMeshSkinnedLegacy src )

Copies all bone transformations from the specified source skinned mesh.
### Arguments

- *const [ObjectMeshSkinnedLegacy](../../../api/library/objects/class.objectmeshskinnedlegacy_usc.md)* **src** - Source skinned mesh from which bone transforms are to be copied.

## int applyMeshProcedural ( ConstMeshSkinned mesh )

**[ Main Thread ]** Replaces the object's current geometry with the provided mesh and **uploads it to VRAM**. Can only be called if [procedural mode](#procedural_modification) is enabled via *[setMeshProceduralMode()()](../../...md#setMeshProceduralMode_int_void)*. If the source mesh contains compatible elements (e.g., bones, surfaces, skinning data) matching the original, then animations, morph targets, and other behaviors will continue to function without interruption. Otherwise, the mesh will remain static, with no animation or morphing applied.
> **Notice:** The procedural mesh remains in memory and will not be unloaded automatically.


### Arguments

- *ConstMeshSkinned* **mesh** - Source mesh.

### Return value

**1** if the information from the mesh is successfully copied into the procedural mesh, otherwise **0**.
## void setSurfaceTargetEnabled ( int surface , int target , int enabled )

Toggles the use of the morph target for the specified surface.
### Arguments

- *int* **surface** - Number of the surface, to which the morph target is to be appended.
- *int* **target** - Number of the morph target to be used.
- *int* **enabled** - **1** to enable the use of the morph target for the surface, **0** to disable it.

## int isSurfaceTargetEnabled ( int surface , int target )

Returns the value indicating if the use of the morph target for the specified surface is enabled.
### Arguments

- *int* **surface** - Number of the surface, to which the morph target is appended.
- *int* **target** - Number of the morph target.

### Return value

**1**if the use of the morph target for the surface is enabled, otherwise **0**.
## void setSurfaceTargetWeight ( int surface , int target , float weight )

Sets the weight of the morph target, i.e. the intensity of it affecting the surface vertices.
### Arguments

- *int* **surface** - Number of the surface, to which the morph target is appended.
- *int* **target** - Number of the morph target.
- *float* **weight** - Weight of the morph target.

## float getSurfaceTargetWeight ( int surface , int target )

Returns the weight of the morph target, i.e. the intensity of it affecting the surface vertices.
### Arguments

- *int* **surface** - Number of the surface, to which the morph target is appended.
- *int* **target** - Number of the morph target.

### Return value

Weight of the morph target.
## void setLayerBoneTransform ( int layer , int bone , mat4 transform )

Sets a transformation matrix for the given bone. The difference from the [setBoneTransform()](#setBoneTransform_int_mat4_void) function is that this method takes into account only the transformation in the specified animation layer (no blending is performed).
> **Notice:** The bone can be scaled only uniformly.


### Arguments

- *int* **layer** - Animation layer number.
- *int* **bone** - Bone number.
- *mat4* **transform** - Bone transformation matrix.

## mat4 getLayerBoneTransform ( int layer , int bone )

Returns a transformation matrix of the given bone relatively to the parent object.
> **Notice:** The difference from [getBoneTransform()](#getBoneTransform_int_mat4) is that this method takes into account only the transformation in the animation layer (no blending is done).


### Arguments

- *int* **layer** - Animation layer number.
- *int* **bone** - Bone number.

### Return value

Bone transformation matrix.
## mat4 getBoneRestLocalTransform ( int bone )

Returns the rest (bind pose) transformation of the specified bone in its local space relative to the parent bone.
### Arguments

- *int* **bone** - Bone number.

### Return value

Rest (bind pose) transformation matrix in the local bone space.
## void setLayerBonePosition ( int layer , int bone , vec3 position )

Sets the position for the given bone.
### Arguments

- *int* **layer** - Animation layer number.
- *int* **bone** - Bone number.
- *vec3* **position** - Bone position.

## vec3 getLayerBonePosition ( int layer , int bone )

Returns the position for the given bone.
### Arguments

- *int* **layer** - Animation layer number.
- *int* **bone** - Bone number.

### Return value

Bone position.
## void setLayerBoneRotation ( int layer , int bone , quat rotation )

Sets the rotation for the given bone.
### Arguments

- *int* **layer** - Animation layer number.
- *int* **bone** - Bone number.
- *quat* **rotation** - Bone rotation.

## quat getLayerBoneRotation ( int layer , int bone )

Returns the rotation for the given bone.
### Arguments

- *int* **layer** - Animation layer number.
- *int* **bone** - Bone number.

### Return value

Bone rotation.
## void setLayerBoneScale ( int layer , int bone , vec3 scale )

Sets the scale for the given bone.
### Arguments

- *int* **layer** - Animation layer number.
- *int* **bone** - Bone number.
- *vec3* **scale** - Bone scale.

## vec3 getLayerBoneScale ( int layer , int bone )

Returns the scale for the given bone.
### Arguments

- *int* **layer** - Animation layer number.
- *int* **bone** - Bone number.

### Return value

Bone scale.
## void setLayerFrameUsesEnabled ( int layer , int enabled )

Toggles the use of animation masks for bones in the specified layer.
### Arguments

- *int* **layer** - Animation layer number.
- *int* **enabled** - **1** to enable the use of animation masks for bones in the specified layer, **0** to disable it.

## int isLayerFrameUsesEnabled ( int layer )

Returns the value indicating if the use of animation masks for bones in the specified layer is enabled.
### Arguments

- *int* **layer** - Animation layer number.

### Return value

**1** if the use of animation masks for bones in the specified layer is enabled, otherwise **0**.
## void setLayerBoneFrameUses ( int layer , int bone , int uses )

Sets the value indicating which components of the frame are to be used to animate the specified bone of the given animation layer.
### Arguments

- *int* **layer** - Animation layer number.
- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).
- *int* **uses** - Value indicating frame components to be used.

## int getLayerBoneFrameUses ( int layer , int bone )

Returns the value indicating which components of the frame are to be used to animate the specified bone of the given animation layer.
### Arguments

- *int* **layer** - Animation layer number.
- *int* **bone** - Number of the bone, in the range from 0 to the [total number of bones](#getNumBones_int).

### Return value

Value indicating frame components to be used.
## void setLayerPose ( int layer , SkeletonPoseDecomposed pose )

Sets the bone transforms for the specified animation layer from the given [SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_usc.md). This overwrites all bone transforms in the layer with the values from the pose.
### Arguments

- *int* **layer** - Animation layer number.
- *[SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_usc.md)* **pose** - Pose to apply to the layer.

## void getLayerPose ( int layer , SkeletonPoseDecomposed out_pose )

Writes the bone transforms of the specified animation layer into the given [SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_usc.md).
### Arguments

- *int* **layer** - Animation layer number.
- *[SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_usc.md)* **out_pose** - Output pose to receive the layer bone transforms.

## int getLayerNumFrames ( int layer )

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
## float getLayerFrame ( int layer )

Returns the frame number passed as the time argument on the last [setLayerFrame()](#setLayerFrame_int_float_int_int_float) call.
### Arguments

- *int* **layer** - Animation layer number.

### Return value

Frame number.
## int getLayerFrameFrom ( int layer )

Returns the start frame passed as the from argument on the last [setLayerFrame()](#setLayerFrame_int_float_int_int_float) call.
### Arguments

- *int* **layer** - Animation layer number.

### Return value

Start frame.
## int getLayerFrameTo ( int layer )

Returns the end frame passed as the to argument on the last [setLayerFrame()](#setLayerFrame_int_float_int_int_float) call.
### Arguments

- *int* **layer** - Animation layer number.

### Return value

End frame.
## long getAnimationResourceID ( string path )

Returns the unique animation ID using the path to it. This method also loads the animation if it hasn't been loaded yet.
### Arguments

- *string* **path** - Path to the animation file. The path can be represented by either a path to the file or its [GUID](../../../principles/filesystem/index.md#guids), which is the recommended approach. After loading the animation, its internal representation is identified by the path when using *[setLayerAnimationFilePath](#setLayerAnimationFilePath_int_cstr_void)* , etc. > **Notice:** When you [import](../../../editor2/fbx/index.md) your model with animations from an FBX container, the following path to your `*.anim` files should be used: `<path_to_your_fbx_file>/<file.fbx>/<your_anim_file.anim>` > For example: *object->setLayerAnimationFilePath(0,"models/soldier/soldier.fbx/run.anim");*

### Return value

The unique animation ID.
## void setLayerAnimationFilePath ( int layer , string path )

Sets the path to animation for the given animation layer.
### Arguments

- *int* **layer** - Layer number.
- *string* **path** - Path to the animation file. > **Notice:** When you [import](../../../editor2/fbx/index.md) your model with animations from an FBX container, the following path to your `*.anim` files should be used: **<path_to_your_fbx_file>/<file.fbx>/<your_anim_file.anim>** > For example: *object->setLayerAnimationFilePath(0,"models/soldier/soldier.fbx/run.anim");*

## string getLayerAnimationFilePath ( int layer )

Returns the path to animation for the given animation layer.
### Arguments

- *int* **layer** - Layer number.

### Return value

Path to the animation file.
## void setLayerAnimationResourceID ( int layer , long resource_id )

Sets the animation for the layer using the unique animation ID.
### Arguments

- *int* **layer** - Layer number.
- *long* **resource_id** - The unique animation ID.

## long getLayerAnimationResourceID ( int layer )

Returns the unique ID of the animation used for the layer.
### Arguments

- *int* **layer** - Layer number.

### Return value

The unique animation ID.
## mat4 getBoneBindLocalTransform ( int bone )

Returns the bone transformation matrix of the bind pose relatively to the parent bone.
> **Notice:** To get the bind pose transformation matrix in the object space, use [getBoneBindObjectTransform()](#getBoneBindObjectTransform_int_mat4).


### Arguments

- *int* **bone** - Bone number.

### Return value

Bind pose transformation matrix.
## mat4 getBoneBindLocalITransform ( int bone )

Returns the inverse bone transformation matrix of the bind pose relatively to the parent bone.
> **Notice:** To get the bind pose transformation matrix in the object space, use [getBoneBindObjectITransform()](#getBoneBindObjectITransform_int_mat4).


### Arguments

- *int* **bone** - Bone number.

### Return value

Inverse bind pose transformation matrix.
## mat4 getBoneBindObjectTransform ( int bone )

Returns the bone transformation matrix of the bind pose in the object space.
> **Notice:** To get the bind pose transformation matrix relatively to the parent bone, use [getBoneBindLocalTransform()](#getBoneBindLocalTransform_int_mat4).


### Arguments

- *int* **bone** - Bone number.

### Return value

Bind pose transformation matrix.
## mat4 getBoneBindObjectITransform ( int bone )

Returns the inverse bone transformation matrix of the bind pose in the object space.
> **Notice:** To get the bind pose transformation matrix relatively to the parent bone, use [getBoneBindLocalITransform()](#getBoneBindLocalITransform_int_mat4).


### Arguments

- *int* **bone** - Bone number.

### Return value

Inverse bind pose transformation matrix.
## mat4 getBoneSkinningTransform ( int bone )

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

## int getNumLookAtChains ( )

Returns the total number of LookAtChains.
### Return value

Total number of LookAtChains.
## int getLookAtChainID ( int num )

Returns the ID of LookAtChain by its index.
### Arguments

- *int* **num** - Index of LookAtChain.

### Return value

LookAtChain ID.
## void setLookAtChainEnabled ( int enabled , int chain_id )

Toggles the use of LookAtChain.
### Arguments

- *int* **enabled** - **1** to enable LookAtChain, **0** to disable it.
- *int* **chain_id** - LookAtChain ID.

## int isLookAtChainEnabled ( int chain_id )

Checks if LookAtChain is enabled.
### Arguments

- *int* **chain_id** - LookAtChain ID.

### Return value

**1** if LookAtChain is enabled, otherwise **0**.
## void setLookAtChainConstraint ( int constraint , int chain_id )

Configures the type of bone constraint for the solver of the specified chain.
### Arguments

- *int* **constraint** - The type of bone constraint for the solver.
- *int* **chain_id** - LookAtChain ID.

## int getLookAtChainConstraint ( int chain_id )

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

## float getLookAtChainWeight ( int chain_id )

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
## int getLookAtChainNumBones ( int chain_id )

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

## int getLookAtChainBone ( int bone_num , int chain_id )

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

## float getLookAtChainBoneWeight ( int bone_num , int chain_id )

Returns the additional local weight of the bone.
### Arguments

- *int* **bone_num** - The index of the bone in the chain.
- *int* **chain_id** - LookAtChain ID.

### Return value

The weight of the bone in the chain.
## void setLookAtChainBoneUp ( Vec3 up , int bone_num , int chain_id )

Sets the UP axis for the bone.
### Arguments

- *Vec3* **up** - The UP vector for the bone.
- *int* **bone_num** - The index of the bone in the chain.
- *int* **chain_id** - LookAtChain ID.

## Vec3 getLookAtChainBoneUp ( int bone_num , int chain_id )

Returns the UP axis for the bone.
### Arguments

- *int* **bone_num** - The index of the bone in the chain.
- *int* **chain_id** - LookAtChain ID.

### Return value

The UP vector for the bone.
## void setLookAtChainBoneAxis ( Vec3 axis , int bone_num , int chain_id )

Sets the axis that is directed at the target of LookAtChain.
### Arguments

- *Vec3* **axis** - The axis that is directed at the target.
- *int* **bone_num** - The index of the bone in the chain.
- *int* **chain_id** - LookAtChain ID.

## Vec3 getLookAtChainBoneAxis ( int bone_num , int chain_id )

Returns the axis that is directed at the target of LookAtChain.
### Arguments

- *int* **bone_num** - The index of the bone in the chain.
- *int* **chain_id** - LookAtChain ID.

### Return value

The axis that is directed at the target.
## void setLookAtChainTargetPosition ( Vec3 position , int chain_id )

Sets the position for the rotation in the object space.
### Arguments

- *Vec3* **position** - The position for the rotation in the object space.
- *int* **chain_id** - LookAtChain ID.

## Vec3 getLookAtChainTargetPosition ( int chain_id )

Returns the position for the rotation in the object space.
### Arguments

- *int* **chain_id** - LookAtChain ID.

### Return value

The position for the rotation in the object space.
## void setLookAtChainTargetWorldPosition ( Vec3 position , int chain_id )

Sets the position for the rotation in the world space.
### Arguments

- *Vec3* **position** - The position for the rotation in the world space.
- *int* **chain_id** - LookAtChain ID.

## Vec3 getLookAtChainTargetWorldPosition ( int chain_id )

Returns the position for the rotation in the world space.
### Arguments

- *int* **chain_id** - LookAtChain ID.

### Return value

The position for the rotation in the world space.
## void setLookAtChainPolePosition ( Vec3 position , int chain_id )

Sets the position of the pole vector in the object space.
### Arguments

- *Vec3* **position** - The position of the pole vector in the object space.
- *int* **chain_id** - LookAtChain ID.

## Vec3 getLookAtChainPolePosition ( int chain_id )

Returns the position of the pole vector in the object space.
### Arguments

- *int* **chain_id** - LookAtChain ID.

### Return value

The position of the pole vector in the object space.
## void setLookAtChainPoleWorldPosition ( Vec3 position , int chain_id )

Sets the position of the pole vector in the world space.
### Arguments

- *Vec3* **position** - The position of the pole vector in the world space.
- *int* **chain_id** - LookAtChain ID.

## Vec3 getLookAtChainPoleWorldPosition ( int chain_id )

Returns the position of the pole vector in the world space.
### Arguments

- *int* **chain_id** - LookAtChain ID.

### Return value

The position of the pole vector in the world space.
## int getIKChainID ( int num )

Returns the IKChain ID by its index.
### Arguments

- *int* **num** - IKChain index.

### Return value

IKChain ID.
## void setIKChainConstraint ( int constraint , int chain_id )

Configures the type of bone constraint for the solver of the specified chain.
### Arguments

- *int* **constraint** - The type of bone constraint for the solver.
- *int* **chain_id** - IK chain ID.

## int getIKChainConstraint ( int chain_id )

Returns the type of bone constraint for the solver of the specified chain.
### Arguments

- *int* **chain_id** - IK chain ID.

### Return value

The type of bone constraint for the solver.
## int addBoneConstraint ( int bone )

Adds the rotation constraint to the specified bone.
### Arguments

- *int* **bone** - The bone index in the mesh.

### Return value

The constraint index.
## void removeBoneConstraint ( int constraint_num )

Removes the specified bone rotation constraint.
### Arguments

- *int* **constraint_num** - The constraint index.

## int findBoneConstraint ( int bone )

Returns the rotation constraint index for the specified bone.
### Arguments

- *int* **bone** - The bone index in the mesh.

### Return value

The constraint index.
## void setBoneConstraintEnabled ( int enabled , int constraint_num )

Enables the use of the rotation constraint for the bone.
### Arguments

- *int* **enabled** - **1** to enable the use of the rotation constraint for the bone, **0** to disable it.
- *int* **constraint_num** - The constraint index.

## int isBoneConstraintEnabled ( int constraint_num )

Returns the value indicating if the use of the rotation constraint for the bone is enabled.
### Arguments

- *int* **constraint_num** - The constraint index.

### Return value

**1** if the use of the rotation constraint for the bone is enabled, otherwise **0**.
## int getBoneConstraintBoneIndex ( int constraint_num )

Returns the index of the bone for which the rotation constraint is set.
### Arguments

- *int* **constraint_num** - The constraint index.

### Return value

The bone index in the mesh.
## void setBoneConstraintYawAxis ( vec3 axis , int constraint_num )

Sets the yaw axis for the bone rotation constraint.
### Arguments

- *vec3* **axis** - The yaw axis.
- *int* **constraint_num** - The constraint index.

## vec3 getBoneConstraintYawAxis ( int constraint_num )

Returns the yaw axis for the bone rotation constraint.
### Arguments

- *int* **constraint_num** - The constraint index.

### Return value

The yaw axis.
## void setBoneConstraintPitchAxis ( vec3 axis , int constraint_num )

Sets the pitch axis for the bone rotation constraint.
### Arguments

- *vec3* **axis** - The pitch axis.
- *int* **constraint_num** - The constraint index.

## vec3 getBoneConstraintPitchAxis ( int constraint_num )

Returns the pitch axis for the bone rotation constraint.
### Arguments

- *int* **constraint_num** - The constraint index.

### Return value

The pitch axis.
## void setBoneConstraintRollAxis ( vec3 axis , int constraint_num )

Sets the roll axis for the bone rotation constraint.
### Arguments

- *vec3* **axis** - The roll axis.
- *int* **constraint_num** - The constraint index.

## vec3 getBoneConstraintRollAxis ( int constraint_num )

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

## float getBoneConstraintYawMinAngle ( int constraint_num )

Returns the minimum angle restricting the bone rotation along the yaw axis.
### Arguments

- *int* **constraint_num** - The constraint index.

### Return value

The minimum rotation angle.
## float getBoneConstraintYawMaxAngle ( int constraint_num )

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

## float getBoneConstraintPitchMinAngle ( int constraint_num )

Returns the minimum angle restricting the bone rotation along the pitch axis.
### Arguments

- *int* **constraint_num** - The constraint index.

### Return value

The minimum rotation angle.
## float getBoneConstraintPitchMaxAngle ( int constraint_num )

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

## float getBoneConstraintRollMinAngle ( int constraint_num )

Returns the minimum angle restricting the bone rotation along the roll axis.
### Arguments

- *int* **constraint_num** - The constraint index.

### Return value

The minimum rotation angle.
## float getBoneConstraintRollMaxAngle ( int constraint_num )

Returns the maximum angle restricting the bone rotation along the roll axis.
### Arguments

- *int* **constraint_num** - The constraint index.

### Return value

The maximum rotation angle.
## int isLayerAnimationStreaming ( int layer )

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

## int loadAsyncRender ( )

Requests asynchronous loading of the mesh for rendering. The mesh becomes available in one of the following frames, so the object keeps rendering whatever it already has until then.
### Return value

true if the request has been queued; otherwise, false.
## int loadForceRender ( )

Loads the mesh for rendering immediately, blocking until it is done.
### Return value

true if the mesh has been loaded; otherwise, false.
