# Unigine.LightProj Class (CS)

**Inherits from:** Light


This class is used to create [projected light sources](../../../objects/lights/proj/index.md) that emit light from a single point and cast a cone of light. It is possible to modulate the light from these light sources with a texture.


## LightProj Class

### Properties

## Texture Texture

The light image texture.
## string TextureFilePath

The name (path) of the cubemap texture file used with this light source.
## float Penumbra

The light attenuation intensity in the penumbra cast from an object by this light source.
## float Fov

The field of view of the projected light source. Please note that a large field of view may lead to shadow distortions.
## float ShapeHeight

The height of the rectangular light source.
## float ShapeLength

The length of the capsule-shaped or rectangular light source.
## float ShapeRadius

The radius of the spherical, capsule-shaped or rectangular light source.
> **Notice:** In case of the rectangular shape, the value is the corner radius.


## Light.SHAPE ShapeType

The shape of the light source.
> **Notice:** A light source of the rectangular shape produces the light and the speck in a form of a rounded rectangle.


## float AttenuationDistance

The distance from the light source shape that defines the maximum value of the attenuation range. If an object is located farther than this from the light source, it won't be illuminated.
## 🔒︎ mat4 Projection

The projection matrix used with this light source.
## 🔒︎ vec2 ShadowDepthRange

The shadow depth range for the light source.
## bool IESRelativeToFov

The value indicating if [IES texture](../../../api/library/lights/class.light_cs.md#setShadowColorTextureMode_int_void) is scaled to fit within the light source's Field of View. Works only when light's distibution is defined by an IES profile (color texture parameter is set to IES), a lighting industry standard of describing how the light is cast based on real-world measured light fixtures.
## 🔒︎ mat4 ShadowProjection

The shadow projection matrix with the shadow coordinates correctly mapped to screen space coordinates.
## float ShadowNearClippingDistance

The distance from the light source shape, within which the object doesn't cast shadow under this light source.
## float NearAttenuationGradientLength

The length of the gradient area smoothering the attenuation border near the light source.
## float NearAttenuationDistance

The distance from the light source shape within which the light intensity is equal to 0. If an object is located within this distance from the light source, it won't be illuminated.
## bool UseEnvironmentColor

The value indicating if the light color is modulated by the environment color. When enabled, the light color is multiplied by the color of the environment behind the light source (a blurred sample of the sky cubemap taken along the light direction), imitating a sky portal: a light source placed in a window follows the sky and the surroundings it faces. Takes effect only when the sky cubemap is available.
### Members

---

## LightProj ( vec4 color , float attenuation_distance , float fov , string name = 0 )

Constructor. Creates a new projected light source with texture modulation based on given parameters.
### Arguments

- *vec4* **color** - Color of the new light source.
- *float* **attenuation_distance** - Distance from the light source shape, at which the light source doesn't illuminate anything.
- *float* **fov** - Field of view of the new light source.
- *string* **name** - Path to a texture of the new light source.

## int SetTextureImage ( Image image , bool dynamic = 0 )

Sets a given Image instance as the light image texture. If you need to set a texture of all the lights in the scene, set dynamic flag to 1.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image.
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
## static int type ( )

Returns the type of the node.
### Return value

[Light](../../../api/library/lights/class.light_cs.md) type identifier.
