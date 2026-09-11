# Patching Project Files


> **Warning:** It is crucial to patch the code to include the Agility SDK � without it, your project will not run on DirectX 12, as DX12 without Agility SDK is not supported.


Upgrading your project to a newer version may sometimes require changes to project files (such as adding new files) or source files (such as adding include directives). These changes are most commonly related to integrating new third-party libraries.


To save you from having to make these modifications manually, the SDK includes built-in functionality to assist with migration. When updating your project, you can select which files should be automatically patched.


![](patch_sdk_browser.png)


By default, all files are selected for patching.


> **Notice:** Remember to rebuild the project after patching, as the patch modifies the code.


## Manual Patching


To upgrade the project or source files in the manual mode, do the following:


1. Put the binary executable `<UnigineSDK>/bin/usc_x64.exe` to the `<UnigineSDK>/utils/upgrade_project` folder that contains the upgrade script. > **Notice:** Use `usc_x64.exe` from the SDK version you are migrating **to**.
2. In the command prompt, [run](../tools/usc/index.md#run) the `upgrade.usc` with the corresponding arguments.


The following arguments are available:


| --project_directory |
|---|
| **Description:** Path to the project directory. Setting just this argument ensures that all other arguments are filled in automatically and all possible files are patched. **Example:** `usc_x64.exe upgrade.usc --project_directory D:/SDK_Browser/projects/unigine_project` |
| --skip_source_paths |
| **Description:** C++ files won't be patched. Use this argument along with [--project_directory](#--project_directory) if you don't need to patch this type of files. |
| --skip_vscode_paths |
| **Description:** VS Code files won't be patched. Use this argument along with [--project_directory](#--project_directory) if you don't need to patch this type of files. |
| --skip_csproj_path |
| **Description:** *.csproj files won't be patched. Use this argument along with [--project_directory](#--project_directory) if you don't need to patch this type of files. |


Here's an example with skipping several types of files:


```bash
usc_x64.exe upgrade.usc --project_directory path/to/project --skip_source_paths --skip_csproj_path

```


In this case, only VS Code files will be patched.


The following arguments are available if you want to have a more controllable patching process:


| --project_path |
|---|
| **Description:** Path to the project - the SDK version from which the project will be migrated is taken from this project. **Example:** `usc_x64.exe upgrade.usc --project_path D:/SDK_Browser/projects/unigine_project/project_name_2_19_1.project` |
| --vscode_paths |
| **Description:** Path to VS Code files. **Example:** `usc_x64.exe upgrade.usc --vscode_paths D:/SDK_Browser/projects/unigine_project/.vscode` |
| --source_paths |
| **Description:** Path to source files. **Example:** `usc_x64.exe upgrade.usc --source_paths D:/SDK_Browser/projects/unigine_project/source` |
| --csproj_path |
| **Description:** Path to *.csproj files. **Example:** `usc_x64.exe upgrade.usc --csproj_path D:/SDK_Browser/projects/unigine_project/unigine_project.csproj` |
| --start_version |
| **Description:** Set the SDK version from which the project will be migrated, if it can't be set by [`--project_path`](#--project_path). |
