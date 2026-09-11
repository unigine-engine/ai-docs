# FieldHeight Class (CS)

**Inherits from:** Field


This class is used to create and modify a [field height](../../../objects/effects/fields/field_height/index.md). The field is applied to [global water](../../../api/library/objects/class.objectwaterglobal_cs.md) and specifies areas where height of waves should be changed.


> **Notice:** The maximum number of the rendered FieldHeight objects per frame/bit mask is **8**.


### Creating a Height Field


> **Notice:** When creating a FieldHeight object you should specify a heightmap texture for it as this object doesn't have any default texture.


```csharp
// create a new instance of the FieldHeight class and set its transformation
FieldHeight height = new FieldHeight();
height.setTransform(Mat4(1));
// set the size of the field
height.setSize(vec3(4096.0f, 4096.0f, 512.0f));
// set the heightmap texture
height.setTexturePath("unigine_project/textures/fh_static.png");

```


### See also


- C++ sample
- UnigineScript sample


## FieldHeight Class

### Properties

## Texture Texture

The heightmap texture for the FieldHeight. If requested, the current texture is obtained from GPU and saved into the texture instance.
## string TexturePath

The path to the FieldHeight's heightmap texture.
## int BlendMode

The
field height blending mode.


> **Notice:** Attenuation parameter is interpreted depending on the selected blending mode:
>
>
> - is used as a mulpiplier for the additive mode
> - lerp(1.0f, value, attenuation) is used for the multiplicative mode


## int Order

The field height rendering order. This parameter is used to properly apply fields with mixed blend modes.
## float Power

The FieldHeight's power value. The power is a multiplier for loaded heightmap texture values.
## float Attenuation

The FieldHeight's attenuation factor value. The attenuation factor indicates the rate of FiledHeight influence attenuation from the center of the object to its edges.
## vec3 Size

The size of the FieldHeight.
### Members

---

## FieldHeight ( )

The default constructor. Creates a FieldHeight instance with the default size vec3(1.0f, 1.0f, 1.0f).
> **Notice:** By default, a heightmap texture is empty. Specify it after creating the FieldHeight by using an appropriate function.


## int SetTextureImage ( Image image )

Sets the given image as the heightmap texture of the FieldHeight.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image instance with heightmap for FieldHeight.

### Return value

**1** if the texture is set successfully; otherwise, **0**.
## int GetTextureImage ( Image image )

Grabs the texture for the FieldHeight (already loaded to GPU) and saves it into the given [Image](../../../api/library/common/class.image_cs.md) instance.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image instance into which the texture will be saved.

### Return value

**1** if the texture has been grabbed successfully; otherwise, **0**.
## static int type ( )

Returns the type of the object.
### Return value

[FieldHeight](../../../api/library/nodes/class.node_cs.md#FIELD_HEIGHT) type identifier.
