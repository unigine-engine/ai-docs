# Field Weather


A **Field Weather** is an object that specifies location of local cloud coverage areas within [cloud layers](../../../../objects/objects/cloud_layer/index.md). The FieldWeather object allows creating local storms or clouds that have their own [coverage texture](#coverage_texture) as well as to control their movement. The number of FieldWeather objects in the scene is not limited as their impact on performance is not significant.


> **Notice:** A *Field Weather* coverage is visible only when the camera is within the [dynamic coverage area](../../../../editor2/settings/render_settings/clouds/index.md#dynamic_coverage_area), which can be set up via the *[Settings](../../../../editor2/settings/render_settings/index.md)* window.
>  A FieldWeather object will affect clouds only if the *Field* mask matches the *Field Weather* mask of the **[clouds_base](../../../../content/materials/library/clouds_base/index.md)** material.


![](intro.png)

*Local stormcloud created by using aField Weatherobject*


### See also


- The *[FieldWeather](../../../../api/library/fields/class.fieldweather_cpp.md)* class to manage FieldWeather objects via API


## Adding a Field Weather


To add a *Field Weather* object in the world via UnigineEditor, do the following:


1. On the Menu bar, choose *Create -> Sky -> Field Weather*. ![](create.png)
2. Place the *Field Weather* object in the world. It doesn't matter if it intersects a CloudLayer object or not, only X and Y coordinates are used.
3. Go to the *Node* tab of the *[Parameters](../../../../editor2/node_parameters/index.md)* window, [and set up necessary parameters](#editing).


## Setting Up Field Weather


In the *Field Weather* section (*[Parameters](../../../../editor2/node_parameters/index.md)* window -> *Node* tab), the following parameters of the *Field Weather* object can be adjusted:


![](settings.png)


### Setting Bit Masks and Size


| Field Mask | A field mask. The *Field Weather* object is applied to a cloud layer only if they have [matching masks](../../../../principles/bit_masking/index.md). |
|---|---|
| Viewport Mask | A *Viewport* mask. A bit mask for rendering the *Field Weather* object into the current viewport. For the *Field Weather* object to be rendered into the viewport, its mask should match the camera *Viewport* mask. |
| Size | Size of the *Field Weather* object along the axes in units. |


### Setting Clouds Parameters


| Attenuation Type | Type of attenuation shape. This parameters determines the way the local clouds of the *Field Weather* object are mixed with the surrounding clouds. Can be one of the following: - Sphere - Box \| ![](attenuation_sphere.png) \| ![](attenuation_box.png) \| \|---\|---\| \| *Attenuation type = Sphere* \| *Attenuation type = Box* \| | ![](attenuation_sphere.png) | ![](attenuation_box.png) | *Attenuation type = Sphere* | *Attenuation type = Box* |
|---|---|---|---|---|---|
| ![](attenuation_sphere.png) | ![](attenuation_box.png) |  |  |  |  |
| *Attenuation type = Sphere* | *Attenuation type = Box* |  |  |  |  |
| Attenuation | Attenuation factor indicating how much the [coverage texture](#coverage_texture) attenuates starting from the center of the *Field Weather* object to its edges. - By the minimum value of 0, only local coverage texture of the *Field Weather* object is visible (the coverage texture of the CloudLayer is totally cut out from the *Field Weather* area). - The higher the value, the less surrounding clouds (CloudLayer coverage) are cut out from the *Field Weather* area. \| ![](attenuation_05.png) \| ![](attenuation_15.png) \| \|---\|---\| \| *Attenuation = 0.5* \| *Attenuation = 1.5* \| | ![](attenuation_05.png) | ![](attenuation_15.png) | *Attenuation = 0.5* | *Attenuation = 1.5* |
| ![](attenuation_05.png) | ![](attenuation_15.png) |  |  |  |  |
| *Attenuation = 0.5* | *Attenuation = 1.5* |  |  |  |  |
| Power | Determines the contrast of the coverage texture. Makes it possible to gradually increase cloudiness without changing the coverage texture. This parameter is analogous to *[Coverage Contrast](../../../../content/materials/library/clouds_base/index.md#coverage_contrast)* parameter of the **[clouds_base](../../../../content/materials/library/clouds_base/index.md)** material. > **Notice:** For this parameter to work properly, the coverage texture must not contain absolutely black pixels. |  |  |  |  |
| Intensity | Determines the degree of impact of the coverage texture of the *Field Weather* object on the clouds. |  |  |  |  |
| Coverage texture | An **RGB8** coverage texture for the *Field Weather* object. This texture is similar to the [coverage texture](../../../../content/materials/library/clouds_base/index.md#texture_coverage) of the **[clouds_base](../../../../content/materials/library/clouds_base/index.md)** material. |  |  |  |  |
| Wind Enabled | Indicates whether the local wind inside the *Field Weather* object is enabled. |  |  |  |  |
| Wind | Wind speed in each direction inside the *Field Weather* object. The wind along **X** and **Y** axes shifts local coverage texture at the specified rates in the corresponding directions. This parameter can be used to animate clouds inside the *Field Weather* object. The texture shifting is looped inside the object, as the wind affects only its offset. \| ![](wind_0.png) \| ![](wind_100.gif) \| \|---\|---\| \| *No wind* \| *Wind X = 100* \| > **Notice:** Setting wind speed values to zero does not return the texture to its initial state. In order to return the initial state disable local wind by unchecking the *Wind enabled* option. | ![](wind_0.png) | ![](wind_100.gif) | *No wind* | *Wind X = 100* |
| ![](wind_0.png) | ![](wind_100.gif) |  |  |  |  |
| *No wind* | *Wind X = 100* |  |  |  |  |
