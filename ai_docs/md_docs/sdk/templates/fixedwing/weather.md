# Fixed-Wing Template - Weather Simulation


The **Weather** framework is implemented using the **[Weather Plugin](../../../ig/weather/index.md)** and provides a simplified *[Weather Configurator](#ui_configurator)* UI to control the weather conditions at runtime.


## Weather Plugin Overview


The *Weather* plugin used for implementation of this framework is a part of the *[IG Template](../../../ig/index.md)* and allows configuring visualization of weather using the following:


- `weather_config.xml` configuration file
- Weather Plugin API and components
- [IG Editor Plugin](../../../ig/ig_plugin.md)


## Weather Configurator


The template contains *Weather Configurator* that provides access to meteo settings at runtime.


The tab **Time** controls the sun position and the intensity of global light sources:


![](../modules/weather/weather_configurator_tab_1.jpg)


| Setting | Description |
|---|---|
| Time | Changes the angle of the sun. |
| Sun Intensity | Toggles the sun and controls its intensity parameter. |
| Moon Intensity | Toggles the moon and controls its intensity parameter. Visible when it's the nighttime or the sun is disabled. |
| Starfield Intensity | Toggles the stars and controls the starfield intensity parameter. Visible when it's the nighttime or the sun is disabled. |


The tab **Precipitation** controls the settings that refer to rain/snow. The tabs **Cloud** and **Cloud 1** allow controlling the settings that refer to clouds.


![](../../../ig/weather/Ig_layers.png)


![](../modules/weather/weather_configurator_tab_2.jpg)


| Setting | Description |
|---|---|
| Type | Type of precipitation to be rendered: - *Rain, Snow* - precipitation implemented using [Object Particles](../../../objects/effects/particles/index.md). May cause artifacts, when an entity is moving quickly. - *GPU Rain, GPU Snow* - experimental implementation of precipitation using the approach based on GPU particles. More suitable for quick-moving entities. |
| Elevation | Height above sea level at which the current layer starts. |
| Thickness | Height of the current layer. |
| Visibility | Visibility distance within the current layer, in meters. Can be used to simulate haze. |
| Coverage | Density of layer effects, from 0% (no effect) to 100% (covers the whole layer). |
| Lightning | Frequency of the lightning, controlled by the slider from none to frequent. |
| Wind Direction | Wind direction in the current layer, value from 0 to 360 degrees. |
| Wind Speed | Wind speed in the current layer, value from 0 to 32 m/s. |
