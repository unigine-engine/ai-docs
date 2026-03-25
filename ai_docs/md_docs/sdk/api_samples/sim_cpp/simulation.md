# Simulation

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


## Crane Winch With Rope

This sample shows how to create a winch system with interactive rope simulation.


You can rotate the crane, adjust the rope length, change the mass of the attached load, and detach the load to observe the resulting physics behavior. Enabling the *[Visualizer](../../../api/library/engine/class.visualizer_cpp.md)* checkbox in the sample's UI displays the system's response to parameter adjustments. The rope includes an optional tension compensation feature, which helps maintain rope stability and realism under varying loads.


This type of winch is suitable for simulation of helicopter operations or heavy duty equipment towing. The rope is implemented as a C++ Component that you can use in your project.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/simulation/crane_winch_with_rope*
## Fire Hose Extinguishing

This sample demonstrates how to implement a fire hose system using *[decals](../../../objects/decals/ortho/index.md)* and *[particle](../../../objects/effects/particles/index.md)* collisions. Foam particles are emitted from a hose, interact with the environment, and leave visual marks on surfaces. When aimed at fire sources, the foam gradually extinguishes them over time. Foam decals accumulate and persist for a limited duration, fading and expanding gradually to simulate realistic dispersion.


The emitter direction can be set to a fixed angle using the *Angle* slider, or enabled to sweep back and forth smoothly when the *Rotate* checkbox is selected, mimicking realistic hose motion.


This approach can be used to simulate fire suppression in interactive gameplay, emergency response training, or realistic firefighting visualizations.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/simulation/fire_hose_extinguishing*
## Floating Buoy

