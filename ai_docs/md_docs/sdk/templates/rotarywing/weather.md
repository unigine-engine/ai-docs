# Rotary-Wing Template - Weather Simulation


![](../modules/weather/img/weather.png)


The template provides runtime control over environmental conditions, weather, and time of day through the **Weather** framework, which includes:


- **[Weather Plugin](#plugin_overview)** - the core system for environmental simulation and visualization.
- **[Weather Configurator](#ui_configurator)** - a simplified UI for adjusting weather conditions at runtime.


## Weather Plugin Overview

 The *Weather* plugin is a ready-to-use solution for simulating various environmental states. Configuring the plugin's visualization is possible using:
1. **[weather_config.xml](../../../ig/weather/config.md) configuration file**, stored in your project `/data` folder. Here you can add or modify cloud presets, set the time zone, or replace standard `.node` files for lightning, rain, snow, and water simulation.
2. **[Weather Plugin API and components](../../../api/library/plugins/weather/index.md)** providing access to advanced features (e.g., fog, haze, humidity, continuous time of day, fixed date and time, and more).
3. **[IG Editor Plugin](../../../ig/ig_plugin.md)** allowing weather and environment configuration right in the Editor.


## Weather Configurator


To control weather at runtime, the template provides the *Weather Configurator* - a simple graphical interface that gives access to the main meteo settings.


*Weather Configurator* demonstrates one possible implementation of runtime weather control built on top of the *Weather Plugin* API. It can be used as a reference for:


- Implementing a custom IOS (Instructor Operator Station);
- Building dynamic weather behavior, including custom weather scenarios and runtime weather transitions.


Weather conditions can also be controlled via supported industry-standard interfaces for distributed simulation like CIGI, DIS, or HLA. In such cases a simulation host sends network packets with environment state updates to the Image Generator.


The *Weather Configurator* is organized into the following tabs:


### Time


Controls the sun position and the intensity of global light sources.


![](../modules/weather/img/weather_configurator_tab_1.jpg)


| **Time** | Changes the angle of the sun. |
|---|---|
| **Sun Intensity** | Toggles the sun and controls its intensity parameter. |
| **Moon Intensity** | Toggles the moon and controls its intensity parameter. Visible when it's the nighttime or the sun is disabled. |
| **Starfield Intensity** | Toggles the stars and controls the starfield intensity parameter. Visible when it's the nighttime or the sun is disabled. |


### Precipitation


Controls the settings that define the behavior of the *Precipitation Layer* .


> **Notice:** ***Wind Speed*** parameter of the *Precipitation Layer* affects the flight behavior of the UAV - higher wind speeds will make the device more difficult to control.


| **Type** | Type of precipitation to be rendered: - *Rain, Snow* - precipitation implemented using *[Object Particles](../../../objects/effects/particles/index.md)*. > **Warning:** May cause artifacts, when an entity is moving quickly. - *GPU Rain, GPU Snow* - experimental implementation of precipitation using the approach based on GPU particles. > **Notice:** More suitable for quick-moving entities. |
|---|---|


Rainfall enables rendering of an *[orthographic decal](../../../objects/decals/ortho/index.md)* that **simulates puddles** on the scene surfaces. You can adjust the decal parameters in the Editor:


- Select the `puddles` node in the *World Nodes* hierarchy.
- Modify the projection box size in the *Parameters* window: *Radius (Z-axis), Width (X-axis), Height (Y-axis)*, and *Near Clipping*.


### Clouds


**Cloud** and **Cloud 1** tabs control cloud-related settings.


![](../../../ig/weather/Ig_layers.png)


| **Type** | A cloud type to be rendered. Two presets are available out-of-the-box: **altocumulus** (on the left) and **stratocumulus** (on the right): ![Altocumulus and Stratocumulus Clouds](../modules/weather/img/clouds.png) |
|---|---|


The ***Precipitation, Clouds***, and ***Clouds 1*** tabs share a common set of parameters that define each layer's behavior.


![](../modules/weather/img/weather_configurator_tab_2.jpg)


| **Elevation** | Height above sea level at which the current layer starts. |
|---|---|
| **Thickness** | Height of the current layer. |
| **Visibility** | Visibility distance within the current layer, in meters. Can be used to simulate haze. |
| **Coverage** | Density of layer effects, from 0% (no effect) to 100% (covers the whole layer). |
| **Lightning** | Frequency of the lightning, controlled by the slider from none to frequent. |
| **Wind Direction** | Wind direction in the current layer, value from 0 to 360 degrees. |
| **Wind Speed** | Wind speed in the current layer, value from 0 to 32 m/s. |


### Weather Configurator Component


You can adjust the minimum, maximum, and default values for the *Weather Configurator* in the Editor via the `WidgetWeatherConfigurator` property assigned to the `weather_configurator` node in the *World Nodes* hierarchy:

 ![](../modules/weather/img/weather_prop_wing.png)
![](../modules/weather/img/weather.gif)
