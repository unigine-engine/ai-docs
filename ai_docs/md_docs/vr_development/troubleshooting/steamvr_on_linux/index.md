# Configuring SteamVR on Linux for Best Experience


This article contains the recommendations for SteamVR settings on Linux for a better performance of UNIGINE-based VR applications.


## Setup Requirements


SteamVR for Linux will not function correctly within the unsupported *Steam Snap* or *Flatpak* builds, as these packages break DRM leasing and asynchronous reprojection. Use the native distribution packages instead.


For *Ubuntu*, install the official *Steam* `*.deb` package available from the **[Steam Downloads](https://store.steampowered.com/about/)** page.


## Graphics Drivers


Keep your system and graphics drivers fully up to date for the best SteamVR experience.


- **NVIDIA**: Use the proprietary driver version 525 or newer. > **Notice:** The open-source *Nouveau* driver does not support Vulkan.
- **AMD / Intel**: Use the open-source Mesa drivers, version 22.0 or newer. > **Notice:** The proprietary *AMDGPU-Pro* and *AMDVLK* drivers are not supported and may break SteamVR, even if not actively in use. **Remove these drivers** from your system before launching SteamVR.


## Desktop Environment Support


SteamVR for Linux requires **DRM leasing** to function. With DRM leasing, SteamVR can use your headset's display directly to keep VR visuals fast and responsive.


**Not all *Wayland* compositors support DRM leasing.** Use X11 or another compatible Wayland compositor to run SteamVR.


Some compatible window managers/compositors include:


- All X11 Window Managers and Compositors
- *KDE Plasma Wayland*
- Most *wlroots* based compositors:

  - *Sway*
  - *LabWC*
  - *Hyprland*


*Gnome Wayland*, the default on Ubuntu, **does not support DRM leasing and cannot run SteamVR**. In this case you have to switch to an alternative compositor:


- Use the *Gnome X11* session: at the login screen, click the gear icon and select *"Ubuntu"* (not *"Ubuntu on Wayland"*).
- Alternatively, you can also use *KDE Plasma* instead of *Gnome* to use SteamVR on *Ubuntu*.


For optimal performance and latest driver support, ***Plasma Wayland* on an Arch-based distribution is recommended**.


## Checking Default Settings


1. Launch SteamVR.
2. Enable **Advanced Settings**.
3. Open SteamVR Settings and make sure that no scaling is applied to resolution: *Settings -> General -> Render Resolution -> Resolution Per Eye = 100%* ![](resolution_per_eye.png)
4. Run the UNIGINE-based application in VR.
5. Open the application settings in SteamVR and make sure that no scaling is applied to resolution and **Legacy Reprojection** is disabled: *Settings -> Video -> PER-APPLICATION VIDEO SETTINGS* [![](per_app_settings_sm.png)](per_app_settings.png)


## Enabling Asynchronous Reprojection


Async reprojection helps stabilize the frame rate. Even if the engine reports only 45 FPS in the application, the headset will still display 90 FPS thanks to reprojection. However, if the application drops to 30 FPS, the headset will display 60 FPS.


Linux may fail to apply asynchronous reprojection even if the **Legacy Reprojection** Mode is disabled (*Use Legacy Reprojection Mode = Off*). To enable asynchronous reprojection, modify the file `steamvr.vrsettings` by adding `"enableLinuxVulkanAsync" : true` in **two** blocks:


| 1. In *steamvr* section: |
|---|
| 1. Close the SteamVR application. 2. Open the file `steamvr.vrsettings`. The relative path to the file is: `~/.steam/steam/config/steamvr.vrsettings`. 3. In this file find the *steamvr* section and add the following: ```xml "steamvr" : { ... "enableLinuxVulkanAsync" : true, ... } ``` 4. Save `steamvr.vrsettings`. |
| 2. In UNIGINE-based application section: |
| 1. Launch the SteamVR application. 2. Enable *Advanced Settings*. 3. Run the UNIGINE-based application in VR. 4. Open the application settings (*Settings -> Video -> PER-APPLICATION VIDEO SETTINGS*). 5. Change any application setting. For example, you can move the *Custom Resolution Multiplier* toggle. This action automatically creates the application section in `steamvr.vrsettings`. > **Notice:** After restarting the UNIGINE application remember to reset the modified setting. 6. Close the SteamVR application. 7. Open the file `steamvr.vrsettings`. 8. In this file find the section with the name of your application and add the following line: ```xml "system.generated.APP_NAME.exe" : { ... "enableLinuxVulkanAsync" : true, ... } ``` 9. Save `steamvr.vrsettings`. |


### Monitor Reprojection Status


You can verify that reprojection is active by using SteamVR's built-in frame timing tools: *Settings -> Developer -> Advanced Frame Timing*. A graph overlay will appear showing frame timings.


Look at the GPU graph (bottom part): if you see red spikes or a red line, that indicates **reprojection is active**:


![](reprojection_on.png)


No red indicators mean that **reprojection is not working**:


![](reprojection_off.png)


You can also check the file `~/.steam/steam/logs/vrcompositor.txt` for the content that should look approximately like this:


```text
Tue May 13 2025 12:12:52.530 [Info] - Lost pipe connection from vr219_x64 (16216)
Tue May 13 2025 12:12:52.530 [Info] - ######################################################################
Tue May 13 2025 12:12:52.530 [Info] - Cumulative stats for pid: 16216
Tue May 13 2025 12:12:52.530 [Info] - Total..................241834 presents.  258 dropped. 57287 reprojected
Tue May 13 2025 12:12:52.530 [Info] - Startup................    73 presents.    0 dropped.   45 reprojected
Tue May 13 2025 12:12:52.530 [Info] - Loading...  0 total....     0 presents.    0 dropped.    0 reprojected
Tue May 13 2025 12:12:52.530 [Info] - Timed out.  0 total.... 26259 presents.   30 dropped. 3811 reprojected
Tue May 13 2025 12:12:52.530 [Info] - Compositor Time........CPU: 0.193ms / GPU: 0.560ms
Tue May 13 2025 12:12:52.530 [Info] - Game Info..............FPS Average Target 90  ApplicationTime CPU: 6.475ms / GPU: 10.412ms

```


> **Notice:** Unfortunately, on some Linux distributions (such as Astra 1.8), there's a bug in SteamVR where it doesn't log the number of reprojected frames, even though the *Advanced Frame Timing* overlay clearly shows that reprojection is working.
