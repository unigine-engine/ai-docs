# Turning Fixed-Wing Template into Your Application


Now that you have created a project and explored the template's core features, let's walk through the key steps to turn it into your own application.


## Changing the Landscape


The first thing you will likely want to replace is the default location. To create your own real-world based landscape, use the *[Sandworm](../../../editor2/sandworm/index.md)* tool.


![](../custom/img/custom_landscape.png)


**See also:**


- *Sandworm tool [detailed reference](../../../editor2/sandworm/workflow/index.md).*


### Generating Terrain with Sandworm


The **Sandworm** tool is a flexible instrument for working with online and offline georeferenced data sources. It allows you to generate scenes based on elevation data and satellite imagery, add auxiliary masks and scatter vegetation, rocks or other terrain elements, place buildings, roads, and spline- or point-based objects (e.g. fences, rivers or GSM towers) with real-world georeferencing on your landscape.


**To generate your own terrain using the *Sandworm* tool, follow these steps:**


1. Open your project in the Editor. ![](../../../sdk/projects/run_editor_cpp.png)
2. In the Editor's menu bar, click *Tools* and select ***Sandworm***. ![](../../../editor2/sandworm/interface/open_sandworm.png)
3. In the dialog window that opens, click *Create New*, then *Next*. A `*.sworm` file will be added to your project. | ![](../../../editor2/sandworm/interface/welcome_dialog_1.png) | ![](../../../editor2/sandworm/interface/project_configuration.png) | |---|---|
4. In the Sandworm tool window, click the ![Add Source(s)](../../../content/materials/graph/parameter_add.png) button to **load elevation and then imagery data**. If you use local *[georeferenced images](../../../editor2/sandworm/sources/index.md#georeferenced_image)*, you can link them as external files or *[import](../../../editor2/managing_packages/index.md#import)* into the project and store as assets. To use online images, specify the necessary *[source link(s)](../../../editor2/sandworm/faq/index.md#geodata_sources)* in the *[TMS URL](../../../editor2/sandworm/sources/index.md#tms)* list. ![](../custom/img/sw_layers.png) You can work with a single or multiple data sources, combine online and offline images, and apply different zoom levels - either to cover the same area with detailed insets or to create several separate terrain patches. For TMS sources, set the *[Boundaries](../../../editor2/sandworm/sources/index.md#boundaries)* size and then click *Create Layer(s)*.
5. Add **vector data** sources to generate buildings, roads, rivers, power lines, fences and standalone objects. Add one or more data sources for each object type. Currently, only `*.shp` and `*.geojson` file formats are supported as assets. If you have other types of files, you can try to add them as *External Files*. Best PracticeShould you have your own sets of materials, use them to vary the appearance of generated buildings. Otherwise, our *[Procedural Generation Assets](https://store.unigine.com/en/add-on/018918bd-a90a-49c8-a18e-a7eef9d05479/description)* addon provides ready-to-use materials and textures for customizing buildings generated with the Sandworm tool.

  - To generate *[Buildings](../../../editor2/sandworm/workflow/buildings/index.md)* object, click the ![Add Source(s)](../../../content/materials/graph/parameter_add.png) button in the *Objects* section and specify the data source. Use geospatial attribute *[filters](../../../editor2/sandworm/sources/index.md#filters)* to pick specific data from a vector source and create the required types of buildings only. To have access to extended building generation parameters (material, roof type, etc.), switch *[Generation Mode](../../../editor2/sandworm/sources/buildings/index.md#parameters)* to *Manual* control. Click the *Create Building Object* button. ![](../custom/img/sw_building.png)
  - To generate *[Roads](../../../editor2/sandworm/workflow/roads/index.md)* object, click the ![Add Source(s)](../../../content/materials/graph/parameter_add.png) button in the *Objects* section and select the data source. Use geospatial attribute *[filters](../../../editor2/sandworm/sources/index.md#filters)* to pick specific data from a vector source and create the required types of roads only. In the *Parameters* window, specify the prefabricated node to use. Click the *Create Road Object* button. ![](../custom/img/sw_road.png)
  - To generate *[Points](../../../editor2/sandworm/workflow/points/index.md)* object, click the ![Add Source(s)](../../../content/materials/graph/parameter_add.png) button in the *Objects* section and select the data source. Use geospatial attribute *[filters](../../../editor2/sandworm/sources/index.md#filters)* to pick specific data from a vector source and create the required types of objects only. In the *Parameters* window, specify the prefabricated node to use. Click the *Create Point Object* button. ![](../custom/img/sw_point.png)
  - To generate *[Spline Objects](../../../editor2/sandworm/workflow/lines/index.md)* (fences, pipes, lights, etc.), click the ![Add Source(s)](../../../content/materials/graph/parameter_add.png) button in the *Objects* section and select the data source. Use geospatial attribute *[filters](../../../editor2/sandworm/sources/index.md#filters)* to pick specific data from a vector source and create the required types of objects only. In the *Parameters* window, specify the prefabricated node to use. Click the *Create Spline Object* button. ![](../custom/img/sw_spline.png)
  - To generate *[Rivers](../../../editor2/sandworm/sources/rivers/index.md)* object, click the ![Add Source(s)](../../../content/materials/graph/parameter_add.png) button in the *Objects* section and select the data source. Use geospatial attribute *[filters](../../../editor2/sandworm/sources/index.md#filters)* to pick specific data from a vector source and create the required types of objects only. Click the *Create River Object* button. ![](../custom/img/sw_river.png)
6. **Vegetation** and other landscape features (such as rocks or sand) are distributed based on the data provided by **raster *[masks](../../../editor2/sandworm/workflow/mask/index.md)***. To add a new mask, click the ![Add Source(s)](../../../content/materials/graph/parameter_add.png) button and select an image source. Configure the mask filter to place objects only on the specified areas: Add a new *Vegetation* **object** and make sure the correct mask is selected in the *Mask* field. Specify the node(s) to apply - use geometry trees for high-quality close-up views and impostors for distant trees to maintain performance. Click *Create Vegetation Object*. ![](../custom/img/sw_vegetation.png)

  - **Indexed** - places objects on areas matching a specific color index from the source raster image.
  - **Single Channel** - places objects on areas matching a specific channel of the source raster image.
  - **Color** - places objects on areas matching a specific color from the source raster image.
7. Adjust *[generation settings](../../../editor2/sandworm/workflow/generate/index.md)* (coordinate system, quality, projection type, etc.) if necessary.
8. Save the `.sworm` file and click *Generate Object Lanscape Terrain* to start generation process. The landscape and all objects will be added to the scene. ![](../custom/img/sw_result.png)


### Editing the Generated Landscape


You can modify the landscape directly in the Editor if needed. Use *[Landscape Paint Mode](../../../editor2/brush_editor/index.md)* to adjust the height in specific areas or edit the masks that control the distribution of vegetation and other features across the terrain.


![](../custom/img/sw_height_modification.png)


### Organizing the Scene


Delete or disable redundant default assets (if any) which you're not going to use in your project, and adjust the position of the necessary nodes in the scene.


> **Notice:** You can specify geo-coordinates for any node that meets either of the following requirements:
>
>
> - It is positioned in the world with a georeferenced terrain generated using the *[Sandworm](../../../editor2/sandworm/index.md)* tool.
> - It is added as a child to the *[GeodeticPivot](../../../objects/geodetics/geodeticpivot/index.md)* node.


If *Point* objects are unevenly distributed or overlap with other scene elements, you can adjust their placement manually. Select the *[Mesh Cluster](../../../objects/objects/mesh_cluster/index.md)* object `Point` in the *World Nodes* hierarchy, and click *Edit* in the *Node* tab of the *Parameters* window. After that, each mesh can be positioned, rotated, and scaled manually.


## Adjusting Spawn Point


To set up a new spawn location for your vehicle:


1. Locate the `spawn_point` node in the *World Nodes* hierarchy.
2. Configure its position in the scene to match your current landscape. Make sure the `spawn_node` is above ground level.


![Spawn Point Node in Editor](../custom/img/spawn_point.png)


## Customizing Sensors


In the template, you can simulate various *[sensors](../../../sdk/templates/fixedwing/sensors.md)* (e.g., thermal imaging) using *[postprocess materials](../../../content/materials/library/postprocess/index.md)* bound to a specific *[IG View](../../../api/library/plugins/ig/api/class.view_cpp.md)* - the *[Sensor Target](../../../sdk/templates/fixedwing/sensors.md#sensor_target)*. The template comes with ***thermal white*** and ***thermal red*** sensors ready to use, but you're not limited to them - you can create your own sensors based on your project needs and switch between them at runtime using the *Sensor Configurator* window available from the main menu.


![](../custom/img/sensor_config_menu_fixed.png)


> **Notice:** Sensors can work in first-person mode (full screen) or as a Picture-in-Picture window in third-person mode.


### Replacing a Default Sensor


If you want to replace one of the existing sensors with another one available out-of-the-box, follow these steps:


1. In the UnigineEditor *World Nodes* hierarchy, under the `logic -> sensors` node, there are *Dummy* nodes named `thermal_white` and `thermal_red`, responsible for simulating the corresponding sensors. In the *Parameters* window of each node, you can see the sensors, currently set up in the project. Each sensor is configured through the parameters of the `SensorType` property. Let's replace the default white and red sensors with a green night-vision and a heat sensor.
2. Click the magnifying glass button next to the ***thermal_white*** sensor material and select the `post_sensor_advanced_green.mat` asset from the `data/modules/sensors/post_effects/post_sensor` folder. Then change the sensor *Name* to `thermal_green.`
3. Repeat the previous step for the ***thermal_red*** sensor: choose the `post_sensor_advanced_heat.mat` asset and name it `thermal_heat`. ![](../custom/img/add_sensor_fixed.png)
4. Locate the vehicle `.node` *Node Reference* file in the `data/template_assets/props` folder of the Asset Browser, and add it to the scene.
5. Select the vehicle node in the *World Nodes* hierarchy and click *Edit* in the *Parameters* window to see the source nodes of the *Node Reference*.
6. Find the `sensor_camera` node in the hierarchy - this is our *Sensor Target*. In the node's *Parameters* window, replace the default sensor names in the *Type* field of `IgSensor` property with the new ones (`thermal_green` and `thermal_heat`). ![](../custom/img/assign_sensor_fixed.png)
7. Save and run the application. Switch to first-person view mode (*N* by default). The result should look like this: ![](../custom/img/sensors.png) *Custom Green and Heat Sensors at runtime*


### Adding a New Sensor


You can also create your own postprocess materials using the base ones (for example, `post_glitch_*` for interference or `post_sensor` for thermal sensors) to simulate even more visual effects:


1. In the Asset Browser, open or create a folder to store the new material.
2. In the *Materials* hierarchy of UnigineEditor, find the base postprocess material from which your new one will inherit its properties.
3. Right-click this material and select *Create Child.* ![](../custom/img/sensor_create.png)
4. In the *Parameters* window, set up the material (e.g., replace the LUT texture with a custom one if necessary). Once that's done, the material is ready to use.
5. In the *World Nodes* hierarchy, select the node to apply the material to (it is recommended to create a new *Node Dummy* inherited from the `sensors` node) and update the existing *SensorType* property or attach a new one. Give it a unique name and select the created material in the *Material* field. ![](../custom/img/custom_sensor_fixed.png)
6. Bind the new sensor to the *Sensor Target* - `sensor_camera` node located inside the vehicle `.node` asset using the `IgSensor` property. ![](../custom/img/binding_sensor_fixed.png)
7. Save the project and run the application. Your new sensor should now appear in the *Sensor Configurator* window. [![](../custom/img/blue_sensor.png)](../custom/img/blue_sensor_s.png)


## Configuring Aircraft Instruments


When operating from a first-person cockpit view, you may need to adjust or replace individual elements or an entire *[aircraft instrument](../../../sdk/templates/fixedwing/avionics_indicators.md)*. This can be done at two levels: visual setup in the Editor and runtime control logic.


### Visual Configuration


1. Find the aircraft `.node` file in the Asset Browser and add it to the scene.
2. In the *Parameters* window, click *Edit* to view the asset's source nodes.
3. Locate the target instrument node under the `indicators` parent node in the *World Nodes* hierarchy. ![](../custom/img/custom_meters_noderef.png)
4. To replace the instrument and change its appearance, replace the property currently assigned to the node with the desired one. You can use an existing template property or create your own custom logic. ![](../custom/img/custom_meters_prop.png) *In this example, the standard compass has been replaced with a simple custom flight clock implementation*
5. Adjust the following render settings as needed: | Size | Resolution of the texture to be rendered on the instrument surface, in pixels. | |---|---| | Surface name | Name of the object surface, onto which the texture is assigned. | | Texture name | Name of the object texture into which the instrument texture is rendered. | | Settings (differ depending on the instrument) | Textures of the instrument background, and moving parts (arrows, plates) | | Runtime parameters | Parameters that read runtime data and change the instrument readings accordingly. |


> **Notice:** When replacing an instrument texture with a custom image, make sure to use the same resolution as the original to ensure proper element alignment. For custom instrument pointers (arrows), ensure they point upward and have their rotation pivot at the center of the image.


![](../custom/img/custom_meters_result.png)


### Runtime Control Logic


By default, all data-driven instruments in the template are controlled by the `AvionicsIndicatorsController` component. You can implement your own custom control logic for any instrument. The following code demonstrates this approach with the *Airspeed* indicator as an example:


```cpp
#include <UnigineComponentSystem.h>
#include <UnigineGame.h>
#include "avionics/Airspeed.h"

using namespace Unigine;

class MyFlightLogic : public ComponentBase
{
public:
		COMPONENT_DEFINE(MyFlightLogic, ComponentBase)
		COMPONENT_INIT(init)
		COMPONENT_UPDATE(update)

		PROP_PARAM(Node, airspeed_node)

private:
	void init()
	{
		// Initialize previous position
		_prevPos = node->getWorldPosition();

		// Get reference to the Airspeed component
		airspeed = getComponent<Airspeed>(airspeed_node);
	}

	void update()
	{
		if (!airspeed)
			return;

		// Calculate speed from position delta
		auto pos = node->getWorldPosition();
		double raw_speed = Math::length(pos - _prevPos) / Game::getIFps();
		_prevPos = pos;

		// low-pass filter to smooth out frame-to-frame jitter
		double alpha = Math::clamp(Game::getIFps() * 4.0, 0.0, 1.0);
		_smoothedSpeed = Math::lerp(_smoothedSpeed, raw_speed, alpha);

		// Feed speed to the instrument
		airspeed->in_speed = _smoothedSpeed;
	}

private:
	Airspeed* airspeed = nullptr;

	// Previous frame position
	Math::Vec3 _prevPos;

	// Smoothed speed value
	double _smoothedSpeed = 0.0;
};

REGISTER_COMPONENT(MyFlightLogic)

```


To implement this custom logic for the `Airspeed` instrument:


1. Open the project in your IDE and add a new `MyFlightLogic.cpp` file.
2. Paste the code and save the file.
3. In the Editor, disable default control via `AvionicsIndicatorsController` on the `cockpit` node inside the aircraft *Node Reference*.
4. Attach the `MyFlightLogic` property to a node inside the aircraft *Node Reference* (you can use the same node from step 3).
5. Drag the `airspeed_left` node into the *Airspeed Node* field of the property. ![](../custom/img/custom_logic.png)
6. Save and run the project. Now the left airspeed indicator is controlled by your `MyFlightLogic` component, which computes speed based on node movement and feeds it to the instrument's `in_speed` parameter.


For more usage examples, see the `<your_project_name>/source/template/FlightLogic.cpp` file.


## Configuring Traffic Simulation Spline


The template provides a simplified *[vehicle traffic simulation](../../../sdk/templates/fixedwing/traffic.md)*. When you change the terrain, this scene element will also need to be updated to match the new layout.


### Editing Vehicle Movement Paths


Vehicle movement follows a *[preconfigured graph.](../../../sdk/templates/fixedwing/traffic.md#create_graph)* You can either reposition and modify the default `WorldSplineGraph` node or create a new spline via *Create -> Spline Graph*, and then place control points to define the vehicle trajectory based on your current road network.


![](../../../objects/worlds/world_spline_graph/wsg_point_create.gif)


The framework uses the `.spl` file data and transforms it with the  `TrafficGraphController` component into a format used to generate the traffic graph. Therefore, make sure that:


- The `TrafficGraphController` component is assigned to the `WorldSplineGraph` node.
- In the *Graph Settings* section of the component's parameters, the output path for the generated graph is specified (or an existing graph is provided if you are reusing one). ![](../modules/traffic/img/graph_settings_json_generation.png)


### Adding custom vehicles


The template includes three vehicle types by default (`PEGASUS_CARS, BILLY_CARS, FIJI_CARS` nodes). You can replace them or add new ones as needed. To add a custom vehicle:


1. Add the desired vehicle model to the world as a *[MeshCluster](../../../objects/objects/mesh_cluster/index.md)* node: click *Create -> Cluster -> Mesh*, specify the `.mesh` file to use, and set up materials for the surfaces and LOD visibility distances. ![](../custom/img/traf_create_mesh_cluster.png)
2. After configuration, click *Edit* to access the cluster's elements and remove the visual entities from the world, leaving only the *ObjectMeshCluster* itself. Click *Apply* to save the changes. ![](../custom/img/traf_mesh_cluster_edit.png)
3. Assign the  `TrafficVehicleType` component property to the cluster node, and set the vehicle's speed in the component's parameters. Now the vehicle is ready to use. ![](../custom/img/traf_type_component.png)
4. Make sure the  `TrafficGraphController` component is attached to the `WorldSplineGraph` node.
5. In the component's parameters, adjust traffic settings and graph generation as needed, and then add the new vehicle cluster to the *Traffic Vehicle Type* field under the *Spawn Types* section to integrate it into runtime spawn. ![](../custom/img/traf_graph_component.png)


![](../custom/img/traf_custom.png)


> **Notice:** Keep in mind that excessive vehicle detail will negatively impact performance. Use the lowest possible model quality that remains visually acceptable for background traffic simulation.


## Configuring Water Traffic


The template provides a simplified *[water traffic simulation](../../../sdk/templates/fixedwing/water_traffic.md)*. When you change the terrain, the shipping lanes will also need to be updated to match the new coastline.


![](../custom/img/custom_boat.png)


### Editing Vessel Routes


A route is a *NodeDummy* carrying the `EntitySplineMovement` component, with its child nodes acting as waypoints. To change where a vessel sails, move these child nodes. Since no spline node is involved, editing a lane requires no dedicated tool - the waypoints are moved like any other node in the scene. Adding a waypoint requires adding another child to the route node.


You can create a new route by copying an existing one with its waypoints and setting the new position for the parent node (`path_*`), or build a new one from scratch:


1. Create a *NodeDummy* anywhere in the world and assign the `EntitySplineMovement` property to it.
2. Right-click the node in the *World Nodes Hierarchy* window and select *Create -> Node -> Dummy* to add a waypoint. Repeat for the other waypoints. ![](../custom/img/custom_w_route.png)
3. Place the waypoints within the water area along the lane the vessel should follow (only their horizontal position is taken into account).


The vessel **visits the waypoints in the order they are listed in the hierarchy**, not in the order they are placed in the scene, and returns from the last one to the first.


> **Notice:** Routes must stay within the area of the *[Global Water](../../../objects/objects/water/water_object.md)* object, as vessels are placed on its wave surface. The spline is built at initialization, so route changes take effect on the next world load.


### Adding a Vessel


Vessel models are **IG entities** rather than scene nodes, so a vessel is defined by two `EntitySplineMovement` component parameters: *Entity Type* selects the model declared in the *[<entity_types>](../../../ig/config.md#config_entities)* section of the `ig_config.xml` file, while *Entity Id* identifies the individual instance. A single type can back any number of instances.


Reusing a type that is already declared requires no changes to `ig_config.xml`. To bring in a model of your own, declare a new entity type, with the path to the `.node` file relative to the `data` folder:


```xml
<entity_types>
	...
	<entity id="30" name="my_ship">
		<path>my_ship/my_ship.node</path>
	</entity>
</entity_types>

```


To add your own vessel to the scene:


1. *[Import](../../../editor2/assets_workflow/assets_create_import.md)* your model into the `data` folder of the project and place it in the world. > **Notice:** The vessel node must be oriented along the **+Y** axis.
2. Drag the node from the *World Nodes* hierarchy to the Asset Browser to save it as a `.node` file. [![](../custom/img/custom_ship_add_sm.png)](../custom/img/custom_ship_add.png)
3. Declare the `.node` file in `ig_config.xml`.
4. In the `EntitySplineMovement` component's parameters of the route parent node, assign an *Entity Id* that is not used by any other vessel. ![](../modules/water_traffic/img/component.png)
5. Set *Entity Type* to the model from `ig_config.xml` this vessel should use, and adjust *Speed* (in meters per second) and *Z Offset* (negative values) to lower the vessel into the water, down to its waterline.


The *Inertion* parameter of the component sets how quickly the vessel adjusts to the surface: a lower value makes the motion smoother, which suits a small craft moving fast, and a larger hull can take a higher rate. The tilt of the vessel comes from wave heights *[measured around it](../../../sdk/templates/fixedwing/water_traffic.md#logic_water)*, at a distance proportional to its size and scaled by *Radius Factor*: smaller vessels need a larger value, as the default keeps the measurements too close to the hull for the waves to tilt it.


#### Adding a Wake


A wake is made of *DecalMesh* nodes driven by the `KelvinWake` and `TurbulentWake` properties. Such nodes can be created from scratch, or copied from a template vessel along with the materials and settings already tuned for it:


1. Place `template_assets/supply_ship/supply_ship.node` in the world and open it for *[editing](../../../objects/nodes/reference/index.md#reference_editing)*. For a small craft, take `modules/ig/entities/maritime/zodiac_boat/zodiac_boat.node` instead: copy it to the `data` folder first.
2. Copy the `wake` node with all its children - the *DecalMesh* nodes and the *NodeDummy* nodes carrying the wake properties.
3. Open the custom model for editing, paste the node as a child to the hull, and place the decals along it.
4. Set *Ship Hull* and *Ship Width* to the dimensions of the model in meters, and scale *Step Distance* accordingly - a shorter step for a smaller vessel. [![](../custom/img/custom_add_wake_sm.png)](../custom/img/custom_add_wake.png)
5. Apply the changes to save them to the `.node` file.


A wake built from scratch requires two things to be set up manually. Each *DecalMesh* node needs its own material: the wake decal is inherited from `kelvin_wake.mgraph`, the foam decals from `particles.mgraph`. And in every wake property, the *Decal Mesh Node* parameter must point to the node it drives.


A large vessel may also need *[Field Spacer](../../../objects/effects/fields/field_spacer/index.md)* nodes, which cut the water off inside the hull so that it does not show through the deck. `supply_ship.node` carries three of them shaped to the hull, the superstructure and the stern. Copy them next to the model geometry, or *[create your own](../../../objects/effects/fields/field_spacer/index.md#adding)* to match its shape.


> **Notice:** Field Spacers affect the water only if the *FieldSpacer Interaction* flag is set in the *States* section of the water material.


## Object Placement with PathPlacer


If you need to place many identical objects in your scene, you can use the **[PathPlacer](../../../sdk/templates/fixedwing/pathplacer.md)** plugin to create your own spline and define custom placement logic along it.


![](../custom/img/pathplacer_plugin.png)


To set up custom spline-based object distribution, follow these steps:


1. In the Editor, open the *Tools -> PathPlacer Plugin* window and click *Create Spline*. A new *NodeDummy* will be added to the scene with the ***[PathPlacerSpline](../../../sdk/templates/fixedwing/pathplacer.md#component_spline)*** and ***[PathPlacerSpawnNode](../../../sdk/templates/fixedwing/pathplacer.md#component_spawnnode)*** components assigned to it. The created spline has three control points by default. ![](../custom/img/workflow_create.png)
2. After creation, the plugin automatically switches to spline *Edit* mode:

  - Left-click a point to ***select*** it.
  - Use the transform gizmo that appears to ***move*** the point along one or two axes. ![](../custom/img/spline_point_gizmo.png) Alternatively, you can do the same in the *Points* section of the *PathPlacerSpline* component parameters. ![](../custom/img/spline_point_move.png)
  - To remove the ***selected*** point, press ***R***.
  - To ***add*** a new point, press ***A***. > **Notice:** A new spline point will only be added if the cursor hits an object (e.g., landscape). ![](../custom/img/edit_spline.gif) *Editing a spline*

    - A new point is created under the cursor position.
    - The point is added to the beginning or the end of the spline, depending on which side is closer.
    - If the cursor is hovering over a spline segment, the point is inserted between the two nearest neighboring points.
  - For a ***straight line*** without curves, set the *Subdivisions* parameter of the *[PathPlacerSpline](#component_spline)* component to 0 and use only two spline points.
3. Configure the parameters exposed by the *PathPlacerSpawnNode* property, assigned to the same *NodeDummy* created for the spline: specify the `.node` asset to be placed, define the distance between spawned instances, etc. ![](../modules/pathplacer/img/spawnnode_component.jpg)
4. In the *PathPlacer* plugin window, click *Generate Objects (Selected Paths)* or *Generate Objects (All Paths)*. ![](../custom/img/workflow_generate.png)

 Best PracticeYou can place different *Node References* along the same spline by adjusting their *Lateral Offset* parameter and using different *Step* values of the *[PathPlacerSpawnNode](#component_spawnnode)* component.
[![](../custom/img/two_nodes_spawned.jpg)](../custom/img/two_nodes_spawned.jpg)

*Two nodes spawned along the same spline*


> **Warning:** Only one *PathPlacerSpline* and one *PathPlacerSpawnNode* component should be assigned per node. Multiple instances may produce incorrect results.


### Practical Tips


1. Nodes are spawned along the projection of the spline onto the terrain surface. They follow the terrain while preserving the source node's transform parameters (height offset and rotation). The spline's vertical curvature affects the vertical rotation of the spawned nodes. Therefore, it is recommended that the **spline closely conform to the terrain surface** for optimal placement results. ![](../custom/img/no_elevation.jpg) *Spline with no elevation changes on an even surface* ![](../custom/img/elevation.jpg) *Spline with elevation changes on an even surface* ![](../custom/img/hills.jpg) *Spline with elevation changes on an uneven surface*
2. For easier spline positioning, parent the spline node to another one and reset its transform to leave the *Start Point* at [0, 0, 0]. Rotate the parent to orient the spline - this lets you work conveniently in local coordinates and set precise values. ![](../custom/img/tip_parent.png)
3. To spawn a single node (or one node per row), set *Step -> (Distance - Offset From Start)*. This results in a single placement at *Offset From Start* (or one node in each row if *Nodes In Row* is more than 1).


> **Warning:** Do not remove the *PathPlacerSpline* component from a node, this may lead to a crash or unexpected behavior. Remove the entire node instead.


## Configuring JSBSim


The physics of flight in the template are handled by *[JSBSim](../../../sdk/templates/fixedwing/jsbsim.md)* - an open-source C++ flight dynamics model.


By default, the project template automatically clones and builds ***JSBSim 1.2.2*** using a dedicated ***build script*** for your platform, located in `<your_project_name>\jsbsim\clone_and_build_jsbsim_*`.


### Using a Newer JSBSim Version


If you prefer to use a newer version of *JSBSim*, you must rebuild the project template locally. To simplify the rebuild process, use the same build script.


> **Notice:** It is recommended to move the script file to a separate folder before running it to keep the project clean, as the script generates files in its own directory.


1. Open the script in a text editor and change the library version to the required one: ![Change the library version to the required one, e.g., `GIT_BRANCH=v1.2.2` to `GIT_BRANCH=v1.2.3`](../custom/img/jsbsim_script_ver.png)
2. Run the script. > **Notice:** Building JSBSim requires CMake. If you already have it installed, make sure your version is compatible with your development environment. Upon completion, the script will create the following folders: ![The script will create "_build", "_stage", "artifacts", and "jsbsim-src" folders.](../custom/img/jsbsim_folder_structure.png) The `artifacts` folder structure should look like this: ```text artifacts/ ├ include   # headers ├ lib       # .lib (Windows) or .so (Linux) └ bin       # .dll (Windows only) ``` > **Notice:** On Linux, additional preparation may be required before cloning the library: > > > 1. In the terminal, run the script with superuser privileges: `sudo ./clone_and_build_jsbsim_linux.sh`. > 2. After cloning the repository from GitHub, mark the directory as safe for Git by entering: `git config --global --add safe.directory /full/path/to/jsbsim-src`. Replace `/full/path/to/jsbsim-src` with the actual absolute path to the cloned repository.
3. Copy the files:

  - `include` and `lib` folders to `<your_project_name>\jsbsim\`
  - `bin` contents to `<your_project_name>\bin`. ![](../custom/img/jsbsim_script_copy.png) > **Notice:** On Linux, the script doesn't generate the `bin` folder. Copy the `.so` files from `artifacts\lib` to `<your_project_name>\bin\`, or set `LD_LIBRARY_PATH`. > > > ![](../custom/img/jsbsim_script_linux.png)
4. Build and run the application. To check the current *JSBSim* version, run the debug build of the application from your IDE or execute `launch_debug.bat` directly from the project root folder. The *JSBSim* version will be printed to the external terminal console. ![](../custom/img/jsbsim_version.png)
