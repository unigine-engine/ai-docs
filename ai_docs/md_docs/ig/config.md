# IG Configuration

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


All IG configuration parameters (**variables** such as system settings, connector parameters, **databases**, and **entity definitions**) are stored by default in a file named `ig_config.xml`.


> **Notice:** You can specify another configuration file to be used via the `-ig_config` startup command-line argument:
> ```bash
> -ig_config "my_config.xml"
> ```


A configuration file is an ordinary ***.xml** file with the following structure (example):


```xml
<?xml version="1.0" encoding="utf-8"?>
<ig_config>
	<variables>
		<!-- ==== ADAPTIVE QUALITY SYSTEM ======================= -->
		<group name="AdaptiveQualitySystem">
			<item name="mode" type="int">0</item>
			<item name="debug" type="int">0</item>
			<item name="sleep_period_after_world_load" type="float">-1.000000</item>
			<item name="cpu_budget" type="float">-1.000000</item>
			<item name="threshold" type="float">-1.000000</item>
			<item name="change_period" type="float">-1.000000</item>
		</group>
		<!-- ==== CONNECTOR PARAMETERS ======================= -->
		<group name="CIGIConnector">
			<item name="version" type="string">3.3</item>
			<item name="host">127.0.0.1</item>
			<item name="send_port">8889</item>
			<item name="recv_port">8888</item>
		</group>
		<!-- ==== CONFIGURATION FILE SETTINGS ======================= -->
		<group name="IG">
			<item name="autoload_database" type="int">-1</item>
			<item name="config_read_only" type="int">0</item>
			<item name="default_view_id" type="int">0</item>
			<item name="terrain_intersection_mask" type="int">0</item>
		</group>

	</variables>
	<!-- ==== DATABASE LIST ======================= -->
		<databases>
			<database id="1" world_name="world_1" geodetic_origin="25 25 0"/>
		</databases>
	<!-- ==== ENTITY DEFINITIONS ======================= -->
		<entity_types>
			<entity id="118" name="a321">
				<path>my_project/entities/aircrafts/A321/a321_air_France.node</path>
				<component id="0" name="light_outer">
					<property>LightAircraftController</property>
					<parameter name="state">enabled</parameter>
					<parameter name="data1">landing</parameter>
					<!-- ..... -->
					<parameter name="data6">logo</parameter>
				</component>
				<!-- ..... -->
				<articulated_part id="1" name="aileron">
					<node invert_pitch="1">aileron_left</node>
					<node>aileron_right</node>
				</articulated_part>
				<articulated_part id="2" name="rudder">
					<node invert_yaw="1">rudder</node>
				</articulated_part>
			</entity>
			<!-- ..... -->
		</entity_types>
	<!-- ==== VIEW TYPES LIST ===================================== -->
		<view_types>
			<view_type type="1" post_materials="post_sensor_heat"/>
			<view_type type="2" post_materials="post_sensor_green"/>
			<view_type type="3" post_materials="post_sensor_white"/>
			<view_type type="4" post_materials="post_sensor_red"/>
			<view_type type="5" post_materials="post_sensor_white,post_sensor_heat"/>
		</view_types>

	<!-- =========================================== -->
		<syncker_channels>
			<channel view_id="0" use_syncker_projection="1" syncker_name="left_view"/>
			<channel view_id="1" use_syncker_projection="0" syncker_name="ground_cam"/>
		</syncker_channels>
	<!-- =========================================== -->
		<cigi_global_terrain_components>
			<component_light id="0" name="tomsk_full">CITY1/*</component_light>
			<component_light id="1" name="RWY_red_only">CITY1/RWY/RED</component_light>
			<component_light id="2" name="RWY_approach">CITY1/RWY/APPROACH/*</component_light>
		</cigi_global_terrain_components>
	<!-- =========================================== -->
		<cigi_weather_layer>
			<layer id="1" name="cloud1" layer_type="1"/>
			<layer id="2" name="cloud2" layer_type="1"/>
			<layer id="3" name="cloud3" layer_type="1"/>
			<layer id="4" name="rain" layer_type="2" precipitation_type="1"/>
			<layer id="5" name="snow" layer_type="2" precipitation_type="2"/>
		</cigi_weather_layer>
	<!-- =========================================== -->
	</ig_config>


```


