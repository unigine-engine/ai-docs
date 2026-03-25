# Customizing Mouse Cursor and Behavior (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


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
engine.controls.setMouseHandle(MOUSE_HANDLE_SOFT);
//or
engine.controls.setMouseHandle(MOUSE_HANDLE_USER);

```


## Customizing Mouse Cursor


You can change the look of the mouse cursor in your application using any square **RGBA8** image you want. This can be done by simply adding the following lines to your code (e.g. the world's *init()* method):


```cpp
// loading an image for the mouse cursor
Image mouse_cursor = new Image("textures/cursor.png");

// resizing the image to make it square
mouse_cursor.resize(mouse_cursor.getWidth(), mouse_cursor.getWidth());

// checking if our image is loaded successfully and has the appropriate format
if (mouse_cursor.isLoaded() && mouse_cursor.getFormat() == IMAGE_FORMAT_RGBA8)
{
	// setting the image for the OS mouse pointer
	engine.app.setMouseCursorCustom(mouse_cursor);

	// show the OS mouse pointer
	engine.app.setMouseCursorSystem(1);
}

```


Here is a sample RGBA8 image (32x32) you can use for your mouse cursor (download it and put it to the `data/textures` folder of your project):


![Sample cursor image](cursor.png)


## Example Code


Below you'll find the code that performs the following:


- Sets a custom icon and title for the application window.
- Sets a custom mouse cursor.
- Switches between the three handling modes on pressing the **ENTER** key.


Insert the following code into your world script file.


> **Notice:** Unchanged methods of the *AppWorldLogic* class are not listed here, so leave them as they are.


```cpp
// my_world.usc

// auxiliary variables
Controls controls;
Gui gui;
string handling_mode[3] = ("GRAB", "SOFT", "USER" );

// widgets
WidgetLabel label;
WidgetLabel label2;
WidgetButton button;

int init() {
	/*...*/

		// initializing auxiliary variables
	controls = engine.game.getPlayer().getControls();
	gui = engine.getGui();

	// setting a custom icon for the application window
	Image icon = new Image("textures/cursor.png");
	if (icon.isLoaded() && icon.getFormat() == IMAGE_FORMAT_RGBA8)
		engine.app.setIcon(icon);

	// setting a custom title for the application window
	engine.app.setTitle("Custom Window Title");

	// preparing UI: creating a label and a button and adding them to the GUI
	label = new WidgetLabel(gui);
	label2 = new WidgetLabel(gui);
	button = new WidgetButton(gui, "BUTTON");
	label.setPosition(10, 20);
	label2.setPosition(10, 40);
	button.setPosition(10, 80);
	gui.addChild(label, GUI_ALIGN_OVERLAP | GUI_ALIGN_TOP | GUI_ALIGN_LEFT);
	gui.addChild(label2, GUI_ALIGN_OVERLAP | GUI_ALIGN_TOP | GUI_ALIGN_LEFT);
	gui.addChild(button, GUI_ALIGN_OVERLAP | GUI_ALIGN_TOP | GUI_ALIGN_LEFT);

	// loading an image for the mouse cursor
	Image mouse_cursor = new Image("textures/cursor.png");

	// resize the image to make it square
	mouse_cursor.resize(mouse_cursor.getWidth(), mouse_cursor.getWidth());
	if (mouse_cursor.isLoaded() && mouse_cursor.getFormat() == IMAGE_FORMAT_RGBA8)
	{
		// setting the image for the OS mouse pointer
		engine.app.setMouseCursorCustom(mouse_cursor);

		// show the OS mouse pointer
		engine.app.setMouseCursorSystem(1);
	}

	return 1;
}

/*...*/

int update() {
	/*...*/

	// checking for STATE_USE (ENTER key by default) and toggling mouse handling mode
	if (controls.clearState(CONTROLS_STATE_USE) == 1)
		switch (engine.controls.getMouseHandle())
			{
				case MOUSE_HANDLE_GRAB:
					// if the mouse is currently grabbed, we disable grabbing and restore GUI interaction
					if (engine.app.isMouseGrab())
					{
						engine.app.setMouseGrab(0);
						engine.gui.setMouseEnabled(1);
					}
					engine.controls.setMouseHandle(MOUSE_HANDLE_SOFT);
					log.message("MOUSE_HANDLE switch from GRAB to SOFT\n");
					break;
				case MOUSE_HANDLE_SOFT:
					engine.controls.setMouseHandle(MOUSE_HANDLE_USER);
					log.message("MOUSE_HANDLE switch from SOFT to USER\n");
					break;
				case MOUSE_HANDLE_USER:
					engine.controls.setMouseHandle(MOUSE_HANDLE_GRAB);
					log.message("MOUSE_HANDLE switch from USER to GRAB\n");
					break;
				default:
					break;
			}

	// updating cursor position info
	label.setText(format("\n MOUSE COORDS: %d, %d)", engine.app.getMouseX(), engine.app.getMouseY()));
	label2.setText(format("\n MOUSE HANDLE: %s", handling_mode[engine.controls.getMouseHandle()]));

	return 1;
}

/*...*/


```
