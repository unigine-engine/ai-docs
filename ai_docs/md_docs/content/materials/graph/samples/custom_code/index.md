# Custom Code Sample


| [**View Fullscreen**](https://matgraph.unigine.com/SampleCustomCode_2.21/fullView) |
|---|


This material graph sample demonstrates how to create and use nodes containing a custom shader code.


*Albedo* RGB value for the material of the *[Mesh Opaque PBR](../../../../../content/materials/graph/index.md#type)* type is specified directly using a **[Float](../../../../../content/materials/graph/node_library/input/float.md)** node (casting to *float3* is performed automatically).


The **[Function](../../../../../content/materials/graph/node_library/misc/function.md)** node has two *float* input ports (**A** and **B**) and two *float* output ports (return value **Out** and **C** output). They are automatically added according to the function signature:


```glsl
float function_1(in float a, in float b, out float c)
{
	c = lerp(a, b, 0.5f);
	return a+b;
}

```


**A** and **B** values for the custom function node are provided by **[Slider](../../../../../content/materials/graph/index.md#params)** parameter nodes (adjustable via the *Parameters* panel in UnigineEditor) connected to it.


The result of linear interpolation between **A** and **B** values is connected to the *Roughness* input port of the master material node, while the sum of **A** and **B** � to *Metalness*.


Finally, the data output is passed to the **[Final](../../../../../content/materials/graph/node_library/misc/final.md)** node.
