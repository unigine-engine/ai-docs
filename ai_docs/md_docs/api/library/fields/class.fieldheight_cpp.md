# FieldHeight Class (CPP)

**Header:** #include <UnigineFields.h>

**Inherits from:** Field


This class is used to create and modify a [field height](../../../objects/effects/fields/field_height/index.md). The field is applied to [global water](../../../api/library/objects/class.objectwaterglobal_cpp.md) and specifies areas where height of waves should be changed.


> **Notice:** The maximum number of the rendered FieldHeight objects per frame/bit mask is **8**.


### Creating a Height Field


> **Notice:** When creating a FieldHeight object you should specify a heightmap texture for it as this object doesn't have any default texture.


```cpp
// create a new instance of the FieldHeight class and set its transformation
FieldHeightPtr height = FieldHeight::create();
height->setTransform(Mat4(1));
// set the size of the field
height->setSize(vec3(4096.0f, 4096.0f, 512.0f));
// set the heightmap texture
height->setTexturePath("unigine_project/textures/fh_static.png");

```


### See also


- C++ sample
- UnigineScript sample


## FieldHeight Class

### Members

## void setTexture ( const Ptr < Texture >& texture )

Sets a new heightmap texture for the FieldHeight. If requested, the current texture is obtained from GPU and saved into the texture instance.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)>&* **texture** - The texture instance.

## Ptr < Texture > getTexture () const

Returns the current heightmap texture for the FieldHeight. If requested, the current texture is obtained from GPU and saved into the texture instance.
### Return value

Current texture instance.
## void setTexturePath ( const char * path )

Sets a new path to the FieldHeight's heightmap texture.
### Arguments

- *const char ** **path** - The path to the heightmap texture.

## const char * getTexturePath () const

Returns the current path to the FieldHeight's heightmap texture.
### Return value

Current path to the heightmap texture.
## void setBlendMode ( int mode )

Sets a new
field height blending mode.


> **Notice:** Attenuation parameter is interpreted depending on the selected blending mode:
>
>
> - is used as a mulpiplier for the additive mode
> - lerp(1.0f, value, attenuation) is used for the multiplicative mode


### Arguments

- *int* **mode** - The blending mode, one of the [BLEND_*](#BLEND_ADDITIVE)values.

## int getBlendMode () const

Returns the current
field height blending mode.


> **Notice:** Attenuation parameter is interpreted depending on the selected blending mode:
>
>
> - is used as a mulpiplier for the additive mode
> - lerp(1.0f, value, attenuation) is used for the multiplicative mode


### Return value

Current blending mode, one of the [BLEND_*](#BLEND_ADDITIVE)values.
## void setOrder ( int order )

Sets a new field height rendering order. This parameter is used to properly apply fields with mixed blend modes.
### Arguments

- *int* **order** - The rendering order.

## int getOrder () const

Returns the current field height rendering order. This parameter is used to properly apply fields with mixed blend modes.
### Return value

Current rendering order.
## void setPower ( float power )

Sets a new FieldHeight's power value. The power is a multiplier for loaded heightmap texture values.
### Arguments

- *float* **power** - The power value. The higher the value, the more FieldHeight's heights will affect the Global Water's object heights. The default value is 1.0f.

## float getPower () const

Returns the current FieldHeight's power value. The power is a multiplier for loaded heightmap texture values.
### Return value

Current power value. The higher the value, the more FieldHeight's heights will affect the Global Water's object heights. The default value is 1.0f.
## void setAttenuation ( float attenuation )

Sets a new FieldHeight's attenuation factor value. The attenuation factor indicates the rate of FiledHeight influence attenuation from the center of the object to its edges.
### Arguments

- *float* **attenuation** - The attenuation factor. The higher the value, the less FieldHeight's heights will affect the Global Water's object heights. The default value is 1.0f.

## float getAttenuation () const

Returns the current FieldHeight's attenuation factor value. The attenuation factor indicates the rate of FiledHeight influence attenuation from the center of the object to its edges.
### Return value

Current attenuation factor. The higher the value, the less FieldHeight's heights will affect the Global Water's object heights. The default value is 1.0f.
## void setSize ( const Math:: vec3 & size )

Sets a new size of the FieldHeight.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **size** - The FieldHeight size. A [vec3](../../../api/library/math/class.vec3_cpp.md) vector with components representing the sizes along the **X**, **Y** and **Z** axes, in units.

## Math:: vec3 getSize () const

Returns the current size of the FieldHeight.
### Return value

Current FieldHeight size. A [vec3](../../../api/library/math/class.vec3_cpp.md) vector with components representing the sizes along the **X**, **Y** and **Z** axes, in units.
---

## static FieldHeightPtr create ( )

The default constructor. Creates a FieldHeight instance with the default size vec3(1.0f, 1.0f, 1.0f).
> **Notice:** By default, a heightmap texture is empty. Specify it after creating the FieldHeight by using an appropriate function.


## int setTextureImage ( const Ptr < Image > & image )

Sets the given image as the heightmap texture of the FieldHeight.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Image instance with heightmap for FieldHeight.

### Return value

**1** if the texture is set successfully; otherwise, **0**.
## int getTextureImage ( const Ptr < Image > & image ) const

Grabs the texture for the FieldHeight (already loaded to GPU) and saves it into the given [Image](../../../api/library/common/class.image_cpp.md) instance.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Image instance into which the texture will be saved.

### Return value

**1** if the texture has been grabbed successfully; otherwise, **0**.
## static int type ( )

Returns the type of the object.
### Return value

[FieldHeight](../../../api/library/nodes/class.node_cpp.md#FIELD_HEIGHT) type identifier.
