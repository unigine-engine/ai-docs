# Creating Weather Effects


Creating atmospheric effects is essentially an artistic task. You can simulate different weather conditions using only the UnigineEditor functionality, unless you need some kind of interaction or complex smooth transitions. This article describes common ways to create such effects in UNIGINE.


## Cloudy Sky


Most weather effects require the overcast [sky](../../../objects/objects/sky/index.md). In some cases, changing the [sky color](../../../content/materials/library/sky_base/index.md#option_background) is enough, but you can also use various types of [clouds](../../../objects/objects/cloud_layer/index.md) available out of the box.


## Raindrops and Snowfall


**Raindrops** and **snowfall** effects are similar and usually simulated using [Particle Systems](../../../objects/effects/particles/index.md).


Check out the *particles_rain_effect* world of the **Art Samples** demo (the ***art_samples > particles > particles_rain_effect*** world) showcasing a rain effect. You can open it in UnigineEditor and see how it is made. For optimization purposes, this sample controls attachment of the particle systems to the camera via scripting to spawn raindrops only in some local area around the player.


| ![](rain.gif) | ![](snowfall.gif) |
|---|---|


## Lightning


**Lightning** can be simulated in many ways; the most common approach is an emissive *[Billboard](../../../objects/objects/billboards/index.md)* or a [mesh](../../../objects/objects/mesh/index.md) depending on the required level of quality. To emulate randomly occuring lightning strikes, you can configure a random [Period](../../../objects/effects/particles/index.md#period) for billboard-based particles and use a [Texture Atlas](../../../objects/effects/particles/index.md#texture_atlas) containing different lightning images.


A more complex solution, including shaders and programming, may be required to simulate how highly-detailed lightning affects the scene lighting.


![](lightning.gif)


## Fog


To simulate **fog**, take a look at the *[Environment Haze](../../../editor2/lighting/environment.md#haze)* settings. This feature is great for enriching the scene with mist and dense fog with support for height-dependent density.


![](haze_1.jpg)


## Storm


**Stormy sea** can be implemented using the *Global Water* [waves](../../../objects/objects/water/water_object.md#creating_waves): you can use a set of predefined Beaufort waves with a smooth transition between the sea states, or customize waves according to your needs.


![](storm.gif)


Waves can also be controlled via [code](../../../api/library/objects/class.objectwaterglobal_cpp.md). A set of the **Water Global** samples included in the SDK demonstrate how to use API to control *Global Water* and [fetch water level](../../../objects/objects/water/water_object.md#fetch_intersection) at a given point simulating a water splash at a point of contact with a boat or another object:


-
-
-
-
-
-


## Wind


**Wind** is a rather compound effect; there are no global wind settings affecting all the content in the project world. The wind effect could be broken into the following components:


1. **Vegetation animation**. There are several approaches to animate plants affected by wind requiring certain adjustments when modeling geometry. Check out these tutorials: ![](wind.gif)

  - [How To Create Vertex Color Based Animation for Vegetation](https://www.youtube.com/watch?v=BfgKnfdv94A)
  - [Vegetation Authoring Tips](../../../content/tutorials/vegetation/index.md#animation)
2. **[Physical Wind](../../../objects/effects/physicals/physical_wind/index.md)** affecting physical objects and particles with mass.
3. **Dust** and **small flying props** can also be made via [Particle Systems](../../../objects/effects/particles/index.md).
4. **Storm** at **[water](../../../objects/objects/water/water_object.md)** and movement of **[clouds](../../../objects/objects/cloud_layer/index.md)** is done in the settings of these objects and their materials.


## Complex Effects


More complex effects like water droplets and streaks on the camera lens, splashes in puddles, screen frost, and windshield wiper effect require shader coding and are provided in the [Weather Add-on](../../../sdk/addons/weather/index.md) available starting with the Engineering SDK (Windows only).


![](wipers.gif)
