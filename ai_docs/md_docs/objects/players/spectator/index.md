# Player Spectator


A **Player Spectator** is a free flying camera without a physical body, which is approximated with a sphere and therefore can collide with objects (however, it cannot push or interact with them).


As well as for *[Player Actor](../../../objects/players/actor/index.md)*, the viewing orientation of a *Player Spectator* in space is defined by 2 angles - *[theta](../../../api/library/players/class.playerspectator_cpp.md#setThetaAngle_float_void)* and *[phi](../../../api/library/players/class.playerspectator_cpp.md#setPhiAngle_float_void)* - and by the *[up](../../../api/library/players/class.player_cpp.md#setUp_vec3_void)* vector that usually coincides with the Z axis:


- When changing the *theta* angle, the vertical view direction of the *Player Spectator* changes.
- When changing the *phi* angle, the horizontal view direction and the basis of the *Player Spectator* change.


![](player_spectator.png)


A *Player Spectator* can be used to create a *spectator mode* that allows for observing the world. Due to collisions, movement of the camera can be limited.


> **Notice:** As any transformation of a player forces it to recalculate its inner state (position, direction, angles and so on), the *up* direction of the player's viewport may become "negative forward". And then transformation will be recalculated by using this direction, causing flip of the player's basis. To avoid such flipping, the theta and phi angles should be [recalculated](../../../api/library/players/class.player_cpp.md#setViewDirection_vec3_void) by using the [current viewing orientation](../../../api/library/players/class.player_cpp.md#getViewDirection_vec3) of the player.


### See also


- The *[PlayerSpectator](../../../api/library/players/class.playerspectator_cpp.md)* class to manage the spectator via API


## Creating a Spectator


To create a spectator camera, do the following:


1. On the Menu bar, choose *Create -> Camera -> Spectator*. ![](creation.png)
2. Place the camera somewhere in the world and specify the required parameters via the *Parameters* window.


## Editing a Player Spectator


In the *Node* tab, you can adjust the [bit masks](../../../objects/players/index.md#set_bit_mask), [viewing frustum parameters](../../../objects/players/index.md#view_frustum_params), and [post-process materials](../../../objects/players/index.md#materials), as well as the specific [physical parameters](#physical) of the camera described below.


![](edit_player_spectator.png)

*Player Spectatorparameters*


### Physical parameters


| **View Direction** | X, Y, and Z values of the vector defining where the player's view is directed. |
|---|---|
| **Controlled** | Toggle controls of the *Player Spectator* on and off (the player's response to them). |
| **Collision** | Toggle on and off the player's ability to collide with other objects. |
| **Collision Mask** | A [bit mask](../../../principles/bit_masking/index.md#collision_mask) defining nodes the player is able to collide with. |
| **Collision Radius** | The radius of the player's sphere. |
| **Min Velocity** | The default velocity of the player. |
| **Max Velocity** | The velocity of the spectator, which is used while the spectator runs (the run control state is pressed). |
| **Min Theta** | The minimum theta angle (zenith angle, also known as pitch angle) that determines how far upward the player can look. |
| **Max Theta** | The maximum theta angle (zenith angle, also known as pitch angle) that determines how far downward the player can look. |
| **Acceleration** | The player's acceleration. |
| **Damping** | The player's velocity damping with the time. |
| **Turning** | The velocity of the player's turning action. |
| **Phi** | The phi angle (azimuth angle, also known as yaw angle). This angle determines the horizontal viewing direction, i.e. left or right. |
| **Theta** | The theta angle (zenith angle, also known as pitch angle). This angle determines the vertical viewing direction, i.e. upward and downward. The value is clamped between the minimum and the maximum theta angle. |
| **Num Contacts** | The number of contacts, in which the player's sphere participates. |
