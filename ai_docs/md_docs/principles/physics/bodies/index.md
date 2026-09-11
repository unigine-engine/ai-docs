# Physical Bodies


**Bodies** can be considered physical approximations of objects. They describe the object's behavior and represent a set of its physical parameters, such as mass, velocity, etc. It is the body that enables interaction of an object with other objects and external physical forces. Each type of body is used for simulation of a specific type of object:


- [Rigid body](../../../principles/physics/bodies/rigid/index.md) (also requires a [shape](../../../principles/physics/shapes/index.md) to be assigned) � enables simulation of objects in accordance with the [rigid body dynamics](#rigid_bodies_dynamics).
- [Ragdoll body](../../../principles/physics/bodies/ragdoll/index.md) (also requires a [shape](../../../principles/physics/shapes/index.md) to be assigned for each bone) � provides [bone-animated](../../../objects/objects/mesh_skinned_legacy/index.md) characters with procedural animation of a death sequence.
- [Fracture body](../../../principles/physics/bodies/fracture/index.md) � enables real-time simulation of destructible objects.
- [Rope body](../../../principles/physics/bodies/rope/index.md) � enables physical simulation of various types of ropes and wires.
- [Cloth body](../../../principles/physics/bodies/cloth/index.md) � enables physical simulation of various types of cloth.
- [Water body](../../../principles/physics/bodies/water/index.md) � enables physical simulation of liquids of different density and viscous behavior including buoyancy effect and wave dynamics.


There are also two types of **auxiliary bodies**:


- [Dummy body](../../../principles/physics/bodies/dummy/index.md) � a static type of body without physical properties. It is used to attach other bodies via [joints](../../../principles/physics/joints/index.md).
- [Path body](../../../principles/physics/bodies/path/index.md) � a static type of body without physical properties. It is a spline, along which an arbitrary rigid body can be moved.


For quick visualization of all types of bodies, watch a fragment of our [video tutorial on physics](https://youtu.be/w_GJrE-6HtI?t=209s).


## Rigid Body Dynamics


Most physics simulations are based on **rigid body dynamics**. A rigid body is an ideal representation of a solid body, which occupies a finite volume of space. This volume of space is determined by a [shape](../../../principles/physics/shapes/index.md) or a set of shapes assigned to the body. Rigid bodies cannot be deformed, i.e. their geometry does not change no matter what happens with this body. Rigid body dynamics is applied to the following bodies with shapes assigned:


- [Rigid body](../../../principles/physics/bodies/rigid/index.md)
- [Ragdoll body](../../../principles/physics/bodies/ragdoll/index.md)
- [Fracture body](../../../principles/physics/bodies/fracture/index.md)


After being **enabled**, all these bodies and their shapes that approximate the object's volume share common properties of rigid objects obeying Newtonian mechanics.


[![Run Lola Run](rigid_body_dynamics_sm.jpg)](rigid_body_dynamics.jpg)

*Ragdolls and rigid bodies moving according to the rigid body dynamics*


Watch a fragment of our [video tutorial on physics](https://youtu.be/w_GJrE-6HtI?t=252s) for illustration of this article.


### Basic Concepts


A state of a rigid body at any moment is specified with its *position*, *orientation* in space (with respect to some reference point � [center of mass](#mass)), and *velocity*. There are two types of body motion and, therefore, two velocity components:


- **Linear motion**. If we imagine that the orientation of the body is fixed, then the only movement the body can undergo is translation motion � change in linear position. This change is performed with **linear velocity**.
- **Angular motion**. On the other hand, if we freeze the center of mass of our body in space, the only movement the body will be able to perform is rotation, which is described by **angular velocity.**


> **Notice:** Setting the body's linear or angular velocity will immediately make it move or rotate in a specified direction.


As the body moves, its linear and angular momenta change. The **linear momentum** can be thought of as an extent to which the body will continue to move along a straight path. It is the product of [mass](#mass) and linear velocity of the body:


***p** = **m** * **v***


The body will keep on moving forever, unless affected by an external force or impulse. **Force** equals mass of the body multiplied by acceleration:


***F** = **m** * **a***


By causing the body to undergo acceleration (i.e., to change its velocity over time), force controls its velocity and position indirectly.


> **Notice:** Forces acting on a body do not affect it immediately � they are accumulated before each [physics simulation frame](../../../code/fundamentals/execution_sequence/index.md#framerates), and during simulation the resulting force, if unbalanced, is applied. Then forces are reset to zero to be calculated anew for the next frame. The same is true for torques.


**Impulse** is the integral of force over time. It may be regarded as a change in momentum of an object to which a resultant force is applied. For example, when two bodies collide, they exchange impulses that are equal and opposite, as Newton's third law applies, and result in moving apart.


Similarly to the linear momentum, the **angular momentum** is the measure of the "quantity of rotation motion" and can be thought of as an extent to which the body will continue to rotate around an axis of symmetry. It is expressed as the product of the [**inertia tensor**](../../../principles/physics/bodies/rigid/index.md#parameter_inertia) of the body and its angular velocity.


Rotation continues until **torque**, a rotational force, is exerted on this body. Torque is the cross product of the radius vector (a vector from the center of mass to the point where torque is applied) and the force vector (the magnitude of the force). Loosely speaking, it acts like a lever affecting rotational speed.


Forces and impulses can also be applied to an arbitrary point of the body and may cause body rotation, when this point is not the center of mass. In this case, force is computed as a cross product of force vector and radius vector (from the center of mass to the necessary point) and is added to the torque. And the other way around, torque applied not to the center of mass increases force.


> **Notice:** Unlike forces and torques, impulses immediately change body velocity as the physics is updated.


To sum it up, the movement is characterized by the following basic parameters:


| Linear Motion | Angular Motion |
|---|---|
| Mass (*scalar*) | Inertia tensor (*mat3*) |
| Linear velocity (*vec3*) | Angular velocity (*vec3*) |
| Force(*vec3*) Impulse ( *vec3*) | Torque (*vec3*) |


Adjustable body parameters that determine its behavior in the framework of rigid body dynamics are as follows:


### Mass


**Mass** of the object multiplied by [gravity](../../../editor2/settings/physics_global/index.md#gravity) specified for the world defines its weight:

 **W** = **m** * **g**
The **center of mass** is automatically calculated as the mean location of mass of all shapes that approximate the object. It serves as a reference point for linear motion and rotation, as well as application of external force and torque.


Mass parameters of the body can be set up manually or determined automatically using the [shape-based](../../../principles/physics/bodies/rigid/index.md#parameter_shapebased) parameters. It is convenient when a body has several [shapes](../../../principles/physics/shapes/index.md).


### Density


**Density** of the objects is defined as its mass per unit volume:

 **ρ** = **m** / **V**
Density value evidently depends on the mass value and vice versa � the higher the values are, the heavier and more dense the object is.


[![Boxes of different mass and density](mass_sm.jpg)](mass.jpg)

*Buoyant boxes of different mass and density*


Density determines buoyancy of the body in accordance with Archimedes' principle. The higher the density, the less tendency a body has to float.


### Linear Damping and Angular Damping


When the object begins moving in a definite direction, the **linear damping** force slows it down to a complete stop. Similar to linear damping, **angular damping** reduces angular velocity of objects over time, so that their rotation ceases. To the linear damping of the body, the global [Linear Damp](../../../editor2/settings/physics_global/index.md#linear_damp) is added, and the exponential function is calculated. In exactly the same way to angular damping of the body, the global [Angular Damp](../../../editor2/settings/physics_global/index.md#angular_damp) is added.


These two parameters ensure that objects smoothly come to a stop and no calculations are done for unnecessary motion.


### Maximum Linear Velocity and Maximum Angular Velocity


**Maximum linear and angular velocity** define the maximum possible velocities of the body. Velocities that exceed this limit are clipped. For example, the maximum linear velocity parameter can help to avoid tunneling (penetration) effect.


> **Notice:** There are also **global** maximum [linear](../../../editor2/settings/physics_global/index.md#max_linear) and [angular](../../../editor2/settings/physics_global/index.md#max_angular) velocities thresholds. The global maximum is compared with the maximum set for the body, and the *minimum* value is chosen to clip the actual velocity.


### Friction


Coefficient of **friction** allows to model more rough rubbing of surfaces and is opposite to the body's movement direction. The **higher** the value, the less tendency the body has to slide. The friction values of both surfaces being in contact are considered.


The resulting calculated friction depends on the objects' [masses](#mass) and [gravity](../../../editor2/settings/physics_global/index.md#gravity), and the angle between contacting surfaces. For example, if a body slides down an inclined plane, the friction becomes lower because the force of gravity, which is perpendicular to the face of the surface, diminishes.


Friction is calculated at contact between physical bodies.


> **Notice:** If the [**Collision**](../../../editor2/node_parameters/physics/index.md#collision_enabled) option is enabled for a surface, it also contributes to calculations.


### Restitution


Coefficient of **restitution** determines the degree of relative kinetic energy retained after a collision. It defines how bouncy the object is by contacting with another object. It depends on the elasticity of materials of colliding bodies. The simulated restitution, like friction, considers the total value for both objects being in contact.


- The maximum value of **1** models *elastic* collision. Objects bounce off according to the impulse they get by contact.
- The minimum value of **0** models *inelastic* collision. Objects do not bounce at all.


Again, just like friction, restitution is calculated by the contact between physical bodies.


> **Notice:** If the **[Collision](../../../editor2/node_parameters/physics/index.md#collision_enabled)** option is enabled for a surface, it also contributes to calculations.


## Freezing


When a body does not move and stays in the equilibrium for some time, it will most probably be immobile until an external force is exerted on it and urges it to move again. During this period of inactivity, there is actually no need to simulate it. This state is called **freezing** and it allows saving a great deal of computational resources.


> **Notice:** Freezing can be applied only to the following bodies:
>
>
> - [Rigid body](../../../principles/physics/bodies/rigid/index.md)
> - [Ragdoll body](../../../principles/physics/bodies/ragdoll/index.md)
> - [Fracture body](../../../principles/physics/bodies/fracture/index.md)


| ![Frozen boxes](freezing0.jpg) � � | ![Simulation starts again as the impulse unfreezes boxes](freezing1.jpg) |
|---|---|
| *Frozen blue and unfrozen red boxes. The impulse applied to the pyramid of boxes unfroze all but one* |  |


The body is frozen, i.e. stops to be simulated, if:


1. Its linear velocity is lower than **Frozen linear velocity** and its angular velocity is lower than **Frozen angular velocity**. Both velocity values must be lower at the same time, otherwise, the simulation will not stop. There are also *[Frozen linear velocity](../../../editor2/settings/physics_global/index.md#frozen_linear)* and *[Frozen angular velocity](../../../editor2/settings/physics_global/index.md#frozen_angular)* thresholds set for the whole world. These global freezing thresholds are compared to the ones set for each body, and the *highest* value is chosen to freeze the body.
2. Velocity values stay lower than frozen velocities for the number of *[Frozen frames](../../../editor2/settings/physics_global/index.md#frozen_frames)*. This is done to ensure that the body has really terminated its motion.


When the body is frozen, its linear and angular velocity are set to **0**. The simulation of the body movement starts again as another non-frozen object touches it or some force is applied to it.


## Setting Body Parameters


The parameters of each body are determined by its type. To view or adjust these parameters via [UnigineEditor](../../../editor2/index.md):


1. Select a node in the *[Editor Viewport](../../../editor2/select_position_nodes/index.md#select_nodes)* or in the *[World Nodes](../../../editor2/interface/index.md#world_hierarchy)* hierarchy window.
2. Go to the ***Physics*** tab in the *[Parameters](../../../editor2/interface/index.md#parameters)* window.
3. Specify available body parameters.
