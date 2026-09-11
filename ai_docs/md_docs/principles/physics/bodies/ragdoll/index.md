# Ragdoll Body


**Ragdoll body** allows applying physical forces to [bone-animated](../../../../objects/objects/mesh_skinned_legacy/index.md) characters, such as [inverse kinematics](#combined) and procedural animation of a death sequence.


[![Ragdoll animation](ragdolls_sm.jpg)](ragdolls.jpg)

*Ragdoll animation*


> **Notice:** *Ragdoll body* can be assigned to **[Mesh Skinned](../../../../objects/objects/mesh_skinned_legacy/index.md)** objects only.


### See also


- *[BodyRagdoll](../../../../api/library/physics/class.bodyragdoll_cpp.md)* class
- Fragment of the video tutorial on physics illustrating [inverse kinematics of a *Ragdoll body*](https://youtu.be/w_GJrE-6HtI?t=705s)


## Assigning a Ragdoll Body


To assign a *Ragdoll* body to an object in [UnigineEditor](../../../../editor2/index.md), perform the following steps:


1. In the *[World Nodes](../../../../editor2/interface/index.md#world_hierarchy)* window, select the **[Mesh Skinned](../../../../objects/objects/mesh_skinned_legacy/index.md)** object that you want to assign a *Ragdoll* body to.
2. Switch to the ***Physics*** tab in the *[Parameters](../../../../editor2/interface/index.md#parameters)* tab and select *Body -> **RagDoll***. ![Adding a body](../add_body.jpg)
3. Set the body name and proceed with [creating a skeleton](#create).


## Creating a Skeleton


*Ragdoll* body is requires a **skeleton** (or a **rig**), which is in fact a hierarchy of the character bones each represented by an *[Object Dummy](../../../../objects/objects/dummy/index.md)* with a *[Rigid](../../../../principles/physics/bodies/index.md#rigid_bodies_dynamics)* body assigned. These bones are connected by joints that limit their movement relative to each other, creating a realistic look.


When the *Ragdoll* body is assigned to the *Mesh Skinned* object, all the bones are **free**, i.e. not united into a skeleton. Click the ***Create*** button to configure the **Ragdoll bone generation parameters** and automatically generate a skeleton.


> **Notice:** To generate the skeleton properly, the mesh should be in the Reference Pose (T-pose for human-like characters). If animation has been already applied to the mesh, apply an animation with the static Reference Pose.


Automatic generation is performed on the basis of the following parameters:


![](bone_gen_parameters.png)


| Total Mass | Total [mass](../../../../principles/physics/bodies/index.md#mass) of the *Ragdoll* will be automatically distributed among all the shapes that approximate bones. By distribution, the volume that the shape occupies is taken into account. If the mass is changed afterwards, masses of all the shapes are recalculated. And the opposite way, if shape mass is changed, the total mass is modified correspondingly. |  |  |  |  |  |
|---|---|---|---|---|---|---|
| Approximation Error | The value that makes it possible to control the number of vertices in the resulting shape. Depending on the use case, the shape may be more or less detailed. - *Lower* values ensure a more accurate and close to the mesh approximated shape. - The maximum value of 1 provides quite rough approximation that may not cover all the mesh volume. |  |  |  |  |  |
| Volume Threshold | When creating a *Ragdoll*, small bones (like finger bones, for example) are rarely simulated. They are too insignificant to change the motion of the whole object, as their mass and volume is not sufficient for that. Volume threshold allows to merge all small adjacent bones, the volume of which is too small, into one shape: \| **Value = 0** (minimum): all the bones without exception are represented in rigid bodies and hence shapes. \| **Value = 1** (maximum): approximation shapes are big and follow only the major bones. Small bones are included in this volume, but their individual transformations are not considered in physical simulation. \| \|---\|---\| \| [![Minimum volume threshold](threshold0_sm.jpg)](threshold0.jpg) �� \| [![Maximum volume threshold](threshold1_sm.jpg)](threshold1.jpg) \| \| *Volume threshold defines whether all bones up to the smallest one should be simulated separately or merged into bigger shapes* \|  \| | **Value = 0** (minimum): all the bones without exception are represented in rigid bodies and hence shapes. | **Value = 1** (maximum): approximation shapes are big and follow only the major bones. Small bones are included in this volume, but their individual transformations are not considered in physical simulation. | [![Minimum volume threshold](threshold0_sm.jpg)](threshold0.jpg) �� | [![Maximum volume threshold](threshold1_sm.jpg)](threshold1.jpg) | *Volume threshold defines whether all bones up to the smallest one should be simulated separately or merged into bigger shapes* |
| **Value = 0** (minimum): all the bones without exception are represented in rigid bodies and hence shapes. | **Value = 1** (maximum): approximation shapes are big and follow only the major bones. Small bones are included in this volume, but their individual transformations are not considered in physical simulation. |  |  |  |  |  |
| [![Minimum volume threshold](threshold0_sm.jpg)](threshold0.jpg) �� | [![Maximum volume threshold](threshold1_sm.jpg)](threshold1.jpg) |  |  |  |  |  |
| *Volume threshold defines whether all bones up to the smallest one should be simulated separately or merged into bigger shapes* |  |  |  |  |  |  |
| Capsule Shape | This setting defines the approximation shape to be used for bones: - If enabled, the *Capsule* shape is used � it provides very fast physics simulation and continuous collision detection. - If disabled, *Convex hull* is used � it ensures more accurate approximation. If any other shape is required, approximation is to be done [manually](#manual). [![Approximation with capsules and convex hulls](approximation_shapes_sm.jpg)](approximation_shapes.jpg) *Approximation with capsules and convex hulls* > **Notice:** Remember that physical shapes don't need to reproduce the mesh precisely. Rough approximation provides physical interaction that is realistic and convincing enough. |  |  |  |  |  |


### Body Hierarchy for Bones


After the skeleton has been created, all the bones that participate in the physical body movement have rigid bodies and shapes and are marked as **bound** in the hierarchy. All the small bones not participating in physical body movement remain marked as **free**. If automatically generated shapes don't fit the object contours, they can be tuned manually till their approximation is satisfying enough.


The hierarchy of bodies and shapes that approximate bones may be **saved** into a `*.node` file and **loaded** from it. You can also **remove** the set hierarchy from the *Ragdoll* body and **create** it anew.


![Hierarchy of rigid bodies that represent bones](bones.png)


### Manual Editing of the Skeleton


It is also possible to edit or even create a skeleton manually. In this case you can use arbitrary shapes to approximate the skeleton bones.


To **edit the automatically created skeleton**, click the ***Save*** button and add the saved `*.node` file to the scene for editing.


> **Notice:** To visualize the the skeleton in the Editor, enable the corresponding option in *Helpers -> Physics -> Shapes*. All shapes available in the scene will be highlighted. The same can be done for joints.


To **create a skeleton manually** from scratch, follow these steps:


1. Create a *[Node Dummy](../../../../objects/nodes/dummy/index.md)* that will be a parent node for the future skeleton hierarchy.
2. Add a *Dummy* object as a child node. Assign a *[Rigid](../../../../principles/physics/bodies/rigid/index.md)* body to it and name the body after the bone it will represent. After that, approximate the bone with any necessary shape.
3. Create all *Rigid* bodies and shapes for the skeleton bones. Hierarchy is of no importance, only names of the bodies do � they should be the same as the names of the bones. If body names mismatch bone names, an error will occur.
4. Export the parent node into the `*.node` file.
5. Select the character and load this file for its *Ragdoll* body.
6. Add and set up joints that connect rigid bodies within the skeleton.


## Parameters


![](body_parameters.jpg)


In addition to the parameters available for the [rigid bodies](../../../../principles/physics/bodies/rigid/index.md#parameters), the following parameters can be adjusted to configure the *Ragdoll* body:


| Frame-Based | Toggles frame-based animation on and off. When disabled, bone transformations are conditioned by physics, instead of being based on skinned animation data. This option is available for both the [whole ragdoll body](#enable) and individually selected [bound bones](#combined). |
|---|---|
| Rigidity | Allows to additionally constrain the motion of the skeleton. This parameter determines how uniform the motion of *Ragdoll* parts is. To achieve that, both linear and angular velocities of each separate rigid body are corrected according to the total velocities interpolated from all the bodies. - By the minimum value of 0, all *Ragdoll* parts represented in rigid bodies move independently and unrestricted (of course, except for joint constrains). This gives an impression of loose and floppy movement. - By the maximum value of 1, *Ragdoll* parts move in a uniform and stiff manner, which may seem over-constrained. |


## Enabling Ragdoll Animation


When the character, for example, hits some obstacle or is shot and dies, it is necessary to turn off bone-based animation playback and simulate the character realistically falling according to the physical laws. When the **[Frame-based](#frame_based)** option is disabled, *Ragdoll body* is no longer driven by the bone transformations. It collapses according to [*Rigid body* dynamics](../../../../principles/physics/bodies/index.md#rigid_bodies_dynamics) ([masses](../../../../principles/physics/bodies/index.md#mass) of all rigid bodies, that represent parts of the skeleton, [velocity damping](../../../../principles/physics/bodies/index.md#damping), etc.), joint constraints and [Rigidity](#rigidity) of motion.


> **Notice:** Enabling the *Ragdoll* animation affects only the bones that were physically approximated. For example, small bones that were discarded based on the [volume threshold](#threshold), will still move. To prevent this from happening, mesh animation should be [stopped](../../../../api/library/objects/class.objectmeshskinnedlegacy_cpp.md#stop_void) explicitly.


### Combined Animation and Inverse Kinematics


The problem with pre-baked animation is that it does not offer proper environmental interaction. For example, when walking up or down the hill, character's feet do not land firmly on terrain. Or as it climbs the ladder, the hands have to tightly grab the rungs. This effect is achieved with combined animation: motion animation is played for the basic bones, while smaller bones (feet or hands, for example) are simulated physically.


**Frame-based animation** can be disabled for each of the rigid bodies that approximate bones. Instead of following specific bone transformation, rigid body sags loose under its own weight and connects to collider objects underneath it.


For instance, physically-driven motion of the leg requires disabling bone animation of the whole limb: thigh, calf, and foot. Inverse kinematics allows to properly position the chain of bones given the position of the lowest bone in the hierarchy, the foot. So when the character walks or runs, his foot collides with the ground, while the knee bends and straightens according to the joint constrain.


[![Inverse Kinematics](inverse_kinematics_sm.jpg)](inverse_kinematics.jpg)

*With inverse kinematics feet of the characters are tightly glued to the floor no matter how tilted the surface is*
