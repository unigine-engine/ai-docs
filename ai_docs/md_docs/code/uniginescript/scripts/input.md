# Input System

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


## Introduction


One of the features the Unigine engine provides is a High-Level Input API. It allows to work with the variety of input devices (such as keyboard, mouse, joystick, gamepad etc.) in the same way, utilizing their capabilities simultaneously. For the sake of usability all input devices recognized by the engine have a common interface. The controls of the input devices can be assigned to definite user's actions in the virtual world. According to the application needs the editing of the controls using GUI can be enabled.


The Input scripts are located in `data/scripts/input` directory of the UNIGINE SDK.


## Entities


### Input device


**Input device** is a peripheral hardware equipment providing data and control signals to the processing unit. It is one of the key resources for the interactive virtual reality systems. Each input device regardless of its type has an ID and is characterized by the number and states of its axes and buttons.


### Input


**Input** represents the input data provided to the engine.


#### Button


**Button** of the input device gives only off/on digital signal, indicating two discrete values: �0� and �1�. The user's application reacts accordingly.


#### Axis


**Axis** of the input device is an analogue signal data corresponding to the angle of displacement. It has three basic positions: minimum, neutral, and maximum. For Unigine engine it is recommended that they belong to the interval between -1.0 and 1.0, with 0 as a neutral value.


According to the characteristics of the axes they can be divided into 4 calibration types:


1. Increasing axis - with the range from 0.0 to 1.0;
2. Decreasing axis - with the range from 0.0 to -1.0;
3. Positive axis with the range from -1.0 to 1.0;
4. Negative axis with the range from 1.0 to -1.0.


#### Virtual axis


**Virtual axis** allows to emulate analogue signal using digital input device. It is used to implement smooth value changing, similar to a steering wheel rotation, for example. If a button with the virtual axis assigned is pressed continuously or repeatedly, virtual axis value will be incremented to 1.0 with the specified changing speed. When the button is no longer pressed, the axis value will be decremented to 0 with the returning speed.


### Action


The user can perform a number of actions in the virtual world, such as moving in different directions, jumping, or shooting. The actions can be activated in many ways: by pressing a button or rotating an analogue stick of the gamepad. The Unigine engine makes it possible to assign multiple Inputs for each of the action. The names of the actions and input axes assigned to them can be saved in the configuration file.


## Configuration file syntax


The syntax of the configuration stored in the XML file is the following:


```xml
<controls definition="controls_def.xml">
	<action name="accelerate">
		<input device="Logitech Racing Wheel" state="3" min="1" max="-1"/>
		<input device="Keyboard" state="119"/>
	</action>
	<action name="brake">
		<input device="Logitech Racing Wheel" state="2" min="1" max="-1"/>
		<input device="Keyboard" state="115"/>
	</action>
</controls>

```


**Сontrols tag** is used to describe control action map. Action tags are included into this tag. *Сontrols tag* has the following attribute:


- *Definition* � definition file name, where action attributes are defined.


**Action tag** describes action configuration, identified by its name (name attribute required). Action tag can contain Input tags.


**Input tag** contains input configuration. It has the following attributes:


- *Device* is a required attribute. It specifies input device name and is used to identify input device. Specifying *keyboard* and *mouse* as input devices is sufficient for all types of keyboards and mice.
- *State* is a required attribute. It specifies input device state number and is used to map input to a particular input device axis or button. > **Notice:** Direct names of the buttons can't be used, as each input device has its own states and state names. They also depend on the installed driver. Taking these facts into consideration, the names are not universal. >  However, controls can be edited [using GUI interface](#gui_edit5). In this case, there is no need to specify the exact state number and it is possible to see input state names.
- *Min* is an optional attribute. It specifies the minimum input device axis value.
- *Max* is an optional attribute. It specifies the maximum input device axis value.
- *Neutral* specifies the neutral value, when input is inactive. The default is 0.
- *Threshold* specifies the threshold for input device response in decimal units. The default value is 0.2.
- *Change_speed* is an optional attribute. It specifies the axis changing speed.
- *Return_speed* is an optional attribute. It specifies the axis returning speed.


## How to Use


### Step 1. Include the required input devices headers


```cpp
#include <scripts/input/input_device.h>
#include <scripts/input/control.h>

```


### Step 2. Add initialization, update and shutdown handlers to corresponding code sections


```cpp
int init() {
	Unigine::Input::init();

	/*...*/

	return 1;
}

int update() {
	Unigine::Input::update();

	/*...*/

	return 1;
}

int shutdown() {
	Unigine::Input::shutdown();

	/*...*/

	return 1;
}

```


