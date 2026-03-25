# Fracture Body


**Fracture body** enables real-time persuasive destruction of objects. When collision with some body occurs, a destructible object is procedurally [fractured](#fracturing) into pieces, which in turn can also be fractured until the desired level of destruction is achieved. Fracture bodies are quite inexpensive type, and can be broken into a moderately large number of pieces.


![Slice Pieces](fracture_body.png)

*Fracture bodies broken into pieces*


You can configure the fracture body either in the Editor or via code, however the [type of fracturing](#fracturing) and changing the body state to [broken](#broken) is defined **only via code**.


> **Notice:** *Fracture body* can be assigned only to **[Mesh Dynamic](../../../../objects/objects/mesh_dynamic/index.md)** objects and can be used for convex meshes only.


### See also


- *[BodyFracture](../../../../api/library/physics/class.bodyfracture_cpp.md)* class
- Fragment of the video tutorial on physics demonstrating [procedural destruction of fracture bodies](https://youtu.be/w_GJrE-6HtI?t=814s)


## Fracturing


There are three patterns of fracturing:


- [Slicing](#slice)
- [Cracking](#crack)
- [Shattering](#shatter)


These patterns determine fracture paths that are relevant to different mechanical properties of materials (e.g., its toughness and porosity). Fracture patterns are available for choosing on the script level.


### Slicing


**Slicing** is a fracture pattern separating the mesh volume into two pieces by a plane. The plane passes through a specified point of the body. Slicing angle is determined by a specified normal.


![Slice Pieces](slice_pieces_sm.jpg)

*Fracturing body into two slice pieces*


To slice a *Fracture body* use the *[createSlicePieces()](../../../../api/library/physics/class.bodyfracture_cpp.md#createSlicePieces_Vec3_vec3_int)* method.


### Cracking


**Cracking** is a fracture pattern involving formation of radial cracks from the point of collision. All of the crack pieces slightly vary in size to ensure visual realism. Moreover, the mesh can be additionally fractured along concentric rings, simulating spread of the impulse. The thiner and more brittle the material is (e.g., glass), the more rings tend to be formed by fracturing. The specified distance between the rings is also randomly varied to provide convincing result.


![Crack Pieces](crack_pieces_sm.jpg)

*Creating crack pieces with different number of radial cracks and concentric rings*


To crack a *Fracture body* use the *[createCrackPieces()](../../../../api/library/physics/class.bodyfracture_cpp.md#createCrackPieces_Vec3_vec3_int_int_float_int)* method.


### Shattering


**Shattering** is a fracture pattern randomly dividing the mesh volume into the specified number of convex chunks.


![Shatter Pieces](shatter_pieces_sm.jpg)

*Creating different number of shatter pieces*


To shatter a *Fracture body* use the *[createShatterPieces()](../../../../api/library/physics/class.bodyfracture_cpp.md#createShatterPieces_int_int)* method.


## Broken Body


To make the body broken (sliced, cracked, or shattered), the **Broken** flag should be set for it. Unsetting this flag puts the fractured mesh back into unbroken state.


> **Notice:** The *Broken* flag can be controlled [via API](../../../../api/library/physics/class.bodyfracture_cpp.md#setBroken_int_void) only.


The broken body remains represented as one node in the nodes hierarchy. Generated fractured pieces are automatically represented as *Fracture* bodies and they inherit physical parameters of the fractured body (such as [damping](../../../../principles/physics/bodies/index.md#damping) of linear and angular velocities, [friction](../../../../principles/physics/bodies/index.md#friction), [restitution](../../../../principles/physics/bodies/index.md#restitution) and masks).


## Assigning a Fracture Body


To assign a *Fracture body* to an object via [UnigineEditor](../../../../editor2/index.md) perform the following steps:


1. In the *[World Nodes](../../../../editor2/interface/index.md#world_hierarchy)* window, select **[Mesh Dynamic](../../../../objects/objects/mesh_dynamic/index.md)** object to assign a *Fracture body* to.
2. Go to the ***Physics*** tab in the *[Parameters](../../../../editor2/interface/index.md#parameters)* window and assign a physical [body](../../../../principles/physics/bodies/index.md) to the selected object by selecting *Body -> **Fracture***. ![Adding a body](../add_body.jpg)
3. Set body name and change other parameters, if necessary.
4. Define the [fracturing pattern](#fracturing) and set the *[Broken](#broken)* flag via code.


## Parameters


*Fracture body* (as well as all the pieces it fractures into) is, in fact, a *[Rigid body](../../../../principles/physics/bodies/rigid/index.md)* that moves according to [rigid body dynamics](../../../../principles/physics/bodies/index.md#rigid_bodies_dynamics).


After the body was fractured, its mass is distributed among the pieces and they tumble down as rigid bodies would do.


In addition to the [rigid body parameters](../../../../principles/physics/bodies/rigid/index.md#parameters) available in accordance with the [rigid body dynamics](../../../../principles/physics/bodies/index.md#rigid_bodies_dynamics), the following *Fracture* body parameters are available for configuring:


![](body_parameters.jpg)


| Error | Shape approximation error. *Fracture body* is always approximated with a [convex hull](../../../../principles/physics/shapes/index.md#convex), which may contain too much detail for collision geometry. As a rule, it is unnecessary, because a highly detailed shape does not provide noticeable visual difference while significantly affecting performance. **Approximation error** makes it possible to control the number of vertices in the resulting collision shape: - By the value of 0, the shape precisely duplicates the mesh; the whole volume of it is enclosed. - The **higher** the value, the fewer vertices there are in the created shape, but the more details are skipped and the shape may not cover the whole mesh volume. The maximum value is 1. > **Notice:** An autogenerated shape of a *Fracture body* is not displayed in the *Shapes* list on the *Physics* tab of the *[Parameters](../../../../editor2/interface/index.md#parameters)* window. You can not remove it or assign any other shape to a *Fracture body*. |
|---|---|
| Threshold | Volume threshold for fractured pieces. As the body is fractured, especially for several times, small pieces may start to hit the performance. **Volume threshold** determines the minimum volume for fractured pieces and thus controls the level of fracturing. All chunks that are smaller than the specified value, will not be generated. - By the minimum value of 0, all the pieces up to the smallest one created by fracturing are simulated. - By higher values, only pieces big enough are generated. If no pieces have sufficient volume, the body stays unbroken. |
| Material | Set the material to be applied the the fracture surface. When the mesh is [broken](#broken), it is necessary to set the material that will be applied to all newly created fracture surfaces. Those faces of fracture pieces that were external, keep the initial material. |
| Property | Set the property for all fracture surfaces that come into existence when the mesh is [broken](#broken). They define the game behavior and additional physical properties, however, body parameters override them. |
| Density | Density of the body defined as its mass per unit volume. Density determines buoyancy of the body in accordance with Archimedes' principle. The higher the density, the less tendency a body has to float. |
| Friction | Friction coefficient of the body, enables modeling of rough rubbing of surfaces. The higher the value, the less tendency the body has to slide. |
| Restitution | Coefficient of restitution determines the degree of relative kinetic energy retained after a collision. It defines how bouncy the object is when colliding with another object: - **Higher** values result in more elastic collisions. Objects bounce off according to the impulse they get by contact. - **Lower** values result in more inelastic collisions. Objects do not bounce at all. |


## Performance Optimization Tips


Although the *Fracture body* is a relatively inexpensive type, in case of large number of fracture pieces, the impact on performance may become significant. To avoid performance drops the following tips can be used:


- Use [volume threshold](#threshold) parameter to reduce the number of fracture pieces.
- Remove the pieces of a fractured body from the scene.


A code-based example, illustrating how to remove (fade with the time) the fracture pieces from the scene can be found in the *Physics* section of the [UnigineScript samples](../../../../sdk/index.md#samples).
