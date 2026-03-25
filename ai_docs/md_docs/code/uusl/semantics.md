# UUSL Semantics


Redefined UUSL semantics allows you to create unified input\output shader structures for both graphics APIs.


## Vertex Shader Semantics


Vertex shader semantics contain necessary input and output data for shader. You should initialize variables first and then use them.


| UUSL | Direct3D | Description |
|---|---|---|
| *INIT_ATTRIBUTE(TYPE,NUM,SEMANTICS)* | *TYPE attribute_ ## NUM : SEMANTICS;* | Adds a semantic to a vertex shader variable. |
| *INIT_OUT(TYPE,NUM)* | *TYPE data_ ## NUM : TEXCOORD ## NUM;* | Adds an output data semantic. |
| *INIT_POSITION* | *float4 position : SV_POSITION;* | Adds a position system-value semantic. |
| *INIT_INSTANCE* | *uint instance : SV_INSTANCEID;* | Adds a per-instance identifier system-value semantic. |
| *INIT_VERTEX_ID* | *uint vertex_id: SV_VertexID* | Adds a per-vertex identifier. |


Here is an example of vertex shader input and output structures:


```glsl
// Input vertex data
STRUCT(VERTEX_IN)
	INIT_ATTRIBUTE(float4,0,POSITION)	// Vertex position
	INIT_ATTRIBUTE(float4,1,TEXCOORD0)	// Vertex texcoord (uv)
	INIT_ATTRIBUTE(float4,2,TEXCOORD1)	// Vertex basis tangent
	INIT_ATTRIBUTE(float4,3,TEXCOORD2)	// Vertex color
END

// Our output vertex data
STRUCT(VERTEX_OUT)
	INIT_POSITION		// Out projected position
	INIT_OUT(float4,0)	// Texcoord (uv)
	INIT_OUT(float3,1)	// Vertex direction
END

```


Use the following pre-defined variables to use the input\output vertex shader semantics:


| UUSL | Direct3D | Description |
|---|---|---|
| *IN_INSTANCE* | *input.instance* | An input per-instance identifier system-value variable. |
| *IN_ATTRIBUTE(NUM)* | *input.attribute_ ## NUM* | An input shader variable. |
| *IN_VERTEX_ID* | *input.vertex_id* | An input per-vertex identifier. |
| *OUT_DATA(NUM)* | *output.data_ ## NUM* | An output texture coordinates variable. |
| *OUT_POSITION* | *output.position* | An output position system-value variable. |


## Fragment Shader Semantics


Fragment shader semantics contain necessary input and output data for shader. You should initialize variables first and then use them.


| UUSL | Direct3D | Description |
|---|---|---|
| *INIT_IN(TYPE,NUM)* | *TYPE data_ ## NUM : TEXCOORD ## NUM;* | Adds an input texture coordinates semantic. |
| *INIT_COLOR(TYPE)* | *TYPE color : SV_TARGET;* | Add an output diffuse or specular color semantic (single RT). |
| *INIT_DEPTH* | *float depth : SV_DEPTH;* | Add an output depth system-value semantic. |
| *INIT_MRT(TYPE,NUM)* | *TYPE color_ ## NUM : SV_TARGET ## NUM;* | Add an output color system-value semantic (some RTs). |
| *INIT_FRONTFACE* | *bool frontface : SV_ISFRONTFACE;* | Adds an input semantic indicates primitive face (frontface or not). |


To use the variables in the code, use the following variables:


| UUSL | Direct3D | Description |
|---|---|---|
| *IN_POSITION* | *input.position* | An input position value. |
| *IN_DATA(NUM)* | *input.data_ ## NUM* | An input texture coordinates variable. |
| *IN_FRONTFACE* | *input.frontface* | Floating-point scalar that indicates a back-facing primitive. A negative value faces backwards, while a positive value faces the camera. |
| *OUT_COLOR* | *output.color* | An output color value (single RT). |
| *OUT_DEPTH* | *output.depth* | An output depth value. |
| *OUT_MRT(NUM)* | *output.color_ ## NUM* | An output color value for MRTs. |


Here is a simple example of using the variable in the main function of the shader:


```glsl
MAIN_FRAG_BEGIN(FRAGMENT_IN)

	float4 texcoord = IN_DATA(0);

	/* ... other code ... */
MAIN_FRAG_END

```


## Geometry Shader Semantics