### Step 3. Create controls config files


Create 2 configuration files: **controls_def.xml** and **controls.xml**.


**Controls_def** file defines the action attributes:


```xml
<?xml version="1.0" encoding="utf-8"?>
<controls_def>
	<action_def name="accelerate" min="0" max="1" neutral="0" type="state"/>
</controls_def>

```


*Action tag* has the following attributes:


- *Name* � action name.
- *Min* � minimum axis value for application accepted input.
- *Max* � maximum axis value for application accepted input.
- *Neutral* � neutral axis value for application accepted input.
- *Type* � action type:

  - *State* specifies the action having effect until the corresponding input is pressed. In other words, state action is used when it is necessary to change something continuously according to key / axis state. An example is car steering. > **Notice:** In the case of a *state* action, *getState()* returns the current input state (corrected according to the input range and action range).
  - *Switch* is used when it is necessary to toggle something on and off. It allows to handle key up and key down events (just one at a time). An example is turning car head lights on and off. > **Notice:** In the case of a *switch* action, the current state is irrelevant, but rather the difference between the current and the previous state matters. > > > - When the key is pressed down, *getState()* returns the maximum value. > - When the key is up, *getState()* returns **-1** * maximum value. > - If the key did not change its state since the previous update, the function will return the minimum value.


**Controls** file binds input with actions:


```xml
<?xml version="1.0" encoding="utf-8"?>
<controls definition="/config/controls/controls_def.xml">
	<action name="accelerate"/>
	<action name="brake"/>
	<!-- etc. -->
</controls>

```


> **Notice:** Don't forget to specify input devices for the actions.


### Step 4. Adding and integrating controls


To load control configuration use:


```cpp
// somewhere in initialization code

// creating control and loading config files
Unigine::Input::Control control = new Unigine::Input::Control();
control.loadFromFile("you_config_file.xml");

```


To check control states use:


```cpp
// somewhere in the update() code

// updating controls
control.update(engine.game.getIFps())

// getting current actions' states and passing them to the controlled object
Unigine::Input::Action action = control.getAction("accelerate");
current_car.setAccelerator(action.getState());
action = control.getActionByName("brake");
current_car.setBrake(action.getState());
// etc.

```


> **Notice:** It is necessary to call the function *void Unigine::Input::Control::update(float ifps)* every *update()* so that all the actions are detected.


### Editing the controls using GUI interface


To enable this function do the following:


#### Step 1. Include headers


```cpp
#include <scripts/input/control_setup_window.h>
```


#### Step 2. Add initialization, update and shutdown handlers for ControlSetupWindow to corresponding code sections


```cpp
int init() {
	Unigine::Input::ControlSetupWindow::init(engine.getGui());

	/*...*/

	return 1;
}

int update() {
	Unigine::Input::ControlSetupWindow::update();

	/*...*/

	return 1;
}

int shutdown() {
	Unigine::Input::ControlSetupWindow::shutdown();

	/*...*/

	return 1;
}


```


#### Step 3. Showing configuration window


```cpp
void controller_setup_button_clicked() {
	if(controller_setup_button.isToggled()) {
		// show window
		Unigine::Input::ControlSetupWindow::addOnHideCallback("TestCarGui::on_save_car_controls",NULL);
		Unigine::Input::ControlSetupWindow::show(control); // see control definition above
	} else {
		// hide window
		Unigine::Input::ControlSetupWindow::hide();
	}
}

```


## Example


To illustrate the whole process let's create a simple application that allows you to control movement of a node in the world using the keyboard (**W, A, S, D** keys by default) as well as changing keyboard configuration via the GUI interface (*Control Setup* window). We are going to create a new *Pawn* class implementing response to control states and actually moving a node it is bound to.


We are going to use the following controls definition and binding files:


`controls_def.xml` file


```xml
<?xml version="1.0" encoding="utf-8"?>
<controls_def>
  <action_def name="forward" min="0" max="1" neutral="0" type="state"/>
  <action_def name="backward" min="0" max="1" neutral="0" type="state"/>
  <action_def name="left" min="0" max="1" neutral="0" type="state"/>
  <action_def name="right" min="0" max="1" neutral="0" type="state"/>
</controls_def>

```


`controls.xml` file


```xml
<?xml version="1.0" encoding="utf-8"?>
<controls definition="controls_def.xml">
	<action name="forward">
		<input device="Keyboard" state="119"/>
	</action>
	<action name="backward">
		<input device="Keyboard" state="115"/>
	</action>
	<action name="left">
		<input device="Keyboard" state="97"/>
	</action>
	<action name="right">
		<input device="Keyboard" state="100"/>
	</action>
</controls>

```


