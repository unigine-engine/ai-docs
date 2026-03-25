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

---

## static PhysicalNoise ( vec3 size )

Constructor. Creates a physical noise node of the specified size.
### Arguments

- *vec3* **size** - Physical noise box size in units.

## void setForce ( float force )

Sets the value of the force multiplier.
### Arguments

- *float* **force** - Force multiplier. The higher the value is, the higher the value of the resulting force that affects an object inside the physical noise node will be.

## float getForce ( )

Returns the value of the force multiplier.
### Return value

Force multiplier. The higher the value is, the higher the value of the resulting force that affects an object inside the physical noise node will be.
## void setFrequency ( int frequency )

Sets the number of octaves for the Perlin noise texture generation.
> **Notice:** It is not recommended to change this parameter in run-time as the noise texture will be regenerated and the performance will decrease.


### Arguments

- *int* **frequency** - Number of octaves for the Perlin noise texture generation. The minimum value is **1**, the maximum value is **16**. The higher the value is, the more details the noise texture has.

## int getFrequency ( )

Returns the number of octaves for the Perlin noise texture generation.
> **Notice:** It is not recommended to change this parameter in run-time as the noise texture will be regenerated and the performance will decrease.


### Return value

Number of octaves for the Perlin noise texture generation. The minimum value is **1**, the maximum value is **16**. The higher the value is, the more details the noise texture has.
## Image getImage ( )

Returns the noise texture image.
### Return value

Noise texture image.
## void setImageSize ( int size )

Sets the size of the noise texture in pixels.
### Arguments

- *int* **size** - Size of the noise texture in pixels.

## int getImageSize ( )

Returns the size of the noise texture in pixels.
### Return value

Size of the noise texture in pixels.
## void setNoiseScale ( float scale )

Sets the scale of the noise texture.
> **Notice:** It is not recommended to change this parameter in run-time as the noise texture will be regenerated and the performance will decrease.


### Arguments

- *float* **scale** - Scale of the noise texture. The minimum value is **0**, the maximum value is **1**.

## float getNoiseScale ( )

Returns the scale of the noise texture.
### Return value

Scale of the noise texture. The minimum value is 0, the maximum value is 1.
## void setOffset ( vec3 offset )

Sets the sampling offset that will be used for pixel sampling from the noise texture.
> **Notice:** This parameter can be used to animate a force field in run-time.


### Arguments

- *vec3* **offset** - Sampling offset along the X, Y and Z axes.

## vec3 getOffset ( )

Returns the sampling offset that is used for pixel sampling from the noise texture.
> **Notice:** This parameter can be used to animate a force field in run-time.


### Return value

Sampling offset along the X, Y and Z axes.
## void setSize ( vec3 size )

Sets the size for the physical noise node.
### Arguments

- *vec3* **size** - Size of the physical noise box in units. If a negative value is provided, 0 will be used instead.

## vec3 getSize ( )

Returns the current size of the physical noise node.
### Return value

Size of the physical noise box in units.
## void setStep ( vec3 step )

Sets the sampling step that is used for pixel sampling from the noise texture.
> **Notice:** This parameter can be used to animate a force field in run-time.


### Arguments

- *vec3* **step** - Sampling step size along the X, Y and Z axes.

## vec3 getStep ( )

Returns the sampling step that is used for pixel sampling from the noise texture.
> **Notice:** This parameter can be used to animate a force field in run-time.


### Return value

Sampling step size along the X, Y and Z axes.
## void setThreshold ( vec3 threshold )

Sets a threshold distance set for the physical noise node.  The threshold determines the distance of gradual change from zero to full force value. This values are relative to the size of the physical noise box. It means that the threshold values should be less than the size of the physical noise box.
![](../../../objects/effects/physicals/threshold.png)


### Arguments

- *vec3* **threshold** - Threshold distance along the X, Y and Z axes.

## vec3 getThreshold ( )

 Returns the threshold distance set for the physical noise node. The threshold determines the distance of gradual change from zero to full force value. This values are relative to the size of the physical noise box. It means that the threshold values should be less than the size of the physical noise box.
### Return value

Threshold distance along the X, Y and Z axes.
## static int type ( )

Returns the type of the node.
### Return value

[PhysicalNoise](../../../api/library/nodes/class.node_usc.md#PHYSICAL_NOISE) type identifier.
