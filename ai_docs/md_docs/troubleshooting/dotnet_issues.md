# .NET Issues


This section provides information on typical .NET related issues.


## .NET SDK Version


To develop a project using [C# Component System](../principles/component_system/component_system_cs/index.md), a developer (artist, designer, and any other person working with the project) should have .NET SDK 8 installed on their computer.


It is required to install the **SDK**, not the runtime, because SDK contains both the compiler, which compiles *.cs-components in UnigineEditor, and the runtime, which runs an already compiled application from UnigineEditor at the development stage.


### Do I Need to Install .NET on All PCs to Run the Final Build?


Running a final application built by UnigineEditor via the *[Build Tool](../editor2/projects/build_project.md)* **does not require** .NET SDK or .NET runtime. The output applications are self-contained and can be run flawlessly on almost any computer.


## Typical Errors


If you don't have .NET SDK installed, you can come across various errors while working with the project in both SDK Browser and UnigineEditor. For example, when running the application (clicking the *RUN* button) after creating it in SDK Browser, you may receive the error stating that *File Not Found � File *_x64.dll doesn't exist*:


![](file_not_found.png)

*File Not Found � File *_x64.dll doesn't exist*


Errors also can occur when clicking the **Play** button in UnigineEditor (*Required .NET SDK not found*):


![](dotnet_sdk_not_found.png)

*Required .NET SDK not found*


## Fixing Errors with Missing SDK


To fix any possible errors with missing .NET SDK, you need to download and install .NET SDK using the following link: *[https://dotnet.microsoft.com/en-us/download/dotnet/8.0](https://dotnet.microsoft.com/en-us/download/dotnet/8.0)*.


> **Warning:** After installing .NET SDK, restart UnigineEditor to have all the changes in the OS be implemented correctly. For Windows, it is also recommended to restart the PC to have the *%PATH%* variable updated.


### Installing .NET SDK on Windows


Install a version 8.0.x: *[https://dotnet.microsoft.com/en-us/download/dotnet/8.0](https://dotnet.microsoft.com/en-us/download/dotnet/8.0)*.


Download the required installer and run it following all installation steps.


**Optional**: After installing the SDK you might find it useful to [disable .NET SDK telemetry](https://docs.microsoft.com/en-us/dotnet/core/tools/telemetry).


### Installing .NET SDK on Linux


Install a .NET SDK version 8.0.x: *[https://docs.microsoft.com/en-us/dotnet/core/install/linux](https://docs.microsoft.com/en-us/dotnet/core/install/linux)*.


Linux operating systems supported by .NET include at least the following:


- Red Hat Enterprise Linux 7, 8
- CentOS 7, 8
- Fedora 32, 33
- Debian 9, 10
- Ubuntu 16.04, 18.04, 19.10, 20.04, 20.10
- openSUSE 15+
- SUSE Enterprise Linux (SLES) 12 SP2+, 15
- Alpine Linux 3.11+


.NET SDK can be installed on Linux in a number of ways. Please check the official website for installing .NET SDK [with Snap](https://docs.microsoft.com/en-us/dotnet/core/install/linux-snap) or [manually](https://docs.microsoft.com/en-us/dotnet/core/install/linux-scripted-manual).


After installing the SDK, you might find it useful to [disable .NET SDK telemetry](https://docs.microsoft.com/en-us/dotnet/core/tools/telemetry).


## Checking .NET SDK Version


You can check which .NET SDK Version (or versions) is installed on your PC.


### On Windows


1. Open the Command Prompt (Click the *Start* button and type **cmd**).
2. In the window that opens, type the following: ```bash dotnet --list-sdks ```


The following information should appear:


![](win_sdk_list.png)

*List of the SDKs installed on the PC*


### On Linux


1. Open the terminal.
2. In the window that opens, type the following: ```bash dotnet --list-sdks ```


The following information should appear:


![](linux_sdk_list.png)

*List of the SDKs installed on the PC*


In the output, all installed .NET SDK versions are listed. If you installed .NET SDK and it is not listed, address Microsoft support.


## Checking SDK Compatibility


When loading a C# Component System based project, UnigineEditor lists all found .NET versions in its log:


| ![](sdk_not_found.png) | .NET SDK is **not found**. |
|---|---|
| ![](wrong_sdk_found.png) | **Unsuitable versions** of .NET SDK are found. |
| ![](sdk_found.png) | Suitable .NET SDK version is found and C# Component System is initialized successfully. |


## Visual Studio Code Issues


### OmniSharp extension Error: spawn cmd ENOENT


In case IntelliSense cannot be started due to the **spawn cmd ENOENT** error in the OmniSharp extension, it is recommended to add `%WINDIR%\System32` to the *PATH* variable.


[![](omnisharp_path.png)](omnisharp_path.png)

*Editing thePATHvariable on Windows 10*


On Linux, you may require adding `~/.vscode/extensions` to the path, for example in the `.bashrc` file:
*export PATH=$HOME/.vscode/extensions:$PATH*


For more details see *[https://github.com/OmniSharp/omnisharp-vscode/issues/32](https://github.com/OmniSharp/omnisharp-vscode/issues/32)*.


### Project Opening Issues


In case a single source file of a C# component is opened in VS Code when double-clicking it in UnigineEditor, it is recommended to make sure the path to the VS Code bin (`%VSCODE_INSTALLATION_FOLDER%\bin`) folder is added to the *%PATH%* environment variable, for example, as follows: `C:\Program Files\Microsoft VS Code\bin`.


[![](vscode_path.png)](vscode_path.png)

*Editing thePATHvariable on Windows 10*


For Windows, it is also recommended to restart the PC to have the *%PATH%* variable updated.
