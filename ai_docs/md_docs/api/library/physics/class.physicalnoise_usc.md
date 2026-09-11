# Unigine.PhysicalNoise Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Physical


The *PhysicalNoise* class is used to simulate a force field affecting physical bodies and particles based on a volumetric noise texture.  It creates an additional distribution flow specifying the force and the displacement direction for bodies and particles at each point of the force field.


> **Notice:** - The physical noise can affect only a [*cloth*](../../../principles/physics/bodies/cloth/index.md), a [*rope*](../../../api/library/physics/class.bodyrope_usc.md) or a [*rigid*](../../../principles/physics/bodies/rigid/index.md) body. Also you should remember that a rigid body requires a [shape](../../../principles/physics/shapes/index.md) to be assigned.
> - The physical noise will affect particles only if their physical mass is nonzero.


### Usage Example


In this example a physical noise node and 50 boxes, each with a body and a shape, are created. Generated boxes fall down under the set gravity and are affected by the physical noise as they get into it.


```cpp

```


### See Also


- Article on [*Physical Noise*](../../../objects/effects/physicals/physical_noise/index.md) to learn more about the parameters
- UnigineScript sample:


## PhysicalNoise Class

### Members

## void setThreshold ( vec3 threshold )

Sets a new threshold distance set for the physical noise node. the threshold determines the distance of gradual change from zero to full force value. this values are relative to the size of the physical noise box. it means that the threshold values should be less than the size of the physical noise box.
### Arguments

- *vec3* **threshold** - The threshold distance for the physical noise node

## vec3 getThreshold () const

Returns the current threshold distance set for the physical noise node. the threshold determines the distance of gradual change from zero to full force value. this values are relative to the size of the physical noise box. it means that the threshold values should be less than the size of the physical noise box.
### Return value

Current threshold distance for the physical noise node
## void setStep ( vec3 step )

Sets a new sampling step that is used for pixel sampling from the noise texture. This parameter can be used to animate a force field in run-time.
### Arguments

- *vec3* **step** - The sampling step for pixel sampling from the noise texture

## vec3 getStep () const

Returns the current sampling step that is used for pixel sampling from the noise texture. This parameter can be used to animate a force field in run-time.
### Return value

Current sampling step for pixel sampling from the noise texture
## void setSize ( vec3 size )

Sets a new size of the physical noise node.
### Arguments

- *vec3* **size** - The size of the physical noise node

## vec3 getSize () const

Returns the current size of the physical noise node.
### Return value

Current size of the physical noise node
## void setNoiseScale ( float scale )

Sets a new scale of the noise texture.
### Arguments

- *float* **scale** - The scale of the noise texture

## float getNoiseScale () const

Returns the current scale of the noise texture.
### Return value

Current scale of the noise texture
## void setOffset ( vec3 offset )

Sets a new sampling offset that is used for pixel sampling from the noise texture. This parameter can be used to animate a force field in run-time.
### Arguments

- *vec3* **offset** - The sampling offset for pixel sampling from the noise texture

## vec3 getOffset () const

Returns the current sampling offset that is used for pixel sampling from the noise texture. This parameter can be used to animate a force field in run-time.
### Return value

Current sampling offset for pixel sampling from the noise texture
## void setImageSize ( int size )

Sets a new size of the noise texture in pixels.
### Arguments

- *int* **size** - The size of the noise texture in pixels

## int getImageSize () const

Returns the current size of the noise texture in pixels.
### Return value

Current size of the noise texture in pixels
## void setFrequency ( int frequency )

Sets a new number of octaves for the perlin noise texture generation. It is not recommended to change this parameter in run-time as the noise texture will be regenerated and the performance will decrease.
### Arguments

- *int* **frequency** - The number of octaves for the noise texture generation

## int getFrequency () const

Returns the current number of octaves for the perlin noise texture generation. It is not recommended to change this parameter in run-time as the noise texture will be regenerated and the performance will decrease.
### Return value

Current number of octaves for the noise texture generation
## void setForce ( float force )

Sets a new value of the force multiplier.
### Arguments

- *float* **force** - The force multiplier

## float getForce () const

Returns the current value of the force multiplier.
### Return value

Current force multiplier
---

## static PhysicalNoise ( vec3 size )

Constructor. Creates a physical noise node of the specified size.
### Arguments

- *vec3* **size** - Physical noise box size in units.

## Image getImage ( )

Returns the noise texture image.
### Return value

Noise texture image.
## static int type ( )

Returns the type of the node.
### Return value

[PhysicalNoise](../../../api/library/nodes/class.node_usc.md#PHYSICAL_NOISE) type identifier.
