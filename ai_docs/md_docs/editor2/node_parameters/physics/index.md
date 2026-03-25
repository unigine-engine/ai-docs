# Physics and Sound


[Physics settings](../../../principles/physics/index.md) of a node can be changed on the *Physics* tab of the *Parameters* window. Here you can assign a required body to the selected node and then set it up.


![](node_physics.png)

*Physics Settings*


However, a node can participate in physical interactions even if it has no physical body assigned: you can enable [collision](../../../principles/physics/collision/index.md) and [intersection](../../../code/usage/intersections/index_cpp.md) detection for node's surfaces on the *Node* tab of the *Parameters* window. Some node's surfaces may not participate in collisions and intersections: these options can be enabled on a per-surface basis.


> **Notice:** To adjust settings of **all** physical objects in the scene at once, tweak the [global physics-related settings](../../../editor2/settings/physics_global/index.md).


## Intersection Parameters


![](surface_intersection.png)

*Intersection Settings*


This section provides parameters for setting up how the selected surface participates in [intersections](../../../code/usage/intersections/index_cpp.md#world_intersection).


| Enabled | Flag indicating if intersections are enabled for the surface. |
|---|---|
| Mask | *[Intersection](../../../principles/bit_masking/index.md#intersection_mask)* mask of the surface. Intersections with the surface will be detected, if its intersection mask matches the intersection mask passed as a [function argument](../../../code/usage/intersections/index_cpp.md), otherwise it is ignored. |


## Physics Intersection Parameters


![](surface_physics_intersection.png)

*Physics Intersection Settings*


This section provides parameters for setting up how the selected surface participates in [physics intersections](../../../code/usage/intersections/index_cpp.md#physics_intersection).


| Enabled | Flag indicating if intersections are enabled for the surface. |
|---|---|
| Mask | *[Physics Intersection](../../../principles/bit_masking/index.md#physics_intersection_mask)* mask of the surface. Physics intersections with the surface will be detected, if its *Physics Intersection* mask matches the one passed as a [function argument](../../../code/usage/intersections/index_cpp.md), otherwise it is ignored. |


## Collision Parameters


![](surface_collision.png)

*Collision Settings*


This section provides parameters for setting up how the selected surface [collides](../../../principles/physics/collision/index.md) with other physical bodies and shapes.


| Enabled | Flag indicating if collisions with the surface are enabled. |
|---|---|
| Mask | *[Collision](../../../principles/bit_masking/index.md#collision_mask)* mask of the surface. The surface will collide with a shape only if their *Collision* masks match. |


## Friction and Restitution


![](surface_physics.png)

*Friction and Restitution Settings*


This section provides parameters for setting up how the selected surface behaves when [colliding](../../../principles/physics/collision/index.md) with physical bodies and shapes.


| Friction | Coefficient of friction for the surface. This coefficient allows to model more rough rubbing of surfaces and is opposite to the body's movement direction. *Friction* parameter values of both surfaces being in contact are considered. The resulting calculated friction depends on the objects' masses and gravity, and the angle between contacting surfaces. - The *higher* the value, the less tendency the body has to slide. Friction is calculated by the contact between physical bodies. |
|---|---|
| Restitution | Coefficient of restitution for the surface. This coefficient determines the degree of relative kinetic energy retained after a collision. It defines how bouncy the object is by contacting with another object. It depends on the elasticity of the materials of colliding bodies. The simulated restitution, like [friction](#surface_friction), considers the total value for both objects being in contact. - The value of 1.0 models elastic collision. Objects bounce off according to the impulse they get by contact. - The value of 0.0 models inelastic collision. Objects do not bounce at all. Restitution is calculated by the contact between physical bodies. |


## Sound Parameters


![](surface_sound.png)

*Sound Settings*


This section provides parameters for setting up how the selected surface affects sound propagation.


| Occlusion | Occlusion value of the selected surface. This value determines how much the surface affects sounds in case of occlusion. > **Notice:** *[Source Occlusion](../../../editor2/settings/sound_global/index.md#source_occlusion)* option must be enabled in the *Sound Settings* window. |
|---|---|
| Occlusion Mask | Bit mask, that determines which sound sources are occluded by the selected surface.  For a sound source to be occluded by the surface, at least one bit of this mask should match the *[Occlusion](../../../objects/sounds/sound_source.md#occlusion)* mask of the sound source. > **Notice:** *[Source Occlusion](../../../editor2/settings/sound_global/index.md#source_occlusion)* must be enabled in the *Sound Settings* window. |
