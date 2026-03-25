# Cloth Body


**Cloth body** enables physical simulation of textiles, clothing and foliage, as well as sheets of any soft material. A cloth can be torn to pieces and also it can be pinned to the following types of bodies:


- [Rigid body](../../../../principles/physics/bodies/rigid/index.md)
- [Ragdoll body](../../../../principles/physics/bodies/ragdoll/index.md)
- [Dummy body](../../../../principles/physics/bodies/dummy/index.md)


To pin a cloth to a body so it would hang like a cape or a curtain, use the [Particles Joint](../../../../principles/physics/joints/index.md#particles).


*Cloth body* greatly enhances the appearance of dressed characters (otherwise entirely animated) and saves the time of game artists. However, simulation of this type of body is quite costly and it is strongly recommended to use [distance optimization](#distance) to avoid performance hits.


> **Notice:** *Cloth body* can be assigned only to **[Dynamic mesh](../../../../objects/objects/mesh_dynamic/index.md)** objects.


### See also


- *[BodyCloth](../../../../api/library/physics/class.bodycloth_cpp.md)* class
- An [example](../../../../code/usage/cloth_particle_joint/index_cpp.md) illustrating the use of *Cloth body* and [Particles Joint](../../../../principles/physics/joints/index.md#particles)
- Fragment of the video tutorial on physics illustrating [simulation of cloth using *Cloth body*](https://youtu.be/w_GJrE-6HtI?t=890s)


## Mesh Requirements


In most cases, it is important that polygon triangulation of the mesh, for which *Cloth body* is generated, is as illustrated! Otherwise, it may not [stretch](#stretching) properly and evenly in all directions.


[![Required mesh triangulation](mesh_sample_sm.jpg)](mesh_sample.jpg)


For example in *3ds Max*, mesh topology needs to be edited manually: choose *Modify > Selection > Edit Edges* rollout and click *Turn* to turn the triangles in a poly.


## Mass-Spring Simulation Model


*Cloth body* is modeled as set of point masses (particles) located in the mesh vertices. Each particle is represented with a sphere shape and is linked together with other particles by inner spring joints that are located along the mesh edges. Inner joints allow to recreate mesh topology, on the one hand, and constrain stretching and folding, on the other.


Each particle is characterized by a position, mass and velocity and has a constant spherical shape with a set [radius](#radius). The total [mass](../../../../principles/physics/bodies/index.md#mass) of the whole body is equally distributed among them. In accordance with Newton's second law particles can be acted upon by a [force](../../../../principles/physics/bodies/index.md#force) or an [impulse](../../../../principles/physics/bodies/index.md#impulse) applied by inner joints and external forces ([collision](../../../../principles/physics/collision/index.md#collision_response), [gravity](../../../../editor2/settings/physics_global/index.md#gravity), air resistance, wind, etc.).


Self-collision of the particles and collisions between different cloth bodies are not calculated. However, the cloth interacts with environment by colliding with other physical bodies if the **Collision** box is checked. Its behavior in case of contact is controlled by such parameters as [friction](../../../../principles/physics/bodies/index.md#friction) and [restitution](../../../../principles/physics/bodies/index.md#restitution). Selective physical interaction is available via corresponding [bitmasks](../../../../principles/bit_masking/index.md#collision_mask).


Thus, *Cloth body* can be regarded as constrained system of rigid particles and therefore shares some parameters with rigid bodies:


- **[mass](../../../../principles/physics/bodies/index.md#mass)**
- **[friction](../../../../principles/physics/bodies/index.md#friction)**
- **[restitution](../../../../principles/physics/bodies/index.md#restitution)**
- **[linear and angular damping](../../../../principles/physics/bodies/index.md#damping)**


### Particle Radius


As it was already mentioned, each particle is a sphere with a set **radius**. That brings the following:


- Cloth particles use continuous collision detection, so higher values are preferable for more robust behavior. Collisions between the particles are not calculated and should not be considered when setting a radius. Be careful, however, as particles too big in diameter can provide incorrect interaction with environment (twitching or blowing up of the cloth). Too low radius results in poor collision handling.
- As cloth particles are approximated with spheres, the cloth never lies flat on the ground or tightly adheres to the surfaces. There is always some gap that corresponds in size to set radius.


> **Notice:** An object can pass through the cloth, when the particle radius is small and the cloth is [stretched](#stretching). The reason is that continuous collision detection is performed only for particle spheres located in vertices of cloth mesh.


### Joints Solver Iterations


The number of **iterations** controls the accuracy of the solution of cloth inner joints. This number indicates how many times the joints are solved per [physics frame](../../../../code/fundamentals/execution_sequence/index.md#framerates). Joints are solved in a random order to provide more predictable stretching results.


- **Low number of iterations** results in faster simulation. However, in this case the cloth is more prone to stretching and looks more elastic. The minimum value is 1.
- **High number of iterations** provides more accurate solution of constraints. In this case the cloth looks stiffer. The maximum value is 16. > **Notice:** Increased number of iterations is considerably expensive and at some point ceases to bring a noticeable benefit, so it should be kept within a reasonable cost-effectiveness limit.


Increasing the number of iterations may help to avoid twitching of a cloth.


## Stretching and Folding


A cloth may be deformed by **stretching** and **folding**. These deformations are controlled with joint constraints of two types:


- **[Linear restitution](#linear_restitution)** controls stretching.
- **[Angular restitution](#angular_restitution)** controls folding.


With these types of constraints, it is possible to obtain the desired look and feel of the cloth and simulate a variety of different deformable materials ranging from a stiff carton to soft lycra.


### Linear Restitution


**Linear restitution** determines how far the cloth particles can be stretched apart from each other. It enforces cloth joints to restore the distance that was between the vertices of the original mesh:


- By the maximum value of 1, the particles spring back with great force and the cloth is hard to stretch. It gives the effect of stiff non-stretch cloth, e.g. linen or tweed.
- The **lower** the value, the easier the particles are moved away from each other and the more stretchable and elastic the cloth is, e.g. nylon or spandex. > **Notice:** 0 and near zero values are not allowed because they cause unstable simulation and blowing up of the cloth.


### Angular Restitution


**Angular restitution** determines the possible angle between cloth triangles that are formed by particles. It constrains the folding of the cloth by enforcing joints to keep the angle that was between triangles of the original mesh:


- By the maximum value of 1, the angles tend to be retained and the cloth resists folding. The cloth appears to be stiff and wrinkle-free (for example, paper). > **Notice:** The maximum value may provide unsteady behavior.
- By the minimum value of 0, the cloth can be easily folded and bent in any direction, regardless of the original topology of the mesh.


> **Notice:** If the cloth is too stretchy and rubbery, try one of the following:
>
>
> - Set linear restitution to 1.
> - Increase the number of joints solver [iterations](#iterations).
> - Use the mesh with fewer vertices.


## Rigidity of Motion


**Rigidity** parameter is an additional constraint of the cloth motion to make it stiffer and more inflexible. For that purpose, linear and angular velocities of each cloth particle are corrected according to the total velocities interpolated for all the particles.


- The minimum value of 0, makes the cloth elastic, flexible and easily deformable.
- The maximum value of 1, makes the cloth stiffer and less prone to deformation.


## Tearing


When the cloth is stretched beyond its elastic limit or folded, it tears and shreds into pieces. **Tearing** is caused by applying the force or collision with a physical body, and depends on the cloth stiffness (controlled by [linear](#linear_restitution) and [angular restitution](#angular_restitution) parameters). For example, imagine the cannonball hitting the sail and leaving the hole in it. The cloth is torn only along the edges of cloth triangles, splitting mesh vertices and duplicating particles.


![Cloth tearing](cloth_tearing.jpg)

*Tearing of cloth*


> **Notice:** If torn pieces of cloth fall onto one plane, they cause Z-fighting.


### Linear Threshold Distance


**Linear threshold** sets the distance limit for [stretching](#linear_restitution) the cloth. When two particles move away from each other further than this limit, joints that connect them break and the tear appears.


- If set to infinity (inf), the cloth is stretched without tearing. This value is set by default.


### Angular Threshold Angle


Same as linear threshold, **angular threshold** represents a maximum angle to [fold](#angular_restitution) the cloth relative to its initial state. If cloth triangles are bent any further, the joint breaks and triangles are separated along the adjacent edge.


- If set to infinity (inf), the cloth is folded without tearing. This value is set by default. > **Notice:** It is recommended to keep the angular threshold lower or equal to 180 degrees.


## Optimizing Simulation


Updating each frame a huge number of objects located far away from the camera that are hardly distinguishable or observed as a mass is a waste of resources.


To improve performance and avoid the excessive load, simulation of the cloth can be [updated with a reduced framerate](../../../../principles/world_management/index.md#periodic_update). When the player is out of the area specified by the **Update Distance Limit**, the cloth stops to be updated and freezes statically.


The set of frame rates given below enables you to specify how often the cloth simulation should be updated when the object is visible, when only its shadow is visible, or when it is not visible at all.


![](../../../../principles/world_management/periodic_update.png)

*Parameters -> Physicstab ->Periodic Updatesection*


| FPS When Object Is Rendered To Viewport | Update rate value for the case when the object is rendered to viewport. |
|---|---|
| FPS When Only Object Shadows Are Rendered | Update rate value when the object itself is outside the viewing frustum, and only its shadow is rendered to viewport. |
| FPS When Object Is Not Rendered At All | Update rate value when both the object and its shadow are not rendered to the viewport. |
| Update Distance Limit | Distance from the camera up to which the object should be updated. |


> **Notice:** These values are not fixed and can be adjusted by the Engine at any time to ensure best performance.


This feature is enabled with default settings ensuring optimum performance and can be adjusted per-object in UnigineEditor or via API at run time.


> **Warning:** Please be aware that using reduced update frame rate for an object should be carefully considered in your application's logic, as it may lead to various issues with rendering skinned and dynamic meshes (flickering due to misalignment, e.g. in case of attaching a cloth to a skinned mesh).


## Assigning a Cloth Body


To assign a *Cloth body* to an object via [UnigineEditor](../../../../editor2/index.md) perform the following steps:


1. Open the *[World Hierarchy](../../../../editor2/interface/index.md#world_hierarchy)* window.
2. Select a **[Dynamic Mesh](../../../../objects/objects/mesh_dynamic/index.md)** object to assign a *Cloth body* to. > **Notice:** Make sure that object's mesh meets [requirements](#requirements)!
3. Go to the ***Physics*** tab in the *[Parameters](../../../../editor2/interface/index.md#parameters)* window and assign a physical [body](../../../../principles/physics/bodies/index.md) to the selected object by selecting *Body -> **Cloth***. ![Adding a body](../add_body.jpg)
4. Set body's name and change other parameters, if necessary.


## Attaching the Cloth


[![I'm Batman!](attached_cloth_sm.jpg)](attached_cloth.jpg)

*Cloth attached to animated character*


A cloth can be attached to the following types of bodies:


- [Rigid body](../../../../principles/physics/bodies/rigid/index.md)
- [Ragdoll body](../../../../principles/physics/bodies/ragdoll/index.md)
- [Dummy body](../../../../principles/physics/bodies/dummy/index.md)


To attach a cloth to a body use a *[Particles Joint](../../../../principles/physics/joints/index.md#particles)*. In case of *Rigid* bodies (either static, or dynamic) and *Dummy* bodies, pinned particles stay fixed in their position and follow transformations of attached objects pulling the cloth with it.


1. Select *Rigid body, Ragdoll body* or *Dummy body*.
2. Add *Particles Joint*.
3. Specify *Cloth body*.
4. Adjust the pinning area using the *Threshold* and *Size* parameters of the particles joint.


> **Notice:** To ensure stable simulation, set appropriate masses of the cloth and the attached body. Unbalanced masses may cause twitching of the cloth joints.


### Attachment to Skinned Mesh


Convincing simulation of the clothing on a skinned character requires a different approach. To follow bones transformations, each vertex of the cloth that is found in the *[Particles Joint](../../../../principles/physics/joints/index.md#particles)* area is mapped to the nearest skinned mesh vertex (up to the distance specified by the **Threshold** parameter of the particles joint).


> **Notice:** It is not recommended to attach the cloth directly to the skinned character, because difference in topologies may result in visual artifacts. Instead of it, it is better to create an identical cloth surface on the skinned mesh character, make it invisible and attach a physical cloth to it.


For example, we need to create a cape that is glued to the shoulders of a skinned character while the rest flaps and folds loosely. It is done in the following steps:


1. When creating a *[Mesh Skinned](../../../../objects/objects/mesh_skinned_legacy/index.md)*, add a cape surface identical to the cape that the character would wear. It can be either a whole cape, or only its clipped part that needs to be pinned. The latter is preferable when complex clothing is simulated, which requires more flexible control over which parts to simulate physically and which ones to move with skinned character. In our case, it's cloth part over the shoulders.
2. Add skinned mesh that has a *[Ragdoll body](../../../../principles/physics/bodies/ragdoll/index.md)* assigned. Make sure that the cape surface is **enabled**.
3. Add a separate dynamic cloth mesh and synchronize its position with skinned character. Turn off physical simulation (**CTRL + SPACE**) and [assign](#assign) a *Cloth body*.
4. [Attach](#attaching) *Cloth body* to *Ragdoll body*. If the **Threshold** distance of the particles joint is set low enough, the physical cape will be automatically attached only to the cape surface (i.e. shoulders). After that, the cape surface is simply disabled and does not provide any load at all.
