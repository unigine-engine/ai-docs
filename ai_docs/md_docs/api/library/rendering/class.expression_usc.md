# EngineExpression Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to implement [Scriptable Material](../../../content/materials/scriptable.md) expressions in [UnigineScript](../../../code/uniginescript/index.md). You should only use it to write materials-related logic.


### See Also


- The scriptable material *[creation workflow](../../../content/materials/scriptable.md#scriptable_base_material)* for an expression example.


## EngineExpression Class

### Members

---

## float noise ( float pos , float size , int frequency )

Returns [a noise](../../../api/library/engine/class.game_usc.md#getNoise1_float_float_int_float) value calculated using a Perlin noise function.
### Arguments

- *float* **pos** - Float position.
- *float* **size** - Size of the noise.
- *int* **frequency** - Noise frequency.

### Return value

Noise value.
## float random ( float from , float to )

Returns a pseudo-random float number.
### Arguments

- *float* **from** - The initial point of the range.
- *float* **to** - The end point of the range.

### Return value

Random float number.
## Node getNode ( )

Returns the current node.
### Return value

The current node.
## Node getParent ( )

Returns the parent node of the current node.
### Return value

The parent node of the current node, if it exists; otherwise, NULL.
## int getNumChildren ( )

Returns the number of node�s children.
### Return value

The number of children for the node, if it exists; otherwise, 0.
## Node getChild ( int num )

Returns the child node by its index.
### Arguments

- *int* **num** - Index of the child node to return.

### Return value

The child node of the current node, if it exists; otherwise, 0.
## Material getMaterial ( )

Returns the current material.
### Return value

The pointer to the current material.
## int getState ( string name )

Returns the value of the state.
### Arguments

- *string* **name** - Name of the state.

### Return value

The value of the state for the material, if it exists; otherwise, 0.
## void setState ( string name , int value )

Sets the value to the state by its name.
### Arguments

- *string* **name** - Name of the state.
- *int* **value** - Value of the state.

## Variable getParameter ( string param )

Returns the parameter of the material by its name.
### Arguments

- *string* **param** - Name of the parameter.

### Return value

The value of the parameter for the material, if it exists; otherwise, 0.
## void setParameter ( string param , Variable value )

Sets the value to the parameter by its name.
### Arguments

- *string* **param** - Name of the parameter.
- *Variable* **value** - Value to set.

## void getParameterArray ( Variable param , int value_id )

Returns a value of the array parameter (type: [*PARAMETER_ARRAY_FLOAT4*](../../../api/library/rendering/class.material_usc.md#PARAMETER_ARRAY_FLOAT4)) with the specified number and puts it to the specified buffer array.
### Arguments

- *Variable* **param** - Material parameter identifier. Can be of the following:

  - Parameter name.
  - Parameter number in the range from 0 to the [total number of parameters](../../../api/library/rendering/class.material_usc.md#getNumParameters_int).
- *int* **value_id** - ID of the buffer array to store parameter values.

## void setParameterArray ( Variable param , int value_id )

Sets a value of the array parameter (type: [*PARAMETER_ARRAY_FLOAT4*](../../../api/library/rendering/class.material_usc.md#PARAMETER_ARRAY_FLOAT4)) with the specified number using the specified array.
### Arguments

- *Variable* **param** - Material parameter identifier. Can be of the following:

  - Parameter name.
  - Parameter number in the range from 0 to the [total number of parameters](../../../api/library/rendering/class.material_usc.md#getNumParameters_int).
- *int* **value_id** - ID of the array of values to be set.

## Texture getTexture ( string name )

Returns the texture by its name.
### Arguments

- *string* **name** - Name of the texture.

## void setTexture ( string name , Texture texture )

Sets the new texture to the specified texture slot of the material.
### Arguments

- *string* **name** - Name of the texture slot.
- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - Pointer to the new texture.

## void renderPassCompute ( string pass , int w , int h )

Calls the specified compute shader dispatch.
### Arguments

- *string* **pass** - Name of the pass.
- *int* **w** - The number of thread groups dispatched in the **X** direction.
- *int* **h** - The number of thread groups dispatched in the **Y** direction.

## void renderPassCompute ( string pass , int w , int h , int d )

Calls the specified compute shader dispatch.
### Arguments

- *string* **pass** - Name of the pass.
- *int* **w** - The number of thread groups dispatched in the **X** direction.
- *int* **h** - The number of thread groups dispatched in the **Y** direction.
- *int* **d** - The number of thread groups dispatched in the **Z** direction.

## void renderPass ( string pass )

Renders the pass to the manually set render target.
### Arguments

- *string* **pass** - Name of the pass.

## void renderPassToTexture ( string pass , Texture texture )

Renders the pass to the texture (render target initialization and realease is done automatically).
### Arguments

- *string* **pass** - Name of the pass.
- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - Target texture for the pass rendering.
