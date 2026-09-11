# Adding Scripts to the Project

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


Starting coding your project is simple with the use of [UnigineScript](../../../code/uniginescript/index.md) language (no compilation is required).


For this tutorial we are going to get a primitive object (a box) from a script and add game logic to rotate it.


## Step 1. Add The Primitive Object To The World


1. Open the project in UNIGINE Editor via the SDK Browser. ![](../edit_content.png)
2. In the Menu Bar, choose *Create -> Primitive -> Box* to create a box object. ![](add_box.png)
3. In *Create Box* window that opens, specify the size of the box and click *OK*. ![](1_create_box.png)
4. Place the box somewhere in the world. ![](1_box_added.png)
5. By default, the added node is named *Cuboid*. Right-click it in the *[World Hierarchy](../../../editor2/organizing_nodes/index.md)* window and rename it *box*. ![](1_rename.png)
6. In the *Node* tab of the *Parameters* window, change the position of the box to **0.0, 0.0, 1.0**. ![](1_new_position.png)
7. In the Menu Bar, click *File -> Save World* or press **CTRL + S** to save the world.


## Step 2. Add Script Logic


There are two methods to add a script to the object:


- [Method 1: By Editing the `.usc` World Script File](#usc_file)
- [Method 2: By Using WorldExpression Objects](#world_expression)


### Method 1: By Editing the .usc World Script File


To add logic that will rotate the box, you should modify the `<your_project_name>.usc` world script file in a plain text editor.


> **Notice:** The `.usc` files do not require compilation, as they are interpreted by the Engine itself during its [initialization](../../../code/fundamentals/execution_sequence/init.md).


1. Open the project folder via the SDK Browser. ![](../open_folder.png) > **Notice:** If there is no *Open Folder* button, choose *Other Actions -> Open Folder*.
2. Open `<your_project_name>.usc` script file located in the `data` directory by using plain text editor. ```cpp #include <core/unigine.h> // This file is in UnigineScript language. // World script, it takes effect only when the world is loaded. int init() { // Write here code to be called on world initialization: initialize resources for your world scene during the world start. Player player = new PlayerSpectator(); player.setPosition(Vec3(0.0f,-3.401f,1.5f)); player.setDirection(Vec3(0.0f,1.0f,-0.4f)); engine.game.setPlayer(player); return 1; } // start of the main loop int update() { // Write here code to be called before updating each render frame: specify all graphics-related functions you want to be called every frame while your application executes. return 1; } int postUpdate() { // The engine calls this function before rendering each render frame: correct behavior after the state of the node has been updated. return 1; } int updatePhysics() { // Write here code to be called before updating each physics frame: control physics in your application and put non-rendering calculations. // The engine calls updatePhysics() with the fixed rate (60 times per second by default) regardless of the FPS value. // WARNING: do not create, delete or change transformations of nodes here, because rendering is already in progress. return 1; } // end of the main loop int shutdown() { // Write here code to be called on world shutdown: delete resources that were created during world script execution to avoid memory leaks. return 1; } ``` The world script contains the following functions by default: The following part of the *init()* function code creates a new free-flying game camera that collides with objects (but does not push or interact with them). Read [more](../../../api/index.md) about the Engine functions. ```cpp // create a new spectator player Player player = new PlayerSpectator(); // place it in the specified point player.setPosition(Vec3(0.0f,-3.401f,1.5f)); // turn it in the specified direction player.setDirection(Vec3(0.0f,1.0f,-0.4f)); // set the player as default one engine.game.setPlayer(player); ``` > **Notice:** Comments were added to explain the meaning of each line of the code.

  - *init()* function is used to create objects and initialize all other necessary resources on the world load.
  - *update()* function is used to code project logic and executed every frame.
  - *postUpdate()* function is used for correction purposes: it implements logic that is executed after updating the node's state.
  - *updatePhysics()* function is used to code physics simulation logic
  - *shutdown()* function is used to code project logic and executed when the world is unloaded.
3. Add a variable to handle the required `box` node before the *init()* function. > **Warning:** We do NOT recommend you to create global variables for the real project. ```cpp Node box; // add a box node int init() { /* ... */ } ```
4. Put this code into the *init()* function to get the `box` node. ```cpp Node box; // add a box node int init() { /* ... */ // get the node by the specified name box = engine.world.getNodeByName("box"); return 1; } ``` > **Notice:** Though nodes can be handled by any of the scripts (world, system or editor one) and [UnigineEditor](../../../api/library/engine/class.editor_cpp.md) (that loads and stores all the nodes from the `.world` file), they should be [owned](../../../code/uniginescript/memory_management.md#script) only by one of them. Otherwise, such nodes can cause Engine crash or memory leak problems. > See [Memory Management](../../../code/uniginescript/memory_management.md) article for details.
5. Set the node transformation in the [*update()*](../../../code/fundamentals/execution_sequence/main_loop.md#update) function. Note that it is necessary to scale the rotation angle each frame with the frame duration (because it's different for each individual frame) to get constant angular velocity. ```cpp /* ... */ int update() { // check whether the node exists if(box != NULL) { // get the frame duration float ifps = engine.game.getIFps(); // set the angle of rotation float angle = ifps * 90.0f; // get the current transformation of the node and apply rotation mat4 transform = box.getTransform() * rotateZ(angle); // set new transformation to the node box.setTransform(transform); } return 1; } ``` Thus, the resulting script is: ```cpp #include <core/unigine.h> // This file is in UnigineScript language. // World script, it takes effect only when the world is loaded. Node box; // add a box node int init() { // Write here code to be called on world initialization: initialize resources for your world scene during the world start. Player player = new PlayerSpectator(); player.setPosition(Vec3(0.0f,-3.401f,1.5f)); player.setDirection(Vec3(0.0f,1.0f,-0.4f)); engine.game.setPlayer(player); // get the node by the specified name box = engine.world.getNodeByName("box"); return 1; } // start of the main loop int update() { // Write here code to be called before updating each render frame: specify all graphics-related functions you want to be called every frame while your application executes. // check whether the node exists if(box != NULL) { // get the frame duration float ifps = engine.game.getIFps(); // set the angle of rotation float angle = ifps * 90.0f; // get the current transformation of the node and apply rotation mat4 transform = box.getTransform() * rotateZ(angle); // set new transformation to the node box.setTransform(transform); } return 1; } int postUpdate() { // The engine calls this function before rendering each render frame: correct behavior after the state of the node has been updated. return 1; } int updatePhysics() { // Write here code to be called before updating each physics frame: control physics in your application and put non-rendering calculations. // The engine calls updatePhysics() with the fixed rate (60 times per second by default) regardless of the FPS value. // WARNING: do not create, delete or change transformations of nodes here, because rendering is already in progress. return 1; } // end of the main loop int shutdown() { // Write here code to be called on world shutdown: delete resources that were created during world script execution to avoid memory leaks. return 1; } ```
6. Save all the changes in the `<your_project_name>.usc` world script file.
7. In the Menu Bar of UnigineEditor, choose *File -> Reload World* or run the `world_reload` console command. ![](2_console.png)
8. Check the result. ![](box_sc.gif)


### Method 2: By Using WorldExpression Objects


You can add the script to the box by using the *[WorldExpression](../../../objects/worlds/world_expression/index.md)* object.


1. In the Menu Bar, choose *Create -> Logic -> Expression* to create the *[WorldExpression](../../../objects/worlds/world_expression/index.md)* object. ![](add_expression.png)
2. Place the World Expression box somewhere in the world. The added World Expression node will appear in the *[World Hierarchy](../../../editor2/organizing_nodes/index.md)*. ![](2_place_worldex.png)
3. Choose the added *WorldExpression* node in the *World Hierarchy* window and go to the *Node* tab of the *Parameters* window. Here change the position to **1.0, -1.0, 0.5**. ![](2_we_position.png) Now you have the primitive box and the World Expression object on a plane. ![](2_two_nodes.png)
4. Specify the **Update Distance Limit** for the *WorldExpression* node - it is the maximum distance from the camera up to which the expression shall be executed. Let's set it to 10 units. ![](update_distance.png)
5. Choose the `WorldExpression` node in the World Hierarchy and go to the *World Expression* section of the *Parameters* window.
6. Put the following code into the *Source* field. ```cpp { // get the WorldExpression node via its internal function Node worldExpression = getNode(); // get the frame duration float ifps = engine.game.getIFps(); // set the angle of rotation float angle = ifps * 90.0f; // get the current transformation of the node and apply rotation mat4 transform = worldExpression.getTransform() * rotateZ(angle); // set new transformation to the node worldExpression.setTransform(transform); } ``` > **Warning:** Curly braces are mandatory! Other ways of attaching scripts to the *World Expression* object you can read [here](../../../objects/worlds/world_expression/index.md#attach_script).
7. Make the *box* node a child of the *WorldExpression* node by dragging it in the *World Hierarchy*. ![](2_add_child.png) Now the *box* node is the child of the *WorldExpression* node. It means that the box object inherits all expression transformations of the World Expression object. > **Notice:** All the child nodes of the *WorldExpression* node inherit expression transformations. Our expression shall be executed (i.e. the transformation shall be updated according to the script) as long as the distance from the camera to the *WorldExpression* node does not exceed the specified **Update Distance Limit**)
8. Check the result. ![](box_we.gif)


If you reset the position of the *box* node to its parent position, you will get the same result as in the [Method 1](#usc_file).


![](reset_position.png)


![](box_sc.gif)
