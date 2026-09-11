# Collision Detection


The body movement without constraints and obstacles rarely happens in real life, the same is true for a virtual world. To correctly describe the situation when the body meets an obstacle the **collision detection** is used.


Collision detection algorithms, regardless of their implementation, usually operate with invisible simplified shapes that approximate the [meshes](../../../start/index.md#mesh) of colliding objects. Such approximations are called *colliders* (or [collision shapes](../../../principles/physics/shapes/index.md)). There are several types of colliders, which can be combined: boxes, spheres, cylinders, capsules, convex hulls.


There are two types of collisions implemented in UNIGINE depending on the types of colliding objects:


- **Shape � Shape collision**: between two objects with physical properties assigned (i.e. having a [body](../../../principles/physics/bodies/index.md) and at least one [shape](../../../principles/physics/shapes/index.md), *both must be enabled*). In this case contact points between the shapes are found.
- **Shape � Surface collision**: between an object with physical properties assigned and a non-physical object (i.e. without physical representation). If the [surface](../../../start/index.md#surface) has the *Collision* flag set, it can also passively participate in physical interaction and prevent the physical object from going through. In this case, contact points between the shape and surface polygons are computed.


> **Warning:** Don't scale meshes that are going to participate in collision detection � physics doesn't work properly with scaled objects. To avoid scaling, reimport the mesh with the required [scale](../../../editor2/fbx/index.md#fbx_scale).


In order for an object to participate in collision detection (i.e. be a **collider**), it must be added to a specific BSP-tree representing the physics scene. Collision detection is automatically enabled for an object if it has a [body](../../../principles/physics/bodies/index.md) assigned or at least one of its surfaces has the *Collision* flag set. The algorithm of enabling/disabling collision detection is illustrated below.


![](cd_algorithm.png)

*Algorithm of enabling/disabling collision detection.*


> **Notice:** - Disabling physics simulation globally does not turn off Collision detection.
> - In case if an object has a body and a shape assigned and enabled, the collision detection algorithms will use only shape's parameters, while the parameters of its surfaces will be ignored.


### See Also


- *[getCollision()](../../../api/library/engine/class.world_cpp.md#getCollision_WorldBoundBox_VECObject_int)* methods
- The [video tutorial on physics](https://youtu.be/w_GJrE-6HtI?)
- The [video tutorial on handling contacts](../../../videotutorials/how_to/how_to_cs/contacts.md)
- The [Handling Contacts on Collision](../../../code/usage/handling_contacts_on_collision/index_cpp.md) usage example


## Process Pipeline


The whole process is divided into the following stages and phases:


1. [**Collision Detection**](#detection) � during this phase we find all collisions with all contact points and collect all necessary information.
2. [**Collision Response**](#collision_response) � it is the result of collision (e.g. two balls bounce off of each other). Without the response there would be no difference between collision and intersection of two objects. [Friction](../../../principles/physics/bodies/index.md#friction), [restitution](../../../principles/physics/bodies/index.md#restitution) and other parameters are taken into account in calculation of collision response.
3. [**Callbacks Execution**](#callbacks) � custom user-defined actions to be performed on certain physics-related events.


![](collision_phases.jpg)

*Phases: (a) � collision detection, (b) � collision response*


### Detecting Collisions


Checking all pairs of objects for collision is too time consuming, especially if the scene is large. Before doing more precise and costly calculations, we can filter out pairs of objects that are positioned too far to collide. Thus, all objects that have physical bodies are found within the [Physical distance](../../../editor2/settings/physics_global/index.md#physics_distance) using the scene tree.


> **Notice:** Non-colliding [dummy bodies](../../../principles/physics/bodies/dummy/index.md) are skipped and not simulated unless they interact with other bodies via joints.


Actually, there are no broad and narrow phases *per se*, so on the next step all collisions ([shape-shape](#collision_types) and [shape-surface](#collision_types)) along with contact points are found for all colliding bodies, i.e., if they are intersecting or have the distance between them less than the value of [penetration tolerance](../../../editor2/settings/physics_global/index.md#penetration_tolerance). Contact points are represented by their coordinates, normals, depth of shapes penetration, relative velocity (between two bodies), relative friction and restitution. So, here we collect all the data that is required to resolve collisions later.


In a constrained physics simulation some objects influence the motion of others, while others don�t. Thus, these objects can be grouped into **islands**, which are self-contained groups of bodies that can influence the motion of each other in the group through constraint forces/impulses, but do not affect objects belonging to other islands. So, all contacting bodies as well as the ones having joints that connect them are combined in an island.


![](islands.gif)

*Objects grouped into islands*


In case *[Deterministic](../../../principles/physics/simulation.md#deterministic)* mode of physics simulation is enabled bodies, shapes, and joints are sorted inside islands to ensure that contacts are solved in the predefined order and visualization of physics in the world is repetitive (on one computer).


Collision detection uses certain optimization approaches to decrease computational load and improve efficiency (e.g., space partitioning, islands, freezing etc.).


### Collision Response


So, we've got all necessary information about collisions, now something has to be done with this information to provide realistic reaction. Collision response stands for simulation of the changes in the motion of two solid bodies after collision. On collision, the kinetic properties of two bodies change instantaneously. Typically the bodies rebound away from each other, slide, or settle into a static contact, depending on their elasticity and the configuration of the collision. UNIGINE uses an **impulse-based reaction** model. During the collision, the first body applies a collision impulse to the second one at a contact point equal in magnitude but opposite in direction to the impulse applied by the second body, as per the Newtonian principle of action and reaction.


![](collision_response1.gif)

*Collision response*


At this stage all found contacts are cached together with contacts from the previous frame � to ensure proper interaction. On the basis of gathered contact points data, UNIGINE computes the impulse a shape gets by collision. Contact points are solved in a pseudo-random order to achieve simulation stability and reproducibility.


[Joints](../../../principles/physics/joints/index.md) are solved in the process of contact response calculation. The impulses that joints give the bodies attached to them are computed: how according to the current state of the joint, the bodies should respond to keep the joint unbroken (i.e. based on their masses, linear and angular velocities, change their movement direction and orientation), and how that response affects the joint (a joint can be broken by a too large impulse). Joints are also solved in the pseudo-random order.


> **Notice:** Within one physics iteration, joints can be solved several times. High number of joint iterations increases the precision of calculations, as well as computational load.


The results of contact and joint solving are accumulated and applied to bodies. The coordinates of the bodies change according to their new linear and angular velocities.


There are two material parameters taken into account in the process of collison response calculation, which can be set for a [shape](../../../principles/physics/shapes/index.md#shape_params) and for a [surface](../../../start/index.md#surface) as well:


- **Restitution** � the degree of relative kinetic energy retained after a collision. It depends on the elasticity of the materials of colliding bodies.

  - The minimum value of **0** indicates *inelastic* collisions (a piece of soft clay hitting the floor)
  - The maximum value of **1** represents highly *elastic* collisions (a rubber ball bouncing off a wall)
- **Friction** � the force that impedes the relative motion of two surfaces in contact. The higher the value, the less tendency the body has to slide.


> **Notice:** In case if an object contains a surface and a shape, both with specified restitution and friction, only the shape's parameters are to be used.


### Callbacks Execution


After the simulation stage all physics callbacks are called. These callbacks are mainly used for creation, destruction or modification of other objects, such operations can only be performed in the main thread.


> **Notice:** Physics callbacks are called in the main thread.


## Discrete and Continuous Collision Detection


Regarding the way the time scale is considered, two basic approaches to finding contact points in case of collision are used. Both of these approaches are implemented in UNIGINE.


- **Discrete collision detection** is performed in certain intervals of time and each frame is treated separately from others. In general, discretization improves performance. However, when a project framerate is already low, a small fast-moving object is likely to teleport from one point to another instead of moving there smoothly and collision will not be detected.
- **[Continuous collision detection](../../../principles/physics/simulation.md#ccd)** does not suffer this problem as the moving body is extruded along its trajectory (between two adjacent frames). In cases when something gets into this volume and a collision is detected, the body is taken back in time to correct the collision reaction. > **Notice:** By default, continuous collision detection is enabled only for [sphere](../../../principles/physics/shapes/index.md#sphere) and [capsule](../../../principles/physics/shapes/index.md#capsule) shapes. For other shape types, it must be [enabled manually](../../../api/library/physics/class.shape_cpp.md#setContinuous_int_void).


![](collision_detection.jpg)

*Discrete (a) and continuous (b) collision detection*


The primary advantage of discrete detection is that it tends to be much faster and simpler for objects with complex shape or large size. Continuous collision detection requires mathematical descriptions of all objects and their motions and the solving systems of equations, which can be difficult, slow, or even impossible in many circumstances.


## Collision Mask


To make collision detection flexible and selective, and to reduce calculation costs, the mechanism of [bit masking](../../../principles/bit_masking/index.md) is used. For example, we have an object, which does not participate in interactions with others, but we want it to lie on the ground. Matching the collision bit masks of this object and the ground (at least one bit in the masks should match) provides the necessary effect. One object can participate in several collision checks as only one bit in the mask is required to match for a pair of objects.


All scene objects, if not configured, are created with the default collision mask i.e. everything collides with everything. This may reduce performance in case if the number of objects in the world is large. The best practice here would be to establish what should collide with what.


## Static and Dynamic Contacts


Basically there are two types of contacts:


- **Static**, when the body rests on another body. In this case, bodies are considered "[frozen](../../../principles/physics/bodies/index.md#freezing)" until an external force affects them. This makes it possible to avoid unnecessary calculations.
- **Dynamic**, when two bodies, at least one of which is moving, collide. In this case, we have to calculate instantaneous change of velocities for both colliding objects.


![](collision_static_dynamic.jpg)

*Static (left) and dynamic (right) contacts*


## Collision Examples


See the following example illustrating several aspects of collision detection:


- [Enabling Selective Surface-Based Collision](../../../code/usage/enabling_collision/index_cpp.md).
