# Simulation of Physics


At physics simulation, physics calculations are in the **[multi-threaded](#multi_threaded)** mode � some operations are performed in parallel.


[**Physics performance profiler**](../../tools/profiling/profiler/index.md#physics) enables real-time tracking of simulation performance.


> **Notice:** To show the physics performance [profiler](../../code/console/index.md#show_profiler) that reports statistics on different physics simulation aspects, press ***1*** hotkey three times or type ***[show_profiler_physics](../../code/console/index.md#show_profiler_physics) �1*** in the console.


## Rate of Physics Simulation


UNIGINE physics module performs all its calculations. There are few things to point out about physics.


- It is simulated with its **[own fixed FPS](../../editor2/settings/physics_global/index.md#fps)**, which [does not depend](../../code/fundamentals/execution_sequence/index.md#framerates) on the rendering framerate. (The Engine FPS can also be [synchronized](../../api/library/physics/class.physics_cpp.md#isSyncEngineUpdateWithPhysics_int) with the physics one). > **Notice:** If physics takes more than the [assigned budget](../../editor2/settings/physics_global/index.md#physics_budget), further calculations are delayed. These calculations shall be performed during the subsequent rendering frames, making physics simulation look like in a "slow-motion" mode. The default budget is 50ms, but it can be increased, as necessary.
- During each tick, a number of calculation **[iterations](../../editor2/settings/physics_global/index.md#iterations)** can be performed. This includes the full cycle of physics simulation: > **Notice:** There is no point in setting the [number of iterations](../../editor2/settings/physics_global/index.md#iterations) too high. UNIGINE checks whether the next iteration can be performed within [physics budget limit](../../editor2/settings/physics_global/index.md#physics_budget), and if not, it is delayed and moved to the next rendering frame.

  1. *[updatePhysics()](../../code/fundamentals/execution_sequence/main_loop.md#physics_updatePhysics)* from the world logic is called.
  2. [Collision detection](../../principles/physics/collision/index.md) is performed.
  3. [Joints](../../principles/physics/joints/index.md) are solved.
  4. [Collision response](../../principles/physics/collision/index.md#collision_response) is performed.


## Physics Update Modes


There are two update modes available for physics simulation (each of them has its advantages and use cases):


- **Before Rendering** � physics update (along with the spatial tree update and user callbacks) is executed in the Main thread just before rendering is performed (*render*). The number of physics ticks executed before the rendering frame here is defined by the [physics and the Engine framerates](../../code/fundamentals/execution_sequence/index.md#cape_framerate). This mode is the most clear and straightforward (everything is executed safely in a strictly determined order) with no frame lag (results of physics calculations are applied in the current frame). But, on the other hand, this mode is the slowest as there are no asynchronous parallel calculations (everything's in the Main thread). Use this mode in case the time lag is unacceptabe for your application (you need all physics calculations to be applied in the current frame) and you want maximum simplicity and strictly determined order of execution for user code (*physicsUpdate* and physics callbacks).
- **Async Rendering** � physics update is performed asynchronously to rendering. In case of several physics ticks per one rendering frame (when the Engine framerate is lower, or [catching up](#catch_up) is performed), only the first one is executed in parallel, then the physics module waits for the completion of the rendering process, returns to the Main thread and executes the rest of the physics ticks. There is a frame lag (results of physics calculations are applied in the next frame) and there is some ambiguity regarding the time, when user code (*physicsUpdate* and physics callbacks) is to be executed in case of several physics ticks per one rendering frame (some part is executed before rendering while the other just after it). This mode is the fastest one and is used by default.


The modes are toggled in [Global Physics Settings](../../editor2/settings/physics_global/index.md#update_mode) in UnigineEditor.


### Catching Up


As the Engine has a variable framerate while the physics framerate is fixed, execution of physics calculations always adapts to the current situation.


In case the Engine framerate drops below the physics framerate (which is a very rare case), some of the physics frames have no enough time for execution and become missed. The physics module keeps such **missed frames** in memory for a certain period (called *Missed Frame Lifetime*) and tries to execute them when the situation gets better (Engine FPS grows) or when the CPU is idle while [waiting for GPU](../../code/fundamentals/execution_sequence/index.md#waiting_gpu) to complete rendering (if there is enough time). This is called **catching up** and helps avoiding "slow-motion" effect that occurs when physics frames are dropped off. In case of insufficient hardware capabilities missed frames are removed from the buffer as their lifetime expires and become lost forever.


Actual time of physics calcuations can go beyond the current [budget](../../editor2/settings/physics_global/index.md#physics_budget) as the ones performed while waiting for GPU are not taken into account. So the budget is not absolutely strict in this respect and can be exceeded if the CPU is idle.


## Deterministic Mode


Deterministic mode ensures that all contacts are solved in the predefined order and visualization of physics in the world is repetitive (on one computer). When this mode is enabled the Engine performs additional sorting of bodies, shapes and joints inside islands after building them.


Deterministic mode is unavailable in case there are missed frames � it is simply impossible. Moreover, there may be differences between visualization of physics on different hardware (e.g., AMD and Intel).


Determinism **is guaranteed** if there are no missed frames, the same Engine version is used, and the CPUs perform SSE operations similarly.


Please note that deterministic mode does not come for free, it may eat up to 10-20% of the frame rate, and it also depends on the scene a lot.


The mode can be enabled in [Global Physics Settings](../../editor2/settings/physics_global/index.md#determinism) in UnigineEditor.


## Stages of Physics Simulation


**Simulation** of physics goes through a number of stages when it is updated each iteration. They are as follows.


1. [Physics update](#updatePhysics)
2. [Сollision detection](#collision_detection)
3. [Simulation](#simulation)
4. [Synchronization of physics](#sync)


In the performance [profiler](../../code/console/index.md#show_profiler), the total time of physics simulation is displayed by the ***Physics*** counter.


### 1. Physics Update


1. Before anything else, a spatial tree is updated, this is performed in the Main thread regardless of the current [update mode](#update_mode). After we have the up-to-date data regarding how all objects with physical bodies are positioned, it would be safe to transform them or calculate collisions.
2. [C++ API Plugin](../../code/cpp/plugin.md) *[updatePhysics()](../../api/library/common/class.plugin_cpp.md#updatePhysics_void)* is called, if this function is implemented for the plugin.
3. Physics module calls the *updatePhysics()* of the *[world logic](../../code/fundamentals/execution_sequence/app_logic_system.md#world_script)*. Here you can call all functions that handle physics simulation and interactions (and not only that, see the details on *[updatePhysics()](../../code/fundamentals/execution_sequence/code_update.md#code_updatePhysics)* usage).


### 2. Collision Detection


After the script-based changes have been made (bodies with their [shapes](../../principles/physics/shapes/index.md) and [joints](../../principles/physics/joints/index.md) were transformed according to game logic, physics-based callbacks were set, etc.), physics can be simulated.


1. All objects that have physical [bodies](../../principles/physics/bodies/index.md) are found within the [Physical distance](../../editor2/settings/physics_global/index.md#physics_distance). They will be simulated during the current physics tick. Make sure that the physical distance in your UNIGINE-based application is not too small, because physical interactions beyond this limit are not simulated, so objects become frozen. However, even if at least one body belonging to an [island](../../principles/physics/collision/index.md#islands) is found within the physical distance, the whole island shall be simulated. > **Notice:** You can force to update nodes that are outside the [Physical distance](../../editor2/settings/physics_global/index.md#physics_distance) using *[addUpdateNode()](../../api/library/physics/class.physics_cpp.md#addUpdateNode_Node_void)* function.
2. All collisions ([shape-shape](../../principles/physics/collision/index.md#collision_types) and [shape-surface](../../principles/physics/collision/index.md#collision_types)) along with contact points are found for all colliding bodies among the ones found at the previous step (i.e., intersecting or have the distance between them less than the value of [penetration tolerance](../../editor2/settings/physics_global/index.md#penetration_tolerance)). Contact points are represented by their coordinates, normals, depth of shapes penetration, relative velocity (between two bodies), relative friction and restitution. So, here we collect all the data that is required to resolve collisions later. > **Notice:** If a body is [frozen](../../principles/physics/bodies/index.md#freezing) and no contacts are found that would push it out of its frozen state with strong enough impulse, such body is not simulated in the current tick.
3. [Islands](../../principles/physics/collision/index.md#islands) are built using the contacts obtained at the previos step.
4. Bodies, shapes and joints are sorted inside islands. By that, we ensure that contacts are solved in the predefined order and visualization of physics in the world is repetitive (on one computer).


In the performance [profiler](../../code/console/index.md#show_profiler_physics) you can find:


- The total time of collision detection is displayed by the **PCollision** counter.
- The number of contacts is displayed by the **PContacts** counter.
- The number of islands is shown by the **PIslands** counter.
- The number of bodies is shown by the **PBodies** counter.
- The total number of joints is shown by the **PJoints** counter.


#### Continuous Collision Detection


If a shape participates in the contact with any other shape or surface, continuous collision detection (**CCD**) is performed. UNIGINE takes velocities of the body, radius of its shape and calculates what contacts this body will have (during the current physics tick), assuming it continues its current trajectory. So, unlike the simple collision detection, contacts are analyzed not discretely, once per physics tick, but are instead calculated for the entire current physics tick.


> **Notice:** By default, continuous collision detection is enabled only for [sphere](../../principles/physics/shapes/index.md#sphere) and [capsule](../../principles/physics/shapes/index.md#capsule) shapes. For other shape types, it must be [enabled manually](../../api/library/physics/class.shape_cpp.md#setContinuous_int_void).


### 3. Simulation


When a collision has been detected, [**collision response**](../../principles/physics/collision/index.md#collision_response) is calculated, so that the colliding bodies would gain new velocities.


1. Here bodies are prepared to participate in collisions: contacts found for them are cached together with contacts from the previous frame � to ensure that they interact with each other properly.
2. Collision response for each body is calculated. Based on the gathered contact points data, the Engine computes the impulse each body gets after collision. Contact points are solved in a pseudo-random order to achieve simulation stability and reproducibility.
3. When contact responses are calculated, [joints](../../principles/physics/joints/index.md) constraining relative motion of bodies are solved. Joints are solved in the pseudo-random order just like contact points. > **Notice:** Within one physics iteration, joints can be solved several times. The high number of joint iterations increase the precision of calculations, as well as computational load. In the performance [profiler](../../code/console/index.md#show_profiler), the total time of both collision response and joint solving stages is displayed by the **PResponse** counter.
4. The results of contact and joint solving are accumulated and, finally, are applied to bodies. The coordinates of the bodies change according to their new linear and angular velocities. In the performance [profiler](../../code/console/index.md#show_profiler), the time of this stage is displayed by the **PIntegrate** counter.


In the performance [profiler](../../code/console/index.md#show_profiler), the total time of simulation stage is displayed by the **PSimulation** counter.


### 4. Synchronization of Physics


**Synchronization** is the final stage of physics simulation. During the *[swap()](../../code/fundamentals/execution_sequence/main_loop.md#swap)* in the UNIGINE main loop, physics module calls its internal *updatePhysics()* function. Bodies set their calculated transformations to objects. In the next frame, objects will be rendered in their new physics-based positions.


> **Notice:** In the *[Async Rendering](#update_mode)* update mode physics simulation [goes in parallel](../../code/fundamentals/execution_sequence/main_loop.md#postUpdate) to the actual rendering process. This is the reason calculated physics is visible only in the next frame.


If visualizer options are enabled, shapes, joints or contacts of non-frozen bodies will be rendered.


## Multi-Threaded Physics Simulation


**Multi-threaded** simulation of physics is run when the *[Async Rendering](#update_mode)* update mode is selected and there are two or more physics threads.


1. *[updatePhysics()](../../code/fundamentals/execution_sequence/code_update.md#code_updatePhysics)* from the world script is always performed in the main physics thread.
2. After that, the Engine takes advantage of multiple CPUs during the [collision detection](#collision_detection) and [simulation stage](#simulation).

  - Contacts for all physical bodies within the [physical distance](../../editor2/settings/physics_global/index.md#physics_distance) are found along with all necessary information.
  - [Islands](../../principles/physics/collision/index.md#islands) are created based on the data on object collisions.
  - As islands have been created, they can be safely handled in separate threads, because they are isolated.
  - Then threaded islands are synchronized in the main physics thread to exchange data about the current contacts and ones from the previous frames. It will ensure proper physical behavior of bodies.
  - From there on, collision response and joints solving are again calculated per island in separate threads.
3. Before physics is synchronized with the world, the engine waits for all threads to finish their calculations. When thread synchronization happens (during the *[swap](../../code/fundamentals/execution_sequence/main_loop.md#swap)* stage of the UNIGINE main loop), all assigned physics callbacks are executed in the main thread (the order is as follows: bodies, joints, and triggers), and then physics is applied to nodes. > **Notice:** Physics callbacks (mainly used for creation, destruction or modification of other objects) are called in the main thread, as this is the only place where such operations can be performed safely.
