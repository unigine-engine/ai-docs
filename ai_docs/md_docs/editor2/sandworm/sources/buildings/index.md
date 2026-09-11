# Buildings Customization and Parameters


This article reviews the main concepts of the building composition to give a deeper understanding of how the assets should be prepared.


### See Also


- [Example](../../../../editor2/sandworm/workflow/buildings/index.md) of creating a *Building* object
- [Filter parameters](../../../../editor2/sandworm/sources/index.md#filters) description
- The [Procedural Generation Assets](../../../../sdk/addons/procedural_generation_assets/index.md) add-on containing ready-to-use materials and textures to customize buildings


## Main Concepts


For the sake of the generation of buildings, we differentiate between the following two types of buildings:


- **Single-story** buildings, which have only one floor
- **Multi-story** buildings, which have two or more floors


![](buildings.png)

*Concept of single-story and multi-story buildings*


- *Underground Basement* is the part of the basement that goes down under the terrain level. This part is required when a building is generated on uneven terrain and would otherwise partially hover above the ground. Its height is controlled by the [*Underground Basement Height*](#underground_height) value.
- The *Basement* height is defined by the *[Basement Height](#basement_height)* value and is 0.7 meter high above terrain by default.
- The *Ground Floor* height is defined by the [Row Size](#row_size) value and is 3 meters high by default.
- Single-story buildings don't require any texture for upper floors, while the texture for the basement is mandatory, as it is an anchor for all other textures in a set.


### Buildings Texturing


UNIGINE provides a set of built-in materials for generated buildings: they are inherited from *[mesh_base](../../../../content/materials/library/mesh_base/index.md)* and named according to the [rules](#materials_naming). You can also create your custom textures and set up materials. However, your textures should meet a set of requirements described below.


Four types of textures should be prepared for a building: a texture for the basement, a texture for the wall with windows (and sometimes doors), a texture for the solid wall, and a texture for the roof. The *UV* map of each [part of the building](#building_elements) depends on the size of the wall segment that is shown on the texture.


> **Notice:** Textures for walls differ depending on the part of the building they are applied to: if a texture is applied to *Basement*, it should depict *Basement* and *Underground Basement*.


- For *Underground Basement* and *Basement*, a single texture for a wall is applied. The texture height corresponds to the height of all these parts (in sum), and the texture is stretched vertically to fit this part of the building. ![](building_basement.png) *Texture forUnderground BasementandBasement*
- For the *Ground Floor*, an individual texture is applied. The texture height is applied to the building using the [Row Size](#row_size) value as the floor height. | ![](building_first_floor_0.png) | ![](building_first_floor_1.png) | |---|---| | *Texture with windows forGround Floor* | *Solid texture forGround Floor* |
- For *Upper Floors*, a single texture for a wall with windows is applied. | ![](building_upper_floors_0.jpg) | ![](building_upper_floors_1.jpg) | |---|---| | *Texture with windows forUpper Floors* | *Solid texture forUpper Floors* | There are two parameters � [Rows per Texture](#rows_per_texture) and [Columns per Texture](#columns_per_texture) � that form a grid for this texture. ![Texture Grid](texture_grid.png) The texture for the upper floors with windows is applied wherever possible along the wall from the first floor upward and from the center to the building corners horizontally and is cut according to these imaginary grid lines, creating one surface. Edges are tiled using the solid texture and form another surface.
- For *Roof*, two textures should be applied � for the roof and the ridges. Ridges are used to cover the connection of two roof planes. | *Roof texture* | ![](building_roof_0.png) | |---|---| | *Ridges texture* | ![](building_roof_1.png) | The roof material can be used as is or change the color based on the imagery data. Enabling the [corresponding option](#use_imagery_color) allows multiplying the material albedo by the color taken from the imagery data.


### Materials Naming


> **Notice:** Each material should be inherited from *[mesh_base](../../../../content/materials/library/mesh_base/index.md)*.


For materials to be correctly applied by *Sandworm* to the generated buildings, follow these rules:


- Define a prefix that a group of materials applied to walls (basement, ground floor, and upper floors) will use. You can use the source data material value as the prefix of the material. In this case, the material will be applied automatically to all buildings that have this value assigned. Roof materials also can use a key value of source data as a prefix. In this case, the material will be applied automatically to all roofs that have this value assigned. If your source data don't have material details, you can choose an arbitrary name.
- Materials should use the following name postfixes:

  - ****_basement_sw*** � material for Basement and Underground Basement, a mandatory material which is an anchor for other building materials, except roofs.
  - ****_ground_sw*** � material for the *Ground Floor* wall without doors and windows
  - ****_ground_windows_sw*** � material for the *Ground Floor* wall with doors and windows
  - ****_upper_sw*** � material for the *Upper Floors* wall without doors and windows
  - ****_upper_windows_sw*** � material for the *Upper Floors* wall with doors and windows
  - ****_ridge_face_sw*** � materials for the top part of the upper wall to be applied right below the roof. This type of material is used with [flat, gabled, and hipped roofs](#roof_type) (not with skillion ones).
  - ****_roof_sw*** � material for *Roof*
  - ****_ridges_sw*** � material for the *Roof* ridges connecting the roof sections


The basic set of building materials is available in the `/core/materials/buildings/` folder.


#### Naming Example


Let's assume we have an area with buildings, which can be made of bricks or wood. If we use OSM data with their [specific naming](https://wiki.openstreetmap.org/wiki/Key:building:material), we should use the following prefixes for building materials:


| Building | OSM Value | Material Names |
|---|---|---|
| made of bricks | brick | `brick_basement_sw.mat` `brick_ground_sw.mat` `brick_ground_windows_sw.mat` `brick_upper_sw.mat` `brick_upper_windows_sw.mat` `brick_ridge_face_sw.mat` |
| made of wood | wood | `wood_basement_sw.mat` `wood_ground_sw.mat` `wood_ground_windows_sw.mat` `wood_upper_sw.mat` `wood_upper_windows_sw.mat` `wood_ridge_face_sw.mat` |


Then, the roofs of these buildings can be covered with tiles, metal, or concrete. According to the OSM [roof material naming](https://wiki.openstreetmap.org/wiki/Key:roof:material), we should name the roof materials as follows:


| Roof | OSM Value | Material Name |
|---|---|---|
| covered with tiles | roof_tiles | `roof_tiles_roof_sw.mat` `roof_tiles_ridges_sw.mat` |
| covered with metal | metal | `metal_roof_sw.mat` `metal_ridges_sw.mat` |
| covered with concrete | concrete | `concrete_roof_sw.mat` `concrete_ridges_sw.mat` |


## Parameters


The following parameters for the *Buildings* object generation are available:


> **Notice:** Every ** Attributes* field is shown only while the matching ** Distribution* parameter is set to *Attribute + Random*; with *Random* selected the field is hidden.


![](buildings_parameters_auto.png)


| Generation Mode | Buildings generation mode. There are two options: - *Auto* � materials and roof types are assigned automatically: the built-in material sets from the `/core/materials/buildings/` folder are applied. Materials from the add-ons are used in *Manual* mode only. - *Manual* � allows configuring materials and roof types. Selecting this mode enables additional parameters. > **Warning:** In *Auto* mode all parameters below except *[Use Imagery Color](#use_imagery_color)* and *[Split Length](#split_length)* are reset to the built-in preset when the generation starts, so the values you set there do not survive it. Switch to *Manual* to keep your own values. |
|---|---|
| Base Material Attributes | The name of the column where the building material is specified, in the source data [Attributes table](../../../../editor2/sandworm/sources/index.md#attributes_table). By default, the corresponding [OpenStreetMap](https://www.openstreetmap.org/) key is used. You can replace it or add another key using a comma, if necessary. |
| Floor Attributes | The name of the column where the number of floors is specified, in the source data [Attributes table](../../../../editor2/sandworm/sources/index.md#attributes_table). |
| Roof Type Attributes | The name of the column where the roof shape is specified, in the source data [Attributes table](../../../../editor2/sandworm/sources/index.md#attributes_table). By default, the corresponding [OpenStreetMap](https://www.openstreetmap.org/) key is used. You can replace it or add another key using a comma, if necessary. |
| Roof Height Attributes | The name of the column where the roof height is specified, in the source data [Attributes table](../../../../editor2/sandworm/sources/index.md#attributes_table). By default, the corresponding [OpenStreetMap](https://www.openstreetmap.org/) key is used. You can replace it or add another key using a comma, if necessary. |
| Roof Unit Size (m) | The size of one side of the square area to which the texture is applied (i.e. one tile). The default value is 6 meters, the range is 0.1 to 1000. |
| Use Imagery Color | If disabled, the color from the roof material is used. If enabled, the color from the *Imagery* source is used as the roof color. > **Notice:** To use the imagery color, the roof material should have the [Vertex Color state](../../../../content/materials/library/mesh_base/index.md#option_vertex_color) enabled with Vertex Color Albedo set to RGB. |
| Roof Material Attributes | The name of the column where the roof material is specified, in the source data [Attributes table](../../../../editor2/sandworm/sources/index.md#attributes_table). By default, the corresponding [OpenStreetMap](https://www.openstreetmap.org/) key is used. You can replace it or add another key using a comma, if necessary. |
| Split Length (km) | The size of the grid cell by which the generated geometry will be divided. The geometry of each cell is represented as a separate *[Mesh Static](../../../../objects/objects/mesh/index.md)* object. If the specified value is greater than or equal to both side lengths of the *[Export Area](../../../../editor2/sandworm/generation/export_area/index.md)* bounding box, a single *Mesh Static* object is generated. For example, if you specify 100 and have a 1000x1000 km area, the buildings are generated as up to 100 separate *Mesh Static* objects (a 10x10 grid), 100x100 km each � a mesh is created only for a cell that contains buildings. The default value is 100 km. |
| Random Seed | Seed of the random number generator used to generate buildings. The same value always gives the same result: the number of floors, the choice of materials and the roof parameters. Change it to get another variant of the same set of buildings. The default value is 0. |
| Min Visibility | Minimum visibility distance from the camera at which generated objects (*Mesh Static*) start to appear on the screen. By default, this value is -inf. |
| Max Visibility | Maximum visibility distance at which generated objects (*Mesh Static*) are no longer fully visible: they can either disappear entirely or start to fade out. By default, this value is inf. |
| Min Fade | Minimum fade distance, over which generated objects (*Mesh Static*) fade in until they are entirely visible. Along this distance, the engine automatically interpolates the level of detail from Alpha of 0.0 (entirely invisible) to 1.0 (entirely visible). Fading-in starts when the camera has reached the [minimum visibility distance](#min_visibility) and is in the full visibility range. |
| Max Fade | Maximum fade distance, over which generated objects (*Mesh Static*) fade out until they are entirely invisible. Fading-out starts when the camera has reached the [maximum visibility distance](#max_visibility) and is out of the full visibility range. |


In addition to the basic parameters that are available for *Auto* generation, the following parameters become available in the *Manual* generation mode:


| **Base Parameters:** ![Base Building Parameters](buildings_base_parameters.png) Base parameters fine-tune the look of the building walls. |  |  |  |  |  |  |  |  |  |
|---|---|---|---|---|---|---|---|---|---|
| Base Material Distribution | - *Attribute + Random* � the value is taken from Attribute. If Attribute contains no value, the material is applied randomly. - *Random* � materials are applied randomly from the materials that *[Random Material List](#random_material_list)* contains. |  |  |  |  |  |  |  |  |
| Random Material List | The list of materials that will be applied to generated buildings. Only the base material (`*_basement_sw`) of each group is displayed. Other materials from this group are referred to using the prefix, which should be identical for all materials of a group. The number right to each material specifies its frequency. The toggle to the left of each material allows enabling/disabling it. |  |  |  |  |  |  |  |  |
| Column Size (m) | Width of one texture column, in meters. A texture [cell](#grid) is mapped to this width on the building wall. |  |  |  |  |  |  |  |  |
| Columns per Texture | Number of columns in one texture. This value allows forming a [grid](#grid) for a more precise texture mapping. The texture mapped to walls above the ground floor is split into a grid in order to be cut properly, avoiding such visual artifacts as a part of a window. |  |  |  |  |  |  |  |  |
| Row Size (m) | Height of one row, in meters. In fact, this is a floor height. A texture [cell](#grid) is mapped to this height on the building wall. |  |  |  |  |  |  |  |  |
| Rows per Texture | Number of rows in one texture. This value allows forming a [grid](#grid) for a more precise texture mapping. The texture mapped to walls above the ground floor is split into a grid in order to be cut properly, avoiding such visual artifacts as a part of a window. |  |  |  |  |  |  |  |  |
| Floor Number | - *Attribute + Random* � the value is taken from Attribute. If Attribute contains no value, the number of floors is applied randomly from *[Floor Number Range](#floor_number_range)*. - *Random* � number of floors is assigned randomly from *[Floor Number Range](#floor_number_range)*. |  |  |  |  |  |  |  |  |
| Floor Number Range | Minimum and maximum floor number values. A random value from this range will be used as a floor number if no data is available or *[Floor Number](#floor_number)* is set to *Random*. |  |  |  |  |  |  |  |  |
| **Roof Parameters:** ![Roof Parameters](buildings_roof_parameters.png) Roof parameters fine-tune the look of roofs. |  |  |  |  |  |  |  |  |  |
| Roof Type Distribution | - *Attribute + Random* � the value is taken from Attribute. If Attribute contains no value, the roof type is applied randomly from the available *[Roof Types](#roof_type)*. - *Random* � the roof type is assigned randomly from the available *[Roof Types](#roof_type)*. |  |  |  |  |  |  |  |  |
| Roof Type | Type of the roof with a probability multiplier. The following types of roofs are available: \| Flat \| ![Flat roof](roof_flat.jpg) \| \|---\|---\| \| Skillion \| ![Skillion roof](roof_skillion.jpg) \| \| Gabled \| ![Gabled roof](roof_gabled.jpg) \| \| Hipped \| ![Hipped roof](roof_hipped.jpg) \| You can delete the roof types that are not required to exclude them at all; one line always remains in the list. Click the ![Plus](plus.png) button to add a line and select the roof type you need in its drop-down list. > **Notice:** If the same roof type is selected in more than one line, only the lowest of these lines is applied: its probability multiplier replaces the ones above, they are not summed up. Duplicate lines are not saved � the list is rebuilt with a single line per roof type the next time the object parameters are opened. A building whose footprint is not rectangular always gets a flat roof; the other roof types are unavailable for it. | Flat | ![Flat roof](roof_flat.jpg) | Skillion | ![Skillion roof](roof_skillion.jpg) | Gabled | ![Gabled roof](roof_gabled.jpg) | Hipped | ![Hipped roof](roof_hipped.jpg) |
| Flat | ![Flat roof](roof_flat.jpg) |  |  |  |  |  |  |  |  |
| Skillion | ![Skillion roof](roof_skillion.jpg) |  |  |  |  |  |  |  |  |
| Gabled | ![Gabled roof](roof_gabled.jpg) |  |  |  |  |  |  |  |  |
| Hipped | ![Hipped roof](roof_hipped.jpg) |  |  |  |  |  |  |  |  |
| Roof Height Distribution | - *Attribute + Random* � the value is taken from Attribute. If Attribute contains no value, the roof height is taken randomly from the user-defined *[height range](#roof_type_height)* for the corresponding roof type. - *Random* � the roof height is assigned randomly from the available *[height range](#roof_type_height)* for the corresponding roof type. |  |  |  |  |  |  |  |  |
| Roof Type Height | The height range (minimum and maximum possible height) of the corresponding roof type. A random value is taken from this range, if necessary. The height value for the flat roof defines the height of the roof parapet. The range is 0.01 to 99, and the lowest value you can set depends on the roof type: 0.01 for *Flat* and 0.5 for the other types. > **Notice:** If the same roof type is selected in more than one line, only the lowest of these lines is applied: its height range replaces the ones above. Duplicate lines are not saved � the list is rebuilt with a single line per roof type the next time the object parameters are opened. |  |  |  |  |  |  |  |  |
| Roof Material Distribution | - *Attribute + Random* � the value is taken from Attribute. If Attribute contains no value, the roof material is taken from the *[material](#roof_type_material)* set for the corresponding roof type. - *Random* � the roof material is assigned as *[set](#roof_type_material)* for the corresponding roof type. |  |  |  |  |  |  |  |  |
| Roof Type Material | The material set for the corresponding roof type. You can enable or disable materials, to avoid incorrect use of a material for an unsuitable type of roof, for example, disable tiles for flat roofs because it's nonsense. > **Notice:** If the same roof type is selected in more than one line, only the lowest of these lines is applied: its material set replaces the ones above. Duplicate lines are not saved � the list is rebuilt with a single line per roof type the next time the object parameters are opened. |  |  |  |  |  |  |  |  |
| **Common Parameters:** ![Common Parameters](buildings_common_parameters.png) Common parameters fine-tune the look of the basement, visibility of buildings, and splitting of the Buildings object into sectors. |  |  |  |  |  |  |  |  |  |
| Underground Basement Height (m) | The height of the underground basement part. Used for uneven ground surfaces where buildings partially hover above the ground. The default value is 3 meters. You can set this value to 0 if you don't require it to be displayed. |  |  |  |  |  |  |  |  |
| Basement Height (m) | The height of the basement above the terrain level. The default value is 0.7 meter. You can set this value to 0 if you don't require it to be displayed. |  |  |  |  |  |  |  |  |
