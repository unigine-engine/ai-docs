# High-Level Car Physics System (C++)


![](car_physics.jpg)


Wheeled vehicles are widely used in various simulations. The high-level Car Physics system, implemented as a set of [C++ components](../../../principles/component_system/component_system_cpp/index.md), is intended to simplify creation of realistic wheeled vehicles in UNIGINE. It minimizes efforts required to create virtually any wheeled vehicle, be it a 4WD SUV, an exploration rover, or a sophisticated multi-axle transporter.


The following features are available:


- Setting the engine power and resistance curves, as well as idle speed (RPM)
- Gearbox simulation (manual and automatic) enabling you to adjust throttle and speed values for shifting gears along with transition time, as well as to set the number of gears and configure gear ratios
- A [transfer case](#components_car_transfer_case) distributing torque between the axles, with low and high range for off-road driving
- Easy setup of steering and driving axes, with locking of both the interwheel and inter-axle differentials
- Mathematical wheel model for more realistic steering, enabling simulation of forces affecting the rotating wheel, along with an ability to adjust suspension travel distance, spring, and damping values
- [Simulation of various surface conditions](#friction) (such as dry, wet, snow-covered, or icy road, mud, and so on)
- [Switching between different views](#camera_switch) (driver's, external camera, etc.)
- [Keyboard, gamepad, and wheel device input](#user_input) working simultaneously
- A set of [debug windows](#debug_windows) displaying information on all vehicle parameters in real time


Instructions given below cover the process of creation of a wheeled vehicle using the C++ SIM sample from the SDK in a new empty project. The step-by-step guide will take you through the process of creating all necessary nodes and configuring component parameters you need to have a functional vehicle, assuming that you have a model of the vehicle's body and models of its wheels at your disposal.


### See also


- The *[C++ Component System](../../../principles/component_system/component_system_cpp/index.md)* article to learn more about implementing logic in C++ using components.
- The C++ SIM sample included in the SDK.


## Step 1. Prepare a Project


First, we should prepare a project and get all necessary source files containing implementation of components from the C++ SIM sample. So, we perform the following actions:


1. [Create a new C++ project](../../../sdk/projects/index_cpp.md#creation). ![](../using_component_system/create.png)
2. Open your new project's `source` folder and create the new `vehicle_components` folder in it.
3. Then open the folder of the C++ SIM sample and copy all the files it contains to the `vehicle_components` folder that you've just created.
4. Open your project in the IDE and add all source files from the `vehicle_components` folder to it.
5. Add initialization code for C++ Component System to the *[AppSystemLogic::init()](../../../code/fundamentals/execution_sequence/app_logic_system.md#systemlogic_init)* method: ```cpp #include <UnigineComponentSystem.h> /* ... */ int AppSystemLogic::init() { /* ... */ // initialize ComponentSystem and register all components Unigine::ComponentSystem::get()->initialize(); /* ... */ } ```
6. Build and run your project to register all components and generate necessary properties. We are going to use these properties later to configure our vehicle. Meanwhile, we can proceed to the next step.


## Step 2. Prepare Your Vehicle Model


Next, we create a model representing the vehicle's body and a model for vehicle's wheels (or several models, depending on how many different types of wheels your vehicle has).


> **Notice:** A single mesh should be used for dual wheels.


The **Y** axis of all models (including wheels) should be pointing forward. So, you can't just make a copy of a wheel and rotate it around the **Z** axis by 180 degrees.


![](model_axes.png)


The scale of all models should be equal to 1 along all axes, to ensure correct physics simulation.


## Step 3. Create Node Hierarchy


In order for the system to work, your vehicle's hierarchy should be properly organized. The following hierarchy is recommended:


![](node_hierarchy.png)


All nodes in the hierarchy, except for the vehicle's body and wheels, are *[Node Dummy](../../../objects/nodes/dummy/index.md)*. These *Node Dummy* serve only to organize the components logic and have an identity transform matrix, except for the **center_of_mass**, as its position defines the position of the vehicle's center of mass in the local coordinates of the vehicle's body (must have the body as parent).


## Step 4. Engage Physics


Then, we should assign a [rigid body](../../../principles/physics/bodies/rigid/index.md) to the object representing the vehicle's body and disable the *Shape-Based* option for it, to turn off automatic calculation as inertia, mass, and center of mass are specified in the component. Then, add necessary number of physical shapes to specify the geometry of the body.


[![](add_physics_sm.png)](add_physics.png)


## Step 5. Assign and Configure Components


At this stage we assign component properties generated at **[Step 1](#prepare)** and configure necessary parameters for the engine, transmission, wheels, etc.


### Configure Vehicle Body


Assign the **car** component to the object representing the vehicle's body. For this component we should specify necessary car characteristics, such as *dimensions, mass, frontal area*, etc. along with the *number of iterations*, which defines joints simulation accuracy. Here we also set up links to *[Node Dummy](../../../objects/nodes/dummy/index.md)* with other logic components assigned ([engine](#components_car_engine), [gearbox](#components_car_gearbox), [transfer case](#components_car_transfer_case), [wheels](#components_car_wheel), [axles](#components_car_axle)).


![](car_component.png)


| Iterations | The number of iterations used to solve joints. If the value is too low, the precision of calculations will suffer. |
|---|---|
| Car Body Node | Object representing the car body. |
| Size | Car dimensions, in meters (width, length, height). |
| Mass | Vehicle mass, in kilograms. A lifelike value is to be used. Higher values increase the car stability when colliding with other cars. Along with that, higher values increase inertia thus requiring enhanced brakes and springs, better grip of wheels, etc. > **Notice:** This value affects numerous aspects of the vehicle behavior, therefore it's better to set it first. |
| Driving Efficiency | Multiplier of the gear ratio. The efficiency of the whole transmission - all moving parts from wheels to the gearbox. Higher values mean less inertia and resistance in the gearbox. |
| Movement Resistance | The effect of resistance to the movement. The higher the value, the more the wheels resist rotation (transmitting this resistance to the engine, reducing its power). The effect is amplified by large and heavy wheels. |
| Moving Transmission Parts Inertia | Inertia multiplier for moving parts of transmission used to calculate the vehicle moment of inertia. The higher the value, the more inert the gearbox is. |
| Air Density | Air density that affects downforce. The faster you drive, the more the car is pressed against the asphalt, while at the same time control is improved due to increased road grip. It is recommended to keep this value unchanged and adjust the *[CarFrontalArea](#carfrontalarea)* and *[ShapeResistanceCoefficient](#shaperesistancecoefficient)* parameters, if required. |
| Car Frontal Area | Maximum cross-sectional area of the vehicle used for calculation of the drag coefficient (less for cars, more for trucks). |
| Shape Resistance Coefficient | Drag coefficient of the shape which can be obtained experimentally in the wind tunnel (more in cars, less in trucks). |
| Clutch Sync Factor | Clutch multiplier, the degree of synchronization between the engine and the gearbox. The higher the value, the more the engine rpm drops when torque is transmitted. |
| Center Of Mass | Reference to the node that is the vehicle's center of mass. This node affects the wind resistance and stability of the vehicle. The closer it is to the ground, the higher is the stability. If the center of mass is below the ground, the behavior may feel unrealistic when the car rolls over. |
| Input | Node with a vehicle [input interface component](#user_input) assigned. |
| Engine | Node with a vehicle [engine component](#components_car_engine) assigned. |
| Gearbox | Node with a vehicle [gearbox component](#components_car_gearbox) assigned. |
| Transfer Case | Node with a vehicle [transfer case component](#components_car_transfer_case) assigned. |
| Axles | Nodes with a vehicle [axle component](#components_car_axle) assigned. Axles are to be specified in the **front-to-rear** order. |


### Engine


Assign the **car_engine** component to the **engine** *Node Dummy* and specify necessary engine parameters, such as *maximum, minimum*, and *idle rpm* values, *inertia* of moving parts of the transmission and set up dependencies for *torque* and *resistance* on rpm.


> **Notice:** **RPM-Torque** and **RPM-Resistance** values should be specified in the ascending order. Each of these arrays must have at least **2** elements.


![](car_engine.png)


| Min RPM | Minimum engine rotation per minute. If the engine RPM is less than this value, the engine is considered to have stalled. |
|---|---|
| Max RPM | Maximum engine rotation per minute. |
| Idle RPM | Idle engine rotation per minute, when the vehicle is not moving and the gas pedal is not pressed. |
| Inertia | Moment of inertia of the engine moving parts. Higher values mean slower changes in engine RPM. |
| Idle Throttle | Automatic throttle level helping to keep stable idle rpm. It defines the minimum throttle plate position, if the engine RPM is less than minimum (idle). |
| RPM - Torque | Correlation between the engine RPM and Torque. Specific torque values can be set for various RPMs. Changing the value affects speed and acceleration. |
| RPM - Resistance | Correlation between the engine RPM and Resistance - friction of the internal engine details depending on the RPM changes. Higher resistance values mean that the vehicle will pick up speed less. |


Formulas applied in the engine implementation:


- result_torque = torque - resistance - gearbox_resistance * clutch
- result_inertia = inertia + gearbox_inertia * clutch
- current_rpm += result_torque / result_inertia


### Gearbox


Assign the **car_gearbox** component to the **gearbox** node. Here we set transmission type (MT or AT), specify all gear numbers and shifting time. This component also controls switching between the gears (AT), so for each gear we should set *throttle* and *speed* values for switching up or down to the next gear.


![](car_gearbox.png)


The array of gear values must contain at least **3** elements: *neutral, first front*, and *rear*. Tables describing Up and Down switching sequences should have the number of elements equal to the number of transitions: **number of forward gears - 1**. For example, for a 3-speed gearbox we have:


- **1 -> 2**
- **2 -> 3**


> **Notice:** Each element of the array should contain at least one *Throttle-Speed* pair for the corresponding transition.


| Gear Values | Gear ratio at each stage. The first element is set for neutral, and the last one is for the reverse. Higher values mean a higher output (it will be easier for the vehicle to climb the hill) at a slower speed (wheels rotate slower). Usually the gear values are in descending order. Adjust these values if you want a faster car (higher values at the beginning and lower values at the end). |
|---|---|
| Automatic | If enabled, the transmission is automatic (AT), if disabled, the transmission is manual (MT). |
| Shift Time | Interval for switching between gears, in seconds. |
| Gear Switching Sequence Up | Array of conditions describing the sequence of switching the gears up: the Throttle value (0, 1] and current speed in km/h. The first row corresponds to switching 1->2, the second one 2->3, etc. |
| Gear Switching Sequence Down | Array of conditions describing the sequence of switching the gears down: the Throttle value (0, 1] and current speed in km/h. The first row corresponds to switching 2->1, the second one 3->2, etc. |


### Transfer Case


Assign the **car_transfer_case** component to the **transfer_case** *Node Dummy*. Specify necessary parameters and configure torque distribution for all axles in the **front-to-back** order.


![](transfer_case.png)


| Low Gear | Lower gear ratio. It is used to make it easier to pass difficult off-road sections, where the full power of the engine is required, and speed is not important. |
|---|---|
| High Gear | Higher (regular) gear ratio. |
| Is Used | If enabled, transfer case is used. If disabled, an even distribution of torque and rpm from the transmission is used between all axles. |
| Has Inter-Axle Lock | Inter-axle lock. Used on off-the-road vehicles. |
| Dynamic Lock | Dynamic inter-axle differential locking. If this option is enabled, the lock can be enabled when the vehicle is moving on receiving the information that its wheels have started to spin. |
| Torque Distribution | Torque distribution between all axles of the vehicle, in percent. The sum must be equal to 100%. |


### Axles


Assign the **car_axle** component to every *Node Dummy* representing vehicle's axles (e.g. **front_axis** and **rear_axis**). You can create as many axles as you need. For each axle, attach nodes representing wheels as children, and specify them in the corresponding fields of the **car_axle** component.


![](car_axle.png)


Then specify if the axle is a steering/driving one, if it has a locking differential, etc.


| Main Gear Ratio | Main gear ratio, the difference between what goes to the axle and what goes to wheels. |
|---|---|
| Driving | Indicates if the axle is the driving one. |
| Steering | Indicates if the axle is the steering one (i.e. whether the wheels on this axis are turned). |
| Max Steering Angle | The maximum angle of the wheel rotation, in degrees (relative to the steering axis, Z-axis). Affects the ease of turning in tight places. |
| Use Handbrake | Indicates if the axle is affected by the handbrake. |
| Locking Differential | Indicates if the axle has interwheel locking, which is required for off-road vehicles to drive safely in the mud. If it is turned on, it is easier to drive in the mud keeping your wheels straight, but turning corners will be harder, because while turning the wheels should rotate at different speed, however with locking turned on, they start rotating at the same speed, which increases the risk of drifting. |
| Dynamic Lock | Indicates if locking differential can be toggled on and off, while the vehicle is moving. It works only if Locking Differential is enabled. |
| Right Wheel Node | Link to the node representing the right wheel of the axle (relative to forward direction). |
| Left Wheel Node | Link to the node representing the left wheel of the axle (relative to forward direction). |


### Wheels


Assign the **car_wheel** component to all nodes representing vehicle's wheels. By adjusting the parameters of this component we can simulate different physical behavior of the vehicle with various types of wheels. Here you can set up wheel *mass* and *radius, friction* and *additional forces*, as well as suspension parameters.


![](wheel_component.png)


You can enable the **Use General Settings** option and specify a preset property with general wheel settings for a certain wheel type in the **General Settings** field to override values of component parameters. This simplifies configuration process: you set all required parameter values for a certain wheel type in a dedicated property, and then use this property for all similar wheels.


[Suspension settings](#suspension_settings) are to be set individually for each car by eye. These settings affect the vehicle bouncing, rigidity and wind resistance when driving over bumps and around tight corners.


| General |  |
|---|---|
| Wheel Node | Node representing the wheel. A single mesh should be used for dual wheels. |
| Use General Settings | Enabling this option allows using a preset property specified in the *[General Settings](#wheel_general_settings)* field. This property contains general wheel settings for a certain wheel type to override values of the component parameters listed below. This can be used to simplify configuration process: you set all required parameter values for a certain wheel type in a dedicated property, and then enable this option and assign this property to the field below. |
| General Settings | Preset property with general wheel settings for a certain wheel type to be used instead of the values of the component parameters listed below. |
| Mass | Wheel mass, in kilograms. Setting a higher value requires a more powerful engine to rotate the wheel. |
| Radius | Wheel radius, in meters. |
| Joint Parameters |  |
| Linear Restitution | Linear stiffness of the joint. In the physical engine, the wheel and the vehicle body are two different bodies, not connected to each other. When these bodies move apart, the restitution value controls the amount of force applied to both bodies so that their fulcrums are aligned again. At the value of 1.0 all the energy from hitting the wheel is transferred to the body instantly. At the value of 0.5 the wheel moves slightly relative to the body. It imitates the suspension arms reducing the impact. |
| Angular Restitution | Angular stiffness of the joint. This value is similar to *Linear Restitution*, but affects rotation: it controls the effect of the vehicle body rotation on the wheel rotation and vice versa. |
| Linear Softness | Linear elasticity of the wheel joint. Defines whether linear velocities of the bodies are averaged out when the joint is stretched. The value of 0 means that the joint is rigid. |
| Angular Softness | Angular elasticity of the wheel joint. Defines whether angular velocities of the bodies are averaged out when the joint is twisted. The value of 0 means that the joint is rigid. |
| Suspension |  |
| Suspension Damping | Linear damping coefficient of the suspension. Higher values ensure faster vibration damping of the vehicle when driving over the bumps. |
| Suspension Spring | Suspension spring rigidity coefficient determining how strong the spring resists the vertical linear motion. If set to 0, the spring is disabled. Higher values cause more bouncing when hitting the curb. |
| Suspension Distance From | The lowest possible position of the wheel (relative to the initial position). This value together with *Suspension Distance To* forms the height of the vehicle suspension. The more this interval is, the easier it is for the vehicle to drive over bumps, but at the same time it becomes more wobbly. |
| Suspension Distance To | The highest possible position of the wheel (relative to the initial position). This value together with *Suspension Distance From* forms the height of the vehicle suspension. The more this interval is, the easier it is for the vehicle to drive over bumps, but at the same time it becomes more wobbly. |
| Suspension Target Distance | Suspension height at rest, the value between the *Distance From* and *Distance To* values. The suspension spring, if enabled, tries to keep the specified height. |
| Braking |  |
| Max Brake Damping | Maximum damping coefficient of the brake. |
| Max Handbrake Damping | Maximum damping coefficient of the handbrake. |
| Tire |  |
| Tire Damping | Damping coefficient of the tire. This value adds up to *Max Brake Damping* and *Max Handbrake Damping*. Can be perceived as the resistance of the wheels to air flow. |
| Friction |  |
| Forward Friction | Longitudinal friction of the tires. Higher values reduce the likelihood of wheels spinning in place. This value also may enhance acceleration and improve braking performance. |
| Lateral Friction | Transverse friction of the tires. Higher values reduce the likelihood of drifting (for the front wheels) or skidding (for the rear wheels) also increasing the steerability - the vehicle seems to turn sharper and faster. |
| Additional Forces |  |
| Forward Factor | Coefficient specifying how fast the optimum longitudinal force can be achieved. Higher values increase the impulse produced by the tire. |
| Lateral Factor | Coefficient specifying how fast the optimum lateral force can be achieved. Higher values increase the impulse produced by the tire. |
| Threshold Factor | Threshold value between the wheel and "ground" velocities. If the value is too small, the longitudinal force is scaled down to prevent unnatural vibrations. |


## Step 6. Set Up Input Controls


You can choose to use various types of input devices to control your vehicle, be it a joystick or a gamepad, a driving wheel or a keyboard. The following *NodeDummy* hierarchy is recommended to implement user input handling:


![](input_component.png)


The **car_input_manager** component implements vehicle control and enables simultaneous handling of input events from several input devices. It contains an array of nodes (*NodeDummy*), each having the corresponding input component (*car_keyboard_input, car_joystick_input*, or *car_gamepad_input*) assigned. Each component implements input handling for the corresponding device.


> **Notice:** After configuring inputs don't forget to link the **input_manager** *Node Dummy* to the **Input** field of the **car** component assigned to the vehicle's body at **[previous step](#components_car)**.


Input events can be generated by either of the following:


- **Button**
- **Axis** - can be either a physical axis of the controller, or it can be imitated with buttons


So here we simply configure necessary buttons and axes. Several options are available for an axis:


- **Full** - full axis range: [-1, 1]
- **Positive range** - only the positive range of axis values is taken: [0, 1]
- **Negative range** - only the negative range of axis values is taken: [-1, 0]
- **Full to positive** - converts values in the full [-1, 1] range to values in the positive [0, 1] range
- **Full to negative** - converts values in the full [-1, 1] range to values in the negative [-1, 0] range


The *NONE* value for a button indicates that it's not used.


> **Notice:** Input bindings for gears and driving axles are to be specified in the front-to-rear order.


![](joystick_input.png)


## Debug Configuration (Optional)


Convincing simulation of any vehicle requires fine-tuning. To simplify the process of adjusting parameters, a set of debug windows displaying various vehicle parameters (engine, transmission, wheels, etc.) is at your disposal.


![](debug_info.png)


In order to enable the debug option, you should create the following hierarchy of *[Node Dummy](../../../objects/nodes/dummy/index.md)* (they're just used to enable component logic) and assign the corresponding components to them as shown below:


![](debug_hierarchy.png)


## Switching Views (Optional)


You can switch between the driver's view and other custom views (e.g. external cameras, etc.). Suppose you have various cameras (players) added to the scene and placed at desired locations. To enable switching between them, simply add a *[Node Dummy](../../../objects/nodes/dummy/index.md)* to the scene and assign the **camera_switcher** component to it. Then, in the **Input** field, specify the node responsible for input handling, that we added at **[Step 6](#user_input)**. And, finally, specify the number of cameras you want to use, and drag the corresponding *Player* nodes to the fields of the **Cameras** parameter. All available cameras will be switched in a looped sequence according to the order they are listed.


![](camera_switcher.png)


## Road Surface Conditions Simulation


Driving simulation would be incomplete without the ability to set various surface conditions, such as dry, wet, snow-covered, or icy road, mud, etc. You can simulate various surface conditions by setting up friction coefficients and specifying masks to define areas of the *[Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md)* for them.


To enable simulation of surface conditions add a *[Node Dummy](../../../objects/nodes/dummy/index.md)* to the scene and assign the **friction_controller** component to it. Then specify [masks of *Landscape Terrain*](../../../objects/objects/terrain/landscape_terrain/index.md#layers_masks) defining the areas to which the values of longitudinal (forward) and lateral friction will be applied.


![](friction_controller.png)


Now you can mark areas with different surface conditions on your terrain and fine-tune your vehicle using the [debug windows](#debug_windows) to make your driving simulation as close to real conditions as possible.