This sample demonstrates realistic water interaction in UNIGINE, showcasing both the current state of **[Global Water](../../../objects/objects/water/water_object.md)** control via changing **[Beaufort](../../../objects/objects/water/water_object.md#creating_waves)** levels and the use of fetching the water level at a certain point for a simplified simulation of buoyancy without engaging Physics.


**Core Features:**


**Global Water Control.** Adjust ocean conditions in real-time using the **Beaufort slider** (0-12). Higher values create stormier waves with enhanced foam and detail.


**Optimized Buoyancy System**. Simulates floating objects without full physics collisions. Uses three anchor points for stable wave-following behavior. It then smoothly adjusts the object's position and rotation to match the waves, with calculations based on:


- Object mass (customizable)
- Global buoyancy coefficient (adjustable via **Buoyancy slider**)
- Water surface steepness and wave height.


**Use Cases:**


- Marine simulations
- Weather system prototyping
- Performance-sensitive scenes with many floating objects
- Games needing stylized water interactions.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/simulation/floating_buoy*
## Flocking

This sample demonstrates the simulation and control of flocking behavior (Boids algorithm) for different types of entities, such as birds and fish. Two separate controllers manage the behavior of these groups using common flocking principles like cohesion, alignment, and separation.


You can adjust various parameters in real time to observe how they influence the behavior of each flock:


- **Cohesion** - strength of attraction toward the center of the flock.
- **Spot Radius** - distance within which other units are considered for cohesion and alignment.
- **Alignment** - force that aligns a unit's direction with the average heading of its neighbors.
- **Separation** - repulsion force that prevents units from crowding too closely.
- **Separation Desired Range** - distance threshold for applying separation force.
- **Target** - amount of force directed towards target.
- **Unit Max Speed** - maximum unit speed.
- **Unit Max Force** - maximum steering force applied for movement corrections.
- **Unit Max Turn Speed** - how quickly a unit can rotate to adjust direction.


Two independent flocks (e.g., fish and birds) demonstrate how multiple controllers can operate simultaneously with distinct settings. Optional debug visualization renders bounding boxes around each flock, helping observe bounds and transitions.


**Use Cases**


- **Games and simulations** - realistic swarm behavior for birds, fish, insects, crowds, or drones.
- **Training AI systems** - testing multi-agent behavior and interaction dynamics.
- **Environmental storytelling** - adding life to ecosystems and natural environments.
- **Cinematic scenes** - choreographed group movements for visual impact.
- **Education and research** - exploring emergent behavior in decentralized systems.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/simulation/flocking*
## High-Level Car Physics System

![](../../../samples/img/cpp_sim_samples_high_level_car_physics_system.jpg)

This sample showcases the **[High-Level Car Physics System](../../../code/usage/vehicle_physics/index.md)**. To learn more on using the system to create your own wheeled vehicle simulation please refer to this article.


**Features:**


- Setting engine's power and resistance curves, as well as idle speed (RPM).
- Gearbox simulation (manual and automatic) enabling you to adjust throttle and speed values for shifting gears along with transition time, as well as to set the number of gears and configure gear ratios.
- Mathematical wheel model for more realistic steering, enabling simulation of forces affecting the rotating wheel, along with an ability to adjust suspension travel distance, spring, and damping values.
- Easy setup of steering and driving axes along with capability to turn the differential lock on and off.
- Switching between different views (driver's view, external camera, etc.).
- Simulation of various surface conditions (such as dry, wet, snow-covered, or icy road, mud, and so on).
- A set of debug windows displaying information on all vehicle parameters in real time.


Fine-Tuning the *Wheel Joystick*:


If you use a wheel device, you might need to readjust settings to control the vehicle properly.


- Run the sample and press **F3** to visualize the axes.
- Check the controls status - which axis each control corresponds to.
- If the controls mismatch, open the demo project in UnigineEditor to reconfigure them. Find the **joystick_input** node, it has the **car_joystick_input** property assigned. Adjust the **Joystick Axis** parameter where required.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/simulation/high_level_car_physics_system*
## LiDAR Sensor Emulation

![](../../../samples/img/cpp_sim_samples_lidar_sensor_emulation.jpg)

This sample demonstrates a realistic **LiDAR** sensor simulation, used in self-driving cars, robotics, robot vacuum cleaners, and drones to map their surroundings. It works by combining four (or optionally more) virtual depth cameras to create a full 360-degree scan. The **LiDAR** emits rays and measures distances by rendering a depth map of the environment. In addition, a response intensity for each ray is calculated using normal, roughness and metalness from the G-buffer. You can tweak its settings (scan range, FOV, resolution, etc.) via API.


**Key Features:**


- Emulated LiDAR using 4 or more rendered views
- Configurable **min/max range, FOV, beam resolution** (number of stacks and slices)
- Asynchronous data transfer using *[asyncTransferTextureToImage](../../../api/library/rendering/class.render_cpp.md#asyncTransferTextureToImage_TextureToImageTransfered_TextureToImageTransfered_Texture_void)*
- Dynamic beam caching, image post-processing, and world-space point rendering
- Optional visual debugging: depth maps, scan points, and frustums
- Auto-refreshing system with internal transform and scan updates.


**Use Cases:**


- Autonomous vehicle simulation (robot vacuums, drones, cars)
- Autopilot and AI training using virtual LiDAR input
- Robot navigation and localization (SLAM, path planning).


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/simulation/lidar_sensor_emulation*
## Moving Crane With Rope Slings

![](../../../samples/img/cpp_sim_samples_moving_crane_with_rope_slings.jpg)

This sample demonstates how to imitate a crane with sling ropes transferring an object.


The scene contains the manipulator with the ropes connected to it. Ropes are also connected to the load, which has *[BodyRigid](../../../principles/physics/bodies/rigid/index.md)* assigned. The connection points are set via **AttachPoint**.


You can move the load around the scene by dragging the manipulator with the mouse, and make it interact with the wall also available in the scene.


Physics is simulated at 120 fps with 10 iterations to adjust the distance between points. The physics update for the load is adjusted by impulses to ensure proper interaction with the environment.


Ropes are created using an arbitrary set of points and *[joints](../../../principles/physics/joints/index.md)* between them. This approach can be used to create any kind of rope or even a net consisting of a number of ropes, a wire, or a primitive *[cloth](../../../principles/physics/bodies/cloth/index.md)*.


You can use the sample ropes as a basis for your specific task by configuring their parameters as required.


Indices for segments are generated randomly to avoid a linear accumulation of error in joints.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/simulation/moving_crane_with_rope_slings*
## Power Line Wires Sag

![](../../../samples/img/cpp_sim_samples_power_line_wires_sag.jpg)

This sample demonstrates how to create wires using the **RopeSystem** component. You can adjust the wire diameter and generate a new mesh based on the updated value. The plane included in the scene can be moved to make the wires swing.


Simulating wires doesn't require a high number of physics iterations or a high frame rate, as they typically remain stationary and only swing in place. However, if the wires in your scene are primarily decorative and don't need any physical interaction, consider using a static mesh instead to improve performance.


Ropes are created using an arbitrary set of points and *[joints](../../../principles/physics/joints/index.md)* between them. This approach can be used to create any kind of rope or even a net consisting of a number of ropes, a wire, or a primitive *[cloth](../../../principles/physics/bodies/cloth/index.md)*.


You can use the sample ropes as a basis for your specific task by configuring their parameters as required.


Indices for segments are generated randomly to avoid a linear accumulation of error in joints.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/simulation/power_line_wires_sag*
## Robot Arm Manipulator

![](../../../samples/img/cpp_sim_samples_robot_arm_manipulator.jpg)

This sample demonstrates how to build a physics-based robotic arm with a kinematic chain composed of six links: one fixed and five movable. Each movable link is connected via a hinge joint (*[JointHinge](../../../principles/physics/joints/index.md#hinge)*) and driven by a motor that responds to keyboard inputs.


The arm's **end effector** is a **magnetic gripper** capable of **grabbing, holding, and releasing** dynamic objects in its environment. The gripper and each joint can be controlled independently via key bindings, which are configurable and demonstrated in the *Controls* section.


This setup provides a flexible starting point for creating custom robotic arms with any required number of degrees of freedom (DoF). You can replace manual input with a control system (e.g., inverse kinematics, AI, joystick, or ROS integration) to adapt the robot arm to your specific use case.


**Use Cases:**


- **Simulation & prototyping** of industrial robotic manipulators.
- **Educational environments** to teach principles of robotics, joint control, or physics-based animation.
- **AI training** for robotic arms using reinforcement learning or motion planning.
- **Human-machine interfaces**: test robotic interaction with dynamic environments.
- **Virtual reality** robotics simulations or operator training.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/simulation/robot_arm_manipulator*
## Ship Buoyancy (High-Accuracy Voxel Approximation)

This sample demonstrates how to implement **physically accurate buoyancy** for objects floating on **[Global Water](../../../objects/objects/water/water_object.md)**. A grid of virtual volume elements is generated around a physical body using its surface. Each voxel in the grid is evaluated to determine whether it lies above or below the water surface. Submerged voxels are visualized in blue. For every voxel below the water surface, the system:


- Calculates and applies distributed **buoyant forces**.
- Applies **[linear and angular damping](../../../principles/physics/bodies/index.md#damping)**.


You can also define a **custom [center of mass](../../../principles/physics/bodies/index.md#mass_center)**, and optionally enable **debug visualization** of force directions, and sampling points via API. Use the **Beaufort** slider parameter to adjust wave intensity.


**Use Cases:**


- Marine simulations involving boats, ships, debris
- Performance-sensitive scenes with many floating objects
- Games needing stylized water interactions.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/simulation/ship_buoyancy_high_accuracy_voxel_approximation*
## Ship Buoyancy (Physical)

This sample demonstrates how to implement **physically accurate buoyancy** for dynamic objects floating on **[Global Water](../../../objects/objects/water/water_object.md)**. A physical body is divided into a grid of virtual volume elements, each sampled independently for water height. Based on how much of each cell is submerged, the system:


- Calculates and applies distributed **buoyant forces**
- Adds appropriate **torque** to simulate rotation
- Applies **linear and angular damping** depending on submerged volume.


You can also define a **custom center of mass**, and optionally enable **debug visualization** of submerged sections, force directions, and sampling points via API. Use the **[Global Water](../../../objects/objects/water/water_object.md)** object across different **[Beaufort](../../../objects/objects/water/water_object.md#creating_waves)** slider parameter to adjust wave intensity.


This approach is useful for games and simulators involving boats, ships, debris, or physics-based water interactions.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/simulation/ship_buoyancy_physical*
## Tracked Vehicle (Physical)

This sample demonstrates how to imitate the vehicle tracks using physical (i.e. having body and shape) track plates, wheels, and hinge joints (**[JointHinge](../../../principles/physics/joints/index.md#hinge)**). It illustrates how physical tracks behave on interacting with various obstacles and when rotating depending on the vehicle speed.
**SDK Path:***<SAMPLES_PROJECT_PATH>/source/simulation/tracked_vehicle_physical*

## Tracked Vehicle (Simple)

This sample demonstrates how to imitate the vehicle tracks using non-physical (i.e. without body assigned) track plates, wheels, and joints (**[JointWheel](../../../principles/physics/joints/index.md#wheel)**). It illustrates how non-physical tracks interact with various obstacles.
**SDK Path:***<SAMPLES_PROJECT_PATH>/source/simulation/tracked_vehicle_simple*
