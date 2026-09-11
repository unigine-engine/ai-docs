# NoesisGUI Sample (CS)


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
- **.NET 8 SDK**
- **Visual Studio 2022** on Windows. On Linux the `dotnet` CLI is enough, optionally with *[VS Code](https://code.visualstudio.com/download)* or *[Rider](https://www.jetbrains.com/rider/)*.
- **GitHub access** to clone the repository.


### Third-Party Dependency


The C# sample uses the managed ***NoesisGUI*** C# binding - two NuGet packages, both of version 3.2.13:


- **Noesis.GUI** (*[nuget.org](https://www.nuget.org/packages/Noesis.GUI/)*) - the runtime binding itself: the Noesis namespace with GUI, View, Renderer, RenderDevice and the providers. It also carries the native ***NoesisGUI*** library for every platform under `runtimes/<rid>/native/` (`win-x64/Noesis.dll`, `linux-x64/libNoesis.so`).
- **Noesis.App** (*[nuget.org](https://www.nuget.org/packages/Noesis.App/)*) - the *App framework* interactivity package. The sample registers its NoesisApp.Interaction types at startup, so the i: and ei: event triggers used in `data/ui/overlay.xaml` work.


Neither package is bundled with the repository: both are restored automatically from nuget.org via the PackageReference entries in the `.csproj` file. The build copies the managed `Noesis.GUI.dll` and `Noesis.App.dll` next to the application in `bin/` and the native libraries into `bin/runtimes/<rid>/native/`, with the one for your platform placed next to the executable as well - nothing has to be copied by hand.


> **Notice:** Do **not** use **Noesis.GUI.Extensions** - it contains only the Blend/WPF design-time helpers, not the runtime binding. Its NoesisGUIExtensions namespace is declared in the sample's XAML because the design-time tools expect that form, while at run time the types addressed through it - such as noesis:SetFocusAction - come from **Noesis.App**.


### Step-by-Step Guide


Starting the ***NoesisGUI*** C# sample requires you to perform the following steps:


1. Clone or download the sample from the *[UNIGINE Git repository](https://github.com/unigine-engine/unigine-noesis-csharp-integration-sample)*.
2. Open SDK Browser and make sure you have the latest version.
3. Add the sample project to SDK Browser:

  - Go to the *My Projects* tab.
  - Click *Add Existing* then select the `*.project` file located in the cloned sample folder corresponding to your setup (OS, SDK edition, and precision), and click *Import Project*. ![](photon/add_project.png)
4. Repair the project.

  - After importing, you'll see a **Repair** warning - this is expected, as only essential files are stored in the Git repository. SDK Browser will restore the rest. ![](repair_project.png)
  - Click *Repair* to let SDK Browser restore the required files.
  - When the configuration window opens, click *Configure Project*.
5. **Build** the project. On the first build, NuGet restores both ***NoesisGUI*** packages automatically, so an internet connection is required the first time. > **Warning:** Precision of the coordinates (see [Double Precision Coordinates](../../../code/double_precision/index.md)) must match the `.project` file you have selected. It is defined by the **build configuration**: use Release-Double / Debug-Double for a `*_double.project` file, and Release / Debug for a `*_float.project` one. The -Double configurations define UNIGINE_DOUBLE and link the `*_double_*` engine binding. Either way the binaries land in the project's `bin/` folder, next to the engine libraries.

  - **Windows**: open the `unigine-noesis-csharp-integration-sample.sln` file in Visual Studio 2022 and build the project.
  - **Linux**: Visual Studio is not available there, so the project is built with the `dotnet` CLI - see [Building and Running on Linux](#noesis_linux_cs).
6. **Run** the application.

  - **Windows**: press **Run** in Visual Studio - the main profile from `Properties/launchSettings.json` passes the startup arguments and loads the noesis_sample world. You can also start the executable from the project's `bin` folder: ```text unigine-noesis-csharp-integration-sample_double_x64.exe -console_command "world_load noesis_sample" ``` The name of the executable ends with the suffix of the configuration you have built: _double_x64 or _x64 for the release configurations, _double_x64d or _x64d for the debug ones.
  - **Linux**: the application is started through `dotnet` on the *Vulkan* backend - see [Building and Running on Linux](#noesis_linux_cs).


If you're still having trouble running the application, revisit the steps above to ensure nothing was skipped, and check the following:


- The **Noesis.GUI** and **Noesis.App** 3.2.13 NuGet packages have been restored successfully (an internet connection is required the first time), and the build produced `bin/Noesis.GUI.dll` and `bin/Noesis.App.dll` along with the native runtime in `bin/runtimes/<rid>/native/`.
- There is no native `Noesis.dll` / `libNoesis.so` from another ***NoesisGUI*** version lying directly in `bin/` - it takes precedence over the one from the package and makes Noesis fail at initialization.
- On Windows with the *Direct3D 12* backend, the **D3D12 Agility SDK** redistributable is present in `bin/D3D12/`.
- The build **configuration** matches the precision of the selected `.project` file (*-Double for double precision, plain ones for float).
- You're using the correct `.project` file for your installed SDK edition and platform (Windows/Linux).
- Your SDK version is not older than the version specified for the project.


### Building and Running on Linux


On Linux, the project is built with the `dotnet` CLI (you can also open the `.csproj` file in VS Code or Rider). Everything in the [Step-by-Step Guide](#noesis_cs) above up to [building the project](#noesis_cs_step_build) - cloning the sample, importing the project into SDK Browser and repairing it - is exactly the same, just select a `*_lin_*` `.project` file.


1. Build the project. Run the following command from the project root, substituting the configuration you need - Release-Double, Debug-Double, Release or Debug: ```bash dotnet build -c Release-Double unigine-noesis-csharp-integration-sample.csproj ``` > **Warning:** Precision must match the `.project` file you have selected - see [the details in the guide above](#noesis_cs_precision). The binaries land in the project's `bin/` folder, next to the engine libraries and the native `libNoesis.so` library. The name of the resulting assembly depends on the configuration you have built:

  - `unigine-noesis-csharp-integration-sample_double_x64.dll` - release, double precision
  - `unigine-noesis-csharp-integration-sample_x64.dll` - release, single precision (float)
  - `unigine-noesis-csharp-integration-sample_double_x64d.dll` - debug, double precision
  - `unigine-noesis-csharp-integration-sample_x64d.dll` - debug, single precision (float)
2. Run the application from the console on *Vulkan* - the engine has no *Direct3D 12* backend on Linux. The command below is an **example** for a release build with double precision, started from the project's `bin` folder: ```bash cd bin export LD_LIBRARY_PATH="$PWD:$LD_LIBRARY_PATH" dotnet unigine-noesis-csharp-integration-sample_double_x64.dll \ -video_app vulkan -sound_app openal \ -console_command "world_load noesis_sample" ``` Substitute the name of the `.dll` file for the configuration you have built.


If the application fails to start, check that LD_LIBRARY_PATH contains the project's `bin/` folder and that you passed -video_app vulkan.


## What the Sample Contains


The sample loads `data/noesis_sample.world`, which holds only a ground plane, a world light and a spectator camera. The interfaces are created at run time by *AppWorldLogic.cs* from the XAML files in `data/ui/`, and all of them share one data context and the `ui/themes/noesis/NoesisTheme.DarkBlue.xaml` theme:


| Interface | XAML file | What you see |
|---|---|---|
| Screen-space view in a rectangle | `ui/overlay.xaml` | The *NEW GAME* and *SETTINGS* buttons in a 500x300 rectangle in the upper left corner. |
| Full-window screen-space view | `ui/text_font.xaml` | The *Font* and *Size* combo boxes with a sample text in the lower left corner. The chosen font family goes into the data context and comes back to the text - the two-way binding of the sample. |
| GUI mapped onto a 3D surface | `ui/world.xaml` | A 2x2 m panel with a resolution of 1024x1024, tilted in front of the camera. Its sliders and the color list control the DropShadowEffect of the drawn cloud - a purely ***NoesisGUI*** effect inside the interface. |


The interfaces get the mouse only while it is not grabbed for camera control. The panel in the world is picked by a ray limited to the control distance set for it - 5 m in this sample, so if its sliders do not react, move the camera closer.


The integration itself lives in `source/`: NoesisIntegration owns the lifetime of ***NoesisGUI*** and forwards input, NoesisRenderDevice is the render device implementation itself, NoesisProviders loads XAML, textures and fonts through the UNIGINE file system, and *NoesisGuiObject* is the panel in the 3D world - see [C++ and C# Implementations](#noesis_differences).


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


That is why *AppSystemLogic.cs* points the fallback chain at one of the bundled faces - ui/themes/noesis/Fonts/#PT Root UI. Naming a system family such as *Arial* there works on Windows only, where Noesis resolves it through *DirectWrite*; on Linux every character is rendered as a .notdef box.
