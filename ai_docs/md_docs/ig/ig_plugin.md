# IG Editor Plugin

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


> **Warning:** These tools are experimental, some settings and parameters are still under development.


The **IG Editor Plugin** allows you to adjust the [weather](../ig/weather/index.md) properties for [IG](../ig/index.md) right in the Editor.


To make the plugin available in the Editor:


1. Create a new project with an *IG template* via SDK Browser. ![](ig_template.png)
2. Open the plugin windows via *Tools->Image Generator Plugin*. ![](menu.png)


The **IG Editor Plugin** provides the following features.


## DateTime


Allows to set up the date and time parameters which affect the sky and world illumination due to stars, Sun, and Moon position change.


![](datetime.png)


- **DateTime** � sets the current date and time
- **Timezone** � sets the current UTC time zone for the date and time (e.g., for the *UTC-3:30* timezone the value will be equal to -3.5)
- **Continuous Time** � enables or disables the passage of time
- **Sun** � enables the sun and its light rendering and sets brightness intensity
- **Moon** � enables the moon and its light rendering and sets brightness intensity
- **Stars** � enables the stars rendering and sets their brightness intensity


### Buttons


- **Show Sun Node** � selects the sun node in the *World Nodes* window
- **Show Moon Node** � selects the moon node in the *World Nodes* window
- **Save** � saves the data, time, and timezone to [configuration file](../ig/config.md)


## Meteo


The *Meteo* window provides a way to create **regions** and **layers** inside them. By default there is always a *Global* region present which have an unlimited and non-removable *Global* layer.


![](meteo.png)


### Regions


A [weather region](../ig/weather/settings.md#weather_regions) provides a top-down form for the weather map. There are three types of regions supported.


![](weather/region.png)


#### Setting Up Region


To set up a custom weather region, do the following:


1. Go to *Tools->Image Generator Plugin->Meteo*.
2. Click *Add Region* and then press the *Edit Region* button to start editing the newly created region in the world. ![](add_region.png)
3. Select and use *handle* nodes in the world to specify the region shape (you can add a cloud layer to see the region boundaries more clearly).

  - ![](handle_world.png) The rectangle shape type supports translation and scale of the rectangle regional area. ![](rectangle_region.png)
  - ![](handles_world.png) For the polygon shape type the handles can be moved, reordered, added, and deleted. This way you can make a region of any custom shape you require. ![](polygon_region.png)


#### Editing Regions


The following buttons are provided to setup a region:


- **Add Region** � adds a region.
- **Remove Region** � removes the selected region.
- **Edit Region** � enables edit mode for the selected region.


#### Saving the Region Configuration


You can save the region via the *Save Region Mask* button as a texture on a disk, so later it can be used as a *[Clouds Region Mask](../content/materials/library/clouds_base/index.md#clouds_region_mask)* value for a *[defined](../content/materials/library/clouds_base/index.md#layer_type)* layer type of various clouds materials.


![](clouds_regional_mask.png)


#### Saving and Loading Meteo Presets


Meteo Presets store the data about regions with layers and their parameters to a file of special format (`*.igmeteo`). The *IG:Meteo* window allows you to use presets the following ways:


- **Save** � saves the region on a disk as a meteo preset.
- **Load** � loads the meteo preset from a disk.


### Layers


Layers comprise a vertical profile of the region. Various heights can store different cloud or precipitation layers.


![](weather/Ig_layers.png)


#### Types of Layers


- **Base Layer** � base layer without any visual representation. Contains only parameters (visibility distance, temperature, humidity, etc.).
- **Cloud Layer** � layer that describes the clouds.
- **Precipitation Layer** � layer that describes the precipitation (rains or snow).


#### Setting Up Layers


To add a new layer to a region, do the following:


1. Select the region in the left *Regions* list and click the required *Add Layer* button. ![](weather/add_layer.png)
2. Increase the **Coverage** parameter to make the layer affect the weather.
3. Set the **Elevation** and **Thickness** parameters to adjust the layer's height and size (in meters). ![](layers_parameters.png) You can use the scroll manipulator to set the elevation and thickness parameters visually (changes will be reflected in the viewport). ![](scroll.png)
4. Depending on the type of the layer (base, cloud, precipitation), you must specify its properties.
5. In order to see the cloud/precipitation node in the world, click the *Show Node* button.
6. If you want to delete the added layer, select it and click the *Remove Layer* button.


#### Cloud Types


Specifies the type of cloud for the given layer. Can be one of the types specified for this project via the *[Cloud Types](#cloud_types)* window.


Upon selection of a cloud type the recommended parameters are automatically set for this type of clouds.


##### Setting Up Clouds


To start adjusting clouds in the corresponding layer, select it in the *Layers* list and specify the required *Cloud Type*.


![](adjust_clouds.png)


Use the **Coverage** parameter to make clouds appear and stand out in the sky.


#### Precipitation


Specifies the type of precipitation:


- -1: **None** � no precipitation is set for this layer
- 1: **Rain** � raindrops
- 2: **Snow** � snowflakes


##### Setting Up Precipitations


To start adjusting rain or snow precipitations in the corresponding layer, select it in the *Layers* list and specify the required *Precipitation Type*.


![](adjust_precipitation.png)


Don't forget to increase the **Coverage** parameter to make precipitation appear and stand out in the viewport.


#### Lightning


To adjust the lightning appearance for the corresponding layer, select it in the *Layers* list and specify the required frequency of lighting spawn.


![](adjusting_lightning.png)


The maximum frequency that can be set via the *IG Editor Plugin* is once per second.


#### Wind


Specifies wind properties for this layer by setting the direction and force of the wind.


- **Direction** � wind direction inside the layer
- **Wind Force** � force of the wind for the layer


![](wind.png)


## Cloud Types


![](cloud_types.png)


This window describes all types of clouds available in IG:


<details>
<summary>Default cloud types</summary>

- 1: altocumulus
- 2: altostratus
- 3: cirrocumulus
- 4: cirrostratus
- 5: cirrus
- 6: cumulonimbus_1
- 7: cumulus
- 8: nimbostratus
- 9: stratocumulus
- 10: stratus
- 12: cumulonimbus_2
- 13: cumulonimbus_3

</details>


### Adjusting Clouds


Via this window you can add your own custom types of clouds or change the default ones. The following parameters are available:


- **Cloud ID** � ID of the cloud in the list
- **Name** � cloud name
- **Material** � cloud material
- **Tracker** � cloud track used for coverage changing
- **Shadow** � power of the shadow cast by this cloud
- **Elevation** � default elevation for this type of cloud (height above sea level)
- **Thickness** � default thickness for this type of cloud
- **Padding** � lower and upper bound for this type of cloud


To understand the parameters' meaning, check the diagram below.


![](padding.png)


Clouds list and parameters are saved to the `ig_config.xml` file, so it can be restored and used in other instances of IG.


## Other Settings


![](other_settings.png)


- **Visualize Collision Segments** � toggles visualization of collision segments in the Editor.
