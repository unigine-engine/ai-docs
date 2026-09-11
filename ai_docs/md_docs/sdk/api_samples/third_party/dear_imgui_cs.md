# DearImGUI Sample (CS)

> **Notice:** The complete sample source code is available on GitHub:
> **[github.com/unigine-engine/unigine-imgui-csharp-integration-sample](https://github.com/unigine-engine/unigine-imgui-csharp-integration-sample)**.


## General Information


***Dear ImGui*** is a fast, minimalistic, and highly portable immediate-mode GUI library primarily used for creating in-game and real-time development tools. It's designed to be simple to integrate into existing applications and is especially popular in the game development, graphics, and visualization communities.


![](../../../code/integration/dear_imgui.png)


Rather than creating traditional GUI layouts, ***Dear ImGui*** allows developers to quickly build dynamic interfaces - perfect for debugging tools, editors, data visualizations, and real-time control panels. It focuses on responsiveness and ease of use, making it ideal for prototyping and tools where performance and simplicity matter.


## How to Run the Sample


### Prerequisites


- **UNIGINE SDK Browser** (latest version)
- **UNIGINE SDK Community** or **Engineering** edition (**Sim** upgrade supported)
- **Visual Studio 2022** (recommended)
- **GitHub access** to clone the repository.


### Step-by-Step Guide


Starting the ***Dear ImGui*** C# sample requires you to perform the following steps:


1. Clone or download the sample from the *[UNIGINE Git repository](https://github.com/unigine-engine/unigine-imgui-csharp-integration-sample)*.
2. Open SDK Browser and make sure you have the latest version.
3. Add the sample project to SDK Browser:

  - Go to the *My Projects* tab.
  - Click *Add Existing* then select the `*.project` file located in the cloned sample folder corresponding to your setup (OS, SDK edition, and precision), and click *Import Project*. ![](photon/add_project.png)
4. Repair the project.

  - After importing, you'll see a **Repair** warning - this is expected, as only essential files are stored in the Git repository. SDK Browser will restore the rest. ![](repair_project.png)
  - Click *Repair* to let SDK Browser restore the required files.
  - When the configuration window opens, click *Configure Project*.
5. Open the project in your IDE.

  - Launch Visual Studio 2022 and open the sample `.sln` file.
  - Once the project is loaded, you might see a warning under *Dependencies -> Assemblies ->* *ImGui.NET* in the *Solution Explorer* window.
6. Install the required **NuGet** package.

  - In Visual Studio 2022, go to *Tools -> NuGet Package Manager -> Manage NuGet Packages for Solution�*
  - Search for and install the **ImGui.NET** package (version 1.86.0). [![](imgui_nuget_setup_small.png)](imgui_nuget_setup.png)
7. **Build** and **Run** the project.

  - Click **Build** to compile the project and then **Run** to launch the application.


If you're still having trouble running the application, revisit the steps above to ensure nothing was skipped. Check that you're using the correct `.project` file for your installed SDK edition and platform (Windows/Linux). If you encounter missing assembly errors, verify that **ImGui.NET** was installed successfully via **NuGet**. If build issues persist, try rebuilding the project by right-clicking on it and selecting **Rebuild**.
