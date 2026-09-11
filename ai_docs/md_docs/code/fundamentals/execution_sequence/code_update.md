# Where to Put Your Code


To bring interactivity and behavior to your world, you need to define the logic that drives it.


Your code can be placed in predefined parts of the [application logic system](../../../code/fundamentals/execution_sequence/app_logic_system.md) - the Engine will automatically call the corresponding methods according to the [execution sequence](../../../code/fundamentals/execution_sequence/index.md). In addition, the Engine supports an extensive event system, allowing you to handle various events that may occur at any time during runtime.


The [World Logic](../../../code/fundamentals/execution_sequence/app_logic_system.md#world_logic) has a set of functions that are used to implement logic of the application.


- [Initialization](../../../code/fundamentals/execution_sequence/init.md) function of the World Logic (***init()***) is used to create objects and initialize all other necessary resources on the world load.
- [Shutdown](../../../code/fundamentals/execution_sequence/shutdown.md) function (***shutdown()***) is called when the world is unloaded and is used to delete resources that were created during the logic execution to avoid memory leaks.


The same set of methods applies to components, since the Component System is a part of WorldLogic, although their behavior slightly differs:


- Each component's ***init()*** method is called during component initialization, which occurs at the moment the component is attached to a node.
- Each component's ***shutdown()*** method is called when a component is removed, or the node this component is attached to, is destroyed.


But what about the frame-by-frame update? Both [World Logic](../../../api/library/common/logic/class.worldlogic_cpp.md) (AppWorldLogic.cs or AppWorldLogic.cpp) and [Components](../../../principles/component_system/index.md) provide a set of methods that enable per-frame processing of application logic:


- *[updateAsyncThread()](#code_updateAsyncThread)* can contain logic functions to be called every frame independently of the rendering thread: pathfinding, generation of procedural textures, custom physics, etc.
- *[updateSyncThread()](#code_updateSyncThread)* can contain any parallel logic functions to be executed before *update()*.
- *[update()](#code_update)* can contain any logic: control what to render on the screen and how to do it, render to textures, create nodes, call console commands, etc.
- *[updatePhysics()](#code_updatePhysics)* can be used to simulate physics: perform continuous operations (pushing a car forward depending on current motor's RPM, simulating a wind blowing constantly, perform immediate collision response, etc.).
- *[postUpdate()](#code_postUpdate)* can be used to correct behavior according to the updated node states in the same frame.
- *[swap()](#code_swap)* can be used to process the results of the *[updateAsyncThread()](#code_updateAsyncThread)* function.


> **Notice:** Unlike *World Logic*, which is bound to a world, *System Logic* operates at the application level and includes a similar set of methods: *init(), shutdown(), update(), postUpdate()*.


In addition to the standard lifecycle and per-frame update methods, components include several unique callbacks that extend their functionality:


- *[OnReady()](../../../api/library/common/logic/component_system/cs/class.component.md#on_ready_void)* for C# or *[on_ready()](../../../api/library/common/logic/component_system/cpp/class.componentbase_cpp.md#on_ready_void)* for C++ - triggered **immediately** after the component has been created and attached to a node.
- *[OnEnable()](../../../api/library/common/logic/component_system/cs/class.component.md#on_enable_void)* for C# or *[on_enable()](../../../api/library/common/logic/component_system/cpp/class.componentbase_cpp.md#on_enable_void)* for C++ - triggered **immediately** when the component becomes enabled (both the node and the property are active).
- *[OnDisable()](../../../api/library/common/logic/component_system/cs/class.component.md#on_disable_void)* for C# or *[on_disable()](../../../api/library/common/logic/component_system/cpp/class.componentbase_cpp.md#on_disable_void)* for C++ - triggered **immediately** when the component becomes disabled (both the node and the property are disabled).


## Code UpdateAsyncThread


In the world logic ***updateAsyncThread()***, you can specify all logic functions you want to be called every frame independently of the rendering thread. This function can be used to perform some heavy resource-consuming calculations performed during the whole frame, such as pathfinding, generation of procedural textures, custom physics, and so on. This function does not block the main thread, however, its completion is awaited at the end of the frame, so long-running tasks should be avoided.


## Code UpdateSyncThread


In the world logic ***updateSyncThread()***, you can specify any parallel logic functions you want to be executed before *[update()](#code_update)*. This function **blocks the Main Thread** until all calls are completed.


This function can be used to perform some heavy resource-consuming calculations such as pathfinding, generation of procedural textures, manipulations with big amounts of data, the result of which is required before the frame starts to be rendered. This function can also be used for simpler operations, that can be implemented in the *[update()](#code_update)* function, to distribute between threads and improve performance.


## Code Update


In the world logic ***update()***, you can put all functions to be called every frame, while your application is executed. It serves for implementing any logic. In brief, you can control a lot of things (whether graphics-related or not) from within the *update()*. Here you can:


- Create and delete nodes.
- [Move](../../../api/library/nodes/class.node_cpp.md#setPosition_Vec3_void) nodes around the scene and [rotate](../../../api/library/nodes/class.node_cpp.md#setRotation_quat_int_void) them.
- Change any parameters of nodes.
- Simulate [particle systems](../../../api/library/objects/class.objectparticles_cpp.md).
- Control [skinned animation](../../../api/library/objects/class.objectmeshskinned_cpp.md).
- Set global [rendering settings](../../../api/library/rendering/class.render_cpp.md).
- Create and manipulate your [GUI](../../../api/library/gui/class.gui_cpp.md).
- [Render to textures](../../../api/library/rendering/class.viewport_cpp.md).
- Execute [console](../../../api/library/engine/class.console_cpp.md) commands.
- Even do some physics � perform some momentary actions: add [impulses](../../../api/library/physics/class.bodyrigid_cpp.md#addImpulse_vec3_vec3_void), simulate a hit or a push, set [linear](../../../api/library/physics/class.bodyrigid_cpp.md#setLinearVelocity_vec3_void) or [angular velocity](../../../api/library/physics/class.bodyrigid_cpp.md#setAngularVelocity_vec3_void), add or remove [shapes](../../../api/library/physics/class.shape_cpp.md) and [joints](../../../api/library/physics/class.joint_cpp.md), and change their parameters.


> **Notice:** Do not apply [forces](../../../api/library/physics/class.bodyrigid_cpp.md#addForce_vec3_vec3_void) and [torques](../../../api/library/physics/class.bodyrigid_cpp.md#addTorque_vec3_void) to rigid bodies in the *update()*. Otherwise, you will get an unstable result that varies with each rendering frame. All continuous operations must be within *[*updatePhysics()*](#code_updatePhysics)*.


## Code UpdatePhysics


The ***updatePhysics()*** function of the world logic is mainly used to control physics in your application. As a rule this function is used for continuous operations such as pushing a car forward depending on current motor's RPM, simulating a wind blowing constantly, performing immediate collision response (as *updatePhysics()* can be executed several times during a single rendering frame, you can process multiple bounces of objects, when they collide with each other and monitor them, while the *update()* will only show us the final result), etc. The *updatePhysics()* is executed in the Main thread, so you can perform any actions here just like in the *update()*:


- Operate on all physical [bodies](../../../principles/physics/bodies/index.md) and [shapes](../../../principles/physics/shapes/index.md).
- Apply [forces](../../../api/library/physics/class.bodyrigid_cpp.md#addForce_vec3_void), [impulses](../../../api/library/physics/class.bodyrigid_cpp.md#addImpulse_vec3_vec3_void), and [torques](../../../api/library/physics/class.bodyrigid_cpp.md#addTorque_vec3_void) to [rigid bodies](../../../principles/physics/bodies/rigid/index.md).
- Create, attach, or break [joints](../../../api/library/physics/class.joint_cpp.md), as well as modify their parameters.
- Create and manipulate [shapes](../../../api/library/physics/class.shape_cpp.md) and modify their parameters.
- Create and adjust [physicals](../../../objects/effects/physicals/index.md).


You can as well do the following (and a lot more):


- Reposition and transform nodes if they are enabled.
- Create new nodes.
- Delete nodes.


## Code PostUpdate


The ***postUpdate()*** function of the world logic is an additional function used to correct behavior after the state of the node has been updated (for example, skinned animation has been played in the current frame or particle system has spawn its particles).


Imagine a situation when we need to attach an object (let's say, a sword) to the hand of a skinned mesh character. If we get transformation of the character hand bone and set it to the sword in the *[*update()*](#code_update)* function, the attachment will be loose rather than precise. The sword will not be tightly held in the hand, because the animation is actually played right after the world logic *update()* has been executed. This means, returned bone transformations in the *update()* will be for the previous frame. The world logic *postUpdate()* is executed after animation is played, which means you can get updated bone transformations for the current frame from within this function and set them to the sword.


> **Notice:** Use *postUpdate()* for correction purposes only; otherwise, this will increase the main loop time. All other functions should be placed within *[update()](#code_update)* or *[updatePhysics()](#code_updatePhysics)* (physics).


## Code Swap


Engine calls this function after the following processes are completed: rendering (CPU portion), physics calculations and pathfinding, GUI rendering, and all Async threads. The function is designed to process the results of the *[updateAsyncThread()](#code_updateAsyncThread)* method � all other methods (threads) have already been performed and are idle. After this function, only two actions occur:


- All objects that are queued for deletion are deleted.
- Profiler is updated.


## Event Handlers


You can also define your logic through callbacks that are invoked when certain events occur in your application.


It is important to note that event callbacks are not always executed immediately. For some types of events callbacks are placed into an internal execution queue and are processed during the next scheduled execution point according to the [Execution Sequence](../../../code/fundamentals/execution_sequence/index.md).


For instance, [body and joint events](../../../code/fundamentals/events/index_cpp.md#physics) are triggered at the end of the physics update, while *[WorldTrigger](../../../objects/worlds/world_trigger/index.md)* and *[NodeTrigger](../../../objects/nodes/trigger/index.md)* events are invoked in the middle of the Update stage. These events are executed at strictly defined points in the frame cycle, as the logic defined within them can affect rendering or other systems.


For more information about the Engine events, see the **[Event Handling](../../../code/fundamentals/events/index_cpp.md)** article.
