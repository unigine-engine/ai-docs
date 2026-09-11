# Weather Configuration (CS)


Weather configuration parameters (date, time, clouds, precipitation, lightning, etc.) are stored by default in a file named `weather_config.xml`.


> **Notice:** You can specify another configuration file to be used via the `-weather_config` startup command-line argument:
> ```bash
> -weather_config "my_config.xml"
> ```


A configuration file is an ordinary ***.xml** file with the following structure (example):


```xml
<?xml version="1.0" encoding="utf-8"?>
<weather_config version="2.20.0.0">
	<variables>
		<group name="Meteo">
			<item name="region_blur_material" type="string">modules/weather/shader/region_blur.basemat</item>
			<item name="visibility_tracker" type="string">modules/weather/tracks/visibility.track</item>
		</group>
		<group name="SkyMap">
			<item name="datetime" type="string">2023-10-26T11:00:24</item>
			<item name="timezone" type="float">0</item>
		</group>
		<group name="Water">
			<item name="node_path" type="string">editor2/resources/nodes/global_water_beauforts/beaufort_%d.node</item>
		</group>
		<group name="Planet">
			<item name="enabled" type="int">1</item>
			<item name="clouds_radius_min_m" type="float">1000000</item>
			<item name="clouds_radius_max_m" type="float">2000000</item>
			<item name="clouds_radius_low_alt_m" type="float">0</item>
			<item name="clouds_radius_high_alt_m" type="float">50000</item>
			<item name="haze_enabled" type="int">0</item>
		</group>
	</variables>
	<cloud_types>
		<cloud_type type="1" name="altocumulus" material="core/materials/base/objects/clouds/presets/clouds_altocumulus.mat" tracker_file="modules/weather/clouds/track/altocumulus_density.track" shadow_density="0.50999999" padding="0.180000007 0.310000002" elevation="6000" thickness="100"/>
		<cloud_type type="2" name="stratocumulus" material="core/materials/base/objects/clouds/presets/clouds_stratocumulus.mat" tracker_file="modules/weather/clouds/track/stratocumulus_density.track" shadow_density="0" padding="0.0599999987 0.600000024" elevation="1200" thickness="720"/>
	</cloud_types>
	<precipitation_types>
		<precipitation_type type="1" name="rain" far_node_path="" near_node_path="modules/weather/fx/rain_particles/nodes/rain_particles.node"/>
		<precipitation_type type="2" name="snow" far_node_path="" near_node_path="modules/weather/fx/snow_particles/nodes/snow_flakes.node"/>
		<precipitation_type type="3" name="gpu_rain" far_node_path="" near_node_path="modules/weather/fx/precipitation_gpu/rain_gpu.node"/>
		<precipitation_type type="4" name="gpu_snow" far_node_path="" near_node_path="modules/weather/fx/precipitation_gpu/snow_gpu.node"/>
	</precipitation_types>
	<lightning_sources>
		<lightning_source id="0" node_path="modules/weather/fx/lightning/nodes/lightning_particles.node"/>
	</lightning_sources>
</weather_config>

```


## Weather Settings


The weather settings are added to the variables group with the name **Meteo**.


```xml
<group name="Meteo">
	<item name="visibility_transition_time" type="float">3.000000</item>
	<item name="precipitations_transition_time" type="float">3.000000</item>
	<item name="cloud_transition_time" type="float">3.000000</item>
	<item name="visibility_tracker" type="string">ig/weather/tracks/visibility.track</item>
	<item name="overcast_preset_tracker" type="string">ig/weather/tracks/clouds_environment.track</item>
	<item name="clouds_density_tracker" type="string">ig/weather/tracks/clouds_density.track</item>
	<item name="lightning" type="string">ig/weather/fx/lightning/nodes/lightning_particles.node</item>
	<item name="water_beaufort_material_prefix" type="string">water_global_beaufort_%d</item>
</group>

```


The following items are available:


- **visibility_transition_time** � time, in seconds, for gradual change of visibility conditions (fog, etc.)
- **precipitations_transition_time** � time, in seconds, for gradual change of precipitation
- **cloud_transition_time** � time, in seconds, for gradual change of cloudiness
- **visibility_tracker** � path to the `.track` file containing visibility transition effect
- **overcast_preset_tracker** � path to the `.track` file containing the overcast preset
- **clouds_density_tracker** � path to the `.track` file containing gradual change of cloudiness
- **lightning** � path to the node storing lighting
- **water_beaufort_material_prefix** � name of the water material for the corresponding number according to the Beaufort scale


## Date and Time Settings


The date and time settings are added to the variables group with the name **SkyMap**.


```xml
<group name="SkyMap">
	<item name="timezone" type="int">0</item>
	<item name="datetime" type="string">2003-12-06T10:30:00</item>
</group>

```


The following items are available:


- **timezone** � UTC timezone, only an integer value is possible (if not set, UTC=0)
- **datetime** � date and time set for the specified timezone


## Round Planet Settings


