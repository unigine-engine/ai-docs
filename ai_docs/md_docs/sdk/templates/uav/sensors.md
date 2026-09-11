# UAV Template - Sensors Simulation


The template provides a framework (*[API](#api)* and a set of *[postprocess materials](../../../content/materials/library/postprocess/index.md)*) for simulating various sensors, such as a thermal imaging camera, visual interference effects, or other sensor-like visual augmentations.


The system supports rendering a camera with active sensors either in **first-person view (fullscreen)** or as a **Picture-in-Picture (PiP)** display at runtime.


![](../modules/sensors/img/sensor_pip.png)


## Core Concepts


| Sensor | In this framework, a *sensor* is a postprocess material bound to one or more [*Sensor Targets*](#sensor_target) that simulates a specific imaging effect (e.g., thermal or night vision). Sensors operate at the rendering level and are dynamically enabled or disabled at runtime. |
|---|---|
| Sensor Manager | *Sensor Manager* is the central system that stores all information about sensor states, and provides a unified *[API](#api)* for working with sensors through code. In the template, *Sensor Manager* is implemented via the *[SensorManager](#sensormanager_component)* component. |
| Sensor Target | *Sensor Target* is the rendering output to which a sensor is bound. In the template, *Sensor Target* is implemented as a *[Player](../../../objects/players/index.md)* node with the *[Sensor](#sensor_component)* component and a *sensor_camera* *[tag](#tag_component)* attached. |
| Sensor Type | *Sensor Type* defines a specific sensor effect. Each *Type* is identified by a unique name and is associated with a single base postprocess material that determines its core behavior. The framework includes a set of predefined postprocess materials located in the `data/` directory. You can *[create your own Sensor Types](../../../sdk/templates/uav/custom.md#custom_sensors)*, using the template's base materials as a foundation. In the template, *Sensor Types* are implemented via the *[SensorType](#sensortype_component)* component. |


## Sensor Framework Structure


This section demonstrates how the *[core concepts](#core_concepts)* are implemented in the system and interact through sensor-related components.


### SensorManager Component


*[Sensor Manager](#sensor_manager)* operates through the *SensorManager* component, which can be assigned to any node in the world. In the template, it is attached to a *Node Dummy* named `sensors`.


![SensorManager Component in the Editor](../modules/sensors/img/sensor_manager.png)


### SensorType Component


*SensorType* component determines the functionality of a specific *[Sensor Type](#sensor_type)*. Just like the *SensorManager* component, it can be assigned to any node in the world, however, for convenience, it is recommended to place it on the same node. During world initialization, *SensorManager* automatically discovers and registers all *SensorType* components.


In the template, it is also assigned to the `sensors` node.


Each *Sensor Type* is defined by:


- *a unique name* - the identifier for binding *[Sensors](#sensor_concept)* to *[Targets](#sensor_target)*;
- *a base postprocess material* - the material that determines the visual behavior of a sensor, for example:

  - **post_depth** for depth sensors;
  - **post_glitch_*** for interference effects;
  - **post_sensor** for heat sensors.


![SensorType Component in the Editor](../modules/sensors/img/sensor_type.png)


### Sensor


***Sensor*** binds a *[Sensor Type](#sensor_type)* to a *[Sensor Target](#sensor_target)*, specifying which sensor to use for a particular camera. Multiple *Sensor* properties can be used on the same *Player* node, making more than one sensor available at runtime.


> **Warning:** The *Sensor* component must be assigned to a *[Player](../../../objects/players/index.md)* node.


When assigned, the component exposes the following parameters:


- **Type** - the *[unique name](#sensor_type_name)* of the *Sensor Type* to be used;
- **Enabled** - the parameter that sets the initial state of the sensor at application startup.


> **Warning:** For correct work, the *Sensor Target* node must also have the *[Tag](#tag_component)* property with the `sensor_camera` parameter set.


In the template, the component is assigned to the `firstperson_camera` *Player Dummy* node, located inside the vehicle *Node Reference* (accessible in the *[Edit](../../../objects/nodes/reference/index.md#reference_editing)* mode).


![](../modules/sensors/img/sensor_uav.png)


### Tag Component


*Tag* is an auxiliary component for labeling cameras and sensors according to their intended purpose. It supports the following parameters:


- `main_camera` - selects the default camera on the application startup (`thirdperson_camera` node in the template);
- `sensor_camera` - selects the camera used for rendering sensor effects (also displayed in the *[PiP](#widgetpictureinpicture_component)* view);
- `rolling_shutter_camera` - enables fast movement distortion effects (e.g., in rotor blades) for the camera.


![](../modules/sensors/img/tag_uav.png)


### UI Components


The following UI components are designed for managing sensors and displaying their output in a separate viewport at runtime. In the Editor, UI-related components are typically assigned to a *Dummy Node*. In the template, thes nodes with UI-components are grouped under the `ui` parent node.


![](../modules/sensors/img/ui_components_uav.png)


#### WidgetSensorConfigurator


At runtime, the `WidgetSensorConfigurator` component creates a *Sensor Configurator* window that displays the following information:


- A list of all sensors initialized by the *[Sensor Manager](#sensor_manager)*;
- *[Sensor Types](#sensor_type)* and their system IDs;
- Bound *[Sensor Targets](#sensor_target)*.


The *Configurator* allows enabling and disabling individual sensor bindings via the *Enabled* checkbox, and also indicates the current state of the sensor binding (*Active* - sensor binding is currently active).


In the template, this component is assigned to the `sensor_configurator` *Dummy Node*.


![](../modules/sensors/img/widgetsensorconfigurator_component.png)

*WidgetSensorConfigurator component in the Editor and Sensor Configurator window at runtime*


#### WidgetPictureInPicture


The `WidgetPictureInPicture` component enables a *Picture-in-Picture (PiP)* widget that renders the output of a camera, marked with the `sensor_camera` *[tag](#tag_component)*. In the Editor, `WidgetPictureInPicture` is attached to the `pip_display` node and allows configuring the default position, offset, and size of the PiP window.


![](../modules/sensors/img/widgetpictureinpicture_component.png)

*WidgetPictureInPicture component in Editor*


[![](../modules/sensors/img/pip_widget.png)](../modules/sensors/img/pip_widget.png)

*Picture-in-Picture widget at runtime*


#### WidgetPictureInPictureConfigurator


The `WidgetPictureInPictureConfigurator` component creates a configuration window for the *Picture-in-Picture* widget at runtime, used to adjust the position and size of the PiP widget.


In the Editor, it is attached to the `pip_configurator` node. When assigned, the component requires a reference to the node with the *[WidgetPictureInPicture](#widgetpictureinpicture_component)* component (`pip_display` in the template). This component also allows setting the default state (enabled/disabled) and position of the PiP window at application startup.


![](../modules/sensors/img/widgetpictureinpictureconfig_component.png)

*WidgetPictureInPictureConfigurator component in the Editor, and Picture-in-Picture configurator window at runtime*


## Framework API


The *[API](../../../sdk/templates/uav/api.md)* provides direct access to sensor creation, binding, state control, and synchronization via the following classes:


- *[Sensor Class](../../../api/modules/sensors/class.sensor.md)*
- *[SensorManager Class](../../../api/modules/sensors/class.sensormanager.md)*
- *[SensorTarget Class](../../../api/modules/sensors/class.sensortarget.md)*
- *[SensorTypeComponent Class](../../../api/modules/sensors/class.sensortypecomponent.md)*
- *[WidgetPictureInPicture Class](../../../api/modules/sensors/class.widgetpictureinpicture.md)*
- *[WidgetPictureInPictureConfigurator Class](../../../api/modules/sensors/class.widgetpictureinpictureconfigurator.md)*
- *[WidgetSensorConfigurator Class](../../../api/modules/sensors/class.widgetsensorconfigurator.md)*
