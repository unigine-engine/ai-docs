# Player Dummy


A **Player Dummy** is a simple viewport into the world that has no physical properties and cannot collide with objects.


### See also


- The *[PlayerDummy](../../../api/library/players/class.playerdummy_cpp.md)* class to manage the *Player Dummy* via API


> **Notice:** As any transformation of a player forces it to recalculate its inner state (position, direction, angles, and so on), the *up* direction of the player's viewport may become "negative forward". And then transformation will be recalculated by using this direction, causing flip of the player's basis. To avoid such flipping, the theta and phi angles should be [recalculated](../../../api/library/players/class.player_cpp.md#setViewDirection_vec3_void) by using the [current viewing orientation](../../../api/library/players/class.player_cpp.md#getViewDirection_vec3) of the player.


## Creating a Dummy Player


To create a *Player Dummy*, do the following:


1. On the Menu bar, choose *Create -> Camera -> Dummy*. ![](creation.png)
2. Place the camera somewhere in the world and specify the required [parameters](../../../objects/players/index.md#view_frustum_params) via the *Parameters* window.


## Editing a Dummy Player


In the *Player Dummy* section of the *Node* tab, you can adjust the [bit masks](../../../objects/players/index.md#set_bit_mask) and [viewing frustum parameters](../../../objects/players/index.md#view_frustum_params) of the *Player Dummy* and assign [post-process materials](../../../objects/players/index.md#materials) to be applied to the camera view.


![](../parameters_0.png)

*Vertical Player Parameters*


![](../parameters_1.png)

*Physically-Based Player Parameters*
