# Water Body


**Water body** enables physical simulation of liquids of different [density](#density) and [viscous behavior](#liquidity). It also models the appropriate buoyant force on submerged objects and wave dynamics as [two-way interaction](#objects) is calculated. Water simulation is visually pleasant and fast enough, so it can be used within a game environment; however, if the mesh is big and dense, it can become quite costly.


*Water body* can be assigned to the following types of objects:


- *[Water Mesh](../../../../objects/objects/water/water_mesh.md)* object
- *[Dynamic Mesh](../../../../objects/objects/mesh_dynamic/index.md)* object


> **Notice:** In case of an arbitrary mesh, water will not have appropriate shading, but all physical properties will still be present.


### See also


- The article on *[Water Mesh](../../../../objects/objects/water/water_mesh.md)*
- *[BodyWater](../../../../api/library/physics/class.bodywater_cpp.md)* class
- Fragment of the video tutorial on physics demonstrating the [use of the *Water body* for simulation of various types of liquids](https://youtu.be/w_GJrE-6HtI?t=956s)


## Mesh Requirements


A mesh, to which a *Water body* is assigned, should meet the requirements given [here](../../../../objects/objects/water/water_mesh.md#mesh_requirements). Mesh requirements are the same for both *[Dynamic Mesh](../../../../objects/objects/mesh_dynamic/index.md)* and *[Water Mesh](../../../../objects/objects/water/water_mesh.md)* objects.


## Grid Simulation Model


The *Water body* is modeled as a two-dimensional grid with point particles positioned in the vertices of the mesh. The particle movement is restricted to two directions: it can be lifted upwards or dragged downwards. In the case of changing its position, the particle acquires a velocity that affects the neighboring particles and thus describes the grid of *Water body* at each physics [time step](../../../../editor2/settings/physics_global/index.md#fps). Thus, the waves are generated when physical bodies get in contact with water or a particle is directly assigned new velocity.


![](waves_simulation.jpg)

*Water grid changes during physics simulation*


### Liquidity


**Liquidity** defines the viscosity of water (or any other liquid): it determines how readily it splashes and affects wave formation. It multiplies the speed with which water particles pass velocity vectors to the neighboring ones.


- The **higher** the value, the more viscous the water is and the smaller are the waves risen by the objects (e.g. syrup).
- **Low** values provide higher surface waves (e.g. tap water). > **Notice:** Be careful not to set too high or too low values, because that may lead to unstable simulation and blowing up of the water. To regain stability, try to tweak *[Interaction](#interaction)*.


### Density


**Density** of water determines the buoyancy of objects according to Archimedes' principle. Based on the volume of the submerged part of the [shape](../../../../principles/physics/shapes/index.md) and its mass, buoyancy force is applied to its [center of mass](../../../../principles/physics/bodies/index.md#mass) and pushes the object upwards, whereto the mean normal of the grid covered by submerged shape points.


- By the minimum value of 0, the objects will not float in the water, but rather fall through it without any resistance.
- **Higher** values increase the buoyant force. If set too high, the immersed objects start to be pushed out in the air.


## Physical Behavior of Objects in Water


Two-way dynamic interaction provides both physically and visually convincing simulation of the waves from the physical bodies as they disturb the fluid. Imagine a moving boat that forms a wake wave behind it, or a character creating ripples while moving in the water (see the picture [above](#model)).


### Interaction with Objects


A physical object submerged into the water (or any other liquid) has its own velocity vector. On the other hand, all the water particles that are covered by this physical body or surround it, have their own integrated velocity vector, which approximates the state of water. The **Interaction** value is a coefficient that determines how much the object's velocity influences the velocities of water particles and thus generate waves.


- By the minimum value of 0, an object produces no disturbances on the water surface.
- **Higher** values make the disturbances of water surface more intense and the waves from moving objects become higher. > **Notice:** Too high values may blow the water up, as the law of conservation of energy does not constrain the system! Try decreasing [damping](#damping) values to regain stability.


### Linear Damping and Angular Damping


Objects getting into the water are expected to slow down, as resistance of the water is higher than the drag in the air. Damping values work the other way around compared to the *Interaction* coefficient:


**Linear Damping** defines how much linear velocity of the submerged object is decreased over time when influenced by velocities of surrounding water particles. And similarly, **Angular Damping** defines the gradual decrease in the object's rotation. Both linear and angular damping forces are accumulated before being applied.


- By the minimum value of 0, objects movement is not hindered by the water. As a result, there are no waves in the water.
- **Higher** values make the damping of linear or angular velocities more intense, and objects slow down faster as they get into the water. The waves from the objects in this case become more pronounced, as the energy of the system increases. > **Notice:** The water may blow up in case the values are be very high. Try decreasing the *[Interaction](#interaction)* value to regain stability.


### Emission of Particles


It is possible to create an additional visual effect of small droplets, splashes or bubbles on the water when objects fall into it. To enable this effect perform the following steps:


1. Create a *Particle system* effect by clicking *Create -> Effect -> **Particle system*** in the main menu of [UnigineEditor](../../../../editor2/index.md).
2. Go to the *[Parameters](../../../../editor2/interface/index.md#parameters)* window.
3. In the *Dynamic* section, choose the [Spark Emitter](../../../../objects/effects/particles/index.md#spark_emitter) to spawn particles by selecting *Emitter -> **Spark***.
4. Make *Particle system* a **[child](../../../../editor2/organizing_nodes/index.md#reparent_node)** of the *Water Mesh* object.


Particles will be generated only when the object first contacts the water surface, while already submerged bodies will float without generating them.


![](water_splash.jpg)

*Effect of water splashes*


## Water Boundaries


The following parameters relating to **water boundaries** make it possible to create different types of basins in the game environment. These parameters provide flexibility in setting up physical behavior of water for big natural lakes and small pools.


### Depth


**Depth** determines the size of waves: high waves are formed in deep waters (e.g. a sea), while only a slight ripple is generated in shallow waters (e.g. a pool):


- With the minimum value of 0, the objects raise no waves in the water.
- **Higher** values result in higher waves generated by moving objects.


### Intersection with the Ground


**Intersection** of water with the underlying terrain can be necessary, for example, to estimate the actual [depth](#depth) of the water basin.  To enable ground intersection perform the following steps:


1. Make *[Water Mesh](../../../../objects/objects/water/water_mesh.md)* or *[Dynamic Mesh](../../../../objects/objects/mesh_dynamic/index.md)* object a *child* node of the *[Terrain](../../../../objects/objects/terrain/index.md)* or *[Static Mesh](../../../../objects/objects/mesh/index.md)*
2. Check the *Intersection* box in the *[Parameters](../../../../editor2/interface/index.md#parameters)* window -> *Physics* tab -> *Body* section.


Intersection is implemented in the following way: the rays are traced downwards from the water mesh surface, as far as the *[Depth](#depth)* distance. If a ray intersects the parent node, the obtained depth is used in calculations; otherwise the [preset depth value](#depth) is used.


Intersection is also traced upward to check if the water is under terrain and there is no need to render it.


### Absorption


**Absorption** is an option that creates either an effect of a limited basin or, on the contrary, of an open water surface that does not have marked boundaries.


- If *Absorption* is **enabled**, the waves are dispersed along the mesh perimeter. In this case the water level at mesh edges will gradually fall down to zero level.
- If **disabled**, the backwash from the wall is simulated: the wave when reaching the brink of the water is reflected and returns in the reversed direction.


![](water_bound.jpg)

*Water bodyabsorption: enabled(left) and disabled(right)*


## Optimizing Simulation


Updating each frame a huge number of objects located far away from the camera that are hardly distinguishable or observed as a mass is a waste of resources.


To improve performance and avoid the excessive load, water simulation can be [updated with a reduced framerate](../../../../principles/world_management/index.md#periodic_update). When the *Water body* is out of the area specified by the **Update Distance Limit** parameter, physical calculations are not performed, though objects preserve their buoyancy.


The set of frame rates given below enables you to specify how often the water simulation should be updated when the object is visible, when only its shadow is visible, or when it is not visible at all.


![](../../../../principles/world_management/periodic_update.png)

*Parameters -> Physicstab ->Periodic Updatesection*


| FPS When Object Is Rendered To Viewport | Update rate value for the case when the object is rendered to viewport. |
|---|---|
| FPS When Only Object Shadows Are Rendered | Update rate value when the object itself is outside the viewing frustum, and only its shadow is rendered to viewport. |
| FPS When Object Is Not Rendered At All | Update rate value when both the object and its shadow are not rendered to the viewport. |
| Update Distance Limit | Distance from the camera up to which the object should be updated. |


> **Notice:** These values are not fixed and can be adjusted by the Engine at any time to ensure best performance.


This feature is enabled with default settings ensuring optimum performance and can be adjusted per-object in the UnigineEditor or via API at run time.


> **Warning:** Be aware that using reduced update frame rate for an object should be carefully considered in your application's logic, as it may lead to various issues with rendering *Skinned Mesh* and *Dynamic Mesh* (flickering due to misalignment of objects inside the *Water body*).


## Assigning a Water Body


To assign a *Water body* to an object via [UnigineEditor](../../../../editor2/index.md) perform the following steps:


1. Open the *[World Hierarchy](../../../../editor2/interface/index.md#world_hierarchy)* window.
2. Select a **[Water Mesh](../../../../objects/objects/water/water_mesh.md)** or a **[Dynamic Mesh](../../../../objects/objects/mesh_dynamic/index.md)** object to assign the *Water body* to. > **Notice:** Make sure that the object's mesh meets [requirements](../../../../objects/objects/water/water_mesh.md#mesh_requirements)!
3. Go to the ***Physics*** tab in the *[Parameters](../../../../editor2/interface/index.md#parameters)* window and assign a physical [body](../../../../principles/physics/bodies/index.md) to the selected object by selecting *Body -> **Water***. ![Adding a body](../add_body.jpg)
4. Set the body name and change other parameters, if necessary.
