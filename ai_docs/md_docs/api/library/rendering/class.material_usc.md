# Unigine.Material Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


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


When an object is deleted, all unique materials assigned to it should also be deleted via  to free memory. This method checks each material (having **[Material::canRenderNode()()](../../...md#canRenderNode_int)* == **true***) to see if it is also used by other objects (i.e., all other world objects are checked individually). According to the policy, all checked materials will be deleted in the next swap stage of the main loop. If there are thousands of objects in the world, you'll get a spike.


To avoid a spike you need to use a right pipeline of material inheritance. Don't get a material from another object via *[Object::getMaterial(surface)()](../../../api/library/objects/class.object_usc.md#getMaterial_int_Material)* and call *[Material::inherit()()](../../...md#inherit_Material)* on it. It is better to use *[Object::getMaterialInherit(surface)()](../../../api/library/objects/class.object_usc.md#getMaterialInherit_int_Material)*, which creates a new material instance having its lifetime associated with this object, and you won't have to delete it manually.


### Usage Examples


#### Changing Textures


The first example describes how to inherit a material from a base one, change the material texture, and set [texture flags](../../../api/library/rendering/class.texture_usc.md#SAMPLER_ANISOTROPY_1) for it. We inherit a new material *my_mesh_base_0.mat* from the *mesh_base* material, assign it to the default *material ball* object, change its albedo texture, and set the [SAMPLER_FILTER_POINT](../../../api/library/rendering/class.texture_usc.md#SAMPLER_FILTER_POINT) flag for it.


Add the following code to the world script file.


```cpp
// your_world_name.usc

/* .. */

int init() {

	/* .. */

	// inherit a new material from the material_ball
	Material m = engine.materials.findManualMaterial("Unigine::mesh_base").inherit("my_mesh_base_0");

	// getting the material_ball object and assigning the material_ball_0 material to it
	ObjectMeshStatic material_ball = node_cast(engine.world.getNodeByName("material_ball"));
	material_ball.setMaterialPath("materials/my_mesh_base_0", "*");


	// check if our material is editable and perform modifications
	if (m.isEditable()){
		log.message("Material (%s) is editable.\n", m.getPath());

		// get the number of the albedo texture of the my_mesh_base_0 material
		int num = m.findTexture("albedo");
		// change albedo texture of the material to core/textures/common/checker_d.texture
		m.setTexturePath(num, "core/textures/common/checker_d.texture");

		// get current flags, check if point filtering is enabled and display the result in the console
		int flags = m.getTextureSamplerFlags(num);
		log.message("Flags for %s texture (%d):%d \n", m.getTextureName(num), num, flags);
		log.message("FILTER_POINT %s\n", (flags & TEXTURE_FILTER_POINT)? "enabled": "disabled");

		// set the FILTER_POINT flag
		m.setTextureSamplerFlags(num, TEXTURE_FILTER_POINT);

		// get the flags, check if point filtering is enabled and display the result in the console
		int flagsSet = m.getTextureSamplerFlags(num);
		log.message("Flags for %s texture (%d):%d \n", m.getTextureName(num), num, flagsSet);
		log.message("FILTER_POINT %s\n", (flagsSet & TEXTURE_FILTER_POINT) ? "enabled" : "disabled");
	}

	return 1;
}

/* .. */

```


As a result you'll see that the albedo texture of the *material ball* object has changed and the following text is displayed in the [console](../../../code/console/index.md):


```text
Material (guid://4dfec30f491f753f6e89094db6d3d695e89f9d6f) is editable.
Flags for albedo texture (1):524288000
FILTER_POINT disabled
Flags for albedo texture (1):1048576
FILTER_POINT enabled

```


#### Changing States and Parameters


The second example illustrates how to inherit a material from the [mesh_base](../../../content/materials/library/mesh_base/index.md) and change two parameters affecting the look of reflections.


Add the following code to the world script file.


```cpp
// your_world_name.usc

/* .. */

int init() {

	/* .. */

	// find the mesh_base material
	Material mesh_base = engine.materials.findManualMaterial("Unigine::mesh_base");
	// inherit a new material from it
	Material reflector_material = mesh_base.inherit();

	// set metallness and roughness parameters to make the surface look like a mirror
	// by the name of the parameter
	reflector_material.setParameter("metalness", 1.0f);
	// or by its id, which is the same
	reflector_material.setParameter(reflector_material.findParameter("roughness"), 0.0f);

	// save the material asset to planar_reflector.mat file in the data project folder
	reflector_material.createMaterialFile("planar_reflector.mat");

	// assign the mesh_base material to the material ball by its path
	ObjectMeshStatic material_ball = node_cast(engine.world.getNodeByName("material_ball"));
	material_ball.setMaterialPath("core/materials/base/objects/mesh/mesh_base.basemat","*");

	// assign new reflective material to the ground object
	ObjectMeshDynamic ground = node_cast(engine.world.getNodeByName("ground"));
	ground.setMaterial(reflector_material, 0);


	return 1;
}

/* .. */

```


## Material Class

### Members

## int isEmpty () const

Returns the current value indicating if an empty shader is used as a vertex shader in the current material.
### Return value

Current an empty shader is used as a vertex shader in the current material
## int isFileEngine () const

Returns the current value indicating if the material is a core Engine or UnigineEditor material (i.e. required for Engine/Editor operation).
Such materials are stored in the `core`, `editor` and `editor2` folders/packages.

> **Notice:** It is not recommended to delete files of non-core materials (e.g., created by plugins or otherwise) at run-time, as this may affect materials caching and result in a crash.

### Return value

Current the material is a core Engine or UnigineEditor material
## int isAutoSave () const

Returns the current value indicating if the material can be saved automatically (automatic material saving is performed, for example, on world saving).
The value is 0 in the following cases:


- The *[canSave()](#canSave_int)* function returns 0 for the material.
- The material is [non-editable](#isEditable_int).
- The material [GUID](../../../api/library/filesystem/class.uguid_usc.md) is not a valid one.


### Return value

Current the material can be saved automatically
## int isManual () const

Returns the current value indicating if the current material is [manual](../../../content/materials/index.md#manual_internal_materials).
### Return value

Current the current material is manual
## int isInternal () const

Returns the current value indicating if the current material is [internal](../../../content/materials/index.md#manual_internal_materials).
### Return value

Current the current material is internal
## int isReflection2D () const

Returns the current value indicating if the material has a 2D reflection texture.
### Return value

Current the material has a 2D reflection texture
## int isBrush () const

Returns the current value indicating if the material is used for brushes (`*.brush` or `*.basebrush` file extension).
### Return value

Current the material is used for brushes
## int isBase () const

Returns the current value indicating if the material is the [base](../../../content/materials/index.md#base_materials) one.
### Return value

Current the material is the base one
## int isHidden () const

Returns the current value indicating if the material is hidden.
### Return value

Current the material is hidden
## int isEditable () const

Returns the current value indicating if the material can be edited.
### Return value

Current the material can be edited
## void setViewportMask ( int mask )

Sets a new bit mask for rendering into the viewport. The material is rendered if its mask matches the player's one.
### Arguments

- *int* **mask** - The bit mask for rendering into the viewport

## int getViewportMask () const

Returns the current bit mask for rendering into the viewport. The material is rendered if its mask matches the player's one.
### Return value

Current bit mask for rendering into the viewport
## void setTwoSided ( int sided )

Sets a new value indicating if the material is two-sided.
### Arguments

- *int* **sided** - The the material is two-sided

## int isTwoSided () const

Returns the current value indicating if the material is two-sided.
### Return value

Current the material is two-sided
## int isAlphaTest () const

Returns the current value indicating if the material has an alpha test option enabled.
### Return value

Current the material has an alpha test option enabled
## int isForward () const

Returns the current value indicating if the material is rendered in the forward pass.
### Return value

Current the material is rendered in the forward pass
## int isDeferred () const

Returns the current value indicating if the material is rendered in the deferred pass.
### Return value

Current the material is rendered in the deferred pass
## int isWater () const

Returns the current value indicating if the material is rendered in the water pass.
### Return value

Current the material is rendered in the water pass
## void setTransparent ( int transparent )

Sets a new transparency type of the material. One of the [TRANSPARENT_*](#TRANSPARENT_NONE) values. If it is set to [TRANSPARENT_NONE](#TRANSPARENT_NONE) or *TRANSPARENT_DEFERRED*, the [source](#setBlendSrcFunc_int_void) and [destination](#setBlendDestFunc_int_void) blending functions are not used.
### Arguments

- *int* **transparent** - The transparency type of the material

## int getTransparent () const

Returns the current transparency type of the material. One of the [TRANSPARENT_*](#TRANSPARENT_NONE) values. If it is set to [TRANSPARENT_NONE](#TRANSPARENT_NONE) or *TRANSPARENT_DEFERRED*, the [source](#setBlendSrcFunc_int_void) and [destination](#setBlendDestFunc_int_void) blending functions are not used.
### Return value

Current transparency type of the material
## void setTransparentOrder ( int order )

Sets a new rendering order of transparent surfaces relative to SSR and post-effects. One of the [TRANSPARENT_ORDER_*](#TRANSPARENT_ORDER_BEFORE_SSR) values.
### Arguments

- *int* **order** - The rendering order of transparent surfaces relative to SSR and post-effects

## int getTransparentOrder () const

Returns the current rendering order of transparent surfaces relative to SSR and post-effects. One of the [TRANSPARENT_ORDER_*](#TRANSPARENT_ORDER_BEFORE_SSR) values.
### Return value

Current rendering order of transparent surfaces relative to SSR and post-effects
## int getNumTextures () const

Returns the current number of textures used by the material.
### Return value

Current number of textures used by the material
## int getNumStates () const

Returns the current number of the material's states.
### Return value

Current number of the material's states
## int getNumParameters () const

Returns the current number of the material's parameters.
### Return value

Current number of the material's parameters
## String getFilePath () const

Returns the current path to the current material file.
### Return value

Current path to the current material file
## UGUID getFileGUID () const

Returns the current GUID of the current material file.
### Return value

Current GUID of the current material file
## UGUID getGUID () const

Returns the current [GUID](../../../content/materials/inheritance.md#material_guid) of the material.
### Return value

Current GUID of the material
## int getNumChildren () const

Returns the current number of child materials.
### Return value

Current number of child materials
## Material getBaseMaterial () const

Returns the current base material of the current material.
### Return value

Current base material of the current material
## void setOrder ( int order )

Sets a new [rendering order](#setOrder_int_void) of materials, in the range from -128 to 127. The higher the rendering order, the lower the rendering priority (the material with the -128 order is rendered first).
### Arguments

- *int* **order** - The rendering order of materials

## int getOrder () const

Returns the current [rendering order](#setOrder_int_void) of materials, in the range from -128 to 127. The higher the rendering order, the lower the rendering priority (the material with the -128 order is rendered first).
### Return value

Current rendering order of materials
## void setOrderClouds ( int clouds )

Sets a new rendering order of transparent surfaces relative to clouds.
Takes effect only when the render_clouds_transparent_order console variable is set to 2 (Sort Transparent). One of the [*ORDER_CLOUDS_**](#ORDER_CLOUDS_DEFAULT) values.


> **Notice:** To render a transparent surface behind clouds, [Depth Test](#isDepthTest_int) should be disabled for the material, otherwise the surface will be rendered in front of clouds regardless of the OrderClouds value.

### Arguments

- *int* **clouds** - The rendering order of transparent surfaces relative to clouds

## int getOrderClouds () const

Returns the current rendering order of transparent surfaces relative to clouds.
Takes effect only when the render_clouds_transparent_order console variable is set to 2 (Sort Transparent). One of the [*ORDER_CLOUDS_**](#ORDER_CLOUDS_DEFAULT) values.


> **Notice:** To render a transparent surface behind clouds, [Depth Test](#isDepthTest_int) should be disabled for the material, otherwise the surface will be rendered in front of clouds regardless of the OrderClouds value.

### Return value

Current rendering order of transparent surfaces relative to clouds
## void setDepthTest ( int test )

Sets a new value indicating if depth testing is enabled for the material. This option can be used to render certain objects, that are behind other ones.
### Arguments

- *int* **test** - The depth testing is enabled for the material

## int isDepthTest () const

Returns the current value indicating if depth testing is enabled for the material. This option can be used to render certain objects, that are behind other ones.
### Return value

Current depth testing is enabled for the material
## void setShadowMask ( int mask )

Sets a new shadow mask of the material.
For the shadow to be rendered for a light source from an object's surface having this material assigned, this mask must match the following ones (one bit, at least):


- [Shadow mask of the light source](../../../api/library/lights/class.light_usc.md#setShadowMask_int_void)
- [Shadow mask of the surface](../../../api/library/objects/class.object_usc.md#setShadowMask_int_int_void) of the object having this material assigned


### Arguments

- *int* **mask** - The shadow mask of the material

## int getShadowMask () const

Returns the current shadow mask of the material.
For the shadow to be rendered for a light source from an object's surface having this material assigned, this mask must match the following ones (one bit, at least):


- [Shadow mask of the light source](../../../api/library/lights/class.light_usc.md#setShadowMask_int_void)
- [Shadow mask of the surface](../../../api/library/objects/class.object_usc.md#setShadowMask_int_int_void) of the object having this material assigned


### Return value

Current shadow mask of the material
## void setCastWorldShadow ( int shadow )

Sets a new value indicating if an object with the material applied casts shadows from the world light.
### Arguments

- *int* **shadow** - The an object with the material applied casts shadows from the world light

## int isCastWorldShadow () const

Returns the current value indicating if an object with the material applied casts shadows from the world light.
### Return value

Current an object with the material applied casts shadows from the world light
## void setCastShadow ( int shadow )

Sets a new value indicating if an object with the material applied casts shadows.
### Arguments

- *int* **shadow** - The an object with the material applied casts shadows

## int isCastShadow () const

Returns the current value indicating if an object with the material applied casts shadows.
### Return value

Current an object with the material applied casts shadows
## int isPreviewHidden () const

Returns the current value indicating if preview in UnigineEditor is disabled for the material. This is used for custom materials (e.g., landscape terrain brushes).
### Return value

Current preview in UnigineEditor is disabled for the material
## int isLegacy () const

Returns the current value indicating if the material is a legacy one. A legacy material is a non-ULON base material described in an XML file.
### Return value

Current the material is a legacy one
## void setBlendSrcFunc ( int func )

Sets a new source [blending](../../../principles/render/blending/index.md) function. One of the [BLEND_*](../../../api/library/rendering/class.renderstate_usc.md#BLEND_NONE) values.
### Arguments

- *int* **func** - The source blending function

## int getBlendSrcFunc () const

Returns the current source [blending](../../../principles/render/blending/index.md) function. One of the [BLEND_*](../../../api/library/rendering/class.renderstate_usc.md#BLEND_NONE) values.
### Return value

Current source blending function
## void setBlendDestFunc ( int func )

Sets a new destination [blending](../../../principles/render/blending/index.md) function. One of the [BLEND_*](../../../api/library/rendering/class.renderstate_usc.md#BLEND_NONE) values.
### Arguments

- *int* **func** - The destination blending function

## int getBlendDestFunc () const

Returns the current destination [blending](../../../principles/render/blending/index.md) function. One of the [BLEND_*](../../../api/library/rendering/class.renderstate_usc.md#BLEND_NONE) values.
### Return value

Current destination blending function
## void setBlendAlphaSrcFunc ( int func )

Sets a new source alpha [blending](../../../principles/render/blending/index.md) function. One of the [BLEND_*](../../../api/library/rendering/class.renderstate_usc.md#BLEND_NONE) values.
### Arguments

- *int* **func** - The source alpha blending function

## int getBlendAlphaSrcFunc () const

Returns the current source alpha [blending](../../../principles/render/blending/index.md) function. One of the [BLEND_*](../../../api/library/rendering/class.renderstate_usc.md#BLEND_NONE) values.
### Return value

Current source alpha blending function
## Material getParent () const

Returns the current parent material, or NULL (0) if the current material has no parent.
### Return value

Current parent material
## int getNumUIItems () const

Returns the current number of UI items. UI items represent material parameters, options, states, textures, and groups in UnigineEditor.
### Return value

Current number of UI items
## const char * getManualName () const

Returns the current name of the manual material.
### Return value

Current name of the manual material
## const char * getNamespaceName () const

Returns the current namespace where this material is defined.
### Return value

Current namespace where this material is defined
## unsigned int getFeatureBits () const

Returns the current bit mask of screen-space effect features enabled for the material (screen-space shadows, shoreline wetness, motion blur, SSAO, SSR, SSSSS, DOF). The bits are computed from the corresponding material states and are available to shaders in the material parameters structure.
### Return value

Current bit mask of screen-space effect features enabled for the material
## unsigned int getMaterialID () const

Returns the current runtime ID of the material. The ID is assigned by the engine on demand when the material is first rendered, is unique among live materials, and indexes the row of this material in the global GPU buffer of material parameters. IDs of removed materials are recycled. IDs below **[MATERIAL_MATERIAL_ID_RESERVED_NUM()](../../...md#MATERIAL_ID_RESERVED_NUM)** are reserved.
### Return value

Current runtime ID of the material
---

## static Material ( )

Constructor. Creates a new material instance.
## Material getChild ( int num )

Returns a child material with a given number.
### Arguments

- *int* **num** - Child material number.

### Return value

Child material.
## int isParameterExpressionEnabled ( int num )

Returns a value indicating if the value of the specified material parameter is represented by an expression in UnigineScript. Values of certain parameters can be calculated by an arbitrary expression, written in [UnigineScript](../../../code/uniginescript/index.md).
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).

### Return value

**1** if the value of the specified material parameter is represented by an expression in UnigineScript; otherwise, **0**.
## void setParameterExpressionEnabled ( int num , int enabled )

Sets a value indicating if the value of the specified material parameter is represented by an expression in UnigineScript. Values of certain parameters can be calculated by an arbitrary expression, written in [UnigineScript](../../../code/uniginescript/index.md).
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).
- *int* **enabled** - **1** to enable setting the values of the specified material parameter by an expression in UnigineScript; **0** - to disable.

## int isParameterOverridden ( int num )

Returns a value indicating if a given parameter is overridden.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).

### Return value

**1** if the given parameter is overridden; otherwise, **0**.
## void setParameter ( int num , Variable arg2 )

Sets a material's parameter value.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).
- *Variable* **arg2** - Parameter value.

## void setParameter ( string name , Variable arg2 )

Sets the specified value to the parameter with the given [name](#copy_name).
### Arguments

- *string* **name** - [Parameter name](#copy_name).
- *Variable* **arg2** - Parameter value to set.

## Variable getParameter ( string name )

Returns a value of the parameter with the given [name](#copy_name).
### Arguments

- *string* **name** - [Parameter name](#copy_name).

### Return value

Parameter value.
## Variable getParameter ( int num )

Returns a value of the parameter with the given number.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).

### Return value

Parameter value.
## int isParameterInt ( int num )

Returns a value indicating if the parameter with the specified number is an integer-type parameter.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).

### Return value

**1** if the parameter with the specified number is an [integer-type parameter](#PARAMETER_ARRAY_INT); otherwise, **0**.
## int isParameterFloat ( int num )

Returns a value indicating if the parameter with the specified number is a float-type parameter.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).

### Return value

**1** if the parameter with the specified number is an [float-type parameter](#PARAMETER_ARRAY_FLOAT); otherwise, **0**.
## int getParameterArraySize ( int num )

Returns the number of elements in the array parameter with the specified number.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).

### Return value

Number of elements of the specified array parameter.
## int isParameterArray ( int num )

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

**1** if the parameter is an array-type parameter; otherwise, **0**.
## void getParameterArray ( int num )

Returns a value of the array parameter (type: [*PARAMETER_ARRAY_FLOAT4*](#PARAMETER_ARRAY_FLOAT4)) with the specified number and puts it to the specified buffer array.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).

## void setParameterArray ( int num )

Sets a value of the array parameter (type: [*PARAMETER_ARRAY_FLOAT4*](#PARAMETER_ARRAY_FLOAT4)) with the specified number using the specified array.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).

## void setParameterArray ( Variable param , int values )

Sets a value of the array parameter (type: [*PARAMETER_ARRAY_FLOAT4*](#PARAMETER_ARRAY_FLOAT4)) with the specified number using the specified array.
### Arguments

- *Variable* **param** - Material parameter identifier. Can be of the following:

  - [Parameter name](#copy_name).
  - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).
- *int* **values** - ID of the array of values to be set.

## void getParameterArray ( Variable param , int values )

Returns a value of the array parameter with the specified number and puts it to the specified buffer array.
### Arguments

- *Variable* **param** - Material parameter identifier. Can be of the following:

  - [Parameter name](#copy_name).
  - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).
- *int* **values** - ID of the buffer array to store parameter values.

## int setParameterExpression ( int num , string expression )

Sets the expression used as a parameter value.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).
- *string* **expression** - New expression.

### Return value

1 if the expression is set successfully; otherwise, 0.
## string getParameterExpression ( int num )

Returns an expression used as a parameter value.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).

### Return value

Parameter expression, if it exists; otherwise, **NULL** (**0**).
## string getParameterName ( int num )

Returns the name of a given parameter.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).

### Return value

[Parameter name](#copy_name).
## int getParameterType ( int num )

Returns the type of a given parameter.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).

### Return value

One of the [*MATERIAL_PARAMETER_**](#PARAMETER_FLOAT) pre-defined variables or **-1**, if an error has occurred.
## bool isStateInternal ( int num )

Returns a value indicating if a given state is internal.
### Arguments

- *int* **num** - State number.

### Return value

**1** if the given state is internal; otherwise, **0**.
## int isStateOverridden ( int num )

Returns a value indicating if a given state is overridden.
### Arguments

- *int* **num** - State number.

### Return value

**1** if the given state is overridden; otherwise, **0**.
## void setState ( int num , int value )

Sets the state value.
### Arguments

- *int* **num** - State number.
- *int* **value** - State value to be set.

## void setState ( int value )

Sets the value of the given state.
### Arguments

- *int* **value** - State value.

## int getState ( int num )

Returns the state value. A 0 value returned by this method does not necessarily mean the value of the state, as you'll also get 0 in case the **state with the given number does not exist**. To check whether the state exists use **[findState()()](../../...md#findState_cstr_int)**. You should also be aware that states, parameters, and textures can be ignored in case [conditions](../../../code/formats/materials_formats/ulon_materials/states.md) they depend on are not met. To check conditions call **[checkStateConditions()()](../../...md#checkStateConditions_int_int)**.
### Arguments

- *int* **num** - State number.

### Return value

State value.
## int getState ( )

Returns the value of the given state. A 0 value returned by this method does not necessarily mean the value of the state, as you'll also get 0 in case the **state with the given name does not exist**. To check whether the state exists use **[findState()()](../../...md#findState_cstr_int)**. You should also be aware that states, parameters, and textures can be ignored in case [conditions](../../../code/formats/materials_formats/ulon_materials/states.md) they depend on are not met. To check conditions call **[checkStateConditions()()](../../...md#checkStateConditions_int_int)**.
### Arguments

### Return value

State value.
## string getStateName ( int num )

Returns the name of a given state.
### Arguments

- *int* **num** - State number.

### Return value

State name.
## string getStateSwitchItem ( int num , int item )

Returns the switch item name for a given state.
### Arguments

- *int* **num** - State number.
- *int* **item** - Item number.

### Return value

Switch item name or **NULL** (**0**), if an error has occurred.
## int getStateSwitchNumItems ( int num )

Returns the number of switch items for a given state.
### Arguments

- *int* **num** - State number.

### Return value

Number of switch items.
## int getStateType ( int num )

Returns the type of a given state.
### Arguments

- *int* **num** - State number.

### Return value

One of the [*MATERIAL_STATE_**](#STATE_INT) pre-defined variables or **-1**, if an error occurred.
## int isTextureInternal ( int num )

Returns a value indicating if a given texture is internal.
### Arguments

- *int* **num** - Texture number.

### Return value

**1** if the given texture is internal; otherwise, **0**.
## int isTextureOverridden ( int num )

Returns a value indicating if a given texture is overridden.
### Arguments

- *int* **num** - Texture number.

### Return value

**1** if the given texture is overridden; otherwise, **0**.
## int isTextureLoaded ( int num )

Returns a value indicating if a given texture is loaded.
### Arguments

- *int* **num**

### Return value

**1** if the given texture is loaded; otherwise, **0**.
## string getTextureName ( int num )

Returns the name of a given texture.
### Arguments

- *int* **num** - Texture number.

### Return value

Texture name.
## int getTextureUnit ( int num )

Returns the number of the unit for a given texture used in shaders.
### Arguments

- *int* **num** - Texture number.

### Return value

Texture unit number.
## int isTextureEditable ( int num )

Returns a value indicating if the texture with the specified number is editable (can be modified).
### Arguments

- *int* **num** - Texture number.

### Return value

**1** if the texture with the specified number is editable; otherwise, **0** (the texture is read-only).
## int getTextureSource ( int num )

Returns the source for the texture with the specified number.
### Arguments

- *int* **num** - Texture number.

### Return value

One of the **[MATERIAL_TEXTURE_SOURCE_*()](../../...md#TEXTURE_SOURCE_AUXILIARY)** pre-defined variables or **-1**, if an error has occurred.
## int findParameter ( string name )

Searches for a parameter by a given [name](#copy_name) among all parameters of the current material.
### Arguments

- *string* **name** - [Parameter name](#copy_name).

### Return value

Parameter number, if it is found; otherwise, **-1**.
## int findState ( string name )

Searches for a state by a given name among all states of the current material.
### Arguments

- *string* **name** - State name.

### Return value

State number, if it is found; otherwise, **-1**.
## int findTexture ( string name )

Searches for a texture by a given [name](#copy_name) among all textures used by the current material.
### Arguments

- *string* **name** - [Texture name](#copy_name).

### Return value

Texture number, if it is found; otherwise, **-1**.
## int saveState ( Stream stream , int forced = 0 )

Saves the settings of a given material (all of its options, states and parameters) into a binary stream.


Saving into the stream requires creating a blob to save into. To restore the saved state the [restoreState()](#restoreState_Stream_int_int) method is used:


```cpp
// initialize object
Material mat = object.getMaterial(0);
mat.setViewportMask(1); // viewport mask = 1

// save state
Blob blob_state = new Blob();
mat.saveState(blob_state);

// change something
mat.setViewportMask(~0);  // now viewport mask = 111111111

// restore state
blob_state.seekSet(0);		// returning the carriage to the start of the blob
mat.restoreState(blob_state);  // restore viewport mask = 1

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - The stream to save material state data.
- *int* **forced** - Forced saving of material settings.

### Return value

**1** if the material settings are saved successfully; otherwise, **1**.
## int restoreState ( Stream stream , int forced = 0 )

Restores the state of a given material (all of its options, states and parameters) from a binary stream.


Restoring from the stream requires creating a blob to save into and saving the state using the [saveState()](#saveState_Stream_int_int) method:


```cpp
// initialize object
Material mat = object.getMaterial(0);
mat.setViewportMask(1); // viewport mask = 1

// save state
Blob blob_state = new Blob();
mat.saveState(blob_state);

// change something
mat.setViewportMask(~0);  // now viewport mask = 111111111

// restore state
blob_state.seekSet(0);		// returning the carriage to the start of the blob
mat.restoreState(blob_state);  // restore viewport mask = 1

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - The stream with saved material data.
- *int* **forced** - Forced restoring of material settings.

### Return value

**1** if the material settings are restored successfully; otherwise, **0**.
## int canRenderNode ( )

Returns a value indicating if the material can be rendered for at least one [type](../../../api/library/nodes/class.node_usc.md#DECAL_MESH) of nodes.
### Return value

**1** if the material is rendered for at least one type of nodes; otherwise, **0**.
## void resetState ( int num )

Resets the [overridden](#isStateOverridden_int_int) value of the given state to the parent one.
### Arguments

- *int* **num** - State number.

## void setTexturePath ( int num )

Sets a new path to the texture with the given number.
### Arguments

- *int* **num** - Texture number.

## void setTexturePath ( )

Sets a new path to the texture with the given [name](#copy_name).
### Arguments

## void resetTexture ( int num )

Resets the [overridden](#isTextureOverridden_int_int) value of the given texture to the parent one.
### Arguments

- *int* **num** - Texture number.

## getTexturePath ( int num )

Returns a path to the texture with the specified number.
### Arguments

- *int* **num** - Texture number.

### Return value

A path to the texture.
## getTexturePath ( )

Returns a path to the texture with the specified [name](#copy_name).
### Arguments

### Return value

A path to the texture.
## int isNodeTypeSupported ( int type )

Returns a value indicating if the given type of nodes is supported by the material.
### Arguments

- *int* **type** - Node type: one of the *[OBJECT_*](../../../api/library/nodes/class.node_usc.md#OBJECT_BILLBOARDS)* or *[DECAL_*](../../../api/library/nodes/class.node_usc.md#DECAL_MESH)* variables.

### Return value

**1** if the node type is supported; otherwise, **0**.
## int setParent ( Material material , int save_all_values = 1 )

Sets the given material as the parent for this material and saves the material's properties values (if the corresponding flag is set).


> **Notice:** The method isn't available for the [manual](#isManual_int) and [base](#isBase_int) materials.


### Arguments

- *[Material](../../../api/library/rendering/class.material_usc.md)* **material** - Material to be set as the parent for this material.
- *int* **save_all_values** - Flag indicating if the material's properties will be saved after reparenting.

### Return value

**1** if the material's parent is changed; otherwise, **0**.
## int checkTextureConditions ( int num )

Checks if [conditions](../../../code/formats/materials_formats/ulon_materials/conditions.md) set for the given texture are met.
### Arguments

- *int* **num** - Texture number.

### Return value

**1** if conditions are met; otherwise, **0**.
## int loadXml ( Xml xml )

Loads material settings from the specified Xml source.
### Arguments

- *[Xml](../../../api/library/common/class.xml_usc.md)* **xml** - An Xml node containing material settings.

### Return value

**1** if the material settings are loaded successfully; otherwise, **0**.
## int loadUlon ( UlonNode ulon )

Loads material settings from the specified [ULON](../../../code/formats/ulon_format.md) source.
### Arguments

- *[UlonNode](../../../api/library/common/class.ulonnode_usc.md)* **ulon** - A ULON-node containing material settings.

### Return value

**1** if the material settings are loaded successfully; otherwise, **0**.
## int hasOverrides ( )

Returns a value indicating if the material has at least one overridden property.
### Return value

**1** if the material has at least one overridden property; otherwise, **0**.
## int canSave ( )

Returns a value indicating if the material can be saved. For example, this function will return 0 for a base or manual material.
### Return value

**1** if the material can be saved; otherwise, **0**.
## int checkStateConditions ( int num )

Checks if [conditions](../../../code/formats/materials_formats/ulon_materials/states.md) set for the given state are met.
### Arguments

- *int* **num** - State number.

### Return value

**1** if conditions are met; otherwise, **0**.
## int checkParameterConditions ( int num )

Checks if [conditions](../../../code/formats/materials_formats/ulon_materials/parameters.md) set for the given parameter are met.
### Arguments

- *int* **num** - [Parameter name](#copy_name).

### Return value

**1** if conditions are met; othersiwe, **0**.
## int save ( )

Save the material to the [current path](#getFilePath_String) used for this material.


> **Notice:** The method isn't available for the [manual](#isManual_int) and [base](#isBase_int) materials.


### Return value

**1** if the material is saved successfully; otherwise, **0**.
## int load ( string path )

Loads a material from the given file. The function can be used to load materials created during application execution or stored outside the `data` directory.
### Arguments

- *string* **path** - A path to the material file.

### Return value

**1** if the material is loaded successfully; otherwise, **0**.
## int saveXml ( Xml xml )

Saves the material into the given Xml.


> **Notice:** The method isn't available for the [manual](#isManual_int) and [base](#isBase_int) materials.


### Arguments

- *[Xml](../../../api/library/common/class.xml_usc.md)* **xml** - An Xml node.

### Return value

**1** if the material is saved successfully; otherwise, **0**.
## int isNodeSupported ( Node node )

Returns a value indicating if the material can be applied to the given node.
### Arguments

- *[Node](../../../api/library/nodes/class.node_usc.md)* **node** - A node.

### Return value

**1** if the given node is supported; otherwise, **0**.
## void setTexture ( int num , Texture texture )

Sets the given texture to the texture with the specified number.
### Arguments

- *int* **num** - Texture number.
- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - Texture to be set.

## getTexture ( int num )

Returns a texture set for the current material. You should be aware that states, parameters, and textures can be ignored in case [conditions](../../../code/formats/materials_formats/ulon_materials/states.md) they depend on are not met. To check conditions call **[checkTextureConditions()()](../../...md#checkTextureConditions_int_int)**.
### Arguments

- *int* **num** - Texture number.

### Return value

Texture used with the given number if it exists; otherwise *nullptr*.
## UGUID getFileGUID ( )

Returns a GUID of the current material file.
### Return value

GUID of the current material file.
## void resetParameter ( int num )

Resets the [overridden](#isParameterOverridden_int_int) value of the given parameter to the parent one.
### Arguments

- *int* **num** - Parameter number in the range from 0 to the [total number of parameters](#getNumParameters_int).

## int reload ( )

Reloads the material and all its children.
### Return value

**1** if the material is reloaded successfully; otherwise, **0**.
## int setTextureImage ( int num , Image image )

Set a given [image](../../../api/library/common/class.image_usc.md) to a given texture.
### Arguments

- *int* **num** - Texture number.
- *[Image](../../../api/library/common/class.image_usc.md)* **image** - An image to set.

### Return value

1 if the image is set successfully; otherwise, 0.
## int getTextureImage ( int num , Image image )

Reads a given texture into a given image.
### Arguments

- *int* **num** - Texture number.
- *[Image](../../../api/library/common/class.image_usc.md)* **image** - An image.

### Return value

1 if the texture is read successfully; otherwise, 0.
## TextureRamp getTextureRamp ( int num )

Returns a [ramp texture](../../../api/library/rendering/class.textureramp_usc.md) instance for the data stored in the specified ramp texture (gradient).


> **Notice:** Modifications made to the ramp shall propagate to the parent and sibling materials. To modify an overridden ramp for this material only use the [*getTextureRampOverride()*](#getTextureRampOverride_int_TextureRamp) method.


### Arguments

- *int* **num** - Texture number.

### Return value

[TextureRamp](../../../api/library/rendering/class.textureramp_usc.md) class instance for the data stored in the gradient texture with the specified number.
## TextureRamp getTextureRampOverride ( int num )

Returns a new [ramp texture](../../../api/library/rendering/class.textureramp_usc.md) instance for the data stored in the specified ramp texture (gradient) overriding the default one. This method enables you to set individual RGBA curves, adjusting color values of the resulting ramp texture (gradient).


> **Notice:** Modifications made to the ramp shall not propagate to the parent and sibling materials.


### Arguments

- *int* **num** - Texture number.

### Return value

New [TextureRamp](../../../api/library/rendering/class.textureramp_usc.md) class instance overriding the data stored in the specified ramp texture (gradient).
## void createShaders ( int recursive = 0 )

Creates all shaders for the current material and its children (if specified).
### Arguments

- *int* **recursive** - **1** to create shaders for child materials of the current material; otherwise, **0**.

## void destroyTextures ( )

Deletes all textures used by the current material and its children.
## int getRenderPass ( string pass_name )

Returns the type of the rendering pass by its name (including custom passes).
### Arguments

- *string* **pass_name** - Name of the rendering pass.

### Return value

Rendering pass number in the range from 0 to 18 + custom_passes_number, if it exists; otherwise -1.
## string getRenderPassName ( int type )

Returns the name of the rendering pass by its number (including custom passes).
### Arguments

- *int* **type** - Rendering pass number in range [0;[NUM_PASSES](../../../api/library/rendering/class.render_usc.md#NUM_PASSES)) (one of the *[PASS_*](../../../api/library/rendering/class.render_usc.md#PASS_WIREFRAME)* variables).

### Return value

Rendering pass name if it exists; otherwise NULL.
## int runExpression ( string name , int w , int h , int d = 1 )

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

**1** if the specified expression is executed successfully; otherwise, **0**.
## int renderScreen ( string pass_name )

Renders the screen-space material. The material must have a shader for the specified pass associated with it.
### Arguments

- *string* **pass_name** - Name of the rendering pass.

### Return value

**0** if the specified pass was not found; otherwise, **1**.
## int renderCompute ( string pass_name , int group_threads_x = 1 , int group_threads_y = 1 , int group_threads_z = 1 )

Renders the material using a compute shader. The material must have a compute shader for the specified pass associated with it.
### Arguments

- *string* **pass_name** - Name of the rendering pass.
- *int* **group_threads_x** - Local X work-group size of the compute shader.
- *int* **group_threads_y** - Local Y work-group size of the compute shader.
- *int* **group_threads_z** - Local Z work-group size of the compute shader.

### Return value

**0** if the specified pass was not found; otherwise, **1**.
## int getUIItemDataType ( int item )

Returns the type of data of the specified UI item. UI items represent material parameters, options, states, textures, and groups in UnigineEditor.
### Arguments

- *int* **item** - UI item index in the range from 0 to the [total number of UI items](#getNumUIItems_int).

### Return value

UI item data type (parameter, option, state, texture, or group).
## int getUIItemDataID ( int item )

Returns the id of the data type controlled by the specified UI item. UI items represent material parameters, options, states, textures, and groups in UnigineEditor.
### Arguments

- *int* **item** - UI item index in the range from 0 to the [total number of UI items](#getNumUIItems_int).

### Return value

UI item data id: one of the *[STATE_*](#STATE_INT)*, *[PARAMETER_*](#PARAMETER_INT)*, *[OPTION_*](#OPTION_TRANSPARENT)*, *[TEXTURE_SOURCE_*](#TEXTURE_SOURCE_ASSET)* pre-defined variables or -1, if an error has occurred.
## int isUIItemHidden ( int item )

Returns a value indicating if the specified UI item is hidden.
### Arguments

- *int* **item** - UI item index in the range from 0 to the [total number of UI items](#getNumUIItems_int).

### Return value

**1** is the specified UI item is hidden; otherwise, **0**.
## string getUIItemTitle ( int item )

Returns the title set for the specified UI item.
### Arguments

- *int* **item** - UI item index in the range from 0 to the [total number of UI items](#getNumUIItems_int).

### Return value

Title set for the specified UI item.
## string getUIItemTooltip ( int item )

Returns the text of the tooltip set for the specified UI item.
### Arguments

- *int* **item** - UI item index in the range from 0 to the [total number of UI items](#getNumUIItems_int).

### Return value

Text of the tooltip set for the specified UI item.
## int getUIItemWidget ( int item )

Returns the type of the widget for the specified UI item.
### Arguments

- *int* **item** - UI item index in the range from 0 to the [total number of UI items](#getNumUIItems_int).

### Return value

UI item widget type.
## int getUIItemParent ( int item )

Returns an index of the parent of the specified UI item. This method is used to get the index of the group to which the specified parameter/state/option/texture belongs.
### Arguments

- *int* **item** - UI item index in the range from 0 to the [total number of UI items](#getNumUIItems_int).

### Return value

Global index of the parent UI element in the range from 0 to the [total number of UI items for the material](#getNumUIItems_int).
## int getUIItemNumChildren ( int item )

Returns the number of child items for the group UI item with the specified number.


> **Notice:** This method is to be used for UI item groups only ([DATA_TYPE_GROUP](#DATA_TYPE_GROUP)), other items cannot have children!


### Arguments

- *int* **item** - UI item group index in the range from 0 to the [total number of UI items](#getNumUIItems_int).

### Return value

Number of child items for the specified group UI item.
## int getUIItemChild ( int item , int num )

Returns the index of a child UI item that belongs to the specified group by the item number within the group.


> **Notice:** This method is to be used for UI item groups only ([DATA_TYPE_GROUP](#DATA_TYPE_GROUP)), other items cannot have children!


### Arguments

- *int* **item** - UI item group index in the range from 0 to the [total number of UI items](#getNumUIItems_int).
- *int* **num** - Number of UI item within the group (in the list of children).

### Return value

Global index of the child UI element in the range from 0 to the [total number of UI items for the material](#getNumUIItems_int).
## int isUIItemSliderMinExpand ( int item )

Returns a value indicating if the maximum slider value for the specified UI item can be increased.
### Arguments

- *int* **item** - UI item index in the range from 0 to the [total number of UI items](#getNumUIItems_int).

### Return value

**1** if the maximum value can be increased; otherwise, **0**.
## int isUIItemSliderMaxExpand ( int item )

Returns a value indicating if the minimum slider value for the specified UI item can be decreased.
### Arguments

- *int* **item** - UI item index in the range from 0 to the [total number of UI items](#getNumUIItems_int).

### Return value

**1** if the minimum value can be decreased; otherwise, **0**.
## float getUIItemSliderMinValue ( int item )

Returns the minimum allowed value of the slider for the specified UI item.
### Arguments

- *int* **item** - UI item index in the range from 0 to the [total number of UI items](#getNumUIItems_int).

### Return value

Minimum value of the slider.
## float getUIItemSliderMaxValue ( int item )

Returns the maximum allowed value of the slider for the specified UI item.
### Arguments

- *int* **item** - UI item index in the range from 0 to the [total number of UI items](#getNumUIItems_int).

### Return value

Maximum value of the slider.
## int getUIItemGroupToggleStateID ( int item )

Returns the global index of the state toggle UI element turning the specified group on and off.


> **Notice:** This method is to be used for UI item groups only ([DATA_TYPE_GROUP](#DATA_TYPE_GROUP))!


### Arguments

- *int* **item** - UI item index in the range from 0 to the [total number of UI items](#getNumUIItems_int).

### Return value

Global index of the state toggle UI element in the range from 0 to the [total number of UI items for the material](#getNumUIItems_int).
## int isUIItemGroupCollapsed ( int item )

Returns a value indicating if the specified group of UI items is currently collapsed in the UI of the Unigine Editor.


> **Notice:** This method is to be used for UI item groups only ([DATA_TYPE_GROUP](#DATA_TYPE_GROUP))!


### Arguments

- *int* **item** - UI item index in the range from 0 to the [total number of UI items](#getNumUIItems_int).

### Return value

**1** if the specified group of UI items is currently collapsed in the UI; otherwise, **0** (the group is expanded).
## void setOption ( int num , int value )

Sets a new value for the specified option.
### Arguments

- *int* **num** - Option number.
- *int* **value** - New value to be set for the specified option.

## int getOption ( int num )

Returns the current value of the specified option.
### Arguments

- *int* **num** - Option number.

### Return value

Current value of the specified option.
## int isOptionOverridden ( int num )

Returns a value indicating if a given option is overridden.
### Arguments

- *int* **num** - Option number.

### Return value

**1** if the given option is overridden; otherwise, **0**.
## void resetOption ( int num )

Resets the [overridden](#isOptionOverridden_int_int) value of the given option to the parent one.
### Arguments

- *int* **num** - Option number.

## int isParent ( Material parent )

Returns a value indicating if the given material is a parent of the current material.
### Arguments

- *[Material](../../../api/library/rendering/class.material_usc.md)* **parent**

### Return value

**1** if the material is the parent, otherwise - **0**.
## Material clone ( )

Clones the material. The cloned material will be empty: it will have a GUID but won't be displayed in the materials hierarchy.
### Return value

Cloned material.
## Material clone ( UGUID guid )

Clones the material and assigns the given GUID to it.
> **Notice:** A [base material](../../../content/materials/index.md#base_materials) cannot be cloned.

### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - Cloned material GUID.

### Return value

Cloned material.
## Material inherit ( )

Inherits the material. The inherited material will be empty: it will have a GUID but won't be displayed in materials hierarchy.
### Return value

Inherited material.
## Material inherit ( UGUID guid )

Inherits a new material from the current one and assigns the specified GUID to it.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - Inhereted material GUID.

### Return value

Inhereted material.
## string widgetToString ( int widget )

Returns the name of the widget by its type.
### Arguments

- *int* **widget** - [Widget type](#WIDGET).

### Return value

Name of the widget.
## int stringToWidget ( string str )

Returns the widget type by its name.
### Arguments

- *string* **str** - Name of the widget.

### Return value

[Widget type](#WIDGET).
## int getTextureSamplerFlags ( int num )

Returns the sampler flags of the texture with the given number.
### Arguments

- *int* **num** - Number of the texture.

### Return value

Texture sampler flags.
## void setTextureSamplerFlags ( int num , int sampler_flags )

Sets the sampler flags for the texture with the given number.
### Arguments

- *int* **num** - Number of the texture.
- *int* **sampler_flags** - Sampler flags.

## int getTextureFormatFlags ( int num )

Returns the format flags of the texture with the given number.
### Arguments

- *int* **num** - Number of the texture.

### Return value

Texture format flags.
## int createMaterialFile ( string path )

Creates a file and saves the [internal](../../../content/materials/index.md#manual_internal_materials) material to it.
### Arguments

- *string* **path** - A path to save the material

### Return value

The value indicating if the material was successful saved.
## Shader getShaderAsync ( int pass , int node )

Returns the [rendering shader](../../../api/library/rendering/class.shader_usc.md) for the specified rendering pass and [node type](../../../api/library/nodes/class.node_usc.md#TYPE):


- If the shader has been compiled previously, the function will return it immediately.
- If the shader hasn't been compiled yet, the function will initiate its asynchronous compilation in another thread and return the successfully compiled shader. > **Notice:** The function will keep returning null until the shader is compiled.


> **Notice:** To compile the shader asynchronously, enable the [asynchronous compilation mode](../../../api/library/rendering/class.render_usc.md#getShadersCompileMode_int). Otherwise, the function will work the same as *[getShaderForce()](#getShaderForce_int_int_Shader)*.


### Arguments

- *int* **pass** - Rendering pass number in range [0;[NUM_PASSES](../../../api/library/rendering/class.render_usc.md#NUM_PASSES)) (one of the *[PASS_*](../../../api/library/rendering/class.render_usc.md#PASS_WIREFRAME)* variables).
- *int* **node** - [Node type](../../../api/library/nodes/class.node_usc.md#TYPE).

### Return value

Shader for the specified rendering pass and node type, if compiled successfully. Otherwise, null.
## Shader getShaderAsync ( int pass )

Returns the [rendering shader](../../../api/library/rendering/class.shader_usc.md) for the specified rendering pass:


- If the shader has been compiled previously, the function will return it immediately.
- If the shader hasn't been compiled yet, the function will initiate its asynchronous compilation in another thread and return the successfully compiled shader. > **Notice:** The function will keep returning null until the shader is compiled.


> **Notice:** To compile the shader asynchronously, enable the [asynchronous compilation mode](../../../api/library/rendering/class.render_usc.md#getShadersCompileMode_int). Otherwise, the function will work the same as *[getShaderForce()](#getShaderForce_int_Shader)*.


### Arguments

- *int* **pass** - Rendering pass number in range [0;[NUM_PASSES](../../../api/library/rendering/class.render_usc.md#NUM_PASSES)) (one of the *[PASS_*](../../../api/library/rendering/class.render_usc.md#PASS_WIREFRAME)* variables).

### Return value

Shader for the specified rendering pass, if compiled successfully. Otherwise, null.
## Shader getShaderForce ( int pass , int node )

Returns the [rendering shader](../../../api/library/rendering/class.shader_usc.md) for the specified rendering pass and [node type](../../../api/library/nodes/class.node_usc.md#TYPE):


- If the shader has been compiled previously, the function will return it immediately.
- If the shader hasn't been compiled yet, the function will immediately compile and return it.


> **Notice:** The function causes a spike because it compiles the shader in the current thread.


### Arguments

- *int* **pass** - Rendering pass number in range [0;[NUM_PASSES](../../../api/library/rendering/class.render_usc.md#NUM_PASSES)) (one of the *[PASS_*](../../../api/library/rendering/class.render_usc.md#PASS_WIREFRAME)* variables).
- *int* **node** - [Node type](../../../api/library/nodes/class.node_usc.md#TYPE).

### Return value

Shader for the specified rendering pass and node type, if compiled successfully. Otherwise, null.
## Shader getShaderForce ( int pass )

Returns the [rendering shader](../../../api/library/rendering/class.shader_usc.md) for the specified rendering pass:


- If the shader has been compiled previously, the function will return it immediately.
- If the shader hasn't been compiled yet, the function will immediately compile and return it.


> **Notice:** The function causes a spike because it compiles the shader in the current thread.


### Arguments

- *int* **pass** - Rendering pass number in range [0;[NUM_PASSES](../../../api/library/rendering/class.render_usc.md#NUM_PASSES)) (one of the *[PASS_*](../../../api/library/rendering/class.render_usc.md#PASS_WIREFRAME)* variables).

### Return value

Shader for the specified rendering pass, if compiled successfully. Otherwise, null.
## void setTextureStreamingDensityMultiplier ( int num , float streaming_density_multiplier )

Sets a multiplier adjusting the distance at which the texture mipmaps are rendered.
### Arguments

- *int* **num** - Number of the texture.
- *float* **streaming_density_multiplier** - Multiplier applied to the texture mipmaps rendering distance.

## float getTextureStreamingDensityMultiplier ( int num )

Returns the current adjusting the distance at which the texture mipmaps are rendered.
### Arguments

- *int* **num** - Number of the texture.

### Return value

Multiplier applied to the texture mipmaps rendering distance.
## int needCreateShaderCache ( )

Returns a value indicating if shader cache needs to be created for current material states and options.
### Return value

**1** if shader cache is required for current material states and options; or **0**, if shader combination for current material states and options is already in cache.
## int needCreateShaderCache ( int pass , int node_type )

Returns a value indicating if shader combination needs to be created for the given rendering pass and node type.
### Arguments

- *int* **pass** - Rendering pass number in range [0;[NUM_PASSES](../../../api/library/rendering/class.render_usc.md#NUM_PASSES)) (one of the *[PASS_*](../../../api/library/rendering/class.render_usc.md#PASS_WIREFRAME)* variables).
- *int* **node_type** - Node type.

### Return value

**1** if shader cache needs to be created for the given rendering pass and node type; or **0**, if shader combination for the given rendering pass and node type is already in cache.
## int shaderCacheExist ( int pass , int node_type )

Returns a value indicating if shader combination for the given rendering pass and node type is already in cache.
### Arguments

- *int* **pass** - Rendering pass number in range [0;[NUM_PASSES](../../../api/library/rendering/class.render_usc.md#NUM_PASSES)) (one of the *[PASS_*](../../../api/library/rendering/class.render_usc.md#PASS_WIREFRAME)* variables).
- *int* **node_type** - Node type.

### Return value

**1** if shader combination for the given rendering pass and node type is already in cache; otherwise, **0**.
## void createShaderForce ( int pass , int node_type )

Compiles shader combination for the given rendering pass and node type. Shaders are compiled immediately, which may cause spikes, therefore this method is recommended only for critical cases, where  doesn't ensure a satisfying result.
### Arguments

- *int* **pass** - Rendering pass number in range [0;[NUM_PASSES](../../../api/library/rendering/class.render_usc.md#NUM_PASSES)) (one of the *[PASS_*](../../../api/library/rendering/class.render_usc.md#PASS_WIREFRAME)* variables).
- *int* **node_type** - Node type.

## void createShaderAsync ( int pass , int node_type )

Compiles shader combination for the given rendering pass and node type. Shaders are compiled asynchronously, which ensures smooth performance without spikes and is suitable for most cases. For the shaders that requre to be compiled immediately, use .
### Arguments

- *int* **pass** - Rendering pass number in range [0;[NUM_PASSES](../../../api/library/rendering/class.render_usc.md#NUM_PASSES)) (one of the *[PASS_*](../../../api/library/rendering/class.render_usc.md#PASS_WIREFRAME)* variables).
- *int* **node_type** - Node type.

## void createRenderMaterials ( )

Creates render materials (internal materials required for rendering). For example, you can create all necessary render materials during initialization to avoid spikes that may occur later.
## void createShaderCache ( int recursive = false , int force = false )

Compiles and caches all shader permutations needed by this material for every render pass and node type. With asynchronous compilation the material may render with a fallback until the shaders are ready.
### Arguments

- *int* **recursive** - Flag defining whether the shader cache is also created for all inherited (child) materials, recursively.
- *int* **force** - Flag defining whether missing shaders are compiled immediately (blocking); otherwise the compilation is queued to run asynchronously in the background.

## void createShadersFromCache ( int recursive = false )

Compiles all shaders available in shader cache for the current material and its children (if any).
### Arguments

- *int* **recursive** - **1** to compile shaders for child materials; otherwise, **0**.

## int isCustomParameterOverridden ( int num )

Checks if the value of the custom material parameter with the given number is overridden by this material rather than inherited. For a material without a parent, this method always returns false.
### Arguments

- *int* **num** - Parameter number.

### Return value

**1** if the parameter value is overridden by this material; otherwise, **0**.
## int isCustomParametersSupported ( )

Checks if custom material parameters are supported for this material. Custom parameters are available only for materials that can be assigned to nodes (e.g. post-process and scriptable materials do not support them).
### Return value

**1** if custom material parameters are supported for the material; otherwise, **0**.
## void resetCustomParameter ( int num )

Resets the override of the custom material parameter with the given number: the value is inherited from the parent material again. This method has no effect on base materials.
### Arguments

- *int* **num** - Parameter number.

## void resetCustomParameters ( )

Resets the overrides of all custom material parameters of the material.
