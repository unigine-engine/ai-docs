# VR Template Project Setup (CS)


Before we dive into the template's systems, let's get a project up and running. It only takes a few minutes.


> **Notice:** The code and content of the VR Template differ slightly between the C++ and C# API versions. You can switch between languages using the selector in the upper-right corner of the page.


## 1. Creating a VR Project


Open your SDK Browser and go to the *Templates* tab. Find the **VR C#** template and click **Create Project**.


![](cs_vr_template.png)


Choose a name for your project, its location, the SDK version, and the precision -*Float* or *Double*.


![](create_from_template.png)


Once the project is created, it will appear on the *My Projects* tab of the SDK Browser.


## 2. Setting Up a Device and Configuring Project


Let's assume you've already installed your Head-Mounted Display (HMD) of choice.


[Learn more](../../../vr_development/index.md#vr_backends) on setting up devices for different VR platforms. For guidance on configuring your device, refer to the official documentation provided by your runtime or hardware vendor.


> **Notice:** *Mixed Reality*  functionality is supported through both the [OpenXR](../../../vr_development/index.md#backend_openxr) and [Varjo](../../../vr_development/index.md#backend_varjo) backends. The Varjo backend provides a richer set of MR features including chromakey, camera controls, and color correction.
>
>
> If you're using a Varjo headset, make sure *[Varjo Base](https://varjo.com/downloads/#varjo-base)* is installed and running.


The VR Template supports [any VR device](../../../vr_development/index.md#vr_devices) that exposes input and tracking through a supported runtime backend.


By default, VR is not initialized. To enable it, do one of the following:


- If you run the application via UNIGINE SDK Browser, set the **Stereo 3D** option to the value that corresponds to your HMD (*OpenXR*, *OpenVR* or *Varjo*) in the **Global Options** tab and click **Apply**. ![](options_openxr.png)
- When running from the command line, specify the VR runtime backend using the *[-vr_app](../../../code/command_line.md#vr_app)* option: ```bash your_app_name -vr_app <backend> ``` Supported backends: For example: ```bash your_app_name -vr_app openxr ``` You can also specify this option in the *Customize Run Options* window when launching through the SDK Browser: ![](customize_run.png)

  - *openxr* -for devices compatible with the OpenXR standard.
  - *openvr* -for devices running via OpenVR-compatible runtimes.
  - *varjo* -for Varjo headsets via the Varjo SDK.


## 3. Open Project's Source


To open the project in your IDE, select it on the *My Projects* tab and click *Open Code IDE*.


You'll see quite a few component scripts -don't worry, [this overview](../../../vr_development/vr_template/vr_template_classes_and_components/index_cs.md) explains what each one does.


All C# component scripts are located in the `data/vr_template/components/` folder and are automatically compiled when you run the application. You can edit them in your preferred IDE (Visual Studio, Visual Studio Code, or Rider).


Launch the application by selecting the project on the *My Projects* tab and clicking **Run**.


Before running, make sure the right *Customize Run Options* are selected -click the ellipsis under the **Run** button to check.


![](customize_run_debug.png)


That's it -the project is set up and running. Let's move on to exploring what's inside!
