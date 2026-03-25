# Unigine::Plugins::Weather::MeteoPositionParam Structure

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


This data structure is used to store [weather layers](../../../../api/library/plugins/weather/class.weatherlayer_cpp.md) along with their corresponding [impact](../../../../api/library/plugins/weather/class.weatherlayer_cpp.md#getImpact_double_float) factors obtained for a certain point and has the following set of parameters:

| **impact** | Degree of [impact](../../../../api/library/plugins/weather/class.weatherlayer_cpp.md#getImpact_double_float) of the layer's conditions. |
|---|---|
| **layer** | [Weather layer](../../../../api/library/plugins/weather/class.weatherlayer_cpp.md). |

 The **MeteoPositionParam** structure is declared as follows:
```cpp
struct MeteoPositionParam
{
	float impact = 1.0f;
	WeatherLayer *layer = nullptr;
};

```
