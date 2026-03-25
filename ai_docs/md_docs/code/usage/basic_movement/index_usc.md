# Basic Object Movements (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


After adding an object to UNIGINE, you can control its transformations with your control devices. This article shows how to control basic object movements and combine different transformations.


### See Also


- Article on [Matrix Transformations](../../../code/fundamentals/matrix_transformations/index_usc.md)
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


### Moving Forward


This section demonstrates how to set the forward movement of the mesh.


In this example, we use the *"p"* key pressing to move the mesh forward. The direction vector is visualized for clarity.


```cpp
// define the ObjectMeshStatic mesh, player, and movement speed
ObjectMeshStatic mesh;
float movement_speed = 5.0f;
Player player;

/*
	the world script init() function
 */
int init() {

	// enable visualizer
	engine.visualizer.setEnabled(1);

	// create a camera and add it to the world
	player = new PlayerSpectator();
	player.setPosition(Vec3(4.0f, -3.401f, 1.5f));
	player.setDirection(vec3(0.0f, 1.0f, -0.4f),player.getUp());
	engine.game.setPlayer(player);

	// create a mesh by adding a box surface to it
	Mesh mesh_0 = new Mesh();
	mesh_0.addBoxSurface("box_surface", vec3(1.0f));
	// add the mesh to the editor as the ObjectMeshStatic
	mesh = new ObjectMeshStatic(mesh_0);
	// set the mesh position
	mesh.setPosition(Vec3(4.0f,0.0f,1.0f));

	// check if the key is pressed and update the state of the specified control
	// you can use both 'p' or ASCII code (112)
	engine.controls.setStateKey(CONTROLS_STATE_AUX_0,'p');

	return 1;
}

/*
	the world script update() function
*/
int update() {

	// get the frame duration
	float ifps = engine.game.getIFps();

	// get the current world transform matrix of the mesh
	Mat4 transform = mesh.getWorldTransform();

	// get the direction vector of the mesh by using swizzling
	Vec3 direction = transform.m01m11m21;

	// render the direction vector for visual clarity
	engine.visualizer.renderDirection(mesh.getWorldPosition(), vec3(direction), vec4(1.0f, 0.0f, 0.0f, 1.0f), 0.1f, 0);

	// check if the control key is pressed
	if(engine.controls.getState(CONTROLS_STATE_AUX_0)) {

		// calculate the delta of movement
		Vec3 delta_movement = direction * movement_speed * ifps;

		// set a new position to the mesh
		mesh.setWorldPosition(mesh.getWorldPosition() + delta_movement);
	}

	return 1;
}

```


Another way of getting the direction vector is by using this command:


```cpp
Vec3 direction = Vec3(transform.col1);
```


#### Another Way of Setting Mesh Position


