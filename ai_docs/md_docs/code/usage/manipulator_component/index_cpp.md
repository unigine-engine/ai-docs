# Using Manipulators to Transform Objects (CPP)


After adding an object to the scene in Unigine Editor, you can control object transformations with control devices. But sometimes transformations are supposed to be made at application runtime. For example, when you create your own game with a world editor, where you can place objects in the world and move them around.


This usage example will teach you how to:


1. Select an object on the screen with the mouse using [Intersections](../../../code/usage/intersections/index_cpp.md).
2. Use manipulator widgets to modify the object transform matrix.
3. Switch between different manipulator widgets using the keyboard.


![](widget_showcase.gif)


### See Also


- Article on [Matrix Transformations](../../../code/fundamentals/matrix_transformations/index_cpp.md)
- Article on [Intersections](../../../code/usage/intersections/index_cpp.md)


## Creating Manipulators to Control Object Transformations


There are 3 types of manipulator widgets used for object transforming:


- *[Widget Manipulator Translator](../../../api/library/gui/class.widgetmanipulatortranslator_cpp.md)* creates a mover manipulator used to translate objects along three axes with arrows at the end.
- *[Widget Manipulator Rotator](../../../api/library/gui/class.widgetmanipulatorrotator_cpp.md)* creates a rotation manipulator used to rotate objects around three axes in the form of a sphere.
- *[Widget Manipulator Scaler](../../../api/library/gui/class.widgetmanipulatorscaler_cpp.md)* creates a scaling manipulator used to scale objects along three axes in the form of a triangle.


All these manipulators work the same way, each of them visually represents a part of the transformation matrix that you can change by dragging the control elements of the widget. Use the *CHANGED* callback of the widget to make the selected object follow manipulators transformations.


```cpp
// method used to apply transformation according to users actions
void AppSystemLogic::ApplyTransform()
{
	if (obj && Input::isMouseButtonPressed(Input::MOUSE_BUTTON::MOUSE_BUTTON_LEFT))
		obj->setWorldTransform(CurrentObjectManipulator->getTransform());
}


```


## Selecting Objects Using Mouse Cursor


