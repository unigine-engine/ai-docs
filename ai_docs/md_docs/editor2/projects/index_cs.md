# Working with Projects (CS)


A **project** is an independent entity that contains all data on your application content organized in a set of directories. The `*.project` file containing metadata is associated with the project.


> **Notice:** One project can consist of several [worlds](../../principles/world_structure/index.md). So, there is no need to create a separate project for each world.


## Creating New Project


In UNIGINE, projects are created, configured, and managed through the [SDK Browser](../../sdk/index.md#projects). Once the Browser is installed and ready to use, the first step in creating a new project is selecting a suitable project **template** - a basis that matches your project's goals.


**Templates** provide a ready-to-use foundation: a preconfigured scene, core systems, and commonly used objects. They also include optimal settings for rendering, camera, physics, input, and plugins, set up for specific types of tasks. For a detailed description of each template, refer to the *[Project Templates](../../sdk/templates/index.md)*article.


Before starting to create new projects you should have an [SDK](../../sdk/index.md#sdks) installed. Once you have the required version of the SDK, you can create a new project as follows:


1. Open the *Templates* tab in the SDK browser. [![](../../sdk/projects/templates_sm.png)](../../sdk/projects/templates.png) *Templates are organized into logical categories (Base, Aviation, etc.) to simplify navigation* > **Notice:** Each template card indicates the SDK **[editions](https://unigine.com/get-unigine/)** in which the template is available: > > > ![](../../sdk/projects/sdk_edition.png)
2. Select a template that meets your needs, and click **Create Project**. The project creation window will open. ![](../../sdk/projects/create_project_cs.png) > **Notice:** You can also create a project by clicking *Create New* in the *My Projects* tab of the SDK browser, which automatically redirects you to the *Templates* tab. > > > ![](../../sdk/projects/projects.png)
3. Specify the name of the project, choose a path to store project files, and select the SDK to be used. Enable any required [application and general settings](#application_settings) if needed. If the selected template or SDK version has not been installed previously, a notification will appear informing you that the required files will be downloaded before the project is created. ![](../../sdk/projects/download_data.png)
4. Click *Create New Project*. You can monitor the creation progress in the *My Projects* tab and in the left panel of the SDK Browser. ![](../../sdk/projects/download_data_progress.png) The project will appear in the *My Projects* tab list. [![](../../sdk/projects/my_projects_sm.png)](my_projects.png) The project files are located in the `<project path>/<unigine_project>` folder. > **Notice:** You can change the project settings any time by clicking **Other Actions -> [Configure](#configure)**.


See the **[video tutorial](../../videotutorials/how_to/how_to_cs/create_project.md)** demonstrating how to create a new C# project.


### Application Settings


Projects can be created with the following application settings available depending on the selected template:


![](../../sdk/projects/application_settings.png)


| API+IDE | Programming language to be used for project creation. The following APIs are available: - *UnigineScript only* � UnigineScript will be used to implement the project. - *C++* � C++ API will be used to implement the project. One of the following variants can be used depending on the OS: - On Windows: - *C++ (Visual Studio 2022)* - *C++ (CMake)* - On Linux: - *C++ GNU Make* - *C# (.NET)* � C# API and [Component System](../../principles/component_system/component_system_cs/index.md) will be used to implement the project. .NET is required for building the project. |
|---|---|
| Precision | The coordinates precision to be used: - *Float* � single precision - *Double* � [double precision](../../code/double_precision/index.md) |


### Features


The project can be created with the following **features**:


![](../../sdk/projects/general_settings.png)


| Command-line Runtimes�Generator | Enables [Command-line Runtimes Generator](../../tools/runtimes_generator/index.md) for the project. |
|---|---|
| Command-line Build�Tool | Enables the [Command-line Build Tool](../../editor2/projects/build_project.md#console_build) for the project. |
| Sandworm Distributed�& Headless Mode | Enables creation of the console application required on *Worker* computers for [distributed computing and headless generation](../../editor2/sandworm/generation/distributed_computing/index.md) of terrain using the Sandworm tool for the project. |
| Editor Plugin�Template | Enables the creation of an [editor plugin](../../editor2/extensions/custom_plugin.md) based on available templates for the project. |
| Engine Plugin�Template | Enables creation of an [Engine plugin](../../code/cpp/plugin.md#step_1) to extend the core functionality of the Engine. |


The **Plugins (0)** button opens the list of available plugins:


| **STEREO 3D** |  |
|---|---|
| Dual output stereo 3D (Separate plugin) | Output [2 separate images](../../principles/render/output/stereo/appseparate/index.md) for each eye. > **Notice:** The Separate plugin is available on Windows only. |
| **MULTI-MONITOR** |  |
| SpiderVision (SpiderVision plugin) | Render the application into the [configurable number of monitors or projections](../../principles/render/output/multi_monitor/spidervision_plugin/index.md), or use a multi-projector setup stored in a calibration file created via *Scalable Display Manager* and set up via *EasyBlend SDK*. |
| 3-monitor output (Surround plugin) | Render the application across [3 monitors simultaneously](../../principles/render/output/multi_monitor/appsurround/index.md). |
| **NETWORK** |  |
| ARTTracker plugin | Create a project with the [ARTTracker](../../code/plugins/arttrack/index.md) plugin. |
| Steam plugin | Create a project with the plugin for Steam integration. |
| Syncker plugin | Create a project with the *[Syncker](../../code/plugins/syncker/index.md)* plugin for multi-channel rendering synchronization. |
| VRPN Client plugin | Create a project with the *[VRPN Client](../../code/plugins/vrpn/index.md)* plugin. |
| WebStream plugin | Create a project with the *[WebStream](../../code/plugins/webstream/index.md)* plugin. |
| **SPECIALS** |  |
| GPU Monitor plugin | Enable [GPU frequencies and temperature monitoring](../../code/plugins/gpumonitor/index.md) for your project. |
| Gaussian Splatting plugin | Importing and rendering 3D [Gaussian Splatting](../../code/plugins/gaussian/index.md) (`*.ply`) files in your project. |
| Kinect2 Plugin | Create a project with the [Kinect2](../../code/plugins/kinect2/index.md) plugin. |
| Ultraleap | Tracking hands and fingers with *[Ultraleap](../../code/plugins/ultraleap/index.md)*. |
| VCSIntegration Plugin | Using the [version control system (SVN, Git)](../../editor2/assets_workflow/version_control/vcs_plugin/index.md) to track all file changes performed in UNIGINE Editor. |
| **SOUND** |  |
| FMOD plugin | [Plugin](../../code/plugins/fmod/index.md) providing integration with [FMOD](https://www.fmod.com/) library developed by Firelight Technologies. FMOD is a solution that includes all the tools you need to add sound and music to video games and applications. |


## Adding Existing Project


To add an existing project to the browser:


1. Click **Add Existing** in the *Projects* tab. ![](../../sdk/projects/add_existing.png)
2. In the file dialog window that opens, specify the path to the project folder and click **Import Project**. The project will appear in the projects list. ![](../../sdk/projects/add_existing_form.png)


> **Notice:** If the added project was created in the SDK of a previous version, it will be marked with the *[Upgrade](#upgrade_project)* label.


## Upgrading Existing Project


Projects that require upgrade are marked with the *Upgrade* label:


![](../../sdk/projects/upgrade_available.png)


To upgrade your project to the newest installed version of UNIGINE SDK:


1. Click the **Upgrade** label on the project image or **[Other Actions](#other_actions) -> Configure**. The following form will open: ![](../../sdk/projects/upgrade_form.png)
2. If a project upgrade requires installing a [template](../../sdk/templates/index.md) (for example, when upgrading a non-template-based project created with an SDK version earlier than **2.21**), you will see the following notification: ![](../../sdk/projects/template_download.png) The template will be downloaded and installed during upgrade process. If **no network connection** is available, the following message will appear: ![](../../sdk/projects/no_connection.png) > **Notice:** To upgrade the project without a network connection, see the [manual template installation](../../sdk/templates/index.md#manual_setup) guide.
3. Choose the newest installed version of the SDK and click **CONFIGURE PROJECT**.
4. Specify a path to the backup folder into which the original project will be copied. Keep *Migrate Content* checked and click *UPGRADE PROJECT*. ![](../../sdk/projects/upgrade_confirm.png)


The project will be upgraded automatically. You can also manually upgrade the project by running the [upgrade script](../../tools/upgrade/index.md). In both cases, the same script will be used.


> **Notice:** The source code should be upgraded manually by using the *[Migration Guide](../../upgrade/migration_api.md)*.


## Repairing a Project


If critical project files are missing (e.g., due to deleting the project with the ***Keep Data*** option enabled and then re-importing it), the SDK Browser will prompt you to repair the project. The repair process will restore the project to a working state.


![repairing_project](../../sdk/projects/repair_project.png)


## Running a Project


To run the actual compiled binary of the project with default settings, click the **Run** button:


![](../../sdk/projects/run_level.png)


You can also use **launchers** created by default in the project folder:


- ![](../../sdk/projects/file.png) `launch_debug` - the launcher of the project's debug version.
- ![](../../sdk/projects/file.png) `launch_editor` - the launcher of the project's with the loaded editor.
- ![](../../sdk/projects/file.png) `launch_release` - the launcher of the project's release version. > **Notice:** To use the release launcher, you should [reconfigure your project](#engine_build) to the *Release* binaries first.


### Running Project with Custom Settings


To run the project with custom settings, click an ellipsis on the **Run** button:


![](../../sdk/projects/run_ellipsis.png)


The *Customize Run Options* form will open.


Depending on the value of the **Application** option, different sets of options are available:


- *Default* - the default main application (`<project_name>_x*.exe`) will be run: ![](../../sdk/projects/custom_run.png) The default main application should be used when only [UnigineScript](#api) is used to implement the project. In this case, the following options can be customized: | Debug | Indicates whether debug or release version of the application should be run. | |---|---| | Microprofile Enabled | Run the application with the [Microprofile](../../tools/profiling/microprofile/index.md) tool enabled. | | Arguments | [Start-up command-line options](../../code/command_line.md). | | Remember | Indicates whether to remember the specified custom settings for the future run. |
- *Custom* � a custom main application will be run: ![](../../sdk/projects/custom_run_custom.png) This option should be chosen if the *[C++ or C# API](#api)* is used to implement the project (besides UnigineScript). In this case, the following options can be customized: | Binary | Name of the custom main application. Here the name of the compiled binary executable located in the `bin` folder of the project should be specified. If the binary executable is located outside this folder, a path to it relative to the `bin` folder should be specified. | |---|---| | Arguments | [Start-up command-line options](../../code/command_line.md). | | Remember | Indicates whether to remember the specified custom settings for future run. |


## Editing a Project


The project content is edited via UNIGINE Editor, code is edited via IDE.


- To edit the project content, click **Open Editor**. ![](../../sdk/projects/run_editor.png)
- To edit the source code use **Open Code IDE**. The IDE selected as the default one will be used to open code. ![](../../sdk/projects/edit_code.png)


The project editing tools can also be run in a customized mode.


### Customizing UNIGINE Editor Options


Customize the UNIGINE Editor running options by clicking an ellipsis on the **Open Editor** button:


![](../../sdk/projects/edit_ellipsis.png)


In the *[Customize UNIGINE Editor Options](#customize_edit)* form that opens, set the required values and click **Edit**.


![](../../sdk/projects/custom_edit.png)


| Additional arguments | [Start-up command-line options](../../code/command_line.md). |
|---|---|
| Debug | The editor version (debug or release) that will be used for project's editing. |
| Microprofile Enabled | Run the application with the [Microprofile](../../tools/profiling/microprofile/index.md) tool enabled. |
| Remember | Indicates whether to remember the specified custom settings for a future run or not. |


### Customizing IDE Options


To change a tool, do the following:


- On **Windows**, click an ellipsis on the **Open Code IDE** button. The following form will open: ![](../../sdk/projects/customize_edit_code.png) Choose **Custom** in the drop-down list and specify a path to a custom tool (e.g. IDE or editor) with required arguments: ![](../../sdk/projects/custom_edit_code.png)
- On **Linux**, click **[Open Folder](#other_actions)** and then edit code in an associated tool. ![](../../sdk/projects/open_folder.png)


#### See Also


- Articles in the [*Programming Overview*](../../code/fundamentals/programming_overview/index.md) section to learn how to edit the opened project
- The [video tutorial](https://youtu.be/tZPiBybsnbE) demonstrating how to change the IDE


## Release and Development Builds


You can choose the *Development* or *Release* build of UNIGINE Engine:


- The *Development* build includes additional features that can be useful for project's development (*[Microprofile](../../tools/profiling/microprofile/index.md)*, etc.)
- The *Release* build allows checking the final performance of the application.


By default, the project is configured to use **Development** Engine binaries that contain additional debugging tools. **Development** binaries of the Engine require a running SDK Browser instance, just the same way as for the UnigineEditor.


You can run your application without running SDK Browser via the [`launch_release`](#launchers) file in the project folder, but first, you should reconfigure the project to use the **Release** binaries.


To reconfigure the project:


1. Click **Other Actions -> [Configure](#configure)**. ![](../../sdk/projects/other_actions.png)
2. Select the *Release* option in the **Engine** drop-down. ![](../../sdk/projects/change_build_type.png)
3. Click the **Update Configuration** button at the bottom of the configuration window to save the configuration.


As soon as the project has been reconfigured to the *Release* build, it can be run without SDK Browser - run the `launch_release` file in the project folder.


The *Release* binaries should be used in the final build of the project.


## Other Actions


![](../../sdk/projects/other_actions.png)


When clicking the **Other Actions** button, the following options are available:


| Configure | [Change](#update_config) project settings. |
|---|---|
| Open Folder | Open the project folder. |
| Delete | Delete the project. |


## Updating Project Configuration


When clicking **Other Actions -> Configure**, the following form opens:


![](../../sdk/projects/update_configuration.png)


Via this form, you can change settings of an existing project: the [UNIGINE Engine build](#engine_build) used for the project, the version of the release application, the coordinates precision, and the [general settings](#general_settings). This option should also be used when you need to [upgrade](#upgrade_project) the existing project to the newest SDK version.


Moreover, you can restore the project's files that were corrupted, missed, or mistakenly modified. For this, you should leave settings in the form unchanged and press the **Update Configuration** button. In this case, the following files of the project will be restored (they will be copied from the SDK):


- Binaries
- `core.ung`, `editor.ung` and `scripts.ung`
- Launchers


> **Notice:** If some of the files listed above are changed, the `.modified` postfix is added to names of such files. At that, the files from the SDK will also be copied.
