# Physics


![](tank.jpg)


Unlike many other engines using third-party solutions, UNIGINE features its own built-in physics module.


The advantages of using a built-in physics module:


- **Memory efficiency** � a single instance of the world is used (if an external solution is used, one more copy of the world has to be created and stored).
- **Performance** � calls to external functions, excessive data conversion and transmission between integrated systems are avoided.


It should be clear that it is not a high-precision simulation of real world physics! The simulation is just an approximation based on **simplified calculations** and **decreased accuracy** providing a realistic look within the strict limits of the real-time mode. Achieving a true-to-life result always involves a trade-off between accuracy and performance.


> **Notice:** It is not recommended to use real values of mass, density, gravity, etc. To ensure realistic behavior, the values are to be chosen experimentally.


Though in general UNIGINE uses a simplified Newtonian physics with an impulse-based approach, the integration of [collision detection](../../principles/physics/collision/index.md), gravity, [friction](../../principles/physics/bodies/index.md#friction), [buoyancy](../../principles/physics/bodies/water/index.md), [joints](../../principles/physics/joints/index.md), and external physical [forces](../../principles/physics/bodies/index.md#force) provides realistic simulation of [physical bodies](../../principles/physics/bodies/index.md) and complex interactions between them.


### See also


- The [video tutorial on physics](https://youtu.be/w_GJrE-6HtI?)


## Use Cases and Limitations of Built-in Physics


UNIGINE's physics module is quite limited; however, in a number of cases it helps programmers and designers to make their work easier. Here is the list of the use cases where it is better to use built-in physics rather than hard-coding or bone-based animation:


- [Collision detection](#collision_intersection) (prevention of moving through walls, interpenetration of solid bodies, etc.)
- Simulation of perfectly elastic collisions (redistribution of kinetic energy)
- Simulation of various [joints](#joint), motors, and springs
- Simulation of basic physical phenomena: gravity, [friction](../../principles/physics/bodies/index.md#friction) (static and sliding), [buoyancy](../../principles/physics/bodies/water/index.md) (for relatively calm water without big waves)
- Simulation of external forces ([wind](../../objects/effects/physicals/physical_wind/index.md), [force field](../../objects/effects/physicals/physical_force/index.md))
- Procedural [destruction of meshes](../../principles/physics/bodies/fracture/index.md)
- Simulation of deformable [cloth](../../principles/physics/bodies/cloth/index.md) and ropes
- [Rag doll](../../principles/physics/bodies/ragdoll/index.md) simulation


It should be understood that the scope of simulation using built-in physics is limited to the cases listed above. Thus, there is a large number of cases that cannot be solved this way, including the following:


- [High-precision physics simulation](#extengine)
- [Flight dynamics simulation](#extengine)
- [Fluid dynamics simulation](#extengine)
- [Simulation of gravitational fields](#extengine)
- [Simulation of inelastic collisions](#codebased)
- [Digging of the ground](#extengine)
- [Physical destruction of complex objects](#combined)


Though some tasks involving a large number of objects can be solved using built-in physics, it may significantly reduce performance. In this case, as in the cases listed above, it is recommended to use alternative ways described in the next chapter.


Watch a fragment of our [video tutorial on physics](https://youtu.be/w_GJrE-6HtI?t=188s) illustrating this chapter.


## Alternatives to Built-in Physics


When a problem cannot be solved by means of the built-in physics module or takes too much time, several other approaches can be used: bone-based animation, hard coding, or using an external physics engine.


### Bone-based Animation


In some cases, when an object's behavior cannot be implemented by using physics simulation or requires too many calculations, the bone-based animation can be used instead.


**Bone-based animation** is a technique in which animated object is represented by two components:


- Surface representation used to draw the object (called skin or [mesh](../../start/index.md#mesh))
- Hierarchical set of interconnected bones (called the skeleton or rig) used to animate (pose and keyframe) the mesh


![Mesh and skeleton](skeletal.jpg)

*Mesh and skeleton*


This technique serves to make the animation process more convenient. Each bone of the rig is associated with some part of the object's mesh. Skinning is the process of creating this association. Changing bone transformations modifies the mesh.


There are two ways of using bone animation:


- [Baked bone animation](../../objects/objects/mesh_skinned_legacy/index.md) using pre-baked keyframes stored in **[.anim](../../code/formats/animations_formats.md#anim)** file
- Procedural bone animation using *[ObjectMeshSkinnedLegacy](../../api/library/objects/class.objectmeshskinnedlegacy_cpp.md)* class to change bone transformations in real time


Meshes and animation can be created using third-party graphics software (*3ds Max, Maya*, etc.), then [imported to UNIGINE](../../editor2/fbx/index.md) in their [native format](../../code/formats/file_formats.md) (`.mesh` and `.anim`) and used in the world.


- **The first use case** is creation of a complex mechanism with a large number of various joints working in the background of a factory workshop. Simulation of this mechanism using physics will significantly reduce performance. You can use a baked bone-based animation instead.
- **The second use case** is determined by the fact that bones cannot be affected physically. Imagine that we have an antenna, which is represented by a single [mesh](../../start/index.md#mesh) containing a number of bones, attached to a vehicle. To make it move realistically we have to write a script (in [C++](../../code/cpp/index.md) or [C#](../../code/csharp/index.md)) calculating necessary bone transformations and providing desired behavior of the antenna.


### Code-based Approach


Another way to replace physics simulation achieving a realistic result without performance drops is code-based approach, which involves writing some code to programmatically change transformations of objects and their behavior.


- **The first use case** is simulation of the object deformation as a result of an inelastic collision. The built-in physics does not implement inelastic collision simulation. However, we can detect a collision and then change the deformed object's mesh in the script (in [UnigineScript](../../code/uniginescript/index.md), [C++](../../code/cpp/index.md) or [C#](../../code/csharp/index.md)) providing the desired deformation. > **Notice:** Deformation (i.e. changing positions of mesh vertices) is available for [dynamic meshes](../../objects/objects/mesh_dynamic/index.md) only!
- **The second use case** is when there is a large number of interacting elements, e.g. tank tracks and suspension. If we have many tanks, the calculation of physics will drop FPS down. Moreover, due to approximation errors the whole mechanism may blow up or look unnatural. We write a script, which calculates the movement of suspension and track plates, providing stability and a desired degree of realism.


Using code-based tricks makes it possible to maintain acceptable FPS and tweak the behavior of objects.


### External Physics Engines


In cases where a precise physical simulation is required (e.g. flight dynamics, fluid dynamics, etc.) it is recommended to use a specialized third-party solution that provides required functionality. UNIGINE does not currently offer a solution for third-party physics integration. Therefore, all necessary product-specific guidelines on how to integrate a certain third-party solution into your application are to be obtained from the party offering this solution.


### Combined Approach


Very often, the best results can be achieved using a combination of different methods or techniques. So, the approaches described above can be successfully combined to provide a convincing look and acceptable performance.


**The use case** illustrating a successful combination of several approaches is associated with simulation of physical destruction of complex objects, e.g. collapsing bridges, exploding buildings, etc. Realistic simulation in this case is impossible in real time. However, it can be pre-computed using third-party offline physics simulation software and then converted to a baked bone-based animation to be used in a real-time application.


## Physical Interaction of Objects. Basic Entities


While the majority of node types in the scene serve as auxiliary means or decorations, the [Object](../../objects/objects/index.md) type can have physical properties and interact with other objects and the environment. For these properties to be assigned, the object should have a "[body](#body)" (a physical approximation of the object), and the body should have at least one "[shape](#shape) " (a volume in space occupied by a body). To connect bodies and restrict their movement relative to each other, the "[joints](#joint)" are used. The picture below illustrates relationships between these entities.


![Relationships between the entities](entities.jpg)

*Relationships between the entities*


### Body


To interact with other objects as well as external physical forces, an object must have a body. The body can be considered a physical approximation of the object, it describes its behavior and represents a set of its dynamic parameters, such as mass, velocity, etc. There are several types of bodies: *[dummy](../../principles/physics/bodies/dummy/index.md), [rigid](../../principles/physics/bodies/rigid/index.md), [ragdoll](../../principles/physics/bodies/ragdoll/index.md), [fracture](../../principles/physics/bodies/fracture/index.md), [rope](../../principles/physics/bodies/rope/index.md), [cloth](../../principles/physics/bodies/cloth/index.md), [water](../../principles/physics/bodies/water/index.md), [path](../../principles/physics/bodies/path/index.md)*. Each type of body is used for simulation of a specific type of object.


![Scene with several types of bodies](bodies.jpg)

*Scene with several types of bodies: water, ragdoll, rigid*


Mass parameters of the body can be set up manually or determined automatically using the shape-based parameters. It is convenient when a body has several shapes.


Body mass and density are used for [buoyancy](../../principles/physics/bodies/water/index.md) simulation in accordance with the Archimedes' principle.


### Shape


While the body determines the object�s behavior, the shape represents the volume of space occupied by a physical body. The shape is invisible and doesn�t have to be the same as the object�s [mesh](../../start/index.md#mesh). Actually a rough approximation (*[sphere](../../principles/physics/shapes/index.md#sphere), [capsule](../../principles/physics/shapes/index.md#capsule), [cylinder](../../principles/physics/shapes/index.md#cylinder), [box](../../principles/physics/shapes/index.md#box), [convex hull](../../principles/physics/shapes/index.md#convex)*) is often more efficient and indistinguishable. A physical body has one or several collision shapes allowing objects to [collide](#collision_intersection) with each other.


![A car approximation using one and several shapes](car_shapes.jpg)

*A car approximation using one and several shapes*


> **Notice:** The maximum number of collision shapes for one body is limited to 32768.


Objects with shapes also fall down under gravity, bounce off static surfaces, or slide along them. Sliding and bouncing are determined by restitution and friction coefficients included in the list of shape parameters. A body without a single shape assigned behaves as a [dummy body](../../principles/physics/bodies/dummy/index.md) that can be connected to other bodies using joints, but does not collide and is immune to gravity.


### Joint


In virtual worlds, like in the real world, we would like to have complex objects consisting of several interconnected parts (for example, a robotic arm or a car). That's exactly what the joints are used for.


![A joint connecting two rigid bodies](joint.jpg)

*A joint connecting two rigid bodies*


A joint connects two [rigid bodies](../../principles/physics/bodies/rigid/index.md) and represents certain constraints i.e. it restricts the movement of connected bodies relative to each other. When the force applied to a joint is too much, the joint breaks. The implementation of destructible joints includes the limits of linear and angular motion, so if a force exceeds these limits, the joint is broken. There are several types of joints: *[fixed](../../principles/physics/joints/index.md#fixed), [hinge](../../principles/physics/joints/index.md#hinge), [ball](../../principles/physics/joints/index.md#ball), [prismatic](../../principles/physics/joints/index.md#prismatic), [cylindrical](../../principles/physics/joints/index.md#cylindrical), [suspension](../../principles/physics/joints/index.md#suspension), [wheel](../../principles/physics/joints/index.md#wheel), [path](../../principles/physics/joints/index.md#path)*.


When using joints, it is very important to ensure mass balance � avoid connection of too heavy bodies to light ones, otherwise the system may become unstable. As mentioned before, physics simulation uses approximate calculations, therefore, if the difference of mass between two connected bodies is significant, accumulation of errors and precision issues lead to instability of the result.


Thus, when making a car model, do not set the mass of the car body equal to 2000 kg and the wheels � to 10 kg, it might be better to use 5 kg for the body and 1 kg for each wheel to provide realistic behavior.


## Collision and Intersection Detection


To restrict interpenetration of solid bodies, prevent moving through walls, and make things look more natural and familiar to the eye, the **collision detection** is used.


There are two types of collision detection implemented in UNIGINE:


- **Discrete collision detection** is performed in certain intervals of time and each frame is treated separately from others. In general, discretization improves performance. However, when a project framerate is already low, a small fast-moving object is likely to teleport from one point to another instead of moving there smoothly, and a collision will not be detected.
- **[Continuous collision detection](../../principles/physics/simulation.md#ccd)** does not suffer this problem as the moving body is extruded along its trajectory (between two adjacent frames). If something gets into this volume and a collision is detected, the body is taken back in time to correct the collision reaction. > **Notice:** By default, continuous collision detection is enabled only for [sphere](../../principles/physics/shapes/index.md#sphere) and [capsule](../../principles/physics/shapes/index.md#capsule) shapes. For other shape types, it must be [enabled manually](../../api/library/physics/class.shape_cpp.md#setContinuous_int_void).


![Discrete and continuous collision detection](collision_detection.jpg)

*Discrete (a) and continuous (b) collision detection*


Collision detection is a very expensive operation, and since our scene may have hundreds of objects, a lot of effort is put into optimization.


- The first parameter contributing to the cost is collision shape complexity. As a rule, most 3D objects are represented by a complex and detailed visible [mesh](../../start/index.md#mesh) and an invisible simplified [shape](#shape) used by a physics engine for collision detection. Types of shapes available are listed [above](#shape). > **Notice:** To reduce computational load it is strongly recommended to use simple collision shapes instead of complex ones wherever possible.
- The second parameter is a number of checks to be performed � the worst case would be all-against-all. To exclude unnecessary checks (e.g. two objects hardly collide if they are far from each other) the scene is to be split into sections.


There is an important step which follows collision detection � **collision response**, or the result of collision (e.g. two balls bounce off each other). [Friction](../../principles/physics/bodies/index.md#friction), [restitution](../../principles/physics/bodies/index.md#restitution), and other parameters are taken into account in calculation of the collision response.


If some [surfaces](../../start/index.md#surface) of an object participate in collisions, and others don't, collision detection can be enabled on a per-surface basis. For example, you can disable collision detection for a dashboard inside a cockpit, as it is covered by other surfaces.


> **Warning:** Don't scale meshes that are going to participate in collision detection � physics doesn't work properly with scaled objects. To avoid scaling, reimport the mesh with the required [scale](../../editor2/fbx/index.md#fbx_scale).


**Intersection detection** lies at the heart of collision detection, but is a particular case of ray intersection (**ray casting**) that serves slightly different purposes. Calculation of the intersection between a ray cast from a certain point in a certain direction and a surface is fast and inexpensive and therefore sometimes can be used instead of computing a collision. For example, calculation of collisions of car wheels with the ground takes time and decreases framerate. In this case we can use intersection of rays cast from the bottom of the car with the ground instead of precise collision detection using collision shapes, thus reducing computational costs and increasing performance.


![Ray-box intersection](intersection.jpg)

*Ray-box intersection*


To make collision and intersection detection flexible and selective, and to reduce calculation costs, the mechanism of [bit masking](../../principles/bit_masking/index.md) is used. For example, we have an object that does not participate in interactions with others, but we want it to lie on the ground. Matching the collision bit masks of this object and the ground (at least one bit in the masks should match) provides the necessary effect. One object can participate in several collision and intersection checks as only one bit in the mask is required to match for a pair of objects.


## Simulation of Physics


Simulation of physics is performed in a looped sequence of the following stages on a per-frame basis:


![Physics simulation loop](loop.jpg)

*Physics simulation loop*


Physics in UNIGINE is simulated in the [multi-threaded mode](../../principles/physics/simulation.md#multi_threaded), when some operations are performed in parallel.


Physics is simulated with its [own **fixed** FPS](../../code/fundamentals/execution_sequence/index.md#framerates), which does not depend on the rendering framerate: a variable FPS cannot be used here because it makes calculation results unstable.


Calculation of physics for all dynamic objects on the scene takes too much time. To ensure a consistent framerate and exclude unnecessary calculations, some optimization approaches are used:


- When a body is moving slower than a specified minimum [linear](../../editor2/settings/physics_global/index.md#frozen_linear) or [angular velocity](../../editor2/settings/physics_global/index.md#frozen_angular) for a specified period ([freeze frames](../../editor2/settings/physics_global/index.md#frozen_frames)), it is assumed that it has come to a halt. During this period of inactivity, there is actually no need to simulate it. If this happens, the object remains in a resting state until it is affected by another object or force. Therefore, such object is excluded from all steps of the simulation except [collision detection](#collision_intersection). This state is called **freezing** and it allows to save a great deal of computational resources. | ![](freezing0.jpg) | ![](freezing1.jpg) | |---|---| | *Frozen blue and unfrozen red boxes: the impulse applied to the pyramid of boxes unfroze all but one* |  |
- If interacting objects are far away from the viewer, they do not make a noticeable contribution to the whole image and thus can be neglected. The [Simulation distance](../../editor2/settings/physics_global/index.md#physics_distance) setting specifies the distance from the viewer when physical interactions are no longer calculated.


## Global Physics Settings


Global physics settings (FPS, gravity, simulation distance, freeze frames and velocities, penetration factor, penetration tolerance) can be accessed via the [Physics settings](../../editor2/settings/physics_global/index.md) panel in the [Editor](../../editor2/index.md).
