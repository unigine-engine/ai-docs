# Unigine::Plugins::Weather::WeatherLayerCloud Class (CS)

**Inherits from:** WeatherLayer


This class is used to represent a cloud layer within a [weather region](../../../../api/library/plugins/weather/class.region_cs.md). It enables you to define the cloud type and obtain the current *[Cloud Layer](../../../../objects/objects/cloud_layer/index.md)* to manage its settings.


## WeatherLayerCloud Class

### Properties

## 🔒︎ int CloudType

The type of cloud set for the layer.
## ObjectCloudLayer Node

The node representing the cloud layer (*[ObjectCloudLayer](../../../../objects/objects/cloud_layer/index.md)*).
### Members

---

## void SetCloudType ( int cloud_type , bool reset_cloud_to_default )

Sets a new cloud type for the layer.
### Arguments

- *int* **cloud_type** - Index of the [cloud type](../../../../ig/weather/settings.md#clouds) for the layer.
- *bool* **reset_cloud_to_default** - true to reset all cloud layer parameters to defaults, false to keep current values.
