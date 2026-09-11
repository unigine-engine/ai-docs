# MRO Simulator Template


![](img/mro.png)


**MRO (Maintenance, Repair, and Operations) Simulator** is a configurable training-focused project template that serves as a foundation for creating an immersive environment for professional skill development, competency assessment, certification exams, or recurrent training.


The **default scene** contains the following elements:


- A simplified 3D model of the *TBM7* aircraft.
- An aircraft maintenance station equipped with a grounding clamp, a fuel nozzle, and a fuel sample syringe.
- A refueling ramp model.
- VR-related GUI objects for runtime use.


In the template, you can **perform various actions**: *[pick up](../../../sdk/templates/maintenance/index.md#component_objmovable)* objects, *[rotate](../../../sdk/templates/maintenance/index.md#component_objecthandlerotatable)*, and store them in the *[inventory](../../../sdk/templates/maintenance/index.md#component_vrinventory)*. Items can be connected to or disconnected from *[predefined sockets](../../../sdk/templates/maintenance/index.md#component_vrsocketobject)*. Every action is tracked in real time, and task status updates automatically as you *[progress](../../../sdk/templates/maintenance/index.md#mro_scenario)*.


The training scenario is built with the ***[Scenario Manager](../../../code/plugins/scenariomanager/index.md)*** plugin: the task chain, tooltips, and safety checks are defined as *[node graphs](../../../code/plugins/scenariomanager/index.md#graph_entry)* that you can edit visually in the *[Scenario Manager editor](../../../code/plugins/scenariomanager/editor.md)* instead of writing code. The graphs communicate with the scene through the ***[DataBridge](../../../code/plugins/databridge/index.md)*** system.


The scene is a simplified working prototype that serves as a base for further development. Its contents are only a placeholder for immediate replacement with project-specific assets. The template is **not limited to aviation**. You can replace the aircraft model with any other asset and use the template as a foundation for repair and service training across any equipment domain or in game industry projects.


The template is primarily intended for VR use. It supports all *Open VR/XR* and *Varjo VR API* *[compatible headsets](../../../vr_development/index.md#vr_devices)*, as well as multiple control and input devices (gamepads, keyboard/mouse).


## Features


The template features a training-focused simulation application designed to demonstrate key features that can be configured to meet the requirements of a wide range of simulation applications.


**Key features:**


- Aircraft maintenance and servicing simulation
- First-person interaction mode
- Tooltips for training guidance and control hints
- Visual scenario authoring via the *[Scenario Manager](../../../code/plugins/scenariomanager/index.md)* framework (no coding required)
- Training example (aircraft refueling):

  - Maintenance operations
  - Training and examination modes
  - Predefined exercises and scenarios
- Training results management:

  - Scoring and evaluation of user performance
- Support for multiple control and input devices:

  - Gamepads
  - Keyboard + mouse (in desktop mode for debugging)


## Template Scenario


The template includes a built-in scenario implemented with the *[Scenario Manager](../../../code/plugins/scenariomanager/index.md)* framework. The task chain, tooltips, and safety checks are defined as `.sgraph` node graphs stored in the `tasks/` folder, so the scenario can be modified in the *[Scenario Manager editor](../../../code/plugins/scenariomanager/editor.md)* without recompiling the project.


> **Notice:** The scenario relies on the *[Scenario Manager](../../../code/plugins/scenariomanager/index.md)* and *[DataBridge](../../../code/plugins/databridge/index.md)* plugins. Both are loaded automatically on startup.


To reach 100% completion, the user must perform a specific sequence of operations on the aircraft, following on-screen prompts and arrow indicators.


Press `M` (by default) to bring up the *[tablet](#mro_component_tablet)*, where you can find the complete task list and each task's current status.


Safety rules are checked against the current state of the aircraft and equipment: whenever a state changes, the validation graph verifies that all required conditions hold together. Breaking a rule displays an error message on the tablet, for example: `"Ground the aircraft before inserting the fuel nozzle."`


![](../maintenance/img/mro_tablet.png)


The *Validate* button runs a task completion check and prints the final result. The *Exam mode* checkbox enables knowledge testing: *[hints](#component_tooltip)* are disabled, safety checks are enabled, and per-task results stay hidden until you press *Validate*.


The *Restart* button starts the exercise all over again: all objects return to their initial places and task statuses are cleared. Keep the button pressed until the progress bar fills up to confirm the restart. The objects to be restored are defined by the *[ScenarioReset](#mro_component_scenarioreset)* component.


## Core Template Components


The nature of interaction with scene objects (moving, rotation, inventory storage) is defined by the following template components:


### Scenario Components


#### TabletController


In the Editor, the *TabletController* property is assigned to the `tablet` *Dummy Node* in the *World Nodes* hierarchy. It drives the scenario: it loads the *[Scenario Manager](../../../code/plugins/scenariomanager/index.md)* graphs, fills the tablet task list, and reports task statuses and safety messages. The following graphs are assigned to it:


- *Core script* - the scenario itself (`tasks/scenario.sgraph`), always running.
- *Education script* - tooltips and guidance (`tasks/tooltip.sgraph`), used in training mode.
- *Validation script* - safety checks (`tasks/validation.sgraph`), used in *Exam mode*.


The education and validation graphs are mutually exclusive: the *Exam mode* checkbox on the tablet selects which one runs.


The graphs never address the tablet directly - they only write to *[DataBridge](../../../code/plugins/databridge/index.md)* topics, and *TabletController* turns those topics into the task list displayed on the tablet at runtime. Two parameters specify the topics to read:


- *Tasks topic* - the parent topic of the task list. At runtime, *TabletController* takes every child topic of this one as a single task and adds a row for it to the tablet, using the values the graphs publish for that task: `display_name` for the row title, `state` for its status, and `progress` for an optional progress bar.
- *Error message topic* - the topic the validation graph writes a safety violation to. As soon as a message appears there, the run is over: the message is displayed on the tablet and every unfinished task is marked as failed.


![](../maintenance/img/component_tabletcontroller.png)


#### Tablet


In the Editor, the *[Tablet](../../../api/templates/template_aviation_maintenance/missions/class.tablet.md)* property is assigned to the `tablet` *Dummy Node* in the *World Nodes* hierarchy, and exposes the following configuration parameters:


![](../maintenance/img/component_tablet.png)


#### FuelTank


In the Editor, the *FuelTank* property is assigned to the `plane_fuel_pistol_socket` node in the *World Nodes* hierarchy. It stores the amount of fuel pumped into the aircraft and exposes the following configuration parameters:


- *Db topic* - the *[DataBridge](../../../code/plugins/databridge/index.md)* topic the tank publishes the refueling progress to, so that the scenario graphs can track it.


![](../maintenance/img/component_fueltank.png)


#### ScenarioReset


In the Editor, the *ScenarioReset* property is assigned to the `reset` *Dummy Node* in the *World Nodes* hierarchy. On startup it remembers the initial state of the listed objects, and restores it when the *[Restart](#mro_scenario)* button is pressed: their position, the *[socket](#component_vrsocketobject)* each object was connected to, and the *[inventory](#component_vrinventory)* it was stored in. The component exposes the following configuration parameters:


- *Items* - the list of objects whose initial state is saved and restored. Objects that are not on this list keep their current state when the scenario is restarted.
- *Initial plug items* - the objects that start the scenario already connected to a *[socket](#component_vrsocketobject)*.
- *Initial plug sockets* - the sockets these objects are connected to.


![](../maintenance/img/component_reset.png)


#### DataBridge Components


The scenario graphs do not access the scene directly - they exchange data with it through *[DataBridge](../../../code/plugins/databridge/index.md)* topics. The following components form that bridge:


- *VRSocketObjectDB* - publishes which item is currently plugged into a socket.
- *VRPluggableDB* - publishes what a pluggable item is connected to, and whether it is grabbed.
- *VRInventoryDB* - publishes the presence of each tracked item in the inventory.
- *TooltipDB* - reads a topic and shows or hides the corresponding *[tooltip](#component_tooltip)*.
- *NodeSwitchDB* - reads a topic and enables or disables the node it is assigned to.


The first three report the state of the world to the graphs, while the last two let the graphs affect the scene.


Each of these components has a *Db topic* parameter where you specify a name for the object, for example `plane_grounding_hook_socket`. This name is not a single value but a group: at runtime the component creates a separate *[DataBridge](../../../code/plugins/databridge/index.md)* path under it for each piece of information it handles. The graphs then read and write these paths, so the name you specify here must be the one your graphs expect. Which paths a component creates under the name, and what each of them holds, is listed in *[Preparing Assets](../../../code/plugins/scenariomanager/assets.md#how_wrapper)*.


![](../maintenance/img/component_databridge.png)


### Interaction Components


#### ObjectHandleRotatable


In the Editor, the *[ObjectHandleRotatable](../../../api/modules/vr/components/objects/class.objecthandlerotatable.md)* property is assigned to the `fuel_cap_right` node in the *World Nodes* hierarchy, and exposes the following configuration parameters:


![](../maintenance/img/component_objecthandlerotatable.png)


#### ObjMovable


![](../maintenance/img/mro_station.png)


In the Editor, the *[ObjMovable](../../../api/modules/vr/components/objects/class.objmovable.md)* property is assigned to the following nodes in the *World Nodes* hierarchy:


- `fuel_syringe`
- `clamp`
- `fuel_cap_right`
- `fuel pistol`


and exposes the following configuration parameters:


![](../maintenance/img/component_objmovable.png)


#### VRObjectPhysicalCable


In the Editor, the *[VRObjectPhysicalCable](../../../api/modules/vr/components/objects/class.vrobjectphysicalcable.md)* property is assigned to the `grounding_cable` *Dummy Node* in the *World Nodes* hierarchy, and exposes the following configuration parameters:


![](../maintenance/img/component_vrobjectphysicalcable.png)


#### FuelHose


In the Editor, the *[FuelHose](../../../api/templates/template_aviation_maintenance/scenarios/fuel_scenario/class.fuelhose.md)* property is assigned to the `fuel_hose` *Dummy Node* in the *World Nodes* hierarchy, and exposes the following configuration parameters:


![](../maintenance/img/component_fuelhose.png)


#### VRInventory


In the Editor, the *[VRInventory](../../../api/modules/vr/components/objects/class.vrinventory.md)* property is assigned to the `inventory` *Dummy Node* in the *World Nodes* hierarchy, and exposes the following configuration parameters:


![](../maintenance/img/component_vrinventory.png)


#### VRInventoryItem


![](../maintenance/img/mro_inventory.png)

*A fuel cap stored in inventory*


In the Editor, the *[VRInventoryItem](../../../api/modules/vr/components/objects/class.vrinventoryitem.md)* property is assigned to the `fuel_cap_right` node in the *World Nodes* hierarchy, and exposes the following configuration parameters:


![](../maintenance/img/component_vrinventoryitem.png)


#### VRSocketObject


In the Editor, the *[VRSocketObject](../../../api/modules/vr/components/objects/class.vrsocketobject.md)* property is assigned to the following nodes in the *World Nodes* hierarchy:


- `plane_grounding_hook_socket`
- `fuel_cap_socket`
- `plane_fuel_pistol_socket`
- `plane_fuel_sample_socket`
- `fuel_station_pistol_socket`
- `fuel_station_grounding_clamp_socket`
- `fuel_station_syringe_socket`


and exposes the following configuration parameters:


![](../maintenance/img/component_vrsocketobject.png)


#### VRPluggable


In the Editor, the *[VRPluggable](../../../api/modules/vr/components/objects/class.vrpluggable.md)* property is assigned to the `fuel_syringe` and `clamp` nodes in the *World Nodes* hierarchy, and exposes the following configuration parameters:


![](../maintenance/img/component_vrpluggable.png)


#### FuelPistol


![](../maintenance/img/mro_pistol.png)


In the Editor, the *[FuelPistol](../../../api/templates/template_aviation_maintenance/scenarios/fuel_scenario/class.fuelpistol.md)* property is assigned to the `fuel pistol` node in the *World Nodes* hierarchy, and exposes the following configuration parameters:


![](../maintenance/img/component_fuelpistol.png)


#### FuelCap


![](../maintenance/img/mro_fuelcap.png)


In the Editor, the *[FuelCap](../../../api/templates/template_aviation_maintenance/scenarios/fuel_scenario/class.fuelcap.md)* property is assigned to the `fuel_cap_right` node in the *World Nodes* hierarchy, and exposes the following configuration parameters:


![](../maintenance/img/component_fuelcap.png)


### Tooltip Components


#### Tooltip


![](../maintenance/img/mro_tips.png)


In the Editor, the *[Tooltip](../../../api/modules/vr/components/objects/tooltip/class.tooltip.md)* property is assigned to the *Dummy Nodes* named after the scenario steps (`00_open_tablet`, `01_take_clamp`, and so on) in the *World Nodes* hierarchy, and exposes the following configuration parameters:


Each of these nodes also has a *[TooltipDB](#mro_components_databridge)* property assigned, so the scenario graphs decide when the tooltip is shown.


![](../maintenance/img/component_tooltip.png)


#### SocketOutliner


![](../maintenance/img/mro_socket_outline.png)


In the Editor, the *[SocketOutliner](../../../api/modules/vr/components/objects/class.socketoutliner.md)* property is assigned to the `socket_outliner` *Dummy Node* node in the *World Nodes* hierarchy.


### VR-Specific Components


#### AttachToHand


In the Editor, the *[AttachToHand](../../../api/modules/vr/components/objects/class.attachtohand.md)* property is assigned to the `hand_menu` node in the *World Nodes* hierarchy, and exposes the following configuration parameters:


![](../maintenance/img/component_attachtohand.png)


#### AttachToHead


In the Editor, the *[AttachToHead](../../../api/modules/vr/components/objects/class.attachtohead.md)* property is assigned to the `Plane_1` and `head_menu` nodes in the *World Nodes* hierarchy, and exposes the following configuration parameters:


![](../maintenance/img/component_attachtohead.png)


#### MixedRealityMenuGui


In the Editor, the *[MixedRealityMenuGui](../../../api/templates/template_vr/gui/class.mixedrealitymenugui.md)* property is assigned to the `head_menu` node in the *World Nodes* hierarchy, and exposes the following configuration parameters:


![](../maintenance/img/component_mixedrealitymenugui.png)


#### HandMenuSampleGui


In the Editor, the *[HandMenuSampleGui](../../../api/templates/template_vr/gui/class.handmenusamplegui.md)* property is assigned to the `hand_menu` node in the *World Nodes* hierarchy, and exposes the following configuration parameters:


![](../maintenance/img/component_handmenusamplegui.png)


#### MaskHolder


In the Editor, the *[MaskHolder](../../../api/modules/vr/components/class.maskholder.md)* property is assigned to the `Common` node in the *World Nodes* hierarchy, and exposes the following configuration parameters:


![](../maintenance/img/component_maskholder.png)


#### MeshSkinnedHandMapper


In the Editor, the *[MeshSkinnedHandMapper](../../../api/modules/vr/components/players/class.ultraleapmeshskinnedhandmapper.md)* property is assigned to the `hands_1` node in the *World Nodes* hierarchy, and exposes the following configuration parameters:


![](../maintenance/img/component_meshskinnedhandmapper.png)


#### VRMeshSkinnedHandMapper


In the Editor, the *[VRMeshSkinnedHandMapper](../../../api/modules/vr/components/players/class.vrmeshskinnedhandmapper.md)* property is assigned to the `Hands` node in the *World Nodes* hierarchy, and exposes the following configuration parameters:


![](../maintenance/img/component_vrmeshskinnedhandmapper.png)


#### NodeSwitchEnableByGesture


In the Editor, the *[NodeSwitchEnableByGesture](../../../api/templates/template_vr/global/class.nodeswitchenablebygesture.md)* property is assigned to the `switcher` *Dummy Node* in the *World Nodes* hierarchy, and exposes the following configuration parameters:


![](../maintenance/img/component_nodeswitchenablebygesture.png)


#### NodeSwitchEnableByKey


In the Editor, the *[NodeSwitchEnableByKey](../../../api/templates/template_vr/global/class.nodeswitchenablebykey.md)* property is assigned to the `VR` *Dummy Node* in the *World Nodes* hierarchy, and exposes the following configuration parameters:


![](../maintenance/img/component_nodeswitchenablebykey.png)


#### VRHandController


In the Editor, the *[VRHandController](../../../api/modules/vr/components/players/class.vrhandcontroller.md)* property is assigned to the `controllers` *Dummy Node* in the *World Nodes* hierarchy, and exposes the following configuration parameters:


![](../maintenance/img/component_vrhandcontroller.png)


#### VRHandTrackingControllerOpenXR


In the Editor, the *[VRHandTrackingControllerOpenXR](../../../api/modules/vr/components/players/class.vrhandtrackingcontrolleropenxr.md)* property is assigned to the `controllers` *Dummy Node* in the *World Nodes* hierarchy, and exposes the following configuration parameters:


![](../maintenance/img/component_vrhandtrackingcontroller_openxr.png)


#### VRHandTrackingControllerUltraleap


In the Editor, the *[VRHandTrackingControllerUltraleap](../../../api/modules/vr/components/players/class.vrhandtrackingcontrollerultraleap.md)* property is assigned to the `controllers` *Dummy Node* in the *World Nodes* hierarchy, and exposes the following configuration parameters:


![](../maintenance/img/component_vrhandtrackingcontroller_ultraleap.png)


#### VRPlayerSpawner


In the Editor, the *[VRPlayerSpawner](../../../api/modules/vr/components/class.vrplayerspawner.md)* property is assigned to the `spawn_point` *Dummy Player* node in the *World Nodes* hierarchy, and exposes the following configuration parameters:


![](../maintenance/img/component_vrplayerspawner.png)


## Main Menu


At runtime, click the ***Windows*** button in the top-left corner to open the main menu, from which the **Quality Settings** configuration panel can be accessed. Switch between rendering presets: *(Low / Medium / High)* in VR/PC modes.


![](../maintenance/img/mro_main_menu.png)


In the Editor, the Quality Presets widget is configured via the *WidgetQualitySettings* property, assigned to the `quality_settings` node.


![](../maintenance/img/component_ui.png)
