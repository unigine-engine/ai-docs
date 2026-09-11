# Joints


**Joints** provide constraints removing degrees of freedom from a [body](../../../principles/physics/bodies/index.md) and are used to connect pairs of bodies. Each joint has an anchor point, which is by default placed between the centers of mass of connected bodies. The properties of each connection depend on the selected joint type and its parameters. Joint parameters can be divided into two groups:


- **[Common parameters](#joint_params)** � basic set of parameters shared by all joints.
- **Type-specific parameters** � a set of specific parameters for each joint type.


### See also


Programming implementation:


- [*Joint*](../../../api/library/physics/class.joint_cpp.md) class
- [*JointFixed*](../../../api/library/physics/class.jointfixed_cpp.md) class
- [*JointHinge*](../../../api/library/physics/class.jointhinge_cpp.md) class
- [*JointBall*](../../../api/library/physics/class.jointball_cpp.md) class
- [*JointPrismatic*](../../../api/library/physics/class.jointprismatic_cpp.md) class
- [*JointCylindrical*](../../../api/library/physics/class.jointcylindrical_cpp.md) class
- [*JointWheel*](../../../api/library/physics/class.jointwheel_cpp.md) class
- [*JointSuspension*](../../../api/library/physics/class.jointsuspension_cpp.md) class (**Deprecated**)
- [*JointPath*](../../../api/library/physics/class.jointpath_cpp.md) class
- [*JointParticles*](../../../api/library/physics/class.jointparticles_cpp.md) class


Usage examples:


- [A Simple Mechanism Using Joints](../../../code/usage/simple_mechanism_joints/index_cpp.md)
- [Creating a Car with Wheel Joints](../../../code/usage/car_wheel_joints/index_cpp.md)


Fragment of video tutorial on physics about [joints](https://youtu.be/w_GJrE-6HtI?t=1145s)


## Adding a Joint


Assume you have two objects with physical bodies assigned. Remember that a body must have a shape assigned. To connect them using a joint via [UnigineEditor](../../../editor2/index.md), perform the following steps:


1. Open the *[*World Hierarchy*](../../../editor2/interface/index.md#world_hierarchy)* window.
2. Select the first body to connect.
3. Go to the ***Physics*** tab in the *[*Parameters*](../../../editor2/interface/index.md#parameters)* window.
4. In the ***Joints*** section, click ![](../shapes/add_sign.png) and choose an appropriate type of joint. ![Adding a joint](addjoint.jpg)
5. Select the second body by picking its name in the dialog window and click ***OK***. ![Selecting a body](select_body.jpg)
6. Set joint parameters in the ***Joints*** section.


You can enable visualization of the joint by checking *[Helpers](../../../editor2/using_visual_helpers/index.md)* panel → *Physics* item → ***Joints*** option (*Visualizer* should be enabled).


## Common Joint Parameters


| ![](joint_params.png) |
|---|
| *Common Joint Parameters* |


All joints regardless of their type have a set of common parameters:


| **Type** | Type of the joint. It can be changed after creation, while the name will remain unchanged. |
|---|---|
| **Collision** | A flag indicating if [collision detection](../../../principles/physics/collision/index.md) between the connected bodies is enabled. |
| **Iterations** | Joints, like collisions, are calculated iteratively. This parameter specifies the number of iterations used to solve joints. Note that if this value is too low, the precision of calculations will suffer. |
| **Max Force** | Maximum force that can be exerted on the joint. If this limit is exceeded, the joint breaks. The default value is inf, i.e. the joint is unbreakable. |
| **Max Torque** | Maximum torque that can be exerted on the joint. If this limit is exceeded, the joint breaks. The default value is inf, i.e. the joint is unbreakable. |
| **Linear Restitution** | Linear stiffness of the joint. Defines how fast it compensates for linear coordinate change between two bodies. When bodies are dragged apart, restitution controls the magnitude of force which is applied to both bodies so that their anchor points to become aligned again. - 1 means that the joint is to return bodies in place throughout 1 physics tick. - 0.2 means that the joint is to return bodies in place throughout 5 physics ticks. > **Notice:** The maximum value of 1 can lead to destabilization of physics (as too great forces are applied). |
| **Angular Restitution** | Angular stiffness of the joint. Defines how fast it compensates for change of the angle between two bodies. When bodies are turned relative each other, restitution controls the magnitude of force which is applied to both bodies so that their anchor points to become aligned again. - 1 means that the joint is to return bodies in place throughout 1 physics tick. - 0.2 means that the joint is to return bodies in place throughout 5 physics ticks. > **Notice:** The maximum value of 1 can lead to destabilization of physics (as too great forces are applied). |
| **Linear Softness** | Linear elasticity of the joint. Defines whether linear velocities of the bodies are averaged out when the joint is stretched. - 0 means that the joint is rigid. Velocities of the first and the second body are independent. - 1 means that the joint is elastic (jelly-like). If the first body changes its velocity, velocity of the second body is equalized with it. |
| **Angular Softness** | Angular elasticity of the joint. Defines whether linear velocities of the bodies are averaged out when the joint is twisted. - 0 means that the joint is rigid. Velocities of the first and the second body are independent. - 1 means that the joint is elastic (jelly-like). If the first body changes its velocity, velocity of the second body is equalized with it. |
| **Anchor 0 Node** | Node of the first body connected to the joint. This is the current node and it cannot be changed. |
| **Anchor 0 Position** | Position of the anchor point of the first connected body in the body coordinate space. |
| **Anchor 1 Node** | Node of the second body connected to the joint. It can be changed by dragging the node that is an object having a physical body from the World Nodes hierarchy. |
| **Anchor 1 Position** | Position of the anchor point of the second connected body in the body coordinate space. |
| **Fix 0** | Changes the position of Anchor 0 to match the position of Anchor 1. |
| **Fix 1** | Changes the position of Anchor 1 to match the position of Anchor 0. |
| **Fix 01** | Shifts both anchors to the middle of the line between them. |


To organize the joints, the following options are available:


![](organize_joints.png)


| ![](../shapes/add.png) | Adds a new joint. |
|---|---|
| ![](../shapes/move.png) | A pair of buttons to move the joint up or down in the list. |
| ![](../shapes/delete.png) | Deletes the selected joint(s). |


To disable a joint, uncheck the checkbox:


![](disabled_joint.png)


## Fixed Joint


Fixed joints connect two bodies in a manner that strictly preserves their positions with respect to each other.


| ![Fixed joint](fixed_joint.jpg) |
|---|
| *Fixed Joint* |


In addition to the [common parameters](#joint_params), fixed joints also have the following constraint parameters:


![Fixed Joint Parameters](joint_params_fixed.png)

*Fixed JointParameters*


| **Anchor 0 Rotation** | Orientation of the first body relative to the anchor point. |
|---|---|
| **Anchor 1 Rotation** | Orientation of the second body relative to the anchor point. |


For more information refer to *[JointFixed Class](../../../api/library/physics/class.jointfixed_cpp.md)* description. An example illustrating connection of two bodies using a fixed joint can be found [here](../../../api/library/physics/class.jointfixed_cpp.md#intro).


Watch the illustration of the Fixed joint in our [video tutorial on physics](https://youtu.be/w_GJrE-6HtI?t=1162s).


## Hinge Joint


Hinge joints allow the connected bodies to rotate along the joint's axis at the anchor point. This joint has an angular [motor](#motors) attached.


| ![Hinge joint](hinge_joint1.jpg) | ![Hinge joint](hinge_joint2.jpg) |
|---|---|
| *Hinge Joint* |  |


In addition to the [common parameters](#joint_params), hinge joints also have the following constraint parameters:


| ![](joint_params_hinge.png) |
|---|
| *Hinge JointParameters* |


| **Anchor 0 Axis** | Axis of the first connected body represented by a normalized vector. |
|---|---|
| **Anchor 1 Axis** | Axis of the second connected body represented by a normalized vector. |
| **Damping** | Angular damping coefficient of the hinge joint. |
| **From** | Minimum angle in the range of movement at which the hinge stops. The angle is specified in degrees in the [-180; 180] range. |
| **To** | Maximum angle in the range of movement at which the hinge stops. The angle is specified in degrees in the [-180; 180] range. |
| **Velocity** | Target velocity of the attached angular motor. |
| **Torque** | Maximum torque of the angular motor. 0 detaches the motor. |
| **Angle** | Target angle of the attached angular spring. The spring (if it is enabled) tries to keep the specified angle between the connected bodies. |
| **Spring** | Spring rigidity coefficient, determines how strong the joint resists rotation. If rigidity is set to 0, the spring is disabled. |


For more information refer to *[JointHinge Class](../../../api/library/physics/class.jointhinge_cpp.md)* description. An example illustrating connection of two bodies using a hinge joint can be found [here](../../../api/library/physics/class.jointhinge_cpp.md#intro).


Watch the illustration of the Hinge joint settings in our [video tutorial on physics](https://youtu.be/w_GJrE-6HtI?t=1227s).


## Ball Joint


Ball joints provide a point around which the connected objects can rotate.


| ![Ball joint](ball_joint1.jpg) | ![Ball joint](ball_joint2.jpg) |
|---|---|
| *Ball Joint* |  |


In addition to the [common parameters](#joint_params), ball joints also have the following constraint parameters:


| ![](joint_params_ball.png) |
|---|
| *Ball JointParameters* |


| **Anchor 0 Axis** | Axis of the first connected body represented by a normalized vector. |
|---|---|
| **Anchor 1 Axis** | Axis of the second connected body represented by a normalized vector. |
| **Damping** | Angular damping coefficient of the ball joint. |
| **Angle** | Swing angle limit, specifies how much connected bodies can bend from the joint axis. |
| **From** | Minimum angle in the range of twisting around the joint axis. The angle is specified in degrees in the [-180; 180] range. |
| **To** | Maximum angle in the range of twisting around the joint axis. The angle is specified in degrees in the [-180; 180] range. |


For more information refer to [JointBall Class](../../../api/library/physics/class.jointball_cpp.md) description. An example illustrating connection of two bodies using a ball joint can be found [here](../../../api/library/physics/class.jointball_cpp.md#intro).


Watch the illustration of the Ball joint settings in our [video tutorial on physics](https://youtu.be/w_GJrE-6HtI?t=1254s).


## Prismatic Joint


Prismatic joints allow movement along the joint axis. This joint has a linear [motor](#motors) attached.


| ![Prismatic joint](prismatic_joint1.jpg) | ![Prismatic joint](prismatic_joint2.jpg) |
|---|---|
| *Prismatic Joint* |  |


In addition to the [common parameters](#joint_params), prismatic joints also have the following constraint parameters:


| ![](joint_params_prismatic.png) |
|---|
| *Prismatic JointParameters* |


| **Anchor 0 Axis** | Axis of the first connected body represented by a normalized vector. |
|---|---|
| **Anchor 0 Rotation** | Orientation of the first body relative to the anchor point. |
| **Anchor 1 Rotation** | Orientation of the second body relative to the anchor point. |
| **Damping** | Linear damping coefficient of the prismatic joint. |
| **From** | Minimum distance between the bodies along the joint axis. |
| **To** | Maximum distance between the bodies along the joint axis. |
| **Velocity** | Target velocity of the attached linear motor. |
| **Force** | Maximum force of the attached linear motor. 0 detaches the motor. |
| **Distance** | Target linear distance of the attached spring. The spring (if it is enabled) tries to keep the specified distance between the connected bodies. |
| **Spring** | Spring rigidity coefficient, determines how strong the joint resists linear motion. If rigidity is set to 0, the spring is disabled. |


For more information refer to *[JointPrismatic Class](../../../api/library/physics/class.jointprismatic_cpp.md)* description. An example illustrating connection of two bodies using a prismatic joint can be found [here](../../../api/library/physics/class.jointprismatic_cpp.md#intro).


Watch the illustration of the Prismatic joint in our [video tutorial on physics](https://youtu.be/w_GJrE-6HtI?t=1263s).


## Cylindrical Joint


Cylindrical joints are like prismatic ones with an additional degree of freedom: rotation around the joint axis. This joint has a linear and an angular [motors](#motors) attached.


| ![Cylindrical joint](cylindrical_joint1.jpg) | ![Cylindrical joint](cylindrical_joint2.jpg) |
|---|---|
| *Cylindrical Joint* |  |


In addition to the [common parameters](#joint_params), cylindrical joints also have the following constraint parameters:


| ![](joint_params_cylindrical.png) |
|---|
| *Cylindrical JointParameters* |


| **Anchor 0 Axis** | Axis of the first connected body represented by a normalized vector. |
|---|---|
| **Anchor 1 Axis** | Axis of the second connected body represented by a normalized vector. |
| **Linear Damping** | Linear damping coefficient of the cylindrical joint. |
| **Linear From** | The minimum distance between the bodies along the joint axis. |
| **Linear To** | The maximum distance between the bodies along the joint axis. |
| **Linear Velocity** | Target velocity of the attached linear motor. |
| **Linear Force** | Maximum force of the attached linear motor. 0 detaches the motor. |
| **Linear Distance** | A target linear distance of the attached spring. The spring (if it is enabled) tries to keep the specified distance between the connected bodies. |
| **Linear Spring** | Spring rigidity coefficient, determines how strong the joint resists linear motion. If rigidity is set to 0, the spring is disabled. |
| **Angular Damping** | Angular damping coefficient of the cylindrical joint. |
| **Angular From** | The minimum angle in the range of twisting around the joint axis. The angle is specified in degrees in the [-180; 180] range. |
| **Angular To** | The maximum angle in the range of twisting around the joint axis. The angle is specified in degrees in the [-180; 180] range. |
| **Angular Velocity** | Target velocity of the attached angular motor. |
| **Angular Torque** | Maximum torque of the angular motor. 0 detaches the motor. |
| **Angular Angle** | A target angle of the attached angular spring. The spring (if it is enabled) tries to keep the specified angle between the connected bodies. |
| **Angular Spring** | Spring rigidity coefficient, determines how strong the joint resists rotation. If rigidity is set to 0, the spring is disabled. |


For more information refer to *[JointCylindrical Class](../../../api/library/physics/class.jointcylindrical_cpp.md)* description. An example illustrating connection of two bodies using a cylindrical joint can be found [here](../../../api/library/physics/class.jointcylindrical_cpp.md#intro).


Watch the illustration of the Cylindrical joint in our [video tutorial on physics](https://youtu.be/w_GJrE-6HtI?t=1263s).


## Wheel Joint


Wheel joints are used to create ray-cast vehicle wheels. It connects two [rigid bodies](../../../principles/physics/bodies/rigid/index.md): the first body is a frame, the second one is a wheel. There is no need to assign a shape to the wheel: ray casting is used to detect collision of the wheel with a surface. This joint has an angular [motor](#motors) attached.


> **Notice:** **The order** of the bodies connected using a wheel joint, **matters**!
>
>
> - If the bodies are connected using [UnigineEditor](../../../editor2/index.md):
>
>   1. Select the vehicle frame.
>   2. Add a wheel joint.
>   3. Specify the wheel to be attached.
> - If the bodies are connected via code:
>
>   - **b0** is a frame.
>   - **b1** is a wheel.


| ![Wheel joint](wheel_joint1.jpg) | ![Wheel joint](wheel_joint2.jpg) |
|---|---|
| *Wheel Joint* |  |


In addition to the [common parameters](#joint_params), wheel joints also have the following constraint parameters:


| ![](joint_params_wheel.png) |
|---|
| *Wheel JointParameters* |


| **Anchor 00 Axis** | Coordinates of a vertical axis (suspension axis) that acts like a cylindrical joint providing steering and damping. |
|---|---|
| **Anchor 10 Axis** | Coordinates of a horizontal axis around which the wheel rotates, in the coordinate system of the frame (which is *body 0*). |
| **Anchor 11 Axis** | Coordinates of a horizontal axis around which the wheel rotates, in the coordinate system of the wheel (which is *body 1*). |
| **Linear Damping** | Linear damping coefficient of the suspension. |
| **Linear From** | Lower suspension ride limit. |
| **Linear To** | Upper suspension ride limit. |
| **Linear Distance** | Target suspension height. The suspension spring (if it is enabled) tries to keep the specified height. |
| **Linear Spring** | Suspension spring rigidity coefficient, determines how strong the joint resists vertical linear motion. If rigidity is set to 0, the spring is disabled. |
| **Angular Damping** | Angular damping coefficient of wheel rotation. |
| **Angular Velocity** | Target velocity of the attached angular motor. |
| **Angular Torque** | Maximum torque of the angular motor. 0 detaches the motor. |
| **Tangent Angle** | Coefficient specifying how fast the optimal longitudinal force can be achieved. The larger this value, the more is the impulse produced by the tire. |
| **Tangent Friction** | Longitudinal (forward) friction of the tire. |
| **Binormal Angle** | Coefficient specifying how fast the optimal lateral force can be achieved. The larger this value, the more is the impulse produced by the tire. |
| **Binormal Friction** | Lateral (sideways) friction of the tire. |
| **Wheel Mass** | Mass of the attached wheel. |
| **Wheel Threshold** | Threshold difference between the wheel and ground velocities. When it is too small, the longitudinal force is scaled down to prevent unnatural vibrations. |
| **Wheel Radius** | Radius of the attached wheel. |


For more information refer to *[JointWheel Class](../../../api/library/physics/class.jointwheel_cpp.md)* description. For an example illustrating the use of wheel joints see the [Creating a Car with Wheel Joints](../../../code/usage/car_wheel_joints/index_cpp.md) article.


Watch how to simulate a wheel using the Wheel joint in our [video tutorial on physics](https://youtu.be/w_GJrE-6HtI?t=1282s).


## Suspension Joint


> **Warning:** This joint type is deprecated and will be removed in the upcoming releases. It is recommended to use the [Wheel Joint](#wheel) instead.


Suspension joints are used to create wheel suspension for vehicles. It connects two [rigid bodies](../../../principles/physics/bodies/rigid/index.md): the first body is a frame, the second one is a wheel. This joint has an angular [motor](#motors) attached.


> **Notice:** **The order** of the bodies connected using a suspension joint, **matters**!
>
>
> - If the bodies are connected using [UnigineEditor](../../../editor2/index.md):
>
>   1. Select the vehicle frame.
>   2. Add a suspension joint.
>   3. Specify the wheel to be attached.
> - If the bodies are connected via code:
>
>   - **b0** is a frame.
>   - **b1** is a wheel.


| ![Suspension joint](wheel_joint1.jpg) | ![Suspension joint](wheel_joint2.jpg) |
|---|---|
| *Suspension Joint* |  |


In addition to the [common parameters](#joint_params), suspension joints also have the following constraint parameters:


| ![](joint_params_suspension.png) |
|---|
| *Suspension JointParameters* |


| **Anchor 00 Axis** | Coordinates of a vertical axis (suspension axis) that acts like a cylindrical joint providing steering and damping. |
|---|---|
| **Anchor 10 Axis** | Coordinates of a horizontal axis around which the wheel rotates, in the coordinate system of the frame (which is *body 0*). |
| **Anchor 11 Axis** | Coordinates of a horizontal axis around which the wheel rotates, in the coordinate system of the wheel (which is *body 1*). |
| **Linear Damping** | Linear damping coefficient of the suspension. |
| **Linear From** | Lower suspension ride limit. |
| **Linear To** | Upper suspension ride limit. |
| **Linear Distance** | Target suspension height. The suspension spring (if it is enabled) tries to keep the specified height. |
| **Linear Spring** | Suspension spring rigidity coefficient, determines how strong the joint resists vertical linear motion. If rigidity is set to 0, the spring is disabled. |
| **Angular Damping** | Angular damping coefficient of wheel rotation. |
| **Angular Velocity** | Target velocity of the attached angular motor. |
| **Angular Torque** | Maximum torque of the angular motor. 0 detaches the motor. |


For more information refer to *[JointSuspension Class](../../../api/library/physics/class.jointsuspension_cpp.md)* description. An example illustrating connection of two bodies using a suspension joint can be found [here](../../../api/library/physics/class.jointsuspension_cpp.md#intro).


For the difference between the Suspension and Wheel joints, see our [video tutorial on physics](https://youtu.be/w_GJrE-6HtI?t=1282s).


## Path Joint


Path joint is used to attach a [rigid body](../../../principles/physics/bodies/rigid/index.md) to a [path body](../../../principles/physics/bodies/path/index.md) and to make it move along this path. This joint can be used to make a train move along the tracks. This joint has a linear [motor](#motors) attached.


> **Notice:** Assign a [shape](../../../principles/physics/shapes/index.md) to a rigid body before connecting it to a path body!
> **The order** of the bodies connected using a path joint, **matters**!
>
>
> - If the bodies are connected using [UnigineEditor](../../../editor2/index.md):
>
>   1. Select a rigid body.
>   2. Add a path joint.
>   3. Specify the path body.
> - If the bodies are connected via code:
>
>   - **b0** is a *BodyRigid*.
>   - **b1** is a *BodyPath*.


| ![Path joint](path_joint.gif) |
|---|
| *Path Joint* |


In addition to the [common parameters](#joint_params), path joints also have the following constraint parameters:


| ![](joint_params_path.png) |
|---|
| *Path JointParameters* |


| **Anchor 0 Rotation** | Orientation of the body relative to the path. |
|---|---|
| **Damping** | Linear damping coefficient of the path joint. |
| **Velocity** | Target velocity of the attached linear motor. |
| **Force** | Maximum force of the attached linear motor. 0 detaches the motor. |


For more information refer to *[JointPath Class](../../../api/library/physics/class.jointpath_cpp.md)* description. An example illustrating connection of two bodies using a path joint can be found [here](../../../api/library/physics/class.jointpath_cpp.md#intro).


Our [video tutorial on physics](https://youtu.be/w_GJrE-6HtI?t=1356s) shows how to attach a rigid body to a path body using the Path joint.


## Particles Joint


Particles joint is used to pin [cloth body](../../../principles/physics/bodies/cloth/index.md) or [rope body](../../../api/library/physics/class.bodyrope_cpp.md) to a [rigid body](../../../principles/physics/bodies/rigid/index.md), [ragdoll body](../../../principles/physics/bodies/ragdoll/index.md) or a [dummy body](../../../principles/physics/bodies/dummy/index.md).


> **Notice:** **The order** of the bodies connected using a particles joint, **matters**!
>
>
> - If the bodies are connected using [UnigineEditor](../../../editor2/index.md):
>
>   1. Select a rigid body, a ragdoll body or a dummy body.
>   2. Add a particles joint.
>   3. Specify a cloth body or a rope body.
> - If the bodies are connected via code:
>
>   - **b0** is a *BodyRigid / BodyRagdoll / BodyDummy*.
>   - **b1** is a *BodyCloth / BodyRope*.


| ![Particles joint](particles_joint.gif) |
|---|
| *Particles Joint* |


In addition to the [common parameters](#joint_params), particles joints also have the following constraint parameters:


| ![](joint_params_particles.png) |
|---|
| *Particles JointParameters* |


| **Size** | Size of the area for pinning vertices of cloth or rope body to another body. |
|---|---|
| **Threshold** | Distance for pinning vertices of cloth or rope body to another body. If vertices are closer than the threshold, they are pinned together; otherwise, particles stay loose. |


For more information refer to *[JointParticles Class](../../../api/library/physics/class.jointparticles_cpp.md)* description. An example illustrating attachment of a [cloth body](../../../principles/physics/bodies/cloth/index.md) using a particles joint can be found [here](../../../code/usage/cloth_particle_joint/index_cpp.md).


An example illustrating the use of [rope body](../../../principles/physics/bodies/rope/index.md) and particles joint can be found [here](../../../code/usage/ropes_creating_pylons_and_wires/index_cpp.md).


Our [video tutorial on physics](https://youtu.be/w_GJrE-6HtI?t=1316s) shows how to attach a rope or a cloth to other bodies using the Particles joint.


## Motors and Springs


Joints can have motors and springs associated with them.


**Springs** try to keep the bodies connected with a joint at some specific distance (linear) or angle (angular). The behavior of a particular spring depends on its rigidity and damping coefficient.


**Motors** provide movement or rotation of bodies connected with a joint relative to each other by applying a torque (or force) to a joint's degree of freedom. There are **linear** and **angular** motors that exert a limited force to a joint, pushing or rotating connected objects.


![Springs and Motors](spring_motor.png)


Motors have two parameters:


- **Target velocity**
- **Maximum force** (or torque) that is available to reach that velocity.


This is a very simple model of real life motors. However, is it quite useful when modeling a motor, that is geared down with a gearbox before being connected to the joint. Such devices are often controlled by setting a target velocity, and can only generate a maximum amount of power to achieve that speed (which corresponds to a certain amount of force available at the joint).


To **activate an angular motor** perform the following steps:


1. Set **angular velocity** � target angular velocity of the motor, This value determines how fast the motor can rotate.

  - **positive value** � the motor rotates counterclockwise.
  - **negative value** � the motor rotates clockwise.
2. Set **angular torque** � maximum torque applied by the motor to reach target velocity. This value determines how fast the motor reaches maximum velocity.

  - 0 disables the motor.
  - If a negative value is provided, 0 will be used instead.


To **activate a linear motor** perform the following steps:


1. Set **linear velocity** � target linear velocity of the motor, This value determines how fast the motor can push.

  - **positive value** � the motor pushes forward.
  - **negative value** � the motor pulls backward.
2. Set **linear force** � maximum force applied by the motor to reach target velocity. This value determines how fast the motor reaches maximum velocity.

  - 0 disables the motor.
  - If a negative value is provided, 0 will be used instead.


## Vehicles


Vehicles are important in real-time games, therefore, they are to be described separately. There are two approaches to simulation of moving vehicles. Each approach has a corresponding joint type to connect wheels to vehicle body.


- **The first approach** uses a *[suspension joint](#suspension)* and assumes that wheels are represented as physical bodies with shapes. As each wheel has a collider shape, collisions with objects on the ground are handled correctly. For example, such car runs on a curb smoothly. This approach requires more calculations and is to be used when more accurate simulation is needed especially for step-like ground surface and wheels have a complex shape.
- **The second approach** uses a *[wheel joint](#wheel)* and assumes that the wheels are virtual. Wheels do not collide with the surface of the road. Instead, rays are cast down from the car body to detect surface unevenness. In this case steep changes of the terrain are not handled accurately. This approach is faster then the first one and provides acceptable results for smooth terrain, e.g. for racing cars simulation. However, on cross-country terrains it may not work correctly.


Both joints have a [motor](#motors) associated with them, which rotates the wheels and pushes the vehicle forward.


![Problems with ray cars and steep obstacles](raycar.jpg)


*A problem with the wheels simulated using ray casting*
