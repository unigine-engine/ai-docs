# Windows Development Environment


> **Notice:** Supported OS versions: **Windows 10/11 x64**.
> For hardware specifications, see [System Requirements](../../start/requirements.md#hardware).


To start working with the Unigine engine on the Windows platform you should install the UNIGINE SDK and additional software.


## Prepare the Environment for Windows


### Install UNIGINE SDK


There are two ways to install SDK:


- If you have a **UNIGINE SDK archive** downloaded at the [UNIGINE developer portal](https://developer.unigine.com/en/downloads):

  1. Extract the archive into a target directory.
  2. Run `browser.exe` to launch [UNIGINE SDK Browser](../../sdk/index.md). The downloaded UNIGINE SDK will be available on the [SDKs](../../sdk/index.md#sdks) tab. > **Notice:** UNIGINE SDK Browser is required when using UnigineEditor or debug builds of the engine.
- If you have [**UNIGINE SDK Browser**](../../sdk/index.md) downloaded at the [UNIGINE developer portal](https://developer.unigine.com/en/downloads):

  1. Install the browser.
  2. [Install](../../sdk/index.md#install_new_sdk) or [add installed](../../sdk/index.md#add_installed_sdk) UNIGINE SDK.


### Additional Software


To start your project with UNIGINE SDK you need to install the required software to prepare the development environment:


1. **IDE** � we recommend using [Microsoft Visual Studio 2022](http://www.microsoft.com/) (C#/C++), [Visual Studio Code](https://code.visualstudio.com/download) (C#/C++), [Rider](https://www.jetbrains.com/rider/) (C#), [Qt Creator](https://www.qt.io/product/development-tools) (mostly used for Qt framework development, but also suitable for regular C++ projects).
2. **CMake 3.21+** or higher (can be [downloaded for free](http://www.cmake.org/)). CMake is a tool that simplifies project building for different platforms.
3. **.NET SDK** (can be [downloaded for free](https://dotnet.microsoft.com/en-us/download/dotnet/8.0)). It is required to develop projects using [C# Component System](../../principles/component_system/component_system_cs/index.md). See [here](../../troubleshooting/dotnet_issues.md#install_dotnet_sdk_windows) how to install **.NET SDK** and check its version.
