# Unigine.FieldWeather Class (CPP)

**Header:** #include <UnigineFields.h>

**Inherits from:** Field


This class is used to create and modify a [weather field](../../../objects/effects/fields/field_weather/index.md). The field is applied to [CloudLayer object](../../../api/library/objects/class.objectcloudlayer_cpp.md) and specifies a local weather area. This type of field makes it possible to create local storms or clouds having their own coverage texture as well as to control their movement.


> **Notice:** The number of weather fields on the scene is not limited as their impact on performance is not significant.


### Creating a Weather Field


> **Notice:** When creating a FieldWeather node you should specify a coverage texture for it as it doesn't have any default texture.


```cpp
// create a new instance of the FieldWeather class and set its transformation
FieldWeatherPtr weather = FieldWeather::create();
weather->setTransform(Mat4(1));
// set the size of the field
weather->setSize(vec3(4096.0f, 4096.0f, 4096.0f));
// set the coverage texture
weather->setTexturePath("unigine_project/textures/coverage.png");

```


## FieldWeather Class

### Members

## void setCloudsAnimationOffset ( const Math:: vec3 & offset )

Sets a new offset of the FieldWeather coverage texture.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **offset** - The coverage texture offset. A [vec3](../../../api/library/math/class.vec3_cpp.md) vector with components representing the offset values of the coverage texture along the **X**, **Y** and **Z** axes.

## Math:: vec3 getCloudsAnimationOffset () const

Returns the current offset of the FieldWeather coverage texture.
### Return value

Current coverage texture offset. A [vec3](../../../api/library/math/class.vec3_cpp.md) vector with components representing the offset values of the coverage texture along the **X**, **Y** and **Z** axes.
## void setWindEnabled ( int enabled )

Sets a new value indicating if local wind inside the fieldweather is enabled.
### Arguments

- *int* **enabled** - The value indicating if local wind inside the fieldweather is enabled:

  - **1** - local wind enabled
  - **0** - local wind disabled

## int getWindEnabled () const

Returns the current value indicating if local wind inside the fieldweather is enabled.
### Return value

Current
value indicating if local wind inside the fieldweather is enabled:


- **1** - local wind enabled
- **0** - local wind disabled


## void setWindAnimation ( const Math:: vec3 & animation )

