# Field Shoreline


A **Field Shoreline** is an object, specifying [global water](../../../../objects/objects/water/water_object.md) areas where swash zone should be located. Field Shoreline helps to create swashes near the shores and applies the wetness effect on objects near the shoreline.


> **Notice:** - A field shoreline object affects water only if the *FieldShoreline interaction* option is enabled on the *States* tab of the **[water_global_base](../../../../content/materials/library/water_global_base/index.md)** material.
> - The shoreline effect is rendered on the surface of the *[Global Water](../../../../objects/objects/water/water_object.md)* object and requires a high-density wireframe to display correctly. At greater distances tessellation increases triangle sizes which can prevent the *Field Shoreline* from rendering as intended. Setting the *[Geometry Preset](../../../../editor2/settings/render_settings/water_ssr/index.md#geometry_preset)* for *Global Water* to *Ultra* is often enough to resolve this issue. If not, you can switch to *Custom* preset and adjust *Geometry Progression* and *Polygon Size* according to your specific needs.


![](intro.png)

*Swash zone created by using FieldShoreline object.*


> **Notice:** The maximum number of FieldShorelines rendered per frame/bit mask is limited to:
> - **113** (DirectX)


### See also


- The *[FieldShoreline](../../../../api/library/fields/class.fieldshoreline_cpp.md)* class to manage FieldShoreline objects via API
- The `render_field_shoreline_resolution` console command to change the resolution of the texture into which all textures set for the object are rendered


## Adding Field Shoreline


To add a shoreline field in the world via UnigineEditor, do the following:


1. On the Menu bar, choose *Create -> Water -> Field Shoreline*. ![](create.png)
2. Place the *Field Shoreline* in the world so that it intersects *Global Water* object. > **Notice:** Make sure that the *FieldShoreline Interaction* option is enabled for **[water_global_base](../../../../content/materials/library/water_global_base/index.md)** material.
3. Go to the *Node* tab of the *[Parameters](../../../../editor2/node_parameters/index.md)* window, [set up necessary parameters](#editing) and grab the shoreline texture.


> **Notice:** After adding a FieldShoreline object to the scene, you can't see any changes of the global water object because FieldShoreline object doesn't have any default texture.


## Setting Up Field Shoreline


In the *Field Shoreline* section (*[Parameters](../../../../editor2/node_parameters/index.md)* window -> *Node* tab), the following parameters of the shoreline field can be adjusted:


![](settings.png)


### Setting Bit Masks


| Field Mask | A field mask. A bit mask that specifies an area of the shoreline field to be applied to water. The shoreline field will be applied to water only if they have [matching masks](../../../../principles/bit_masking/index.md). |
|---|---|
| Viewport Mask | A viewport mask. A bit mask for rendering the shoreline field into the current viewport. For the shoreline field to be rendered into the viewport, its mask should match the camera viewport mask. |


### Setting Shoreline Parameters


| Size | Size of the shoreline field along the axes in units. A large *FieldShoreline* object provides less detailed swash zones. |
|---|---|
| Texture | Shoreline texture. Grab the texture to fill that field. |


### Grabber Parameters


| Distance | Padding distance (from shore to the beginning of swash). |
|---|---|
| Blur | Blur coefficient (make shoreline smoother). |
| Resolution | Grabbing texture resolution. |
| Grab texture | Grabbing texture button. |
