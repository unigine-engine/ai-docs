# Enabling Additional Features on Quest Devices


When using the OpenXR backend in your VR application, features like hand tracking, eye tracking, and mixed reality are generally supported out of the box. However, on *Quest* devices (e.g. **Quest 3 / Quest Pro**), a few additional requirements and setup steps are needed.


The following sections describe how to enable and configure these features step by step.


## Enabling Developer Features


### Create a Developer Account


To access additional OpenXR features, a **Developer Account** is required:


- If you don't have an account yet:

  1. Go to the Developer portal: *[https://developers.meta.com/horizon/](https://developers.meta.com/horizon/)*
  2. Sign in with your existing account or create a new one.
- Once you have an account, you can convert it to a developer account:

  1. Open the developer account management page: *[https://developers.meta.com/horizon/manage/verify](https://developers.meta.com/horizon/manage/verify)*
  2. Complete the verification process: ![](verification.png)


### Enable Developer Runtime Features


After creating a developer account, you will need to enable runtime features for development:


- Open the **Quest Link** app, you may need to restart it for the new settings to appear.
- Navigate to **Settings -> Beta**.
- Toggle on **Developer Runtime Features**.


![](settings_developer_features_enabled.png)

*Turn On the Developer Runtime Features*


> **Notice:** If the option does not appear, please restart the application and try again.


### Enable Mixed Reality and Eye Tracking


For further functionality, toggle


- **Passthrough over Meta Quest Link** - required for mixed reality features.
- **Eye Tracking over Meta Quest Link** - required for eye tracking features.


These can be found in the same **Settings -> Beta** section.


![](mixed_reality_settings.png)

*Turn On Additional Features*


### Set Meta Quest Link as the Active OpenXR Runtime


Make sure that **Meta Quest Link** is selected as the current OpenXR runtime:


- Navigate to **Settings -> General**.
- Click ***Set Meta Quest Link as active OpenXR Runtime***.


![](select_meta_as_runtime.png)

*SettingMeta Quest Linkas the active OpenXR runtime*


After applying these changes, Mixed Reality and other features will be available for use with UNIGINE.


## PCVR Connection and Bandwidth Requirements


Use a *USB 3.1 Gen 2* (or better) cable and port to ensure enough bandwidth. It is recommended to verify the connection speed using tools like *USB Tree Viewer* or similar utilities. The headset should be connected at **5 Gbps** or higher for a stable experience.


![](bandwidth.png)

*Bandwidth Limit Configuration*


Keep in mind that *Passthrough via Quest Link* processes images from the mixed reality cameras **on the PC side**. This means your system needs enough bandwidth both for camera image processing and for sending the encoded stereo image back to the headset. The final latency depends on the resolution and refresh rate, which can be configured per device in the **Quest Link** app under **Devices -> HMD -> Graphics Preferences**.
