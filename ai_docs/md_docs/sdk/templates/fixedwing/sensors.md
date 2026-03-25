# Fixed-Wing Template - Sensors Simulation


The template provides the framework (API and a set of post-processing materials) for adding various sensors such as a thermal imaging camera, visual interference effects, or other sensor-like visual augmentations.


The system supports rendering a camera with active sensors into a Picture-in-Picture display. Using the PiP Display and Sensor Configurator UI windows, sensors can be enabled or disabled dynamically, and the PiP display can be repositioned on the screen.


![](../modules/sensors/pip_thermal_white.jpg)


## Core Concepts


| Sensor | In the context of this framework, a sensor is a post-processing material that is bound to one or more targets. Sensors operate entirely at the rendering level and can be dynamically enabled, disabled, or reconfigured at runtime. |
|---|---|
| Sensor Type | A sensor type defines a class of sensors based on a shared base post-processing material. This base material specifies the fundamental behavior of the sensor, while all sensors of the same type inherit from it and customize their behavior through parameters. Each sensor type is uniquely identified by name and is associated with a single base post-material. The framework provides a small set of predefined post-materials located in the `data/` directory. |
| Sensor Target | A sensor target is the rendering output to which a sensor is bound. Targets include: - Engine Player - IG View |
| Sensor Manager | The Sensor Manager is the central system responsible for managing all sensors. It stores their state, synchronizes them when [Syncker](../../../code/plugins/syncker/index.md) or [IG](../../../ig/index.md) is used, and exposes a unified API for managing sensors through code. |


## Configuring Sensors


The approach to configuring the sensors is as follows:


1. Assign the *SensorManager* component to any node in the world.
2. Create a Node Dummy and assign the [SensorType](#sensortype_component) component to it. Set a unique name and select the post material that will create a sensor-like effect.
3. Create a Node Dummy and assign the [WidgetSensorConfigurator](#widgetsensorconfigurator_component) component to it - it will create a window at runtime to view all sensors.
4. Create a Node Dummy and assign the [WidgetPictureInPicture](#widgetpictureinpicture_component) component to render the output of a camera.
5. Create a Node Dummy and assign the [WidgetPictureInPictureConfigurator](#widgetpictureinpictureconfig_component) component to adjust the position and size of the PiP display at runtime.


## Sensor Components


The following set of components is available in UnigineEditor for configuration.


### SensorManager


Sensor Manager is implemented as the *SensorManager* component. It must be assigned to any node in the world.


### SensorType


Sensor types are defined using the *SensorType* component. This component can be assigned to any nodes in the world; during world initialization, the Sensor Manager automatically discovers and registers them.


For clarity and maintainability, it is recommended to keep all *SensorType* components grouped together in one place rather than scattered throughout the scene.


![](../modules/sensors/sensortype_component.png)


Each sensor type is defined by:


- A unique name
- A base post-material inherited by all sensors of that type, for example:

  - **post_depth** for depth sensors
  - **post_glitch_*** for jamming
  - **post_sensor** for heat sensors


### Sensor


The *Sensor* component automatically creates sensors of a specified type and binds them to a specific Player (sensor target) during world initialization. This component also allows specifying the initial sensor state (enabled or disabled).


> **Warning:** This component must be assigned only to a Player node.


![](../modules/sensors/sensor_component.png)


### IgSensor


The *IgSensor* automatically creates sensors of a specified type and binds them to the specified IG View (View ID) during world initialization. This component also allows specifying the initial sensor state (enabled or disabled).


![](../modules/sensors/igsensor_component.png)


The following UI components are designed for managing sensors and displaying their output in a separate viewport. In the Editor, these components are added like other UI elements—by attaching them to a Dummy node within the UI hierarchy.


### WidgetSensorConfigurator


The *Sensor Configurator* window that displays:


- List of all sensors
- Sensor IDs and types
- Bound targets


It allows enabling and disabling individual sensor bindings at runtime.


![](../modules/sensors/widgetsensorconfigurator_component.png)

*WidgetSensorConfigurator component in Editor*


![](../modules/sensors/sensor_configurator.png)

*Sensor Configurator window at runtime*


### WidgetPictureInPicture


The Picture-in-Picture (PiP) widget (WidgetSprite) that renders the output of a camera (specified via code). The widget exposes parameters for controlling the position and size of the PiP display.


![](../modules/sensors/widgetpictureinpicture_component.png)

*WidgetPictureInPicture component in Editor*


[![](../modules/sensors/pip_widget.jpg)](../modules/sensors/pip_widget.jpg)

*Picture-in-Picture widget at runtime*


### WidgetPictureInPictureConfigurator


A small helper Picture-in-Picture Display window used to adjust the position and size of the PiP display at runtime.


![](../modules/sensors/widgetpictureinpictureconfig_component.png)

*WidgetPictureInPictureConfigurator component in Editor*


![](../modules/sensors/pip_config_window.png)

*Picture-in-Picture configurator window at runtime*


## Framework API


The entire API is exposed through the header `sensors/SensorManager.h`


This API provides direct access to sensor creation, binding, state control, and synchronization.
