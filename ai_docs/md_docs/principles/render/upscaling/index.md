# Upscaling with DLSS and FSR


> **Warning:** The feature is still **EXPERIMENTAL**.


UNIGINE provides support for two advanced upscaling technologies: *[NVIDIA DLSS](https://www.nvidia.com/en-gb/geforce/technologies/dlss/)* (*Deep Learning Super Sampling*) and *[AMD FSR 3](https://gpuopen.com/fidelityfx-super-resolution-3/)* (*FidelityFX Super Resolution 3*). These technologies enable upscaling on a wide range of devices from different manufacturers.


> **Notice:** UNIGINE provides support for **DLSS up to version 4** and **FSR up to version 3.1.3**.


These upscaling technologies are used to render high-resolution images based on the lower resolution source. If both upscalers are available, you can choose between them, or you can turn off upscaling at all. We suggest using the DLSS technology as it produces high-quality results with fewer visual artifacts.


> **Notice:** DLSS is not available out-of-the-box and requires [additional configuration of your UNIGINE project](#dlss_use).


![](dlss.png) ![](fsr.png)


> **Notice:** The *[TAA](../../../principles/render/antialiasing/taa.md)* effect is automatically disabled for the final image rendering when the DLSS or FSR 3 upscaling is applied.


## Requirements and Restrictions


The DLSS and FSR 3 upscalers have specific requirements and compatibility restrictions determining whether the application supports these features.


The upscalers are initialized on render initialization. To verify whether they are supported and initialized after application startup, you can do one of the following:


- Check the *Render* section of the console output.
- Run the `dlss_info` and/or `fsr_info` console commands.


For example, the *Render* section may provide the following information:


```text
---- Render ----
DLSS is supported
DLSS Streamline version: 2.7.32
FSR is supported
FSR Version: 3.1.3
FSR Max Contexts: 8
FSR RAM Scratch Size: 10 MB

```


If the upscaler is not supported, a corresponding message will be displayed in the console.


### DLSS


For proper work, DLSS must meet the following requirements:


- **Platforms:** Windows, Linux
- **Graphic API:** DirectX 12, Vulkan
- **Hardware:** any GeForce RTX GPU
- **Driver:** 522.25 version or newer


For example, if you run the application with a GPU that is not listed, you will receive the following message in the console:


```text
DLSS is not supported
Not an Nvidia GPU

```


> **Notice:** In addition, you can receive messages on missing libraries, as DLSS requires [additional configuration of your UNIGINE project](#dlss_use).


If you notice unusually long startup times when using DLSS, refer to [***DLSS Startup Troubleshooting***](../../../troubleshooting/antivirus/index.md#dlss_startup_issues)


### FSR 3


FSR 3 must meet the following requirements:


- **Platforms:** Windows
- **Graphic API:** DirectX 12, Vulkan
- **Hardware:** any GPUs supporting *[Shader Model 6.2](https://github.com/microsoft/DirectXShaderCompiler/wiki/Shader-Model-6.2)*
- **Driver:** no special requirements


## Using DLSS


For DLSS technology to work properly with UNIGINE, additional environment configuration is required.


### DLSS on Windows


> **Warning:** NVIDIA Streamline SDK **version 2.7.32** was used to test DLSS integration on Windows. Other versions have not been tested and may produce unexpected results.


1. Follow [this link](https://developer.nvidia.com/rtx/streamline/get-started) to download the *NVIDIA Streamline SDK*, which serves as a wrapper for DLSS and all its features.
2. Click **Access Github**. ![](access_github.png)
3. Before proceeding, review the license details and **make sure you accept** all of its terms and conditions: > **Notice:** 1. On the page that opens, find the `license.txt` file in the list of files and folders. ![](license_file.png) > 2. Open the file and **read the text carefully**. > 3. Switch to the repository homepage by clicking *Streamline*. ![](streamline_repo_home.png) > 4. Find the `NVIDIA Nsight Perf SDK License (28Sept2022).pdf` file mentioned in the `license.txt` in the same list of files and folders. > 5. Open it and **read the license carefully**. > 6. **If you accept all of the terms and conditions**, proceed with the following steps.
4. Switch to the repository homepage by clicking *Streamline* as you did previously.
5. Download *Streamline SDK 2.7.32 Release*. Click on the *Releases* link: ![](streamline_sdk_download_1.png) Find *Streamline SDK 2.7.32 Release* and download the `streamline-sdk-v2.7.32.zip` archive: ![](streamline_sdk_download_2.png)
6. Extract the ZIP archive. By default, it is extracted to the `streamline-sdk-v2.7.32` folder. However, you can rename it if necessary.
7. Before proceeding, review the license details and **make sure you accept** all of its terms and conditions: > **Notice:** 1. Open the `streamline-sdk-v2.7.32/bin/x64` folder and find the `nvngx_dlss.license.txt` text file. > 2. Open the file and **read the license carefully**. > 3. **If you accept all of the terms and conditions**, proceed with the following steps.
8. Close the file, return to the `streamline-sdk-v2.7.32/bin/x64` folder and find the following files: > **Notice:** You don't need to install the *Streamline SDK*. Simply navigate to the folder.

  - `nvngx_dlss.dll`
  - `nvngx_dlss.license.txt`
  - `sl.common.dll`
  - `sl.dlss.dll`
  - `sl.interposer.dll`
9. Copy these files to the `bin` folder of your UNIGINE project: > **Notice:** By copying the license file, you confirm that you accept all the terms and conditions it provides.

  1. Find your project in the UNIGINE SDK Browser and select **Other Actions -> Open folder**. ![](../../../sdk/projects/other_actions.png)
  2. In the directory that opens, find and open the `bin` folder.
  3. Copy the 5 files listed above.
10. Return to the `streamline-sdk-v2.7.32` root folder and find the following license files:

  - `license.txt`
  - `NVIDIA Nsight Perf SDK License (28Sept2022).pdf`
11. Copy these files to the root folder of your UNIGINE project. > **Notice:** By copying the license files, you confirm that you accept all the terms and conditions it provides.
12. The changes will be applied at the next application start-up. So, if you have UnigineEditor opened, restart it to apply changes.
13. In UnigineEditor, open the console and check that DLSS is available. The corresponding information is provided in the *Render* section: ![](dlss_console.png) > **Notice:** If DLSS is [not available](#dlss_requirements), the corresponding message will be shown in the console.


To use DLSS for the scene, enable it in one of the following ways and specify settings:


- Via the UnigineEditor interface: ![](dlss_mode.png)
- Using the `render_upscale_mode` console command: ```text render_upscale_mode 2 ```


### DLSS on Linux


On Linux, DLSS SDK 310.2.1 is used.


1. Follow [this link](https://github.com/NVIDIA/DLSS/tree/v310.2.1) to download the *NVIDIA RTX DLSS SDK*, which serves as a wrapper for DLSS and all its features.
2. Before proceeding, review the license details and **make sure you accept** all of its terms and conditions: > **Notice:** 1. On the page that opens, find the `LICENSE.txt` file in the list of files and folders. > 2. Open the file and **read the text carefully**. > 3. **If you accept all of the terms and conditions**, proceed with the following steps.
3. Download the following libraries available in `DLSS/lib/Linux_x86_64` folder:

  - `libnvidia-ngx-dlssd.so.310.2.1`
  - `libnvidia-ngx-dlss.so.310.2.1`
4. Copy these files to the `bin` folder of your UNIGINE project: > **Notice:** By copying the license file, you confirm that you accept all the terms and conditions it provides.

  1. Find your project in the UNIGINE SDK Browser and select **Other Actions -> Open folder**. ![](../../../sdk/projects/other_actions.png)
  2. In the directory that opens, find and open the `bin` folder.
5. Return to the `DLSS` root folder on github and find the following license file:

  - `LICENSE.txt`
6. Copy this file to the root folder of your UNIGINE project. > **Notice:** By copying the license file, you confirm that you accept all the terms and conditions it provides.
7. The changes will be applied at the next application start-up. So, if you have UnigineEditor opened, restart it to apply changes.
8. In UnigineEditor, open the console and check that DLSS is available. The corresponding information is provided in the *Render* section. > **Notice:** If DLSS is [not available](#dlss_requirements), the corresponding message will be shown in the console.


To use DLSS for the scene, enable it in one of the following ways and specify settings:


- Via the UnigineEditor interface: ![](dlss_mode.png)
- Using the `render_upscale_mode` console command: ```text render_upscale_mode 2 ```


## Using FSR 3


Before applying FSR 3 upscaling, you should check if it is available. In UnigineEditor, open the console and check the information provided in the *Render* section:


> **Notice:** If FSR 3 is [not available](#fsr2_requirements), the corresponding message will be shown in the console.


![](fsr3_console.png)


To use FSR 3 for the scene, enable it in one of the following ways and specify settings:


- Via the UnigineEditor interface: ![](fsr2_mode.png)
- Using the `render_upscale_mode` console command: ```text render_upscale_mode 1 ```


## Startup and Console Commands


The following startup command-line options are available:


- `dlss_application_id`
- `fsr_max_contexts`


The list of console commands related to upscaling is available [here](../../../code/console/index.md#upscalers).


## Settings of Upscalers


Depending on the current upscale mode, the set of settings differs. Please refer to the *[Upscalers](../../../editor2/settings/render_settings/upscalers/index.md)* article.


## When to Apply Upscaling


By default, upscaling is applied **before** all post-processing effects are rendered. However, you can choose to apply upscaling **after** rendering the post-process effects.


It can be done via the console using the `render_upscale_post` command or in UnigineEditor by toggling the *Upscale After Post Effects* parameter.


[![](rendering_sequence_modified_sm.png)](rendering_sequence_modified.png)


## Contexts


A **context** is a single call per upscaling operation.


The number of contexts that can be upscaled with FSR 3 is limited and can defined by the `fsr_max_contexts` console command. The recommended number of contexts is 8. Specifying the number of contexts is necessary when rendering into multiple viewports: the number of the viewports must correspond to the number of contexts.


The number of DLSS contexts is limited to 8.
