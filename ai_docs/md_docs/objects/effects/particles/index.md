# Particle Systems


A particle system is a really versatile technique that allows creating complex moving structures that produce dynamic and "fuzzy" effects. These structures are used for simulation of abstract effects of fire, smoke, explosions, electricity, fountains, rocket trails, flocking, magic, and many many more. All these effects are hard to reproduce using traditional rigid objects: particles are represented not by a set of primitive surface elements, but by point masses forming the volume of particle primitives. Another distinctive feature is that particles are not static � they may change not only their position, but also the form with the time.


[![](fire_sm.png)](fire.png)

*Fire and smoke simulated by using particles systems*


A particle system consists of three main entities:


- Emitter � the source that emits particles according to the values set in the [Emitter](#emitter_parameters) parameters.
- Particles themselves, which are emitted according to the predefined [behavior after emission](#behavior_after_emission).
- Additional [physical effects](#forces) applied to the particles that affect their behavior.


### See also


- The *[particles_base](../../../content/materials/library/particles_base/index.md)* material to adjust the particles appearance
- The *[ObjectParticles](../../../api/library/objects/class.objectparticles_cpp.md)* class to manage particles via API
- A set of samples located in the `Art Samples` suite.


## Creating Particles


To create particles, perform the following steps:


1. On the Menu bar, click *Create -> Particle System -> Particles*. ![](create_part.png)
2. Place the Particles object somewhere in the world.
3. Specify the particles parameters.


## Emitter Parameters


The particles emitter's behaviour is set via the Emitter parameters.


![](emitter_params.png)


| Clear On Enable | Enables re-initialization of the particle system each time it is enabled. When this option is disabled, turning on the particle system restores the state it had before it was turned off. |  |  |  |  |  |  |  |  |  |  |  |  |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Emitter Enabled | Enables the emitter. |  |  |  |  |  |  |  |  |  |  |  |  |
| Emitter Sync | Enables synchronization of the child particle system with the parent one, even if the child particle system has the *[Emitter Enabled](#emitter_enabled)* option disabled. |  |  |  |  |  |  |  |  |  |  |  |  |
| Emitter Shape | The shape of the volume within which the particles are generated: \| ![](point_emitter.gif) \| **Point** � particles are emitted from a single point. \| \|---\|---\| \| ![](sphere_emitter.gif) \| **Sphere** � particles are generated at random positions within a sphere that has a specified *radius*. \| \| ![](cylinder_emitter.gif) \| **Cylinder** � particles are generated at random positions within a cylinder that has a specified *radius* and *height*. \| \| ![](box_emitter.gif) \| **Box** � particles are generated at random positions within a cube that has a specified *width* (X axis), *height* (Y axis), and *depth* (Z axis). \| \| ![](spark_emitter.gif) \| **Spark** � this emitter generates particles in the points of collision of the parent particles. The spark particle system should be made a child node of a particle system that generates initial particles. Spark emitter can be used to simulate cascades of particles. \| \| ![](random_emitter.gif) \| **Random** � particles are generated on the surface of an arbitrary parent mesh. The particle system should be made a child node of a mesh. At rendering time, random vertices of the mesh are chosen to generate particles. \| | ![](point_emitter.gif) | **Point** � particles are emitted from a single point. | ![](sphere_emitter.gif) | **Sphere** � particles are generated at random positions within a sphere that has a specified *radius*. | ![](cylinder_emitter.gif) | **Cylinder** � particles are generated at random positions within a cylinder that has a specified *radius* and *height*. | ![](box_emitter.gif) | **Box** � particles are generated at random positions within a cube that has a specified *width* (X axis), *height* (Y axis), and *depth* (Z axis). | ![](spark_emitter.gif) | **Spark** � this emitter generates particles in the points of collision of the parent particles. The spark particle system should be made a child node of a particle system that generates initial particles. Spark emitter can be used to simulate cascades of particles. | ![](random_emitter.gif) | **Random** � particles are generated on the surface of an arbitrary parent mesh. The particle system should be made a child node of a mesh. At rendering time, random vertices of the mesh are chosen to generate particles. |
| ![](point_emitter.gif) | **Point** � particles are emitted from a single point. |  |  |  |  |  |  |  |  |  |  |  |  |
| ![](sphere_emitter.gif) | **Sphere** � particles are generated at random positions within a sphere that has a specified *radius*. |  |  |  |  |  |  |  |  |  |  |  |  |
| ![](cylinder_emitter.gif) | **Cylinder** � particles are generated at random positions within a cylinder that has a specified *radius* and *height*. |  |  |  |  |  |  |  |  |  |  |  |  |
| ![](box_emitter.gif) | **Box** � particles are generated at random positions within a cube that has a specified *width* (X axis), *height* (Y axis), and *depth* (Z axis). |  |  |  |  |  |  |  |  |  |  |  |  |
| ![](spark_emitter.gif) | **Spark** � this emitter generates particles in the points of collision of the parent particles. The spark particle system should be made a child node of a particle system that generates initial particles. Spark emitter can be used to simulate cascades of particles. |  |  |  |  |  |  |  |  |  |  |  |  |
| ![](random_emitter.gif) | **Random** � particles are generated on the surface of an arbitrary parent mesh. The particle system should be made a child node of a mesh. At rendering time, random vertices of the mesh are chosen to generate particles. |  |  |  |  |  |  |  |  |  |  |  |  |
| Emitter Size | The size of the particles source. The number of fields (whether it is radius or boundary dimensions) depend on the chosen [shape](#emitter_shape). |  |  |  |  |  |  |  |  |  |  |  |  |
| Particles Type | - **Billboard** represent rotating square planes that are camera-oriented. For example, billboard particles can be used to create smoke. - **Flat** particles are perpendicular to the Z axis of their particle system. They are good for simulating some effects on plane surfaces such as water. - **Point** particles are similar to the billboard type. They also always face the camera, but have the fixed screen-aligned orientation. - **Length** particles are billboard particles that can be stretched along the direction of their movement. *[Stretching](#length_stretch)* is an adjustable factor. Sparks and splashes can be effectively simulated using this type of particles. - **Random** particles are square particles randomly oriented in the space. Leaf-fall can be successfully imitated with this type of particles. - **Route** particles can be used to create tracks from moving objects (for example, trail following a ship). They are similar to the previous implementation of flat particles. - **Chain** particles are billboard particles that form a continuous, visually uninterrupted flow. Their length directly depends on the [spawn rate](#spawn_rate) of the emitter. This type of particles is intended to be used with *[Emitter Shift](#shift_emitter)* creating a chain-like trail after it. |  |  |  |  |  |  |  |  |  |  |  |  |
| Sequence Order | The order of rendering for particle systems, especially when creating a complex effects like shots (with muzzle flash, smoke and the shot itself, each rendered with different particle systems). This parameter is very much the same as *[Rendering Order](../../../editor2/materials_settings/index.md#order)* option in the Materials Settings. But it allows setting a rendering sequence inside of the particle system hierarchy, to avoid such situations when the smoke from a distant shot is rendered atop of the fire of the foreground shot. - **0** means a default sorting according to bounding boxes of particle systems. - Particles with the **lowest** Sequence number are rendered first and are covered by the particles with the **highest** Sequence number, which are rendered last and above others. |  |  |  |  |  |  |  |  |  |  |  |  |
| Emitter Shift | Enabling this checkbox makes the emitter generate particles only when the Particle System is moving. |  |  |  |  |  |  |  |  |  |  |  |  |
| Emitter Continuous | Enables continuous particles that follow the shift of the emitter. |  |  |  |  |  |  |  |  |  |  |  |  |
| Texture Atlas | Enabling this feature makes the following: a random image from the [albedo texture](../../../content/materials/library/particles_base/index.md#texture_albedo) is picked up for every particle. > **Notice:** For using this option, [Animation](../../../content/materials/library/particles_base/index.md#anim_texture) of the texture should be disabled. |  |  |  |  |  |  |  |  |  |  |  |  |
| Texture Atlas Size | The size of the texture atlas. |  |  |  |  |  |  |  |  |  |  |  |  |
| Random Flip X | Flipping of random emitted particles horizontally (along the X axis). ![](random_flip_x.png) |  |  |  |  |  |  |  |  |  |  |  |  |
| Random Flip Y | Flipping of random emitted particles vertically (along the Y axis). ![](random_flip_y.png) |  |  |  |  |  |  |  |  |  |  |  |  |
| Warming On Start | Toggles on and off the particle system initialization with the illusion of prior activity. The particle system evolves with time, so after encountering it in the virtual world, the system only starts to be generated, particle by particle, until the whole system gains the intended look. When the character comes out on a glade, we will see a fire gradually burn up. Warm start for the particles enables rendering the full-grown particle system straight away. The technical implementation of warm start is the following: when the particle system is initialized on the encounter, its life is computed starting from the generation of the *first particle* to its disappearance. After that, the particle system is considered evolved and is rendered in this state. The calculations are taken at a fixed frame rate of 25 fps, which is the minimum required for the correct simulation of particle systems (see also information about *[correlation between framerates](../../../code/fundamentals/execution_sequence/index.md#framerates)*). Warm start can be enabled without any detrimental effect for any particles systems, except for huge ones. |  |  |  |  |  |  |  |  |  |  |  |  |
| Max Warming Time (Sec) | Maximum time of the particle system warmup. |  |  |  |  |  |  |  |  |  |  |  |  |
| Spawn Rate | Number of spawn actions per second. The value defines how many times a [certain number of particles](#number_per_spawn) will be spawned in **one second**. For example, the value set to **5** equals to 5 spawn actions per second. **0** results in no particles at all. |  |  |  |  |  |  |  |  |  |  |  |  |
| Number Per Spawn | Number of particles to be spawned simultaneously each time according to the *[Spawn Rate](#spawn_rate)*. |  |  |  |  |  |  |  |  |  |  |  |  |
| Spawn Threshold | Threshold of the number of particles depending on the velocity of the parent particles. This parameter is used to additionally synchronize the number of particles spawned by *[spark](#spark_emitter)* and *[random](#random_emitter)* emitters with the parent particle system. > **Notice:** Threshold for *[random](#random_emitter)* emitter functions only with a particle system as a parent node. - By the value of **0**, the spawn rate of the *spark* emitter is independent of the parent particle system. - The *higher* the threshold value, the higher must be velocity of the parent particles for the sparks to be generated. If it is not high enough, there will be only few particles, if any. |  |  |  |  |  |  |  |  |  |  |  |  |
| Limit Per Spawn | The total maximum number of particles emitted per spawn. This parameter specifies the number of particles that can simultaneously exist in the world. In other words, the number of particles existing in the world cannot exceed the limit value. For example, if the *[Number per Spawn](#number_per_spawn)* value is 10, and the *Limit Per Spawn* value is 5, 5 particles will be emitted. And no particles will be spawned until the previous ones exist. |  |  |  |  |  |  |  |  |  |  |  |  |
| Life Time (Sec) | Duration of the particles existence after emission in seconds. This parameter also has the *[Spread](#spread)* value that creates the variety of the *Life Time* value, in seconds. |  |  |  |  |  |  |  |  |  |  |  |  |
| Delay | This option defines the time to pass between the *parent* system initialization and initialization of the *child* node. If any delay is set, the parent system starts emitting particles, and after the delay, the generation of child particles is activated. If a particle system doesn't have children, the delay defines the time after which the particles are emitted. This parameter also has the *[Spread](#spread)* value that creates the variety of delay of particle initialization, in seconds. |  |  |  |  |  |  |  |  |  |  |  |  |
| Period | Duration of a pause between generation cycles, in seconds. - If the value is set to 0, the particles are spawned constantly, without any pauses. - If infinity (inf) is specified, the particles emitter becomes inactive after one generation cycle. This parameter also has the *[Spread](#spread)* value that creates the variety of the Period value, in seconds. |  |  |  |  |  |  |  |  |  |  |  |  |
| Duration | Duration of generation cycle, within which emission occurs, in seconds. - The *higher* the value, the longer are the periods when particles are generated. - Setting the value to 0 means that particles are simultaneously spawned over an infinitely small time interval (i.e. during one frame). This value can be used when you need to simulate a one-particle gun shot, for example. This parameter also has the *[Spread](#spread)* value that creates the variety of the Duration value, in seconds. |  |  |  |  |  |  |  |  |  |  |  |  |
| Spread (+/-) | Spread option introduces additional modulation of the corresponding parameter. It represents the range of values that can be randomly added to or subtracted from the specified parameter value. |  |  |  |  |  |  |  |  |  |  |  |  |


## Behavior After Emission


This set of parameters defines how the particles behave after they are emitted:


![](behavior_after_emission.png)


### Value Setting Options


Most parameters in this section have multiple options for setting a value:


![](../../../editor2/curve_editor/particles_curves_switch.gif)


- **Const** � the value is precise and unchanged over time.
- **Between Const** � an interval is set, from which a random value is selected for each instance.
- **Curve** � the parameter value changes over time based on the curve defined in [Curve Editor](../../../editor2/curve_editor/index.md). > **Notice:** In case of small values (close to 0), the curves may lose accuracy if the *[Max Value](../../../editor2/curve_editor/index.md#navigation)* value significantly exceeds the actual maximum value of the curve. To avoid this, *Max Value* should be set as close to the actual maximum as possible.
- **Between Curve** � there are two curves set in [Curve Editor](../../../editor2/curve_editor/index.md) that define the limits, and a random value is taken at every moment of time within these limits. The parameter value changes over time based on this randomly generated set of values.


To select a desired value type, use the gear button.


| Depth Sort | Depth sorting is required, if particles use *alpha blending* (except for the *additive* one). If not enabled, then based on the depth buffer data, opaque objects positioned farther can be wrongly rendered in front of transparent particles. With depth sorting, geometry is rendered in the order *from back to front*, which rules out visual artifacts. |  |  |  |  |
|---|---|---|---|---|---|
| Emitter Based | Enabling this option makes particles move along with the emitter. |  |  |  |  |
| Position | Particle position coordinates relative to the emitter along *X*, *Y* and *Z* axes. |  |  |  |  |
| Gravity | Gravity force affecting particles along the *X*, *Y* and *Z* axes. - *Positive* values equal gravity vector directed upwards. - *Negative* values equal gravity vector directed downwards. The rotation of particle system node does not affect the gravity vector. |  |  |  |  |
| Direction | Direction in which all emitted particles move forming a flow, specified along the *X*, *Y* and *Z* axes. |  |  |  |  |
| Velocity | The speed of particles movement in the set [direction](#direction), in units per second. To grant the natural-looking flow, the final velocity of each separate particle can differ, if the range of values is set. |  |  |  |  |
| Linear Damping | The decrease in particles linear [velocity](#velocity) over time. This parameter is used to simulate effect of friction of the medium for particles. |  |  |  |  |
| Angle | Angle of particles orientation in space, in degrees. If the angle value is set to 180 degrees, the particles will be randomly oriented in all directions. > **Notice:** This option is not available for particles of *[point](#point)* and *[length](#length)* types. |  |  |  |  |
| Rotation Speed | Angular velocity of particles, in degrees per second. - *Positive* numbers rotate the particles clockwise. - *Negative* numbers rotate the particles counterclockwise. |  |  |  |  |
| Radius | Radius (half-size) of the particle. |  |  |  |  |
| Increase In Radius | Increment of the size of a particle, in units per second. - *Positive* numbers result in particles increasingly growing after they are spawned. For example, fireworks grow and blossom in the sky. - *Negative* number define the particles gradually lessening. For example, to imitate the smoke dissipating in air. |  |  |  |  |
| Screen Size Mode | Screen size mode to be used for particles. This mode defines whether the [maximum](#screen_max_size) and [minimum](#screen_min_size) sizes of emitted particles should be limited relative to screen size or not (e.g., to avoid cases when snowflakes or raindrops obscure the view if they are too close to the camera or when they become invisible as the distance to the camera increases). Three modes are available: - **None** � minimum and maximum sizes of particles on the screen are not limited. - **Width** � minimum and maximum sizes of particles on the screen are limited relative to screen width. - **Height** � minimum and maximum sizes of particles on the screen are limited relative to screen height. |  |  |  |  |
| Screen Min Size | Minimum screen size to be set for particles limiting the minimum fraction of the screen a single particle can occupy: - 0 (minimum) � the particle has a zero size and therefore is invisible on the screen (occupies no space at all). - 1 (maximum) � the particle occupies the whole screen. |  |  |  |  |
| Screen Max Size | Maximum screen size to be set for particles limiting the maximum fraction of the screen a single particle can occupy: - 0 (minimum) � the particle has a zero size and therefore is invisible on the screen (occupies no space at all). - 1 (maximum) � the particle occupies the whole screen. |  |  |  |  |
| Length Stretch | Stretching of a particle billboard, available for the *[Length Particles](#length)*. With the value of **0**, the length particle is simply a square billboard. Increasing the value stretches particles in the direction of their movement. The result is calculated by multiplying the stretch value by the [particle velocity](#velocity) value. So, the higher the velocity is, the more stretched the particles are in the direction of their movement, while the other side remains of the same width. \| ![](fire_0.gif) \| ![](fire_1.gif) \| \|---\|---\| \| *Sparks Length Stretch = 0* \| *Sparks Length Stretch = 0.3* \| | ![](fire_0.gif) | ![](fire_1.gif) | *Sparks Length Stretch = 0* | *Sparks Length Stretch = 0.3* |
| ![](fire_0.gif) | ![](fire_1.gif) |  |  |  |  |
| *Sparks Length Stretch = 0* | *Sparks Length Stretch = 0.3* |  |  |  |  |
| Length Flattening | Makes the *[Length Particles](#length)* not camera-oriented as usual billboard particles, but more perpendicular to the Z axis. With the value of **0**, the particles are not flattened. With the maximum value of **1**, the particles will be flat (perpendicular to the Z axis) when they are emitted. \| [![](length_flattering_0_sm.png)](length_flattering_0.png) \| [![](length_flattering_1_sm.png)](length_flattering_1.png) \| \|---\|---\| \| *Length Flattening = 0* \| *Length Flattening = 1* \| | [![](length_flattering_0_sm.png)](length_flattering_0.png) | [![](length_flattering_1_sm.png)](length_flattering_1.png) | *Length Flattening = 0* | *Length Flattening = 1* |
| [![](length_flattering_0_sm.png)](length_flattering_0.png) | [![](length_flattering_1_sm.png)](length_flattering_1.png) |  |  |  |  |
| *Length Flattening = 0* | *Length Flattening = 1* |  |  |  |  |


## Interaction


Interaction of the particles is limited to the application of [forces](#forces) and collisions with external objects. There are two methods to detect the collision with external objects: by using the *[Physics Intersection](#intersection)* parameter or the *[Collision](#collision)* parameter.


> **Notice:** Particle-particle collisions are not checked as collision detection is an expensive operation.


![](interaction.png)


| Physical Mask | For a more selective interaction of the particles systems with *physical nodes*, the *[physical](../../../principles/bit_masking/index.md#physical_mask)* bit mask is used. This bit mask is set for both the **particles system** and the **force**. These masks should have at least one bit matching, otherwise there would be no interaction. The other bits of the mask can match masks of other forces, thus providing perfect control over the scene integration. |
|---|---|
| Particles Field Mask | Bit mask for interaction with *Particles Field* nodes (*[Deflectors](../../../objects/effects/particles/field_deflector/index.md)* and *[Spacers](../../../objects/effects/particles/field_spacer/index.md)*). Emitted particles will be affected by a *Particles Field* only if their masks match (one bit at least). |
| Physical Mass | To participate in the scene dynamics, particles should have a certain mass in kilograms. This value defines the intensity of the impact of the *physical node* on the particles flow. > **Notice:** The *Physical Mass* parameter doesn't affect other calculations. - With the mass of **0**, the trajectory of particles is not affected by any external physical forces ([deflectors](#deflector) work regardless of the mass). - The *more* the mass, the heavier the particles are, and the less *physical nodes* can decline their flow, stretch them, or otherwise affect. |
| Restitution | Strength of particles bouncing off an obstacle. This option is very convenient for simulation of some water effects that include splashes. The strength the bouncing effect depends on both the restitution parameter of particles and the value of the *restitution* surface parameter set for the colliding object (*[Properties](../../../editor2/properties_settings/index.md) -> Parameters -> Restitution*), or the *restitution* value of a *[Particles Deflector](../../../objects/effects/particles/field_deflector/index.md)*. - With the minimum value of **0**, the particles does not bounce off. - With the maximum value of **1**, the angle of particles fall equals the angle of their bouncing off. |
| Roughness | Roughness of the surface of an obstacle the particle collides with. It determines whether the particles scatter in different directions or react as a uniformly directed flow. - The minimum value of **0** means the trajectory of all particles after the collision is the same. - The maximum value of **1** means the particles will scatter in different directions and a bit angularly. This angle arising from particle roughness also affects [bouncing](#restitution) behaviour. In contacts of particles with a *[Particles Deflector](../../../objects/effects/particles/field_deflector/index.md)* its *roughness* value is also taken into account. |
| Collision | Enables collision detection with the *whole* shape of a particle. If particles are big enough, this method is more preferable than *[Intersection](#intersection)*, as it provides a higher degree of visual realism: particles react according to the set parameters, when their edge or vertex comes in contact with an object. Collision calculations are more expensive, so big particles systems should use this option carefully. Collisions are detected for matching *[collision](../../../principles/bit_masking/index.md#collision_mask)* bit masks. |
| Physics Intersection | Enables detection of physics intersections with particles. Physics intersections can be used, for example, to detect collisions of spawned particles with physical shapes and bodies or static collider surfaces to ensure proper interaction, or as a quick way to detect collisions for raycast-wheels of a simulated ground vehicle, or to check if a destructible object or a player was hit by a projectile. Physics intersections are detected for matching *[Physics Intersection](../../../principles/bit_masking/index.md#physics_intersection_mask)* bit masks. |
| Destroy In Collision/Intersection | Toggles on and off culling of particles that have already undergone either collision or intersection. |


## Render To Texture


Particles can be rendered into a procedural texture to be used by an *[Orthographic Decal](../../../objects/decals/ortho/index.md)* or a *[Field Height](../../../objects/effects/fields/field_height/index.md)*. This feature can be used, for example, to create ship wake effects or oil splashes.


![](render_to_texture.gif)


The following settings are available:


![](render_to_texture.png)


| Rendering | Enables rendering of particles to a procedural texture. |
|---|---|
| Positioning | Defines positioning mode to be used for child nodes (decal or field) using the procedural texture, to which the particle system is rendered. The following values are available: - **Manual** � position of a child decal/field node can be changed manually - **Auto** � position of a child decal/field node, which uses the procedural texture, is automatically defined by the position of particle system and cannot be changed manually > **Notice:** Takes effect only when *[Procedural Parenting](#procedural_parenting)* is set to **Children**. |
| Parenting | Defines relationship between the particle system and a *[Decal](../../../objects/decals/ortho/index.md) / [Field](../../../objects/effects/fields/field_height/index.md)* node, that uses the procedural texture into which the particle system is rendered: - **Parent** � the decal/field node is a parent of the particle system - **Children** � the decal/field node is a child of the particle system |
| Resolution | Specifies resolution of the procedural texture into which particles are rendered. - *128x128* - *256x256* - *512x512* - *1024x1024* - *2048x2048* - *4096x4096* - *8192x8192* - *Custom* activates additional fields for specifying a custom resolution. |


## Additional Physical Effects


More intricate changes in further movement of the particles may be performed by applying the additional physical effects. They have influence on the particles flow in the desired direction or on the contrary deflect it. The effects can be of three general types:


- [Forces](#point_force)
- [Noises](#noises)
- [Deflectors](#deflector)


There is no limitation to the number of additional physical effects applied to one particle system and they can freely overlap, enabling to constitute complex trajectories easily and fast.


### Forces


You can apply a physical force to particles inside a sphere-shaped volume in order to affect their movement and behavior. For that, simply add a *[Physical Force](../../../objects/effects/physicals/physical_force/index.md)* node, adjust necessary settings and set up *[Physical Masks](../../../principles/bit_masking/index.md#physical_mask)* to selectively enable interaction.


> **Notice:** By default, particles have their masses equal to zero, in order to be affected by *[Physical Force](../../../objects/effects/physicals/physical_force/index.md)* the particles should have a non-zero mass, so don't forget to set the *[Physical Mass](#physical_mass)* parameter.


### Noises


You can apply physical noise adding a distribution flow based on a volumetric noise texture inside a cuboid-shaped volume. For that, simply add a *[Physical Noise](../../../objects/effects/physicals/physical_noise/index.md)* node, adjust necessary settings and set up *[Physical Masks](../../../principles/bit_masking/index.md#physical_mask)* to selectively enable interaction.


> **Notice:** By default, particles have their masses equal to zero, in order to be affected by *[Physical Noise](../../../objects/effects/physicals/physical_noise/index.md)* the particles should have a non-zero mass, so don't forget to set the *[Physical Mass](#physical_mass)* parameter.


### Deflectors


Sometimes it is necessary to put an obstacle for particles to make them change their trajectory by bouncing off or sliding along a certain surface. For this purpose you can use a *[Particles Deflector](../../../objects/effects/particles/field_deflector/index.md)* node, a surface field that has no visual representation, but physically interacts with Particle Systems leaving other objects unaffected. You can control interaction between the particles and deflectors via the *Particles Field* mask: a deflector will interact with particles generated by a Particle System if they both have matching *Particles Field* masks (one bit at least).


For more information on *Particles Deflector* please refer to [this article](../../../objects/effects/particles/field_deflector/index.md).


## Particles Node Hierarchy


To create complex effects, it is necessary that all particles systems are synchronized in time. Setting a particle system as a **parent** node results in the following:


- All particles systems that are **child** nodes are synchronized relative to their parent particle systems. If the children have children of their own, they still are synchronized with the main parent system, which is the highest in the hierarchy.
- When creating a new child particle system, it should be synchronized with the parent one by *disabling* and again *enabling* the **parent** emitter (*Node* tab -> ***Enabled*** box). At this moment, each of the child systems is initialized with its [Emitter parameters](#emitter_parameters) (such as [generation duration](#duration), [period](#period) of generation pause, and [delay](#delay) of initialization).
- Disabling or enabling the **parent emitter** (*Node* tab -> ***Enabled*** box) affects all child particle systems: they synchronously stop or start emitting particles (emitted particles still live out their time).
- Disabling or enabling the **parent node** (*Node* tab -> ***Enabled*** box) also affects all children: all particle systems in the hierarchy are turned off and on � and preserve the *same state* as was at the moment of their disabling.


### Synchronizing Several Particle Systems


To synchronize several particle systems, for example, to create a shot effect (with three particle systems: muzzle flash, smoke and the bullet), you can do the following:


1. Create the parent particle system that will be used as a dummy one, purely for synchronization purposes (you can even disable its surface). Its [Duration](#duration) time interval should cover all duration intervals and delay intervals (if any) of the children particle systems. Other parameters (Spawn Rate, etc.) do not matter. ![](hierarchy.png)
2. Add the child particle systems. They can have any Duration time required (but it should be smaller than the one of the parent). For example, to synchronize all child particle systems at once and spawn only one particle, you can set the following:

  - [Duration](#duration) = 0
  - [Limit Per Spawn](#limit) = 1
  - [Spawn Rate](#spawn_rate) = inf/100000


## Optimizing Simulation


Updating each frame a huge number of objects located far away from the camera that are hardly distinguishable or observed as a mass is a waste of resources.


To improve performance and avoid the excessive load, particle systems simulation can be [updated with a reduced framerate](../../../principles/world_management/index.md#periodic_update). When a particle system is out of the area specified by the **Update Distance Limit**, particles stop to be updated and freeze statically.


The set of frame rates given below enables you to specify how often the particles simulation should be updated when the particle system is visible, when only its shadow is visible, and when it is not visible at all.


![](../../../principles/world_management/periodic_update.png)

*Parameterstab ->Periodic Updatesection*


| FPS When Object Is Rendered To Viewport | Update rate value for the case when the object is rendered to viewport. |
|---|---|
| FPS When Only Object Shadows Are Rendered | Update rate value when the object itself is outside the viewing frustum, and only its shadow is rendered to viewport. |
| FPS When Object Is Not Rendered At All | Update rate value when both the object and its shadow are not rendered to the viewport. |
| Update Distance Limit | Distance from the camera up to which the object should be updated. |


> **Notice:** These values are not fixed and can be adjusted by the Engine at any time to ensure best performance.


This feature is enabled with default settings ensuring optimum performance and can be adjusted per-object in the UnigineEditor or via API at run time.


If your project, for example, contains an invisible particle system (e.g., using the *[Viewport](../../../principles/bit_masking/index.md#viewport)* mask) and some logic attached to its update (e.g. spawning some visible particles on collision with objects) this logic won't work, as the particle system might be updated with a reduced rate or might not be updated at all. To enable updating such objects regardless of their visibility you can set the **Update Distance Limit** and corresponding update rate values for it to infinity.


## Mesh-Based Particles


It is possible to create mesh-based particle systems. For that, *[Mesh Cluster](../../../objects/objects/mesh_cluster/index.md)* should be added as a child node of the particle system (*ObjectParticles*). After that, meshes are automatically spawned by the emitter.


> **Notice:** Change the *[Viewport](../../../principles/bit_masking/index.md#viewport)* mask for particles, if you do not want to spawn them together with meshes.


![](mesh_particles.jpg)

*Mesh Cluster-based particles*
