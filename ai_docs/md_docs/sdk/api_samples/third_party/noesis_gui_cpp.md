# NoesisGUI Sample (CPP)


## General Information


***NoesisGUI*** (*[https://www.noesisengine.com/](https://www.noesisengine.com/)*) is a lightweight high-performance cross-platform UI framework based on Microsoft's **XAML** technology. It renders WPF/XAML interfaces - styles, templates, data binding, animations, and vector graphics - on top of a game engine's renderer.


It follows the **MVVM** architecture: the interface is authored in XAML separately from the application code and is connected to the application data through a view model.


The sample integrates ***NoesisGUI*** with UNIGINE: it implements a custom Noesis render device on top of the UNIGINE rendering API and displays XAML both as screen-space overlays and as a GUI mapped onto a 3D surface in the world. The interface is wired to the application through a data context that all the XAML views share: the application puts values into it by key, XAML reads them through {Binding [key]} expressions and writes them back, and the application logic is notified of every change.


![](noesis.png)

*Two screen-space overlays and a XAML interface mapped onto a 3D surface.*


The sample is available for both **C++** and **C#**. Both versions look and behave the same and use the same XAML files; they differ only in the way the GUI panel in the 3D world is implemented - see [C++ and C# Implementations](#noesis_differences).


## How to Run the Sample


The sample supports the following rendering backends:


- **Windows** - *Direct3D 12* or *Vulkan*. The *Direct3D 12* backend loads the **D3D12 Agility SDK** redistributable from the `bin/D3D12/` folder next to the executable.
- **Linux** - *Vulkan* only.


### Prerequisites


- **UNIGINE SDK Browser** (latest version)
- **UNIGINE SDK**
- **Visual Studio 2022** (Windows) or **GCC**/**Clang** (Linux)
- **CMake** 3.19 or newer (Visual Studio 2022 ships with a suitable version)
- **GitHub access** to clone the repository.


### Third-Party Dependency


The C++ sample uses the ***NoesisGUI*** SDK version 3.2.13. The SDK is **not** bundled with the sample: download it from the *[official site](https://www.noesisengine.com/developers/downloads.php)* and unpack it into the `source/NoesisSDK/` folder of the project, where `source/cmake/modules/FindNoesisGUI.cmake` looks for it.


The SDK folder structure must be kept unchanged - the sample expects the following files:


| File | Description |
|---|---|
| `Include/` | Header files of the SDK. |
| `Lib/windows_x86_64/Noesis.lib` | Import library used at link time. **Windows only**: on Linux the application links against the shared library directly, so the `Lib/` folder is not used. |
| `Bin/windows_x86_64/Noesis.dll` `Bin/linux_x86_64/libNoesis.so` | Runtime library for the corresponding platform. The build copies it next to the application, into the project's `bin/` folder. |


> **Notice:** If the SDK is not found, CMake does not fail: it prints a NoesisGUI SDK not found message and skips the sample target.


The vendored ***NoesisGUI*** *App framework* interactivity sources are shipped in `source/Src/Packages/App/Interactivity/` and are compiled into the sample. They register the components that the sample's XAML addresses through the NoesisGUIExtensions namespace, such as noesis:SetFocusAction in `data/ui/overlay.xaml`. The namespace is declared there as a *.NET* one because the Blend/WPF design-time tools expect that form, but no such assembly is loaded at run time.


### Step-by-Step Guide


Starting the ***NoesisGUI*** C++ sample requires you to perform the following steps:


1. Clone or download the sample from the *[UNIGINE Git repository](https://github.com/unigine-engine/unigine-noesis-cpp-integration-sample)*.
2. Make the ***NoesisGUI*** SDK available to the project, as described in the [Third-Party Dependency](#noesis_dependency_cpp) section above.
3. Open SDK Browser and make sure you have the latest version.
4. Add the sample project to SDK Browser:

  - Go to the *My Projects* tab.
  - Click *Add Existing* then select the `*.project` file located in the cloned sample folder corresponding to your setup (OS, SDK edition, and precision), and click *Import Project*. ![](photon/add_project.png)
5. Repair the project.

  - After importing, you'll see a **Repair** warning - this is expected, as only essential files are stored in the Git repository. SDK Browser will restore the rest. ![](repair_project.png)
  - Click *Repair* to let SDK Browser restore the required files.
  - When the configuration window opens, click *Configure Project*.
6. Open the project in your IDE. > **Notice:** On Linux the project is configured and built with CMake from the command line - see [Building and Running on Linux](#noesis_linux_cpp). > **Warning:** By default, the project uses **single precision (float)**. If you need **double precision** coordinates (see [Double Precision Coordinates](../../../code/double_precision/index.md)), open the `source/CMakeLists.txt` file and change the following line: > > > ```text > set(UNIGINE_DOUBLE False CACHE BOOL "Double coords") > ``` > >  to > ```text > set(UNIGINE_DOUBLE True CACHE BOOL "Double coords") > ``` > > > Make sure this setting matches the `.project` file you selected (e.g., `*_double.project` for double precision builds).

  - Launch the recommended Visual Studio 2022 (other C++ IDE with CMake support can be used as well) and open the folder containing the `source/CMakeLists.txt` file.
  - If everything is set up correctly, the `CMakeLists.txt` file will be highlighted in **bold** in the *Solution Explorer* window, indicating that the project is ready to build.
7. **Build** and **Run** the project. > **Notice:** Visual Studio starts the executable without any command-line arguments, so the world has to be loaded explicitly: add -console_command "world_load noesis_sample" to the debug arguments of the target, or start the project from SDK Browser, which uses the world specified in the `.project` file. You can also start the executable from the project's `bin` folder: ```text unigine-noesis-cpp-integration-sample_double_x64.exe -console_command "world_load noesis_sample" ``` The name of the executable ends with the suffix of the configuration you have built: _double_x64 or _x64 for the release configurations, _double_x64d or _x64d for the debug ones.

  - Click **Build** to compile the project and then **Run** to launch the application.


If you're still having trouble running the application, revisit the steps above to ensure nothing was skipped, and check the following:


- The ***NoesisGUI*** SDK 3.2.13 is unpacked into the `source/NoesisSDK/` folder, and `Noesis.dll` / `libNoesis.so` ended up in the `bin/` folder next to the executable.
- On Windows with the *Direct3D 12* backend, the **D3D12 Agility SDK** redistributable is present in `bin/D3D12/`.
- The CMake variable UNIGINE_DOUBLE matches the precision of the selected `.project` file.
- You're using the correct `.project` file for your installed SDK edition and platform (Windows/Linux).
- Your SDK version is not older than the version specified for the project.


If you encounter CMake issues in Visual Studio, try rebuilding the project by right-clicking on it in the Visual Studio 2022, selecting **Delete Cache and Reconfigure** and then **Build** again.


### Building and Running on Linux


On Linux, the project is configured and built with CMake from the command line (you can also open the `source/CMakeLists.txt` file in any IDE with CMake support). Everything in the [Step-by-Step Guide](#noesis_cpp) above up to [opening the project in an IDE](#noesis_cpp_step_ide) - cloning the sample, providing the ***NoesisGUI*** SDK, importing the project into SDK Browser and repairing it - is exactly the same, just select a `*_lin_*` `.project` file.


1. Configure and build the project. Run the following commands from the project's `source` folder - this builds a release version with double precision: ```bash cmake -B build -DCMAKE_BUILD_TYPE=Release -DUNIGINE_DOUBLE=True cmake --build build -j ``` The build type and the precision are set independently: use -DCMAKE_BUILD_TYPE=Debug for a debug build, and -DUNIGINE_DOUBLE=False for single precision (float). > **Warning:** Precision must match the `.project` file you have selected - see [the details in the guide above](#noesis_cpp_precision). > > > Note that the project removes UNIGINE_DOUBLE from the CMake cache at the end of the configuration step, so the option does not persist between runs - pass it explicitly every time you reconfigure the project. Alternatively, you can change its default value directly in the `source/CMakeLists.txt` file.
2. Check the resulting binary. It is placed in the project's `bin/` folder, next to the engine libraries, and is named after the build options you have chosen:

  - `unigine-noesis-cpp-integration-sample_double_x64` - release, double precision
  - `unigine-noesis-cpp-integration-sample_x64` - release, single precision (float)
  - `unigine-noesis-cpp-integration-sample_double_x64d` - debug, double precision
  - `unigine-noesis-cpp-integration-sample_x64d` - debug, single precision (float)
3. Run the application from the console on *Vulkan* - the engine has no *Direct3D 12* backend on Linux. The command below is an **example** for a release build with double precision, started from the project's `bin` folder: ```bash cd ../bin export LD_LIBRARY_PATH="$PWD:$LD_LIBRARY_PATH" ./unigine-noesis-cpp-integration-sample_double_x64 \ -video_app vulkan -sound_app openal \ -console_command "world_load noesis_sample" ``` Substitute the binary name for the configuration you have built.


If the application fails to start, check that LD_LIBRARY_PATH contains the project's `bin/` folder and that you passed -video_app vulkan.


## What the Sample Contains


The sample loads `data/noesis_sample.world`, which holds only a ground plane, a world light and a spectator camera. The interfaces are created at run time by *main.cpp* from the XAML files in `data/ui/`, and all of them share one data context and the `ui/themes/noesis/NoesisTheme.DarkBlue.xaml` theme:


| Interface | XAML file | What you see |
|---|---|---|
| Screen-space view in a rectangle | `ui/overlay.xaml` | The *NEW GAME* and *SETTINGS* buttons in a 500x300 rectangle in the upper left corner. |
| Full-window screen-space view | `ui/text_font.xaml` | The *Font* and *Size* combo boxes with a sample text in the lower left corner. The chosen font family goes into the data context and comes back to the text - the two-way binding of the sample. |
| GUI mapped onto a 3D surface | `ui/world.xaml` | A 2x2 m panel with a resolution of 1024x1024, tilted in front of the camera. Its sliders and the color list control the DropShadowEffect of the drawn cloud - a purely ***NoesisGUI*** effect inside the interface. |


The interfaces get the mouse only while it is not grabbed for camera control. The panel in the world is picked by a ray limited to the control distance set for it - 5 m in this sample, so if its sliders do not react, move the camera closer.


The integration itself lives in `source/`: NoesisIntegration owns the lifetime of ***NoesisGUI*** and forwards input, NoesisRenderDevice is the render device implementation itself, NoesisProviders loads XAML, textures and fonts through the UNIGINE file system, and *ObjectNoesisGui* is the panel in the 3D world - see [C++ and C# Implementations](#noesis_differences).


## C++ and C# Implementations


Both versions share most of the integration: the custom Noesis render device, the screen-space views rendered straight into the viewport from the EventFuncBeginRenderGui callback of the application window, and the data context implementing INotifyPropertyChanged along with a key-based indexer - so the same XAML files work unchanged in both.


The GUI panel placed in the 3D world is the only substantial difference: ObjectExternBase cannot be inherited from managed code, so in C# the panel is assembled from regular engine objects instead of being a custom node.


|  | C++ | C# |
|---|---|---|
| Panel node | Custom node: ObjectNoesisGui inherited from ObjectExternBase and registered by its class ID, with its own surface and bounding volumes | Managed NoesisGuiObject class owning an ordinary ObjectMeshDynamic quad |
| Off-screen rendering of the view | Performed by the node itself in the ambient render pass | Performed in the same GUI callback that draws the screen-space views |
| Displaying the texture | The node draws a quad itself, setting the blending and depth states manually | The quad samples the render target texture through its material, so the panel lags one frame behind |
| Material | `noesis/materials/noesis_gui_object.basemat` | `noesis/materials/noesis_gui_mesh.basemat` |
| Mouse picking | The node's getIntersection implementation, i.e. the standard engine object interface | Ray-quad intersection implemented as ordinary math in C# |


## Fonts


The sample installs its own Noesis font provider, so the **only** fonts available in XAML are the ones shipped with the sample in `data/ui/` - no font installed in the system is reachable. At startup the sample registers the following font files, one call per face (a single style of a font family):


- `ui/fonts/Muli-Regular.ttf` - the Muli family
- `ui/fonts/CourierPrime-Regular.ttf` - the Courier Prime family
- `ui/fonts/Caladea-Regular.ttf` - the Caladea family
- `ui/themes/noesis/Fonts/PT Root UI_Regular.otf` and `ui/themes/noesis/Fonts/PT Root UI_Bold.otf` - the regular and the bold face of the PT Root UI family


Each face is registered together with the folder it is stored in, so a FontFamily value resolves only if it addresses the family through that folder. The path is specified relative to the referencing XAML file - e.g. Fonts/#PT Root UI in the XAML files inside `data/ui/themes/noesis/` - or relative to the data root if the value has no XAML context, that is, comes from a binding or from the font fallback list - e.g. ui/fonts/#Muli.


That is why *main.cpp* points the fallback chain at one of the bundled faces - ui/themes/noesis/Fonts/#PT Root UI. Naming a system family such as *Arial* there works on Windows only, where Noesis resolves it through *DirectWrite*; on Linux every character is rendered as a .notdef box.
