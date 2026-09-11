# Setting Up Materials


The multi-purpose *[Parameters](../../editor2/interface/index.md#parameters)* window provides access to all available parameters of the selected material.


![](material_parameters.png)

*Parameters Window with Material Settings*


> **Notice:** If the window isn't opened, choose *Windows -> Add Parameters* in the main menu.


Via this window, you can change a name of the selected material, set up its [transparency](#blending), rendering into the [viewport](#viewport_mask), rendering of [shadows](#cast_shadow), specify [states](#states_tab), [textures](#textures_tab), and [parameters](#parameters_tab) of the material.


Materials can be created by inheriting from the [base materials](../../content/materials/index.md#base_materials) or via [Material Editor](../../content/materials/graph/index.md).


> **Notice:** - Only [user materials](../../content/materials/index.md#user_materials) can be modified via this window. Settings of [base](../../content/materials/index.md#base_materials) and [manual](../../content/materials/index.md#manual_internal_materials) materials are read-only.
> - All changes to materials are saved automatically as you make them.


### Multi-Selection Editing


As well as for [nodes](../../editor2/node_parameters/index.md#multi_selection_edit), UNIGINE Editor allows multi-selection editing for materials. Select several materials in the [Materials Hierarchy](../../editor2/materials_settings/organizing_materials/index.md) window and tweak the required settings. For example, you can specify [transparency](#blending) options for several materials at once and then adjust other settings of each particular material (e.g., specify albedo color, roughness, transparency multiplier and so on).


The selected user materials inherited from the different base materials can also be edited: only settings that are common for all the selected materials will be visible in the *Parameters* window.


## Preview Panel and Material Name


The selected material is shown as applied to a selected object in the **Preview Panel**. You can change the display object and rotate the it with a mouse, holding the left button pressed.


![](preview_panel.gif)

*Displaying Materials in Preview Panel*


A name of the selected material is displayed to the left of the Preview Panel. It is editable, so you can [rename](../../editor2/materials_settings/organizing_materials/index.md#rename_material) the material.


## Common Tab


> **Notice:** The display of the material parameters and options depends on the material type: some states and options of the materials created via [Material Editor](../../content/materials/graph/index.md) are configured via the Material Editor window.


The **Common** tab contains common material settings. These settings are the same for almost all materials except the *[water_global_base](../../content/materials/library/water_global_base/index.md)* and *water_mesh_base* ones.


![](common_tab.png)

*CommonTab*


### Transparency


> **Notice:** The [water-related materials](../../content/materials/library/water_global_base/index.md) don't require transparency settings as water is always rendered as a transparent object.


This section contains transparency settings:


| Preset | [Blending](../../principles/render/blending/index.md) presets. One of the following can be selected: - Opaque - Alpha test - Alpha blend - Additive - Multiplicative - Custom |
|---|---|
| Src | Option used to scale the source color (the color of an overlaying material). Available only when **Custom** preset is selected. |
| Dest | Option used to scale the destination color (the color of an obscured material). Available only when **Custom** preset is selected. |
| Depth Write | Toggles writing in the depth buffer for the material on and off. This option can be used for transparent objects to prevent them from obstructing the others. With this option enabled the inner part of a transparent object won't be rendered if the outside surface was rendered first. The same can happen to a concave object. |
| Transparent Order | The point of the frame at which transparent surfaces with this material are rendered: - **Before SSR** � the default: the surface takes part in screen-space reflections and receives all post effects. - **Before Post** � the surface is invisible to SSR and receives tonemapping and TAA. - **After Post** � the surface is drawn after the whole post chain, so post effects never touch it. Suitable for overlays, HUD and in-world tooltips. |


### Options


This section contains common material options:


| Rendering Order | Sort order used when rendering transparent objects (objects that are assigned materials with the *Alpha Blend, Additive*, and *Multiplicative* presets). Objects with the *lowest* order numbers are rendered first, and objects with the *highest* order numbers are rendered last. |
|---|---|
| Shadow Mask | A [shadow mask](../../principles/bit_masking/index.md#shadow_mask) of the material. A surface, having this material assigned, casts shadows from a light source, if its surface and material shadow masks match the [shadow mask](../../objects/lights/parameters/index.md#shadow_mask) of a light source (one bit at least). |
| Viewport Mask | A [viewport mask](../../principles/bit_masking/index.md#viewport) of the material. A surface, having this material assigned, is rendered into a viewport, if its surface and material viewport masks match the viewport mask of the camera (one bit at least). |
| Two Sided | Rendering of polygons, to which the material is applied, two times per lighting pass. The option should be disabled to gain performance, if there is no need to render both sides of the polygons. |
| Depth Test | Depth testing for the material. This option can be used to make the object visible, when occluded by other objects (e.g. a character behind a wall). |
| Cast Proj and Omni Shadow | Render polygons, to which the material is applied, casting shadows from *Omni* and *Proj* light sources. |
| Cast World Shadow | Render polygons, to which the material is applied, casting shadows from *World* light sources. |


## States Tab


The **States** tab contains a set of flags that are used for a shader corresponding to the material.


![](states_tab.png)

*States Tab*


A set of states can differ depending on the base material. States define a set of textures and parameters of the material. Detailed descriptions of states for each particular material are available in the corresponding article of the [Built-In Base Materials](../../content/materials/library/index.md) section.


## Textures Tab


The **Textures** tab contains paths to textures used by the material.


![](textures_tab.png)

*Textures Tab*


A set of textures can differ depending on the base material and the [states](#states_tab) enabled for the selected material. Detailed descriptions of textures for each particular material are available in the corresponding article of the [Built-In Base Materials](../../content/materials/library/index.md) section.


The following settings are available for each texture:


![](texture_settings.png)


| Clamp X / Clamp Y / Clamp Z | Disable tiling of the texture along the specified axis. |
|---|---|
| Anisotropy | Apply anisotropic filtering to the texture. |
| Texture Streaming Density Multiplier | Multiplier adjusting the distance at which the texture mipmaps are rendered. |


## Parameters Tab


The **Parameters** tab contains parameters associated with the available states.


![](parameters_tab.png)

*ParametersTab*


For every parameter, there are two modes available. They can be selected by clicking the Gear icon next to the relevant parameter:


![](tex_coords_transform_edit_button.png)


- **Simple** mode provides adjustment of the default parameter value.
- **Expression** mode allows using expressions in the parameter field. The type of the expression result must be one of the following: A number of aliases to variables and functions are available from the expression, for convenience:

  - **[int](../../code/uniginescript/language/data_types.md#int)** � an integer value. With the input value of 4, the result will be equal to **vec4(4.0f, 4.0f, 4.0f, 4.0f)**
  - **[long](../../code/uniginescript/language/data_types.md#long)** � a long integer. With the input value of 2L, the result will be equal to **vec4(2.0f, 2.0f, 2.0f, 2.0f)**
  - **[float](../../code/uniginescript/language/data_types.md#float)** � a floating point value. With the input value of 3.0f, the result will be equal to **vec4(3.0f, 3.0f, 3.0f, 3.0f)**
  - **[double](../../code/uniginescript/language/data_types.md#double)** � a double value. With the input value of 7.4, the result will be equal to **vec4(7.4, 7.4, 7.4, 7.4)**
  - **[vec3](../../code/uniginescript/language/data_types.md#vec3)** � a vector of three float components. With the input value of vec3(2.0f, 2.0f, 2.0f), the result will be equal to **vec4(2.0f, 2.0f, 2.0f, 1.0f)**
  - **[vec4](../../code/uniginescript/language/data_types.md#vec4)** � a vector of four float components. With the input value of vec4(2.0f, 2.0f, 2.0f, time), the result will change each frame due to [**time**](#expression_time).
  - **[dvec3](../../code/uniginescript/language/data_types.md#dvec3)** � a double point value. With the input value of dvec3(2.0, 2.0, 2.0), the result will be equal to **vec4(2.0f, 2.0f, 2.0f, 1.0f)**
  - **[dvec4](../../code/uniginescript/language/data_types.md#dvec4)** � a double point value. With the input value of dvec4(2.0, 2.0, 2.0, 2.0), the result will be equal to **vec4(2.0f, 2.0f, 2.0f, 2.0f)**

  - **ifps** � a global variable referring to the *[engine.game.getIFps()](../../api/library/engine/class.game_cpp.md#getIFps_float)* function.
  - **time** � a variable referring to the *[engine.game.getTime()](../../api/library/engine/class.game_cpp.md#getTime_float)* function.
  - **noise(float pos, float size, int frequency)** � a function referring to the *[engine.game.getNoise1()](../../api/library/engine/class.game_cpp.md#getNoise1_float_float_int_float)* function.
  - **random(float from, float to)** � a function referring to the *[engine.game.getRandomFloat()](../../api/library/engine/class.game_cpp.md#getRandomFloat_float_float_float)* function.
  - **getNode()** � a function returning a current node pointer.
  - **getParent()** � a function returning a parent node pointer.
  - **getNumChildren()** � a function returning the number of children nodes.
  - **getChild(int num)** � a function returning a node child by its number.
  - **getState(string name)** � a function returning a specified [state of the current material](../../api/library/rendering/class.material_cpp.md#getState_int_int).
  - **getParameter*(string name)** � a function returning the value of a specified [parameter of the current material](../../api/library/rendering/class.material_cpp.md#getParameterFloat_cstr_float).


The *[UV Transform](../../content/materials/library/mesh_base/index.md#texture_transform)* parameter additionally has the **Animated** mode, which allows procedural animation of texture coordinates by fine-tuning the following values:


- **Scale X** � the first component of the vector defining the scale along the X axis.
- **Scale Y** � the second component of the vector defining the scale along the Y axis.
- **Frequency** � the frequency of the circular motion.
- **Amplitude** � the maximum extent of the circular motion, in pixels.
- **Velocity** � the velocity of the constant linear offset, in pixels per frame.
- **Angle** � the direction of the constant linear offset, in degrees.


A set of parameters can differ depending on the base material and [states](#states_tab) enabled for the selected material. Detailed description of parameters for each particular material is available in the corresponding article of the [Built-In Base Materials](../../content/materials/library/index.md) section.


## Video Tutorial: Materials
