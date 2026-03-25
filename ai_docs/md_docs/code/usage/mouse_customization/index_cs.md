# Customizing Mouse Cursor and Behavior (CS)


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


```csharp
ControlsApp.MouseHandle = Input.MOUSE_HANDLE.SOFT;
//or
ControlsApp.MouseHandle = Input.MOUSE_HANDLE.USER;

```


## Customizing Mouse Cursor


You can change the look of the mouse cursor in your application using any square **RGBA8** image you want. This can be done by simply adding the following lines to your code (e.g. the world's *init()* method):


```csharp
// loading an image for the mouse cursor
Image mouse_cursor = new Image("textures/cursor.png");

// resize the image to make it square
mouse_cursor.Resize(mouse_cursor.Width, mouse_cursor.Width);

// checking if our image is loaded successfully and has the appropriate format
if ((mouse_cursor.IsLoaded) && (mouse_cursor.Format == Image.FORMAT_RGBA8))
{
	// set the image for the OS mouse pointer
	Input.SetMouseCursorCustom(mouse_cursor);

	// show the OS mouse pointer
	Input.MouseCursorSystem = true;
}


```


Here is a sample RGBA8 image (32x32) you can use for your mouse cursor (download it and put it to the `data/textures` folder of your project):


![Sample cursor image](cursor.png)


## Example Code


Below you'll find the code that performs the following:


- Sets a custom icon and title for the application window.
- Sets a custom mouse cursor.
- Switches between the three handling modes on pressing the **ENTER** key.


You can use the following C# component:


<details>
<summary>AppMouseCustomizer.cs | Close</summary>

**AppMouseCustomizer.cs**


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class AppMouseCustomizer : Component
{
	// widgets
	WidgetLabel label1;
	WidgetLabel label2;
	WidgetButton button;

	private void Init()
	{
			// preparing UI: creating a label and a button and adding them to the GUI
			label1 = new WidgetLabel(Gui.GetCurrent());
			label2 = new WidgetLabel(Gui.GetCurrent());
			button = new WidgetButton(Gui.GetCurrent(), "BUTTON");
			label1.SetPosition(10, 20);
			label2.SetPosition(10, 40);
			button.SetPosition(10, 80);
			Gui.GetCurrent().AddChild(label1, Gui.ALIGN_OVERLAP | Gui.ALIGN_TOP | Gui.ALIGN_LEFT);
			Gui.GetCurrent().AddChild(label2, Gui.ALIGN_OVERLAP | Gui.ALIGN_TOP | Gui.ALIGN_LEFT);
			Gui.GetCurrent().AddChild(button, Gui.ALIGN_OVERLAP | Gui.ALIGN_TOP | Gui.ALIGN_LEFT);


			EngineWindow MWindow = WindowManager.MainWindow;
			// setting a custom icon for the application window
			Image icon = new Image("textures/cursor.png");
			if ((icon.IsLoaded) && (icon.Format == Image.FORMAT_RGBA8))
				MWindow.SetIcon(icon);

			// set a custom title for the application window
			MWindow.Title = "Custom Window Title";
			// loading an image for the mouse cursor
			Image mouse_cursor = new Image("textures/cursor.png");

			// resize the image to make it square
			mouse_cursor.Resize(mouse_cursor.Width, mouse_cursor.Width);

			// checking if our image is loaded successfully and has the appropriate format
			if ((mouse_cursor.IsLoaded) && (mouse_cursor.Format == Image.FORMAT_RGBA8))
			{
				// set the image for the OS mouse pointer
				Input.SetMouseCursorCustom(mouse_cursor);

				// show the OS mouse pointer
				Input.MouseCursorSystem = true;
			}
	}

	private void Update()
	{
		// checking for STATE_USE (ENTER key by default) and toggling mouse handling mode
		if (Game.Player.Controls.ClearState(Controls.STATE_USE) == 1)
			switch (ControlsApp.MouseHandle)
			{
				case Input.MOUSE_HANDLE.GRAB:
					// if the mouse is currently grabbed, we disable grabbing and restore GUI interaction
					if (Input.MouseGrab)
					{
						Input.MouseGrab = false;
						Gui.GetCurrent().MouseEnabled = true;
					}
					Input.MouseHandle = Input.MOUSE_HANDLE.SOFT;
					Log.Message($"MOUSE_HANDLE switch from GRAB to SOFT\n");
					break;
				case Input.MOUSE_HANDLE.SOFT:
					Input.MouseHandle = Input.MOUSE_HANDLE.USER;
					Log.Message($"MOUSE_HANDLE switch from SOFT to USER\n");
					break;
				case Input.MOUSE_HANDLE.USER:
					Input.MouseHandle = Input.MOUSE_HANDLE.GRAB;
					Log.Message($"MOUSE_HANDLE switch from USER to GRAB\n");
					break;
				default:
					break;
			}

			// updating info on the current cursor position and mouse handling mode
			label1.Text = $"MOUSE COORDS: ({Input.MousePosition})";
			label2.Text = $"MOUSE MODE: {Input.MouseHandle}";
	}
}

```

</details>