| UUSL | Direct3D | Description |
|---|---|---|
| *INIT_GEOM_IN(TYPE,NUM)* | *TYPE data_ ## NUM : TEXCOORD ## NUM;* | Add an input texture coordinates semantic for the geometry-shader stage. |
| *INIT_GEOM_OUT(TYPE,NUM)* | *TYPE data_ ## NUM : TEXCOORD ## NUM;* | Add an output texture coordinates semantic for the geometry-shader stage. |


| UUSL | Direct3D | Description |
|---|---|---|
| *IN_GEOM_DATA(NUM,INDEX)* | *input[INDEX].data_ ## NUM* | An input texture coordinates value. |
| *IN_GEOM_POSITION(INDEX)* | *input[INDEX].position* | An input position value. |
| *OUT_GEOM_DATA(NUM)* | *output.data_ ## NUM* | An output texture coordinates value. |
| *TRIANGLE_IN* | *triangle* | Input primitive type: triangle list or triangle strip. |
| *TRIANGLE_OUT* | *TriangleStream* | Output primitive type: a sequence of triangle primitives |
| *LINE_IN* | *line* | Input primitive type: line. |
| *LINE_OUT* | *LineStream* | Output primitive type: a sequence of line primitives |


## Unified Shader Semantics


Unified shader semantics allows you to create single structure for both vertex and fragment shaders. It facilitates the work with vertex and fragment shaders input/output structure by using single structure for both shaders: this structure will be output for vertex shader and input for fragment shader respectively.


You can write vertex and fragment shader in a single file with `.shader` extension. In this case, in the material you should specify this `.shader` file for both shader stages.


```xml
BaseMaterial <texture_prefix=tex var_prefix=var>
{
	// ...

	Pass auxiliary if [auxiliary]
	{
		Vertex = "core/materials/base/objects/mesh/shaders/auxiliary/auxiliary.shader"
		Fragment = "core/materials/base/objects/mesh/shaders/auxiliary/auxiliary.shader"
	}

	// ..
}

```


| UUSL | VERTEX | FRAGMENT | Description |
|---|---|---|---|
| *INIT_DATA(TYPE,NUM,NAME)* | *INIT_OUT(TYPE,NUM) \ #define NAME GET_DATA(NUM)* | *INIT_IN(TYPE,NUM) \  #define NAME GET_DATA(NUM)* | Data initialization. |
| *GET_DATA(V)* | *OUT_DATA(V)* | *IN_DATA(V)* | Helper for getting/setting data by using data name. |


### IF statement


There is also the *IF_DATA(NAME)* statement to execute an operation if the data is not null.


| UUSL | VERTEX | FRAGMENT | Description |
|---|---|---|---|
| *IF_DATA(NAME)* | *#ifdef NAME* | *#ifdef NAME* | Opening IF conditional statement. |
| *ENDIF* | *#endif* | *#endif* | Closing IF conditional statement. |


Here is a code snippet of shader, where the shader's IF statement is used.


```glsl
//input struct
STRUCT(FRAGMENT_IN)
/* ... */
	#ifdef ALPHA_FADE && USE_ALPHA_FADE
		INIT_DATA(float,1,DATA_ALPHA_FADE)
	#endif
/* ... */
END

//main functions
MAIN_FRAG_BEGIN(FRAGMENT_IN)
/* ... */
	IF_DATA(DATA_ALPHA_FADE)
		//code to execute if the data is not null
		alphaFadeDiscard(DATA_ALPHA_FADE,IN_POSITION.xy);
	ENDIF
/* ... */
MAIN_FRAG_END

```


## Interpolation Modifiers


| UUSL | Direct3D | Description |
|---|---|---|
| *MODIFIER_LINEAR* | *linear* | Interpolate between shader inputs; linear is the default value if no interpolation modifier is specified. |
| *MODIFIER_CENTROID* | *centroid* | Interpolate between samples that are somewhere within the covered area of the pixel (this may require extrapolating end points from a pixel center). Centroid sampling may improve antialiasing if a pixel is partially covered (even if the pixel center is not covered). The centroid modifier must be combined with either the linear or noperspective modifier. |
| *MODIFIER_NOINTERPOLATION* | *nointerpolation* | Do not interpolate. |
| *MODIFIER_NOPERSPECTIVE* | *noperspective* | Do not perform perspective-correction during interpolation. The noperspective modifier can be combined with the centroid modifier. |
| *MODIFIER_SAMPLE* | *sample* | Interpolate at sample location rather than at the pixel center. This causes the pixel shader to execute per-sample rather than per-pixel. |


### See Also


See also the [article](https://msdn.microsoft.com/en-us/library/windows/desktop/bb509668(v=vs.85).aspx) on Interpolation Modifiers.
