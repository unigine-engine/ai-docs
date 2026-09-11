# Unigine.LightProj Class (CPP)

**Header:** #include <UnigineLights.h>

**Inherits from:** Light


This class is used to create [projected light sources](../../../objects/lights/proj/index.md) that emit light from a single point and cast a cone of light. It is possible to modulate the light from these light sources with a texture.


### Example


The following code illustrates how to create a projected light source and set its parameters.


```cpp
#include <UnigineLights.h>
using namespace Unigine;

/* .. */

// creating a projected light source and setting its color to white, attenuation distance to 10 units and FOV angle to 60 degrees
LightProjPtr projector = LightProj::create(Math::vec4(1.0f, 1.0f, 0.5f, 1.0f), 10.0f, 60.0f, "");

// setting position of the light source
projector->setWorldPosition(Math::Vec3(2.5f, 2.5f, 3.0f));

// setting the name of the light source
projector->setName("projector");

// setting rotation of the light source
projector->setWorldRotation(Math::quat(-45.0f, 45.0f, 0.0f));

// setting penumbra factor
projector->setPenumbra(0.425f);

// setting a texture named "mytexture.tga" for light modulation
projector->setTextureFilePath("mytexture.tga");

// setting light intensity
projector->setIntensity(1.0f);

```


## LightProj Class

### Members

## void setTexture ( const Ptr < Texture >& texture )

Sets a new light image texture.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)>&* **texture** - The texture smart pointer.

## Ptr < Texture > getTexture () const

Returns the current light image texture.
### Return value

Current texture smart pointer.
## void setTextureFilePath ( const char * path )

Sets a new name (path) of the cubemap texture file used with this light source.
### Arguments

- *const char ** **path** - The cubemap texture file path.

## const char * getTextureFilePath () const

Returns the current name (path) of the cubemap texture file used with this light source.
### Return value

Current cubemap texture file path.
## void setPenumbra ( float penumbra )

Sets a new light attenuation intensity in the penumbra cast from an object by this light source.
### Arguments

- *float* **penumbra** - The intensity of the shadow.

## float getPenumbra () const

Returns the current light attenuation intensity in the penumbra cast from an object by this light source.
### Return value

Current intensity of the shadow.
## void setFov ( float fov )

Sets a new field of view of the projected light source. Please note that a large field of view may lead to shadow distortions.
### Arguments

- *float* **fov** - The field of view in degrees. The set value is saturated in range [1; 180].

## float getFov () const

Returns the current field of view of the projected light source. Please note that a large field of view may lead to shadow distortions.
### Return value

Current field of view in degrees. The set value is saturated in range [1; 180].
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
## void setShapeType ( Light::SHAPE type )

Sets a new shape of the light source.
> **Notice:** A light source of the rectangular shape produces the light and the speck in a form of a rounded rectangle.


### Arguments

- *[Light::SHAPE](../../../api/library/lights/class.light_cpp.md#SHAPE)* **type** - The shape of the light source (one of the [SHAPE_*](../../../api/library/lights/class.light_cpp.md#SHAPE_DEFAULT) variables).

## Light::SHAPE getShapeType () const

Returns the current shape of the light source.
> **Notice:** A light source of the rectangular shape produces the light and the speck in a form of a rounded rectangle.


### Return value

Current shape of the light source (one of the [SHAPE_*](../../../api/library/lights/class.light_cpp.md#SHAPE_DEFAULT) variables).
## void setAttenuationDistance ( float distance )

Sets a new distance from the light source shape that defines the maximum value of the attenuation range. If an object is located farther than this from the light source, it won't be illuminated.
### Arguments

- *float* **distance** - The distance from the light source shape, at which the light source doesn't illuminate anything.

## float getAttenuationDistance () const

Returns the current distance from the light source shape that defines the maximum value of the attenuation range. If an object is located farther than this from the light source, it won't be illuminated.
### Return value

Current distance from the light source shape, at which the light source doesn't illuminate anything.
## Math:: mat4 getProjection () const

Returns the current projection matrix used with this light source.
### Return value

Current projection matrix.
## Math:: vec2 getShadowDepthRange () const

Returns the current shadow depth range for the light source.
### Return value

Current shadow depth range for the light source as a two-component vector (min, max).
## void setIESRelativeToFov ( bool fov )

Sets a new value indicating if [IES texture](../../../api/library/lights/class.light_cpp.md#setShadowColorTextureMode_int_void) is scaled to fit within the light source's Field of View. Works only when light's distibution is defined by an IES profile (color texture parameter is set to IES), a lighting industry standard of describing how the light is cast based on real-world measured light fixtures.
### Arguments

- *bool* **fov** - Set **true** to enable scaling of IES texture; **false** - to disable it.

## bool isIESRelativeToFov () const

Returns the current value indicating if [IES texture](../../../api/library/lights/class.light_cpp.md#setShadowColorTextureMode_int_void) is scaled to fit within the light source's Field of View. Works only when light's distibution is defined by an IES profile (color texture parameter is set to IES), a lighting industry standard of describing how the light is cast based on real-world measured light fixtures.
### Return value

**true** if scaling of IES texture is enabled ; otherwise **false**.
## Math:: mat4 getShadowProjection () const

Returns the current shadow projection matrix with the shadow coordinates correctly mapped to screen space coordinates.
### Return value

Current shadow projection matrix.
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
## void setUseEnvironmentColor ( bool color )

Sets a new value indicating if the light color is modulated by the environment color. When enabled, the light color is multiplied by the color of the environment behind the light source (a blurred sample of the sky cubemap taken along the light direction), imitating a sky portal: a light source placed in a window follows the sky and the surroundings it faces. Takes effect only when the sky cubemap is available.
### Arguments

- *bool* **color** - Set **true** to enable taking the light color from the environment; **false** - to disable it.

## bool isUseEnvironmentColor () const

Returns the current value indicating if the light color is modulated by the environment color. When enabled, the light color is multiplied by the color of the environment behind the light source (a blurred sample of the sky cubemap taken along the light direction), imitating a sky portal: a light source placed in a window follows the sky and the surroundings it faces. Takes effect only when the sky cubemap is available.
### Return value

**true** if taking the light color from the environment is enabled ; otherwise **false**.
---

## static LightProjPtr create ( const Math:: vec4 & color , float attenuation_distance , float fov , const char * name = 0 )

Constructor. Creates a new projected light source with texture modulation based on given parameters.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color of the new light source.
- *float* **attenuation_distance** - Distance from the light source shape, at which the light source doesn't illuminate anything.
- *float* **fov** - Field of view of the new light source.
- *const char ** **name** - Path to a texture of the new light source.

## int setTextureImage ( const Ptr < Image > & image , bool dynamic = 0 )

Sets a given Image instance as the light image texture. If you need to set a texture of all the lights in the scene, set dynamic flag to 1.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Image.
- *bool* **dynamic** - Dynamic texture flag.

  - If set to 0, changing a texture of the light instance will also affect all the lights in the scene.
  - If set to 1, an image will be successfully set only for the current light instance.

### Return value

Returns 1 if the texture is set successfully; otherwise, 0.
## int getTextureImage ( const Ptr < Image > & image ) const

Reads the light image texture into an Image instance.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Image, into which the texture is read.

### Return value

Returns 1 if the texture is read successfully; otherwise, 0.
## static int type ( )

Returns the type of the node.
### Return value

[Light](../../../api/library/lights/class.light_cpp.md) type identifier.
