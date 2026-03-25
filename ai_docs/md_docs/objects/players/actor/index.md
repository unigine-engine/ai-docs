# Player Actor


A **Player Actor** is a player with a rigid physical body, which is approximated with a capsule and has physical properties. Unlike all other players that can move in any direction, the *Player Actor* can only walk on the ground.


The viewing orientation of a *Player Actor* in space is defined by 2 angles - *[theta](../../../api/library/players/class.playeractor_cpp.md#setThetaAngle_float_void)* and *[phi](../../../api/library/players/class.playeractor_cpp.md#setPhiAngle_float_void)* - and by the *[up](../../../api/library/players/class.player_cpp.md#setUp_vec3_void)* vector that usually coincides with the Z axis:


- When changing the *theta* angle, the vertical view direction of the *Player Actor* changes.
- When changing the *phi* angle, the horizontal view direction and the basis of the *Player Actor* change.


![](player_actor.png)

*Player ActorApproximated with Capsule*


> **Notice:** As any transformation of a player forces it to recalculate its inner state (position, direction, angles and so on), the *up* direction of the player's viewport may become "negative forward". And then transformation will be recalculated by using this direction, causing flip of the player's basis. To avoid such flipping, the theta and phi angles should be [recalculated](../../../api/library/players/class.player_cpp.md#setViewDirection_vec3_void) by using the [current viewing orientation](../../../api/library/players/class.player_cpp.md#getViewDirection_vec3) of the player.


If you need a *Player Actor* to go up and down a staircase smoothly, without getting stuck on each stair, you should carefully adjust the [radius](../../../api/library/players/class.playeractor_cpp.md#setCollisionRadius_float_void) of the capsule that approximates the player. Or you can approximate the staircase with a plane: in this case, the capsule can be of any radius.


The [height](../../../api/library/players/class.playeractor_cpp.md#setCollisionHeight_float_void) of the player's capsule should also be set correctly to avoid getting stuck in a doorway.


A *Player Actor* can be used to create a first person view. Also a *Player Actor* can be used in pair with *[Player Persecutor](../../../objects/players/persecutor/index.md)* to create a 3rd person view (see the corresponding [samples](#see_also) in the SDK).


### See also


- The *[PlayerActor](../../../api/library/players/class.playeractor_cpp.md)* class to manage the *Player Actor* via API
- A set of samples located in the `<UnigineSDK>/data/samples/players/` folder:

  - `actor_00`
  - `actor_01`


## Calculating Collisions


When a *Player Actor* is not [simulated as a rigid body](../../../api/library/players/class.playeractor_cpp.md#setPhysical_int_void), a simple *Body Dummy* with a capsule shape is used to calculate collisions:


1. All contacts with the shape are found.
2. The *Player Actor* is pushed out of objects it collided with along the contact normal (the global penetration factor is also taken into account here). Effectively, it's a sum of all normal vectors of found contacts.
3. The velocity change is calculated: the initial velocity vector is projected onto each contact normal (the dot product is calculated) and the result is subtracted from the initial velocity.


## Creating an Actor


To create a *Player Actor* camera, do the following:


1. On the Menu bar, choose *Create -> Camera -> Actor*. ![](creation.png)
2. Place the camera somewhere in the world and specify the required parameters via the *Parameters* window.


## Editing a Player Actor


In the *Player Actor* section of the *Node* tab, you can adjust [common camera parameters](../../../objects/players/index.md#common): [bit masks](../../../objects/players/index.md#set_bit_mask), [viewing frustum parameters](../../../objects/players/index.md#view_frustum_params), and [post-process materials](../../../objects/players/index.md#materials), as well as actor-specific [physical parameters](#physical) of the camera described below.


![](edit_player_actor.png)

*Player Actorparameters*


### Physical parameters


| **Physical** | Toggle on and off the [rigid body](../../../principles/physics/bodies/rigid/index.md) of the *Player Actor*. Enabled Physical allows interacting with the environment as a physical object. |
|---|---|
| **Physical Mass** | The player's [physical mass](../../../principles/physics/bodies/index.md#mass). If *g* (Earth's gravity) equals to ***9.8** m/s^2*, and **1** unit equals to **1** meter, the mass is measured in kilograms. |
| **Physical Mask** | A [bit mask](../../../principles/bit_masking/index.md#physical_mask) defining the player's interaction with physicals. |
| **Physics Intersection Mask** | A [bit mask](../../../principles/bit_masking/index.md#physics_intersection_mask) defining the player's physics intersection with other objects. |
| **Collision** | Toggle on and off the player's ability to collide with other objects. |
| **Collision Mask** | A [bit mask](../../../principles/bit_masking/index.md#collision_mask) defining nodes the *Player Actor* is able to collide with. |
| **Collision Radius** | The radius of the player's capsule. |
| **Collision Height** | The height of the player's capsule. |
| **Min Velocity** | The default velocity of the *Player Actor*. |
| **Max Velocity** | The velocity of the *Player Actor* used when the actor runs. |
| **Min Theta** | The minimum *theta* angle (zenith angle, also known as pitch angle) that determines how far upward the player can look. |
| **Max Theta** | The maximum *theta* angle (zenith angle, also known as pitch angle) that determines how far downward the player can look. |
| **Acceleration** | The player's acceleration. |
| **Damping** | The player's velocity damping with the time. |
| **Turning** | The velocity of the player's turning action. |
| **Jumping** | The jumping coefficient. The greater the value, the higher the *Player Actor* jumps. |
| **Max Step Height** | The maximum step height. The value defines the maximum height of a surface to which the player can make a step. It can be used for walking up and down the stairs and stepping over curbs. |
| **Phi** | The *phi* angle (azimuth angle, also known as yaw angle). This angle determines the horizontal viewing direction, i.e. left or right. |
| **Theta** | The *theta* angle (zenith angle, also known as pitch angle). This angle determines the vertical viewing direction, i.e. upward and downward. The value is clamped between the minimum and the maximum *theta* angle. |
| **View Direction** | X, Y, and Z values of the vector defining where the player's view is directed. |
| **Ground** | A flag indicating that the player currently stands on the ground surface. This flag is used to set actor state, i.e. play the corresponding skinned animation of standing/walking instead of being in the air. |
| **Ceililng** | A value indicating if the actor touches the ceiling surface with its head. |
| **Num Contacts** | The number of contacts, in which the player's capsule participates. |
