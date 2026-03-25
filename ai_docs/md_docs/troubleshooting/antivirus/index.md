# Antivirus Recommendations


This section contains recommendations on how to configure your antivirus settings to ensure smooth engine operation and avoid performance drops.


> **Notice:** ***Windows Defender*** is taken as an example. If you have another antivirus software, check and adjust the similar functions.


## Firewall blocking UNIGINE


Antiviruses may block the operation of applications.


To check and unblock UNIGINE-related apps in *Windows Defender*:


1. Click the *Start* button, type `Windows Defender Firewall` and select the matching app. The *Windows Defender Firewall* window will open.
2. On the left pane, click **Allow an app or feature through Windows Defender Firewall**.
3. In the *Allowed apps* window that opens, scroll down to find UNIGINE-related apps, check if they are enabled: ![Allowed apps](allowed_apps.png)


## Impact on Build Speed and Editor Performance


If antivirus software has real-time scanning enabled, files are checked in real time when they are created, opened or copied. This may cause slowing down of the development process: UnigineEditor initialization, assets validation, etc. Adding the project folder (or folders) to exclusions allows avoiding this drop-down in performance.


When building a project, scanning every file also may slow down the build. To avoid that, you can add the target folder (and probably folders that store involved cache and settings) to exclusions, and the files created in it won't be scanned.


To disable real-time scanning in *Windows Defender* for a specific folder:


1. Open **Windows Security** settings (click the *Start* button, type `Windows Security` and select the matching app).
2. Select **Virus & threat protection**.
3. Click **Manage settings**. [![](exclusion_1.png)](exclusion_1.png)
4. Click **Add or remove exclusions** option. [![](exclusion_2.png)](exclusion_2.png)
5. Click the **Add an exclusion** button to see the types of content that can be excluded: [![](exclusion_3.png)](exclusion_3.png)
6. Add the folder (or folders) containing your project as an exclusion following the on-screen directions. These folders should include:

  - Folder that was created for the project and named accordingly (which contains the folders `bin, data`, etc.). [![Project folder](pf_path.png)](pf_path_big.png) *Project folder in Windows Explorer* [![Project folder added as exclusion](pf_exclusion.png)](pf_exclusion_big.png) *Project folder added as exclusion*
  - All folders that [mount points](../../principles/filesystem/index_cpp.md#root_mount) refer to (if they are outside the project folder mentioned above). ![Mount point](mount_path.png) *Mount point created in UnigineEditor* [![Mount point added as exclusion](mount_exclusion.png)](mount_exclusion_big.png) *Mount folder added as exclusion*
  - Output folder where the build is going to be stored. [![Build folder](build_path.png)](build_path_big.png) *Build created in UnigineEditor* [![Build folder added as exclusion](build_exclusion.png)](build_exclusion_big.png) *Build output folder added as exclusion*


## Ensuring the Availability of TCP Port


TCP Port **33333** is crucial for the UNIGINE SDK performance, thus, ensure that it is not blocked by the antivirus.


Adjust the antivirus settings to allow TCP Port **33333**.


If you use *Windows Defender*, [create an inbound port rule](https://docs.microsoft.com/en-us/windows/security/threat-protection/windows-firewall/create-an-inbound-port-rule).


> **Notice:** Also ensure that TCP Port 33333 is not used by any other applications. Read [this article](../../troubleshooting/editor_issues.md#error_3) for more recommendations.


## DLSS Startup Troubleshooting


Launching the Engine with the installed **Streamline SDK (DLSS support)** may take longer than expected if network environment settings restrict outbound traffic.


```text
10:31:22 ...
10:31:22 ---- Render ----
10:31:22 Loading "dxgi.dll"...
10:32:51 Renderer: NVidia 11855MB
10:32:51 Renderer API: Direct3D 12.0
10:32:51 ...

```


Although the Streamline SDK `DLL`s are installed locally and can operate without internet access, the application may attempt to connect to NVIDIA servers during startup (e.g., for license validation or OTA updates).


If startup delays occur:


- Make sure you are using the latest GPU NVIDIA drivers (required for stable DLSS work).
- Try starting the engine with the argument *[dlss_log_mode 2](../../code/console/index.md#dlss_log_mode)* to enable detailed logging and help localize the issue.
- Review your network environment settings and ensure that outbound connections to public networks are not blocked by a firewall.
