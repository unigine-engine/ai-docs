# Unigine.FieldWeather Class (CS)

**Inherits from:** Field


This class is used to create and modify a [weather field](../../../objects/effects/fields/field_weather/index.md). The field is applied to [CloudLayer object](../../../api/library/objects/class.objectcloudlayer_cs.md) and specifies a local weather area. This type of field makes it possible to create local storms or clouds having their own coverage texture as well as to control their movement.


> **Notice:** The number of weather fields on the scene is not limited as their impact on performance is not significant.


### Creating a Weather Field


> **Notice:** When creating a FieldWeather node you should specify a coverage texture for it as it doesn't have any default texture.


```csharp
// create a new instance of the FieldWeather class and set its transformation
FieldWeather weather = new FieldWeather();
weather.setTransform(Mat4(1));
// set the size of the field
weather.setSize(vec3(4096.0f, 4096.0f, 4096.0f));
// set the coverage texture
weather.setTexturePath("unigine_project/textures/coverage.png");

```


## FieldWeather Class

### Properties

## vec3 CloudsAnimationOffset

The offset of the FieldWeather coverage texture.
## int WindEnabled

The value indicating if local wind inside the fieldweather is enabled.
## vec3 WindAnimation

The local wind speed in **X**, **Y** and **Z** directions. The wind along **X** and **Y** axes shifts local coverage texture at the specified rates in the corresponding directions. This parameter can be used to animate clouds inside the weather field. The texture shifting is looped inside the field, as the wind affects only its offset.
> **Notice:** Setting wind speed values to 0 does not return the texture to its initial state. In order to return the initial state disable local wind by using the [setWindEnabled()](#setWindEnabled_int_void) method.


## Texture Texture

The coverage texture of the FieldWeather. If requested, the current texture is obtained from GPU and saved into the texture instance.
## string TexturePath

The path to the FieldWeather's coverage texture.
## float Intensity

The intensity of the FieldWeather. This parameter determines the degree of impact of the FieldWeather coverage texture on the clouds.
## float Power

The power value for the FieldWeather coverage texture. This parameter derermines the contrast of the coverage texture and makes it possible to gradually increase cloudiness without changing the coverage texture.
> **Notice:** For this parameter to work properly, the coverage texture must not contain absolotely black pixels.


## float Attenuation

The attenuation factor value. This parameter indicates how much the coverage texture attenuates starting from the center of the FieldWeather to its edges.
## int AttenuationType

The type of attenuation shape.
## vec3 Size

The size of the FieldWeather.
### Members

---

## FieldWeather ( )

Constructor. Creates a new empty FieldWeather instance with default properties.
## int SetTextureImage ( Image image )

Sets the given image as the coverage texture of the FieldWeather.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image instance with a coverage texture for the FieldWeather.

### Return value

**1** if the coverage texture was set successfully; otherwise, **0**.
## int GetTextureImage ( Image image )

Grabs the coverage texture of the FieldWeather (already loaded to GPU) and saves it into the given Image instance.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image instance into which the current coverage texture will be grabbed.

### Return value

**1** if the coverage texture was grabbed successfully; otherwise, **0**.
## static int type ( )

Returns the type of the object.
### Return value

[FieldWeather](../../../api/library/nodes/class.node_cs.md#FIELD_WEATHER) type identifier.
