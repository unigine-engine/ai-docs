# Customizing Mouse Cursor and Behavior (CPP)


![Customizing Mouse](mouse_usage.gif)

*Customizing Mouse*


This example shows how to customize the mouse cursor appearance and change default mouse behavior in your application. It will help you to solve the following tasks:


- Changing the default mouse cursor image.
- Toggling mouse cursor's handling modes.
- Customizing your application's icon and title.


## Defining Mouse Behavior


The mouse behavior is defined by assigning any of the following modes:


- **Grab** - the mouse is grabbed when clicked (the cursor disappears and camera movement is controlled by the mouse). This mode is set **by default**.
- **Soft** - the mouse cursor disappears after being idle for a short time period.
- **User** - the mouse is not handled by the system (allows input handling by some custom module).


There are two ways to set the required mouse behavior mode:


- In the Editor, by selecting the corresponding [option](../../../editor2/settings/controls/index.md#mouse_handle) in the Controls Settings
- Via code by adding the corresponding line to the logic ([world](../../../code/fundamentals/execution_sequence/app_logic_system.md#world_script) or [system](../../../code/fundamentals/execution_sequence/app_logic_system.md#system_script) logic, components, expressions, etc.)


```cpp
ControlsApp::setMouseHandle(Input::MOUSE_HANDLE_SOFT);
//or
ControlsApp::setMouseHandle(Input::MOUSE_HANDLE_USER);

```


## Customizing Mouse Cursor


You can change the look of the mouse cursor in your application using any square **RGBA8** image you want. This can be done by simply adding the following lines to your code (e.g. the world's *init()* method):


```cpp
// loading an image for the mouse cursor
ImagePtr mouse_cursor = Image::create("textures/cursor.png");

// resizing the image to make it square
mouse_cursor->resize(mouse_cursor->getWidth(), mouse_cursor->getWidth());
// checking if our image is loaded successfully and has the appropriate format
if (mouse_cursor->isLoaded() && mouse_cursor->getFormat() == Image::FORMAT_RGBA8)
{
	// setting the image for the OS mouse pointer
	Input::setMouseCursorCustom(mouse_cursor);

	// showing the OS mouse pointer
	Input::setMouseCursorSystem(1);
}

// clearing pointer
mouse_cursor.clear();


```


Here is a sample RGBA8 image (32x32) you can use for your mouse cursor (download it and put it to the `data/textures` folder of your project):


![Sample cursor image](cursor.png)


## Example Code


Below you'll find the code that performs the following:


- Sets a custom icon and title for the application window.
- Sets a custom mouse cursor.
- Switches between the three handling modes on pressing the **ENTER** key.


Insert the following code into the `AppWorldLogic.cpp` file.


> **Notice:** Unchanged methods of the *AppWorldLogic* class are not listed here, so leave them as they are.


```cpp
#include "AppWorldLogic.h"
#include "UnigineUserInterface.h"
#include "UnigineGui.h"
#include "UnigineGame.h"

using namespace Unigine;

// auxiliary variables
ControlsPtr controls;
GuiPtr gui;
String handling_mode[3] = { "GRAB", "SOFT", "USER" };

// widgets
WidgetLabelPtr label;
WidgetLabelPtr label2;
WidgetButtonPtr button;

AppWorldLogic::AppWorldLogic()
{
}

AppWorldLogic::~AppWorldLogic()
{
}

int AppWorldLogic::init()
{
	// initializing auxiliary variables
	controls = Game::getPlayer()->getControls();
	gui = Gui::getCurrent();
    EngineWindowPtr MWindow = WindowManager::getMainWindow();
	// setting a custom icon for the application window
	ImagePtr icon = Image::create("textures/cursor.png");
	if (icon->isLoaded() && icon->getFormat() == Image::FORMAT_RGBA8)
		MWindow->setIcon(icon);
	icon.clear();

	// setting a custom title for the application window
	MWindow->setTitle("Custom Window Title");

	// preparing UI: creating 2 labels and a button and adding them to the GUI
	label = WidgetLabel::create(gui);
	label2 = WidgetLabel::create(gui);
	button = WidgetButton::create(gui, "BUTTON");
	label->setPosition(10, 20);
	label2->setPosition(10, 40);
	button->setPosition(10, 80);
	gui->addChild(label, Gui::ALIGN_OVERLAP | Gui::ALIGN_TOP | Gui::ALIGN_LEFT);
	gui->addChild(label2, Gui::ALIGN_OVERLAP | Gui::ALIGN_TOP | Gui::ALIGN_LEFT);
	gui->addChild(button, Gui::ALIGN_OVERLAP | Gui::ALIGN_TOP | Gui::ALIGN_LEFT);

		// loading an image for the mouse cursor
	ImagePtr mouse_cursor = Image::create("textures/cursor.png");

	// resizing the image to make it square
	mouse_cursor->resize(mouse_cursor->getWidth(), mouse_cursor->getWidth());
	// checking if our image is loaded successfully and has the appropriate format
	if (mouse_cursor->isLoaded() && mouse_cursor->getFormat() == Image::FORMAT_RGBA8)
	{
		// setting the image for the OS mouse pointer
		Input::setMouseCursorCustom(mouse_cursor);

		// showing the OS mouse pointer
		Input::setMouseCursorSystem(1);
	}

	// clearing pointer
	mouse_cursor.clear();
		return 1;
}

int AppWorldLogic::update()
{
	// checking for STATE_USE (ENTER key by default) and toggling mouse handling mode
	if (controls->clearState(Controls::STATE_USE) == 1) {
		switch (ControlsApp::getMouseHandle())
		{
		case Input::MOUSE_HANDLE_GRAB:
			// if the mouse is currently grabbed, we disable grabbing and restore GUI interaction
			if (Input::isMouseGrab())
			{
				Input::setMouseGrab(false);
				Gui::getCurrent()->setMouseEnabled(true);
			}
			Input::setMouseHandle(Input::MOUSE_HANDLE_SOFT);
			break;
		case Input::MOUSE_HANDLE_SOFT:
			Input::setMouseHandle(Input::MOUSE_HANDLE_USER);
			break;
		case Input::MOUSE_HANDLE_USER:
			Input::setMouseHandle(Input::MOUSE_HANDLE_GRAB);
			break;
		}
	}

	// updating info on the current cursor position and mouse handling mode
	label->setText(String::format("\n MOUSE COORDS: %d, %d)", Gui::getCurrent()->getMouseX(), Gui::getCurrent()->getMouseY()));
	label2->setText(String::format("\n MOUSE HANDLE: %s", handling_mode[Input::getMouseHandle()].get()));

	return 1;
}

// ...
int AppWorldLogic::postUpdate()
{
	// ...
	return 1;
}

int AppWorldLogic::updatePhysics()
{
	// ...
	return 1;
}

int AppWorldLogic::shutdown()
{
	// ...
	return 1;
}

```
