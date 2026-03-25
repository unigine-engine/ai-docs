# Unigine::Plugins::Weather::WeatherLayerCloud Class (CPP)

**Header:** #include <plugins/Unigine/Weather/UnigineWeather.h>

**Inherits from:** WeatherLayer


This class is used to represent a cloud layer within a [weather region](../../../../api/library/plugins/weather/class.region_cpp.md). It enables you to define the cloud type and obtain the current *[Cloud Layer](../../../../objects/objects/cloud_layer/index.md)* to manage its settings.


## WeatherLayerCloud Class

### Members

## int getCloudType () const

Returns the current type of cloud set for the layer.
### Return value

Current index of the [cloud type](../../../../ig/weather/settings.md#clouds) for the layer.
## void setNode ( const Ptr < ObjectCloudLayer >& node )

Sets a new node representing the cloud layer (*[ObjectCloudLayer](../../../../objects/objects/cloud_layer/index.md)*).
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ObjectCloudLayer](../../../../api/library/objects/class.objectcloudlayer_cpp.md)>&* **node** - The node representing the cloud layer.

## Ptr < ObjectCloudLayer > getNode () const

Returns the current node representing the cloud layer (*[ObjectCloudLayer](../../../../objects/objects/cloud_layer/index.md)*).
### Return value

Current node representing the cloud layer.
---

## void setCloudType ( int cloud_type , bool reset_cloud_to_default )

Sets a new cloud type for the layer.
### Arguments

- *int* **cloud_type** - Index of the [cloud type](../../../../ig/weather/settings.md#clouds) for the layer.
- *bool* **reset_cloud_to_default** - true to reset all cloud layer parameters to defaults, false to keep current values.