To select an object under the mouse cursor we should cast a ray from the cursor location in the view direction of the camera using the *[World::getIntersection()](../../../api/library/engine/class.world_cpp.md#getIntersection_Vec3_Vec3_int_WorldIntersection_Object)* method, that will return an intersected object (if any):


```cpp
// method used to find an object
ObjectPtr AppSystemLogic::GetNodeUnderCursor()
{
	auto player = Game::getPlayer();
	WorldIntersectionPtr intersection;

	// take into account main window position to obtain correct direction
	EngineWindowPtr main_window = WindowManager::getMainWindow();

	if (!main_window)
		return nullptr;

	// find mouse position on the screen
	Math::ivec2 mouse = Input::getMousePosition();
	Math::ivec2 main_pos = main_window->getPosition();
	mouse.x -= main_pos.x;
	mouse.y -= main_pos.y;

	const Math::ivec2 window_size = main_window->getClientSize();

	Math::Vec3 p0;
	Math::Vec3 p1;
	player->getDirectionFromScreen(p0, p1, mouse.x, mouse.y, 0, 0, window_size.x, window_size.y);

	// return an object intersected by the ray cast from the cursor position in the direction of the camera
	return World::getIntersection(p0, p1, 1, intersection);
}


```


## Putting it All Together


Now let's put it all together and add a keyboard handler to switch the current manipulator. For example, let's use **Z, X, C** keys to select *Translator, Rotator, Scaler* Manipulators accordingly. The selected widget will be displayed on the screen where the object is located (i.e. it will have the same transformation).


1. Create a [new C++ project](../../../code/cpp/application.md).
2. Copy the code below and paste it to the corresponding source files in your project.


<details>
<summary>AppSystemLogic.h | close</summary>

```cpp
#ifndef __APP_SYSTEM_LOGIC_H__
#define __APP_SYSTEM_LOGIC_H__

#include <UnigineLogic.h>
#include <UnigineWidgets.h>
#include <UniginePlayers.h>

class AppSystemLogic : public Unigine::SystemLogic
{
public:
	AppSystemLogic();
	virtual ~AppSystemLogic();

	int init() override;

	int update() override;
	int postUpdate() override;

	int shutdown() override;

	// define auxiliary methods used for the project
	void ApplyTransform();
	Unigine::ObjectPtr GetNodeUnderCursor();
	void SwitchManipulator(Unigine::WidgetManipulatorPtr CurrentManipulator);

private:
	// define a pointer to access object parameters
	Unigine::ObjectPtr obj;

	// define a pointer to access UI
	Unigine::GuiPtr gui;

	// define a pointer to store transformation matrix of an active widget
	Unigine::WidgetManipulatorPtr CurrentObjectManipulator;

	// define pointers to display transformation matrix for each type of transform
	Unigine::WidgetManipulatorTranslatorPtr ManObjTranslator;
	Unigine::WidgetManipulatorRotatorPtr ManObjRotator;
	Unigine::WidgetManipulatorScalerPtr ManObjScaler;
};

#endif // __APP_SYSTEM_LOGIC_H__

```

</details>


<details>
<summary>AppSystemLogic.cpp | close</summary>

```cpp
#include "AppSystemLogic.h"
#include <UnigineWidgets.h>
#include <UnigineGame.h>
#include <UnigineWorld.h>
#include <UniginePlayers.h>
#include <UnigineMathLib.h>

using namespace Unigine;

// System logic, it exists during the application life cycle.
// These methods are called right after corresponding system script's (UnigineScript) methods.
// method used to apply transformation according to users actions
void AppSystemLogic::ApplyTransform()
{
	if (obj && Input::isMouseButtonPressed(Input::MOUSE_BUTTON::MOUSE_BUTTON_LEFT))
		obj->setWorldTransform(CurrentObjectManipulator->getTransform());
}
// method used to find an object
ObjectPtr AppSystemLogic::GetNodeUnderCursor()
{
	auto player = Game::getPlayer();
	WorldIntersectionPtr intersection;

	// take into account main window position to obtain correct direction
	EngineWindowPtr main_window = WindowManager::getMainWindow();

	if (!main_window)
		return nullptr;

	// find mouse position on the screen
	Math::ivec2 mouse = Input::getMousePosition();
	Math::ivec2 main_pos = main_window->getPosition();
	mouse.x -= main_pos.x;
	mouse.y -= main_pos.y;

	const Math::ivec2 window_size = main_window->getClientSize();

	Math::Vec3 p0;
	Math::Vec3 p1;
	player->getDirectionFromScreen(p0, p1, mouse.x, mouse.y, 0, 0, window_size.x, window_size.y);

	// return an object intersected by the ray cast from the cursor position in the direction of the camera
	return World::getIntersection(p0, p1, 1, intersection);
}
// method used to switch manipulators
void AppSystemLogic::SwitchManipulator(WidgetManipulatorPtr CurrentManipulator)
{
	// move to selected object and display chosen manipulator
	CurrentManipulator->setTransform(obj->getWorldTransform());
	CurrentManipulator->setHidden(false);

	// hide other widget manipulators
	CurrentObjectManipulator = CurrentManipulator;
	if (ManObjTranslator != CurrentObjectManipulator)
		ManObjTranslator->setHidden(true);
	if (ManObjRotator != CurrentObjectManipulator)
		ManObjRotator->setHidden(true);
	if (ManObjScaler != CurrentObjectManipulator)
		ManObjScaler->setHidden(true);
}

AppSystemLogic::AppSystemLogic()
{
}

AppSystemLogic::~AppSystemLogic()
{
}

int AppSystemLogic::init()
{
	// create widget manipulators
	gui = Gui::getCurrent();
	ManObjTranslator = WidgetManipulatorTranslator::create(gui);
	ManObjRotator = WidgetManipulatorRotator::create(gui);
	ManObjScaler = WidgetManipulatorScaler::create(gui);

	// add widgets to the UI
	gui->addChild(ManObjTranslator);
	gui->addChild(ManObjRotator);
	gui->addChild(ManObjScaler);

	// hide manipulators, so that they wouldn't appear after application initialization
	ManObjTranslator->setHidden(true);
	ManObjRotator->setHidden(true);
	ManObjScaler->setHidden(true);
	CurrentObjectManipulator = ManObjTranslator;
	// subscribe each widget manipulator for the Changed event
	ManObjTranslator->getEventChanged().connect(this, &AppSystemLogic::ApplyTransform);
	ManObjRotator->getEventChanged().connect(this, &AppSystemLogic::ApplyTransform);
	ManObjScaler->getEventChanged().connect(this, &AppSystemLogic::ApplyTransform);

	return 1;
}

////////////////////////////////////////////////////////////////////////////////
// start of the main loop
////////////////////////////////////////////////////////////////////////////////

int AppSystemLogic::update()
{
	// set projection and viewmodel for the each widget every frame
	auto player = Game::getPlayer();
	if (player)
	{
		ManObjTranslator->setProjection(player->getProjection());
		ManObjRotator->setProjection(player->getProjection());
		ManObjScaler->setProjection(player->getProjection());
		ManObjTranslator->setModelview(player->getCamera()->getModelview());
		ManObjRotator->setModelview(player->getCamera()->getModelview());
		ManObjScaler->setModelview(player->getCamera()->getModelview());
	}

	// find object with a right-click
	if (Input::isMouseButtonDown(Input::MOUSE_BUTTON::MOUSE_BUTTON_RIGHT))
	{
		obj = GetNodeUnderCursor();
		CurrentObjectManipulator->setTransform(obj->getWorldTransform());
	}
	// switch widgets on command with Z,X,C keys
	if (obj)
	{
		if (!Input::isMouseButtonPressed(Input::MOUSE_BUTTON::MOUSE_BUTTON_LEFT))
			CurrentObjectManipulator->setTransform(obj->getWorldTransform());
		if (Input::isKeyDown(Input::KEY::KEY_Z))
			SwitchManipulator(ManObjTranslator);
		if (Input::isKeyDown(Input::KEY::KEY_X))
			SwitchManipulator(ManObjRotator);
		if (Input::isKeyDown(Input::KEY::KEY_C))
			SwitchManipulator(ManObjScaler);
	}

	return 1;
}

int AppSystemLogic::postUpdate()
{
	// Write here code to be called after updating each render frame.
	return 1;
}

////////////////////////////////////////////////////////////////////////////////
// end of the main loop
////////////////////////////////////////////////////////////////////////////////

int AppSystemLogic::shutdown()
{
	// Write here code to be called on engine shutdown.
	return 1;
}

```

</details>