Just copy the code below and paste it to a world script file of a new project.


<details>
<summary>world.usc | Close</summary>

**world.usc**


```cpp
#include <core/unigine.h>

// including all necessary files
#include <scripts/input/input_device.h>
#include <scripts/input/control.h>
#include <scripts/input/control_setup_window.h>

// declaring a control
Unigine::Input::Control control;

// UI
Gui gui;
WidgetButton button;

/// Pawn class definition
class Pawn
{
	// movement states
	int forward = 0;
	int backward = 0;
	int left = 0;
	int right = 0;

	// node to be controlled
	Node pawn_node;

	// Pawn constructor
	Pawn(Node n)
	{
		pawn_node = n;
	}

	// updated controlled node's position depending on the current control states
	int  update(float ifps)
	{
		Vec3 delta_movement = Vec3(0.0f, 0.0f, 0.0f);
		if(forward)
		{
			delta_movement = Vec3(0.0f, 1.0f, 0.0f);
		}
		else if (backward)
		{
			delta_movement = Vec3(0.0f, -1.0f, 0.0f);
		}
				else if (left)
		{
			delta_movement = Vec3(-1.0f, 0.0f, 0.0f);
		}
		else if (right)
		{
			delta_movement = Vec3(1.0f, 0.0f, 0.0f);
		}

		pawn_node.setWorldPosition(pawn_node.getWorldPosition() + delta_movement*ifps);
		return 1;
	}

	// setting forward state
	void setForward(int f){	forward = f; }

	// setting backward state
	void setBackward(int b)	{ backward = b;	}

	// setting left state
	void setLeft(int l)	{ left = l; }

	// setting right state
	void setRight(int r) { right = r; }
};

/// click event handler for the button
void button_clicked() {
	if(button.isToggled()) {
		// show window
		Unigine::Input::ControlSetupWindow::addOnHideCallback("hide_window",NULL);
		Unigine::Input::ControlSetupWindow::show(control); // see control definition above
	} else {
		// hide window
		Unigine::Input::ControlSetupWindow::hide();
	}
}

/// hide event handler for the Controls Setup window
void hide_window() {
	button.setToggled(0);
}

Pawn pawn;

int init() {

	// creating and initializing a player
	Player player = new PlayerSpectator();
	player.setPosition(Vec3(0.0f,-3.401f,1.5f));
	player.setDirection(Vec3(0.0f,1.0f,-0.4f));

	// disabling standard keybord control for player and setting it as a game player
	player.setControlled(0);
	engine.game.setPlayer(player);

	// preparing UI (adding a button to toggle the Controls Setup window)
	gui = engine.getGui();
	button = new WidgetButton(gui, "Controls Setup");
	button.setPosition(10, 40);
	button.setToggleable(1);
	button.setCallback(GUI_CLICKED, "button_clicked");
	gui.addChild(button, GUI_ALIGN_OVERLAP | GUI_ALIGN_TOP | GUI_ALIGN_LEFT);


	// initializing the input system
	Unigine::Input::init();

	// creating and loading controls from the controls.xml file
	control = new Unigine::Input::Control();
	control.loadFromFile("controls.xml");

	// initializing the control setup window with desired number of alternatives
	Unigine::Input::ControlSetupWindow::init(engine.getGui(),1);

	// creating a new pawn and binding it to the player
	pawn = new Pawn(node_cast(player));

	return 1;
}

// start of the main loop
int update() {

	// updating the input system
	Unigine::Input::update();
	float ifps = engine.game.getIFps();

	// updating controls
	control.update(ifps);

	// getting current actions' states and passing them to our pawn object
	Unigine::Input::Action action = control.getAction("forward");
	pawn.setForward(action.getState());
	action = control.getAction("backward");
	pawn.setBackward(action.getState());
	action = control.getAction("left");
	pawn.setLeft(action.getState());
	action = control.getAction("right");
	pawn.setRight(action.getState());

	// calling pawn's update
	pawn.update(ifps);

	// updating the control setup window
	Unigine::Input::ControlSetupWindow::update();

	return 1;
}

int postUpdate() {

	return 1;
}

int updatePhysics() {

	return 1;
}
// end of the main loop

int shutdown() {

	// shutting down the input system and control setup window
	Unigine::Input::shutdown();
	Unigine::Input::ControlSetupWindow::shutdown();

	// removing all widgets grom GUI
	for (int i = 0; i < gui.getNumChildren(); i++)
		gui.removeChild(gui.getChild(i));

	return 1;
}

```

</details>
