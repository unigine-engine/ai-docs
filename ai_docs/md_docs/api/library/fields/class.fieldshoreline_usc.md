# FieldShoreline Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Field


This class is used to create and modify a [field shoreline](../../../objects/effects/fields/field_shoreline/index.md). The field is applied to [global water](../../../api/library/objects/class.objectwaterglobal_usc.md) and helps to create swashes near the shores and applies the wetness effect on objects near the shoreline.


> **Notice:** A field shoreline object will affect water only if the *FieldShoreline interaction* option is enabled on the *States* tab of the [water_global_base](../../../content/materials/library/water_global_base/index.md) material.


### Creating a Shoreline Field


> **Notice:** When creating a FieldShoreline object you should specify a shoreline texture for it as this object doesn't have any default texture.


```cpp
// create a new instance of the FieldShoreline class and set its transformation
FieldShoreline shoreline = new FieldShoreline();
shoreline.setTransform(Mat4("1 0 0 0 0 1 0 0 0 0 1 0 1878 2734 0 1"));
// set the size of the field
shoreline.setSize(vec3(4096.0f,4096.0f,512.0f));
// set the path to the shoreline texture
shoreline.setTexturePath("unigine_project/textures/shorelines/shoreline_0.texture");

```


## FieldShoreline Class

### Members

## void setTexture ( Texture texture )

Sets a new shoreline texture used by GPU for FieldShoreline.
### Arguments

- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - The shoreline texture instance.

## Texture getTexture () const

Returns the current shoreline texture used by GPU for FieldShoreline.
### Return value

Current shoreline texture instance.
## void setTexturePath ( string path )

Sets a new path to the FieldShoreline's texture.
### Arguments

- *string* **path** - The path to the FieldShoreline's texture.

## const char * getTexturePath () const

Returns the current path to the FieldShoreline's texture.
### Return value

Current path to the FieldShoreline's texture.
## void setSize ( vec3 size )

Sets a new vec3 size vector of FieldShoreline.
### Arguments

- *vec3* **size** - The vec3 size vector of FieldShoreline. The default value is (**512.0f**, **512.0f**, **512.0f**).

## vec3 getSize () const

Returns the current vec3 size vector of FieldShoreline.
### Return value

Current
vec3 size vector of FieldShoreline.


The default value is (**512.0f**, **512.0f**, **512.0f**).


## getEventProgress () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
---

## static FieldShoreline ( )

Default constructor. Creates a FieldShoreline instance with the default size vec3(**512.0f, 512.0f, 512.0f**).
> **Notice:** By default, a shoreline texture is empty. Specify it after creating the FieldShoreline by using an appropriate function.


## int bakeWaterLevel ( Image image )

Bakes shoreline for the current water level of the global water object and puts it to the specified image. This method generates a shoreline texture by finding intersections of the [Global Water](../../../objects/objects/water/water_object.md) object with terrains ([Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md) and [Terrain Global](../../../objects/objects/terrain/terrain_global/index.md))
### Arguments

- *[Image](../../../api/library/common/class.image_usc.md)* **image** - Image instance to which the shoreline for the current water level is to be baked.

### Return value

**1** if the shoreline is baked successfully; otherwise, **0**.
## int setTextureImage ( Image image )

Sets the given image as the shoreline texture of the FieldShoreline.
### Arguments

- *[Image](../../../api/library/common/class.image_usc.md)* **image** - Image instance with a shoreline texture for the FieldShoreline.

## int getTextureImage ( Image image )

Grabs the texture for the FieldShoreline (already loaded to GPU) and saves it into the given Image instance.
### Arguments

- *[Image](../../../api/library/common/class.image_usc.md)* **image** - Image instance into which the texture will be saved.

### Return value

**1** if the texture has been grabbed successfully; otherwise, **0**.
## int createShorelineDistanceField ( Texture texture , int shoreline_radius , int blur_radius , int downsample_resolution )

Creates a shoreline distance field with the specified parameters and puts it to the specified Image.
```text
float shoreline_radius = 64;
int blur_radius = 8;
int downsample_resolution = 128;
Texture distance_field = new Texture();
field.createShorelineDistanceField(distance_field,shoreline_radius,blur_radius,downsample_resolution);

```


### Arguments

- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - Texture to which the shoreline distance field will be put.
- *int* **shoreline_radius** - Radius of the shoreline.
- *int* **blur_radius** - Radius of the blurred area.
- *int* **downsample_resolution** - Shoreline resolution.

### Return value

**1** if the field was created successfully; otherwise, **0**.
## static int type ( )

Returns the type of the object.
### Return value

[FieldShoreline](../../../api/library/nodes/class.node_usc.md#FIELD_SHORELINE) type identifier.
