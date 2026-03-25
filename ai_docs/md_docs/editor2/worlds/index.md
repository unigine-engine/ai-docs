# Managing Worlds


A world in UNIGINE is a scene that includes a set of different [built-in objects](../../objects/index.md) with certain parameters. UnigineEditor provides an ability to create new worlds, load or reload existing ones, and save them if any changes are made. You can also [adjust various settings](#world_settings) for the worlds you create.


### See Also


- [World](../../api/library/engine/class.world_cpp.md) class to manage worlds via code


## Creating a New World


To create a new world via UnigineEditor:


1. Click *File -> Create New World* in the Main Menu, or press **CTRL + N**. ![](create_new_world.png)
2. In the window that opens, specify a name for the new world and choose the target directory within your project. ![](select_world_to_create.png)


After that, a new asset is created in the target folder: `your_world_name.world` - an XML file containing rendering settings of the created world.


> **Notice:** A new world with default [*sun*](../../objects/lights/world/index.md) node will be created. You can keep this node or delete it at your own discretion.


Unlike the world, which is created at the project creation, all other worlds are created without a [world script](../../code/fundamentals/execution_sequence/app_logic_system.md#world_script) file. If necessary, this file is added as a script to the `*.world` file via UnigineEditor as follows:


1. Click the **Create** button in the Asset Browser and select *Create USC*. The `script.usc` file is created. You can rename and relocate the created file. ![](create_usc.png)
2. Select the required `*.world` file in the Asset Browser.
3. In the Parameters tab, [assign](#assign_script) the `*.usc` that you created as a script.


## Loading an Existing World


To load an existing world via UnigineEditor:


1. Click *File -> Open World* in the Main Menu, or press **CTRL + O**. ![](load_world.png)
2. Choose the directory and select the required world. > **Notice:** Via UnigineEditor, you can only load worlds that are available within your project. ![](select_world_to_load.png)
3. Click *OK*. The selected world will be loaded.


To load one of the *recently closed worlds*, click *File -> Recent Worlds* in the Main Menu, choose the required world and select it.


![](recent_worlds.png)


## Saving a World


To save the current world under a different name via UnigineEditor:


1. Click *File -> Save World As...* in the main menu. ![](save_world_as.png)
2. Specify a new name for the world to save and choose the target directory within your project: ![](select_world_to_create.png)
3. Click *OK*.


To save a world under its current name:


1. Click *File -> Save World* in the main menu, or press **CTRL + S**. ![](save_world.png)


## Reloading a World


To reload the current world:


1. Click *File -> Reload World* in the main menu. ![](reload_world.png) If there are unsaved changes in the world, the dialog box will open.
2. Click *Yes* in the dialog box to save all changes before reloading. ![](close_confirm.png)


## Closing a World


To close the current world:


1. Click *File -> Close World* in the main menu. ![](close_world.png) If there are unsaved changes in the world, the dialog box will open.
2. Click *Yes* in the dialog box to save all changes before closing. ![](close_confirm.png) The world will be closed as a result.


## Assigning a Script


By default, your world is assigned [the script](../../code/fundamentals/execution_sequence/app_logic_system.md#world_script), which is created when a [new world is created](#create_world). To assign another script, select the world in the Asset Browser and drag and drop a script to the Parameters Tab:


![](world_script.gif)


## Adjusting World Settings


Each world can have its unique sound, physics, and rendering settings. This allows you to adjust everything from gravity to how the Global Illumination will look in a particular world. All world settings are available in the corresponding section of the [*Settings window*](../../editor2/settings/index.md).


To view or adjust settings for your current world:


1. Click *Windows -> Settings* in the Main Menu. ![](../settings/settings_open.png)
2. Then in the left panel of the *Settings* window choose the desired section from *Runtime -> World*. ![](world_settings.png)


You can save your settings in a corresponding settings file: `*.physics, *.sound, *.render` and use them for another world or project.


![](../settings/settings_load.png)


Learn more about the [*Settings window*](../../editor2/settings/index.md).
