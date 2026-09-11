# Water


Unigine provides realistic water with complex behavior and ability to interact with rigid bodies. It can represent different types of water basins, from oceans, seas, natural lakes and streams to mud, mires, slush and other types of liquids.


In Unigine, water is implemented as 2 types of objects:


- [![](water.png)](../../../objects/objects/water/water_object.md) � **[Global Water](../../../objects/objects/water/water_object.md)** is an infinitely spread mesh with auto-tessellation that represents a boundless ocean (the wireframe of the water is not scaled; regardless of the camera position it always stays the same). **[Global Water](../../../objects/objects/water/water_object.md)** gives you precise control over the wave spectrum. Unique characteristics of each wave system can be set independently through spectral parameters, wave direction, length, amplitude, and the shape factor of waves at run time via API (as all the data is available on the CPU side). It is optimized so the GPU is not overloaded. Features:

  - Realistic real-time water simulation based on fast implementation of Gerstner waves model
  - Support for the underwater mode.
  - The physical interaction with scene objects is not available.
  - Limited to a *single water level*: the filling level of water always remains the same. So, if you need to create, for example, mountain lakes or water flows with height difference, you should use a **[water mesh](../../../objects/objects/water/water_mesh.md)**.
- [![](water.png)](../../../objects/objects/water/water_mesh.md) � **[Water Mesh](../../../objects/objects/water/water_mesh.md)** is a loaded mesh used to create finite basins of an arbitrary form. Features:

  - Support for buoyancy simulation (it can have a [body](../../../principles/physics/bodies/water/index.md) assigned).
  - The underwater mode is not available for the water mesh.
  - *Multiple water levels*: you can create, for example, a water flow with height difference located above the sea level (i.e. the filling level of global water).


### See also


- The *[water_global_base](../../../content/materials/library/water_global_base/index.md)* material
- The *[water_mesh_base](../../../content/materials/library/water_mesh_base/index.md)* material


## Water Surfaces


Both the global water and the water mesh have a surface approximating optical and dynamic behavior of water (the *Surfaces* section of the *[Parameters](../../../editor2/node_parameters/index.md)* window):


![](object_water_surfaces.png)


The *surface (ObjectWaterMesh)* or *water_surface (ObjectWaterGlobal)* adds the following effects:


- Surface waves � [geometrical waves](../../../objects/objects/water/water_mesh.md#waves) and rippling produced by surface displacement according to the normal map (see the *[water_mesh_base](../../../content/materials/library/water_mesh_base/index.md#texture_normal_detail)* material and *[global water](../../../objects/objects/water/water_object.md#detail)*), as well as waves conditioned by the [physical interaction](../../../objects/objects/water/water_mesh.md#water_physics) with objects (in case the water mesh is used).
- Reflection � specular reflection of direct sunlight and skylight from the water surface. Reflection can be:

  - *Dynamic*. In this case, water reflections are set up by adjusting parameters in the *[Reflection](../../../objects/objects/water/water_object.md#roughness)* field of the *Parameters* tab of the *Materials* window.
  - *Static*. In this case, water reflections are baked into a cube map that should be specified in the *Reflection* field of the *Textures* tab of the *Materials* window.
- Fresnel effect � increase or decrease of water surface reflectance depending on the angle of the camera. In real life when looking at the water straight from above, it is transparent and non-reflective. When looking at the surface from a distance, the view angle becomes smaller and the amount of reflection increases until it seems completely non-transparent.
- [Refraction](../../../objects/objects/water/water_object.md#refraction_scale) as light passes through air-water boundary.
- [Foam](../../../objects/objects/water/water_object.md#foam), spray or bubbles.
- White caps in water. They look like foam, except that they are spread all over the water surface.


## Water Interaction with Field Spacer


Some areas of the water surface can be cut out by using a *[Field Spacer](../../../objects/effects/fields/field_spacer/index.md)*. It allows you to dynamically adapt the water surface to an object placed into water. For example, you can set a field spacer for a boat, so that water is not rendered inside this boat.


If a material assigned to a water object [allows](../../../objects/objects/water/water_object.md#field_spacer_enabled) for interaction with *[FieldSpacer](../../../api/library/fields/class.fieldspacer_cpp.md)* objects, you can specify the *field mask* that specifies an area of the *Field Spacer* node to be applied to water. This mask must match the mask set for the *Field Spacer* node.
