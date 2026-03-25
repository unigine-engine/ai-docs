# Player Persecutor


A **Player Persecutor** is a flying camera without a physical body that follows the target node at the specified distance. The exact point of the target it follows is called an [anchor](#anchor). The persecutor can either turn around its target, or its viewing direction can be [fixed](#fixed_angles). This camera is approximated with a sphere, which allows it to collide with objects (but it cannot, for example, push them or interact with them).


![](player_persecutor.png)

*Player Persecutorfreely rotating around target*


> **Notice:** As any transformation of a player forces it to recalculate its inner state (position, direction, angles, and so on), the *up* direction of the player's viewport may become "negative forward". And then transformation will be recalculated by using this direction, causing flip of the player's basis. To avoid such flipping, the theta and phi angles should be [recalculated](../../../api/library/players/class.player_cpp.md#setViewDirection_vec3_void) by using the [current viewing orientation](../../../api/library/players/class.player_cpp.md#getViewDirection_vec3) of the player.


### See also


- The *[PlayerPersecutor](../../../api/library/players/class.playerpersecutor_cpp.md)* class to manage the persecutor via API


## Creating a Persecutor


To create a *Player Persecutor*, do the following:


1. On the Menu bar, choose *Create -> Camera -> Persecutor*. ![](creation.png)
2. Place the camera somewhere in the world and specify the required [parameters](../../../objects/players/index.md#view_frustum_params) via the *Parameters* window.


A dummy node named **Persecutor_Target** that represents an [anchor](#anchor) is created along with the *Player Persecutor*. To make any object an anchor of the *Player Persecutor*, make that object a child of the **Persecutor_Target** dummy node.


## Editing a Player Persecutor


In the *Player Persecutor* section of the *Node* tab, you can adjust the [bit masks](../../../objects/players/index.md#set_bit_mask), [viewing frustum parameters](../../../objects/players/index.md#view_frustum_params), and [post-process materials](../../../objects/players/index.md#materials), as well as the specific parameters of the camera described below.


![](persecutor.png)

*Player Persecutorparameters*


### Control Parameters


A set of parameters controlling persecutor movements:


| **Fixed Angles** | Toggles on and off the persecutor's ability to freely rotate around its target. If disabled, the *Player Persecutor* is oriented strictly in one direction. If enabled, only the *phi* angle is fixed, the *theta* can change. |
|---|---|
| **Controlled** | Toggles controls of the *Player Persecutor* on and off (the player's response to them). |
| **Collision** | Toggles [collisions](../../../principles/physics/collision/index.md) for the persecutor on and off. |
| **Collision mask** | A [bit mask](../../../principles/bit_masking/index.md#collision_mask) defining nodes the *Player Persecutor* is able to collide with. |


### Anchor Coordinates


Coordinates of the anchor point:


| **Target node** | The anchor node to which the *Player Persecutor* is bound. By default, the **Persecutor_Target** dummy node created together with the *Player Persecutor* is set as a target node. Any node existing in the World hierarchy can be selected as a target node via the drop-down window. |
|---|---|
| **Anchor point** | Coordinates of an anchor point along the *X, Y*, and *Z* axes (in local coordinates of the target node), to which the persecutor is bound. |


### Distance Parameters


A set of distance parameters:


| **Min Distance** | The minimum possible distance between the persecutor and the target. |
|---|---|
| **Max Distance** | The maximum possible distance between the persecutor and the target. |
| **Min Theta** | The minimum theta angle (zenith angle, also known as pitch angle) that determines how far upward the player can look. |
| **Max Theta** | The maximum theta angle (zenith angle, also known as pitch angle) that determines how far downward the player can look. |
