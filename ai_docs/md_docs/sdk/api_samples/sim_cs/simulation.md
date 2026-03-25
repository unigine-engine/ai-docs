# Simulation

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


## Crane Winch With Rope

![](../../../samples/img/csharp_sim_samples_crane_winch_with_rope.jpg)

This sample shows how to create a winch system with interactive rope simulation.


You can rotate the crane, adjust the rope length, change the mass of the attached load, and detach the load to observe the resulting physics behavior. Enabling the *[Visualizer](../../../api/library/engine/class.visualizer_cpp.md)* checkbox in the sample's UI displays the system's response to parameter adjustments. The rope includes an optional tension compensation feature, which helps maintain rope stability and realism under varying loads.


This type of winch is suitable for simulation of helicopter operations or heavy duty equipment towing. The rope is implemented as a C++ Component that you can use in your project.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_sim_samples/simulation/crane_winch_with_rope*
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


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_sim_samples/simulation/floating_buoy*
## LiDAR Sensor Emulation

![](../../../samples/img/csharp_sim_samples_lidar_sensor_emulation.jpg)

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


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_sim_samples/simulation/lidar_sensor_emulation*
## Robot Arm Manipulator

![](../../../samples/img/csharp_sim_samples_robot_arm_manipulator.jpg)

This sample demonstrates how to build a physics-based robotic arm with a kinematic chain composed of six links: one fixed and five movable. Each movable link is connected via a hinge joint (***[JointHinge](../../../principles/physics/joints/index.md#hinge)***) and driven by a motor that responds to keyboard inputs.


The arm's **end effector** is a **magnetic gripper** capable of **grabbing, holding, and releasing** dynamic objects in its environment. The gripper and each joint can be controlled independently via key bindings, which are configurable and demonstrated in the *Controls* section.


This setup provides a flexible starting point for creating custom robotic arms with any required number of degrees of freedom (DoF). You can replace manual input with a control system (e.g., inverse kinematics, AI, joystick, or ROS integration) to adapt the robot arm to your specific use case.


**Use Cases:**


- **Simulation & prototyping** of industrial robotic manipulators.
- **Educational environments** to teach principles of robotics, joint control, or physics-based animation.
- **AI training** for robotic arms using reinforcement learning or motion planning.
- **Human-machine interfaces**: test robotic interaction with dynamic environments.
- **Virtual reality** robotics simulations or operator training.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_sim_samples/simulation/robot_arm_manipulator*
## Ship Buoyancy (Physical)

This sample demonstrates how to implement **physically accurate buoyancy** for dynamic objects floating on **[Global Water](../../../objects/objects/water/water_object.md)**. A physical body is divided into a grid of virtual volume elements, each sampled independently for water height. Based on how much of each cell is submerged, the system:


- Calculates and applies distributed **buoyant forces**
- Adds appropriate **torque** to simulate rotation
- Applies **linear and angular damping** depending on submerged volume.


You can also define a **custom center of mass**, and optionally enable **debug visualization** of submerged sections, force directions, and sampling points via API. Use the **[Global Water](../../../objects/objects/water/water_object.md)** object across different **[Beaufort](../../../objects/objects/water/water_object.md#creating_waves)** slider parameter to adjust wave intensity.


This approach is useful for games and simulators involving boats, ships, debris, or physics-based water interactions.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_sim_samples/simulation/ship_buoyancy_physical*
## Thermal Sensor Emulation

![](../../../samples/img/csharp_sim_samples_thermal_sensor_emulation.jpg)

The sample demonstrates the use of **[post_sensor](../../../content/materials/library/postprocess/post_sensor/index.md)** postprocess materials for meshes and decals to create the effects for real-time sensor simulation of optical sensors in the EO (Electro-Optical) or IR (Infrared) passband (thermal, enhanced night vision, Forward-Looking Infrared (FLIR)).


For detailed information about each effect, refer to the descriptions on the plates in the scene.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_sim_samples/simulation/thermal_sensor_emulation*
