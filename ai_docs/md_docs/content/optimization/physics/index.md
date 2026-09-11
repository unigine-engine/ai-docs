# Physics Optimization


Computation of physical interactions can be very demanding. There are optimization techniques providing high performance and overall stability for your interactive projects.


![](physics.gif)


## Common Settings


Keep the [global physics settings](../../../editor2/settings/physics_global/index.md) at a reasonable demanding level.


> **Notice:** To configure physics settings, open the *Settings* window by choosing *Window -> Settings* in the main menu and select *Runtime -> World -> Physics* section.


![](common_settings.png)


- Specify the [**Distance**](../../../editor2/settings/physics_global/index.md#physics_distance) from the camera, from which physical interactions are not calculated. If the distance between the camera and the physics-based node exceeds this limit, the node freezes and its physical calculations are skipped until the node gets closer to the camera. | ![](distance.gif) | |---| | ![](distance_param.png) | | *Cloth simulation halts starting from the specified distance from the camera* | > **Notice:** *[Cloth](../../../principles/physics/bodies/cloth/index.md#distance), [Rope](../../../principles/physics/bodies/rope/index.md#distance)*, and *[Water](../../../principles/physics/bodies/water/index.md#distance)* physical bodies have their own **Simulation Distance** parameter as well.
- Using the *[**Iterations**](../../../editor2/settings/physics_global/index.md#iterations)* parameter may increase stability, but can also result in a higher load. A high number of iterations may lead to noticeable lags as very time-consuming calculations are automatically skipped. One physics iteration is quite enough for simple scenes.
- Adjust the time [**Budget**](../../../editor2/settings/physics_global/index.md#physics_budget) for Physics simulation.


## Collision Detection Optimization


### Filtering Interactions


It is very unlikely that each physics-based object in your project will interact with all other objects. Most probably, objects can be divided into groups dedicated to certain tasks.


If you have multiple objects that take part in physical simulation, divide the ones that are hardly going to interact with each other, into different "groups" by using the [Bit Masking](../../../principles/bit_masking/index.md) mechanism.


> **Notice:** The [Surfaces](../../../editor2/assets_optimize/content_profiler/surface_profiler.md) tab of the [Content Profiler](../../../editor2/assets_optimize/content_profiler/index.md) tool allows filtering out surfaces that use a specific mask to facilitate the scene optimization.


#### Limiting Collisions


Set matching [*Collision* Masks](../../../principles/bit_masking/index.md#collision_mask) for those particular [shapes](../../../principles/physics/shapes/index.md#collision_mask), [surfaces](../../../editor2/node_parameters/physics/index.md#surface_collision), and [bodies](../../../principles/physics/bodies/index.md) that are expected to collide. If the masks do not match, shapes and bodies will simply ignore each other by going through.


| ![](collision_filter.gif) |
|---|
| *Collisions are calculated for a plane and a sphere while a box is ignored due to unmatchingCollisionMasks* |


| ![](collision_mask_1.png) | ![](collision_mask_0.png) |
|---|---|
| *TheCollisionMask of the sphere's physical shape* | *TheCollisionMask of the box's physical shape* |
| ![](collision_mask_2.png) | ![](collision_mask_3.png) |
| *TheCollisionMask of the plane's surface* | *TheCollisionMask of the ground's surface* |


In Unigine, you can set up filtering accurately by using the [Exclusion Mask](../../../principles/physics/shapes/index.md#exclusion_mask). This mask allows ignoring shapes with the matching exclusion masks regardless of their *Collision Masks*.


Surfaces that are not intended for physical interactions should have the *[**Collision**](../../../editor2/node_parameters/physics/index.md#surface_collision)* flag disabled. For example, a dashboard inside a cockpit would never take part in collision detection on the outside.


Avoiding detection of undesired and unnecessary collisions is a basic way to reduce the amount of physical calculations.


#### Filtering Physical Effects


Specify certain [physicals](../../../objects/effects/physicals/index.md) that should affect only corresponding bodies by using the [*Physical* Masks](../../../principles/bit_masking/index.md#physical_mask) the same way as for collisions. On the image below, a *[Physical Wind](../../../objects/effects/physicals/physical_wind/index.md)* object affects a cloth banner but not a sphere.


| ![](physical.gif) |
|---|
| *A physical wind affects a cloth but not a sphere* |


| ![](physical_mask_0.png) *Physicalmask of the cloth banner* | ![](physical_mask_1.png) *Physicalmask of the sphere* |
|---|---|
| ![](physical_mask_2.png) *Physicalmask of thePhysical Windobject* |  |


#### Intersection Mask


[Intersection](../../../code/usage/intersections/index_cpp.md) is a generic point of a specified area (or line) and an object. Calculation of intersection between a ray cast and a surface is fast and inexpensive and therefore sometimes can be used instead of computing collision. For example, calculation of [collisions of car wheels with the ground](../../../principles/physics/joints/index.md#vehicles) can be simplified by using intersections.


Although it is a programmatic approach only, it requires [***Intersection* Masks**](../../../principles/bit_masking/index.md#intersection_mask) to be set for filtering purposes.


Both physical [shapes](../../../principles/physics/shapes/index.md#intersection_mask) and [surfaces](../../../editor2/node_parameters/physics/index.md#surface_intersection) have intersection masks.


### Reducing Colliders Complexity


As a rule, most 3D objects should be represented by a complex and detailed visible mesh and an invisible simplified shape used by a physics engine for collision detection (*collider*).


| ![](shape_0.png) *Detailed visible mesh* | ![](shape_1.png) *Invisible physical representation by using simplified shapes* |
|---|---|


#### Using Simpler Shapes


Physical [shapes](../../../principles/physics/shapes/index.md) consisting of simple primitives make collision calculations easier while keeping performance high and accuracy acceptable. Therefore, it is recommended to approximate geometry with simple primitives ([Sphere](../../../principles/physics/shapes/index.md#sphere), [Capsule](../../../principles/physics/shapes/index.md#capsule), [Cylinder](../../../principles/physics/shapes/index.md#cylinder), [Box](../../../principles/physics/shapes/index.md#box)), which are faster and less memory demanding.


Complex shapes, such as [Convex Hull](../../../principles/physics/shapes/index.md#convex) and a [set of autogenerated convex hulls](../../../principles/physics/shapes/index.md#autogen), should be selected for representing complex and composite geometry when simple shapes don't allow achieving the desired goals.


![](car_shapes.jpg)

*A car can be approximated using one complex shape and several simple shapes*



At the same time you should keep the number of shapes as *low* as possible in order to avoid heavy calculations leading to the performance drop. Remember that a shape doesn't have to duplicate the mesh it approximates. Even though primitives are not precise, in most cases they provide acceptable results.


![](shape_2.png)

*Rough approximation is accurate enough*


#### Using Simpler Geometry


The simpler geometry is used for [surface collisions](../../../principles/physics/collision/index.md) detection, the more performance will be gained.


If a mesh representing a physical obstacle has several [levels of detail](../../../principles/world_management/index.md#lods) (LODs), the least detailed one is the most preferable for collision and intersection detection. Enable the *[**Collision**](../../../editor2/node_parameters/physics/index.md#surface_collision)* and *[**Intersection**](../../../editor2/node_parameters/physics/index.md#surface_intersection)* options for this LOD and disable them for the other ones.


![](lods_masks.png)

*Use the lowest level of detail for intersections and collisions*



Approximating collision shapes by using primitives is also a good practice. You can apply the following approach:


1. Ensure that the original node is not a [Collider](../../../principles/physics/collision/index.md#collider) � check that *Collision* flag is disabled for its surfaces, bodies, and shapes. Since now it is not taken into account by collision detection.
2. Add a cylinder object to the scene by choosing *Create -> Primitive -> Cylinder* in the Menu Bar and cover the original mesh with the primitive. ![](primitive_cover.png)
3. Make sure that the *[**Collision**](../../../editor2/node_parameters/physics/index.md#surface_collision)* option of the surface is enabled for the primitive node.
4. Hide the visual representation of the primitive's surface. You can do it either by clearing its *[Viewport](../../../principles/bit_masking/index.md#viewport)* and *[Shadow](../../../principles/bit_masking/index.md#shadow_mask)* masks or simply by setting its *[**Max Visibility**](../../../editor2/node_parameters/visual_representation/index.md#max_visibility)* parameter to the negative infinity (**-inf**) � this ensures that the surface is not visible at any distance. ![](max_visibility.png) Now the detailed mesh provides only visual representation, while physical interactions are calculated for the primitive cylinder. ![](primitive_collision.png)


### Collision Detection Approach


[Continuous Collision Detection](../../../principles/physics/collision/index.md#discrete_continuous) is a very demanding operation, therefore, it is recommended to use this approach only for fast-moving objects and objects requiring precise calculations.


In most cases, [Discrete Collision Detection](../../../principles/physics/collision/index.md#discrete_continuous) would be enough. For this purpose, select a shape and uncheck the *[**Continuous**](../../../principles/physics/shapes/index.md#continuous)* flag for it.


![](continuous.png)


> **Notice:** Continuous collision detection is available for [sphere](../../../principles/physics/shapes/index.md#sphere) and [capsule](../../../principles/physics/shapes/index.md#capsule) shapes only.


## Optimizing Physical Bodies


### Freezing


It is recommended to enable *[Freezing](../../../principles/physics/bodies/index.md#freezing)* to all *[Rigid](../../../principles/physics/bodies/rigid/index.md), [Ragdoll](../../../principles/physics/bodies/ragdoll/index.md)*, and *[Fracture](../../../principles/physics/bodies/fracture/index.md)*bodies. This allows saving a great deal of computational resources by skipping physical calculations of immobile objects until they are affected by any force or object.


To enable freezing, perform the following steps:


1. Enable the *[**Freezable**](../../../principles/physics/bodies/rigid/index.md#parameter_freezable)* flag for all types of physical bodies listed above.
2. Set appropriate values of the *[**Frozen Linear Velocity**](../../../principles/physics/bodies/index.md#freezing)* and *[**Frozen Angular Velocity**](../../../principles/physics/bodies/index.md#freezing)* parameters for each physical body or adjust the [global parameters](../../../editor2/settings/physics_global/index.md#frozen_linear). These global freezing thresholds are compared to the ones set for each body, and the highest value is chosen to freeze the body. ![](freezable.png)
3. Adjust the number of *[**Frozen Frames**](../../../editor2/settings/physics_global/index.md#frozen_frames)*. The lower the value, the faster objects get frozen.


### Fracturing


Although the [fracture body](../../../principles/physics/bodies/fracture/index.md) is a relatively inexpensive type, in case of large number of fracture pieces, the impact on performance may become significant. To avoid performance drops, the following tips can be used:


- Use the *[**Volume Threshold**](../../../principles/physics/bodies/fracture/index.md#threshold)* parameter to reduce the number of fracture pieces.
- Remove the pieces of a fractured body from the scene.


A code-based example illustrating how to remove (fade with the time) the fracture pieces from the scene can be found in the *Physics* section of the [UnigineScript samples](../../../sdk/index.md#samples).
