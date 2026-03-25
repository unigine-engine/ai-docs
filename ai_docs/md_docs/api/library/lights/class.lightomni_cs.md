# Unigine.LightOmni Class (CS)

**Inherits from:** Light


This class is used to create [omni directional light sources](../../../objects/lights/omni/index.md). It is possible to modulate the light from omni light sources with a texture.


### See Also


- C++ sample
- UnigineScript sample


## LightOmni Class

### Properties

## float AttenuationDistance

The distance from the light source shape, at which the light source doesn't illuminate anything.
## 🔒︎ vec2 ShadowDepthRange

The shadow depth range for the light source.
## Light.SHAPE ShapeType

The shape of the light source.
> **Notice:** A light source of the rectangular shape produces the light and the speck in a form of a rounded rectangle.


## float ShapeHeight

The height of the rectangular light source.
## float ShapeLength

The length of the capsule-shaped or rectangular light source.
## float ShapeRadius

The radius of the spherical, capsule-shaped or rectangular light source.
> **Notice:** In case of the rectangular shape, the value is the corner radius.


## 🔒︎ vec3 Size

The size of the area illuminated by the light source. depending on the [shape type](#setShapeType_int_void), the size varies:
- If the light is point-shaped, each component of the vector will be equal to the [*attenuation distance*](#setAttenuationDistance_float_void): ```cpp vec3(attenuation_distance) ```
- If the light is spherical, each component of the vector will be equal to the [*attenuation distance*](#setAttenuationDistance_float_void) *+* [*sphere radius*](#setShapeRadius_float_void): ```cpp vec3(attenuation_distance + sphere_radius) ```
- If the light is capsule-shaped, the 1st component of the vector will be equal to [*attenuation distance*](#setAttenuationDistance_float_void) *+* [*capsule length*](#setShapeLength_float_void): ```cpp vec3(attenuation_distance + capsule_length,attenuation_distance,attenuation_distance) ```
- If the light is rectangular, the 2nd component of the vector will be equal to [*attenuation distance*](#setAttenuationDistance_float_void) *+* [*rectangle height*](#setShapeHeight_float_void): ```cpp vec3(attenuation_distance,attenuation_distance + rectangle_height,attenuation_distance) ```


## Texture Texture

The light image texture.
## string TextureFilePath

The name (path) of the cubemap texture file used with this light source.
## float ShadowNearClippingDistance

The distance from the light source shape, within which the object doesn't cast shadow under this light source.
## float NearAttenuationGradientLength

The length of the gradient area smoothering the attenuation border near the light source.
## float NearAttenuationDistance

The distance from the light source shape within which the light intensity is equal to 0. If an object is located within this distance from the light source, it won't be illuminated.
### Members

---

## LightOmni ( vec4 color , float attenuation_distance , string name = 0 )

Constructor. Creates a new omni light source with the given parameters.
### Arguments

- *vec4* **color** - Color of the new light source.
- *float* **attenuation_distance** - Attenuation distance
- *string* **name** - Name of the source.

## int SetTextureImage ( Image image , bool dynamic = 0 )

Sets a given Image instance as the light image texture. If you need to set a texture of all the lights in the scene, set dynamic flag to 1.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - New texture to set.
- *bool* **dynamic** - Dynamic texture flag.

  - If set to 0, changing a texture of the light instance will also affect all the lights in the scene.
  - If set to 1, an image will be successfully set only for the current light instance.

### Return value

Returns 1 if the texture is set successfully; otherwise, 0.
## int GetTextureImage ( Image image )

Reads the light image texture into an Image instance.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image, into which the texture is read.

### Return value

Returns 1 if the texture is read successfully; otherwise, 0.
## void SetShadowSideEnabled ( int side , int enable )

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

## int IsShadowSideEnabled ( int side )

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

[Light](../../../api/library/lights/class.light_cs.md) type identifier.
