# Creating UnigineScript Application

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This article describes how to create an empty project and add logic to it by using the UnigineScript language. Code written in UnigineScript is the same for all supported platforms: Windows and Linux.


### See Also


- The article on [Setting Up Development Environment](../../code/environment/index.md) to learn more on how to prepare the development environment.


## Creating Empty UnigineScript Application


After installing the UNIGINE SDK Browser and preparing [development environment](../../code/environment/index.md) you can start your own UnigineScript-based project.


To create an empty UnigineScript API project, do the following:


1. Open the UNIGINE SDK Browser.
2. Go to *[Templates](../../sdk/index.md#templates)* and click *Create Project* button on the *UnigineScript Empty* template card. ![](../../sdk/projects/create_project_usc.png)
3. Specify the following parameters: ![](../../start/quick_start/setup_project/create_new_usc.png) > **Notice:** Read more about project parameters in [this article](../../sdk/projects/index_cpp.md).

  - *Project Name* � the name of your project.
  - *Location* � the path to your project folder.
  - *SDK* � the UNIGINE SDK.
  - *Precision* � choose [double precision](../../code/double_precision/index.md) for this example.
4. Click the *CREATE NEW PROJECT* button. The project will appear in the *My Projects* tab list. ![](../cpp/project_created.png)


You can [run](../../sdk/projects/index_cpp.md#run) your project by clicking the **Run** button.


## Implementing UnigineScript Logic


In this section we will add logic to the empty UnigineScript application project.


The following example shows how to add a primitive box mesh to the world and rotate it.


1. In UNIGINE SDK Browser, choose the created UnigineScript project and click the **Open Editor** button. ![](edit_content.png)
2. In Unigine Editor that opens, add a primitive box as described in [this section](../../code/uniginescript/add_scripts/index.md#add_primitive). Also name the primitive as in the example. ![](primitive_added.png)
3. Save the World by clicking *File -> Save World* on the Menu bar or press **CTRL + S** and close UnigineEditor.
4. In UNIGINE SDK Browser, choose your UnigineScript project and click the **Open Folder** button. ![](open_folder.png)
5. Open the world script `.usc` file located in the `<YOUR PROJECT FOLDER>/data/<YOUR PROJECT NAME>/` (in our case, it is `script/data/script_project/script_project.usc` file) by using any plain text editor or IDE.
6. Modify the file by adding the following code: ```cpp #include <core/unigine.h> Node box; int init() { PlayerSpectator camera = new PlayerSpectator(); camera.setPosition(Vec3(2.0f,0.0f,1.5f)); camera.setDirection(Vec3(-1.0f,0.0f,-0.5f)); engine.game.setPlayer(camera); // search the node by the specified name int index = engine.editor.findNode("box"); // get the node by its index if(index != -1) { box = engine.editor.getNode(index); } return 1; } int shutdown() { return 1; } int update() { //check whether the node exists if(box != NULL) { // get the frame duration float ifps = engine.game.getIFps(); // set the angle of rotation float angle = ifps * 90.0f; // get the current transformation of the node and apply rotation mat4 transform = box.getTransform() * rotateZ(angle); // set new transformation to the node box.setTransform(transform); } return 1; } ``` > **Notice:** In the code above, we load the `script_project/script_project.usc` world script file. You should specify the name of your project's world script file.
7. Save changes in the world script file.
8. In the UNIGINE SDK Browser, click [*Run*](../../sdk/projects/index_cpp.md#run) to launch the project ![](run.png)
