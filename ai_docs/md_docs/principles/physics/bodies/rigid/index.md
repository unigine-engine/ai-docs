# Rigid Body


**Rigid body** enables simulation of physical bodies in accordance with [*Rigid body* dynamics](../../../../principles/physics/bodies/index.md#rigid_bodies_dynamics). This type of body is the most commonly used and the most efficient one in terms of performance.


> **Notice:** A *Rigid body* must have at least one collision [shape](../../../../principles/physics/shapes/index.md) assigned.


![Rigid bodies](rigid_bodies_domino_sm.jpg)


### See also


- *[BodyRigid](../../../../api/library/physics/class.bodyrigid_cpp.md)* class


## Assigning a Rigid Body


To assign the *Rigid body* to an object via [UnigineEditor](../../../../editor2/index.md) perform the following steps:


1. In the *[World Nodes](../../../../editor2/interface/index.md#world_hierarchy)* window, select the object that you want to assign a *Rigid* body to.
2. Ensure that the [mobility](../../../../editor2/node_parameters/transformation_common/index.md#clutter) of the node is set to *Dynamic*.
3. Go to the ***Physics*** tab in the *[Parameters](../../../../editor2/interface/index.md#parameters)* window and assign a physical [body](../../../../principles/physics/bodies/index.md) to the selected object by selecting *Body -> **Rigid***. ![Adding a body](../add_body.jpg)
4. Set the body name and change other parameters, if necessary.


## Parameters


The set of *Rigid body* parameters in accordance with [*Rigid body* dynamics](../../../../principles/physics/bodies/index.md#rigid_bodies_dynamics) includes the following:


![](body_parameters.png)


| Immovable | Toggles the static mode for a *Rigid body* on and off. If the flag is set, the body will ignore all forces in the world and keep its position while being a collider object. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Gravity | Toggles the gravity for the body on and off. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Freezable | Enables [freezing physical simulation](../../../../principles/physics/bodies/index.md#freezing) of the body when necessary. > **Notice:** This flag is recommended to be always set for all rigid bodies except for *[Player Actor](../../../../api/library/players/class.playeractor_cpp.md)*. Freezing a player causes it to react to the user's input with a time lag, small but nonetheless perceptible. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Shape-Based | Toggles automatic calculation of certain parameters of a rigid body ([total mass](#parameter_mass), [center of mass](#parameter_cmass), and [inertia tensor](#parameter_inertia)) on the basis of parameters determined for its shapes on and off. Volume of a *Rigid body* can be approximated by several [shapes](../../../../principles/physics/shapes/index.md) (e.g. a concave object divided into a set of convex hulls or a *[Ragdoll body](../../../../principles/physics/bodies/ragdoll/index.md)*). Each shape has its [mass](../../../../principles/physics/shapes/index.md#mass) and [density](../../../../principles/physics/shapes/index.md#density). Therefore certain parameters of a *Rigid body*, such as its total mass, center of mass, and inertia tensor, are determined by its shapes. These parameters can be calculated automatically if the **Shape-based** option is enabled. > **Notice:** Setting the individual masses or densities of the shapes is the most intuitive method to achieve correct physical behavior of the body. Even if overridden by the body parameters, they are still used to determine the distribution of mass within the object. Disabling the **Shape-based** option makes it possible to manually redefine such total parameters for the body as Center of mass and moment of Inertia. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| High Priority Contacts | On collision, contacts are distributed randomly between the interacting bodies to optimize performance: some are handled by the first body, others by the second. For a body, contacts that it handles itself are **internal** (access to them is fast), and contacts handled by other bodies are **external**. This option makes the body handle most of its contacts itself (so that most of them are internal). Thus, you can track collisions of a certain body with maximum efficiency. > **Notice:** You can iterate through all contacts for a body, but for better performance it is recommended to process only internal ones. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Name | Name of the body. This name may become helpful for identification when creating joints, detecting contacts, handling callbacks, etc. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Mass | [Mass of the body](../../../../principles/physics/bodies/index.md#mass), in kilograms. > **Notice:** **Do not use real masses**, this can make physics simulation unstable. Adjust mass values when necessary to achieve realistic behavior (e.g. for a wheel mass of **25** kg it might be better to set **60** kg for a car body instead of 2000 kg). It is very important to ensure mass balance � avoid connection of too heavy bodies to very light ones, otherwise the joints may become unstable! |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Inertia | The **moment of inertia** is a rotational analog of mass, describing the resistance of the body to rotation in different directions. It is determined by the distribution of mass throughout the body volume. The farther from the axis of rotation the center of mass is, the more rotational inertia the body has. The **inertia tensor** that allows to compute a moment of inertia about an arbitrary axis is represented as a matrix, **I**: \| ***Ixx*** �� \| ***Ixy*** �� \| ***Ixz*** �� \| \|---\|---\|---\| \| ***Iyx*** �� \| ***Iyy*** �� \| ***Iyz*** �� \| \| ***Izx*** �� \| ***Izy*** �� \| ***Izz*** �� \| where ***Iij*** sets the moment of inertia around the **i** -axis when the body is rotated around the **j**-axis. > **Notice:** To rotate the body evenly about the rotation axis, the matrix should be diagonal, i.e all values outside the main diagonal are set to 0. Otherwise, the body may start to rotate chaotically. As for values of the moment of inertia: - The **higher** the value, the more torque must be be applied to rotate the body about a particular axis. - The **lower** the value, the easier it is to change the angular velocity of a body about a particular axis. > **Notice:** It is not recommended to set values less than 0.011! Otherwise, the matrix won't be properly inverted, which is necessary to apply collision impulse. Values are corrected with respect to the average value to provide smoother movement. For example, the following illustration shows three boxes with different inertia tensors. The yellow box has very high inertia: \| **100** �� \| ��**0** �� \| ��**0** �� \| \|---\|---\|---\| \| ��**0** �� \| **100** �� \| ��**0** �� \| \| ��**0** �� \| ��**0** �� \| **100** �� \| Because of that, it can only slide down when falling upon the tilted plane. The red box, on the contrary, has the lowest inertia and rotates most eagerly. ![Different Inertia tensors](inertia_sm.jpg) *Different inertia tensors that override shape-based parameters* | ***Ixx*** �� | ***Ixy*** �� | ***Ixz*** �� | ***Iyx*** �� | ***Iyy*** �� | ***Iyz*** �� | ***Izx*** �� | ***Izy*** �� | ***Izz*** �� | **100** �� | ��**0** �� | ��**0** �� | ��**0** �� | **100** �� | ��**0** �� | ��**0** �� | ��**0** �� | **100** �� |
| ***Ixx*** �� | ***Ixy*** �� | ***Ixz*** �� |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| ***Iyx*** �� | ***Iyy*** �� | ***Iyz*** �� |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| ***Izx*** �� | ***Izy*** �� | ***Izz*** �� |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| **100** �� | ��**0** �� | ��**0** �� |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| ��**0** �� | **100** �� | ��**0** �� |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| ��**0** �� | ��**0** �� | **100** �� |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| CMass | An arbitrary point can be set to be a **[center of mass](../../../../principles/physics/bodies/index.md#mass_center)** of the body. It may be necessary to correct the motion of an object to provide desirable look. For example, a tilting doll with a sphere shape requires an uneven mass distribution: its center of mass should be located closer to the bottom, so it always stands up when tilted. > **Notice:** Center of mass is set as coordinates of the point in local space of the body. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| LScale | Multipliers for the body's linear velocity along the axes. Setting any value to 0, restricts movement along the corresponding axis. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| AScale | Multiplier for the body's angular velocity along the X axis. When set to 0, rotation along this axis will be restricted. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| LDamping | [Linear damping](../../../../principles/physics/bodies/index.md#damping) reduces linear velocity of the body over time and slows it down up to a complete stop. Higher values make the body slow down faster. [Global linear damping](../../../../editor2/settings/physics_global/index.md#linear_damp) is added to the linear damping of the body to calculate resulting value. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| ADamping | [Angular damping](../../../../principles/physics/bodies/index.md#damping) reduces angular velocity of the body over time and slows it down until its rotation ceases. Higher values make the body slow down faster. [Global angular damping](../../../../editor2/settings/physics_global/index.md#angular_damp) is added to the angular damping of the body to calculate resulting value. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| MLVelocity | [Maximum linear velocity](../../../../principles/physics/bodies/index.md#maximum_velocity) defines the maximum possible velocity of the body. Values exceeding this limit will be clipped. There is also a [global maximum linear velocity](../../../../editor2/settings/physics_global/index.md#max_linear) threshold, it is compared with the maximum set for the body, and the minimum is chosen for actual velocity clipping. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| MAVelocity | [Maximum angular velocity](../../../../principles/physics/bodies/index.md#maximum_velocity) defines the maximum possible angular velocity of the body. Values exceeding this limit will be clipped. There is also a [global maximum angular velocity](../../../../editor2/settings/physics_global/index.md#max_angular) threshold, it is compared with the maximum set for the body, and the minimum is chosen for actual velocity clipping. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| FLVelocity | [Frozen linear velocity](../../../../principles/physics/bodies/index.md#freezing) defines the value of linear velocity at which the body becomes frozen. Such body is excluded from physical simulation until it remains idle, which significantly reduces simulation load and improves performance. There is also a [global frozen linear velocity](../../../../editor2/settings/physics_global/index.md#frozen_linear), it is compared with the value set for the body, and the maximum is chosen for body freezing. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| FAVelocity | [Frozen angular velocity](../../../../principles/physics/bodies/index.md#freezing) defines the value of angular velocity at which the body becomes frozen. Such body is excluded from physical simulation until it remains idle, which significantly reduces simulation load and improves performance. There is also a [global frozen angular velocity](../../../../editor2/settings/physics_global/index.md#frozen_angular), it is compared with the value set for the body, and the maximum is chosen for body freezing. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
