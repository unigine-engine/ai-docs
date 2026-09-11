# ROS Vehicle


![](../../samples/img/ros_vehicle_demo.jpg)


There are multiple types of robots from vacuum cleaners to autonomous combine harvesters, drones etc. Most of them are made of actuators (things that move), sensors (things that read the world), and control systems (robot's brain) There is a way to simplify the complex process of making these components work together - Robot Operating System (ROS), which is a set of free and open-source software libraries and tools that help you build robot applications. ROS enables you to quickly build components and easily connect them via messages. These messages can be sent to various visualization or teleoperation tools so you can work with a simulated robot (digital twin) instead of the real thing. Thus, with ROS you can build complex distributed systems with multiple nodes for different tasks (controls, image generation, etc.), it supports hardware interfaces for many common robot components like motor controllers, LiDARS, and cameras. The whole framework enables you to focus on implementing your logic, not reinventing the wheel. The list of tasks that can be effectively solved using ROS includes logging and diagnostics, fleet management, deep learning data collection (training), testing & quality assurance, and a lot more.


This demo showcases integration of the Robot Operating System (*ROS 2*) with a UNIGINE project to help build robot applications. The demo implements simulation of the automotive vehicle control via ROS and simulation of [sensors](#sensors) (cameras and LiDARs) mounted on the car. In the application, you can control two vehicles available in the demo scene. The data from cameras and LiDARs can be sent via ROS to any other listening app.


> **Notice:** - This demo is based on ***[ROS2 Jazzy](https://docs.ros.org/en/jazzy/index.html)***. However, you can re-build it with any other ROS version (keep in mind that in this case [system requirements](#system_requirements) may differ).
> - The ROS Vehicle project can't be built in Visual Studio or CMake. Use [this instruction](https://docs.ros.org/en/jazzy/Tutorials/Beginner-Client-Libraries/Colcon-Tutorial.html) (or another applicable instruction if you use a different ROS version) to build the project.


## Features


This demo requires at least two modules (ROS nodes) to be run simultaneously:


- **ROS Vehicle** (Simulator) � renders the simulation and sensor data that can be sent via ROS to any other listening app and simulates physics (UNIGINE can also be used as Image Generator with physics and vehicle model calculated on separate nodes). Use *WASD* controls + mouse to move the overall view camera. To control the vehicles, use Teleop applications, the Simulator shall receive user input and move vehicles accordingly.
- **ROS Control** (Teleop) � processes the input (control keys pressed) from the user and transmits it to other ROS nodes. To control two vehicles simultaneously, you can run two Teleop applications on the same PC or on different PCs in the local network. Another control application (e.g. your own implementation of control system of an autonomous vehicle) can be used instead of Teleop to control vehicles in the Simulator.


The Simulator application sends data from cameras and sensors to *RViz 3D* visualization tool for ROS (included in the original ROS2 package) that renders point cloud visualization based on the sensor data received.


To launch *RViz 3D* application use the corresponding script from the project folder depending on your OS: `run_rviz2_linux.sh / run_rviz2_windows.bat`.


### Sensors and camera modes


The following sensors and camera modes are available in **ROS Vehicle Demo**:


| **ROSSensorAirPressure** | Measures atmospheric pressure. |
|---|---|
| **ROSSensorAirspeed** | Measures airspeed relative to the sensor. |
| **ROSSensorAltimeter** | Measures altitude relative to a reference point. |
| **ROSSensorIMU** | Measures linear acceleration and angular velocity. |
| **ROSSensorLiDAR** | Produces LiDAR point cloud data. |
| **ROSSensorNavSat** | Measures global position using GPS-like data. |
| **ROSSensorCamera** | Captures standard RGB images. |
| **ROSSensorBBCamera** | Captures images with bounding box annotations. |
| **ROSSensorDepthCamera** | Captures depth information. |
| **ROSSensorLogicalCamera** | Detects models within a specified volume. |
| **ROSSensorThermalCamera** | Detects heat signature. |
| **ROSSensorWideAngleCamera** | Captures wide field of view. |


All sensors and cameras are available by default and fully configurable in UnigineEditor. They can be found in the *World Nodes* hierarchy at *car_layer -> pegasus -> sensors*. Each node provides a set of adjustable properties and parameters.


## Workflow


The simplified workflow of implementing a robot system using new ROS integration in UNIGINE is as follows:


1. Design your robot, define all sensors and actuators.
2. Implement your robot's control system.
3. Create a 3D model and implement an entity for your robot in UNIGINE (and other entities if necessary).
4. Connect your control system instead of the *Teleop* node.
5. Connect *RViz 3D* or other visualization tools to process and display the data from robot's sensors.


In this case you just concentrate on your task - development of control system and implementation of a digital twin for your robot, without having to think about data transmission or write other utility code.


## System Requirements


Requirements for ***ROS2 Jazzy*** are the following:


- Operating system:

  - *MS Windows 10 x64*
  - *Ubuntu Linux - Noble Numbat (24.04)*
- *Python 3 (3.8-3.10)* > **Notice:** On Windows, you should add a path to `python.exe` to the **PATH** environment variable after installation.

  - Required packages for Python 3: ```bash python3 -m pip install lark python3 -m pip install numpy python3 -m pip install -U colcon-common-extensions ```


### Additional Requirements for Development


- *Qt 5.12.x*
- *MS Visual Studio 2022* on Windows
- *CMake* on Linux ```bash sudo apt install gcc g++ cmake ```


## MATLAB Integration Sample


The demo provides a MATLAB script that implements a vehicle that drives between two points. This script receives telemetry data from the vehicle, processes it, and then sends control commands to this vehicle.


> **Notice:** MATLAB Integration is currently available for Windows only.


Before running the sample, make sure you have installed:


- *Python 3 (3.8-3.10)*. You also need to add a path to `python.exe` to the **PATH** environment variable.
- *MATLAB with [ROS Toolbox](https://www.mathworks.com/help/ros/)*. This option is available during the installation process.


To run the sample on Windows, perform the following:


1. Launch the demo and open the **ROS Vehicle** sample.
2. Run the `matlab_ros_sample.m` MATLAB script and wait for the build to complete. > **Notice:** You might receive a request to delete the `C:/Users/user/source` folder.


The vehicle will then start driving on the lake between two points hardcoded in the MATLAB script.


**SDK Path:***<SAMPLES_PROJECT_PATH>/demos\ros_demo_2.21*
## Accessing Demo Source Code

You can study and modify the source code of this demo to create your own projects. To access the source code do the following:

1. Find the **ROS Vehicle** demo in the *Demos* section and click **[Install](/sdk/#samples)** (if you haven't installed it yet).
2. After successful installation the demo will appear in the *Installed* section, and you can click **Copy as Project** to create a project based on this demo. ![](../../sdk/demos/copy_as_project_gen.png)
3. In the **Create New Project** window, that opens, enter the name for your new project in the corresponding field and click **Create New Project**. ![](../../sdk/projects/create_project_cpp.png)
4. Now you can click **Open Code IDE** to check and modify source code in your default IDE, or click **Open Editor** to open the project in the [UnigineEditor](/editor2/). ![](../../sdk/projects/edit_code.png)
