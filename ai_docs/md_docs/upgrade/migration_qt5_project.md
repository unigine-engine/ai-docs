# Qt5 Project Migration


The Editor has been migrated from Qt5 to Qt6. When migrating an existing Qt5-based project, Qt5 libraries are automatically removed and replaced with Qt6.


Therefore, if you have a Qt5-based project and manually restore Qt5 dependencies to keep using Qt5, the Editor will fail to start. This is due to conflicts between Qt platform plugins (such as `qwindows.dll` on Windows or `libqxcb.so` on Linux), which cannot coexist between different Qt versions by default.


To resolve this issue, follow the below recommendations.


## Custom Qt Plugin Setup


If you want to continue developing your application using Qt5, you need to separate Qt plugin paths (for Qt plugins) between your application and the Editor.


Below is the recommended approach to configure the Editor to use Qt6, while keeping your application on Qt5.


1. Create a file named `qt6.conf` next to the Editor binary. This file should contain the following: ```text [Paths] Plugins = plugins_qt6 ```
2. Create a directory named `plugins_qt6` and move the required Qt plugin folders into it. ```text Example structure: Editor_x64.exe qt6.conf plugins_qt6/ platforms/ qwindows.dll imageformats/ styles/ tls/ ```


This ensures that the Editor loads the correct Qt6 plugins and avoids conflicts with legacy Qt5 setups.


> **Warning:** If you are using [Build Tool](../editor2/projects/build_project.md) with the [GUI-based](../editor2/projects/build_project.md#launcher_type) type (Launcher Default Settings -> Type), the build process will copy the `bin/platforms` and `bin/styles` directories from the project. These directories are for Qt5, which can cause the *ApplicationLauncher* to fail to start.
>
>
> Therefore, you will need to manually replace these plugin folders with Qt6 versions after each build.
