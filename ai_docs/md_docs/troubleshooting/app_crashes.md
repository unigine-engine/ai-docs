# Application Crashes


This section provides information on crashes that may occur during developing a UNIGINE plugin or application.


The information on this page is updated based on your feedback.


## Crash at Developing a Plugin on Windows OS


When you develop a plugin, it is a common thing that it sometimes crashes. However, [Compatibility Administrator](https://docs.microsoft.com/en-us/windows/deployment/planning/compatibility-administrator-users-guide) on Windows may decide to fix this issue on its own and set a flag not to load the plugin. In this case the plugin may crash regardless of the logic. Hot reload will also be impossible, because the plugin is not released.


To fix this issue, you need to [open the Registry Editor](https://support.microsoft.com/en-us/windows/how-to-open-registry-editor-in-windows-10-deab38e6-91d6-e0aa-4b7c-8878d9e07b11) and check the settings stored at `Computer\HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags\Layers`. Delete any data related to your plugin.
