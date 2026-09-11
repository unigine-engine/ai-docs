# Creating C++ Application


> **Warning:** The video tutorial is created with **SDK version 2.12**. Applicable for versions **up to 2.21**.


A UNIGINE-based application can be implemented by means of C++ only, without using UnigineScript.


This article describes how to add logic to your project by using the C++ language. Code written in C++ is the same for all supported platforms: Windows and Linux. The difference is in the way of compiling the project.


### See also


- Articles in the [Development for Different Platforms](../../code/environment/index.md) section to learn more on how to prepare the development environment, install the UNIGINE SDK and build the application for different platforms.
- Examples located in the `<UnigineSDK>/source/samples/Api` and `<UnigineSDK>/source/samples/App` folders.


## Creating Empty C++ Application


It is very easy to start your own C++ project by using UNIGINE SDK Browser:


1. Open the UNIGINE SDK Browser.
2. Go to the *[Templates](../../sdk/index.md#templates)* tab and click *Create Project* button on the *C++ Empty* template card. ![](../../sdk/projects/create_project_cpp.png)
3. Specify the following parameters: ![](cpp_parameters.png) > **Notice:** Read more about these parameters in [this article](../../sdk/projects/index_cpp.md)

  - **Project name** � specify the name of your project.
  - **Location** � specify the path to your project folder.
  - **SDK** � choose the UNIGINE SDK edition.
  - **API+IDE** � choose *C++* to start working with the C++ API. This parameter depends on a platform: You can also can create **C++ CMake** project

    - On **Windows**, you can create **C++ Visual Studio 2022** project.
    - On **Linux** you can create **C++ GNU make** project.
  - **Precision** - specify the precision. In this example we will use [double precision](../../code/double_precision/index.md).
4. Click the *CREATE NEW PROJECT* button. The project will appear in the *My Projects* tab list. ![](project_created.png)


You can [run](../../sdk/projects/index_cpp.md#run) your project by clicking the *Run* button.


> **Notice:** By default, in the [world script](../../code/fundamentals/execution_sequence/app_logic_system.md#world_script) file a WorldLight and a PlayerSpectator are created. You can leave functions of the world script empty, and create your own lights and players by using C++.


## Implementing C++ Logic


In this section we will add logic to the empty C++ application project.


The following example shows how to rotate the material ball that was created by default in your project.


1. If you created the **C++ project for Visual Studio**: If you created **C++ GNU make project**:

  1. Choose your C++ project in the UNIGINE SDK Browser and click the *Open Code IDE* button to open the project in IDE. ![](../../sdk/projects/edit_code.png)

  1. On the created C++ project, click on the *Other Actions* button and then the *Open Folder* button. ![](other_actions.png)
  2. Go to the `<YOUR PROJECT>\source\` folder and open the `AppWorldLogic.cpp` file with any plain text editor.
2. Write (or copy) the following code in your project's `AppWorldLogic.cpp` file. ```cpp #include "AppWorldLogic.h" #include <UnigineWorld.h> #include <UnigineGame.h> using namespace Unigine; // define pointer to node NodePtr node; AppWorldLogic::AppWorldLogic() { } AppWorldLogic::~AppWorldLogic() { } int AppWorldLogic::init() { // get the material ball node node = World::getNodeByName("material_ball"); return 1; } int AppWorldLogic::shutdown() { return 1; } int AppWorldLogic::update() { // get the frame duration float ifps = Game::getIFps(); // set the angle of rotation double angle = ifps * 90.0f; // set the angle to the transformation matrix Unigine::Math::Mat4 transform = node->getTransform(); transform.setRotateZ(angle); // set new transformation to the node node->setTransform(node->getTransform() * transform); return 1; } int AppWorldLogic::postUpdate() { return 1; } int AppWorldLogic::updatePhysics() { return 1; } ```
3. If you use **Visual Studio**, do the following: If you created a **GNU Make project**:

  1. Before compiling your code, check that the appropriate platform and configuration settings for your project are set correctly. ![](ide_project_settings.png)
  2. Build your project by clicking *Build -> Build Solution* in *Visual Studio*. ![](cpp_build.png)
  3. Start your project by clicking *Debug -> Start* in a proper mode in *Visual Studio*. ![](cpp_run.png)

  1. Execute the make command in the terminal to compile the application. ```bash make ```
  2. Launch the application by using the *run* script.


> **Notice:** To run the debug version of your project from SDK Browser, enable the *Debug* mode in *[Customize Run Options.](../../sdk/projects/index_cpp.md#customize_run)*