## Adaptive Quality System


This group contains configuration parameters of the [Adaptive Quality System](../ig/index.md#adaptive_quality_system), which adapts the image quality for the current performance by increasing/decreasing distance scale values ([render_distance_scale](../editor2/settings/render_settings/visibility_distances/index.md#distance_scale) and the [*Simplifier* distance scale](../ig/properties_setup.md#model_simplification)).


```xml
<group name="AdaptiveQualitySystem">
	<item name="mode" type="int">0</item>
	<item name="debug" type="int">0</item>
	<item name="sleep_period_after_world_load" type="float">-1.000000</item>
	<item name="cpu_budget" type="float">-1.000000</item>
	<item name="threshold" type="float">-1.000000</item>
	<item name="max_scale" type="float">1</item>
	<item name="min_scale" type="float">0.100000001</item>
	<item name="scale_step" type="float">0.0500000007</item>
	<item name="change_period" type="float">-1.000000</item>
</group>

```


The following items are available for the Adaptive Quality System:


- **mode** � one of the modes in which the Adaptive Quality System operates:

  - 0 � the system is disabled
  - 1 � the system operates in the *degrading* mode (without re-improving the quality when the conditions are back to normal)
  - 2 � the system in *normal* mode, degrading the image if the CPU budget is exceeded and restoring better quality when the conditions are back to normal.
- **debug** � 0 to disable the debug mode, 1 to enable displaying the debug info.
- **sleep_period_after_world_load** � idle time of the Adaptive Quality System, in seconds, after the world is loaded.
- **cpu_budget** � target CPU Total Time value, in milliseconds. -1 sets the default value of 10 milliseconds.
- **threshold** � a threshold value, in milliseconds. If CPU Total Time has changed less than this value, no adaptation is performed. -1 sets the default value of 3 milliseconds.
- **change_period** � update period, in seconds. This period enables you to ignore spikes, not to treat them as degrading performance. -1 sets the default value of 0.5 milliseconds.
- **min_scale** � minimum scale value defining the lower limit of the range of adjustment of the distance scale ([global rendering](../editor2/settings/render_settings/visibility_distances/index.md#distance_scale) and *[Simplifier](../ig/properties_setup.md#model_simplification)*).
- **max_scale** � maximum scale value defining the upper limit of the range of adjustment of the distance scale ([global rendering](../editor2/settings/render_settings/visibility_distances/index.md#distance_scale) and *[Simplifier](../ig/properties_setup.md#model_simplification)*).
- **scale_step** � the Adaptive Quality System shall use this step when adjusting distance scale.


## Connector Parameters


Configuration parameters for [connectors](../ig/index.md#connector) are added to the variables group with the corresponding name, e.g. **CIGIConnector** for CIGI-connector:


```xml
<group name="CIGIConnector">
	<item name="version" type="string">3.3</item>
	<item name="host">127.0.0.1</item>
	<item name="send_port">8889</item>
	<item name="recv_port">8888</item>
</group>

```


The following items are available for CIGI:


- **version** � CIGI protocol version
- **host** � CIGI Host IP-address
- **send_port** � TCP port number to be used for sending packets to the CIGI Host
- **recv_port** � TCP port number to be used for receiving packets from the CIGI Host
- **packet_size** � maximum size of the packet


The following items are available for DIS:


- **broadcast_address** � a broadcast address of the server computer that is used to broadcast messages to IG over the network
- **site** � the Site ID of this application instance
- **exercise** � the Exercise ID of the DIS
- **app** � the Application ID of this application instance


## Configuration File Settings


The following parameters are available to control automatic update of the configuration file.


```xml
<group name="IG">
	<item name="autoload_database" type="int">-1</item>
	<item name="config_read_only" type="int">0</item>
	<item name="default_view_id" type="int">0</item>
	<item name="terrain_intersection_mask" type="int">0</item>
</group>

```


- **autoload_database** � [ID of the database](#config_databases) to be loaded automatically. Set it to -1 to load nothing on start-up and wait for a host to command the load instead.
- **config_read_only** � set this parameter to 1 to avoid automatic re-writing of the configuration file with deletion of all your comments.
- **default_view_id** � [ID of the view](#config_cameras) to be used by default.
- **terrain_intersection_mask** � intersection mask specifying which surface is considered the ground surface (HAT/HOT requests, entity clamp, etc.).


> **Notice:** With **autoload_database** set to -1 the IG shows an empty scene until a host loads a database � and a host reports the RESET mode until it has one loaded, so nothing in the simulation runs either. See [Adding and Loading the World](../ig/ig_host.md#load) for how that is done from *IG Host*.


## Databases


The list of [databases](../ig/index.md#database) (worlds with terrains) is enclosed in the **<databases/>** tag. You can specify as many worlds as required.


```xml
<databases>
	<database id="1" world_name="world_1" geodetic_origin="25 25 0"/>
	<!-- ..... -->
	<database id="n" world_name="world_n" geodetic_origin="23 10 0"/>
</databases>

```


The following attributes are available:


- **id** � ID of the database (used when loading databases)
- **world_name** � name of the corresponding `*.world` file
- **geodetic_origin** � geodetic origin in ellipsoid coordinates: **latitude** (degrees), **longitude** (degrees), and **altitude** (meters).


> **Notice:** With the *[Cesium](../code/plugins/cesium/index_cpp.md)* plugin the georeference of the world is not static: the live origin is the [anchor](../code/plugins/cesium/index_cpp.md#anchor), which the plugin moves as the camera travels the globe. **geodetic_origin** is then only the value the world starts from, and reading it back as the current origin gives a wrong answer everywhere except at the start.


## Entity Definitions


An IG has a number of models, that are used to represent certain [entities](../ig/index.md#entity) in the virtual environment. Entity definition section is enclosed in the **<entity_types/>** tag. To define each entity, the **<entity/>** tag is used.


> **Notice:** `id` and `name` indicated within the **<entity/>** tag are referred to the **type** of the entity, not to its instances.


Each entity includes the following:


- `*.node` file containing the hierarchy of nodes representing the entity in the virtual world. A path to this file is specified in the **<path/>** tag.
- Set of [**components**](#config_components) (flashing lights, aircraft propellers, afterburners, landing gear, tank tracks, wheels, and like items). Definition of each component is enclosed in the **<component/>** tag. > **Notice:** Component data in packets, received by IG from [connectors](../ig/index.md#connector), is usually represented as a set of a discrete state and up to six values (*data1, data2 ... data6*). IG component definitions in this section are actually used to map parameters from connectors to corresponding [properties](../ig/properties_setup.md) (e.g. *data1* field of the *outer_light* component in the example below corresponds to *landing* light type).
- Set of [**articulated parts**](#config_articulated_parts) (ailerons, flaps, etc.). Definition of each articulated part is enclosed in the **<articulated_part/>** tag.


[![Click to enlarge](entity_config.png)](entity_config.png)


Below is an example of entity definition section:


```xml
<entity_types>
	<entity id="111" name="b52">
		<path>my_project/entities/aircrafts/B52/b52.node</path>
		<component id="0" name="light_outer">
			<property>LightAircraftController</property>
			<parameter name="state">enabled</parameter>
			<parameter name="data1">landing</parameter>
			<!-- ..... -->
			<parameter name="data6">logo</parameter>
		</component>
		<!-- ..... -->
		<articulated_part id="1" name="aileron">
			<node invert_pitch="1">aileron_left</node>
			<node>aileron_right</node>
		</articulated_part>
		<articulated_part id="2" name="rudder">
			<node invert_yaw="1">rudder</node>
		</articulated_part>
		<volume_definition id="0" name="body" shape="0">volumes</volume_definition>
		<volume_definition id="1" name="wings" shape="1">volumes</volume_definition>
		<segment_definition id="0" name="tail">segments/tail</segment_definition>
	</entity>
	<!-- ..... -->

```


### Components


Each entity may have an arbitrary number of components assigned, including [custom ones](../ig/custom_component.md). To define a component of an entity use the **<component/>** tag:


```xml
	<!-- ..... -->
		<entity id="118" name="a321">
			<path>my_project/entities/aircrafts/A321/a321_air_France.node</path>
			<!-- ..... -->
			<component id="22" name="rotorwash">
				<property>rotorwash</property>
				<parameter name="data1">wind_percent</parameter>
				<parameter name="data2">sand_percent</parameter>
			</component>
			<!-- ..... -->
		</entity>
	<!-- ..... -->

```


Components are added to entities by means of assigning corresponding [properties](../principles/properties/index.md) to nodes. By default it is assumed that all properties corresponding to components are assigned to the root node. In fact, a component's property can be assigned to any node in entity's hierarchy. For such a component you should add the **<node/>** tag to specify a path to this node (the path is specified relative to the root node):


```xml
	<!-- ..... -->
		<entity id="118" name="a321">
			<path>my_project/a321_air_France.node</path>
			<!-- ..... -->
			<component id="22" name="rotorwash">
				<property>rotorwash</property>
				<node>path_to_node</node>
				<parameter name="data1">wind_percent</parameter>
				<parameter name="data2">sand_percent</parameter>
			</component>
			<!-- ..... -->
		</entity>
	<!-- ..... -->

```


> **Notice:** You can also specify a path to a node inside a *NodeReference* as follows:
> - **<node>path_to_node_reference/^/path_inside_nodereference</node>**


**Example:**


For a hierarchy shown below, we have the **comp1** component's property assigned to the **aileron_left** node, and **comp2** component's property assigned to the **engine_1_fire** node. Definition of components will look like:


| ![](entity_hierarchy.png) | ```xml <entity id="118" name="a321"> <path>my_project/a321_air_France.node</path> <component id="1" name="comp1"> <property>comp1</property> <node>aileron_left</node> <parameter name="param1">param_1</parameter> <!-- ..... --> </component> <component id="2" name="comp2"> <property>comp1</property> <node>effects/^/engine_1_fire</node> <parameter name="param1">param_1</parameter> <!-- ..... --> </component> <!-- ..... --> </entity> ``` |
|---|---|


### Articulated Parts


Each entity may have an arbitrary number of articulated parts (e.g. flaps, slats, etc.). To define an articulated part of an entity use the <articulated_part/> tag:


```xml
<entity_types>
	<entity id="111" name="b52">
		<path>my_project/entities/aircrafts/B52/b52.node</path>
		<!-- ..... -->
		<articulated_part id="1" name="aileron">
			<node invert_pitch="1">aileron_left</node>
			<node>aileron_right</node>
		</articulated_part>
		<articulated_part id="2" name="rudder">
			<node invert_yaw="1">rudder</node>
		</articulated_part>
	</entity>
	<!-- ..... -->

```


> **Notice:** Options invert_roll, invert_pitch, and invert_yaw are used to indicate that the corresponding rotation direction (Y � roll, X � pitch, Z � yaw) of the articulated part element is inverted.


For each articulated part a corresponding node should be specified using the <node/> tag. Paths are specified relative to the root node, the same way as [for components](#component_node).


> **Notice:** You can also specify a path to a node inside a *NodeReference* as follows:
>
>
> - **<node>path_to_node_reference/^/path_inside_nodereference</node>**


### Volumes


To define an [entity volume](../ig/properties_setup.md#properties_volumes) use the <volume_definition/> tag:


```xml
	<!-- ..... -->
		<entity id="111" name="b52">
			<path>my_project/entities/aircrafts/B52/b52.node</path>
			<!-- ..... -->
			<volume_definition id="0" name="body" shape="0">path/inside/nodereference</volume_definition>
			<volume_definition id="1" name="wings" shape="1">path/inside/nodereference</volume_definition>
		</entity>
		<!-- ..... -->

```


The following attributes are available:


- **id** � the volume identifier in CIGI/IG.
- **name** � the name of the volume. You can use it for debugging or when writing your own collision handler.
- **shape** � the shape order in the [physics/shapes](../principles/physics/shapes/index.md#shape_params) tab.


Using this tag requires creating ObjectDummy and BodyDummy inside the entity NodeReference. The value indicated inside this tag is a path to the ObjectDummy inside the entity *NodeReference*.


### Segments


To define a [collision detection segment](../ig/properties_setup.md#properties_segments), use the <segment_definition/> tag:


```xml
	<!-- ..... -->
		<entity id="200" name="be-200">
			<path>ig/entities/aircrafts/be-200/be_200.node</path>
			<!-- ..... -->
			<segment_definition id="0" name="tail">segments/tail</segment_definition>
		</entity>
		<!-- ..... -->

```


The following attributes are available:


- **id** � the segment identifier in CIGI/IG.
- **name** � the name of the segment. You can use it for debugging or when writing your own collision handler.
- **path** � path to the node with the *CollisionSegmentDef* component assigned. The path is relative to the entity root node.


Using this tag requires the following to be done in UnigineEditor:


1. Create a NodeDummy inside the entity NodeReference and assign the *CollisionSegmentDef* component to it.
2. Create two more dummy nodes that will mark the beginning and the end of the segment and add these nodes as *Start Point* and *End Point* of the *CollisionSegmentDef* component.


[![](collision_segment_def.png)](collision_segment_def.png)


The segment is visualized in the Editor when selecting any of the relevant Node Dummies. To enable or disable the segment visualization in the Editor, toggle the [*Visualize Collision Segments* checkbox](../ig/ig_plugin.md#other_settings).


## Cameras


Cameras in IG are synchronized in a special way. A **View** is an IG wrapper for the *Camera*, so **you can manage a camera via the View only**. IG has the following methods to set the desired view for a Slave:


- *void setCurrentView(int view_id);*
- *void setSlaveView(int slave_index, int view_id);*


The list of available views is enclosed in the **<syncker_channels/>** tag. Here you can set the desired view for each Slave and specify if it is affected by the Syncker�s projections:


```xml
<syncker_channels>
	<channel view_id="0" use_syncker_projection="1" syncker_name="center_view"/>
	<channel view_id="1" use_syncker_projection="1" syncker_name="left_view"/>
	<channel view_id="2" use_syncker_projection="0" syncker_name="ground_cam"/>
</syncker_channels>

```


The following attributes are available:


- **view_id** � ID of the view to be used
- **use_syncker_projection** � flag indicating if the view is affected by the [Syncker�s projections](../code/plugins/syncker/index.md#screen_configs)
- **syncker_name** � name of the view used in the Syncker


## View Types


The list of post effect materials available for the camera is enclosed in the **<view_types/>** tag. The view type can be set via [HEMU](http://cigi.sourceforge.net/product_he.php) / [IG Host](../ig/ig_host.md), or using the *[setViewType()](../api/library/plugins/ig/api/class.view_cpp.md#setViewType_int_void)* method.


```xml
<view_types>
	<view_type type="1" post_materials="post_sensor_heat"/>
	<view_type type="2" post_materials="post_sensor_green"/>
	...
</view_types>

```


The following attributes are available:


- **id** � ID of the database (used when loading databases)
- **post_materials** � list of post effects to be applied


## Weather Layers


The list of layers defining various atmospheric effects is contained within the **<cigi_weather_layer/>** tag. You can create any number of layers as required. The visual appearance of each layer is configured using the [Weather Plugin](../ig/weather/index.md). The plugin is configured via its own configuration file `weather.config` and a set of [weather-related components](../ig/weather/settings.md).


```xml
<cigi_weather_layer>
	<layer id="1" name="cloud1" layer_type="1"/>
	<layer id="2" name="cloud2" layer_type="1"/>
	<layer id="3" name="cloud3" layer_type="1"/>
	<layer id="4" name="rain" layer_type="2" precipitation_type="1"/>
	<layer id="5" name="snow" layer_type="2" precipitation_type="2"/>
</cigi_weather_layer>

```
