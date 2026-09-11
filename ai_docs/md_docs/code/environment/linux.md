# Linux Development Environment


> **Notice:** Supported OS versions: **Linux (kernel 4.19+) x64**.
> For hardware specifications, see [System Requirements](../../start/requirements.md#hardware).


To start working with the Unigine engine on the Linux platform you should install the UNIGINE SDK and additional software.


## Prepare the Environment for Linux


### Install UNIGINE SDK


- If you have a **UNIGINE SDK archive** downloaded at the [UNIGINE developer portal](https://developer.unigine.com/en/downloads):

  1. Extract the archive into a target directory.
  2. Run `browser.run` to launch [UNIGINE SDK Browser](../../sdk/index.md). The downloaded UNIGINE SDK will be available on the [SDKs](../../sdk/index.md#sdks) tab. > **Notice:** UNIGINE SDK Browser is required when using UnigineEditor or debug builds of the engine.
- If you have **[UNIGINE SDK Browser](../../sdk/index.md)** downloaded at the [UNIGINE developer portal](https://developer.unigine.com/en/downloads):

  1. Execute the browser.
  2. [Install](../../sdk/index.md#install_new_sdk) or [add installed](../../sdk/index.md#add_installed_sdk) UNIGINE SDK.


### Additional Software


- **GCC 8.3.0+** � a С++ compiler.
- **CMake 3.21+** � a tool that simplifies project building for different platforms.
- **.NET SDK** � required to develop projects using [C# Component System](../../principles/component_system/component_system_cs/index.md). See [here](../../troubleshooting/dotnet_issues.md#install_dotnet_sdk_linux) how to install **.NET SDK** and check its version.
- **ccache** (optional) � a tool that caches files compiled from C++ sources to avoid recompilation of previously compiled files.


To install all required Debian/Ubuntu packages, use the following:


```bash
sudo apt-get install linux-headers-3.16.0-4-all gcc g++ make ccache libgl1-mesa-dev libxrandr-dev libxinerama-dev libopenal1 libxrender-dev libxext-dev libc6-dev libx11-dev libxi-dev libxml2-dev dotnet-sdk-6.0 cmake
```


### Recommended IDEs


- For C# development � [Visual Studio Code](https://code.visualstudio.com/download), [Rider](https://www.jetbrains.com/rider/)
- For C++ development � [Visual Studio Code](https://code.visualstudio.com/download), [Qt Creator](https://www.qt.io/product/development-tools) (mostly used for Qt framework development, but also suitable for regular C++ projects)
