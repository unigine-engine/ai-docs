# Turning UAV Template into Your Application


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


### Updating Minimap


Once the scene is ready, you will probably want to update the minimap to match your new landscape. To customize the minimap:


1. Go to *Create -> Camera -> Dummy* and place a new camera in the scene.
2. In the camera *Parameters* window, set *Projection Mode* to *Orthographic* and switch to this camera view. ![](../../../learn/11_fps/img/switch_camera.png)
3. Raise the camera above the terrain by adjusting the *Height* value, then set the *Near Clipping* and *Far Clipping* parameters as needed. The required camera height depends on your landscape size and project requirements. ![](../custom/img/sw_minimap_height.png) > **Notice:** If the ground starts to fade out after raising the camera *Height*, increase the visibility distance value: go to *Settings -> Landscape -> Geometry -> Visibility Distance*.
4. From the menu bar, select *Tools -> Video Grabber*. In the *Camera* drop-down, choose the camera you created. Set the desired parameters (destination folder, resolution, etc.) and capture a single frame.
5. In the *World Nodes* hierarchy, locate and select the `minimap` node. In the node's *Parameters* window, under the `MinimapUI` node property, replace the default *Map Image* file with your captured shot. ![](../custom/img/sw_minimap.png) > **Notice:** If the *Map Image* is missing, the minimap is hidden and the corresponding message is reported to the console.
6. In the *Map* section of the property, replace the *Origin Offset* values with the X and Y coordinates of the camera you created. ![](../custom/img/sw_minimap_offset.png)
7. Set the *Pixel To Unit Ratio* parameter based on your minimap resolution and your camera *Height* (for example, if the frame resolution is 2560x2560 and the camera *Height* is 1280, the *Pixel To Unit Ratio* is 2).
8. Adjust other parameters as needed (marker icons, map zoom, flight path trail thickness and color, widget settings, etc.).


![](../custom/img/sw_minimap_result.png)


The appearance of the minimap is defined by the following parameters of the `MinimapUI` property:


| Parameter | Description |
|---|---|
| Border Shape | Shape of the minimap boundary - *Circle* or *Rect*. The map, the trail, and the ruler are clipped by it. |
| Rotation Mode | *Head Up* rotates the map with the heading of the vehicle, keeping the player marker fixed. *North Up* keeps the map oriented to the north and rotates the player marker instead. |
| Ruler Style | Distance ruler drawn over the map: *Concentric* rings around the vehicle, a *Grid*, or *None*. Distances are labeled in meters and follow the current zoom. Use *Ruler Spacing* to set the interval between the rings or the grid lines. |
| Trail Min Distance Trail Max Points | How often the flight path trail records a point, in meters, and how many points are kept - the oldest ones are dropped past this limit. |


The map zoom can be tied to the flight altitude: the `MinimapController` property assigned to the same `minimap` node provides the *Zoom Curve* parameter, where you can use the *[Curve Editor](../../../editor2/curve_editor/index.md)* to define how the height above the `home` node scales the map.


## Adjusting Spawn Point and Signal Range


If you see the *Signal is Lost* message when running the application, it means the UAV is beyond the defined communication range determined by the geo-coordinates of the `home` node.


![Signal is Lost](../custom/img/lost_signal.png)


Here are the two most likely reasons for that:


