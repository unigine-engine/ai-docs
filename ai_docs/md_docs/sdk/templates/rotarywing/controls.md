# Rotary-Wing Template - Controls


The **Input** framework implemented in the template provides a flexible and extensible system for handling user input across different devices. It is designed to support complex interaction logic, configurable bindings, and context-dependent input behavior.


At its core, the framework is built around three main concepts: **[Actions](#actions), [Bindings](#bindings)**, and **[Contexts](#contexts)**.


## Actions


An action is an abstract, device-independent representation of user intent. It defines **what input the application reacts to**.


An action can represent:


- A discrete event (button/key: Down, Pressed, Up)
- A continuous value (axis: float value)


## Bindings


A binding defines **how an action receives its value from a physical or logical input source**. Each action may have multiple bindings.


Bindings may reference:


- Keyboard keys
- Mouse buttons or axes
- Gamepad buttons, axes, or POVs
- Emulated (fake) axes created from button pairs


## Contexts


A context groups actions and defines when they are active. Contexts help segregate input logic and prevent conflicts between different modes of interaction.


Typical examples include:


- Gameplay
- UI / Menu
- Vehicle control
- Free camera


By default, one default context is available; additional contexts can be created as needed.


## Input Configurator


To simplify input setup and management, the template runtime provides the **Input Configurator** window.


![Switching modes](../modules/controls/img/switch_mode.gif)


It offers two working modes:


- Action Display If the device is not connected or the button or axis index is invalid for the connected device, all its bindings are marked as *Unknown* with the button or axis index.

  - Displays all available actions
  - Shows which keys, buttons, or axes are currently bound to each action
- Setup Mode

  - [Create and manage contexts](#create_context)
  - [Create new actions](#create_action)
  - [Bind](#add_binding) keys, buttons, and axes to actions
  - [Configure axis parameters](#axis_bindings) such as sensitivity and dead zone
  - Use automatic input detection


### Creating and Configuring Inputs (Setup Mode)


**Creating a Context**


1. Click ![Plus button](../modules/controls/img/plus_button.jpg) next to the *Context* dropdown, type in the new context name, and click *Add*.
2. Select the newly created context in the *Context* dropdown to configure its actions.


**Creating an Action**


1. Click ![Plus button](../modules/controls/img/plus_button.jpg) in the Action area.
2. Specify the Action name.
3. Select the Action type (Key or Axis).


**Adding Bindings**


Each action provides a ![Plus button](../modules/controls/img/plus_button.jpg) button for every supported input device type.


1. Click the corresponding ![Plus button](../modules/controls/img/plus_button.jpg) button.
2. Select binding settings.
3. Click *Detect*.
4. Press the desired key, button, move the axis, or POV to assign it. (Currently only one button can be bound).


## Saving and Loading Configurations


Input configurations can be saved to and loaded from an **XML file**, allowing:


- Reuse across projects
- Easy customization by users
- Version-controlled input presets


### Action Settings


The action can be referred to by its name or ID.


Action name shall be unique within the context.


### Binding Settings


The following settings are available for the binding depending on its type.


#### Axis Bindings


| Setting | Description |
|---|---|
| axis | Index of the physical input axis. |
| axis_clamp | Defines how axis values are remapped: - **FULL** � full range as-is - **POSITIVE_RANGE** � only positive values, negative values return 0 - **NEGATIVE_RANGE** � only negative values, positive values return 0 - **FULL_TO_POSITIVE** � remaps [-1, 1] -> [0, 1] - **FULL_TO_NEGATIVE** � remaps [-1, 1] -> [-1, 0] |
| axis_inverse | Inverts the axis direction. |
| dead_zone | Defines a neutral zone around zero where axis input is ignored. |
| use_fake_axis | Uses two buttons instead of a physical axis to emulate axis input. |
| use_pov | Uses POV (hat switch) input instead of buttons. |
| positive_key | Button index or POV direction that increases the axis value. |
| negative_key | Button index or POV direction that decreases the axis value. |
| positive_pov | POV index for the positive direction (when using POV input). |
| negative_pov | POV index for the negative direction (when using POV input). |
| sensitivity | Speed at which the axis value changes when input is applied. |
| gravity | Speed at which the axis value returns to zero when input stops. |


#### Key Bindings


| Setting | Description |
|---|---|
| key | Button index or POV direction that triggers the action. |
| use_axis | Treats an axis as a button input. |
| axis | Index of the axis used when *use_axis* is enabled. |
| axis_inverse | Inverts the axis value before evaluation. |
| threshold | Axis value at which the key action is considered pressed. |
| use_pov | Use of POV input instead of a button. |
| pov | Index of the POV used for the key input. |


### Workflow


New actions may be added in either of the following ways.


**Via code:**


1. Create new context in code: ```cpp Context *context = InputManager::get()->createContext("myContext"); ``` Or use the default one: ```cpp Context *context = InputManager::get()->getDefaultContext(); ```
2. Create an action: ```cpp input.restart = context->addKeyAction("Restart"); ```
3. Create and configure the binding: ```cpp { KeySettings settings; settings.key = Input::KEY_R; input.restart->addBinding(InputModule::DEVICE_TYPE::KEYBOARD, settings); } ``` An action may have an unlimited number of bindings. For example: ```cpp input.gear = context->addKeyAction("Gear"); { KeySettings settings; settings.key = Input::KEY_G; input.gear->addBinding(InputModule::DEVICE_TYPE::KEYBOARD, settings); } { KeySettings settings; settings.key = 11; input.gear->addBinding(InputModule::DEVICE_TYPE::JOYSTICK, settings); } ```
4. Use the action in the project logic: ```cpp if (input.restart->isDown()) start(); ```


All configured actions may be saved to an xml:


```cpp
InputManager::get()->saveSettings("mysettings.input");

```


And loaded in another project:


```cpp
InputManager::get()->loadSettings("mysettings.input");

```


The runtime **Input Configurator** may simplify this process:


1. Create a new context, new actions, and bindings via the Input Configurator and save the created configuration by clicking the Save button.
2. Load the created input settings in code: ```cpp InputManager::get()->loadSettings("mysettings.input"); Context *context = InputManager::get()->getDefaultContext(); //and create a variable for the action input.restart = context->getKeyAction("Restart"); ```
3. Use the action in the project logic: ```cpp if (input.restart->isDown()) start(); ```


## Profile Configurator


**Profile Configurator** lets you manage input profiles for different devices when you need to add support for multiple specific controller models.


This is especially useful in professional simulation setups where standard configuration through the *Input Configurator* may not be sufficient, requiring users to re-bind controllers for each device when switching between them. Three profile types are available:


- **Default** - base profiles per device type (keyboard, mouse, gamepad, joystick)
- **Preset** - predefined profiles for specific device models
- **Custom** - user-defined profiles with modified settings.


To create or modify a profile, switch to *Setup* mode and define the required controls.


![](../modules/controls/img/profile_mode.png)


On application startup, profiles are resolved in the following priority order: *Custom > Preset > Default*. The first matching profile is applied and its mappings are loaded into the *Input Configurator*.


![](../modules/controls/img/profile.png)
