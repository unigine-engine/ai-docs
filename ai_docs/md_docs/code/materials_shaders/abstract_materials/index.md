# Abstract Materials


To simplify shaders programming and hide the implementation complexity of various features, Abstract Materials were added. Like abstract classes in object-oriented programming, they serve as a template definition of certain parameters and functionality.


An abstract material itself cannot be assigned to objects, it is used to inherit other abstract and base materials from it, extending its functionality, which gives you a lot of flexibility.


You can create your own custom abstract material or use the ones provided "out of the box" *[Mesh](../../../code/materials_shaders/abstract_materials/mesh.md) / [Mesh Transparent](../../../code/materials_shaders/abstract_materials/mesh_transparent.md) / [Mesh Unlit](../../../code/materials_shaders/abstract_materials/mesh_unlit.md) / [Decal](../../../code/materials_shaders/abstract_materials/decal.md)* with or without tessellation to create a custom base material.


> **Notice:** It is impossible to create an instance of an abstract material.


## Inheritance and Override


By inheriting from an abstract material you can override any values and add some other components to the child material:


```glsl
AbstractMaterial A
{
		Slider t = 0.5
}

BaseMaterial B <parent = A>
{
		Slider t = 1.0
		Slider t2 = 2.0
}

```


> **Notice:** The abstract materials don�t support multiple inheritance.


When the child material implements the shader with the same name, the source code of the parent and the child shader is merged (the parent shader code precedes the child one):


```glsl
AbstractMaterial A
{
		Shader example =
		#{
				// A_fragment
		#}
}

AbstractMaterial B <parent = A>
{
		Shader example =
		#{
				// B_fragment
		#}
}

// the result example shader for the abstract material B will look like this:
Shader example =
#{
		// A_fragment
		// B_fragment
#}


```


You can expand and include the code of another shader by using inheritance and the marker **#shader shader_name**.


```glsl
AbstractMaterial A
{
		// including the different shader code
		Shader a =
		#{
				// shader code A
				#shader b
		#}

		Shader b =
		#{
				// shader code B1
		#}
}

AbstractMaterial B <parent = A>
{
		// expanding the parent shader code
		Shader b =
		#{
				// shader code B2
		#}
}

// the resulting example shader for the abstract material B will look like this:
Shader a =
#{
		// shader code A
		// shader code B1
		// shader code B2
#}

```


