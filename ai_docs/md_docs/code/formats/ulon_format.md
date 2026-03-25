# Unigine Language Object Notation (ULON)


ULON (Unigine Language Object Notation) is a universal format used in UNIGINE to describe complex structures similar to classes in Object-Oriented Programming. *[Landscape Terrain](../../objects/objects/terrain/landscape_terrain/index.md)* brushes as well as some of UNIGINE built-in materials are described using ULON.


The Engine supports loading and parsing files containing ULON-declarations, but does not support saving ULON-based structures to a file as such declarations are treated more like source code.


**ULON Description Example**


![ULON Description Example](ulon.jpg)


### See Also


- Articles on *[UlonNode](../../api/library/common/class.ulonnode_cpp.md), [UlonValue](../../api/library/common/class.ulonvalue_cpp.md), [UlonArg](../../api/library/common/class.ulonarg_cpp.md)* classes to manage ULON files via API


## Nodes


The basic element (building brick) of ULON is called a **node**. Each node has a **type**, a **name**, and a [**value**](#value).


The following construct is used to declare a node:


![ULON Node Declaration](ulon_node.png)


Both node name and type are written as strings:


- either a **quoted string** with standard escape characters,
- or a **bare word**, beginning with a lower case letter, containing only letters, digits, and underscores "_".


Here is an example:


```text
"Node Type" "node name" = node_value
NodeType node_name1 = node_value

```


Node declarations can be nested, thus forming a hierarchy. So a node can have a parent and an unlimited number children.

```text
Node parent
{
	Node child_0
	Node child_1
	{
		Node child_2
		Node child_3
	}
}

```


## Values


ULON node values can be of the following types:


- ***Boolean*** *Node my_node = true*
- ***Integer number*** *Node my_node = 1234*
- ***Floating-point number*** *Node my_node = 3.1459*
- ***String***

  - Quoted string with standard escape characters: *Node node = "word word"*
  - Bare word, beginning with a lower case letter, containing only letters, digits, and underscores "_": *Node node = word1_word2*
  - Heredoc string enclosed in **#{ ... #}**. This type can be used for code fragments (e.g., shader code embedded into material description): *Node my_node = #{C++ C# USC HLSL USSL#}*
- ***Array*** containing a finite number of *integer, float*, and *string* elements *Node my_node = [100, 0.2, str str "str str str", #{vec4 asd = vec4_zero;#}]* This array has the following **6** elements:

  - 100
  - 0.2
  - str
  - str
  - str str str
  - vec4 asd = vec4_zero;


## Arguments


ULON **argument** is a *name - value* pair (**name = value**). Arguments are additional parameters that can be associated with ULON nodes and used for various purposes (e.g. to define a tooltip or a title for a material parameter declaration). Arguments are enclosed in angle brackets *< >* and can be separated using "\t","\n","\r", as well as commas and spaces.


**Example:**


![ULON Arguments Declaration](ulon_arg.png)


## Conditions


For each node a logical condition can be specified, if the condition fails the ULON node with all its children is ignored. Thus you can dynamically build the hierarchy of ULON nodes with a great degree of flexibility. This can be useful when the contents of the node depends on certain parameters, e.g. a shader to be used is defined by the rendering pass.


> **Notice:** Conditions are not parsed and executed automatically, processing of conditions is the responsibility of the user of the ULON format (e.g. in case of materials [UnigineScript](../../code/uniginescript/index.md) and [UUSL](../../code/uusl/index.md) are used).


Conditions are specified after the node's name, starting with the **if** keyword, the condition itself is enclosed in brackets ***[ ... ]***.


Condition of the parent node is added to the condition of the child: ***(parent_conditon) && (child_conditon)***


**Example:**


```text
Node parent if[var1 == 10 || var1 == 5]
{
	Node child_0  if[var2 == 3]
	Node child_1  if[var2 == 4]
	{
		Node child_2 if[var3 != 11]
		Node child_3 if[var3 != 25]
	}
}

```


The resulting conditions for each node are as follows:


- **parent** condition: (var1 == 10 || var1 == 5)
- **child_0** condition: (var1 == 10 || var1 == 5) && (var2 == 3)
- **child_1** condition: (var1 == 10 || var1 == 5) && (var2 == 4)
- **child_2** condition: (var1 == 10 || var1 == 5) && (var2 == 4) && (var3 != 11)
- **child_3** condition: (var1 == 10 || var1 == 5) && (var2 == 4) && (var3 != 25)


## Comments


Adding comments make object declaration easier to understand, especially if the object is a complex one. The following types of comments are supported:


- **single-line** comments starting with "//": *// This is a single-line comment*
- **multi-line** comments enclosed within "/*" and "*/": */* This is* *a multi-line* *comment */*


## ULON-based Scriptable Material Example


Below you can find the example on how to use ULON file format to describe a [Scriptable Material](../../content/materials/scriptable.md) (radial blur in this case):


```glsl
BaseMaterial post_scriptable_blur_radial <preview_hidden=1 var_prefix=var texture_prefix=tex>
{
	// specify an internal texture to be used
	Texture src_color <type=procedural internal=true>

	// define the material's states and parameters available in the Editor
	Group "Blur Radial"
	{
		Int sample_count = 16 <min=1 max=32>
		Slider weight_decay = 0.95 <min=0.1 max=1.0 internal=true>
		Slider radius = 0.2 <min=0.0 max=1.0>
	}

	// define the blur render pass
	Pass render_scriptable_blur_radial
	{
		// write the fragment (pixel) shader in UUSL or HLSL
		Fragment=
		#{
			// default fragment shader include
			#include <core/materials/shaders/render/common.h>

			STRUCT_FRAG_BEGIN
				INIT_COLOR(float4)
			STRUCT_FRAG_END

			MAIN_FRAG_BEGIN(FRAGMENT_IN)

				// get the UV coordinates in [-0.5; 0.5] range
				float2 offset = IN_UV - float2(0.5f, 0.5f);

				// calculate an offset based on the sample count and the radius
				float inv_sample_count = 1.0f / toFloat(var_sample_count);
				offset *= toFloat2(inv_sample_count * var_radius);

				// get the UV coordinates of the texture
				float2 uv = float2(IN_UV.x, IN_UV.y);

				// sum up texture samples along the line
				OUT_COLOR.rgb = float3_zero;
				loop for (int i = 1; i<=var_sample_count; i++)
				{
					OUT_COLOR.rgb += TEXTURE_BIAS_ZERO(tex_src_color, uv).xyz;
					uv -= offset;
				}

				// normalize the result
				OUT_COLOR = float4(OUT_COLOR.rgb * toFloat3(inv_sample_count), 1.0f);

			MAIN_FRAG_END
		#}
	}

	// the expression in Unigine Script defines a callback
	Expression RENDER_CALLBACK_END_POST_MATERIALS =
	#{
		// declare the source texture from the screen frame
		Texture source = engine.render.getTemporaryTexture(engine.render_state.getScreenColorTexture());

		// define the source texture from the screen frame
		source.copy(engine.render_state.getScreenColorTexture());

		// set the color source texture to use it in the shader
		setTexture("src_color", source);

		// render the outline result texture to output it to the screen
		renderPassToTexture("render_scriptable_blur_radial", engine.render_state.getScreenColorTexture());

		//release the temporary texture
		engine.render.releaseTemporaryTexture(source);
	#}
}

```
