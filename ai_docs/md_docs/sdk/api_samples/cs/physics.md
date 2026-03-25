# Physics

> **Notice:** The complete sample source code is available on GitHub:
> **[github.com/unigine-engine/csharp-component-samples](https://github.com/unigine-engine/csharp-component-samples)**.


## Body Events

This sample demonstrates how to use the *[Frozen](../../../api/library/physics/class.body_cpp.md#EventFrozen)*, *[Position](../../../api/library/physics/class.body_cpp.md#EventPosition)*, and *[ContactEnter](../../../api/library/physics/class.body_cpp.md#EventContactEnter)* events of the *[Body](../../../api/library/physics/class.body_cpp.md)* class via the C# API. These events allow responding to physical state changes, such as when a rigid body comes to rest, moves, or collides with another object or surface.


The sample builds a pyramid of boxes by cloning a mesh and arranging it in several layers. Physics settings are adjusted to improve the stability of the stacked boxes and ensure accurate detection of movement or rest states.


This approach is useful for debugging physical behaviors, providing visual feedback in simulations, or triggering logic based on changing body states.


Each body in the pyramid is connected to *[Frozen](../../../api/library/physics/class.body_cpp.md#EventFrozen)*, *[Position](../../../api/library/physics/class.body_cpp.md#EventPosition)*, and *[ContactEnter](../../../api/library/physics/class.body_cpp.md#EventContactEnter)* events using *[lambda](../../../code/fundamentals/events/index.md#lambda_functions)* expressions. All subscriptions are managed through an *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* class instance, which keeps all connections in one place and ensures proper cleanup during shutdown.


For example, the *Frozen* lambda changes the material of the box when it stops moving. The *Position* lambda changes the material whenever the position updates. The *ContactEnter* lambda visualizes contact points during collisions.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/physics/body_events*
## Body Fracture Explosion

This sample demonstrates how to simulate an explosion that fractures physical objects within its radius using the *[BodyFracture](../../../api/library/physics/class.bodyfracture_cpp.md)* class. Each object affected by the explosion is dynamically fractured into separate physical fragments depending on its proximity to the center of the explosion and the decreasing explosion strength over distance.


The force applied to the fragments pushes them outward from the explosion center, creating a realistic dispersal effect. A built-in debug visualization clearly displays the explosion radius and the direction of the applied forces, making it easier to understand and adjust the fracture behavior and explosion dynamics.


Press *Explode!* to manually trigger the explosion.


This example is ideal for scenarios that require realistic destruction, dynamic fracture effects, or visual representations of physical object damage.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/physics/body_fracture_explosion*
## Body Fracture Falling Spheres

This sample demonstrates continuous fracturing of objects using *[BodyFracture](../../../api/library/physics/class.bodyfracture_cpp.md)* class.


Spheres are periodically spawned every 3 seconds and fall freely under gravity. Upon collision with the ground, each sphere fractures dynamically into multiple physical fragments.


The sample includes a debug visualization that displays mesh wireframes, providing clear insight into internal mesh structure and fracture patterns generated upon impact.


This example can be used to explore and evaluate destruction mechanics, test mesh-based fracturing setups, and visually analyze breakage behavior in real-time scenarios.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/physics/body_fracture_falling_spheres*
## Body Fracture Shooting Gallery

This sample shows how to simulate projectile-based interactions in a simple shooting gallery setup using **[Fracture Body](../../../principles/physics/bodies/fracture/index.md)**. When the left mouse button is clicked, a projectile is spawned in front of the camera and propelled forward. Target objects in the scene react to the impact physically and can be fractured using the **[Fracture Body](../../../principles/physics/bodies/fracture/index.md)** system to simulate realistic destruction effects.


**Use Cases:**


- Prototyping physics-based shooting mechanics.
- Demonstrating **[Fracture Body](../../../principles/physics/bodies/fracture/index.md)** impulse interactions.
- Testing fracture behaviors in destructible environment setups.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/physics/body_fracture_shooting_gallery*
## Joint Events

This sample demonstrates how to use the *[Broken](../../../api/library/physics/class.joint_cpp.md#EventBroken)* event of the *[Joint](../../../api/library/physics/class.joint_cpp.md)* class via the C# API. This event allows you to react when a joint is broken due to physical forces during the simulation.


A simple bridge structure is created by cloning a mesh and connecting multiple sections using hinge joints. Some sections are dynamic (*[BodyRigid](../../../api/library/physics/class.bodyrigid_cpp.md)*) and others are static (*[BodyDummy](../../../api/library/physics/class.bodydummy_cpp.md)*) to anchor the ends. Additionally, a few weights are dropped onto the bridge to cause joint breakage. The scene is configured to showcase physically reactive behavior through joints under load. When a joint breaks, the lambda is triggered, changing the material of the connected objects to visually indicate the break.


You can use this for detecting breakage in joint-based systems or adding visual feedback to destruction mechanics.


The Broken event of each joint is connected to a *[lambda](../../../code/fundamentals/events/index.md#lambda_functions)* expression using an *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* class instance, which stores all connections in one place and ensures automatic cleanup when the component is shut down.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/physics/joint_events*
## Physics Movement

This sample demonstrates a simple logic of moving an object using physical methods (by force or by impulse).


You can choose the desired method and control maximum speed, rotation speed, and accelerations using sliders.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/physics/physics_movement*
## Update Physics

This sample demonstrates the difference between *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* and *[updatePhysics()](../../../code/fundamentals/execution_sequence/code_update.md#code_updatePhysics)* methods.


The sample features two physics-enabled cubes that move back and forth along the X-axis. The movement logic is implemented via in the *UpdatePhysicsUsageController.cs* file.


Use *updatePhysics()* to implement continuous or physics-dependent operations (e.g., force application, collision response), as it runs at a fixed time step, unlike *update()* which depends on the rendering frame rate.


Use the **Max FPS** slider to change the target frame rate.


The green cube uses *[updatePhysics()](../../../code/fundamentals/execution_sequence/code_update.md#code_updatePhysics)*, which is called at a fixed physics frame rate, and should be considered a correct example for physics-related logic.


The red cube uses *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)*, which runs every render frame. This approach may cause unstable results when interacting with physics and should generally be avoided when implementing physics-driven movement.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/physics/update_physics*