The same rules apply to the [Script](../../../code/formats/materials_formats/ulon_materials/scripts.md) code (use **#script script_name** as a marker).


Elements in parent and child materials' [Groups](../../../code/formats/materials_formats/ulon_materials/groups.md) with the same name can be merged. Both groups should have the **merge_group** argument set to true. The first group entry defines the place in the Editor�s UI where all the elements of this group are positioned (parent and child):


```glsl
AbstractMaterial A
{
		Group A1
		{
				Slider T1

				Group example <merge_group=true>
				{
					   Slider T2
				}
		}
}

BaseMaterial B <parent = A>
{
		Group B1
		{
				Slider T3

				Group example <merge_group=true>
				{
					   Slider T4
				}
		}
}

// the result grouping for the BaseMaterial B will look like this ("example" in the BaseMaterial B is merged with the parent example group):
Group A1
{
		Slider T1

		Group example
		{
			   Slider T2
			   Slider T4
		}
}

Group B1
{
		Slider T3
}


```


> **Notice:** Groups in the same material can have identical names. If all those groups do not have the **merge_group** argument set to true, they will be shown in the Editor's UI as separate groups.


## Comparison with Traditional Base Material logic


Abstract materials generalize internal logic and provide the simplified input and output interface for derived base materials. The traditional approach involves a lot of repetitive work to create materials with different shading for the same types of objects. Therefore it is recommended to use the abstract and base material mix. See the following examples that help achieve the same modified SSAO effect.


### Combination of Abstract and Base Material


This example demonstrates how the Abstract and the Base Material are combined.


<details>
<summary>Abstract Material (my_abstract.abstmat) | Close</summary>

`my_abstract.abstmat`


```glsl
AbstractMaterial <preview_hidden=true var_prefix=var texture_prefix=tex>
{
	Texture2D color <source=procedural>

	Shader common=
	#{
	#}

	Shader base_shader=
	#{
		#include <core/materials/shaders/render/common.h>

		STRUCT_FRAG_BEGIN
			INIT_COLOR(float4)
		STRUCT_FRAG_END

		#shader common

		MAIN_FRAG_BEGIN(FRAGMENT_IN)
			#shader fragment
		MAIN_FRAG_END
	#}

	Pass post
	{
		Fragment=base_shader
	}

	Expression RENDER_CALLBACK_END_POST_MATERIALS=
	#{
		Texture source = engine.render.getTemporaryTexture(engine.render_state.getScreenColorTexture());

		source.copy(engine.render_state.getScreenColorTexture());
		setTexture("color", source);
		renderPassToTexture("post", engine.render_state.getScreenColorTexture());

		engine.render.releaseTemporaryTexture(source);
	#}
}


```

</details>


<details>
<summary>Base Material (my_base.basemat) | Close</summary>

`my_base.basemat`


```glsl
BaseMaterial <parent=my_abstract>
{
	Texture2D normal <source=gbuffer_normal>
	Texture2D scene_depth <source=current_depth>
	Texture2D modulation = "core/textures/common/checker_d.texture"
	Texture2D <source=ssao>

	Slider global_scale = 2

	Shader common=
	#{
		float3 triplanar_sample(float2 uv, float depth_in)
		{
			float3 normal_ws = mul3(s_imodelview, unpackGBufferNormal(TEXTURE(tex_normal, uv).rgb));
			float3 position_ws = s_camera_position + mul3(s_imodelview, nativeDepthToPositionVS(depth_in, uv));

			float4 texcoord = position_ws.xyyz * var_global_scale;
			float3 weight = triplanarWeightFast(normal_ws, 0.5f);

			return TEXTURE_TRIPLANAR(tex_modulation, texcoord, weight).rgb;
		}

		float4 final(float2 uv, float depth_in)
		{
			float4 base = TEXTURE(tex_color, uv);
			float ssao = TEXTURE(tex_ssao, uv).r;

			float3 effect = triplanar_sample(uv, depth_in);
			return float4(lerp(base.rgb * effect, base.rgb, ssao), base.a);
		}
	#}

	Shader fragment=
	#{
		float depth = TEXTURE(tex_scene_depth, IN_UV).r;
		if (depth == 0.0f || depth == 1.0f)
			discard;

		OUT_COLOR = final(IN_UV, depth);
	#}
}

```

</details>


### Only Base Material


This example demonstrates the same use case as [above](#abstract_base) but using Base Material only.


<details>
<summary>Base Material only (my_single_base.basemat) | Close</summary>

`my_single_base.basemat`


```glsl
BaseMaterial <preview_hidden=true var_prefix=var texture_prefix=tex>
{
	Texture2D color <source=procedural>
	Texture2D normal <source=gbuffer_normal>
	Texture2D scene_depth <source=current_depth>
	Texture2D modulation = "core/textures/common/checker_d.texture"
	Texture2D <source=ssao>

	Slider global_scale = 2

	Shader base_shader=
	#{
		#include <core/materials/shaders/render/common.h>

		STRUCT_FRAG_BEGIN
			INIT_COLOR(float4)
		STRUCT_FRAG_END

		float3 triplanar_sample(float2 uv, float depth_in)
		{
			float3 normal_ws = mul3(s_imodelview, unpackGBufferNormal(TEXTURE(tex_normal, uv).rgb));
			float3 position_ws = s_camera_position + mul3(s_imodelview, nativeDepthToPositionVS(depth_in, uv));

			float4 texcoord = position_ws.xyyz * var_global_scale;
			float3 weight = triplanarWeightFast(normal_ws, 0.5f);

			return TEXTURE_TRIPLANAR(tex_modulation, texcoord, weight).rgb;
		}

		float4 final(float2 uv, float depth_in)
		{
			float4 base = TEXTURE(tex_color, uv);
			float ssao = TEXTURE(tex_ssao, uv).r;

			float3 effect = triplanar_sample(uv, depth_in);
			return float4(lerp(effect, base.rgb, ssao), base.a);
		}

		MAIN_FRAG_BEGIN(FRAGMENT_IN)
			float depth = TEXTURE(tex_scene_depth, IN_UV).r;
			if (depth == 0.0f || depth == 1.0f)
				discard;

			OUT_COLOR = final(IN_UV, depth);
		MAIN_FRAG_END
	#}

	Pass post
	{
		Fragment=base_shader
	}

	Expression RENDER_CALLBACK_END_POST_MATERIALS=
	#{
		Texture source = engine.render.getTemporaryTexture(engine.render_state.getScreenColorTexture());

		source.copy(engine.render_state.getScreenColorTexture());
		setTexture("color", source);
		renderPassToTexture("post", engine.render_state.getScreenColorTexture());

		engine.render.releaseTemporaryTexture(source);
	#}
}

```

</details>


## Creating And Using Your Own Material


Let's create a material from scratch. For this example, we will go with a basic abstract material for post process effects.


### 1. Creating a Parent Abstract Material


Create a new text file with the `*.abstmat` extension. The file name is used as material name, let's call it `my_abstract`.


The abstract material contains all basic parameters that are inherited by all child materials, as well as basic shader code. These basic things are declared as follows:


```glsl
AbstractMaterial <preview_hidden=true var_prefix=var texture_prefix=tex>
{

	// Let's add a screen texture, we will use it later in BaseMaterial
	Texture2D color <source=procedural>

	Shader common=
	#{
	#}

	// Here comes the core of our fragment shader:
	Shader base_shader= // Declare the shader node for further use
	#{
		#include <core/materials/shaders/render/common.h> //Base UUSL include

		// We render to a single texture with 4 channels
		STRUCT_FRAG_BEGIN
			INIT_COLOR(float4)
		STRUCT_FRAG_END

		// Here we'll add code from inherited materials
		#shader common

		// Declare the main fragment function
		MAIN_FRAG_BEGIN(FRAGMENT_IN)
			// Here we'll add code from inherited materials
			#shader fragment
		MAIN_FRAG_END
	#}
}

```


Now we need to add a rendering pass because a single shader doesn't render anything by itself. As we're implementing a post-effect material, we should add the *post* pass and specify shaders to be used for it (we'll use our **base_shader** as a fragment shader).


> **Notice:** If a vertex shader is not specified, the default one from `core/materials/shaders/default/empty.vert` will be used.


```glsl
Pass post
{
	Fragment=base_shader
}

```


UNIGINE supports the [Scriptable Materials](../../../content/materials/scriptable.md) functionality enabling you to execute expressions (fragments of code) at certain stages of the [rendering sequence](../../../principles/render/sequence/index.md), and we are going to use it.


```glsl
// Let's subscribe our USC expression to render callback after all Engine's post-effects
Expression RENDER_CALLBACK_END_POST_MATERIALS=
#{
	// Make a copy of the screen texture
	Texture source = engine.render.getTemporaryTexture(engine.render_state.getScreenColorTexture());
	source.copy(engine.render_state.getScreenColorTexture());

	// Set it as the source texture for the post-effect
	setTexture("color", source);

	// Render the pass "post" directly to the screen
	renderPassToTexture("post", engine.render_state.getScreenColorTexture());

	// Since we won't use a newly requested texture, we can tell the engine that anyone else can use it.
	engine.render.releaseTemporaryTexture(source);
#}

```


Putting it all together we get the complete code of our abstract material that you can copy and paste to your text editor and save it as `my_abstract.abstmat` file to your project's `data` folder:


<details>
<summary>Complete Abstract Material Code (my_abstract_base1.basemat) | Close</summary>

`my_abstract_base1.basemat`


```glsl
AbstractMaterial <preview_hidden=true var_prefix=var texture_prefix=tex>
{

	// Let's add a screen texture, we will use it later in BaseMaterial
	Texture2D color <source=procedural>

	Shader common=
	#{
	#}

	// Here comes the core of our fragment shader:
	Shader base_shader= // Declare the shader node for further use
	#{
		#include <core/materials/shaders/render/common.h> //Base UUSL include

		// We render to a single texture with 4 channels
		STRUCT_FRAG_BEGIN
			INIT_COLOR(float4)
		STRUCT_FRAG_END

		// Here we'll add code from inherited materials
		#shader common

		// Declare the main fragment function
		MAIN_FRAG_BEGIN(FRAGMENT_IN)
			// Here we'll add code from inherited materials
			#shader fragment
		MAIN_FRAG_END
	#}

	// Adding a post pass to render our effect
	Pass post
	{
		Fragment=base_shader
	}

	// Let's subscribe our USC expression to render callback after all Engine's post-effects
	Expression RENDER_CALLBACK_END_POST_MATERIALS=
	#{
		// Make a copy of the screen texture
		Texture source = engine.render.getTemporaryTexture(engine.render_state.getScreenColorTexture());
		source.copy(engine.render_state.getScreenColorTexture());

		// Set it as the source texture for the post-effect
		setTexture("color", source);

		// Render the pass "post" directly to the screen
		renderPassToTexture("post", engine.render_state.getScreenColorTexture());

		// Since we won't use a newly requested texture, we can tell the engine that anyone else can use it.
		engine.render.releaseTemporaryTexture(source);
	#}
}

```

</details>


### 2. Inheriting a Base Material from the Abstract One


Now we are going to inherit a base material from the created abstract one ( `my_abstract.abstmat`) to extend its functionality.


To begin with, we'll implement a simple color filter post-effect.


Create a new file with the `*.basemat` extension. Again, the file name is used as the base material name.


Describe the base material specify that it has the abstract material `my_abstract` as a parent:


```glsl
BaseMaterial <parent=my_abstract>
{

	// Add the color parameter that will define the optical filter color
	Color my_color = [0.5 0.5 0.5 1]

	// All shader variables that are defined in the material should have a prefix to be referred to in shaders
	// For sliders, colors, and other basic parameters, it is defined with var_prefix currently set as 'var'
	// For textures, it is texture_prefix currently set as 'tex'
	Shader fragment=
	#{
		// Sample screen texture
		float4 sample = TEXTURE(tex_color, IN_UV);

		// Multiply the screen texture by specified color
		OUT_COLOR = sample * var_my_color;
	#}
}

```


> **Notice:** All shader variables defined in the material should have a prefix so that they can be referred to in shaders:
>
>
> - The prefix for **slider, color**, and **other basic parameters** is set using the **var_prefix** argument.
> - The prefix for **textures** is set using the **texture_prefix** argument.
>
>
> For example:
>
>
> ```glsl
> // Setting prefixes
> AbstractMaterial <preview_hidden=true var_prefix=var texture_prefix=tex>
>
> /*...*/
>
> // Adding the parameter
> Color my_color = [0.5 0.5 0.5 1]
>
> /*...*/
>
> // Refering to a variable
> OUT_COLOR = sample * var_my_color;
>
>
> ```


Save your base material as `my_abstract_base1.basemat` to your project's `data` folder.


That's it. What we have written is enough to create a simple post-processing effect.


### 3. Adding Another Derived Material


Now we are going to derive another, more complex material, from our abstract one.


This material shall use triplanar mapping to apply a specified *modulation* texture with the specified *intensity* in the occluded areas (according to SSAO map)


Let's create a new base material file and set the same abstract material ( `my_abstract.abstmat`) as its parent.


Here is the complete code of our second base material (save it as `my_abstract_base2.basemat` to your project's `data` folder):


<details>
<summary>Complete Abstract Material Code (my_abstract_base2.basemat) | Close</summary>

`my_abstract_base2.basemat`


```glsl
BaseMaterial <parent=my_abstract>
{
	// For this example more scene textures are required
	Texture2D normal <source=gbuffer_normal>
	Texture2D scene_depth <source=current_depth>
	Texture2D <source=ssao>

	// Modulation texture, UV scale, and effect intensity
	Texture2D modulation = "core/textures/common/checker_d.texture"
	Slider global_scale = 2
	Slider power = 10 <min=0 max=3>

	Shader common=
	#{
		float3 triplanar_sample(float2 uv, float depth_in)
		{
			float3 normal_ws = mul3(s_imodelview, unpackGBufferNormal(TEXTURE(tex_normal, uv).rgb));
			float3 position_ws = s_camera_position + mul3(s_imodelview, nativeDepthToPositionVS(depth_in, uv));

			float4 texcoord = position_ws.xyyz * var_global_scale;
			float3 weight = triplanarWeightFast(normal_ws, 0.5f);

			return TEXTURE_TRIPLANAR(tex_modulation, texcoord, weight).rgb;
		}

		float4 final(float2 uv, float depth_in)
		{
			float4 base = TEXTURE(tex_color, uv);
			float ssao = TEXTURE(tex_ssao, uv).r;

			float3 effect = triplanar_sample(uv, depth_in);
			return float4(lerp(base.rgb * effect * var_power, base.rgb, ssao), base.a);
		}
	#}

	Shader fragment=
	#{
		// Sample depth texture
		float depth = TEXTURE(tex_scene_depth, IN_UV).r;
		if (depth == 0.0f || depth == 1.0f)
		   discard;

		OUT_COLOR = final(IN_UV, depth);
	#}
}

```

</details>


### 4. Inheriting User Materials from Base Ones and Using Them


The values of parameters declared in base materials can be modified in real time only in inherited user materials. Therefore, you need to inherit user materials from base materials for your projects and adjust them as required (assign and change parameter values, etc.).


In order to test our first post-effect do the following:


- Find the `my_abstract_base1.basemat` in the *Materials* window, right-click it, choose **Create Child**, and rename your new material as `my_color_filter` . ![](create_child.png)
- As it is a post-effect, to apply the material globally we should open the *Settings -> Render -> Custom Post Materials*
- Click **Add New Material** and specify the `my_color_filter` material. After shis you can change the filter color. ![](assign_scriptable.png)


Here is the final image with our first post-material applied.


![](material1.gif)


Repeat the steps above for the `my_abstract_base2.basemat` base material to test the second post-effect. Here is what it may look like:


![](material2.gif)
