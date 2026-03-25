# Packing a Final Build for Publishing (CPP)


Before your project can be distributed to users, it must be properly **built**. To build a [C++ Component System](../../../principles/component_system/component_system_cpp/index.md) project, all components should be compiled successfully.


## Step 1. Build the Game


[Packing a final build](../../../editor2/projects/build_project.md) ensures that all content and code, including all necessary libraries, is up to date, in the proper format, and placed to a proper location to run on the desired target platform.


1. In your IDE set the configuration of the solution to *Release* and build the executable for the project. ![](release_config.png)
2. Switch to the UnigineEditor. To assemble the project, choose *File->Create Build*. The **Create Build** window will open.
3. In the *Create Build* window, set the Build Type to *Release*. Set the name to be `quick_start_cpp` and specify the output folder in the *Build Folder* field. Make sure the **Default World** is set to your game world. ![](build_settings_cpp.png)
4. In the **Release App** field of the *Launcher Default Settings* section, set the path to the executable you have just compiled (the default output path in Visual Studio is set to `<my_project>/bin/<my_app>_x64)`. ![](release_app.png)
5. Click the green **Create Build** button at the bottom of the *Create Build* window. The assembling progress bar will appear indicating the status of the build process. ![](progress.png)


> **Notice:** If a project fails to build, check the UnigineEditor console for more details.


## Step 2. Launch the Game


1. Upon completion of the build process, the output folder will be automatically opened. To play the game, launch `quick_start_cpp.exe`.
2. In the Unigine launcher, specify the resolution and the window mode. ![](launcher.png)
3. Click **Run** to launch the standalone application and play the game.


Congratulations, you've made your first project! You may now expand upon it and implement more features.
