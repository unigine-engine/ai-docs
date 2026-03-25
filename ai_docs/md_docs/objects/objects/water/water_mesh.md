# Water Mesh


**Water Mesh** is a loaded mesh usually used to create finite basins of an arbitrary form. The differences between the Water Mesh and the Global Water are the following:


- The *water mesh* can provide buoyancy simulation (it can have a [body](../../../principles/physics/bodies/water/index.md) assigned).
- The underwater mode is not available for the *water mesh*.
- The *water mesh* can have *multiple water levels*. It means that you can create, for example, a water flow with height difference located above the sea level (i.e. the filling level of *global water*).


[![](water_mesh.jpg)](water_mesh.jpg)


### See also


- The *[ObjectWaterMesh](../../../api/library/objects/class.objectwatermesh_cpp.md)* class to edit water meshes via API
- The *[water_mesh_base](../../../content/materials/library/water_mesh_base/index.md)* material that is applied to water
- Physical simulation with [water body](../../../principles/physics/bodies/water/index.md)


## Mesh Requirements


Water mesh can be of any arbitrary form and size, but there are also 3 major requirements:


- The mesh should be flat and have a uniform grid.
- The mesh should be oriented strictly along the axes.
- The mesh should have the UV map. Otherwise, normal maps used to simulate water surface rippling won't be applied.


Besides these requirements, there are also several important notes:


- Triangulation of polygons in the *water mesh* is not important for waves simulation as changes are made for mesh vertices. However, triangulation affects the final appearance of water surface during waves simulation. For example, appearance of the water mesh with polygons that are triangulated as follows will differ: | ![](triangulation_1.png) | ![](triangulation_2.png) | |---|---|
- If one mesh is used to represent several water basins with [dynamic reflections](../../../objects/objects/water/index.md#reflections), they all should be exported on the same level (height) (as dynamic reflections are calculated correctly only for flat horizontal meshes exported on the same level). You still can create a mesh with different heights, however, in this case, you will be limited to [static reflections](../../../objects/objects/water/index.md#reflections) only.
- Scale of mesh UV coordinates affects appearance of water waves simulated by using normal maps. For example, if you apply the same normal map to 2 meshes with UV coordinates at the scale of 1:1 and 2:1 correspondingly, waves on the second mesh will be narrower than on the first mesh because of normal map tiling. | ![](water_uv.jpg) *UV coordinates at scale of 1:1* | ![](water_uv_scaled.jpg) *UV coordinates at scale of 2:1* | |---|---|
- To simulate a river flow, make sure that its UV map is rectangular.


## Adding Water Mesh


To add a water object of a finite size to the scene via UnigineEditor:


1. On the Menu bar, click *Create -> Water -> Mesh*: ![](add_water_mesh.png)
2. Choose a mesh to be used and place the *water mesh* object in the scene: ![](choose_mesh.png)


## Editing Water


Settings of a *water mesh* object can be adjusted via the *[Parameters](../../../editor2/node_parameters/index.md)* window:


- In the *Water Mesh* section, [waves](#waves) that determine periodic and sinusoidal nature of water can be set. Also on the *Water Mesh* tab, you can set a mesh to used for the *water mesh* object and specify a [field mask](../../../objects/objects/water/index.md#field_interaction).
- In the *Surfaces* section, [water surfaces](../../../objects/objects/water/index.md#surfaces) that determine optical and dynamic behaviour of water can be adjusted.


## Water Waves


By default, water surface ripples according to the normal map (see the *[water_mesh_base](../../../content/materials/library/water_mesh_base/index.md#texture_normal_detail)* material). However, different kinds of waves can be also simulated with *4 directional geometrical waves*, summed to create dynamic waves. This model uses static geometry animated in vertex shader. Movement each of the wave is set independently that enhances flexibility of adjustment.


The waves have the following characteristics defining their periodic and sinusoidal nature:


![](object_water_settings.png)


| Direction | A directional wave (unlike the circular one from the objects, for example) travels along the specified direction: - By the minimum value of 0, the wave spreads along the Y axis and is parallel to the X axis. - *Positive* values rotate the wave about the Z axis, meaning the wave direction is slanted counterclockwise relative to its initial spread. - *Negative* values rotate the wave on the water surface clockwise. - By the maximum possible values of 180 or -180, the wave direction becomes parallel to the X axis yet again. |  |  |
|---|---|---|---|
| Speed | The wave progresses along the water surface with the definite speed (measured in units per second): - The minimum value of 0 means the wave is inactive. - *Increasing* the value results in waves following each other faster. |  |  |
| Length | The length represents distance between successive crests of the wave: - The *smaller* the value, the more rippled the water surface is. - The *higher* the value, the broader formed waves are. \| ![](1_wave_length_10.png) *Length of the First Wave = 10* \| ![](1_wave_length_70.png) *Length of the First Wave = 70* \| \|---\|---\| | ![](1_wave_length_10.png) *Length of the First Wave = 10* | ![](1_wave_length_70.png) *Length of the First Wave = 70* |
| ![](1_wave_length_10.png) *Length of the First Wave = 10* | ![](1_wave_length_70.png) *Length of the First Wave = 70* |  |  |
| Amplitude | Amplitude determines the distance between the highest and the lowest wave peaks. Together with *[Length](#length)*, it sets the wave form. - The minimum value of 0 means the wave is not formed. - *Increasing* the value forms higher waves up to tsunami-like ones. \| ![](1_wave_length_10.png) *Amplitude of the First Wave = 0.3; Length = 10* \| ![](1_wave_amplitude_07.png) *Amplitude of the First Wave = 0.7; Length = 10* \| \|---\|---\| | ![](1_wave_length_10.png) *Amplitude of the First Wave = 0.3; Length = 10* | ![](1_wave_amplitude_07.png) *Amplitude of the First Wave = 0.7; Length = 10* |
| ![](1_wave_length_10.png) *Amplitude of the First Wave = 0.3; Length = 10* | ![](1_wave_amplitude_07.png) *Amplitude of the First Wave = 0.7; Length = 10* |  |  |


## Simulating Physical Interaction


To initiate physical simulation of water, it should have a [water body](../../../principles/physics/bodies/water/index.md) assigned and **enabled**. These options are available only for *water mesh* objects, because of their finite size. If prolongation of the covered area is required, it can be done without the artists exerting additional efforts: *water mesh* objects are simply placed next to each other. However, the waves from the objects do not spread on the adjacent mesh. Sinusoidal [waves](#waves) can be synchronized, if necessary, by changing the sign of the *[Amplitude](#amplitude)* value.


As an option, a body of the water can be **named** in the corresponding field to be identified and handled by UnigineScript.


> **Notice:** *Water mesh* must be exported at the center of world coordinates; otherwise, some effects (for example, caustics) may not be rendered correctly.
