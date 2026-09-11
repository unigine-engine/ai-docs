# Version Control


Version Control Systems or VCS (*Git, SVN, Perforce, Mercurial, Bazaar, CVS, TFS*, etc.) are used to manage changes to code and data, and enable teams to coordinate their development efforts. To make tracking of changes efficient and reduce the amount of disk space required, you should know which files must be tracked by the VCS and which can be ignored.


> **Notice:** UNIGINE has [**VCSIntegration Plugin**](../../../editor2/assets_workflow/version_control/vcs_plugin/index.md) that is designed to simplify work with the version control system (SVN,Git) and track all file changes performed in UNIGINE Editor.


## Ignore List


In any project there are files and folders that are not subject to version control. These can be files created by the compiler, `*.obj`, `*.tlog`, or an output folder used to store binary executables.


The following files and folders in you project's root can be ignored, as they are generated automatically on your disk:


### Common ignore list for every API and IDE


- ![](../folder.png) `.thumbnails`
- ![](../folder.png) `bin` > **Notice:** Add this folder to version control before updating the engine�s version or reconfiguring the project in SDK Browser to provide the updated `bin` to all developers.
- ![](../folder.png) `data/.thumbnails`
- ![](../folder.png) `data/microprofile_dump_html`
- ![](../folder.png) `.svn`
- ![](../folder.png) `junk`
- ![](../folder.png) `obj`
- ![](../folder.png) `out`
- ![](../folder.png) `output`
- ![](../folder.png) `source/x64`
- ![](../file.png) `CMakeCache.txt`
- ![](../file.png) `source/**/*.obj`
- ![](../file.png) `unigine_editor.cfg`
- ![](../file.png) `*.cache`
- ![](../file.png) `*.gpu_cache`
- ![](../file.png) `*.modified`
- ![](../file.png) `*.tlog`
- ![](../file.png) `*.log`
- ![](../file.png) `.~lock.*`
- ![](../file.png) `bin/editor_log*.txt`
- ![](../file.png) `bin/log*.txt`
- ![](../file.png) `bin/*.dmp`
- ![](../file.png) `data/configs/default.user`


<details>
<summary>Gitignore file</summary>

```text
.thumbnails
bin
data/.thumbnails
data/microprofile_dump_html
.svn
junk
obj
out
output
source/x64
CMakeCache.txt
source/**/*.obj
unigine_editor.cfg
*.cache
*.gpu_cache
*.modified
*.tlog
*.log
.~lock.*
bin/editor_log*.txt
bin/log*.txt
bin/*.dmp
data/configs/default.user

```

</details>


### Additional ignore list for C++ (CMake) projects


Add these entries to the [common](#all) `.gitignore` specified above when developing projects based on *C++ (CMake)*.


- ![](../folder.png) `build-*`
- ![](../folder.png) `CMakeFiles`
- ![](../folder.png) `CMakeScripts`
- ![](../file.png) `CMakeCache.txt`
- ![](../file.png) `cmake_install.cmake`
- ![](../file.png) `CMakeUserPresets.json`
- ![](../file.png) `compile_commands.json`
- ![](../file.png) `CTestTestfile.cmake`


<details>
<summary>Gitignore file</summary>

```text
build-*
CMakeFiles
CMakeScripts
CMakeCache.txt
cmake_install.cmake
CMakeUserPresets.json
compile_commands.json
CTestTestfile.cmake

```

</details>


### Additional ignore list for C++ (Visual Studio 2015+) projects


Add these entries to the [common](#all) `.gitignore` specified above when developing projects based on C++ (Visual Studio 2015+).


- ![](../folder.png) `.vs`
- ![](../file.png) `*.vcxproj.user`
- ![](../file.png) `*.VC.db`
- ![](../file.png) `*.opendb`
- ![](../file.png) `*.opensdf`
- ![](../file.png) `*.pro.user`
- ![](../file.png) `*.sdf`
- ![](../file.png) `*.suo`


<details>
<summary>Gitignore file</summary>

```text
.vs
*.vcxproj.user
*.VC.db
*.opendb
*.opensdf
*.pro.user
*.sdf
*.suo

```

</details>


## Files and Folders to Add to Version Control


The following files and folders should be subject to version control:


- ![](../folder.png) [`data`](../../../editor2/assets_workflow/project_files.md#data_folder) folder with all its contents > **Notice:** If you do not want to share the editor and application settings with other team members, add the following configuration files to `.gitignore`: > > > - `data/configs/unigine.user` > - `data/configs/default.user` > - `data/.editor2/*` This folder also contains runtime files (`data/.runtimes`) that should be committed. However, if you occasionally fail to commit runtimes, the runtimes validation process will run when UNIGINE Editor is started, and the missing/outdated runtimes are added/updated. The runtime validation is also performed on adding a new mount.
- ![](../folder.png) [`source`](../../../editor2/assets_workflow/project_files.md#data_folder) folder contents except for the elements mentioned above > **Notice:** This folder is created only for projects that use C++ or C# API.
- ![](../file.png) `*.cache` files containing compiled shader cache > **Notice:** When team members develop a project using different GPUs or/and driver�s version for their machine configuration, it is better to add the shader cache files to `.gitignore` since these file will be recompiled by an end developer�s computer.
- ![](../file.png) `*.project` file (and `*.csproj` for C# projects)


## Other Notices


This chapter contains recommendations based on the user experience.


### Perforce


- Set the Allwrite attribute in *Perforce Workspace* (the *Advanced* tab). It's disabled by default, which may cause issues with SDK Browser and `*.project` file.
- Checking out and locking a file does not prevent other users from modifying it, since that's only a *Perforce* abstraction.
