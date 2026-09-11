# Using Manipulators to Transform Objects (CS)


After adding an object to the scene in Unigine Editor, you can control object transformations with control devices. But sometimes transformations are supposed to be made at application runtime. For example, when you create your own game with a world editor, where you can place objects in the world and move them around.


This usage example will teach you how to:


1. Select an object on the screen with the mouse using [Intersections](../../../code/usage/intersections/index_cs.md).
2. Use manipulator widgets to modify the object transform matrix.
3. Switch between different manipulator widgets using the keyboard.


![](widget_showcase.gif)


### See Also


- Article on [Matrix Transformations](../../../code/fundamentals/matrix_transformations/index_cs.md)
- Article on [Intersections](../../../code/usage/intersections/index_cs.md)


## Creating Manipulators to Control Object Transformations


There are 3 types of manipulator widgets used for object transforming:


- *[Widget Manipulator Translator](../../../api/library/gui/class.widgetmanipulatortranslator_cs.md)* creates a mover manipulator used to translate objects along three axes with arrows at the end.
- *[Widget Manipulator Rotator](../../../api/library/gui/class.widgetmanipulatorrotator_cs.md)* creates a rotation manipulator used to rotate objects around three axes in the form of a sphere.
- *[Widget Manipulator Scaler](../../../api/library/gui/class.widgetmanipulatorscaler_cs.md)* creates a scaling manipulator used to scale objects along three axes in the form of a triangle.


All these manipulators work the same way, each of them visually represents a part of the transformation matrix that you can change by dragging the control elements of the widget. Use the *CHANGED* callback of the widget to make the selected object follow manipulators transformations.


```csharp
// transform an object
private void ApplyTransform()
{
	if(obj && Input.IsMouseButtonPressed(Input.MOUSE_BUTTON.LEFT))
		obj.WorldTransform = CurrentObjectManipulator.Transform;
}


```


## Selecting Objects Using Mouse Cursor