Sets a new local wind speed in **X**, **Y** and **Z** directions. The wind along **X** and **Y** axes shifts local coverage texture at the specified rates in the corresponding directions. This parameter can be used to animate clouds inside the weather field. The texture shifting is looped inside the field, as the wind affects only its offset.
> **Notice:** Setting wind speed values to 0 does not return the texture to its initial state. In order to return the initial state disable local wind by using the [setWindEnabled()](#setWindEnabled_int_void) method.


### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **animation** - The local wind speed [vec3](../../../api/library/math/class.vec3_cpp.md) vector with components representing the wind speed values in the **X**, **Y** and **Z** directions.

## Math:: vec3 getWindAnimation () const

Returns the current local wind speed in **X**, **Y** and **Z** directions. The wind along **X** and **Y** axes shifts local coverage texture at the specified rates in the corresponding directions. This parameter can be used to animate clouds inside the weather field. The texture shifting is looped inside the field, as the wind affects only its offset.
> **Notice:** Setting wind speed values to 0 does not return the texture to its initial state. In order to return the initial state disable local wind by using the [setWindEnabled()](#setWindEnabled_int_void) method.


### Return value

Current local wind speed [vec3](../../../api/library/math/class.vec3_cpp.md) vector with components representing the wind speed values in the **X**, **Y** and **Z** directions.
## void setTexture ( const Ptr < Texture >& texture )

Sets a new coverage texture of the FieldWeather. If requested, the current texture is obtained from GPU and saved into the texture instance.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)>&* **texture** - The texture instance.

## Ptr < Texture > getTexture () const

Returns the current coverage texture of the FieldWeather. If requested, the current texture is obtained from GPU and saved into the texture instance.
### Return value

Current texture instance.
## void setTexturePath ( const char * path )

Sets a new path to the FieldWeather's coverage texture.
### Arguments

- *const char ** **path** - The path to the coverage texture.

## const char * getTexturePath () const

Returns the current path to the FieldWeather's coverage texture.
### Return value

Current path to the coverage texture.
## void setIntensity ( float intensity )

Sets a new intensity of the FieldWeather. This parameter determines the degree of impact of the FieldWeather coverage texture on the clouds.
### Arguments

- *float* **intensity** - The intensity value within the **[0.0f; 1.0f]** range. The default value is 1.0f.

## float getIntensity () const

Returns the current intensity of the FieldWeather. This parameter determines the degree of impact of the FieldWeather coverage texture on the clouds.
### Return value

Current intensity value within the **[0.0f; 1.0f]** range. The default value is 1.0f.
## void setPower ( float power )

Sets a new power value for the FieldWeather coverage texture. This parameter derermines the contrast of the coverage texture and makes it possible to gradually increase cloudiness without changing the coverage texture.
> **Notice:** For this parameter to work properly, the coverage texture must not contain absolotely black pixels.


### Arguments

- *float* **power** - The power value within the **[0.0f; 1.0f]** range. The default value is 1.0f.

## float getPower () const

Returns the current power value for the FieldWeather coverage texture. This parameter derermines the contrast of the coverage texture and makes it possible to gradually increase cloudiness without changing the coverage texture.
> **Notice:** For this parameter to work properly, the coverage texture must not contain absolotely black pixels.


### Return value

Current power value within the **[0.0f; 1.0f]** range. The default value is 1.0f.
## void setAttenuation ( float attenuation )

Sets a new attenuation factor value. This parameter indicates how much the coverage texture attenuates starting from the center of the FieldWeather to its edges.
### Arguments

- *float* **attenuation** - The attenuation factor value within the **[0.0f; 1.0f]** range. The default value is 1.0f.

## float getAttenuation () const

Returns the current attenuation factor value. This parameter indicates how much the coverage texture attenuates starting from the center of the FieldWeather to its edges.
### Return value

Current attenuation factor value within the **[0.0f; 1.0f]** range. The default value is 1.0f.
## void setAttenuationType ( int type )

Sets a new type of attenuation shape.
### Arguments

- *int* **type** - The Attenuation shape type:

  - 0 - sphere.
  - 1 - box.

## int getAttenuationType () const

Returns the current type of attenuation shape.
### Return value

Current Attenuation shape type:
- 0 - sphere.
- 1 - box.


## void setSize ( const Math:: vec3 & size )

Sets a new size of the FieldWeather.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **size** - The FieldWeather size. A [vec3](../../../api/library/math/class.vec3_cpp.md) vector with components representing the sizes along the **X**, **Y** and **Z** axes, in units.

## Math:: vec3 getSize () const

Returns the current size of the FieldWeather.
### Return value

Current FieldWeather size. A [vec3](../../../api/library/math/class.vec3_cpp.md) vector with components representing the sizes along the **X**, **Y** and **Z** axes, in units.
---

## static FieldWeatherPtr create ( )

Constructor. Creates a new empty FieldWeather instance with default properties.
## int setTextureImage ( const Ptr < Image > & image )

Sets the given image as the coverage texture of the FieldWeather.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Image instance with a coverage texture for the FieldWeather.

### Return value

**1** if the coverage texture was set successfully; otherwise, **0**.
## int getTextureImage ( const Ptr < Image > & image ) const

Grabs the coverage texture of the FieldWeather (already loaded to GPU) and saves it into the given Image instance.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Image instance into which the current coverage texture will be grabbed.

### Return value

**1** if the coverage texture was grabbed successfully; otherwise, **0**.
## static int type ( )

Returns the type of the object.
### Return value

[FieldWeather](../../../api/library/nodes/class.node_cpp.md#FIELD_WEATHER) type identifier.
