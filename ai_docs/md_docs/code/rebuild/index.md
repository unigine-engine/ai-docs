# Rebuilding the Engine Plugins and Samples


Such UNIGINE Engine components as samples and plugins available in the `<SDK>/source` folder may be customized. If customized, they may be rebuilt using either of the following:


- [Visual Studio](#build_vs)
- [CMake](#build_cmake)


## Third-Party Libraries


If a plugin is built using third-party libraries, such libraries must be installed on your system to rebuild it successfully.


To ensure they are found, update the paths and/or versions of these libraries in **either** of the following:


- *UNIGINE_3RDPARTY_DIR* environment variable (suitable for both cases)
- Dedicated file in the `<SDK>/source/cmake/modules` folder (if building with CMake) For example, for rebuilding the Steam plugin on CMake, you can edit `<SDK>/source/cmake/modules/FindExternSteam.cmake`.


The [third-party library](../../third_party.md) version must match the one used in UNIGINE; otherwise, unexpected results may occur.


## Rebuild in Visual Studio


To rebuild a plugin or sample with **Microsoft Visual Studio**, do the following:


- Open the VS project file (`*.vcxproj`) for the plugin you want to rebuild. All plugins are located in `<UNIGINE_SDK>/source/plugins`.
- Specify the solution configuration: *Debug*, *Debug-Double*, *Release* or *Release-Double*. ![](configuration_p.png)
- Choose *Build -> Build Solution* in the menu or press **Ctrl + Shift + B**. ![](build_p.png)


## Rebuild in CMake


To rebuild a plugin or sample with **CMake**, do the following:


1. Open the folder that stores the source of the plugin or sample you want to rebuild.
2. Configure the project. Run: ```text cmake -H. -B build_folder ``` where `build_folder` is the arbitrary name of the supplementary folder that will store all build-related files.
3. To rebuild a plugin, run: ```xml cmake --build build_folder ``` The rebuilt binaries will be stored in the same folder, where the initial binaries were.
