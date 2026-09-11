# Players


Players are cameras creating viewports into the world. The cameras available in UnigineEditor are:


- **[![](player.png)](../../objects/players/actor/index.md) � [Player Actor](../../objects/players/actor/index.md)** is a player with a rigid physical body that can only walk on the ground.
- **[![](player.png)](../../objects/players/dummy/index.md) � [Player Dummy](../../objects/players/dummy/index.md)** is a simple viewport into the world that has no physical properties and cannot collide with objects.
- **[![](player.png)](../../objects/players/persecutor/index.md) � [Player Persecutor](../../objects/players/persecutor/index.md)** is a free flying camera without a physical body that follows the target node at the specified distance. It can collide with objects but cannot interact with them.
- **[![](player.png)](../../objects/players/spectator/index.md) � [Player Spectator](../../objects/players/spectator/index.md)** is a free flying camera without a physical body that is used to create a *spectator mode*. It can collide with objects but cannot push or interact with them.


There are other types of cameras not present in the Editor. These camera types can be controlled via code.


### See Also


- The *[Player](../../api/library/players/class.player_cpp.md)* class to edit all kinds of players via API
- Recommendations on *[setting up cameras](../../editor2/camera_settings/index.md)*
- Creating and configuring different types of players (*PlayerDummy, PlayerPersecutor, PlayerSpectator, PlayerActor*) in the C++ sample
- *C++ and C# Component* sample sets demonstrating complex solutions for setting up and adjusting cameras for various use cases
- implementation in the C++ sample set demonstrating a multiview split screen combining views from cameras having different projection matrices
- **Zoom** implementation in the *C++* and *C# Component* sample sets demonstrating an interactive camera system with adjustable zoom and focus on selectable scene targets
- *C++* and *C# Component* samples demonstrating how to prevent weapon models from clipping through geometry in first-person view
- implementation in the C++ sample demonstrating how to capture views from two different cameras into separate textures
- implementation in the C++ sample illustrating how to create a two-point perspective projection visual effect using the camera lens shift


## Common settings


For all players listed above, there is the set of common settings. They can be changed on the *Node* tab of the *Parameters* window:


![](parameters_0.png)

*Vertical player parameters*


![](parameters_1.png)

*Physically-based player parameters*


| **Main Player** | Defines whether the player is used as the default camera at run time. If several players have this flag enabled, the last one in [node hierarchy](../../principles/world_structure/index.md#nodes_hierarchy) will be used. > **Notice:** The flag is ignored if you work with a template-based C# project that uses the component (when *Camera Mode = CREATE_AUTOMATICALLY*), as this component creates and sets a new default camera. |
|---|---|
| **Listener** | Defines whether the player is used to listen to sounds at run time. |


### Setting bit masks


A set of bit masks available for the player:


| **[Viewport Mask](../../principles/bit_masking/index.md#viewport)** | Controls rendering of objects, decals, and lights into the camera's viewport. |
|---|---|
| **[Reflection Mask](../../principles/bit_masking/index.md#reflection_mask)** | Controls rendering of the *Environment Probe* and planar dynamic reflections into the camera's viewport. |
| **[Source Mask](../../principles/bit_masking/index.md#source_mask)** | Specifies what sound channels are played for this camera. |
| **[Reverb Mask](../../principles/bit_masking/index.md#reverb_mask)** | Specifies what reverberations are played for this camera. |


### Viewing frustum parameters


| **FOV Mode** | Depending on the **FOV Mode**, parameters defining a player's viewing frustum differ: - **Vertical** FOV is used for the standard player. In this case, the *[FOV](#fov)* is set in degrees. - **Physically-Based Camera** is used for the physically-based player with the horizontal FOV. In this case, the FOV is calculated depending on the [film gate](#film_gate) and [focal length](#focal_length) of the camera according to the formula: **FOV = 2 * atan(film_gate / (2 * focal_length)) * [RAD2DEG](../../api/library/math/constants_cpp.md#UNIGINE_RAD2DEG)** |
|---|---|
| **FOV Degrees** | The camera's vertical field of view, in degrees. |
| **Focal Length** | Focal length of the physically-based camera lens, in millimeters. Determines the area that can be seen in the camera's viewport. |
| **Film Gate** | Horizontal size of the film gate for the physically-based camera with horizontal FOV, in millimeters. Determines the area that can be seen in the camera's viewport. |
| **Near Clipping** | Distance to the near clipping plane of the player's viewing frustum, in units. |
| **Far Clipping** | Distance to the far clipping plane of the player's viewing frustum, in units. |


### Postprocess materials


By clicking *Add New Material*, you can add [postprocess materials](../../content/materials/library/postprocess/index.md) to the camera in the fields that appear. These materials will be applied after all other postprocesses (such as HDR, DOF, etc.) are applied.


To add a postprocess material type its name in the field, or drag the desired material to this field.


Several postprocess materials are rendered according to their order top-down.