The new position can be also set by setting the *[WorldTransform](../../../api/library/nodes/class.node_usc.md#WorldTransform)* variable. The following examples contain the code from the *Update()* function of the *[AppWorldLogic](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic)* class. The part of controls initialization is the same for this method, the difference is in the *Update()* function only.


```cpp
// check if the control key is pressed
if(engine.controls.getState(CONTROLS_STATE_AUX_0)) {

	// calculate the delta of movement
	Vec3 delta_movement = direction * movement_speed * ifps;

	// set a new position to the mesh
	mesh.setWorldTransform(translate(delta_movement) * transform);
}

```


Or you can change the translation column of the world transformation matrix (see the [Matrix Transformations](../../../code/fundamentals/matrix_transformations/index_usc.md) article) to move the node:


```cpp
// check if the control key is pressed
if(engine.controls.getState(CONTROLS_STATE_AUX_0)) {

	// calculate the delta of movement
	Vec3 delta_movement = direction * movement_speed * ifps;

	// set a new position
	// here, you can also use swizzling: transform.m03m13m23 += delta_movement;
	transform.col3 += Vec4(delta_movement,1.0f);

	// set a new position to the mesh
	mesh.setWorldTransform(transform);
}

```


### Rotation


This section contains implementation of the mesh rotation.


You can rotate the mesh in two ways, by changing the transformation matrix represented by the *[WorldTransform](../../../api/library/nodes/class.node_usc.md#WorldTransform)* variable (recommended way) or via the *[SetWorldRotation()](../../../api/library/nodes/class.node_usc.md#setWorldRotation_quat_int_void)* function. The following example uses the second one:


```cpp
// define the ObjectMeshStatic mesh, player, and rotation speed
ObjectMeshStatic mesh;
float rotation_speed = 30.0f;
Player player;

/*
	the world script init() function
 */
int init() {
	// enable visualizer
	engine.visualizer.setEnabled(1);

	// create a camera and add it to the world
	player = new PlayerSpectator();
	player.setPosition(Vec3(4.0f, -3.401f, 1.5f));
	player.setDirection(vec3(0.0f, 1.0f, -0.4f),player.getUp());
	engine.game.setPlayer(player);

	// create a mesh by adding a box surface to it
	Mesh mesh_0 = new Mesh();
	mesh_0.addBoxSurface("box_surface", vec3(1.0f));
	// add the mesh to the editor as the ObjectMeshStatic
	mesh = new ObjectMeshStatic(mesh_0);
	// set the mesh position
	mesh.setPosition(Vec3(4.0f,0.0f,1.0f));

	// check if the key is pressed and update the state of the specified control
	// you can use both 'o' or ASCII code (111)
	engine.controls.setStateKey(CONTROLS_STATE_AUX_1,'o');

	return 1;
}

/*
	the world script update() function
*/
int update() {

	// get the frame duration
	float ifps = engine.game.getIFps();

	// check if the control key is pressed
	if(engine.controls.getState(CONTROLS_STATE_AUX_1)) {
		// set the node rotation along the Z axis assuming node's scale equal to 1
		mesh.setWorldRotation(mesh.getWorldRotation() * quat(rotateZ(rotation_speed * ifps)), 1);
	}

	return 1;
}

```


In the example above, the node is rotated to the left by pressing the *"o"* keyboard key.


> **Notice:** - It is recommended to set the second argument of the *[SetWorldRotation()](../../../api/library/nodes/class.node_usc.md#setWorldRotation_quat_int_void)* function to 1 for all non-scaled nodes to improve performance and accuracy.
> - **Scaling of nodes should be avoided whenever possible**, as it requires addidional calculations and may lead to error accumulation.


To rotate the object by via the *[WorldTransform](../../../api/library/nodes/class.node_usc.md#WorldTransform)* variable, you should replace the line containing the *SetWorldRotation()* function in the example above with the following one:


```cpp
mesh.setWorldTransform(mesh.getWorldTransform() * rotateZ(rotation_speed * ifps));
```


This way is preferred, especially in case of [complex transformations](#combining), as it allows composing the transformation matrix and setting it only once.


## Combining Movements


Combining different movement controls is not more difficult than adding only one movement control.


The following code is an example that adds a mesh to the world and assigns a component on it that allows controlling its movements. You can rotate the mesh by using the *"o", "["* keyboard keys and move forward by using the *"p"* key.


```cpp
// define mesh, player, movement and rotation speed
ObjectMeshStatic mesh;
Player player;
float movement_speed = 5.0f;
float rotation_speed = 30.0f;

/*
	the world script init() function
 */
int init() {
	// enable visualizer
	engine.visualizer.setEnabled(1);

	// create a camera and add it to the world
	player = new PlayerSpectator();
	player.setPosition(Vec3(4.0f, -3.401f, 1.5f));
	player.setDirection(vec3(0.0f, 1.0f, -0.4f),player.getUp());
	engine.game.setPlayer(player);

	// create a mesh by adding a box surface to it
	Mesh mesh_0 = new Mesh();
	mesh_0.addBoxSurface("box_surface", vec3(1.0f));
	// add the mesh to the editor as the ObjectMeshStatic
	mesh = new ObjectMeshStatic(mesh_0);
	// set the mesh position
	mesh.setPosition(Vec3(4.0f,0.0f,1.0f));

	// check if the key is pressed and update the state of the specified control
	// you can use both 'p', 'o', '[' or ASCII codes (112, 111, 113)
	engine.controls.setStateKey(CONTROLS_STATE_AUX_0, 'p');
	engine.controls.setStateKey(CONTROLS_STATE_AUX_1, 'o');
	engine.controls.setStateKey(CONTROLS_STATE_AUX_2, '[');

	return 1;
}

/*
	the world script update() function
*/
int update() {

	// get the frame duration
	float ifps = engine.game.getIFps();

	// get the current world transform matrix of the mesh
	Mat4 transform = mesh.getWorldTransform();

	// get the direction vector of the mesh by using swizzling
	Vec3 direction = transform.m01m11m21;

	// initialize rotation, movement, and update flag
	int update_transform = 0;
	quat rotation = quat(0.0f, 0.0f, 0.0f, 0.0f);
	Vec3 delta_movement = Vec3(0.0f);

	// render the direction vector for visual clarity
	engine.visualizer.renderDirection(mesh.getWorldPosition(), vec3(direction), vec4(1.0f, 0.0f, 0.0f, 1.0f));

	// check if the control key for movement is pressed
	if(engine.controls.getState(CONTROLS_STATE_AUX_0)) {
		// calculate the delta of movement
		delta_movement = direction * movement_speed * ifps;
		update_transform = 1;
	}

	// check if the control key for left rotation is pressed.
	if(engine.controls.getState(CONTROLS_STATE_AUX_1))
	{
		// set the node's rotation along the Z axis
		rotation = quat(rotateZ(rotation_speed * ifps));
		update_transform = 1;
	}
	// check if the control key for right rotation is pressed.
	else if(engine.controls.getState(CONTROLS_STATE_AUX_2))
	{
		// set the node's rotation along the Z axis
		rotation = quat(rotateZ(-rotation_speed * ifps));
		update_transform = 1;
	}

	// update transformation if necessary
    if (update_transform)
    {
		// combining transformations: movement + rotation
		transform = transform*rotation;
		transform.col3 += Vec4(delta_movement, 1.0f);

		// setting the resulting transformation
		mesh.setWorldTransform(transform);
	}

	return 1;
}

```
