# Basic Object Movements (CS)


After adding an object to UNIGINE, you can control its transformations with your control devices. This article shows how to control basic object movements and combine different transformations.


### See Also


- Article on [Matrix Transformations](../../../code/fundamentals/matrix_transformations/index_cs.md)
- Article on *[mat4](../../../code/uniginescript/language/data_types.md#mat4)* and *[dmat4](../../../code/uniginescript/language/data_types.md#dmat4)* UNIGINE data types


## Direction Vector


The direction vector is an important concept of mesh transformation. To move the node forward, you should know where the forward direction of the mesh is. When the mesh is exported from a 3D editor, it saves the information about the forward direction. And when you add the mesh to UNIGINE, it has the same orientation it had in a 3D editor.


| ![](direction_maya.png) | ![](direction_unigine.png) |
|---|---|
| *A mesh in Maya* | *The same mesh in UNIGINE* |


In the images above, the direction vector has the positive Y direction. To move this mesh forward, you should get the direction of the mesh by using the Y component (the second column) of the world transformation matrix of the mesh.


The point is that content creators and programmers should make an arrangement for the direction vector.


## Basic Movements


### Prearrangement


We are going to make a component that allows moving and rotating an object it is assigned to. Follow these steps to prearrange the environment for using the component:


1. [Prepare a C#-based project](../../../code/csharp/usage/using_cs_component_system/index.md#prepare).
2. Open the project in the Editor.
3. [create a C# component](../../../principles/component_system/component_system_cs/index.md#create).
4. Create the object that you are going to move, or select from the existing ones, and assign the component to it. > **Notice:** Make sure you assign the component to the node itself, not to a [Node Reference](../../../objects/nodes/reference/index.md). If the node you want assign this component to is a Node Reference, click *[Edit](../../../objects/nodes/reference/index.md#reference_editing)* in the *Parameters* tab, and assign the component to the node directly.
5. Open the component in IDE.


### Moving Forward


This section demonstrates how to set the forward movement of the mesh.


In this example, we use the *"p"* key pressing to move the mesh forward. The direction vector is visualized for clarity.


In the C# component file add the following (**don't change the Component *PropertyGuid***, it is assigned by the system):


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

#if UNIGINE_DOUBLE
    using Vec3 = Unigine.dvec3;
    using Vec4 = Unigine.dvec4;
    using Mat4 = Unigine.dmat4;
#else
    using Vec3 = Unigine.vec3;
    using Vec4 = Unigine.vec4;
    using Mat4 = Unigine.mat4;
#endif

public class MovementControls : Component
{
	// define the movement speed
	public float movement_speed = 5.0f;

	private void Init()
	{
		// check if the key is pressed and update the state of the specified control
		ControlsApp.SetStateKey(Controls.STATE_AUX_0, Input.KEY.O);
	}

	private void Update()
	{

		// get the frame duration
		float ifps = Game.IFps;

		// enable visualizer
		Visualizer.Enabled = true;

		// get the current world transform matrix of the node
		Mat4 transform = node.WorldTransform;

		// get the direction vector of the mesh from the second column of the transformation matrix
		Vec3 direction = transform.GetColumn3(1);

		// render the direction vector for visual clarity
		Visualizer.RenderDirection(node.WorldPosition, new vec3(direction), new vec4(1.0f, 0.0f, 0.0f, 1.0f), 0.1f, false);

		// check if the control key is pressed
		if (ControlsApp.GetState(Controls.STATE_AUX_0) == 1) {

			// calculate the delta of movement
			Vec3 delta_movement = direction * movement_speed * ifps;

			// set a new position to the node
			node.WorldPosition = node.WorldPosition + delta_movement;
		}
	}

}


```


#### Another Way of Setting Mesh Position


The new position can be also set by setting the *[WorldTransform](../../../api/library/nodes/class.node_cs.md#WorldTransform)* variable. The following examples contain the code from the *Update()* function of the *[AppWorldLogic](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic)* class. The part of controls initialization is the same for this method, the difference is in the *Update()* function only.


```csharp
// check if the control key is pressed
if (ControlsApp.GetState(Controls.STATE_AUX_0) == 1) {

	// calculate the delta of movement
	Vec3 delta_movement = direction * movement_speed * ifps;

	// set a new position to the node
	node.WorldTransform = MathLib.Translate(delta_movement) * transform;
}


```


Or you can change the translation column of the world transformation matrix (see the [Matrix Transformations](../../../code/fundamentals/matrix_transformations/index_cs.md) article) to move the node:


```csharp
// check if the control key is pressed
if (ControlsApp.GetState(Controls.STATE_AUX_0) == 1) {

	// calculate the delta of movement
	Vec3 delta_movement = direction * movement_speed * ifps;

	// set a new position
	// here, you can also use transform.setColumn3(3, transform.getColumn3(3) + delta_movement);
	transform.SetColumn(3, transform.GetColumn(3) + new Vec4(delta_movement, 1.0f));

	// set a new world transform matrix to the node
	node.WorldTransform = transform;
}


```


### Rotation


This section contains implementation of the mesh rotation.


You can rotate the mesh in two ways, by changing the transformation matrix represented by the *[WorldTransform](../../../api/library/nodes/class.node_cs.md#WorldTransform)* variable (recommended way) or via the *[SetWorldRotation()](../../../api/library/nodes/class.node_cs.md#setWorldRotation_quat_int_void)* function. The following example uses the second one:


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

#if UNIGINE_DOUBLE
    using Vec3 = Unigine.dvec3;
    using Vec4 = Unigine.dvec4;
    using Mat4 = Unigine.dmat4;
#else
    using Vec3 = Unigine.vec3;
    using Vec4 = Unigine.vec4;
    using Mat4 = Unigine.mat4;
#endif

public class MovementControls : Component
{
	// define the rotation speed
	public float rotation_speed = 30.0f;

	private void Init()
	{
		// check if the key is pressed and update the state of the specified control
		ControlsApp.SetStateKey(Controls.STATE_AUX_1, Input.KEY.I);
	}

	private void Update()
	{

		// get the frame duration
		float ifps = Game.IFps;

		// enable visualizer
		Visualizer.Enabled = true;

		// check if the control key is pressed
		if (ControlsApp.GetState(Controls.STATE_AUX_1) == 1) {

			// set the node rotation along the Z axis assuming node's scale equal to 1
			node.SetWorldRotation(node.GetWorldRotation() * new quat(MathLib.RotateZ(rotation_speed * ifps)), true);
		}
	}

}


```


In the example above, the node is rotated to the left by pressing the *"o"* keyboard key.


> **Notice:** - It is recommended to set the second argument of the *[SetWorldRotation()](../../../api/library/nodes/class.node_cs.md#setWorldRotation_quat_int_void)* function to 1 for all non-scaled nodes to improve performance and accuracy.
> - **Scaling of nodes should be avoided whenever possible**, as it requires addidional calculations and may lead to error accumulation.


To rotate the object by via the *[WorldTransform](../../../api/library/nodes/class.node_cs.md#WorldTransform)* variable, you should replace the line containing the *SetWorldRotation()* function in the example above with the following one:


```csharp
node.WorldTransform = node.WorldTransform * new Mat4(MathLib.RotateZ(rotation_speed * ifps));


```


This way is preferred, especially in case of [complex transformations](#combining), as it allows composing the transformation matrix and setting it only once.


## Combining Movements


Combining different movement controls is not more difficult than adding only one movement control.


The following code is an example that adds a mesh to the world and assigns a component on it that allows controlling its movements. You can rotate the mesh by using the *"o", "["* keyboard keys and move forward by using the *"p"* key.


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

#if UNIGINE_DOUBLE
    using Vec3 = Unigine.dvec3;
    using Vec4 = Unigine.dvec4;
    using Mat4 = Unigine.dmat4;
#else
    using Vec3 = Unigine.vec3;
    using Vec4 = Unigine.vec4;
    using Mat4 = Unigine.mat4;
#endif

public class MovementControls : Component
{
	// define the movement speed
	public float movement_speed = 5.0f;
	// define the rotation speed
	public float rotation_speed = 30.0f;

	private void Init()
	{
		// check if the key is pressed and update the state of the specified control
		// you can use 'I', 'O', 'P' keys
		ControlsApp.SetStateKey(Controls.STATE_AUX_0, Input.KEY.O);
		ControlsApp.SetStateKey(Controls.STATE_AUX_1, Input.KEY.I);
		ControlsApp.SetStateKey(Controls.STATE_AUX_2, Input.KEY.P);
	}

	private void Update()
	{
		// get the frame duration
		float ifps = Game.IFps;

		// enable visualizer
		Visualizer.Enabled = true;

		// get the current world transform matrix of the mesh
		Mat4 transform = node.WorldTransform;

		// get the direction vector of the mesh from the second column of the transformation matrix
		Vec3 direction = transform.GetColumn3(1);

		// initialize rotation and movement and update flag
		Mat4 rotation = Mat4.IDENTITY;
		Vec3 delta_movement = new Vec3(0.0f);
		bool update_transform = false;

		// render the direction vector for visual clarity
		Visualizer.RenderDirection(node.WorldPosition, new vec3(direction), new vec4(1.0f, 0.0f, 0.0f, 1.0f), 0.1f, false);

		// check if the control key for movement is pressed
		if (ControlsApp.GetState(Controls.STATE_AUX_0) == 1)
		{
			// calculate the delta of movement
			delta_movement = direction * movement_speed * ifps;
			update_transform = true;
		}

		// check if the control key for left rotation is pressed
		if (ControlsApp.GetState(Controls.STATE_AUX_1) == 1)
		{
			// set the node's left rotation along the Z axis
			rotation.SetRotateZ(rotation_speed * ifps);
			update_transform = true;
		}

		// check if the control key for right rotation is pressed
		else if (ControlsApp.GetState(Controls.STATE_AUX_2) == 1)
		{
			// set the node's right rotation along the Z axis
			rotation.SetRotateZ(-rotation_speed * ifps);
			update_transform = true;
		}

		// update transformation if necessary
		if (update_transform)
		{
			// combine transformations: movement + rotation
			transform = transform * rotation;
			transform.SetColumn3(3, transform.GetColumn3(3) + delta_movement);

			// set the resulting transformation
			node.WorldTransform = transform;
		}
	}

}


```
