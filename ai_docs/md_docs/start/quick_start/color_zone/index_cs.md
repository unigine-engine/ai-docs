# Implementing Color Zone (CS)


Now we can implement the zones to throw the objects into. We will make holes in the floor, implement zone visualization, and add a [trigger](../../../objects/worlds/world_trigger/index.md) volume that will destroy objects entering it.


## Step 1. Unpack Node References to Make Holes in the Floor


To make some floor nodes invisible and non-colliding (objects will fall through them), while keeping the character's turning working smoothly, we must unpack some floor node references. The unpacking means breaking the link to the node file on disk and changing its parameters.


1. To create Color Zones select some floor tiles in a group (holding the **Shift** hotkey), right-click and choose *Unpack To Node Content*.
2. Then disable *Collisions* for these nodes but make sure that *Intersection* is enabled, so that the character's turning works correctly.
3. To make them invisible, go to *[Viewport](../../../principles/bit_masking/index.md#viewport)* Mask and click *Clear All*. This way all bits of mask are set to 0 and they will not match the Camera's *Viewport* Mask. ![](holes.png)
4. Disable *Collision* option for the **ground** node. Now, physical objects can fall through the holes and the ground.


## Step 2. Implement Zone Visualization


Let's create a plane with an emission material to represent the Color Zone.


1. Choose *Create->Mesh->Static* and search for `plane.mesh`.
2. Place it in the world via the Viewport.
3. Rename the node to `"color_zone"`.
4. Scale it to the size of the Play Area and position it between the floor and the ground, so it is visible only through the holes.
5. Create a child material for the *plane* surface and call it `color_zone_mat`. In the *States* tab check the *Emission* option. ![](child_material.png) ![](emission.png) *Color Zone Visualization*


## Step 3. Make the Colors Change Over Time


The Color Zone must be easy to spot. Let's create a dynamic material that changes color emission over time using linear interpolation.


1. Create a new *C# component* and call it **ColorChanger**.
2. Edit the *Color Zone* node and add a **ColorChanger** component to it. ![](color_changer.png)
3. The code, that changes the material *[emission](../../../content/materials/library/mesh_base/index.md#option_emission)* color for the Color Zone's material over time, is given below. Open an IDE and write the code. Save your code in an IDE to ensure it's automatic compilation on switching back to UnigineEditor.


<details>
<summary>ColorChanger.cs | Close</summary>

```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class ColorChanger : Component
{
	public float changeSpeed = 1.5f;

	Material color_zone_mat;

	void Init()
	{
		ObjectMeshStatic mesh = node as ObjectMeshStatic;
		// get the color zone's material
		color_zone_mat = mesh.GetMaterial(0);
	}

	void Update()
	{
		if (color_zone_mat != null)
		{
			// calculate the interpolation coefficient for this frame
			float k = (MathLib.Sin(Game.Time * changeSpeed) + 1) / 2.0f;
			//interpolate between two colors with given coefficient and set it to the first surface's material
			color_zone_mat.SetParameterFloat4("emission_color", MathLib.Lerp(new vec4(1.0f, 1.0f, 0.0f, 1.0f), new vec4(0.0f, 1.0f, 1.0f, 1.0f), k));
			//interpolate between two values of emission intensity with given coefficient and set it to the first surface's material
			color_zone_mat.SetParameterFloat("emission_scale", MathLib.Lerp(1.0f, 4.0f, k));
		}
	}
}

```

</details>


## Step 4. Add a World Trigger


To get rid of objects that were thrown in the Kill Zone, let's use a *[World Trigger](../../../objects/worlds/world_trigger/index.md)*. The trigger defines an area into which a physical object will fall and a [callback](../../../code/fundamentals/callbacks/index_cs.md) that fires when an object gets inside.


1. Create a new **World Trigger** by choosing *Create->Logic->World Tigger* and place it in the world.
2. Check the *Touch* option in the *Parameters* window of the *World Trigger* node to make the trigger fire *callbacks* on partial contact with another node. ![](touch.png)
3. Position it beneath the ground, then set its size to cover the whole play area by going to Parameters and clicking *Edit Size* and adjusting the size of the *World Trigger* in the Viewport. ![](trigger.png)
4. Create a new *C# component* and call it **KillZone**. Add the `KillZone` component to the previously created *World Trigger*.
5. Double-click on the *KillZone* in the *Asset Browser* to open an IDE and copy the code below, which adds a **callback** for the trigger that deletes the entered object from the world. Save your code in an IDE to ensure it's automatic compilation on switching back to UnigineEditor. <details> <summary>KillZone.cs | Close</summary> ```csharp using System; using System.Collections; using System.Collections.Generic; using Unigine; public partial class KillZone : Component { // the area into which an object should fall WorldTrigger trigger; void Init() { trigger = node as WorldTrigger; if (trigger != null) trigger.EventEnter.Connect(Enter); // set the handler to be executed when an object enters the area } void Enter(Node target) { target.DeleteLater(); } } ``` </details>
6. Save changes to the world, go to *File->Save World*or press **Ctrl+S** hotkey.
7. To run the project via the **SDK Browser**, click on the ellipsis beneath the *Run* button to open the *Customize Run Options* window. Specify the **debug** binary of the project to run the executable and see the changes made. ![](debug.png) > **Notice:** The debug binaries have a postfix (**d**) in the name of an executable.
