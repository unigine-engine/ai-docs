# Unigine.LightOmni Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Light


This class is used to create [omni directional light sources](../../../objects/lights/omni/index.md). It is possible to modulate the light from omni light sources with a texture.


### See Also


- C++ sample
- UnigineScript sample


## LightOmni Class

### Members

## void setAttenuationDistance ( float distance )

Sets a new distance from the light source shape, at which the light source doesn't illuminate anything.
### Arguments

- *float* **distance** - The distance from the light source shape, at which the light source doesn't illuminate anything.

## float getAttenuationDistance () const

Returns the current distance from the light source shape, at which the light source doesn't illuminate anything.
### Return value

Current distance from the light source shape, at which the light source doesn't illuminate anything.
## vec2 getShadowDepthRange () const

Returns the current shadow depth range for the light source.
### Return value

Current shadow depth range for the light source as a two-component vector (min, max).
## void setShapeType ( int type )

Sets a new
### Arguments

- *int* **type** - The shape of the light source (one of the [LIGHT_SHAPE_*](../../../api/library/lights/class.light_usc.md#SHAPE_DEFAULT) variables).

## int getShapeType () const

Returns the current
### Return value

Current shape of the light source (one of the [LIGHT_SHAPE_*](../../../api/library/lights/class.light_usc.md#SHAPE_DEFAULT) variables).
## void setShapeHeight ( float height )

Sets a new height of the rectangular light source.
### Arguments

- *float* **height** - The height of the light source shape.

## float getShapeHeight () const

Returns the current height of the rectangular light source.
### Return value

Current height of the light source shape.
## void setShapeLength ( float length )

Sets a new length of the capsule-shaped or rectangular light source.
### Arguments

- *float* **length** - The length of the light source shape.

## float getShapeLength () const

Returns the current length of the capsule-shaped or rectangular light source.
### Return value

Current length of the light source shape.
## void setShapeRadius ( float radius )

Sets a new radius of the spherical, capsule-shaped or rectangular light source.
> **Notice:** In case of the rectangular shape, the value is the corner radius.


### Arguments

- *float* **radius** - The radius of the light source shape.

## float getShapeRadius () const

Returns the current radius of the spherical, capsule-shaped or rectangular light source.
> **Notice:** In case of the rectangular shape, the value is the corner radius.


### Return value

Current radius of the light source shape.
## vec3 getSize () const

Returns the current
### Return value

Current size of the illuminated area.
## void setTexture ( Texture texture )

Sets a new light image texture.
### Arguments

- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - The texture.

## Texture getTexture () const

Returns the current light image texture.
### Return value

Current texture.
## void setTextureFilePath ( string path )

Sets a new name (path) of the cubemap texture file used with this light source.
### Arguments

- *string* **path** - The cubemap texture file path.

## const char * getTextureFilePath () const

Returns the current name (path) of the cubemap texture file used with this light source.
### Return value

Current cubemap texture file path.
## void setShadowNearClippingDistance ( float distance )

Sets a new distance from the light source shape, within which the object doesn't cast shadow under this light source.
### Arguments

- *float* **distance** - The distance from the light source shape, within which the object doesn't cast shadow under this light source.

## float getShadowNearClippingDistance () const

Returns the current distance from the light source shape, within which the object doesn't cast shadow under this light source.
### Return value

Current distance from the light source shape, within which the object doesn't cast shadow under this light source.
## void setNearAttenuationGradientLength ( float length )

Sets a new length of the gradient area smoothering the attenuation border near the light source.
### Arguments

- *float* **length** - The length of the gradient area smoothering the attenuation border near the light source.

## float getNearAttenuationGradientLength () const

Returns the current length of the gradient area smoothering the attenuation border near the light source.
### Return value

Current length of the gradient area smoothering the attenuation border near the light source.
## void setNearAttenuationDistance ( float distance )

Sets a new distance from the light source shape within which the light intensity is equal to 0. If an object is located within this distance from the light source, it won't be illuminated.
### Arguments

- *float* **distance** - The distance from the light source shape, within which the light source doesn't illuminate anything.

## float getNearAttenuationDistance () const

Returns the current distance from the light source shape within which the light intensity is equal to 0. If an object is located within this distance from the light source, it won't be illuminated.
### Return value

Current distance from the light source shape, within which the light source doesn't illuminate anything.
---

## static LightOmni ( vec4 color , float attenuation_distance , string name = 0 )

Constructor. Creates a new omni light source with the given parameters.
### Arguments

- *vec4* **color** - Color of the new light source.
- *float* **attenuation_distance** - Attenuation distance
- *string* **name** - Name of the source.

## int setTextureImage ( Image image , int dynamic = 0 )

Sets a given Image instance as the light image texture. If you need to set a texture of all the lights in the scene, set dynamic flag to 1.
### Arguments

- *[Image](../../../api/library/common/class.image_usc.md)* **image** - New texture to set.
- *int* **dynamic** - Dynamic texture flag.

  - If set to 0, changing a texture of the light instance will also affect all the lights in the scene.
  - If set to 1, an image will be successfully set only for the current light instance.

### Return value

Returns 1 if the texture is set successfully; otherwise, 0.
## int getTextureImage ( Image image )

Reads the light image texture into an Image instance.
### Arguments

- *[Image](../../../api/library/common/class.image_usc.md)* **image** - Image, into which the texture is read.

### Return value

Returns 1 if the texture is read successfully; otherwise, 0.
## void setShadowSideEnabled ( int side , int enable )

Enables or disables shadows for the specified side of the omni light source's cube map. By default the light source casts shadows in all directions.
### Arguments

- *int* **side** - Number of the side of the omni light source for which shadows are to be enabled or disabled. One of the following values:

  - 0 - positive X
  - 1 - negative X
  - 2 - positive Y
  - 3 - negative Y
  - 4 - positive Z
  - 5 - negative Z
- *int* **enable** - 1 to enable shadows for the specified side of the omni light source, 0 - to disable.

## int isShadowSideEnabled ( int side )

Returns a value indicating if shadows are to be cast for the specified side of the omni light source. By default the light source casts shadows in all directions.
### Arguments

- *int* **side** - Number of the side of the omni light source for which shadows are to be enabled or disabled. One of the following values:

  - 0 - positive X
  - 1 - negative X
  - 2 - positive Y
  - 3 - negative Y
  - 4 - positive Z
  - 5 - negative Z

### Return value

1 if shadows are to be cast for the specified side of the omni light source; otherwise, 0.
## static int type ( )

Returns the type of the node.
### Return value

[Light](../../../api/library/lights/class.light_usc.md) type identifier.