1. **You changed the position of the UAV node in the Editor** (e.g., after replacing the default landscape). Configure the positions of two key nodes: the `home` node (controls the signal coverage area) and the `spawn` node (sets the initial spawn point for the devices) in the scene to match your current landscape. Make sure the `spawn` node is above the ground level. ![](../custom/img/nodes_reposition.png)
2. **The UAV has flown too far from the `home` node for the current coverage radius.** To change the signal coverage radius: The `Distance to Noise` parameter of the `RadioModule` component allows you to use the *[Curve Editor](../../../editor2/curve_editor/index.md)* to define how the distance from the base (`home` node) affects GNSS signal quality. This parameter also affects the level of visual interference on [camera sensors](#custom_sensors) based on signal quality - it passes the current noise level to the `Camera` component assigned to the `camera` node, which then applies the specified noise sensor - `noise analog` - to the corresponding camera.

  - In the *World Nodes* hierarchy, select the UAV *Node Reference* and click *Edit* in the *Parameters* window.
  - Inside the *Node Reference*, find the `radio` *Dummy Node*.
  - In the `RadioModule` component assigned to the node, set the *Max Distance* and *Max Height* values as needed (in units). ![](../custom/img/sw_signal.png) > **Notice:** If the target UAV node is not present in the world, locate it in the Asset Browser, place it in the scene, and delete from the hierarchy after finishing the editing process.


## Adding Your UAV Model


You can replace the default UAV models with custom ones, or add a new UAV entity.


### Replacing an Existing Vehicle


To replace an existing model:


1. In the Editor, select the `sim_info` node in the *World Nodes* hierarchy.
2. In the *Parameters* window, locate the `SimInfo` property attached to the node.
3. Press ![Select Asset](../custom/img/select_asset.png) and specify the vehicle `*.node` file.


![](../custom/img/entity_replace.png)


### Adding an Additional Vehicle


To add an extra entity:


Select the `sim_info` node in the *World Nodes* hierarchy and increase the value of the `Drone (Files)` parameter of the `SimInfo` property. Specify the additional vehicle in the new entry.


![](../custom/img/add_vehicle.png)


> **Notice:** Different UAVs may have different sets of articulated parts (controlled elements - such as rudders and ailerons for fixed-wing devices) and components that define flight configuration depending on the particular vehicle.


You can view the full set of articulated parts for any default UAV by selecting its *Node Reference* in the *World Nodes* hierarchy and examining its internal structure. Control over these elements is implemented via components assigned to the child nodes of the `components` node. If you use a custom vehicle, you will need to assign and configure the appropriate components to replicate the default behavior, or implement your own custom logic, otherwise, some elements of a custom vehicle might work incorrectly or not at all.


![](../custom/img/uav_elements.png)


### Custom UAV Behavior Configuration


The behavior of default drones is defined by their components. When adding a custom UAV, make sure to specify its type by attaching the `Drone` component and selecting the correct flight model (e.g., ***Multirotor, FixedWing, VTOL***).


![](../custom/img/drone_components.png)


The selected flight model comes with its own property, where the flight parameters are stored as a list of *Configs* - a vehicle can have several of them and switch between them at runtime. Fill in at least one configuration and mark it as *Default*, taking the properties of the default drones as a reference.


### Catapult Configuration


A fixed-wing UAV can be launched from a *[catapult](../../../sdk/templates/uav/index.md#catapult_launch)* instead of taking off from the runway. In the template the catapult node file (`launcher.node` that holds the rail, the moving platform, and the legs geometry of the catapult itself) and the drone node are stored together in the `launcher_airplane.node` file, located in the `data/template_assets/props/launcher` folder of the Asset Browser. To launch your own fixed-wing UAV from the catapult, take this file as a starting point, replace the drone *Node Reference* in it with your own, adjusting the position so that the aircraft rests on the platform, and *[add](#add_replace)* the result to the *Drones (Files)* list of the `SimInfo` property as described above.


The launch is handled by the `UAVLaunch` component assigned to the `launcher` root node of the catapult. Its parameters refer to the nodes of the catapult and define how fast the aircraft leaves the rail:


| Parameter | Description |
|---|---|
| Start Node End Node | The beginning and the end of the launch track. Together they set the direction of the launch and the length of the run-up. With the same *Exit Speed*, a longer track makes the acceleration gentler, and a shorter one makes it more abrupt. |
| Platform Node | The carriage that travels along the track and carries the aircraft. |
| Mount Point | The point the aircraft is locked to before the launch. Its orientation defines the angle at which the aircraft is released. |
| Exit Speed | The speed the aircraft reaches at the end of the track and keeps after the release. It should exceed the stall speed of your flight model, otherwise the aircraft will be released too slow to stay in the air. |


> **Notice:** The catapult only handles vehicles whose `Drone` component uses the *[FixedWing flight model](#uav_flight_model)*.


### Camera Configuration


Default drone models contain two camera nodes inside their `.node` asset:


- `thirdperson_camera` - has a `Tag` component attaced with the `main_camera` label. This is the default camera.
- `firstperson_camera` - simulates an onboard camera. It can be used in fullscreen mode (toggle with the *N* key at runtime by default) or as a *[Picture-in-Picture](#pip)* *(PiP)* view. This camera has *[Sensor](#custom_sensors)* components attached to define which sensors are available at runtime, and `Tag` components with the `sensor_camera` and `rolling_shutter_camera` (for image distortion simulation) labels.


### Battery and Telemetry Configuration


The device **battery level** is controlled by the `Battery` component assigned to the `battery` node inside the device's *Node Reference*. In the Editor, you can adjust the initial charge *level* and the battery discharge *rate*.


![](../custom/img/battery.png)


The displayed telemetry parameters (e.g., geoposition, altitude, etc.) are implemented in the `TelemetryUI` component, which is assigned to the `telemetry` node in the *World Nodes* hierarchy. In the Editor, you can adjust the font settings and telemetry offset parameters.


![](../custom/img/hud.png)


### Device Loading and Configuration Storage


At runtime, the system loads the first device that exists as an instance in the world (even if not specified in the *Drones (File)* list). If no device *Node Reference* is present, you can set the *Default Drone* parameter of the `SimInfo` component to select the device to be used at startup.


If you check the *Save To File* parameter, the current `SimInfo` component settings will be written to a `sim_info.xml` file inside the project's `data/` folder at application launch.


## Adapting ArduPilot SITL To Your Project


The template includes a fully functional autopilot system built on *[ArduPilot](https://ardupilot.org/)* firmware. This system can be reused in your own project following the same integration *[structure](../../../sdk/templates/uav/sitl.md#sitl_architecture)*.


An important *[separation](../../../sdk/templates/uav/sitl.md#sitl_architecture)* to keep in mind is that the bridge - the `ardupilot_sitl` module - is a reusable protocol, while `SITL_Integration` is what defines the vehicle semantics. Therefore, as a starting point, you can copy the `SITL_Integration.{h,cpp}` component into your project and rework only the vehicle-facing parts of your own drone, while `ardupilot_sitl` will be used as-is.


### What The Bridge Provides


The `ArduPilotSITLBridge` class is a plain owned type - not a scene component. Your integration code holds an instance of it and calls its methods.


- `init(port) / shutdown()` - starts/stops the network thread. ArduPilot's JSON interface expects port 9002.
- `getInputs(pwm[16])` - the latest 16 servo PWM values from ArduPilot (1000-2000 �s range).
- `setSensorState(state)` - the sensor reply. The bridge answers every incoming SITL frame with the latest state you set; you just keep it fresh each physics tick.
- `getFrameStats(rate, count)` - SITL's frame rate and a monotonically increasing frame counter, for diagnostics and link-liveness tracking.
- `clearIO()` - zeroes the exchanged I/O; call it on link loss so stale PWM/sensor values don't linger. It leaves the frame stats alone, so liveness tracking still sees the counter stop advancing.


All of these methods are thread-safe: the network thread services the socket, and your code calls them from the physics tick.


### Frame Conversion


ArduPilot and Unigine use different coordinate systems:


- **World frame**: Unigine uses ENU (East-North-Up), ArduPilot uses NED (North-East-Down)
- **Body frame**: Unigine uses X-right, Y-forward, Z-up; ArduPilot uses forward-right-down (FRD)


The conversion is implemented in one place - fill a `UnigineSensorState` with plain Unigine values and call `arduPilotSensorStateFromUnigine()`. Do not hand-convert in your integration code.


`UnigineSensorState::accel` is the plain acceleration of the body in the world frame (e.g. finite-differenced velocity), **not** what an accelerometer reads. Gravity is added during the conversion.


The example integration derives it as *`(velocity - last_velocity) / dt`* with a light low-pass filter, and re-seeds `last_velocity` when the link comes up so the first frame after connecting mid-flight doesn't produce an acceleration spike.


### What Your Integration Owns


The example integration performs three tasks on each physics tick, so should your implementation of it too:


1. **Push PWM values into the vehicle** What the channels mean depends entirely on which firmware is running:

  - **ArduCopter** - drives one motor per channel. The example maps channels to rotors by name (*CHANNEL_MAP* in *CopterIntegration*). The default mapping assumes a quad-X layout. This map must agree with the *FRAME_CLASS* and *FRAME_TYPE* parameters, which is exactly why the `.parm` file explicitly sets them. If you change the airframe, you must edit both the channel map and the parameters together.
  - **ArduPlane** - channels 0-3 carry aileron, elevator, throttle, and rudder (ArduPlane's default *SERVOn_FUNCTION* assignment). Surfaces are signed around the 1500 �s neutral, throttle is 0-1, signs follow ArduPilot conventions (aileron + = roll right, elevator + = nose up, rudder + = yaw right).
2. **Send the drone's current state to the sensors** Read your vehicle's current state (position, velocity, orientation, angular velocity), derive acceleration, convert the results with the helper, and call *setSensorState()*.
3. **Track link liveness and hand over control** The example polls *getFrameStats()* each tick. If the frame counter advances, ArduPilot is alive. If the counter freezes for 1 second, the link is considered lost. On the transition, the example calls *clearIO()*, zeroes the vehicle inputs (so motors don't freeze on stale throttle), and flips the flight model between external control (ArduPilot) and internal (the template's own flight model - manual flight). The comparison is `!=`, not `>`, because restarting SITL rewinds the counter to a lower value.


The handoff logic in **step 3** is the reason the template's flight models stay generic. They only expose a control-source switch (`ControlSource::EXTERNAL / INTERNAL`) and accept inputs - nothing more. If you have your own vehicle code, follow this pattern: keep ArduPilot knowledge out of the vehicle, and let the integration own the switch.


The HUD and the debug visualizer in the example (*SITLHud, FlightViz*) are optional conveniences - you may keep or remove them.


### Startup Wiring


The example registers itself from *AppSystemLogic::init()* via *SITL_Integration::get()->initialize()*, gated behind the **`-sitl`** launch flag. If the flag is absent, no SITL code runs at all.


*initialize()* parses the vehicle name from the flag (copter or plane) and registers the *WorldLogic*. Once registered, everything else hangs off the normal world *init/shutdown* callbacks.


## Customizing Sensors


In the template, you can simulate various *[sensors](../../../sdk/templates/uav/sensors.md)* (e.g., thermal imaging or *[interference](#distance_to_noise_param)*, or other effects) using *[postprocess materials](../../../content/materials/library/postprocess/index.md)* bound to a specific *Player* node (camera) - the *[Sensor Target](../../../sdk/templates/uav/sensors.md#sensor_target)*. The template comes with ***thermal white*** and ***thermal red*** sensors ready to use, but you're not limited to them - you can create your own sensors based on your project needs and switch between them at runtime using the *Sensor Configurator* window available from the main menu.


![](../custom/img/sensor_config_menu_uav.png)


> **Notice:** Sensors can work in first-person mode (full screen) or as a Picture-in-Picture window in third-person mode.


### Replacing a Default Sensor


If you want to replace one of the existing sensors with another one available out-of-the-box, follow these steps:


1. In the *World Nodes* hierarchy of UnigineEditor, find and select the `sensors` node. In the *Parameters* window, you'll see all sensors currently set up in the project. Each sensor is configured through the parameters of the `SensorType` property. Let's replace the default white and red sensors with a green night-vision and a heat sensor.
2. Click the magnifying glass button next to the ***thermal_white*** sensor material and select the `post_sensor_advanced_green.mat` asset from the `data/modules/sensors/post_effects/post_sensor` folder. Then change the sensor *Name* to `thermal_green.`
3. Repeat the previous step for the ***thermal_red*** sensor: choose the `post_sensor_advanced_heat.mat` asset and name it `thermal_heat`. ![](../custom/img/add_sensor.png)
4. Locate the vehicle `.node` *Node Reference* file in the `data/template_assets/props` folder of the Asset Browser, and add it to the scene (the default FPV drone is already added to the world by default).
5. Select the vehicle node in the *World Nodes* hierarchy and click *Edit* in the *Parameters* window to see the source nodes of the *Node Reference*.
6. Find the `firstperson_camera` node in the hierarchy - this is our *Sensor Target*. In the node's *Parameters* window, replace the default sensor names in the *Type* field of `Sensor` property with the new ones (`thermal_green` and `thermal_heat`). ![](../custom/img/assign_sensor.png)
7. Save and run the application. Switch to first-person view mode (*N* by default). The result should look like this: ![](../custom/img/sensors.png) *Custom Green and Heat Sensors at runtime*


### Adding a New Sensor


You can also create your own postprocess materials using the base ones (for example, `post_glitch_*` for interference or `post_sensor` for thermal sensors) to simulate even more visual effects:


1. In the Asset Browser, open or create a folder to store the new material.
2. In the *Materials* hierarchy of UnigineEditor, find the base postprocess material from which your new one will inherit its properties.
3. Right-click this material and select *Create Child.* ![](../custom/img/sensor_create.png)
4. In the *Parameters* window, set up the material (e.g., replace the LUT texture with a custom one if necessary). Once that's done, the material is ready to use.
5. In the *World Nodes* hierarchy, select the `sensors` node and update the existing *SensorType* property or attach a new one. Give it a unique name and select the created material in the *Material* field. ![](../custom/img/custom_sensor.png)
6. Bind the new sensor to the *Sensor Target* - `first_person_camera` node located inside the vehicle `.node` asset using the `Sensor` property. ![](../custom/img/binding_sensor.png)
7. Save the project and run the application. Your new sensor should now appear in the *Sensor Configurator* window. [![](../custom/img/blue_sensor.png)](../custom/img/blue_sensor_s.png)


## Configuring Traffic Simulation Spline


The template provides a simplified *[vehicle traffic simulation](../../../sdk/templates/uav/traffic.md)*. When you change the terrain, this scene element will also need to be updated to match the new layout.


### Editing Vehicle Movement Paths


Vehicle movement follows a *[preconfigured graph.](../../../sdk/templates/uav/traffic.md#create_graph)* You can either reposition and modify the default `WorldSplineGraph` node or create a new spline via *Create -> Spline Graph*, and then place control points to define the vehicle trajectory based on your current road network.


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
