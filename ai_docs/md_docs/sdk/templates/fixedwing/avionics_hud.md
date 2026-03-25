# Fixed-Wing Template - Avionics HUD Simulation


The template contains a framework for simulating aircraft HUD - a transparent display system that projects flight instrument data directly in the pilot’s forward field of view.


![](../modules/avionics_hud/intro.gif)


The framework provides the HUD configurator that allows configuring the scope of the displayed data at runtime, while its visual representation (such as projection color, data to be visualised by default) is configured in the Editor.


## Configuring Avionics HUD


To visualize dynamic values correctly, the instruments must be configured as follows:


- **In the Editor**: assign the **[AvionicsHUD](#settings)** property to the **FlightLogic** node.
- **In the logic**: [changes to the corresponding **in_*** parameters](#logic) (such as `in_speed, in_altitude`) drive the visual updates of the instruments.


## Avionics HUD Settings and Parameters


The template includes the **AvionicsHUD** property assigned to the **FlightLogic** node.


![](../modules/avionics_hud/hud_component.png)


This component allows you to define which instrument data is visualized on the HUD, as well as the projection color.


## Updating Values At Runtime


The runtime parameters exposed by this component can be modified at runtime:


```cpp
avionics_hud->in_rudder = fdm->getNodeValue<float>(property_nodes.rudder);
avionics_hud->in_ground_speed = fdm->getNodeValue<float>("velocities/vg-fps") / 1.687809;
avionics_hud->in_pitch = Consts::RAD2DEG * fdm->getNodeValue<float>("attitude/pitch-rad");

```


The whole list of **in_*** parameters is available in *AvionicsIndicatorsController*.


For more details on usage, see the `FlightLogic.cpp` file.


## User Interface


The user interface for configuring the HUD display scope at runtime is implemented using the **AvionicsHUDConfigurator** property, which is assigned to the *hud_configurator* Node Dummy in the template.

  ![](../modules/avionics_hud/hud_config_window_1.jpg)  ![](../modules/avionics_hud/hud_config_window_2.jpg)  ![](../modules/avionics_hud/hud_config_window_3.jpg)  ![](../modules/avionics_hud/hud_config_window_4.jpg)
