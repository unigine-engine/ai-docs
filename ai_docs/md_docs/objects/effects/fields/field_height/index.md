# Field Height


A **field height** is an object, specifying [global water](../../../../objects/objects/water/water_object.md) areas where height should be changed (for wakefields, water disturbance, etc.).


Global Water object has heightmap for waves and *FieldHeight* has its own heightmap. Inside the field, the heightmap of the global water is gradually changing from the center of the field height object.


> **Notice:** A field height object will affect water only if the *FieldHeight Interaction* option is enabled on the *States* tab of the `water_global_base` material.


FieldHeight objects work fine with [particle systems](../../../../objects/effects/particles/index.md) and [decal objects](../../../../objects/decals/index.md).


![](field_height.png)

*Water disturbance near the buoy is made by using FieldHeight object.*


> **Notice:** The maximum number of FieldHeights rendered per frame/bit mask is limited to:
> - **113** (DirectX)


### See also


- The *[FieldHeight](../../../../api/library/fields/class.fieldheight_cpp.md)* class to manage FieldHeight objects via API
- The `render_field_height_resolution` and `render_field_precision` console commands


## Adding Field Height


To add a height field in the world via *UnigineEditor*, do the following:


1. On the Menu bar, choose *Create -> Water -> Field Height*. ![](create.png)
2. Place the height field in the world so that it intersects Global Water object. > **Notice:** Make sure that the *FieldHeight interaction* option is enabled for **[water_global_base](../../../../content/materials/library/water_global_base/index.md)** material.
3. Go to the *Field Height* tab of the *[Parameters](../../../../editor2/node_parameters/index.md)* window and [set up necessary parameters](#editing).


> **Notice:** After adding a *Field Height* object to the scene, you can't see any changes of the global water object because *Field Height* object doesn't have any default heightmap texture.


## Setting Up Field Height


In the *Field Height* section (*[Parameters](../../../../editor2/node_parameters/index.md)* window -> *Node* tab), the following parameters of the height field can be adjusted:


![](settings.png)


### Setting Bit Masks


| Field Mask | A *Field* mask. A bit mask that specifies an area of the height field to be applied to water. The height field will be applied to water only if they have [matching masks](../../../../principles/bit_masking/index.md). |
|---|---|
| Viewport Mask | A *Viewport* mask. A bit mask for rendering the height field into the current viewport. For the height field to be rendered into the viewport, its mask should match the camera *Viewport* mask. |


### Setting Height Parameters


| Size | Size of the height field along the axes in units. |
|---|---|
| Attenuation | An attenuation factor indicating how much global water object's heights gradually changing from the center of the height field. - The higher the value, the less heights of the *Field Height* will have influence on the heights of the *Global Water* object. |
| Power | Power parameter is a multiplier for *FieldHeight* heightmap texture values. - The higher the value, the more heights of the *Field Height* will have influence on the heights of the *Global Water* object. |
| Order | Rendering order of the *Field Height*. This parameter is used to properly apply fields with mixed [blend modes](#blend_mode). |
| Blend Mode | Bending mode of the *Field Height*. Available values are Additive, Multiplicative. > **Notice:** The [Attenuation](#attenuation) parameter is interpreted depending on the selected blending mode: > - It is used as a multiplier for the Additive mode. > - *lerp(1.0f, value, attenuation)* is used for the Multiplicative mode. |
| Texture | Heightmap R16 or R32F (1-channeled) texture (controlled by the `render_field_precision` console command). Heightmap texture is used to create an additional height displacement for water surface. |
