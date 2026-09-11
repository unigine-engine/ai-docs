# Unigine.Material Class (CS)


This class is used to create [materials](../../../principles/world_structure/index.md#materials) that are assigned to each node (or each surface of the object) and define what the nodes look like. Materials implement the [shaders](../../../principles/world_structure/index.md#material_shaders) and control what [options](../../../principles/world_structure/index.md#material_options), [states](../../../principles/world_structure/index.md#material_states), [parameters](../../../principles/world_structure/index.md#material_parameters) and [textures](../../../principles/world_structure/index.md#material_textures) are used to render the node during the [rendering passes](../../../principles/render/sequence/index.md).


The materials are referenced via [GUID](../../../content/materials/inheritance.md#material_guid). Only the [manual](../../../content/materials/index.md#manual_internal_materials) materials can be referenced via name.


The material name (taken from the file name) defines how the material is displayed in Materials Editor (the materials hierarchy, the nodes surface editor).


### Namespaces


Materials can be separated into different *namespaces* to avoid the engine and the [user](../../../content/materials/index.md#user_materials) materials name collision. Default engine and editor materials have their own namespaces (`Unigine` and `Editor` respectively). For example, *Unigine::mesh_base* or *Editor::brush_draw_post*.


You can create *custom* namespaces for your materials. The [Material::getNamespaceName()](#getNamespaceName_cstr) method returns the namespace of a material, if it has been assigned to any.


### Getting Parameter And Texture Names


Internal names of the material's textures and parameters are displayed in UnigineEditor tooltips, **clicking on the name of the parameter/texture** (LMB, once) copies an internal name for it to the clipboard, which allows to easily paste it to the code.


![](material_internal_names.png)


### Inheriting Materials


If you are developing a project with a large number of dynamically created and deleted objects, you may experience a sudden drop in performance for slightest unforeseen reasons.


When an object is deleted, all unique materials assigned to it should also be deleted via *DeleteLater()* to free memory. This method checks each material (having **[Material.CanRenderNode](../../...md#canRenderNode_int)* == **true***) to see if it is also used by other objects (i.e., all other world objects are checked individually). According to the policy, all checked materials will be deleted in the next swap stage of the main loop. If there are thousands of objects in the world, you'll get a spike.


To avoid a spike you need to use a right pipeline of material inheritance. Don't get a material from another object via *[Object.GetMaterial(surface)](../../../api/library/objects/class.object_cs.md#getMaterial_int_Material)* and call *[Material.Inherit()](../../...md#inherit_Material)* on it. It is better to use *[Object.GetMaterialInherit(surface)](../../../api/library/objects/class.object_cs.md#getMaterialInherit_int_Material)*, which creates a new material instance having its lifetime associated with this object, and you won't have to delete it manually.


Implementation causing a spike:


```csharp
Material mat = obj.GetMaterial(surface);
Material mat_inherited = mat.Inherit();
obj.SetMaterial(mat_inherited, surface);
�
obj.DeleteLater();
mat_inherited.DeleteLater();

```


Recommended implementation:


```csharp
Material mat_inherited = obj.GetMaterialInherit(surface);
�
obj.DeleteLater();

```


### Usage Examples


#### Changing Textures


The first example describes how to inherit a material from a base one, change the material texture, and set [texture flags](../../../api/library/rendering/class.texture_cs.md#SAMPLER_ANISOTROPY_1) for it. We inherit a new material *my_mesh_base_0.mat* from the *mesh_base* material, assign it to the default *material ball* object, change its albedo texture, and set the [SAMPLER_FILTER_POINT](../../../api/library/rendering/class.texture_cs.md#SAMPLER_FILTER_POINT) flag for it.


Create a new component and add the following code into it:


```csharp
// material to be inherited from mesh_base and customized
	Material m;
void Init()
{

	// finding the mesh_base material from the Unigine namespace
        Material mesh_base = Materials.FindManualMaterial("Unigine::mesh_base");
	if(mesh_base){
		// inherit a new material from the mesh_base
		m = mesh_base.Inherit();
            // get the number of the albedo texture of the inherited material
            int num = m.FindTexture("albedo");

            // check if our material is editable and perform modifications
            if (m.IsEditable)
            {
                Log.Message("Material ({0}) is editable.\n", m.FilePath);

                // change albedo texture of the material to core/textures/common/checker_d.texture
                m.SetTexturePath(num, "core/textures/common/checker_d.texture");

                // get current flags, check if point filtering is enabled and display the result in the console
                int flags = m.GetTextureSamplerFlags(num);
                Log.Message("Flags for {0} texture ({1}):{2} \n", m.GetTextureName(num), num, flags);
                Log.Message("FILTER_POINT {0}\n", (flags & Texture.SAMPLER_FILTER_POINT) != 0 ? "enabled" : "disabled");

                // set the FILTER_POINT flag
                m.SetTextureSamplerFlags(num, Texture.SAMPLER_FILTER_POINT);

                // get the flags, check if point filtering is enabled and display the result in the console
                int flagsSet = m.GetTextureSamplerFlags(num);
                Log.Message("Flags for {0} texture ({1}):{2} \n", m.GetTextureName(num), num, flagsSet);
                Log.Message("FILTER_POINT {0}\n", (flagsSet & Texture.SAMPLER_FILTER_POINT) != 0 ? "enabled" : "disabled");
            }

            // saving the material asset to the specified path if it doesn't exist yet
            if (!Materials.FindMaterialByPath("materials/my_mesh_base_0.mat"))
                m.CreateMaterialFile("materials/my_mesh_base_0.mat");

            // assigning the my_mesh_base_0 material to the node if it is an object
            if(node.IsObject)
                (node as Unigine.Object).SetMaterialFilePath("materials/my_mesh_base_0.mat", "*");
            else
                Log.Message("The node is not an object.\n");
	}
}


```


Assign this component to the **template_buildings** node of the default project template, save the world, and click the *Play* button.


As a result you'll see that the albedo texture of the *template_buildings* object has changed and the following text is displayed in the [console](../../../code/console/index.md):


```text
Material (guid://4dfec30f491f753f6e89094db6d3d695e89f9d6f) is editable.
Flags for albedo texture (1):524288000
FILTER_POINT disabled
Flags for albedo texture (1):1048576
FILTER_POINT enabled

```


#### Changing States and Parameters


The second example illustrates how to inherit a material from the [mesh_base](../../../content/materials/library/mesh_base/index.md) and change two parameters affecting the look of reflections.


Create a new component and add the following code into it:


```csharp
void Init()
{

	// finding the mesh_base material
	Material mesh_base = Materials.FindManualMaterial("Unigine::mesh_base");

	// inherit a new material from it
	Material reflector_material = mesh_base.Inherit();

	// set metallness and roughness parameters to make the surface look like a mirror
	// by the name of the parameter
	reflector_material.SetParameterFloat("metalness", 1.0f);

	// or by its id, which is the same
	reflector_material.SetParameterFloat(reflector_material.FindParameter("roughness"), 0.0f);

	// save the material asset to planar_reflector.mat file in the data project folder
	reflector_material.CreateMaterialFile("planar_reflector.mat");


	// assign new reflecting material to the object
	if(node.IsObject)
		(node as Unigine.Object).SetMaterial(reflector_material, "*");
	else
		Log.Message("The node is not an object.\n");
}


```


Assign this component to the **template_buildings** node of the default project template, save the world, and click the *Play* button to see the result.


## Material Class

### Enums

## WIDGET

| Name | Description |
|---|---|
| **EDIT_INT** = 0 | Text widget enabling you to set an integer value. |
| **EDIT_INT2** = 1 | Text widget enabling you to set 2 integer values. |
| **EDIT_INT3** = 2 | Text widget enabling you to set 3 integer values. |
| **EDIT_INT4** = 3 | Text widget enabling you to set 4 integer values. |
| **EDIT_FLOAT** = 4 | Text widget enabling you to set a float or integer value. |
| **EDIT_FLOAT2** = 5 | Text widget enabling you to set 2 float or integer values. |
| **EDIT_FLOAT3** = 6 | Text widget enabling you to set 3 float or integer values. |
| **EDIT_FLOAT4** = 7 | Text widget enabling you to set 4 float or integer values. |
| **TOGGLE** = 8 | Button widget allowing you to enable or disable a certain state. |
| **COMBOBOX** = 9 | ComboBox widget enabling you to select a texture out of available ones. |
| **TEXTURE_ASSET** = 10 | Texture asset widget enabling you to specify a texture. |
| **TEXTURE_RAMP** = 11 | Ramp asset widget enabling you to specify and adjust a 2D Ramp via the dedicated Curve Editor. |
| **ACCORDION** = 12 | Accordion widget enabling you to expand or collapse a set of widgets it contains. |
| **SLIDER** = 13 | Slider widget enabling you to specify and adjust a float or integer value. |
| **COLOR** = 14 | Color widget enabling you to specify a color via a color picker dialog. |
| **UV** = 15 | UV texture asset widget enabling you to specify a UV texture. |
| **MASK24** = 16 | 24-bit [mask](../../../principles/bit_masking/index.md) widget. |
| **MASK32** = 17 | 32-bit [mask](../../../principles/bit_masking/index.md) widget. |

## DATA_TYPE

| Name | Description |
|---|---|
| **OPTION** = 0 | Material option. |
| **STATE** = 1 | Material state. States are flags that are used for a shader corresponding to the material. States define a set of textures and parameters of the material. |
| **PARAMETER** = 2 | Material parameter. |
| **TEXTURE** = 3 | Material texture. |
| **GROUP** = 4 | Material group. |

## TRANSPARENT_ORDER

Point of the rendering sequence at which the surfaces of a transparent (alpha-blend) material are rendered.
| Name | Description |
|---|---|
| **BEFORE_SSR** = 0 | Transparent surfaces are rendered before the SSR (Screen-Space Reflections) pass (*Before SSR*). |
| **BEFORE_POST** = 1 | Transparent surfaces are rendered before the post-processing pass (*Before Post*). |
| **AFTER_POST** = 2 | Transparent surfaces are rendered after the post-processing pass, over the final image (*After Post*). Can be used for UI elements. |

## MATERIAL_ID

Reserved material ID values. A material ID is a runtime index of the row storing the parameters of a material (material mask, feature bits, custom material parameters) in the global GPU buffer. IDs are assigned to materials by the engine on demand; the values below *MATERIAL_ID_RESERVED_NUM* are reserved.
| Name | Description |
|---|---|
| **NONE** = 0 | No material. The buffer row with this ID is zeroed. |
| **SKY** = 1 | Sky. This ID marks sky pixels in the material ID buffers. |
| **RESERVED_NUM** = 2 | Number of reserved material ID values. Materials are assigned IDs starting from this value. |

### Properties

## 🔒︎ bool IsEmpty

The value indicating if an empty shader is used as a vertex shader in the current material.
## 🔒︎ bool IsFileEngine

The value indicating if the material is a core Engine or UnigineEditor material (i.e. required for Engine/Editor operation).
Such materials are stored in the `core`, `editor` and `editor2` folders/packages.

> **Notice:** It is not recommended to delete files of non-core materials (e.g., created by plugins or otherwise) at run-time, as this may affect materials caching and result in a crash.

## 🔒︎ bool IsAutoSave

The value indicating if the material can be saved automatically (automatic material saving is performed, for example, on world saving).
The value is 0 in the following cases:


- The *[canSave()](#canSave_int)* function returns 0 for the material.
- The material is [non-editable](#isEditable_int).
- The material [GUID](../../../api/library/filesystem/class.uguid_cs.md) is not a valid one.


## 🔒︎ bool IsManual

The value indicating if the current material is [manual](../../../content/materials/index.md#manual_internal_materials).
## 🔒︎ bool IsInternal

The value indicating if the current material is [internal](../../../content/materials/index.md#manual_internal_materials).
## 🔒︎ bool IsReflection2D

The value indicating if the material has a 2D reflection texture.
## 🔒︎ bool IsBrush

The value indicating if the material is used for brushes (`*.brush` or `*.basebrush` file extension).
## 🔒︎ bool IsBase

The value indicating if the material is the [base](../../../content/materials/index.md#base_materials) one.
## 🔒︎ bool IsHidden

The value indicating if the material is hidden.
## 🔒︎ bool IsEditable

The value indicating if the material can be edited.
## int ViewportMask

The bit mask for rendering into the viewport. The material is rendered if its mask matches the player's one.
## bool TwoSided

The value indicating if the material is two-sided.
## 🔒︎ bool IsAlphaTest

The value indicating if the material has an alpha test option enabled.
## 🔒︎ bool IsForward

The value indicating if the material is rendered in the forward pass.
## 🔒︎ bool IsDeferred

The value indicating if the material is rendered in the deferred pass.
## 🔒︎ bool IsWater

The value indicating if the material is rendered in the water pass.
## int Transparent

The transparency type of the material. One of the [TRANSPARENT_*](#TRANSPARENT_NONE) values. If it is set to [TRANSPARENT_NONE](#TRANSPARENT_NONE) or *TRANSPARENT_DEFERRED*, the [source](#setBlendSrcFunc_int_void) and [destination](#setBlendDestFunc_int_void) blending functions are not used.
## Material.TRANSPARENT_ORDER TransparentOrder

The rendering order of transparent surfaces relative to SSR and post-effects. One of the [TRANSPARENT_ORDER_*](#TRANSPARENT_ORDER_BEFORE_SSR) values.
## 🔒︎ int NumTextures

The number of textures used by the material.
## 🔒︎ int NumStates

The number of the material's states.
## 🔒︎ int NumParameters

The number of the material's parameters.
## 🔒︎ string FilePath

The path to the current material file.
## 🔒︎ UGUID FileGUID

The GUID of the current material file.
## 🔒︎ UGUID GUID

The [GUID](../../../content/materials/inheritance.md#material_guid) of the material.
## 🔒︎ int NumChildren

The number of child materials.
## 🔒︎ Material BaseMaterial

The base material of the current material.
## int Order

The [rendering order](#setOrder_int_void) of materials, in the range from -128 to 127. The higher the rendering order, the lower the rendering priority (the material with the -128 order is rendered first).
## int OrderClouds

The rendering order of transparent surfaces relative to clouds.
Takes effect only when the render_clouds_transparent_order console variable is set to 2 (Sort Transparent). One of the [*ORDER_CLOUDS_**](#ORDER_CLOUDS_DEFAULT) values.


> **Notice:** To render a transparent surface behind clouds, [Depth Test](#isDepthTest_int) should be disabled for the material, otherwise the surface will be rendered in front of clouds regardless of the OrderClouds value.

## bool DepthTest

The value indicating if depth testing is enabled for the material. This option can be used to render certain objects, that are behind other ones.
## int ShadowMask

The shadow mask of the material.
For the shadow to be rendered for a light source from an object's surface having this material assigned, this mask must match the following ones (one bit, at least):


- [Shadow mask of the light source](../../../api/library/lights/class.light_cs.md#setShadowMask_int_void)
- [Shadow mask of the surface](../../../api/library/objects/class.object_cs.md#setShadowMask_int_int_void) of the object having this material assigned


## bool CastWorldShadow

The value indicating if an object with the material applied casts shadows from the world light.
## bool CastShadow

The value indicating if an object with the material applied casts shadows.
## 🔒︎ bool IsPreviewHidden

The value indicating if preview in UnigineEditor is disabled for the material. This is used for custom materials (e.g., landscape terrain brushes).
## 🔒︎ bool IsLegacy

The value indicating if the material is a legacy one. A legacy material is a non-ULON base material described in an XML file.
## int BlendSrcFunc

The source [blending](../../../principles/render/blending/index.md) function. One of the [BLEND_*](../../../api/library/rendering/class.renderstate_cs.md#BLEND_NONE) values.
## int BlendDestFunc

The destination [blending](../../../principles/render/blending/index.md) function. One of the [BLEND_*](../../../api/library/rendering/class.renderstate_cs.md#BLEND_NONE) values.
## int BlendAlphaSrcFunc

The source alpha [blending](../../../principles/render/blending/index.md) function. One of the [BLEND_*](../../../api/library/rendering/class.renderstate_cs.md#BLEND_NONE) values.
## 🔒︎ Material Parent

The parent material, or NULL (0) if the current material has no parent.
## 🔒︎ int NumUIItems

The number of UI items. UI items represent material parameters, options, states, textures, and groups in UnigineEditor.
## 🔒︎ string ManualName

The name of the manual material.
## 🔒︎ string NamespaceName

The namespace where this material is defined.
## 🔒︎ uint FeatureBits

The bit mask of screen-space effect features enabled for the material (screen-space shadows, shoreline wetness, motion blur, SSAO, SSR, SSSSS, DOF). The bits are computed from the corresponding material states and are available to shaders in the material parameters structure.
## 🔒︎ uint MaterialID

The runtime ID of the material. The ID is assigned by the engine on demand when the material is first rendered, is unique among live materials, and indexes the row of this material in the global GPU buffer of material parameters. IDs of removed materials are recycled. IDs below **[MATERIAL_ID.RESERVED_NUM](../../...md#MATERIAL_ID_RESERVED_NUM)** are reserved.
### Members

---

## Material ( )

Constructor. Creates a new material instance.
## Material GetChild ( int num )

Returns a child material with a given number.
### Arguments

- *int* **num** - Child material number.

### Return value

The child material smart pointer.
## bool IsParameterExpressionEnabled ( int num )

Returns a value indicating if the value of the specified material parameter is represented by an expression in UnigineScript. Values of certain parameters can be calculated by an arbitrary expression, written in [UnigineScript](../../../code/uniginescript/index.md).
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).

### Return value

true if the value of the specified material parameter is represented by an expression in UnigineScript; otherwise, false.
## void SetParameterExpressionEnabled ( int num , bool enabled )

Sets a value indicating if the value of the specified material parameter is represented by an expression in UnigineScript. Values of certain parameters can be calculated by an arbitrary expression, written in [UnigineScript](../../../code/uniginescript/index.md).
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).
- *bool* **enabled** - true to enable setting the values of the specified material parameter by an expression in UnigineScript; false - to disable.

## bool IsParameterOverridden ( int num )

Returns a value indicating if a given parameter is overridden.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).

### Return value

true if the given parameter is overridden; otherwise, false.
## bool IsParameterInt ( int num )

Returns a value indicating if the parameter with the specified number is an integer-type parameter.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).

### Return value

true if the parameter with the specified number is an [integer-type parameter](#PARAMETER_ARRAY_INT); otherwise, false.
## bool IsParameterFloat ( int num )

Returns a value indicating if the parameter with the specified number is a float-type parameter.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).

### Return value

true if the parameter with the specified number is an [float-type parameter](#PARAMETER_ARRAY_FLOAT); otherwise, false.
## float GetParameterFloat ( string name )

Returns a value of a float parameter with the specified [name](#copy_name). A 0 value returned by this method does not necessarily mean the value of the parameter, as you'll also get 0 in case the **parameter with the given name does not exist**. To check whether the parameter exists use **[FindParameter()](../../...md#findParameter_cstr_int)**. You should also be aware that states, parameters, and textures can be ignored in case [conditions](../../../code/formats/materials_formats/ulon_materials/states.md) they depend on are not met. To check conditions call **[CheckParameterConditions()](../../...md#checkParameterConditions_int_int)**.
### Arguments

- *string* **name** - [Parameter name](#copy_name).

### Return value

Float parameter value.
## vec2 GetParameterFloat2 ( string name )

Returns a value of a [*FLOAT2*](#PARAMETER_FLOAT2) parameter with the specified [name](#copy_name).
### Arguments

- *string* **name** - [Parameter name](#copy_name).

### Return value

Parameter value as a [*vec2*](../../../api/library/math/class.vec2_cs.md) vector.
## vec3 GetParameterFloat3 ( string name )

Returns a value of a [*FLOAT3*](#PARAMETER_FLOAT3) parameter with the specified [name](#copy_name).
### Arguments

- *string* **name** - [Parameter name](#copy_name).

### Return value

Parameter value as a [*vec3*](../../../api/library/math/class.vec3_cs.md) vector.
## vec4 GetParameterFloat4 ( string name )

Returns a value of a [*FLOAT4*](#PARAMETER_FLOAT4) parameter with the specified [name](#copy_name).
### Arguments

- *string* **name** - [Parameter name](#copy_name).

### Return value

Parameter value as a [*vec4*](../../../api/library/math/class.vec4_cs.md) vector.
## int GetParameterInt ( string name )

Returns a value of an integer parameter with the specified [name](#copy_name). A 0 value returned by this method does not necessarily mean the value of the parameter, as you'll also get 0 in case the **parameter with the given name does not exist**. To check whether the parameter exists use **[FindParameter()](../../...md#findParameter_cstr_int)**. You should also be aware that states, parameters, and textures can be ignored in case [conditions](../../../code/formats/materials_formats/ulon_materials/states.md) they depend on are not met. To check conditions call **[CheckParameterConditions()](../../...md#checkParameterConditions_int_int)**.
### Arguments

- *string* **name** - [Parameter name](#copy_name).

### Return value

Integer parameter value.
## ivec2 GetParameterInt2 ( string name )

Returns a value of a [*INT2*](#PARAMETER_INT2) parameter with the specified [name](#copy_name).
### Arguments

- *string* **name** - [Parameter name](#copy_name).

### Return value

Parameter value as an [*ivec2*](../../../api/library/math/class.ivec2_cs.md) vector.
## ivec3 GetParameterInt3 ( string name )

Returns a value of a [*INT3*](#PARAMETER_INT3) parameter with the specified [name](#copy_name).
### Arguments

- *string* **name** - [Parameter name](#copy_name).

### Return value

Parameter value as an [*ivec3*](../../../api/library/math/class.ivec3_cs.md) vector.
## ivec4 GetParameterInt4 ( string name )

Returns a value of a [*INT4*](#PARAMETER_INT4) parameter with the specified [name](#copy_name).
### Arguments

- *string* **name** - [Parameter name](#copy_name).

### Return value

Parameter value as an [*ivec4*](../../../api/library/math/class.ivec4_cs.md) vector.
## int GetParameterArraySize ( int num )

Returns the number of elements in the array parameter with the specified number.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).

### Return value

Number of elements of the specified array parameter.
## bool IsParameterArray ( int num )

Returns a value indicating if the parameter with the specified number is an array-type parameter, i.e., one of the following:


- [PARAMETER_ARRAY_FLOAT](#PARAMETER_ARRAY_FLOAT)
- [PARAMETER_ARRAY_FLOAT2](#PARAMETER_ARRAY_FLOAT2)
- [PARAMETER_ARRAY_FLOAT4](#PARAMETER_ARRAY_FLOAT4)
- [PARAMETER_ARRAY_INT](#PARAMETER_ARRAY_INT)
- [PARAMETER_ARRAY_INT2](#PARAMETER_ARRAY_INT2)
- [PARAMETER_ARRAY_INT4](#PARAMETER_ARRAY_INT4)


### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).

### Return value

true if the parameter is an array-type parameter; otherwise, false.
## void GetParameterArray ( int num , float[] OUT_values )

Returns a value of the array parameter (type: [*PARAMETER_ARRAY_FLOAT*](#PARAMETER_ARRAY_FLOAT)) with the specified number and puts it to the specified buffer array.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).
- *float[]* **OUT_values** - Buffer array to store parameter values. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void SetParameterArray ( int num , float[] values )

Sets a value of the array parameter (type: [*PARAMETER_ARRAY_FLOAT*](#PARAMETER_ARRAY_FLOAT)) with the specified number using the specified array.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).
- *float[]* **values** - Array of values to be set.

## void GetParameterArray ( int num , vec2[] OUT_values )

Returns a value of the array parameter (type: [*PARAMETER_ARRAY_FLOAT2*](#PARAMETER_ARRAY_FLOAT2)) with the specified number and puts it to the specified buffer array.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).
- *vec2[]* **OUT_values** - Buffer array to store parameter values. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void SetParameterArray ( int num , vec2[] values )

Sets a value of the array parameter (type: [*PARAMETER_ARRAY_FLOAT2*](#PARAMETER_ARRAY_FLOAT2)) with the specified number using the specified array.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).
- *vec2[]* **values** - Array of values to be set.

## void GetParameterArray ( int num , vec4[] OUT_values )

Returns a value of the array parameter (type: [*PARAMETER_ARRAY_FLOAT4*](#PARAMETER_ARRAY_FLOAT4)) with the specified number and puts it to the specified buffer array.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).
- *vec4[]* **OUT_values** - Buffer array to store parameter values. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void SetParameterArray ( int num , vec4[] values )

Sets a value of the array parameter (type: [*PARAMETER_ARRAY_FLOAT4*](#PARAMETER_ARRAY_FLOAT4)) with the specified number using the specified array.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).
- *vec4[]* **values** - Array of values to be set.

## void GetParameterArray ( int num , int[] OUT_values )

Returns a value of the array parameter (type: [*PARAMETER_ARRAY_INT*](#PARAMETER_ARRAY_INT)) with the specified number and puts it to the specified buffer array.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).
- *int[]* **OUT_values** - Buffer array to store parameter values. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void SetParameterArray ( int num , int[] values )

Sets a value of the array parameter (type: [*PARAMETER_ARRAY_INT*](#PARAMETER_ARRAY_INT)) with the specified number using the specified array.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).
- *int[]* **values** - Array of values to be set.

## void GetParameterArray ( int num , ivec2[] OUT_values )

Returns a value of the array parameter (type: [*PARAMETER_ARRAY_INT2*](#PARAMETER_ARRAY_INT2)) with the specified number and puts it to the specified buffer array.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).
- *ivec2[]* **OUT_values** - Buffer array to store parameter values. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void SetParameterArray ( int num , ivec2[] values )

Sets a value of the array parameter (type: [*PARAMETER_ARRAY_INT2*](#PARAMETER_ARRAY_INT2)) with the specified number using the specified array.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).
- *ivec2[]* **values** - Array of values to be set.

## void GetParameterArray ( int num , ivec4[] OUT_values )

Returns a value of the array parameter (type: [*PARAMETER_ARRAY_INT4*](#PARAMETER_ARRAY_INT4)) with the specified number and puts it to the specified buffer array.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).
- *ivec4[]* **OUT_values** - Buffer array to store parameter values. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void SetParameterArray ( int num , ivec4[] values )

Sets a value of the array parameter (type: [*PARAMETER_ARRAY_INT4*](#PARAMETER_ARRAY_INT4)) with the specified number using the specified array.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).
- *ivec4[]* **values** - Array of values to be set.

## int SetParameterExpression ( int num , string expression )

Sets the expression used as a parameter value.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).
- *string* **expression** - New expression.

### Return value

1 if the expression is set successfully; otherwise, 0.
## string GetParameterExpression ( int num )

Returns an expression used as a parameter value.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).

### Return value

Parameter expression, if it exists; otherwise, **NULL** (**0**).
## string GetParameterName ( int num )

Returns the name of a given parameter.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).

### Return value

[Parameter name](#copy_name).
## void SetParameterFloat ( int num , float value )

Sets the value of a given [float parameter](#PARAMETER_FLOAT) by its number.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).
- *float* **value** - Parameter value to be set.

## void SetParameterFloat ( string name , float value )

Sets the value of a given [float parameter](#PARAMETER_FLOAT) by its name.
### Arguments

- *string* **name** - Name of the target float parameter.
- *float* **value** - Parameter value to be set.

## float GetParameterFloat ( int num )

Returns the current value of a given [float parameter](#PARAMETER_FLOAT). A 0 value returned by this method does not necessarily mean the value of the parameter, as you'll also get 0 in case the **parameter with the given number does not exist**. To check whether the parameter exists use **[FindParameter()](../../...md#findParameter_cstr_int)**. You should also be aware that states, parameters, and textures can be ignored in case [conditions](../../../code/formats/materials_formats/ulon_materials/states.md) they depend on are not met. To check conditions call **[CheckParameterConditions()](../../...md#checkParameterConditions_int_int)**.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).

### Return value

Current parameter value.
## void SetParameterFloat2 ( int num , vec2 value )

Sets the value of a given [float2 parameter](#PARAMETER_FLOAT2) by its number.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).
- *vec2* **value** - Parameter value to be set.

## void SetParameterFloat2 ( string name , vec2 value )

Sets the value of a given [float2 parameter](#PARAMETER_FLOAT2) by its name.
### Arguments

- *string* **name** - Name of the target float2 parameter.
- *vec2* **value** - Parameter value to be set.

## vec2 GetParameterFloat2 ( int num )

Returns the current value of a given [float2 parameter](#PARAMETER_FLOAT2).
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).

### Return value

Current parameter value.
## void SetParameterFloat3 ( int num , vec3 value )

Sets the value of a given [float3 parameter](#PARAMETER_FLOAT3) by its number.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).
- *vec3* **value** - Parameter value to be set.

## void SetParameterFloat3 ( string name , vec3 value )

Sets the value of a given [float3 parameter](#PARAMETER_FLOAT3) by its name.
### Arguments

- *string* **name** - Name of the target float3 parameter.
- *vec3* **value** - Parameter value to be set.

## vec3 GetParameterFloat3 ( int num )

Returns the current value of a given [float3 parameter](#PARAMETER_FLOAT3).
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).

### Return value

Current parameter value.
## void SetParameterFloat4 ( int num , vec4 value )

Sets the value of a given [float4 parameter](#PARAMETER_FLOAT4) by its number.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).
- *vec4* **value** - Parameter value to be set.

## void SetParameterFloat4 ( string name , vec4 value )

Sets the value of a given [float4 parameter](#PARAMETER_FLOAT4) by its name.
### Arguments

- *string* **name** - Name of the target float4 parameter.
- *vec4* **value** - Parameter value to be set.

## vec4 GetParameterFloat4 ( int num )

Returns the current value of a given [float4 parameter](#PARAMETER_FLOAT4).
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).

### Return value

Current parameter value.
## void SetParameterInt ( int num , int value )

Sets the value of a given [int parameter](#PARAMETER_INT) by its number.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).
- *int* **value** - Parameter value to be set.

## void SetParameterInt ( string name , int value )

Sets the value of a given [int parameter](#PARAMETER_INT) by its name.
### Arguments

- *string* **name** - Name of the target int parameter.
- *int* **value** - Parameter value to be set.

## int GetParameterInt ( int num )

Returns the current value of a given [int parameter](#PARAMETER_INT). A 0 value returned by this method does not necessarily mean the value of the parameter, as you'll also get 0 in case the **parameter with the given number does not exist**. To check whether the parameter exists use **[FindParameter()](../../...md#findParameter_cstr_int)**. You should also be aware that states, parameters, and textures can be ignored in case [conditions](../../../code/formats/materials_formats/ulon_materials/states.md) they depend on are not met. To check conditions call **[CheckParameterConditions()](../../...md#checkParameterConditions_int_int)**.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).

### Return value

Current parameter value.
## void SetParameterInt2 ( int num , ivec2 value )

Sets the value of a given [int2 parameter](#PARAMETER_INT2) by its number.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).
- *ivec2* **value** - Parameter value to be set.

## void SetParameterInt2 ( string name , ivec2 value )

Sets the value of a given [int2 parameter](#PARAMETER_INT2) by its name.
### Arguments

- *string* **name** - Name of the target int2 parameter.
- *ivec2* **value** - Parameter value to be set.

## ivec2 GetParameterInt2 ( int num )

Returns the current value of a given [int2 parameter](#PARAMETER_INT2).
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).

### Return value

Current parameter value.
## void SetParameterInt3 ( int num , ivec3 value )

Sets the value of a given [int3 parameter](#PARAMETER_INT3) by its number.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).
- *ivec3* **value** - Parameter value to be set.

## void SetParameterInt3 ( string name , ivec3 value )

Sets the value of a given [int3 parameter](#PARAMETER_INT3) by its name.
### Arguments

- *string* **name** - Name of the target int3 parameter.
- *ivec3* **value** - Parameter value to be set.

## ivec3 GetParameterInt3 ( int num )

Returns the current value of a given [int3 parameter](#PARAMETER_INT3).
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).

### Return value

Current parameter value.
## void SetParameterInt4 ( int num , ivec4 value )

Sets the value of a given [int4 parameter](#PARAMETER_INT4) by its number.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).
- *ivec4* **value** - Parameter value to be set.

## void SetParameterInt4 ( string name , ivec4 value )

Sets the value of a given [int4 parameter](#PARAMETER_INT4) by its name.
### Arguments

- *string* **name** - Name of the target int4 parameter.
- *ivec4* **value** - Parameter value to be set.

## ivec4 GetParameterInt4 ( int num )

Returns the current value of a given [int4 parameter](#PARAMETER_INT4).
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).

### Return value

Current parameter value.
## int GetParameterType ( int num )

Returns the type of a given parameter.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).

### Return value

One of the [*PARAMETER_**](#PARAMETER_FLOAT) pre-defined variables or **-1**, if an error has occurred.
## bool IsParent ( UGUID guid )

Returns a value indicating if the material with the given GUID is a parent of the current material.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - Material GUID.

### Return value

true if the material is the parent; otherwise, false.
## bool IsStateInternal ( int num )

Returns a value indicating if a given state is internal.
### Arguments

- *int* **num** - State number.

### Return value

true if the given state is internal; otherwise, false.
## bool IsStateOverridden ( int num )

Returns a value indicating if a given state is overridden.
### Arguments

- *int* **num** - State number.

### Return value

true if the given state is overridden; otherwise, false.
## void SetState ( int num , int value )

Sets the state value.
### Arguments

- *int* **num** - State number.
- *int* **value** - State value to be set.

## void SetState ( string name , int value )

Sets the value of the given state.
### Arguments

- *string* **name** - State name.
- *int* **value** - State value.

## int GetState ( int num )

Returns the state value. A 0 value returned by this method does not necessarily mean the value of the state, as you'll also get 0 in case the **state with the given number does not exist**. To check whether the state exists use **[FindState()](../../...md#findState_cstr_int)**. You should also be aware that states, parameters, and textures can be ignored in case [conditions](../../../code/formats/materials_formats/ulon_materials/states.md) they depend on are not met. To check conditions call **[CheckStateConditions()](../../...md#checkStateConditions_int_int)**.
### Arguments

- *int* **num** - State number.

### Return value

State value.
## int GetState ( string name )

Returns the value of the given state. A 0 value returned by this method does not necessarily mean the value of the state, as you'll also get 0 in case the **state with the given name does not exist**. To check whether the state exists use **[FindState()](../../...md#findState_cstr_int)**. You should also be aware that states, parameters, and textures can be ignored in case [conditions](../../../code/formats/materials_formats/ulon_materials/states.md) they depend on are not met. To check conditions call **[CheckStateConditions()](../../...md#checkStateConditions_int_int)**.
### Arguments

- *string* **name** - State name.

### Return value

State value.
## string GetStateName ( int num )

Returns the name of a given state.
### Arguments

- *int* **num** - State number.

### Return value

State name.
## string GetStateSwitchItem ( int num , int item )

Returns the switch item name for a given state.
### Arguments

- *int* **num** - State number.
- *int* **item** - Item number.

### Return value

Switch item name or **NULL** (**0**), if an error has occurred.
## int GetStateSwitchNumItems ( int num )

Returns the number of switch items for a given state.
### Arguments

- *int* **num** - State number.

### Return value

Number of switch items.
## int GetStateType ( int num )

Returns the type of a given state.
### Arguments

- *int* **num** - State number.

### Return value

One of the [*MATERIAL_STATE_**](#STATE_INT) pre-defined variables or **-1**, if an error occurred.
## bool IsTextureInternal ( int num )

Returns a value indicating if a given texture is internal.
### Arguments

- *int* **num** - Texture number.

### Return value

true if the given texture is internal; otherwise, false.
## bool IsTextureOverridden ( int num )

Returns a value indicating if a given texture is overridden.
### Arguments

- *int* **num** - Texture number.

### Return value

true if the given texture is overridden; otherwise, false.
## bool IsTextureLoaded ( int num )

Returns a value indicating if a given texture is loaded.
### Arguments

- *int* **num**

### Return value

true if the given texture is loaded; otherwise, false.
## string GetTextureName ( int num )

Returns the name of a given texture.
### Arguments

- *int* **num** - Texture number.

### Return value

Texture name.
## int GetTextureUnit ( int num )

Returns the number of the unit for a given texture used in shaders.
### Arguments

- *int* **num** - Texture number.

### Return value

Texture unit number.
## bool IsTextureEditable ( int num )

Returns a value indicating if the texture with the specified number is editable (can be modified).
### Arguments

- *int* **num** - Texture number.

### Return value

true if the texture with the specified number is editable; otherwise, false (the texture is read-only).
## int GetTextureSource ( int num )

Returns the source for the texture with the specified number.
### Arguments

- *int* **num** - Texture number.

### Return value

One of the **[TEXTURE_SOURCE_*](../../...md#TEXTURE_SOURCE_AUXILIARY)** pre-defined variables or **-1**, if an error has occurred.
## Texture GetTexture ( string name )

Returns the texture used in the material by its name. You should be aware that states, parameters, and textures can be ignored in case [conditions](../../../code/formats/materials_formats/ulon_materials/states.md) they depend on are not met. To check conditions call **[CheckTextureConditions()](../../...md#checkTextureConditions_int_int)**.
### Arguments

- *string* **name** - Name of the desired texture (e.g., albedo, emission, etc.).

### Return value

Texture used with the given name if it exists; otherwise *nullptr*.
## int FindParameter ( string name )

Searches for a parameter by a given [name](#copy_name) among all parameters of the current material.
### Arguments

- *string* **name** - [Parameter name](#copy_name).

### Return value

Parameter number, if it is found; otherwise, **-1**.
## int FindState ( string name )

Searches for a state by a given name among all states of the current material.
### Arguments

- *string* **name** - State name.

### Return value

State number, if it is found; otherwise, **-1**.
## int FindTexture ( string name )

Searches for a texture by a given [name](#copy_name) among all textures used by the current material.
### Arguments

- *string* **name** - [Texture name](#copy_name).

### Return value

Texture number, if it is found; otherwise, **-1**.
## bool SaveState ( Stream stream , bool forced = 0 )

Saves the settings of a given material (all of its options, states and parameters) into a binary stream.


Saving into the stream requires creating a blob to save into. To restore the saved state the [RestoreState()](#restoreState_Stream_int_int) method is used:


```csharp
// initialize object
Material mat = obj.GetMaterial(0);
mat.ViewportMask = 1; // viewport mask = 1

// save state
Blob blob_state = new Blob();
mat.SaveState(blob_state, true);

// change the state
mat.ViewportMask = ~0;  // now viewport mask = 111111111

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
mat.RestoreState(blob_state, true);		// restore viewport mask = 1

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - The stream to save material state data.
- *bool* **forced** - Forced saving of material settings.

### Return value

true if the material settings are saved successfully; otherwise, true.
## bool RestoreState ( Stream stream , bool forced = 0 )

Restores the state of a given material (all of its options, states and parameters) from a binary stream.


Restoring from the stream requires creating a blob to save into and saving the state using the [SaveState()](#saveState_Stream_int_int) method:


```csharp
// initialize object
Material mat = obj.GetMaterial(0);
mat.ViewportMask = 1; // viewport mask = 1

// save state
Blob blob_state = new Blob();
mat.SaveState(blob_state, true);

// change the state
mat.ViewportMask = ~0;  // now viewport mask = 111111111

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
mat.RestoreState(blob_state, true);		// restore viewport mask = 1

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - The stream with saved material data.
- *bool* **forced** - Forced restoring of material settings.

### Return value

true if the material settings are restored successfully; otherwise, false.
## bool CanRenderNode ( )

Returns a value indicating if the material can be rendered for at least one [type](../../../api/library/nodes/class.node_cs.md#DECAL_MESH) of nodes.
### Return value

true if the material is rendered for at least one type of nodes; otherwise, false.
## void ResetState ( int num )

Resets the [overridden](#isStateOverridden_int_int) value of the given state to the parent one.
### Arguments

- *int* **num** - State number.

## void SetTexturePath ( int num , string path )

Sets a new path to the texture with the given number.
### Arguments

- *int* **num** - Texture number.
- *string* **path** - A path to the texture or **NULL** to clear the path.

## void SetTexturePath ( string name , string path )

Sets a new path to the texture with the given [name](#copy_name).
### Arguments

- *string* **name** - [Texture name](#copy_name).
- *string* **path** - A path to the texture or **NULL** to clear the path.

## void ResetTexture ( int num )

Resets the [overridden](#isTextureOverridden_int_int) value of the given texture to the parent one.
### Arguments

- *int* **num** - Texture number.

## string GetTexturePath ( int num )

Returns a path to the texture with the specified number.
### Arguments

- *int* **num** - Texture number.

### Return value

A path to the texture.
## string GetTexturePath ( string name )

Returns a path to the texture with the specified [name](#copy_name).
### Arguments

- *string* **name** - [Texture name](#copy_name).

### Return value

A path to the texture.
## bool IsNodeTypeSupported ( Node.TYPE type )

Returns a value indicating if the given type of nodes is supported by the material.
### Arguments

- *[Node.TYPE](../../../api/library/nodes/class.node_cs.md#TYPE)* **type** - Node type: one of the *[OBJECT_*](../../../api/library/nodes/class.node_cs.md#OBJECT_BILLBOARDS)* or *[DECAL_*](../../../api/library/nodes/class.node_cs.md#DECAL_MESH)* variables.

### Return value

true if the node type is supported; otherwise, false.
## bool SetParent ( Material material , bool save_all_values = 1 )

Sets the given material as the parent for this material and saves the material's properties values (if the corresponding flag is set).


> **Notice:** The method isn't available for the [manual](#isManual_int) and [base](#isBase_int) materials.


### Arguments

- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - Material to be set as the parent for this material.
- *bool* **save_all_values** - Flag indicating if the material's properties will be saved after reparenting.

### Return value

true if the material's parent is changed; otherwise, false.
## bool CheckTextureConditions ( int num )

Checks if [conditions](../../../code/formats/materials_formats/ulon_materials/conditions.md) set for the given texture are met.
### Arguments

- *int* **num** - Texture number.

### Return value

true if conditions are met; otherwise, false.
## int LoadXml ( Xml xml )

Loads material settings from the specified Xml source.
### Arguments

- *[Xml](../../../api/library/common/class.xml_cs.md)* **xml** - An Xml node containing material settings.

### Return value

true if the material settings are loaded successfully; otherwise, false.
## bool LoadUlon ( UlonNode ulon )

Loads material settings from the specified [ULON](../../../code/formats/ulon_format.md) source.
### Arguments

- *[UlonNode](../../../api/library/common/class.ulonnode_cs.md)* **ulon** - A ULON-node containing material settings.

### Return value

true if the material settings are loaded successfully; otherwise, false.
## bool HasOverrides ( )

Returns a value indicating if the material has at least one overridden property.
### Return value

true if the material has at least one overridden property; otherwise, false.
## bool CanSave ( )

Returns a value indicating if the material can be saved. For example, this function will return 0 for a base or manual material.
### Return value

true if the material can be saved; otherwise, false.
## bool CheckStateConditions ( int num )

Checks if [conditions](../../../code/formats/materials_formats/ulon_materials/states.md) set for the given state are met.
### Arguments

- *int* **num** - State number.

### Return value

true if conditions are met; otherwise, false.
## bool CheckParameterConditions ( int num )

Checks if [conditions](../../../code/formats/materials_formats/ulon_materials/parameters.md) set for the given parameter are met.
### Arguments

- *int* **num** - [Parameter name](#copy_name).

### Return value

true if conditions are met; othersiwe, false.
## bool Save ( )

Save the material to the [current path](#getFilePath_String) used for this material.


> **Notice:** The method isn't available for the [manual](#isManual_int) and [base](#isBase_int) materials.


### Return value

true if the material is saved successfully; otherwise, false.
## bool Load ( string path )

Loads a material from the given file. The function can be used to load materials created during application execution or stored outside the `data` directory.
### Arguments

- *string* **path** - A path to the material file.

### Return value

true if the material is loaded successfully; otherwise, false.
## bool SaveXml ( Xml xml )

Saves the material into the given Xml.


> **Notice:** The method isn't available for the [manual](#isManual_int) and [base](#isBase_int) materials.


### Arguments

- *[Xml](../../../api/library/common/class.xml_cs.md)* **xml** - An Xml node.

### Return value

true if the material is saved successfully; otherwise, **false**.
## bool IsNodeSupported ( Node node )

Returns a value indicating if the material can be applied to the given node.
### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)* **node** - A node.

### Return value

true if the given node is supported; otherwise, false.
## void SetTexture ( int num , Texture texture )

Sets the given texture to the texture with the specified number.
### Arguments

- *int* **num** - Texture number.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Texture to be set.

## void SetTexture ( string name , Texture texture )

Sets the given texture to the texture with the specified [name](#copy_name).
### Arguments

- *string* **name** - [Texture name](#copy_name) (one of the textures used by the material, e.g.: *albedo*).
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Texture to be set.

## Texture GetTexture ( int num )

Returns a texture set for the current material. You should be aware that states, parameters, and textures can be ignored in case [conditions](../../../code/formats/materials_formats/ulon_materials/states.md) they depend on are not met. To check conditions call **[CheckTextureConditions()](../../...md#checkTextureConditions_int_int)**.
### Arguments

- *int* **num** - Texture number.

### Return value

Texture used with the given number if it exists; otherwise *nullptr*.
## UGUID GetFileGUID ( )

Returns a GUID of the current material file.
### Return value

GUID of the current material file.
## void ResetParameter ( int num )

Resets the [overridden](#isParameterOverridden_int_int) value of the given parameter to the parent one.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).

## bool Reload ( )

Reloads the material and all its children.
### Return value

true if the material is reloaded successfully; otherwise, false.
## int SetTextureImage ( int num , Image image )

Set a given [image](../../../api/library/common/class.image_cs.md) to a given texture.
### Arguments

- *int* **num** - Texture number.
- *[Image](../../../api/library/common/class.image_cs.md)* **image** - An image to set.

### Return value

1 if the image is set successfully; otherwise, 0.
## int GetTextureImage ( int num , Image image )

Reads a given texture into a given image.
### Arguments

- *int* **num** - Texture number.
- *[Image](../../../api/library/common/class.image_cs.md)* **image** - An image.

### Return value

1 if the texture is read successfully; otherwise, 0.
## TextureRamp GetTextureRamp ( int num )

Returns a [ramp texture](../../../api/library/rendering/class.textureramp_cs.md) instance for the data stored in the specified ramp texture (gradient).


> **Notice:** Modifications made to the ramp shall propagate to the parent and sibling materials. To modify an overridden ramp for this material only use the [*getTextureRampOverride()*](#getTextureRampOverride_int_TextureRamp) method.


### Arguments

- *int* **num** - Texture number.

### Return value

[TextureRamp](../../../api/library/rendering/class.textureramp_cs.md) class instance for the data stored in the gradient texture with the specified number.
## TextureRamp GetTextureRampOverride ( int num )

Returns a new [ramp texture](../../../api/library/rendering/class.textureramp_cs.md) instance for the data stored in the specified ramp texture (gradient) overriding the default one. This method enables you to set individual RGBA curves, adjusting color values of the resulting ramp texture (gradient).


> **Notice:** Modifications made to the ramp shall not propagate to the parent and sibling materials.


### Arguments

- *int* **num** - Texture number.

### Return value

New [TextureRamp](../../../api/library/rendering/class.textureramp_cs.md) class instance overriding the data stored in the specified ramp texture (gradient).
## void CreateShaders ( bool recursive = 0 )

Creates all shaders for the current material and its children (if specified).
### Arguments

- *bool* **recursive** - true to create shaders for child materials of the current material; otherwise, false.

## void DestroyTextures ( )

Deletes all textures used by the current material and its children.
## Render.PASS GetRenderPass ( string pass_name )

Returns the type of the rendering pass by its name (including custom passes).
### Arguments

- *string* **pass_name** - Name of the rendering pass.

### Return value

Rendering pass number in the range from 0 to 18 + custom_passes_number, if it exists; otherwise -1.
## string GetRenderPassName ( Render.PASS type )

Returns the name of the rendering pass by its number (including custom passes).
### Arguments

- *[Render.PASS](../../../api/library/rendering/class.render_cs.md#PASS)* **type** - Rendering pass number in range [0;[NUM_PASSES](../../../api/library/rendering/class.render_cs.md#NUM_PASSES)) (one of the *[PASS_*](../../../api/library/rendering/class.render_cs.md#PASS_WIREFRAME)* variables).

### Return value

Rendering pass name if it exists; otherwise NULL.
## bool RunExpression ( string name , int w , int h , int d = 1 )

Runs the material's expression with the specified name. An expression is a reference to a file containing code in UnigineScript, that can generate various elements used in the material (e.g., textures, texture arrays, unstructured buffers, etc.) or contain other logic. Expressions can be defined in the [`*.basemat` file](../../../code/formats/materials_formats/ulon_base_material_format.md) as follows:


```cpp
Expression name = "expression.usc";

```


An example of *expression.usc* code:


```cpp
// typical most frequently used parameters passed to the expression automatically, when it is called.
int in_width;
int in_height;
int in_depth;
Material in_material;

// If you need extra parameters, you should set them via Material::setParameter*("param_name", value) before calling Material::runExpression()
// then you can access them in the expression via in_material.getParameter*("param_name")

// ...

// get a temporary texture
Texture texture = engine.render.getTemporaryTexture(in_width, in_height);

//get the value of the material parameter named "my_extra_param"
float my_param = in_material.getParameter("my_extra_param");

// modify the temporary texture using the my_param parameter somehow...

// set the modified texture as albedo texture of the material
in_material->setTexture("albedo", texture);

```


To execute this expression the following code can be used:


```cpp
// ...
// setting the value of extra parameter
material->setParameterFloat("my_extra_param", 2.5f);

// running the expression
material->runExpression("expr_name", 512, 512, 1);
// ...

```


> **Notice:** Expressions can be executed only for [base materials](../../../content/materials/index.md#base_materials).


### Arguments

- *string* **name** - Expression name. [Expression](../../../code/formats/materials_formats/ulon_materials/expressions.md) with this name must be defined in the material declaration (`*.basemat` file).
- *int* **w** - Width, e.g. if a texture or a structured buffer is generated by the expression.
- *int* **h** - Height, e.g. if a texture or a structured buffer is generated by the expression.
- *int* **d** - Depth, e.g. if a 3D Texture, 2D array or a structured buffer is generated by the expression.

### Return value

true if the specified expression is executed successfully; otherwise, false.
## bool RenderScreen ( string pass_name )

Renders the screen-space material. The material must have a shader for the specified pass associated with it.
### Arguments

- *string* **pass_name** - Name of the rendering pass.

### Return value

false if the specified pass was not found; otherwise, true.
## void RenderScreen ( Render.PASS pass )

Renders the screen-space material. The material must have a shader for the specified pass associated with it.
### Arguments

- *[Render.PASS](../../../api/library/rendering/class.render_cs.md#PASS)* **pass** - Rendering pass number in range [0;[NUM_PASSES](../../../api/library/rendering/class.render_cs.md#NUM_PASSES)) (one of the *[PASS_*](../../../api/library/rendering/class.render_cs.md#PASS_WIREFRAME)* variables).

## bool RenderCompute ( string pass_name , int group_threads_x = 1 , int group_threads_y = 1 , int group_threads_z = 1 )

Renders the material using a compute shader. The material must have a compute shader for the specified pass associated with it.
### Arguments

- *string* **pass_name** - Name of the rendering pass.
- *int* **group_threads_x** - Local X work-group size of the compute shader.
- *int* **group_threads_y** - Local Y work-group size of the compute shader.
- *int* **group_threads_z** - Local Z work-group size of the compute shader.

### Return value

false if the specified pass was not found; otherwise, true.
## void RenderCompute ( Render.PASS pass , int group_threads_x = 1 , int group_threads_y = 1 , int group_threads_z = 1 )

Renders the material using a compute shader. The material must have a compute shader for the specified pass associated with it.
### Arguments

- *[Render.PASS](../../../api/library/rendering/class.render_cs.md#PASS)* **pass** - Rendering pass number in range [0;[NUM_PASSES](../../../api/library/rendering/class.render_cs.md#NUM_PASSES)) (one of the *[PASS_*](../../../api/library/rendering/class.render_cs.md#PASS_WIREFRAME)* variables).
- *int* **group_threads_x** - Local X work-group size of the compute shader.
- *int* **group_threads_y** - Local Y work-group size of the compute shader.
- *int* **group_threads_z** - Local Z work-group size of the compute shader.

## Material.DATA_TYPE GetUIItemDataType ( int item )

Returns the type of data of the specified UI item. UI items represent material parameters, options, states, textures, and groups in UnigineEditor.
### Arguments

- *int* **item** - UI item index in the range from 0 to the [total number of UI items](#getNumUIItems_int).

### Return value

UI item data type (parameter, option, state, texture, or group).
## int GetUIItemDataID ( int item )

Returns the id of the data type controlled by the specified UI item. UI items represent material parameters, options, states, textures, and groups in UnigineEditor.
### Arguments

- *int* **item** - UI item index in the range from 0 to the [total number of UI items](#getNumUIItems_int).

### Return value

UI item data id: one of the *[STATE_*](#STATE_INT)*, *[PARAMETER_*](#PARAMETER_INT)*, *[OPTION_*](#OPTION_TRANSPARENT)*, *[TEXTURE_SOURCE_*](#TEXTURE_SOURCE_ASSET)* pre-defined variables or -1, if an error has occurred.
## bool IsUIItemHidden ( int item )

Returns a value indicating if the specified UI item is hidden.
### Arguments

- *int* **item** - UI item index in the range from 0 to the [total number of UI items](#getNumUIItems_int).

### Return value

true is the specified UI item is hidden; otherwise, false.
## string GetUIItemTitle ( int item )

Returns the title set for the specified UI item.
### Arguments

- *int* **item** - UI item index in the range from 0 to the [total number of UI items](#getNumUIItems_int).

### Return value

Title set for the specified UI item.
## string GetUIItemTooltip ( int item )

Returns the text of the tooltip set for the specified UI item.
### Arguments

- *int* **item** - UI item index in the range from 0 to the [total number of UI items](#getNumUIItems_int).

### Return value

Text of the tooltip set for the specified UI item.
## Material.WIDGET GetUIItemWidget ( int item )

Returns the type of the widget for the specified UI item.
### Arguments

- *int* **item** - UI item index in the range from 0 to the [total number of UI items](#getNumUIItems_int).

### Return value

UI item widget type.
## int GetUIItemParent ( int item )

Returns an index of the parent of the specified UI item. This method is used to get the index of the group to which the specified parameter/state/option/texture belongs.
### Arguments

- *int* **item** - UI item index in the range from 0 to the [total number of UI items](#getNumUIItems_int).

### Return value

Global index of the parent UI element in the range from 0 to the [total number of UI items for the material](#getNumUIItems_int).
## int GetUIItemNumChildren ( int item )

Returns the number of child items for the group UI item with the specified number.


> **Notice:** This method is to be used for UI item groups only ([DATA_TYPE_GROUP](#DATA_TYPE_GROUP)), other items cannot have children!


### Arguments

- *int* **item** - UI item group index in the range from 0 to the [total number of UI items](#getNumUIItems_int).

### Return value

Number of child items for the specified group UI item.
## int GetUIItemChild ( int item , int num )

Returns the index of a child UI item that belongs to the specified group by the item number within the group.


> **Notice:** This method is to be used for UI item groups only ([DATA_TYPE_GROUP](#DATA_TYPE_GROUP)), other items cannot have children!


### Arguments

- *int* **item** - UI item group index in the range from 0 to the [total number of UI items](#getNumUIItems_int).
- *int* **num** - Number of UI item within the group (in the list of children).

### Return value

Global index of the child UI element in the range from 0 to the [total number of UI items for the material](#getNumUIItems_int).
## bool IsUIItemSliderMinExpand ( int item )

Returns a value indicating if the maximum slider value for the specified UI item can be increased.
### Arguments

- *int* **item** - UI item index in the range from 0 to the [total number of UI items](#getNumUIItems_int).

### Return value

true if the maximum value can be increased; otherwise, false.
## bool IsUIItemSliderMaxExpand ( int item )

Returns a value indicating if the minimum slider value for the specified UI item can be decreased.
### Arguments

- *int* **item** - UI item index in the range from 0 to the [total number of UI items](#getNumUIItems_int).

### Return value

true if the minimum value can be decreased; otherwise, false.
## float GetUIItemSliderMinValue ( int item )

Returns the minimum allowed value of the slider for the specified UI item.
### Arguments

- *int* **item** - UI item index in the range from 0 to the [total number of UI items](#getNumUIItems_int).

### Return value

Minimum value of the slider.
## float GetUIItemSliderMaxValue ( int item )

Returns the maximum allowed value of the slider for the specified UI item.
### Arguments

- *int* **item** - UI item index in the range from 0 to the [total number of UI items](#getNumUIItems_int).

### Return value

Maximum value of the slider.
## int GetUIItemGroupToggleStateID ( int item )

Returns the global index of the state toggle UI element turning the specified group on and off.


> **Notice:** This method is to be used for UI item groups only ([DATA_TYPE_GROUP](#DATA_TYPE_GROUP))!


### Arguments

- *int* **item** - UI item index in the range from 0 to the [total number of UI items](#getNumUIItems_int).

### Return value

Global index of the state toggle UI element in the range from 0 to the [total number of UI items for the material](#getNumUIItems_int).
## bool IsUIItemGroupCollapsed ( int item )

Returns a value indicating if the specified group of UI items is currently collapsed in the UI of the Unigine Editor.


> **Notice:** This method is to be used for UI item groups only ([DATA_TYPE_GROUP](#DATA_TYPE_GROUP))!


### Arguments

- *int* **item** - UI item index in the range from 0 to the [total number of UI items](#getNumUIItems_int).

### Return value

true if the specified group of UI items is currently collapsed in the UI; otherwise, false (the group is expanded).
## void SetOption ( int num , int value )

Sets a new value for the specified option.
### Arguments

- *int* **num** - Option number.
- *int* **value** - New value to be set for the specified option.

## int GetOption ( int num )

Returns the current value of the specified option.
### Arguments

- *int* **num** - Option number.

### Return value

Current value of the specified option.
## bool IsOptionOverridden ( int num )

Returns a value indicating if a given option is overridden.
### Arguments

- *int* **num** - Option number.

### Return value

true if the given option is overridden; otherwise, false.
## void ResetOption ( int num )

Resets the [overridden](#isOptionOverridden_int_int) value of the given option to the parent one.
### Arguments

- *int* **num** - Option number.

## bool IsParent ( Material parent )

Returns a value indicating if the given material is a parent of the current material.
### Arguments

- *[Material](../../../api/library/rendering/class.material_cs.md)* **parent** - Material instance.

### Return value

true if the material is the parent, otherwise - false.
## Material Clone ( )

Clones the material. The cloned material will be empty: it will have a GUID but won't be displayed in the materials hierarchy.
### Return value

Cloned material.
## Material Clone ( UGUID guid )

Clones the material and assigns the given GUID to it.
> **Notice:** A [base material](../../../content/materials/index.md#base_materials) cannot be cloned.

### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - Cloned material GUID.

### Return value

Cloned material.
## Material Inherit ( )

Inherits the material. The inherited material will be empty: it will have a GUID but won't be displayed in materials hierarchy.
### Return value

Inherited material.
## Material Inherit ( UGUID guid )

Inherits a new material from the current one and assigns the specified GUID to it.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - Inhereted material GUID.

### Return value

Inhereted material.
## string WidgetToString ( Material.WIDGET widget )

Returns the name of the widget by its type.
### Arguments

- *[Material.WIDGET](../../../api/library/rendering/class.material_cs.md#WIDGET)* **widget** - [Widget type](#WIDGET).

### Return value

Name of the widget.
## Material.WIDGET StringToWidget ( string str )

Returns the widget type by its name.
### Arguments

- *string* **str** - Name of the widget.

### Return value

[Widget type](#WIDGET).
## int GetTextureSamplerFlags ( int num )

Returns the sampler flags of the texture with the given number.
### Arguments

- *int* **num** - Number of the texture.

### Return value

Texture sampler flags.
## void SetTextureSamplerFlags ( int num , int sampler_flags )

Sets the sampler flags for the texture with the given number.
### Arguments

- *int* **num** - Number of the texture.
- *int* **sampler_flags** - Sampler flags.

## int GetTextureFormatFlags ( int num )

Returns the format flags of the texture with the given number.
### Arguments

- *int* **num** - Number of the texture.

### Return value

Texture format flags.
## bool CreateMaterialFile ( string path )

Creates a file and saves the [internal](../../../content/materials/index.md#manual_internal_materials) material to it.
### Arguments

- *string* **path** - A path to save the material

### Return value

The value indicating if the material was successful saved.
## Shader GetShaderAsync ( Render.PASS pass , int node )

Returns the [rendering shader](../../../api/library/rendering/class.shader_cs.md) for the specified rendering pass and [node type](../../../api/library/nodes/class.node_cs.md#TYPE):


- If the shader has been compiled previously, the function will return it immediately.
- If the shader hasn't been compiled yet, the function will initiate its asynchronous compilation in another thread and return the successfully compiled shader. > **Notice:** The function will keep returning null until the shader is compiled.


> **Notice:** To compile the shader asynchronously, enable the [asynchronous compilation mode](../../../api/library/rendering/class.render_cs.md#getShadersCompileMode_int). Otherwise, the function will work the same as *[getShaderForce()](#getShaderForce_int_int_Shader)*.


### Arguments

- *[Render.PASS](../../../api/library/rendering/class.render_cs.md#PASS)* **pass** - Rendering pass number in range [0;[NUM_PASSES](../../../api/library/rendering/class.render_cs.md#NUM_PASSES)) (one of the *[PASS_*](../../../api/library/rendering/class.render_cs.md#PASS_WIREFRAME)* variables).
- *int* **node** - [Node type](../../../api/library/nodes/class.node_cs.md#TYPE).

### Return value

Shader for the specified rendering pass and node type, if compiled successfully. Otherwise, null.
## Shader GetShaderAsync ( Render.PASS pass )

Returns the [rendering shader](../../../api/library/rendering/class.shader_cs.md) for the specified rendering pass:


- If the shader has been compiled previously, the function will return it immediately.
- If the shader hasn't been compiled yet, the function will initiate its asynchronous compilation in another thread and return the successfully compiled shader. > **Notice:** The function will keep returning null until the shader is compiled.


> **Notice:** To compile the shader asynchronously, enable the [asynchronous compilation mode](../../../api/library/rendering/class.render_cs.md#getShadersCompileMode_int). Otherwise, the function will work the same as *[getShaderForce()](#getShaderForce_int_Shader)*.


### Arguments

- *[Render.PASS](../../../api/library/rendering/class.render_cs.md#PASS)* **pass** - Rendering pass number in range [0;[NUM_PASSES](../../../api/library/rendering/class.render_cs.md#NUM_PASSES)) (one of the *[PASS_*](../../../api/library/rendering/class.render_cs.md#PASS_WIREFRAME)* variables).

### Return value

Shader for the specified rendering pass, if compiled successfully. Otherwise, null.
## Shader GetShaderAsync ( string pass , int node )

Returns the [rendering shader](../../../api/library/rendering/class.shader_cs.md) for the specified rendering pass and [node type](../../../api/library/nodes/class.node_cs.md#TYPE):


- If the shader has been compiled previously, the function will return it immediately.
- If the shader hasn't been compiled yet, the function will initiate its asynchronous compilation in another thread and return the successfully compiled shader. > **Notice:** The function will keep returning null until the shader is compiled.


> **Notice:** To compile the shader asynchronously, enable the [asynchronous compilation mode](../../../api/library/rendering/class.render_cs.md#getShadersCompileMode_int). Otherwise, the function will work the same as *[getShaderForce()](#getShaderForce_cstr_int_Shader)*.


### Arguments

- *string* **pass** - Rendering pass name. One of the following:

  - *wireframe*
  - *visualizer_solid*
  - *deferred*
  - *auxiliary*
  - *emission*
  - *reflection*
  - *refraction*
  - *transparent_blur*
  - *ambient*
  - *light_voxel_probe*
  - *light_environment_probe*
  - *light_omni*
  - *light_proj*
  - *light_world*
  - *shadow*
  - *depth_pre_pass*
  - *post*
  - *object_post*
- *int* **node** - [Node type](../../../api/library/nodes/class.node_cs.md#TYPE).

### Return value

Shader for the specified rendering pass and node type, if compiled successfully. Otherwise, null.
## Shader GetShaderAsync ( string pass )

Returns the [rendering shader](../../../api/library/rendering/class.shader_cs.md) for the specified rendering pass:


- If the shader has been compiled previously, the function will return it immediately.
- If the shader hasn't been compiled yet, the function will initiate its asynchronous compilation in another thread and return the successfully compiled shader. > **Notice:** The function will keep returning null until the shader is compiled.


> **Notice:** To compile the shader asynchronously, enable the [asynchronous compilation mode](../../../api/library/rendering/class.render_cs.md#getShadersCompileMode_int). Otherwise, the function will work the same as *[getShaderForce()](#getShaderForce_cstr_Shader)*.


### Arguments

- *string* **pass** - Rendering pass name. One of the following:

  - *wireframe*
  - *visualizer_solid*
  - *deferred*
  - *auxiliary*
  - *emission*
  - *reflection*
  - *refraction*
  - *transparent_blur*
  - *ambient*
  - *light_voxel_probe*
  - *light_environment_probe*
  - *light_omni*
  - *light_proj*
  - *light_world*
  - *shadow*
  - *depth_pre_pass*
  - *post*
  - *object_post*

### Return value

Shader for the specified rendering pass, if compiled successfully. Otherwise, null.
## Shader GetShaderForce ( Render.PASS pass , int node )

Returns the [rendering shader](../../../api/library/rendering/class.shader_cs.md) for the specified rendering pass and [node type](../../../api/library/nodes/class.node_cs.md#TYPE):


- If the shader has been compiled previously, the function will return it immediately.
- If the shader hasn't been compiled yet, the function will immediately compile and return it.


> **Notice:** The function causes a spike because it compiles the shader in the current thread.


### Arguments

- *[Render.PASS](../../../api/library/rendering/class.render_cs.md#PASS)* **pass** - Rendering pass number in range [0;[NUM_PASSES](../../../api/library/rendering/class.render_cs.md#NUM_PASSES)) (one of the *[PASS_*](../../../api/library/rendering/class.render_cs.md#PASS_WIREFRAME)* variables).
- *int* **node** - [Node type](../../../api/library/nodes/class.node_cs.md#TYPE).

### Return value

Shader for the specified rendering pass and node type, if compiled successfully. Otherwise, null.
## Shader GetShaderForce ( Render.PASS pass )

Returns the [rendering shader](../../../api/library/rendering/class.shader_cs.md) for the specified rendering pass:


- If the shader has been compiled previously, the function will return it immediately.
- If the shader hasn't been compiled yet, the function will immediately compile and return it.


> **Notice:** The function causes a spike because it compiles the shader in the current thread.


### Arguments

- *[Render.PASS](../../../api/library/rendering/class.render_cs.md#PASS)* **pass** - Rendering pass number in range [0;[NUM_PASSES](../../../api/library/rendering/class.render_cs.md#NUM_PASSES)) (one of the *[PASS_*](../../../api/library/rendering/class.render_cs.md#PASS_WIREFRAME)* variables).

### Return value

Shader for the specified rendering pass, if compiled successfully. Otherwise, null.
## Shader GetShaderForce ( string pass , int node )

Returns the [rendering shader](../../../api/library/rendering/class.shader_cs.md) for the specified rendering pass and [node type](../../../api/library/nodes/class.node_cs.md#TYPE):


- If the shader has been compiled previously, the function will return it immediately.
- If the shader hasn't been compiled yet, the function will immediately compile and return it.


> **Notice:** The function causes a spike because it compiles the shader in the current thread.


### Arguments

- *string* **pass** - Rendering pass name. One of the following:

  - *wireframe*
  - *visualizer_solid*
  - *deferred*
  - *auxiliary*
  - *emission*
  - *reflection*
  - *refraction*
  - *transparent_blur*
  - *ambient*
  - *light_voxel_probe*
  - *light_environment_probe*
  - *light_omni*
  - *light_proj*
  - *light_world*
  - *shadow*
  - *depth_pre_pass*
  - *post*
  - *object_post*
- *int* **node** - [Node type](../../../api/library/nodes/class.node_cs.md#TYPE).

### Return value

Shader for the specified rendering pass and node type, if compiled successfully. Otherwise, null.
## Shader GetShaderForce ( string pass )

Returns the [rendering shader](../../../api/library/rendering/class.shader_cs.md) for the specified rendering pass:


- If the shader has been compiled previously, the function will return it immediately.
- If the shader hasn't been compiled yet, the function will immediately compile and return it.


> **Notice:** The function causes a spike because it compiles the shader in the current thread.


### Arguments

- *string* **pass** - Rendering pass name. One of the following:

  - *wireframe*
  - *visualizer_solid*
  - *deferred*
  - *auxiliary*
  - *emission*
  - *reflection*
  - *refraction*
  - *transparent_blur*
  - *ambient*
  - *light_voxel_probe*
  - *light_environment_probe*
  - *light_omni*
  - *light_proj*
  - *light_world*
  - *shadow*
  - *depth_pre_pass*
  - *post*
  - *object_post*

### Return value

Shader for the specified rendering pass, if compiled successfully. Otherwise, null.
## void SetTextureStreamingDensityMultiplier ( int num , float streaming_density_multiplier )

Sets a multiplier adjusting the distance at which the texture mipmaps are rendered.
### Arguments

- *int* **num** - Number of the texture.
- *float* **streaming_density_multiplier** - Multiplier applied to the texture mipmaps rendering distance.

## float GetTextureStreamingDensityMultiplier ( int num )

Returns the current adjusting the distance at which the texture mipmaps are rendered.
### Arguments

- *int* **num** - Number of the texture.

### Return value

Multiplier applied to the texture mipmaps rendering distance.
## bool NeedCreateShaderCache ( )

Returns a value indicating if shader cache needs to be created for current material states and options.
### Return value

true if shader cache is required for current material states and options; or false, if shader combination for current material states and options is already in cache.
## bool NeedCreateShaderCache ( Render.PASS pass , Node.TYPE node_type )

Returns a value indicating if shader combination needs to be created for the given rendering pass and node type.
### Arguments

- *[Render.PASS](../../../api/library/rendering/class.render_cs.md#PASS)* **pass** - Rendering pass number in range [0;[NUM_PASSES](../../../api/library/rendering/class.render_cs.md#NUM_PASSES)) (one of the *[PASS_*](../../../api/library/rendering/class.render_cs.md#PASS_WIREFRAME)* variables).
- *[Node.TYPE](../../../api/library/nodes/class.node_cs.md#TYPE)* **node_type** - Node type.

### Return value

true if shader cache needs to be created for the given rendering pass and node type; or false, if shader combination for the given rendering pass and node type is already in cache.
## bool ShaderCacheExist ( Render.PASS pass , Node.TYPE node_type )

Returns a value indicating if shader combination for the given rendering pass and node type is already in cache.
### Arguments

- *[Render.PASS](../../../api/library/rendering/class.render_cs.md#PASS)* **pass** - Rendering pass number in range [0;[NUM_PASSES](../../../api/library/rendering/class.render_cs.md#NUM_PASSES)) (one of the *[PASS_*](../../../api/library/rendering/class.render_cs.md#PASS_WIREFRAME)* variables).
- *[Node.TYPE](../../../api/library/nodes/class.node_cs.md#TYPE)* **node_type** - Node type.

### Return value

true if shader combination for the given rendering pass and node type is already in cache; otherwise, false.
## void CreateShaderForce ( Render.PASS pass , Node.TYPE node_type )

Compiles shader combination for the given rendering pass and node type. Shaders are compiled immediately, which may cause spikes, therefore this method is recommended only for critical cases, where [*CreateShaderAsync*](#createShaderAsync_int_int_void) doesn't ensure a satisfying result.
### Arguments

- *[Render.PASS](../../../api/library/rendering/class.render_cs.md#PASS)* **pass** - Rendering pass number in range [0;[NUM_PASSES](../../../api/library/rendering/class.render_cs.md#NUM_PASSES)) (one of the *[PASS_*](../../../api/library/rendering/class.render_cs.md#PASS_WIREFRAME)* variables).
- *[Node.TYPE](../../../api/library/nodes/class.node_cs.md#TYPE)* **node_type** - Node type.

## void CreateShaderAsync ( Render.PASS pass , Node.TYPE node_type )

Compiles shader combination for the given rendering pass and node type. Shaders are compiled asynchronously, which ensures smooth performance without spikes and is suitable for most cases. For the shaders that requre to be compiled immediately, use [*CreateShaderForce*](#createShaderForce_int_int_void).
### Arguments

- *[Render.PASS](../../../api/library/rendering/class.render_cs.md#PASS)* **pass** - Rendering pass number in range [0;[NUM_PASSES](../../../api/library/rendering/class.render_cs.md#NUM_PASSES)) (one of the *[PASS_*](../../../api/library/rendering/class.render_cs.md#PASS_WIREFRAME)* variables).
- *[Node.TYPE](../../../api/library/nodes/class.node_cs.md#TYPE)* **node_type** - Node type.

## void CreateRenderMaterials ( )

Creates render materials (internal materials required for rendering). For example, you can create all necessary render materials during initialization to avoid spikes that may occur later.
## void CreateShaderCache ( bool recursive = false , bool force = false )

Compiles and caches all shader permutations needed by this material for every render pass and node type. With asynchronous compilation the material may render with a fallback until the shaders are ready.
### Arguments

- *bool* **recursive** - Flag defining whether the shader cache is also created for all inherited (child) materials, recursively.
- *bool* **force** - Flag defining whether missing shaders are compiled immediately (blocking); otherwise the compilation is queued to run asynchronously in the background.

## void CreateShadersFromCache ( bool recursive = false )

Compiles all shaders available in shader cache for the current material and its children (if any).
### Arguments

- *bool* **recursive** - true to compile shaders for child materials; otherwise, false.

## Texture GetTexture ( int num , float density )

Returns the texture of the given material slot, initiating streaming of its mip levels according to the specified density instead of the material's current frame density.
### Arguments

- *int* **num** - Texture slot number.
- *float* **density** - Requested mipmap density relative to the screen resolution, used to choose the mip level to stream: values up to 1.0 request the full resolution, higher values request coarser mips.

### Return value

Texture of the slot (possibly still streaming at a coarser mip level).
## float GetCustomParameterFloat ( string name )

Returns the current value of the custom material parameter with the given name: the overridden value, or the value inherited from the material hierarchy, bottoming out at the default value defined in the *[material parameters layout](../../../api/library/rendering/class.materials_cs.md#getMaterialParameters_CustomParameterLayout)*.
### Arguments

- *string* **name** - Parameter name.

### Return value

Current parameter value, or 0 if no parameter with this name exists.
## float GetCustomParameterFloat ( int num )

Returns the current value of the custom material parameter with the given number: the overridden value, or the value inherited from the material hierarchy, bottoming out at the default value defined in the *[material parameters layout](../../../api/library/rendering/class.materials_cs.md#getMaterialParameters_CustomParameterLayout)*.
### Arguments

- *int* **num** - Parameter number.

### Return value

Current parameter value.
## int GetCustomParameterInt ( string name )

Returns the current value of the custom material parameter with the given name: the overridden value, or the value inherited from the material hierarchy, bottoming out at the default value defined in the *[material parameters layout](../../../api/library/rendering/class.materials_cs.md#getMaterialParameters_CustomParameterLayout)*.
### Arguments

- *string* **name** - Parameter name.

### Return value

Current parameter value, or 0 if no parameter with this name exists.
## int GetCustomParameterInt ( int num )

Returns the current value of the custom material parameter with the given number: the overridden value, or the value inherited from the material hierarchy, bottoming out at the default value defined in the *[material parameters layout](../../../api/library/rendering/class.materials_cs.md#getMaterialParameters_CustomParameterLayout)*.
### Arguments

- *int* **num** - Parameter number.

### Return value

Current parameter value.
## uint GetCustomParameterUInt ( string name )

Returns the current value of the custom material parameter with the given name: the overridden value, or the value inherited from the material hierarchy, bottoming out at the default value defined in the *[material parameters layout](../../../api/library/rendering/class.materials_cs.md#getMaterialParameters_CustomParameterLayout)*.
### Arguments

- *string* **name** - Parameter name.

### Return value

Current parameter value, or 0 if no parameter with this name exists.
## uint GetCustomParameterUInt ( int num )

Returns the current value of the custom material parameter with the given number: the overridden value, or the value inherited from the material hierarchy, bottoming out at the default value defined in the *[material parameters layout](../../../api/library/rendering/class.materials_cs.md#getMaterialParameters_CustomParameterLayout)*.
### Arguments

- *int* **num** - Parameter number.

### Return value

Current parameter value.
## bool IsCustomParameterOverridden ( int num )

Checks if the value of the custom material parameter with the given number is overridden by this material rather than inherited. For a material without a parent, this method always returns false.
### Arguments

- *int* **num** - Parameter number.

### Return value

true if the parameter value is overridden by this material; otherwise, false.
## bool IsCustomParametersSupported ( )

Checks if custom material parameters are supported for this material. Custom parameters are available only for materials that can be assigned to nodes (e.g. post-process and scriptable materials do not support them).
### Return value

true if custom material parameters are supported for the material; otherwise, false.
## void ResetCustomParameter ( int num )

Resets the override of the custom material parameter with the given number: the value is inherited from the parent material again. This method has no effect on base materials.
### Arguments

- *int* **num** - Parameter number.

## void ResetCustomParameters ( )

Resets the overrides of all custom material parameters of the material.
## void SetCustomParameterFloat ( string name , float value )

Sets a new value of the custom material parameter with the given name. The material overrides the value inherited from its parent; child materials that do not override the parameter receive the new value. If no parameter with this name exists in the layout, the method does nothing.
### Arguments

- *string* **name** - Parameter name.
- *float* **value** - New parameter value.

## void SetCustomParameterFloat ( int num , float value )

Sets a new value of the custom material parameter with the given number. The material overrides the value inherited from its parent; child materials that do not override the parameter receive the new value.
### Arguments

- *int* **num** - Parameter number.
- *float* **value** - New parameter value.

## void SetCustomParameterInt ( string name , int value )

Sets a new value of the custom material parameter with the given name. The material overrides the value inherited from its parent; child materials that do not override the parameter receive the new value. If no parameter with this name exists in the layout, the method does nothing.
### Arguments

- *string* **name** - Parameter name.
- *int* **value** - New parameter value.

## void SetCustomParameterInt ( int num , int value )

Sets a new value of the custom material parameter with the given number. The material overrides the value inherited from its parent; child materials that do not override the parameter receive the new value.
### Arguments

- *int* **num** - Parameter number.
- *int* **value** - New parameter value.

## void SetCustomParameterUInt ( string name , uint value )

Sets a new value of the custom material parameter with the given name. The material overrides the value inherited from its parent; child materials that do not override the parameter receive the new value. If no parameter with this name exists in the layout, the method does nothing.
### Arguments

- *string* **name** - Parameter name.
- *uint* **value** - New parameter value.

## void SetCustomParameterUInt ( int num , uint value )

Sets a new value of the custom material parameter with the given number. The material overrides the value inherited from its parent; child materials that do not override the parameter receive the new value.
### Arguments

- *int* **num** - Parameter number.
- *uint* **value** - New parameter value.
