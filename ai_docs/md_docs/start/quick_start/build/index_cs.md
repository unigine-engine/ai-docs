# Packing a Final Build for Publishing (CS)


Before your project can be distributed to users, it must be properly **built**. To build a [C# Component System](../../../principles/component_system/component_system_cs/index.md) project, all components should be initialized and compiled successfully.


![](build_successful.png)

*Successfully build components*


If you encounter the red error message in the UnigineEditor, indicating that some of your components were not built, check the Editor Console window for details. You may need to [debug](../../../code/csharp/debug_components.md) the source code to find errors.


![](build_failed.png)

*Failure to build some components*


## Step 1. Build the Game


[Packing a final build](../../../editor2/projects/build_project.md) ensures that all content and code, including all necessary libraries, is up to date, in the proper format, and placed to a proper location to run on the desired target platform.


1. Switch to the UnigineEditor. To assemble the project, choose *File->Create Build*. The **Create Build** window will open.
2. In the *Create Build* window, set the *Build Type* to **Release**.
3. Set the name to be `QuickStart` and specify the *output folder* in the *Build Folder* field. Make sure the *Default World* is set to your game world (`level.world` in our example). ![](build_settings.png)
4. The **Delete Unused Assets** option shall by default remove the materials used for our [generated objects](../../../start/quick_start/physical_objects/index_cs.md), as they're only used in our code (the *Build* tool doesn't know that). This is the case when you have to **force-include** them manually. You can do it by adding the following line to the list. ![](force_include.png) For more information on the **Delete Unused Assets** option see the related [HowTo Video](../../../videotutorials/how_to/how_to_basics/delete_unused_assets.md).
5. Click the green **Create Build** button at the bottom of the *Create Build* window. The assembling progress bar will appear indicating the status of the build process. ![](build_process.png)


> **Notice:** If a project fails to build, check the UnigineEditor console for more details.


## Step 2. Launch the Game


1. Upon completion of the build process, the output folder will be automatically opened. To play the game, launch `QuickStart.exe`.
2. In the Unigine launcher, specify the resolution and the window mode. ![](launcher.png)
3. Click **Run** to launch the standalone application and play the game.


Congratulations, you've made your first project! You may now expand upon it and implement more features.
