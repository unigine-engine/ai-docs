# Cloud Layer


A **Cloud Layer** is an object representing a layer of realistic volumetric clouds with convincing dynamics.


There are ten main types of clouds in nature: Altocumulus, Altostratus, Cirrocumulus, Cirrostratus, Cirrus, Cumulonimbus, Cumulus, Nimbostratus, Stratocumulus, Stratus. All of them are implemented in UNIGINE and available out of the box as child materials of the *[clouds_base](../../../content/materials/library/clouds_base/index.md)* material (*clouds_altostratus, clouds_stratus, clouds_cumulus*, etc.).


![](stratus.jpg)


Stratus


![](stratocumulus.jpg)


Stratocumulus


![](nimbostratus.jpg)


Nimbostratus


![](cumulus.jpg)


Cumulus


![](cumulonimbus.jpg)


Cumulonimbus


![](cirrus.jpg)


Cirrus


![](cirrostratus.jpg)


Cirrostratus


![](cirrocumulus.jpg)


Cirrocumulus


![](altostratus.jpg)


Altostratus


![](altocumulus.jpg)


Altocumulus


UNIGINE clouds offer the following features:


- Local clouds coverage simulation using either the [corresponding parameter](../../../content/materials/library/clouds_base/index.md#layer_size) of the *Cloud Layer* object to limit the coverage, or the *[FieldWeather](../../../objects/effects/fields/field_weather/index.md)* object with the ability to control movement of numerous groups of clouds without performance drops
- Cloud dynamics simulation
- Cloud density simulation based on a 3D noise model
- Realistic shadows and lighting
- Large number of configurable cloud layer parameters ([height](../../../content/materials/library/clouds_base/index.md#layer_height), [density](../../../content/materials/library/clouds_base/index.md#cloud_density), [lighting](../../../content/materials/library/clouds_base/index.md#shading_group), [shadows](../../../content/materials/library/clouds_base/index.md#shadows_group), [wind](../../../content/materials/library/clouds_base/index.md#wind_group), etc.)
- Visibility distance up to 400 km
- Correct depth-sorting
- Optimized presets available for every cloud type
- Support of the Earth curvature to simulate real-world scenarios


Several cloud layers can be combined to provide realistic simulation.


![](cloud_layer.png)

*Multiple cloud layers*


### See also


- The *[clouds_base](../../../content/materials/library/clouds_base/index.md)* material to adjust clouds appearance
- [Rendering Settings](../../../editor2/settings/render_settings/clouds/index.md) for clouds to adjust common parameters for all cloud layers on the scene
- The *[Field Weather](../../../objects/effects/fields/field_weather/index.md)* object to specify areas with local weather
- The *[ObjectCloudLayer](../../../api/library/objects/class.objectcloudlayer_cpp.md)* class to edit the *Cloud Layer* via API


## Adding a Cloud Layer


To add a *Cloud Layer* to the scene via UnigineEditor:


1. On the Menu bar, click *Create -> Sky -> Cloud Layer* and select one of the available presets: ![](add_cloud_layer.png)
2. Place the cloud layer object in the scene: ![](added_cloud_layer.png)


A layer of clouds will be added to the scene and you will be able to adjust it via the *[Parameters](../../../editor2/node_parameters/index.md)* window.


## Adjusting a Cloud Layer


Cloud layers have a realistic look with the default settings, so you might not need to tweak them at all. However, if necessary, you don�t need to be a shader guru to adjust the available parameters (type, coverage, wind, etc.) to achieve the desired look of clouds in your project.


You can control your clouds via:


- the corresponding **[Rendering Settings](../../../editor2/settings/render_settings/clouds/index.md)** applied to all cloud layers in the scene
- the parameters of **[clouds_base](../../../content/materials/library/clouds_base/index.md)** material providing an opportunity to tweak each layer separately


Each *Cloud Layer* object can use its own material inherited from *[clouds_base](../../../content/materials/library/clouds_base/index.md)* to define its form and type (like *clouds_altostratus, clouds_stratus, clouds_cumulus*, etc.).
