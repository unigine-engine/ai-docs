# Fixed-Wing Template - Avionics HUD Simulation


The template contains a framework for simulating an aircraft HUD (heads-up display) - a transparent display system that projects flight instrument data into the camera's view.

 ![](../modules/avionics_hud/img/hud_framework_fixed.png)
The HUD replicates the information displayed on the *[cockpit instruments](../../../sdk/templates/fixedwing/avionics_indicators.md)*.


## Avionics HUD Configuration


The framework's functionality is implemented as follows:


- **In the Editor**, the `FlightLogic` and `AvionicsHUD` components are attached to the `flight_logic` *Node Dummy* via the corresponding properties, and allow editing the following HUD-related parameters: ![](../modules/avionics_hud/img/hud_component.png) *Select which elements of HUD must be enabled by default at runtime, set the display color and speed units.*
- **At runtime**, the displayed data is controlled through the *[HUD Configurator](#user_interface)* window, accessible from the main menu. The HUD values update dynamically from the `FlightLogic` component's `in_*` parameters (such as `in_speed`, `in_altitude`) and can be modified at runtime. In the template, these values are provided by *[JSBSim](../../../sdk/templates/fixedwing/jsbsim.md#prop_data_exchange)*. ```cpp avionics_hud->in_rudder = fdm->getNodeValue<float>(property_nodes.rudder); avionics_hud->in_ground_speed = fdm->getNodeValue<float>("velocities/vg-fps") / 1.687809; avionics_hud->in_pitch = Consts::RAD2DEG * fdm->getNodeValue<float>("attitude/pitch-rad"); ``` ![](../modules/avionics_hud/img/hud_labeled.png) The complete list of **in_*** parameters is available in the *[AvionicsIndicatorsController](../../../api/modules/avionics/class.avionicsindicatorscontroller.md)* class. For more usage examples, see the `<your_project_name>/source/template/FlightLogic.cpp` file.


## User Interface


The framework provides a `HUD Configurator` widget for selecting which data should be displayed in the HUD at runtime. In UnigineEditor, the configurator logic is assigned to the *hud_configurator* Node Dummy via the `AvionicsHUDConfigurator` property.


![](../modules/avionics_hud/img/hud_configurator.png)


### Disabling HUD for Particular Cameras


To disable the HUD for a particular camera view of an aircraft:


1. Locate the aircraft `.node` file in the Asset Browser and add it to the scene.
2. In the *Parameters* window click *Edit* to see the source nodes of the *Node Reference*.
3. Select the target camera from the list and click *Add New Property* in its *Parameters* window.
4. Type `Tag` in the field that opens, select the property, and specify `hide_hud` in the *Value* field.


![](../modules/avionics_hud/img/hide_hud.png)