The settings that only apply when the world is rendered on a round planet � as it is with the *[Cesium](../../code/plugins/cesium/index_cs.md)* plugin � are added to the variables group with the name **Planet**. On a flat map none of them has any effect.


```xml
	<group name="Planet">
		<item name="enabled" type="int">1</item>
		<item name="clouds_radius_min_m" type="float">1000000</item>
		<item name="clouds_radius_max_m" type="float">2000000</item>
		<item name="clouds_radius_low_alt_m" type="float">0</item>
		<item name="clouds_radius_high_alt_m" type="float">50000</item>
		<item name="haze_enabled" type="int">0</item>
	</group>

```


The following items are available:


- **enabled** � switch on the round-planet corrections: the altitude-driven cloud rounding, the sky offset that holds the horizon still across a [floating-origin rebase](../../code/plugins/cesium/index_cs.md#anchor), the haze veto and the cloud noise continuity fixup
- **clouds_radius_min_m** and **clouds_radius_max_m** � the bounds, in meters, of the radius the cloud layers are bent to
- **clouds_radius_low_alt_m** and **clouds_radius_high_alt_m** � the observer altitude range, in meters, over which the radius ramps from the minimum to the maximum. Below the lower altitude the minimum is in force, above the upper one the maximum is
- **haze_enabled** � draw the haze. Disabled by default on a planet


> **Notice:** The cloud radius is deliberately far smaller than the real radius of the Earth (about 6378 km), and is a rendering parameter rather than a physical one: the cloud noise is simple enough to tile visibly at true planetary scale. Ramping it with altitude keeps the curvature plausible both from the ground and from orbit.


> **Notice:** Haze is off by default because the flat-world haze is drawn as a hard band across the horizon once the horizon is curved. Enable it only if the camera stays low enough for that not to show.


The values in force at run time can be read back through the *[Weather.Manager.Planet](../../api/library/plugins/weather/class.weather_manager_cs.md#Planet)* interface: *[IsEnabled](../../api/library/plugins/weather/class.planet_cs.md#IsEnabled)*, *[IsHazeEnabled](../../api/library/plugins/weather/class.planet_cs.md#IsHazeEnabled)* and *[CloudsRadius](../../api/library/plugins/weather/class.planet_cs.md#CloudsRadius)*.


## Cloud Types


The list of available cloud types is enclosed in the <cloud_types/> tag. The cloud type can be set via [HEMU](http://cigi.sourceforge.net/product_he.php) / [IG Host](../../ig/ig_host.md), or using the *[WeatherLayerCloud::setCloudType()](../../api/library/plugins/weather/class.weatherlayercloud_cs.md#setCloudType_int_bool_void)* method.


```xml
<cloud_types>
	<cloud_type type="1" name="altocumulus" material="ig/clouds/materials/altocumulus.mat" tracker_file="ig/clouds/track/altocumulus_density.track" shadow_density="0.50999999" padding="0.38499999 0.441000015" elevation="0" thickness="500"/>
	<cloud_type type="2" name="altostratus" material="ig/clouds/materials/altostratus.mat" tracker_file="ig/clouds/track/altostratus_density.track" shadow_density="0" padding="0.187999994 0.486000001" elevation="0" thickness="500"/>
	<!-- ..... -->
	<cloud_type type="12" name="cumulonimbus_2" material="ig/clouds/materials/cumulonimbus_2.mat" tracker_file="ig/clouds/track/cumulus_density.track" shadow_density="0" padding="0.178000003 0.74000001" elevation="0" thickness="500"/>
	<cloud_type type="13" name="cumulonimbus_3" material="ig/clouds/materials/cumulonimbus_3.mat" tracker_file="ig/clouds/track/cumulus_density.track" shadow_density="0.98999995" padding="0.0979999974 0.778999984" elevation="0" thickness="500"/>
</cloud_types>

```


The following attributes are available:


- **type** � type of clouds
- **name** � name of the cloud type
- **material** � material to be used
- **shadow_density** � power of the shadow cast by this cloud within the range [0.0, 1.0]
- **padding** � lower and upper bounds for this type of cloud
- **elevation** � default elevation for this type of cloud (height above sea level), in meters
- **thickness** � default thickness for this type of cloud, in meters


## Precipitation Types


The list of available precipitation types is enclosed in the <precipitation_types/> tag.


```xml
<precipitation_types>
	<precipitation_type type="2" name="snow" far_node_path="" near_node_path="ig/weather/fx/snow_particles/nodes/snow_flakes.node"/>
	<precipitation_type type="1" name="rain" far_node_path="" near_node_path="ig/weather/fx/rain_particles/nodes/rain_particles.node"/>
</precipitation_types>

```


The following attributes are available:


- **type** � precipitation type id
- **name** � name of the precipitation type
- **far_node_path** � path to the node storing a representtation of the precipitation effect for far distances (when left empty the **near_node_path** is used)
- **near_node_path** � path to the node storing a representtation of the precipitation effect for close distances
