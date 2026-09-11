# Usage Example


The article contains the step-by-step implementation of fading-in/fading-out of an object in the scene by means of the *Tracker* tool:


1. [Create](../../../../editor2/create_import_nodes/index.md#menu) two objects (e.g box primitives: *box1* and *box2*) with the same transformation and having two materials with different *[Albedo](../../../../content/materials/library/mesh_base/index.md#texture_albedo)* textures assigned. ![](box_primitives.png)
2. Make the *box1* object [transparent](../../../../editor2/materials_settings/index.md#blending) by setting *Common -> Transparency -> Preset -> Alpha Blend* for its material. ![](box_transparent.png)
3. Open the *[Tracker](../../../../editor2/tools/tracker/index.md)* tool by choosing *Tools -> Tracker* in the Menu Bar.
4. Click ![](../line_add.png) to add a new track and choose *node -> object -> material -> parameterSlider* in the *Add Parameter* window that opens. ![](add_material_parameter.png)
5. Select the transparent *box1* object in the *Select Node* window that opens. ![](select_box_node.png)
6. Select the *box:transparent* parameter in the *Parameter* field of the *[Track Info](../../../../editor2/tools/tracker/index.md#track_param)* section. ![](tracker_transparent_param.png)
7. Add two key frames for the created track: double-click the track line to [add](../../../../editor2/tools/tracker/basics/index.md#approach_1) a key frame and [set](../../../../editor2/tools/tracker/basics/index.md#edit_key_frame) the following values: ![](key_frame_values.png)

  - For the first key frame, set *Time* = **0** and *Value* = **1**.
  - For the second key frame, set *Time* = **1** and *Value* = **0**.


> **Notice:** If any Z-fighting occurs, you can also adjust *[Rendering Order](../../../../editor2/materials_settings/index.md#order)* for the *box1* object�s material.


The result will be the following:


![](fade_in_out.gif)
