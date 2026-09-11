# Bit Masking


**Bit masking** is a flexible mechanism used to access only the specific bits in a set of data. It can be applied to the following systems:


- Rendering into viewport
- Shadowing
- Reflections rendering
- Collisions
- Intersections
- Decals
- Fields
- Sound sources
- Physicals
- Pathfinding


To specify the mask, click the corresponding mask button (*Viewport, Shadow, Intersection*, etc.) and enable required bits of a 32-bit mask. Enabling a bit means setting the value of **1** (when disabled, the value is **0**). The resulting mask is displayed as hexadecimal characters on the top of the context menu window. The name of selected bit or bits is displayed on the mask button.


To collapse the context menu, click the mask button once again.


> **Notice:** The *[Material](#material_mask)* mask stores 24 bits. All other masks store 32 bits.


| ![Surface viewport mask](viewport_mask.png) *Bit mask with the first bit turned on* | - **Set All** turns on all the bits in the mask - **Clear All** turns off all the bits in the mask |
|---|---|


Default names of bits can be changed. The name entered in a field is assigned to a selected bit in all masks of this type. For example, if you assign a name to the first bit of the *Viewport* mask of a surface, the same name is displayed for the first bit of the Camera's *Viewport* mask. Bit masks names are assigned locally and stored in the `<Project Name>/data/default.bitmasks` file, which is created when you open your project in UnigineEditor for the first time.


## Comparing Masks


Masks are compared bitwise using binary operator **and**. As a result, the first bit of the first mask is compared to the first bit of the second mask, the second bit � to the second one, and so on.

> **Notice:** If two masks have **at least one matching bit**, the masks match. Values of other bits won't affect the result.


For example, the following viewport masks have 4 matching bits, so they match:


| ![](compare_masks_0.png) | ![](compare_masks_1.png) |
|---|---|
| *The cameraViewportmask with the first 6 bits enabled* | *The object'sViewportmask with the second, third, fourth, and fifth bits enabled* |


Each mask has a hexadecimal representation, which is displayed in the input field of the context menu. You can copy the hexadecimal value of one mask and paste it in the input field of another mask to enable the same bits of the mask.


See a part of our [video tutorial on bit masking](https://youtu.be/nI8Q3bANsM8?t=12) dedicated to a more detailed and visualized explanation of the bit masking concept.


## Rendering into Viewport


[Objects](../../objects/index.md) (along with [decals](../../objects/decals/index.md) and [lights](../../objects/lights/index.md)) can be selectively rendered into viewport. To that end, the camera *Viewport* mask (set in the *[Camera Settings](../../editor2/camera_settings/index.md#camera_settings)* window opened via the *Camera panel*), should match the following masks:


- Object surface *Viewport* mask (*[Parameters](../../editor2/node_parameters/index.md)* window → *Node* tab → *Surfaces* section → *Rendering* field)
- Object material [viewport mask](../../editor2/materials_settings/index.md#viewport_mask) to render the object's material (*Parameters* window → *Node* tab → *Surface Material* section → *Common* tab → *Options* field)


> **Notice:** All masks match each other by default.


### Usage Example


Suppose, we have two objects with the same material. To make one of them to be rendered into viewport and the other one � not to be rendered, we should change the *Viewport* mask of the second object.

| ![](viewport_0.png) | ![](viewport_1.png) |
|---|---|
| ![](viewport_mask_0.png) *In the surfaceViewportmasks of both objects, the same bitViewport Mask 0is enabled (00000001)* | ![](viewport_mask_1.png) *For the first object, all bits of the surfaceViewportmask are disabled (the mask is set to00000000)* |


See the demonstration of how to set rendering into viewport and one more usage example in our [video tutorial on bit masking](https://youtu.be/nI8Q3bANsM8?t=73).


## Reflection Mask


The reflection mask (*Reflection Viewport*) controls rendering of the environment probe reflections and planar dynamic reflections into the viewport of the reflection camera.


The reflection mask can be set:

- For *environment probes* (*Parameters* window → *Node* tab → *Baking Settings* section → *[Reflection Viewport Mask](../../objects/lights/envprobe/index.md#reflection_mask)* button). The mask is used only in combination with [Realtime Update mode](../../objects/lights/envprobe/index.md#mode) enabled for the environment probe.
- For *planar reflections* (*Parameters* window → *Node* tab → *Surface Material* section → *[Parameters](../../editor2/materials_settings/index.md#parameters_tab)* tab → *Planar Reflection* section → *Viewport Mask* button).


For the dynamic reflection to be rendered, the *Reflection Viewport* mask of the reflecting material (*Parameters* window → *Node* tab → *Surface Material* section → *[Parameters](../../editor2/materials_settings/index.md#parameters_tab)* tab → *Planar Reflection* section → *Viewport Mask* button) must have at least one matching bit with each of the following masks:

- *Reflection Viewport* mask of the camera (*[Camera Settings](../../editor2/camera_settings/index.md#camera_settings)* window → *Masks* field)
- *Viewport* mask of the object (*[Parameters](../../editor2/node_parameters/index.md)* window → *Node* tab → *Surfaces* section → *Rendering* field)
- *Viewport* mask of the object's material (*Parameters* window → *Node* tab → *Surface Material* section → *Common* tab → *Options* field)


See also the fragments of our video tutorial on bit masking demonstrating the use of bit masks with [baked reflections](https://youtu.be/nI8Q3bANsM8?t=173) and [dynamic reflections](https://youtu.be/nI8Q3bANsM8?t=207).


### Usage Example


Suppose, you have a reflecting surface and two objects reflected in this surface.

- To render an object without a reflection, either its *Viewport* mask **or** its material's *Viewport* mask should have no matching bits with the planar reflection's *Viewport* mask **or** the camera's reflection *Viewport* mask.
- To render a reflection without an object, the object's *Viewport* mask **or** its material's *Viewport* mask should have no matching bits with the camera's *Viewport* mask.


In the example below, masks are given in the binary representation. For convenience, let's assume that objects and their materials have identical *Viewport* masks. For masks to match, they should share **1** in the appropriate bit position. You can convert these masks to the hexadecimal number representation and set the obtained values via UnigineEditor.


| ![](reflection_mask_0.png) *An object without the reflection* | ![](reflection_mask_1.png) *A reflection without the object* |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| \| Mask \| Value \| \|---\|---\| \| Camera viewport mask \| 011**1** \| \| Camera reflection viewport mask \| 110**0** \| \| Viewport mask of the first object \| 000**1** \| \| Viewport mask of the second object \| 0110 \| \| Planar reflection viewport mask of the reflecting surface material \| 111**0** \| | Mask | Value | Camera viewport mask | 011**1** | Camera reflection viewport mask | 110**0** | Viewport mask of the first object | 000**1** | Viewport mask of the second object | 0110 | Planar reflection viewport mask of the reflecting surface material | 111**0** | \| Mask \| Value \| \|---\|---\| \| Camera viewport mask \| **0**111 \| \| Camera reflection viewport mask \| **1**100 \| \| Viewport mask of the first object \| **1**000 \| \| Viewport mask of the second object \| 0110 \| \| Planar reflection viewport mask of the reflecting surface material \| **1**110 \| | Mask | Value | Camera viewport mask | **0**111 | Camera reflection viewport mask | **1**100 | Viewport mask of the first object | **1**000 | Viewport mask of the second object | 0110 | Planar reflection viewport mask of the reflecting surface material | **1**110 |
| Mask | Value |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Camera viewport mask | 011**1** |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Camera reflection viewport mask | 110**0** |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Viewport mask of the first object | 000**1** |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Viewport mask of the second object | 0110 |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Planar reflection viewport mask of the reflecting surface material | 111**0** |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Mask | Value |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Camera viewport mask | **0**111 |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Camera reflection viewport mask | **1**100 |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Viewport mask of the first object | **1**000 |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Viewport mask of the second object | 0110 |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Planar reflection viewport mask of the reflecting surface material | **1**110 |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |


In the first example, the object's *Viewport* mask doesn't match the camera's reflection *Viewport* mask. However, it matches the camera's *Viewport* mask, so the object is rendered.


In the second example, the object's *Viewport* mask doesn't match the camera's *Viewport* mask. However, it matches the camera's *Reflection Viewport* mask **and** the planar reflection's *Viewport* mask, so the reflection is rendered.


## Shadow Mask


The *Shadow* mask controls rendering of a shadow cast by an object lit by a light source.


For a shadow to be rendered, the *[Shadow](../../objects/lights/parameters/index.md#shadow_mask)* mask of the light source that illuminates the object must match the following masks (one bit at least):


- Object surface *Shadow* mask (*Parameters* window → *Node* tab → *Surfaces* section → *Rendering* field)
- Object material *[Shadow](../../editor2/materials_settings/index.md#shadow_mask)* mask (*Parameters* window → *Node* tab → *Surface Material* section → *Common* tab → *Options* field)


### Usage Example


The example below demonstrates the difference. On the left, the *Shadow* masks of the surface and its material have all bits enabled, thus they have one bit matching the *Shadow* mask of the light source, and the shadow is rendered. On the right, the *Shadow* masks of the surface and its material don't match the *Shadow* mask of the light source, so the shadow isn't rendered.


| ![](shadow_mask_0.png) | ![](shadow_mask_1.png) |
|---|---|
| ![](surface_shadow_mask_0.png) *Shadowmask of the surface and its material* | ![](surface_shadow_mask_1.png) *Shadowmask of the surface and its material* |
| ![](light_shadow_mask.png) *Shadowmask of the light source* | ![](light_shadow_mask.png) *Shadowmask of the light source* |


See one more usage example in our [video tutorial on bit masking](https://youtu.be/nI8Q3bANsM8?t=288).


## Material Mask


> **Notice:** *Decal* mask was renamed *Material* mask.


A *Material* mask is a 24-bit mask that specifies objects onto which the decal can be projected. An object or one of its surfaces can receive the decal only if the object's *Material* mask corresponds to the *Material* mask of the decal.


The *Material* mask can be specified for a selected material on the *Parameters* tab of the material editor:


![](material_mask.png)

*Materialmask field*


See how the decal projection area can be restricted using the *Material* mask in our [video tutorial on bit masking](https://youtu.be/nI8Q3bANsM8?t=326).


## Intersection Mask


The *Intersection* mask specifies objects (including objects, nodes, shapes, collision objects, and obstacles) for which [intersections](../../code/usage/intersections/index_cpp.md) will or won't be found. An intersection is found only if the *Intersection* mask of the object matches the *Intersection* mask passed as a function argument, otherwise it is ignored.


The mask for the object's surface can be specified via UnigineEditor or [API](../../api/library/objects/class.object_cpp.md).


The *Intersection* mask can be used to clarify the object search or increase performance by limiting the number of objects that can participate in intersections.


Our video tutorial on bit masking features two use cases of the *Intersection* mask: [excluding objects from intersection detection](https://youtu.be/nI8Q3bANsM8?t=356) and [cutting out grass](https://youtu.be/nI8Q3bANsM8?t=406).


## Collision Mask


The *Collision* mask allows you to filter particular shapes and bodies for physical interaction: only objects with the matching *Collision* mask will collide. If masks do not match, shapes and bodies simply ignore each other by going through.


For example, we have four bodies that should collide in the following way:


|  | Body A | Body B | Body C | Body D |
|---|---|---|---|---|
| Body A |  |  |  | ![](check.png) |
| Body B |  |  | ![](check.png) | ![](check.png) |
| Body C |  | ![](check.png) |  | ![](check.png) |
| Body D | ![](check.png) | ![](check.png) | ![](check.png) |  |


For that, each colliding body should share **1** in the appropriate bit position:


| Body | Mask |
|---|---|
| Body A | 0001 |
| Body B | 0010 |
| Body C | 0110 |
| Body D | 1111 |


See how the *Collision* mask works in our [video tutorial on bit masking](https://youtu.be/nI8Q3bANsM8?t=435).


## Exclusion Mask


An analogue of the *[Collision](#collision_mask)* mask but working vice versa. It is used to prevent collisions of the shape with other shapes. For shapes with matching *Collision* masks not to collide, at least one bit of their *Exclusion* mask should match. **0** enables collisions with all shapes with matching *Collision* masks. This mask is independent of the *Collision* mask.


> **Notice:** Can be used for [Shape-Shape collisions](../../principles/physics/collision/index.md#collision_types) only.


See how the *Exclusion* mask works in our [video tutorial on bit masking](https://youtu.be/nI8Q3bANsM8?t=508).


## Physics Intersection Mask


[Physics intersections](../../code/usage/intersections/index_cpp.md#physics_intersection) (between physical objects with bodies and collider shapes, or ray intersections with [collider geometry](../../principles/physics/collision/index.md)) use a separate mask, other than the one described [above](#intersection_mask) and used for [world intersections](../../code/usage/intersections/index_cpp.md#world_intersection) (i.e., between object bound volumes, or ray intersections with object surfaces). This offers more flexibility enabling you to control them independently.


Physics intersections can be used, for example, to detect collisions of spawned particles with physical shapes and bodies, or static collider surfaces to ensure proper interaction, or as a quick way to detect collisions for raycast-wheels of a simulated ground vehicle, or to check if a destructible object or a player was hit by a projectile.


The *Physics Intersection* mask can be specified via the UnigineEditor or via API for a [particle system](../../objects/effects/particles/index.md#interaction), a [shape](../../principles/physics/shapes/index.md#intersection_mask), a [fracture body](../../principles/physics/bodies/fracture/index.md), a [player actor](../../objects/players/actor/index.md#int_mask), or a [wheel joint](../../principles/physics/joints/index.md#suspension) to enable selective physics intersection detection or increase performance by limiting the number of objects that can participate in physics intersections. It san also be set for the object's surface (if this object has no body or shape assigned and is to be treated as a static collider) via [UnigineEditor](../../editor2/node_parameters/physics/index.md#surface_physics_intersection) or [API](../../api/library/objects/class.object_cpp.md#setPhysicsIntersectionMask_int_int_void).


## Physical Mask


A bit mask that filters objects interacting with physical nodes: *force, wind, water*. This mask is set according to the same principle as the *[collision mask](#collision_mask)*. For example, a body with a mismatching mask placed in the physical water will not float.


An example of the *Physical* mask working with physical effects is shown in our [video tutorial on bit masking](https://youtu.be/nI8Q3bANsM8?t=521).


## Sound Sources Masks


Masks can be set via both UnigineEditor and [API](../../api/library/sounds/index.md).


To see and hear how sound-related masks are used, watch our [video tutorial on bit masking](https://youtu.be/nI8Q3bANsM8?t=540).


### Source Mask


A bit mask that determines to what sound channels the sound source belongs to. For a sound source to be heard, its mask should match the [player's sound mask](../../objects/players/index.md#set_bit_mask) in at least one bit.


### Reverb Mask


A bit mask that determines which [reverberation zones](../../objects/sounds/sound_reverb.md) can be heard. For sound to reverberate, at least one bit of this mask should match the [player's reverberation mask](../../objects/players/index.md#set_bit_mask). At the same time, the *Reverb* mask of the player should match the *Reverb* mask of the [sound source](../../objects/sounds/sound_source.md) (but not necessarily in the same bits).


### Occlusion Mask


A bit mask that determines which sound sources are occluded by the selected surface. For a sound source to be occluded by the surface, at least one bit of this mask should match the *[Occlusion](../../objects/sounds/sound_source.md#occlusion)* mask of the sound source.


> **Notice:** *[Source Occlusion](../../editor2/settings/sound_global/index.md#source_occlusion)* must be enabled in the *Sound Settings* window.


## Navigation Mask


The *Navigation* mask is used to specify [navigation areas](../../objects/navigations/navigation/index.md) that participate or don't participate in pathfinding. The *Navigation* mask should match the *Navigation* mask of the [route](../../api/library/pathfinding/class.pathroute_cpp.md) that is calculated within the navigation area; otherwise, the area does not participate in pathfinding.


The *Navigation* mask for the navigation areas can be specified via:


- UnigineEditor in the *Navigation Sector/Navigation Mesh* section of the *[Parameters](../../editor2/node_parameters/index.md)* window
- [Unigine API](../../api/library/pathfinding/class.navigation_cpp.md#setNavigationMask_int_void)


> **Notice:** The *Navigation* mask for a **route** can be specified only via [API](../../api/library/pathfinding/class.pathroute_cpp.md#setNavigationMask_int_void).


Using the *Navigation* mask, you can limit the number of navigation areas, inside which the specific route can be calculated. For example, you can use the mask to calculate 2 non-intersecting routes inside the intersecting navigation areas.


A usage example of the *Navigation* mask is provided in our [video tutorial on bit masking](https://youtu.be/nI8Q3bANsM8?t=601).


In the experimental navigation system the *Navigation* mask does the same job, with the baked [navigation mesh](../../objects/navigations/experimental/navigation_mesh/index.md) in place of a navigation area. A navigation mesh carries a mask, and so does everything that works with it. The ground of a mesh is taken into account only while the two masks share at least one bit.


Four things carry a mask of their own:


- The *[query filter](../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cpp.md)*. A path search walks a navigation mesh only while their masks match. This is how one world holds a navigation mesh baked for infantry and another baked for vehicles, and each unit searches its own.
- The [invoker](../../objects/navigations/experimental/invoker/index.md). It loads tiles only for the navigation meshes its mask matches. A navigation mesh with streaming on and no matching invoker holds no tiles at all, and every query over it fails for lack of data.
- The *[avoidance](../../api/library/pathfinding/class.experimentalnavigationavoidance_cpp.md)* solver. It reads the walls of the navigation meshes its mask matches, so that an agent pushed aside by its neighbors is not pushed off the walkable ground.
- Baking. *[ExperimentalBakeNavigation](../../api/library/pathfinding/class.experimentalbakenavigation_cpp.md)* takes a mask instead of a list of nodes, which bakes or rebuilds a whole group in one call. This form picks up the navigation meshes of the experimental system only, and the enabled ones only.


> **Notice:** A mask of 0 matches nothing. An avoidance solver left with it keeps the agents apart from each other and knows about no walls at all, so a crowd squeezed into a corner walks through them.


Both systems use this one mask, and the names given to its bits are shared: a bit named in the mask of a navigation area is the same bit under the same name in the mask of a baked navigation mesh. What is not shared is the comparing. A route is matched against navigation areas, a query filter against baked navigation meshes, and neither is ever matched against the other, so the same value on both sides means nothing by itself.


The mask of the ground itself is a different one: which surfaces and terrains a navigation mesh takes in is decided by the [Bake](#bake_mask) mask, not by this one.


## Bake Mask


The *Bake* mask decides which geometry is taken in when a navigation mesh is baked. Geometry contributes only when its own bake mask shares at least one bit with the mask the bake runs with.


It is carried by both sides of that comparison:


- A surface of an object, in the *Experimental Navigation* section of the surface. A surface with the section disabled is out of every bake, whatever its mask says.
- A terrain, and separately every detail mask of it. The terrain is taken in when the mask of the node matches, or when at least one of its detail masks does, and a detail mask that matches also brings its own area and its own threshold with it.
- An [area volume](../../objects/navigations/experimental/area_volume/index.md). Its mask picks the navigation meshes the volume marks, so one volume can raise the cost for one navigation mesh and leave the rest untouched.
- The bake settings of the navigation mesh itself, which is what everything above is matched against.


Both node types are baked by the same pipeline, so the mask works the same way for a [Navigation Mesh](../../objects/navigations/navigation/navigation_mesh/index.md) and for an [Experimental Navigation Mesh](../../objects/navigations/experimental/navigation_mesh/index.md): each of them carries bake settings with a mask of its own.


Two masks are therefore in play at different times, and they are easy to confuse. The *Bake* mask acts while the navigation mesh is being built, and decides what the walkable ground is made of. The *[Navigation](#navigation_mask)* mask acts on every query afterwards, and decides who may use the result. They are two separate sets of named bits: the names given to the bits of one say nothing about the bits of the other.


A partial rebuild is filtered by the same mask: a region sent for rebuilding reaches a navigation mesh only while the two bake masks match.


## Obstacle Mask


The *Obstacle* mask is used to specify [obstacles](../../objects/navigations/obstacle/index.md) inside [navigation areas](../../objects/navigations/navigation/index.md) that are or aren't bypassed during pathfinding. The *Obstacle* mask of an obstacle should match the *Obstacle* mask of the route that is calculated; otherwise, the obstacle is not taken into account.


Similar to the navigation mask, the obstacle mask can be specified via:


- UnigineEditor in the *Obstacle Box/Sphere/Capsule* section of the *[Parameters](../../editor2/node_parameters/index.md)* window
- [Unigine API](../../api/library/pathfinding/class.obstacle_cpp.md#setObstacleMask_int_void)


> **Notice:** The obstacle mask for a **route** can be specified only via [API](../../api/library/pathfinding/class.pathroute_cpp.md#setObstacleMask_int_void).


A usage example of the *Obstacle* mask is provided in our [video tutorial on bit masking](https://youtu.be/nI8Q3bANsM8?t=629).


The experimental navigation system reuses the very same [Obstacle](../../api/library/pathfinding/class.obstacle_cpp.md) nodes and the same mask. It is carried by the [query filter](../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cpp.md), by the [corridor](../../api/library/pathfinding/class.experimentalnavigationmeshcorridor_cpp.md) that follows a path, and by [local avoidance](../../api/library/pathfinding/class.experimentalnavigationavoidance_cpp.md), each of which can be told to consider a different set of obstacles. Setting the mask to 0 there means the obstacles are ignored altogether rather than that none of them match.


## Field Mask


The *Field* mask defines if an object such as grass, water, or clouds interacts with a [field](../../objects/effects/fields/index.md) object. The *Field* mask of a field node should match the *Field* mask of the grass, water, or cloud layer.


The *Field* mask can be set via UnigineEditor or API.


A usage example of the *Field* mask is provided in our [video tutorial on bit masking](https://youtu.be/nI8Q3bANsM8?t=646).


## Particles Field Mask


The *Particles Field* mask is used for interaction of particles with *Particles Field* nodes (*[Deflectors](../../objects/effects/particles/field_deflector/index.md)* and *[Spacers](../../objects/effects/particles/field_spacer/index.md)*). Emitted particles will be affected by a *Particles Field* only if their masks match (one bit at least).