To select an object under the mouse cursor we should cast a ray from the cursor location in the view direction of the camera using the *[World.GetIntersection()](../../../api/library/engine/class.world_cs.md#getIntersection_Vec3_Vec3_int_WorldIntersection_Object)* method, that returns an intersected object (if any).


```csharp
// find an object under the cursor
private Unigine.Node GetNodeUnderCursor()
{
	//get mouse position relative to the main window
	ivec2 mouse = Input.MousePosition;

	// find mouse position on the screen
	EngineWindow main_window = WindowManager.MainWindow;
	if (!main_window)
		return null;

	ivec2 main_pos = main_window.Position;
	mouse.x -= main_pos.x;
	mouse.y -= main_pos.y;
	ivec2 window_size = main_window.ClientSize;

	Vec3 p0;
	Vec3 p1;
	Game.Player.GetDirectionFromScreen(out p0, out p1, mouse.x, mouse.y, 0, 0, window_size.x, window_size.y);

	// return an object intersected by the ray cast from the cursor position in the direction of the camera
	return World.GetIntersection(p0, p1, 1, intersection);
}


```


## Putting it All Together


Now let's put it all together and add a keyboard handler to switch the current manipulator. For example, let's use **Z, X, C** keys to select *Translator, Rotator, Scaler* Manipulators accordingly. The selected widget will be displayed on the screen where the object is located (i.e. it will have the same transformation).


1. Create a new [C# component](../../../principles/component_system/component_system_cs/index.md) � *Manipulator*. Double-click it in the Asset Browser to edit code in your IDE.
2. Copy the code below and paste it to your component.
3. Assign *Manipulator* to any enabled node in the world and click *Play*.


<details>
<summary>Manipulator.cs | close</summary>

```csharp
#region Math Variables
#if UNIGINE_DOUBLE
using Scalar = System.Double;
using Vec2 = Unigine.dvec2;
using Vec3 = Unigine.dvec3;
using Vec4 = Unigine.dvec4;
using Mat4 = Unigine.dmat4;
#else
using Scalar = System.Single;
using Vec2 = Unigine.vec2;
using Vec3 = Unigine.vec3;
using Vec4 = Unigine.vec4;
using Mat4 = Unigine.mat4;
using WorldBoundBox = Unigine.BoundBox;
using WorldBoundSphere = Unigine.BoundSphere;
using WorldBoundFrustum = Unigine.BoundFrustum;
#endif
#endregion

using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class Manipulator : Component
{
	// WorldIntersection object to store the information about the intersection
	WorldIntersection intersection = new WorldIntersection();

	// Unigine.Object object to gain access to a selected object's transform in Unigine
	Unigine.Node obj = null;

	// create manipulators for each type of transform(Translating, Scaling, Rotating)
	WidgetManipulator ObjManTranslator;
	WidgetManipulator ObjManScaler;
	WidgetManipulator ObjManRotator;

	// create widget manipulator used to store transformation matrix of an active widget
	WidgetManipulator CurrentObjectManipulator = null;
	Gui gui;

	[Method(Order=2)] private void Init()
	{
		// write here code to be called on component initialization
		gui = Gui.GetCurrent();

		// create widget for each transformation type
		ObjManTranslator = new WidgetManipulatorTranslator(gui);
		ObjManScaler = new WidgetManipulatorScaler(gui);
		ObjManRotator = new WidgetManipulatorRotator(gui);

		// set projection for the widgets
		ObjManTranslator.Projection= Game.Player.Camera.Projection;
		ObjManScaler.Projection = Game.Player.Camera.Projection;
		ObjManRotator.Projection = Game.Player.Camera.Projection;

		// add widgets to UI
		gui.AddChild(ObjManTranslator);
		gui.AddChild(ObjManScaler);
		gui.AddChild(ObjManRotator);

		// subscribing for the "Changed" event
		ObjManTranslator.EventChanged.Connect(ApplyTransform);
		ObjManRotator.EventChanged.Connect(ApplyTransform);
		ObjManScaler.EventChanged.Connect(ApplyTransform);

		// hide created widgets
		ObjManScaler.Hidden = true;
		ObjManRotator.Hidden = true;
		ObjManTranslator.Hidden = true;
	}

	private void Update()
	{
		// write here code to be called before updating each render frame
		 if (!Game.Player)
			return;

		// set modelview for each widget manipulator every frame
		ObjManTranslator.Modelview = Game.Player.Camera.Modelview;
		ObjManScaler.Modelview = Game.Player.Camera.Modelview;
		ObjManRotator.Modelview = Game.Player.Camera.Modelview;

		// select an object with right-click
		if (Input.IsMouseButtonDown(Input.MOUSE_BUTTON.RIGHT))
			obj = GetNodeUnderCursor();

		// choose manipulator with Z,X,C keys
		if(obj)
		{
			if(Input.IsKeyDown(Input.KEY.Z))
				SwitchManipulator(ObjManTranslator);
			if(Input.IsKeyDown(Input.KEY.X))
				SwitchManipulator(ObjManRotator);
			if(Input.IsKeyDown(Input.KEY.C))
				SwitchManipulator(ObjManScaler);
			if (!Input.IsMouseButtonPressed(Input.MOUSE_BUTTON.LEFT) && CurrentObjectManipulator)
				CurrentObjectManipulator.Transform = obj.WorldTransform;
		}
	}
 	// transform an object
	private void ApplyTransform()
	{
		if(obj && Input.IsMouseButtonPressed(Input.MOUSE_BUTTON.LEFT))
			obj.WorldTransform = CurrentObjectManipulator.Transform;
	}
	// find an object under the cursor
	private Unigine.Node GetNodeUnderCursor()
	{
		//get mouse position relative to the main window
		ivec2 mouse = Input.MousePosition;

		// find mouse position on the screen
		EngineWindow main_window = WindowManager.MainWindow;
		if (!main_window)
			return null;

		ivec2 main_pos = main_window.Position;
		mouse.x -= main_pos.x;
		mouse.y -= main_pos.y;
		ivec2 window_size = main_window.ClientSize;

		Vec3 p0;
		Vec3 p1;
		Game.Player.GetDirectionFromScreen(out p0, out p1, mouse.x, mouse.y, 0, 0, window_size.x, window_size.y);

		// return an object intersected by the ray cast from the cursor position in the direction of the camera
		return World.GetIntersection(p0, p1, 1, intersection);
	}
	// relocate chosen manipulator to the position of selected object and make it visible
	void SwitchManipulator(WidgetManipulator CurrentManipulator)
	{
		if (!obj)
			return;
		// relocate a widget and making it visible
		CurrentManipulator.Transform = obj.WorldTransform;
		CurrentManipulator.Hidden = false;

		// make other widgets hidden
		CurrentObjectManipulator = CurrentManipulator;
		if(ObjManTranslator != CurrentManipulator)
			ObjManTranslator.Hidden = true;
		if(ObjManRotator != CurrentManipulator)
			ObjManRotator.Hidden = true;
		if(ObjManScaler != CurrentManipulator)
			ObjManScaler.Hidden = true;
	}
}

```

</details>
