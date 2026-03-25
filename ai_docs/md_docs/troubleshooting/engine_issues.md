# Engine Issues


This section provides information on typical errors displayed in the Engine log and explains how to fix them.


## Agility SDK


When running the upgraded project on DX12, you may come accross the following error in the engine log:


`ERROR: Engine::init(): using D3D12 without Agility SDK is not supported. Please export `D3D12SDKVersion` and `D3D12SDKPath` in your executable. Falling back to Vulkan`


This error occurs because starting from version 2.20, we use the Agility SDK to unlock the full potential of DirectX12. Therefore, [patching](../upgrade/migration_patch.md) is required to ensure the upgraded project runs smoothly on D3D12.


If the project after being patched and rebuilt still doesn't run on D3D12 and this error keeps being displayed, try the following:


**On C++:**


- Open the `<project_name>/source/main.cpp` file and check if it contains the following line: ```cpp #include <UnigineInit.h> ``` Add it, if it's missing.
- Check if the project contains the `<project_name>/bin/D3D12` folder with the following files:

  - `D3D12Core.dll`
  - `D3D12Core.pdb`
  - `D3D12SDKLayers.dll`
  - `D3D12SDKLayers.pdb`


**On C#:**


- Open the `<project_name>/<project_name>.csproj` file and check if it contains the following lines: ```xml <UseAppHost>true</UseAppHost> <AppHostSourcePath Condition="'$(OS)' == 'Windows_NT'">$(OutputPath)\dotnet_host_x64.exe</AppHostSourcePath> ``` Add them, if missing.
- In case of `.vscode`, open `<project_name>/.vscode/launch.json`, and make sure that Windows projects are started via `<project_name>.exe`.
- Check that the project contains the `<project_name>/bin/D3D12` folder with the following files:

  - `D3D12Core.dll`
  - `D3D12Core.pdb`
  - `D3D12SDKLayers.dll`
  - `D3D12SDKLayers.pdb`
- Check that the `dotnet_host_x64.exe` file is available in the `<project_name>/bin/` folder.


## Failed to connect to SDK Browser


When running the application, you may encounter the following error: *"Failed to connect to SDK Browser. Restart SDK Browser and try again."*


![](browser_connection_failure.png)


If you restarted SDK Browser and the problem persists, the following should be checked:


- **Ports and firewall settings**. UNIGINE SDK Browser uses TCP Port **33333** by default to communicate with UNIGINE Engine, so make sure it is available. Sometimes TCP Port 33333 may be occupied by other software (for example, *Goodsync* server, *Yeelight* solutions, etc.), or antivirus software can block this port. To check all open TCP ports, you can use: If this is the case, close the program that uses TCP Port 33333, and start UNIGINE SDK Browser.

  - On Windows - ***Resource Monitor***, a built-in utility. You can open it via the Start menu, or from Task Manager's *Performance* tab and sort by *Port* to see if SDK Browser is the only user of this port. ![](resource_monitor.png) *Checking the port used by SDK Browser in Resource Monitor*
  - On Linux - the following command: ```text sudo netstat -nltup ```
- A certain **application may block communication between SDK Browser and Engine**. To check if this is the issue, boot into a safe mode (for example, [*Windows 10* safe mode (with Networking)](https://support.microsoft.com/en-us/help/12376/windows-10-start-your-pc-in-safe-mode)) and try to run SDK Browser and the application. SDK Browser may load a little bit slower here, please wait. If there are no errors, that would mean that some application running in normal *Windows* boot is blocking communication between SDK Browser and Engine.


If your problem still exists, address the [support](https://developer.unigine.com/forum/).


UNIGINE logs errors to the console and the main log file (stored in `<UserProfile>/AppData/Local/Unigine_SDK_Browser` for *Windows* or `.local/share/Unigine_SDK_Browser` for **nix* systems), so you can check there for more information.
