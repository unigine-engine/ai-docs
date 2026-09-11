# Light Settings

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


Light is an integral part of every scene, and the number of light sources in the world can be close to infinite with all aircraft lights and strobes, airport and city illumination, strobes and so on.


Light sources are categorized by their application � on an aircraft or in the scene:


- Aircraft lights are controlled via the **[LightAircraft](#light_aircraft)** property and are described in `ig_config.xml` as [entity components](../ig/config.md#config_entities).
- To manage all ground-based light sources fast and easy, the *[Light Controller](#light_controller_system)* system is used. You can arrange all lights in the scene into the hierarchy using the **[LightSourceComponent](#light_source_component)** property and enable or disable certain groups of lights, surfaces, or materials according to your needs, adjust their intensity, or make them strobes. For light sources that do not require manual control and depend only on time of day, **[AutomaticTimeLightingComponent](#automatic_time_light)** is foreseen. This component manages automatic switching on/off the light depending on the position of the sun and moon.


### See Also


- The [IG plugin API](../api/library/plugins/ig/api/index.md) section for more details on managing IG via code (C++).


## LightAircraft


Setting aircraft lights requires the use of two components: **LightAircraft** and **LightAircraftController**.


**LightAircraft** is assigned to light nodes of an aircraft. The following parameters are available:


![](lightaircraft_prop.png)


- **Light Type** � type of the aircraft light.
- **Source Type** � type of the light source.

  - **Node Switch** � the node can be enabled and disabled. The min and max light intensity in this case is set for [light nodes](../objects/lights/index.md) only.
  - **Emissive Surface** � emission is enabled and disabled for the specified surface or surfaces of the node.

    - **Emission-Toggled Node** � toggling on disables the node if emission of its surface is disabled.
    - **Surfaces** � surfaces for which emission is enabled. To add a surface, type its name the same way it is written in the list of surfaces of this node.
  - **Emissive Material** � emission is enabled and disabled globally for the specified material.

    - **Materials** � materials for which emission is enabled.
- **Enabled By Default** � the state of the light source when the world is loaded.
- **Min Intensity** and **Max Intensity** � minimum and maximum intensity of the emitting light. For light nodes, the [light intensity](../objects/lights/parameters/index.md#intensity) is adjusted, for emissive surfaces � the *[Emission](../content/materials/library/mesh_base/index.md#emission_scale)* parameter.
- **Strobe** � strobe mode for the light.

  - **Strobe Program** � strobe program used by the light source. The program uses a sequence of indicated time periods in seconds to consecutively enable and disable the light source starting from the Enabled state. For example, a sequence of 0.3;0.05;0.1 means that a strobe is enabled for 0.3 seconds, then disabled for 0.05 seconds, enabled for 0.1 seconds, and then continues to be enabled for 0.3 seconds, etc.


**LightAircraftController** should be assigned to the parent node (aircraft) to make this type of lights work correctly via CIGI. Do not change any parameters in this property.


## Light Controller System


The *Light Controller* system allows implementing an arbitrary hierarchy of ground-based light sources. This is performed by setting a category in the **LightSourceComponent** component assigned to a node.


> **Notice:** The position of a node in the World hierarchy does not affect the hierarchy indicated as the light source category.


Suppose, we have the following hierarchy of scene lights:


- City

  - Airport

    - runway

      - runway_1

        - PAPI
        - touchdown
      - runway_2

        - PAPI
        - touchdown
  - Downtown

    - street_lights

      - lamppost_1
      - lamppost_2
    - buildings
  - District_2

    - street_lights

      - lamppost_1
      - lamppost_2
    - buildings


Using this hierarchy, you can manage any light or group of lights via the console. To generalize, the asterisk symbol (*) is used. Asterisk inside the path means that all categories on this level are checked; at the end of the path � all categories are selected.


```bash
lights City/Airport/runway/runway_1﻿/PAPI 1 � enables the PAPI light on runway_1.
lights City/Airport/runway/*﻿/touchdown 1 � enables touchdown lights on runway_1 and runway_2.
lights City/Downtown/* 0 � disables all lights in the downtown area.

```


To control intensity, values between 0.0 and 1.0 are used:


```bash
lights City/District_2/street_lights/lamppost_1 0.4

```


To enable the strobe mode for the light, 2 is used. For this purpose, the strobe mode should be added to the light component via UNIGINE Editor.


```bash
lights City/District_2/street_lights/lamppost_1 2

```


### LightSourceComponent


**LightSourceComponent** is the basis of the Light Controller system. This component allows setting all conditions describing the light source.


![](lightsourcecomponent.png)


The parameters are the same as in the **[LightAircraft](#light_parameters)** component with the only exception:


- Category � the full path in the [hierarchy of lights](#lights_hierarchy). The hierarchy of lights is developed by a user to consider all lights in the project and assign the corresponding category to a light. This hierarchy does not have any correlation with the *World Nodes hierarchy*.


### AutomaticTimeLightingComponent


**AutomaticTimeLightingComponent** is designed for lights that do not require manual control and need to be switched on and off depending on time of day. This component should be assigned to a node that is always enabled in the scene.


![](automatictimelighting_prop.png)

*This example component enables car daytime running lights from6:00:00to23:12:35, and all downtown lights and car headlights � from23:12:35to6:00:00*


Time of day can be defined either using the Sun position or the sunrise and sunset time � the approach is selected via the **Control Type** parameter.


- **Disabled** � automatic control of lights depending on time of day is disabled.
- **Celestial** � the Sun position is used to define time of day. The *Sun Zenith Threshold* parameter is available for fine-tuning.
- **Time** � the *Sunrise* and *Sunset Time* is set to define time of day in hours, minutes, and seconds.


Four categories of automatically controlled light sources are provided:


- **Categories Day Enabled** � categories of the [light sources hierarchy](#lights_hierarchy) that should be enabled during the day-time and disabled during the night-time.
- **Categories Night Enabled** � categories of the [light sources hierarchy](#lights_hierarchy) that should be enabled during the nignt-time and disabled during the day-time.
- **Materials Day Enabled** � materials that should be enabled during the day-time and disabled during the night-time.
- **Materials Night Enabled** � materials that should be enabled during the nignt-time and disabled during the day-time.


## Controlling Light via CIGI


To make light control available via CIGI, the corresponding components should be added to the configuration file as *Global Terrain* components.


```xml
<?xml version="1.0" encoding="utf-8"?>
    <property version="2.14.0.0" name="WaterDropAircraftController" manual="1" parent_name="node_base">
		<cigi_global_terrain_components>
		   <component_light id="0" name="city_all">CITY/*</component_light>
		   <component_light id="1" name="city_airport">CITY/AIRPORT/*</component_light>
		   <component_light id="2" name="city_streetlights">CITY/DOWNTOWN/STREET_LIGHTS/*</component_light>
		</cigi_global_terrain_components>

```


Then these components should be passed to CIGI via the *ComponentControl* packet as follows:


- Component Class: Global Terrain
- Instance ID: --- (currently not supported)
- Component ID: the corresponding *component_light id* from the configuration file.
- Component State: 1 (enabled) or 0 (disabled)
- Component Data 1: (FLOAT) from 0 to 1 for intensity
- Component Data 2: (INT32) 1 (enabled) or 0 (disabled) for strobes
