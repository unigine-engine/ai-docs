# SDK Browser 2 Changelog


This article contains a summary of changes between the official **SDK Browser 2** releases. The changelog lists releases by date and includes new features, bug fixes, and significant improvements.


The latest **SDK Browser 2** version can be downloaded [here](https://developer.unigine.com/en/downloads/sdk_browser_v2_start_here).


## Version 2.1.3


Release date: **2026-09-09**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.1.3:**


- Added support for **Cross-OS** projects, allowing the same project to be used safely on both Windows and Linux:

  - A project can be created on one operating system, transferred to another, and upgraded to Cross-OS mode in *SDK Browser*. The binaries required for the current platform are added, the project is marked as Cross-OS, and platform-specific files are tracked in the `*.project` file.
  - When a Cross-OS project is upgraded or reconfigured, only the files for the current operating system are updated, and you are notified if the project also has to be upgraded on the other platform.
  - Cross-OS support can be removed later, which converts the project back to a single-OS configuration. The standard single-OS workflow remains unchanged.
- Added the ability to rename projects. A project now has a separate **display name**, which matches the original project name by default and can be changed by double-clicking the project title or from the project card menu. The display name is stored in the `*.project` file only: the project name itself, its code structure and its identity stay untouched, so building and migration are not affected.
- Added proactive disk space checks for SDK installation and project creation. Available storage is monitored throughout downloading, extraction, installation and project creation: if the space runs low, you get a notification instead of a silent failure, and the current task is preserved whenever possible so that it can be resumed. Space requirements are now tracked separately for SDKs, demos, templates, documentation and projects.
- When you upgrade or delete an installed edition of a certain SDK version, *SDK Browser* now offers to remove the demo projects, samples and documentation that belong to that version. This helps to reclaim disk space and keeps obsolete content from being left behind.
- Redesigned the **template information** window: a larger and more flexible layout, improved version descriptions, clearer action buttons, and better handling of long content. Version details can now be expanded right in the version table, with *Download* and *Create Project* available in the expanded view. The *Download* and *Delete* actions now also reflect the state of the template, including separately downloaded templates, empty templates, and templates provided through an installed dependency SDK.
- Added the license expiration notifications, which are based on the **runtime** expiration date. Warnings escalate as the date approaches from a one-time message to a banner plus a message.
- Added the *$(Folder)* and *$(File)* placeholders for the arguments of a custom IDE, so that it opens the project instead of just starting up. They are substituted with the project folder and the IDE project file at launch.
- Added the new **Tools** tab, where UNIGINE tools can be downloaded directly from *SDK Browser*.
- Updated the list of plugins available for 2.22+ projects:

  - Added a new **Cesium** plugin.
  - Added a new **RTSPStreamer** plugin.
  - Added a new experimental **Scenario Manager** plugin.
  - The **MCPBridge** plugin, is now installed together with *AI Documentation* as a part of the **AI Toolkit**.
  - Plugin dependencies are now taken into account: for example, **Scenario Manager** requires **DataBridge**.
  - Plugins are installed into a project according to the directory structure.
- Added the ability to open source code of sample packs on GitHub.
- An installation already in progress can be canceled by clicking *Cancel* in the **SDKs** view.
- You can now open a storage location for any installed SDK right from the SDK card by choosing *Open Folder*.
- The **Visual Studio** is now used as default IDE for C++ templates.
- The Microprofile is now enabled by default for SDK 2.22.
- The **My Projects** tab is now opened on startup if there are any created projects.
- Improved sorting of SDK versions, which now takes pre-release, release, and patched versions into account.
- Platform-specific products now have a **for Windows** or **for Linux** suffix in their names.
- UI elements are now mirrored in the Arabic localization.
- Fixed freezes when downloading at a high speed and when renaming a project during a download.
- Fixed project migration between different SDKs having the same template version, and migration of template-based demos.
- Various bugfixes.

</details>


## Version 2.1.2


Release date: **2026-04-28**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.1.2:**


- Added support for Arabic language in the UI.
- Replaced the default project preview with an updated version.
- Fixed an issue where the world file name in projects created from a template was not consistently updated, resulting in incorrect references to the `.world` file in meta files after project creation.
- Various bugfixes.

</details>


## Version 2.1.1


Release date: **2026-04-09**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.1.1:**


- Added the ability to select the **Template Installation Path** for storing downloaded templates when creating a project (by default, templates are saved to the **Storage** path).
- Fixed text and window layout issues in the **Fixed License Activation** window and template cards on the **Templates** tab.
- Removed a duplicate window showing the result of license activation.
- Fixed an issue with refreshing template card previews on the **Templates** tab.
- Fixed inconsistent quoting in <Target> blocks for C# projects, preventing potential parser issues.
- Fixed a crash when deleting a non-Empty template via the UI in offline mode after it had been removed manually via File Explorer.
- Switching to an SDK version where the currently selected **Samples** category is not available now automatically redirects to an available *Samples* view.
- Fixed an issue preventing a return to default after selecting **Custom** in **Customize Code Options**.
- Fixed a crash on logout.
- Various bugfixes.

</details>


## Version 2.1.0


Release date: **2026-03-25**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.1.0:**


- Added support for the new template-based workflow for 2.21+ projects.
- Added copying of required files for the new experimental Animation System.
- Improved the **Private Support** link redirect; it now correctly processes all user categories and opens the corresponding sections of the website.
- Options for patching project files are now displayed according to the project configuration.
- Eliminated hangs caused by long response times, improving overall stability.
- Fixed an issue with copying source code files when creating a project based on the **ROS Vehicle** demo (via **Copy As Project**).
- Added an option to include Reference Documentation for AI Agents (**AI Documentation**) when creating a project (via **Create Project**) or later via the **Project Configuration** window.
- Added support for Qt 6�based projects.
- Updated the list of plugins available for 2.21+ projects: Incorrect links to plugins were also fixed.

  - Added a new **DataBridge** plugin.
  - Added a new **SQL** plugin.
  - Added a new **PDFRender** plugin.
  - Added a new **MediaPlayer** plugin.
- Various bugfixes.

</details>


## Version 2.0.30


Release date: **2026-03-05**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.0.30:**


- Samples are now marked with the corresponding label on the **My Projects** tab. These projects cannot be upgraded to a newer SDK version; you must download and install a new sample pack for the corresponding SDK version.
- Clicking **Open Code IDE** for **CMake** and **CMake + Qt** projects now opens the default IDE (Visual Studio Code).
- You can now type or paste the path to a project you want to import directly into the corresponding field of the **Import Project** window, without needing to select it via the file selection dialog.
- Fixed an issue where the scroll bar did not scale correctly with the text size in demo project descriptions.
- SDK Browser now waits for project configuration to complete before closing.
- Various bugfixes.

</details>


## Version 2.0.29


Release date: **2025-10-22**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.0.29:**


- Fixed an issue where the **.NET Host** process remained in memory for some time after shutting down the Browser; now, all related processes are terminated upon Browser shutdown.
- Reinstalling samples in offline mode is no longer supported, resolving an issue that caused all subsequent reinstall attempts to fail for the selected SDK.
- Interrupted SDK downloads will now resume automatically after restarting the SDK Browser and logging in.
- Added hot detection for USB-HASP keys; restarting SDK Browser is no longer required.
- Updated layout of the **Login** page for your convenience.
- Fixed an issue that caused frequent automatic logoffs due to session token expiration.
- The **Install** button is now disabled for the selected SDK version and edition while samples are being installed.
- Fixed issues with DPI scaling on Linux.
- Fixed an issue with the SDK Browser executable failing to run on Linux when located in a directory containing a space in its path.
- Added support for importing projects with the same ID but different file paths (e.g. copied via File Explorer).
- Various bugfixes.

</details>


## Version 2.0.28


Release date: **2025-09-22**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.0.28:**


- The project currently being created is now highlighted in the list view and displays a progress bar.
- Fixed an issue where clicking **CREATE NEW PROJECT** repeatedly in quick succession could trigger the simultaneous creation of multiple projects.
- Fixed an issue that occasionally caused the application to freeze during project upgrades.
- Fixed an issue where incorrect source paths for sample pack previews caused preview images to disappear after package installation.
- Added a scrollbar to the Release Notes window to resolve layout issues.
- Added missing plugins to the `.bat/.sh` files for the **IG** and **IG + VR** templates.
- Fixed an issue where the projects list appeared empty when switching to the list view during new project creation.
- Switching the **Template** in the **Create New Project** window no longer resets the values in the **API + IDE** and **Precision** fields, as long as the selected template supports them.
- Various bugfixes.

</details>


## Version 2.0.27


Release date: **2025-08-05**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.0.27:**


- Fixed an issue that caused the preview image for *CPP Samples* to disappear after installing the samples pack.
- Fixed issues that caused multiple console errors when rebuilding the *C# Component Samples* after installation, due to unresolved build configurations in the `*.csproj` file.
- Various bugfixes.

</details>


## Version 2.0.26


Release date: **2025-07-25**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.0.26:**


- Fixed an issue with the modality of the **Import SDK** file dialog, which caused crashes in certain cases.
- Added a dialog that allows you to choose an installation path for sample packages when clicking **INSTALL**.
- Fixed an issue with logging out during the samples installation process, causing all subsequent attempts to install samples to fail.
- Various bugfixes.

</details>


## Version 2.0.25


Release date: **2025-07-16**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.0.25:**


- Fixed SDK Browser to correctly rebuild sample projects in the standalone SDK build.

</details>


## Version 2.0.24


Release date: **2025-07-08**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.0.24:**


- Reorganized the sample library, moving **C++, C#, UnigineScript**, and **Third-Party Integration** samples to the dedicated tab to make it more structured and intuitive, added clear descriptions to each sample. This information is available even if the samples are not installed. For more details on samples reorganization please refer to the **UNIGINE 2.20** devlog.
- Upon clicking on the **Edit in IDE** button SDK Browser will open a `*.vcproj` in *Visual Studio* in case this file is found in the project directory; otherwise, the `CMakeLists.txt` file will be opened on Windows.
- Added information on SDK download size and disk space requirement to the **Add SDK** window.
- Added a project validation and repair feature enabling you to repair deleted projects in case their data was preserved (by selecting the **KEEP DATA** option), as well as projects having some or all of the binary files deleted. For such projects the corresponding message will appear on the project's card, simply click **Repair** and choose necessary configuration options.
- Added the **Patch Project Files** option to the **Upgrade Project** enabling you to make necessary amendments to `*.csproj` and VS Code project files (e.g., adding new sources) or C++ source files (e.g., adding include directives).
- Fixed an issue with saving Global Options on clicking **Apply** when no default SDK is selected.
- Fixed an issue with incorrect setting of startup-arguments when setting **Monitor** and **Stereo Modes** parameters in *Global Options*.
- Updated the list of plugins available for **SDK 2.20+** projects:

  - Added a new **GaussianSplatting** plugin to the list of plugins available for *Sim* and *Engineering* editions.
  - Removed the **TeslaSuit** plugin.
- The **Microprofile Enabled** option is now unchecked by default at running a project or opening it in UnigineEditor.
- Removed the unavailable **DirectX 11** graphics API option for **SDK 2.20+** projects.
- A progress bar will now be displayed on the Project's card on creating, configuring, upgrading, removing it, or performing a back-up operation.
- Required *Agility SDK* binaries are automatically added to new projects on creation, all related startup-arguments were updated for all **SDK 2.20** C# projects including demos.
- Fixed displaying large descriptions for samples.
- Various bugfixes.

</details>


## Version 2.0.23


Release date: **2025-02-12**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.0.23:**


- Fixed an issue with building C# projects in Visual Studio Code.
- Various bugfixes.

</details>


## Version 2.0.22


Release date: **2025-02-11**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.0.22:**


- Added country selection dropdown menu to the account creation form (*Create account*).
- Fixed an issue an unhidden password being displayed in the *Sign In* form after logging out.
- Fixed an issue with building demo-based projects (created via *Copy As Project*).
- Fixed an issue with updating *SDK Browser* resulting in repeated update failures after downloading a new version on Windows for some hardware configurations.
- Various bugfixes.

</details>


## Version 2.0.21


Release date: **2025-01-22**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.0.21:**


- Fixed an issue sometimes causing *SDK Browser* freezes when opening file dialogs and some popup windows (e.g., *Global Options, Create Project*) in case of having connection problems.
- Fixed an issue with clearing the preview image for an **SDK 2.18.1+** project after upgrading it.
- Fixed an issue with *Fixed* license activation, that caused *SDK Browser* to prompt the user to reactivate the license at each startup.
- Fixed an issue with saving *Customized Run Options* for a project via the *Remember* checkbox.
- Various bugfixes.

</details>


## Version 2.0.20


Release date: **2024-12-26**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.0.20:**


- Fixed an issue with shuffling of the list of projects displayed on the *Projects* tab, which resulted in a random order of projects after restarting the SDK Browser.
- Added the ability to set preferred login and download servers for the Content Delivery Network directly in the SDK Browser.
- When the developer server becomes unreachable, a special icon will appear in the bottom-right corner, informing you of a host availability issue without displaying the *Connection Problem* pop-up dialog. Once the developer server is back online, the icon will disappear.
- Added the ability to scroll through the list of available SDK versions.
- Fixed a crash when closing the *SDK Browser* while copying a demo project via *Copy As Project*.
- Various bugfixes.

</details>


## Version 2.0.19


Release date: **2024-12-10**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.0.19:**


- Email is now checked for uniqueness at the moment of submitting the first *Create Account* form. In case the specified email is already registered, the corresponding notification appears.
- Added a language selection option to the *Sign In* form.
- Fixed a crash at *SDK Browser* start-up on Windows due to missing WMI classes.
- Removed *Oculus* from the list of *Stereo 3D* options for 2.18+ projects.
- Removed a redundant *ADDITIONAL_PATH* placeholder from `.bat`-files generated at project creation.
- Binaries of the **SpiderVision** plugin are now automatically added to new projects created on the basis of the *IG* and *IG + VR* templates.
- Fixed an issue with adding and removing plugins that were selected or unselected via checkboxes in the *Plugins* window on project creation.
- Various bugfixes.

</details>


## Version 2.0.18


Release date: **2024-11-25**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.0.18:**


- You can now create a new user account giving you access to UNIGINE services via SDK Browser without visiting the website.
- Updating SDK Browser now automatically updates required Microsoft Visual C++ Redistributable packages. In case of detecting an incompatible Microsoft Visual C++ Redistributable package version a corresponding message will be displayed.
- Fixed a performance drop when building C# projects with the Development binaries.
- Fixed an issue with adding an existing SDK from a local storage via *Add SDK -> Add the already installed* (*SDKs* tab) on Linux OS.
- Fixed freezes during SDK Browser startup in case of network connection issues.
- Added a missing `matlab_ros_sample.m` file to the target project folder when creating a project based on the *ROS Vehicle* demo (via *Copy As Project*).
- Fixed an issue with copying *libcurl* binaries when creating a project based on the *CIGI* demo (via *Copy As Project*).
- Fixed an issue with resetting executable flag (**+x**) for executable included in the SDK.
- Fixed an issue with opening a pre-installed version of offline documentation.
- Dedicated engine debug binaries are now automatically added for each new created project (Linux).
- Renamed **UsdExporter** plugin as **UsdExchanger**.
- Various bugfixes.

</details>


## Version 2.0.17


Release date: **2024-08-14**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.0.17:**


- Various bugfixes.

</details>


## Version 2.0.16


Release date: **2024-08-12**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.0.16:**


- Updated the list of plugins available for 2.19+ projects:

  - Added a new ***SpiderVision*** plugin to replace old ***Wall*** and ***Projection*** plugins.
  - Added a new ***UsdExporter*** plugin.
  - Added a new ***WebStream*** plugin.
  - Renamed ***SVN*** plugin as ***VSC Integration***.
- The ***Geodetics*** plugin is now added by default to all *Engineering* and *Sim* projects. The corresponding option was removed from the list of plugins.
- Added *Varjo* option to the list of *Stereo 3D* modes for the *Auto* API option.
- Added a new *OpenXR* option to the list of *Stereo 3D* modes.
- Removed *Cmake + Qt* option from the *API + IDE* list for *Сommunity* and *Сommunity Pro* SDK editions.
- Removed *OpenGL* API option for 2.19+ projects.
- Updated *.NET* version installer to 8.0 for 2.19+ projects.
- Various bugfixes.

</details>


## Version 2.0.15


Release date: **2024-04-16**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.0.15:**


- Fixed an issue with setting the default UI language.
- Various bugfixes.

</details>


## Version 2.0.14


Release date: **2024-04-15**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.0.14:**


- Fixed a crash on running an application with an invalid value of the `-main_window_size` parameter.
- Fixed an issue with copying IG Host binaries when creating a project based on the CIGI demo (via *Copy As Project*).
- Fixed an issue with rearranging the list of files in the `*.project` file on reimporting a project.
- Added a possibility to create a C++ Qt-based project from the C++ VR Sample via the *Copy As Project* button.
- SDK Browser UI is now available in English, Chinese, German, French, and Russian.
- Various bugfixes.

</details>


## Version 2.0.13


Release date: **2024-02-09**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.0.13:**


- Improved performance of file copying operations (*Copy As Project*).
- Removed Oculus and Varjo from the list of Stereo 3D options on Linux.
- Fixed an issue with multiple *Connection Problem* popup-windows opened repeatedly in case of unavailable network connection.
- Fixed an issue with incorrect user name and avatаr layout.
- Various bugfixes.

</details>


## Version 2.0.12


Release date: **2023-12-13**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.0.12:**


- Added a new **Plugin Vendor** field for projects created on the basis of the *Editor Plugin Template* and added necessary control variables to related `CMakeFiles.txt` to ensure proper naming and location of the target plugin binaries.
- Fixed an issue with unavailable **Edit in IDE** button in *3rd Party Samples* on Linux.
- Removed *VREditorPlugin* for 2.18+ projects including upgraded ones.
- Changed VR-related startup arguments for 2.18+ projects: the new **-vr_app** argument is used to work with VR for all graphic API's except for OpenGL, deprecated VR plugins are used for OpenGL API.
- Updated the list of plugins available for 2.18+ projects.
- Fixed issues with upgrading of 2.15.1 and earlier projects that used old plugins naming convention (unchecked options in the *Plugins* list).
- Added a new **C++(CMake)** option for creation of projects from C++ demos via the *Copy As Project* button.
- Unnecessary files (`*.filter, *.makefile`, etc.) are no longer generated on copying a demo as project (*Copy As Project* button).
- Added an ability to copy C++ demos as projects with C# API making it possible to use demo content in a C# project (C++ logic of the demo is unavailable).
- Fixed an issue with creating a new icons in system tray each time SDK Browser is launched.
- Fixed an issue with building single-precision Editor plugins for double-precision projects.
- Unified storage paths for downloaded offline docs and the ones included into standalone SDK versions.
- Various bugfixes.

</details>


## Version 2.0.11


Release date: **2023-07-03**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.0.11:**


- Fixed an issue with the unavailable **Copy As Project** function for *Demo* projects.
- Other bugfixes.

</details>


## Version 2.0.10


Release date: **2023-06-30**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.0.10:**


- Resolved an issue that prevented the upgrade of projects using the Editor plugins template to version 2.17.
- Fixed the creation of an empty folder when creating projects with the Editor plugins template.
- Other bugfixes.

</details>


## Version 2.0.9


Release date: **2023-06-29**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.0.9:**


- Fixed a crash on upgrading projects to 2.17.
- Fixed an issue with availability of the IG + VR project template.
- Added a missing VREditorPlugin for new projects based on VR+IG Template.
- New project's folder shall no longer contain shader cache for graphics APIs unavailable for selected platform.
- Other bugfixes.

</details>


## Version 2.0.8


Release date: **2023-06-21**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.0.8:**


- Improved SDK Browser logging including info on project parameters; downloading sources and destinations; deletion of project, demo, and SDK files; insufficient disk space.
- Added **VR + IG** template combining the previously available *VR* and *IG* templates.
- Added the possibility to copy **VR Sample C++ (Qt-based)** as a project.
- Rearranged the plugin structure and naming approach.
- Implemented adding *SVN Plugin* to the project at its creation.
- Renamed binaries of demo and sample projects.
- Renamed *Assets* to *Add-Ons* and changed the approach to downloading and adding packages from *Add-On Store*: add-ons are downloaded from the website and added to the project via Editor.
- Fixed the issue with *SDK Browser* running outside the screen.
- Fixed the issue with a failure to download *Varjo* libraries.
- Other bugfixes.

</details>


## Version 2.0.7


Release date: **2022-12-21**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.0.7:**


- All required **VREditorPlugin** binaries are automatically added to new C++/C# projects created on the basis of the **VR Template**.
- Various bugfixes.

</details>


## Version 2.0.6


Release date: **2022-12-21**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.0.6:**


- Increased offline operation period up to 24 hours.
- Added automatic cleanup of the `updates` folder on successful *SDK Browser* update.
- Improved *SDK Browser* logging including API requests and error codes, download and installation processes, creation and reconfiguration of projects, project/demo/SDK removal as well as other operations.
- Added automatic cleanup of *SDK Browser* logs, keeping only the last 3 of them.
- Downloading state is now saved in case *SDK Browser* is closed during the operation, upon the subsequent startup the interrupted downloading process will resume automatically.
- Fixed an issue with ignoring the **-system_script** startup argument.
- Additional plugins specified via the Customize UnigineEditor window are now added to the list of the standard ones instead of replacing them when running the Editor.
- Fixed an issue with the license server, when executing *SDK Browser* via vglrun (VirtualGL).
- Updated the list of script files and added licensing information for the ROS2 demo.
- Fixed an issue with creating *SDK Browser* windows out of the available screen.
- Restored necessary startup command-line arguments in launch scripts generated when creating a new project.
- In case there's no suitable SDK version found for reconfiguring an existing project, the corresponding warning message will be displayed. Downloaded Assets will not be available for non-suitable SDK versions.
- Fixed an issue with always running the Editor with Microprofile enabled regardless of the state of the corresponding checkbox.
- Fixed an issue with paths to plugins becoming invalid in case of non-standard naming of the SDK installation directory (e.g. created by the previous version of the *SDK Browser*).
- Fixed an issue with accidental removal of shader compiler libraries after reconfiguring a project.
- Fixed an issue with the contents of the Samples section becoming unavailable in the *SDK Browser* (subsections are grayed and non-clickable) in case the storage path contains chinese, cyrillic, or arabic symbols.
- In case there are no execution rights for the SDK installation directory (which is required to launch **ung_x64** during the project creation) the corresponding warning-message will be displayed.
- Fixed an issue with resetting start-up parameters (*Customize Run*) to defaults after making changes to project configuration.
- Various bugfixes.

</details>


## Version 2.0.5


Release date: **2022-10-14**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.0.5:**


- Improved event logging for the browser.
- Fixed an issue with shifting user name and avatar on the top *SDK Browser* panel when switching the Default SDK in case the window size is minimized.
- Fixed an issue with incorrect displaying of an Asset(Add-On) preview image in the assets management window of the project.
- Fixed an issue with asset availability checks in accordance with SDK version.
- Added the `system_dialog_00` sample to the list of UnigineScript system samples.
- Fixed an issue with resetting start-up parameters (*Customize Run*) to defaults after making changes to project configuration.
- Special symbols in passwords are now processed normally without breaking the authorization process.
- Various bugfixes.

</details>


## Version 2.0.4


Release date: **2022-10-10**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.0.4:**


- Fixed an issue with an attempt to launch UnigineEditor in fullscreen mode.
- Fixed an issue with an attempt to run the removed *Interface* plugin when opening *Interface* samples for Unigine Script via the *SDK Browser*.
- A required **libdxcompiler.so.3.7 / dxcompiler.dll** library is now added to the project directory on its creation.
- A required **libopenvr_api.so** library is now added to the project directory when a new VR project is created on Linux.
- A required **LeapC.dll** library is now added to the project directory when a new project based on Ultraleap functionality is created.
- Fixed issues with adding content from multiple selected assets(add-ons) to the project.
- Various bugfixes.

</details>


## Version 2.0.3


Release date: **2022-09-27**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.0.3:**


- Updated fullscreen and resolution settings in Global Options (SDK versions 2.16+).
- A path to the `.project` file is now used instead of the project directory eliminating issues with manual renaming and cloning of existing projects.
- Images for assets and demos are now displayed correctly.
- Updated .NET installer to version 6.0.
- Added automatic migration for user `main.csproj` files in C# projects to .NET 6.
- Beta SDK versions are now sorted correctly in the dropdown list.
- The *Offscreen* option as well Vulkan and DirectX 12 graphic APIs (General Options) are now displayed only for projects based on SDK versions 2.16+.
- SDK Browser shall only load plugins after checking their availability for the current SDK Edition.
- Filtered out property files related to C# components when creating a C++ project using the **Docs Sample Content** assets pack.
- Current Default SDK version in *SDK Browser* is now taken into account when opening an asset from the *Asset Store* via the **Open in SDK Browser** button.
- Various bugfixes.

</details>


## Version 2.0.2


Release date: **2022-08-10**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.0.2:**


- Added Ultraleap plugin to the list of available plugins displayed when creating/updating Unigine projects.
- Added precision selection for Community projects (SDK versions 2.16+).
- Replaced Visual C++ Redistributable for Visual Studio 2017 with Visual C++ Redistributable 2015-2022.
- Fixed an issue with incorrect detection of SDK version for Experimental and Custom builds.
- Updated names for former *App** plugins in the list of available plugins displayed when creating/updating Unigine projects(SDK versions 2.16+).
- Added Vulkan and DirectX 12 to the list of graphics APIs in the *Global Options* window.
- Various bugfixes.

</details>


## Version 2.0.1


Release date: **2022-07-07**


<details>
<summary>View Main Changes | Close</summary>

**Main changes in 2.0.1:**


- *Asset Store* integration.

</details>


## Version 2.0.0


The first release of SDK Browser 2.


Release date: **2022-06-09**
