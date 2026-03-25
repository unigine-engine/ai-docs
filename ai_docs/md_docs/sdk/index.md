# SDK Browser 2


> **Notice:** Use **SDK Browser v2** for working with your UNIGINE projects based on **SDK 2.9+**. You can download it for your OS via the link below:
>
>
> - [Download SDK Browser](https://developer.unigine.com/en/downloads)
>
>
> ![](sdk_versions.png)
>
>
> If you have ongoing projects based on SDK 2.16+ and at same time the ones based on SDK versions earlier than 2.9, you should use both versions of SDK Browser as follows:
>
>
> - *SDK Browser v2*: **SDK 2.9+**
> - *SDK Browser v1* (Deprecated): **SDK 2.8 and earlier**.


This article contains a brief description of UNIGINE SDK Browser features:


- Integration with *[developer.unigine.com](https://developer.unigine.com)* accounts
- Convenient downloading, installation and upgrade of multiple UNIGINE SDKs
- Quick creation of projects with customizable settings
- Browsing through various samples: UnigineScript, C++ API, C# API, 3rd party
- Downloading content on demand
- Self-update via Internet


The following video provides the overview of the SDK Browser:


The information on the browser downloading and installing can be found [here](../start/installing_sdk.md).


The information on licensing is available in the [Licenses](../sdk/licenses/index.md) article.


> **Warning:** SDK Browser may not launch correctly if you have **Astra Linux Special Edition 1.5 / 1.6** with **PaX** installed. As a workaround you can disable **MPROTECT** for the `browser.linux` binary as follows:
> ```text
> sudo paxctl -m browser_x64.linux
> ```
>
>
> For more detailed information on **MPROTECT** you can [click here](https://pax.grsecurity.net/docs/mprotect.txt).


## Creating an Account


You need an account to use UNIGINE SDK. This account also grants you authorized access to the [Developer Portal](https://developer.unigine.com) and [Forum](https://developer.unigine.com/forum/).


To create an account via SDK Browser, click ***Create account***:


![](create_account_button.png)


In the sign-up form:


1. Enter your name and email in the corresponding fields.
2. Create the password that will be used for signing in.
3. Check the box to confirm that you have read and agree with the specified terms and requirements.
4. Click the ***SUBMIT*** button.


![](create_account_form.jpg)


Upon clicking the ***SUBMIT*** button, an email will be sent to the email address specified by you at the account creation. The email contains the verification code to be entered in the corresponding field.


![](verification_code.jpg)


> **Notice:** If you haven't received the code:
>
>
> 1. Check the spam folder in your email box.
> 2. Check that you entered the email correctly - click *Back* to return to your sign up details.
> 3. Click *Send again* under the *SUBMIT* button, and we will send you another email.


After you've verified your email, your account is ready for use: you can use either your email or the login generated for you and the password you set during the account creation process.


## Signing In


Click *Options* and make sure that the [Login Server](#options_server) is set to a preferable location (*Global* or *China*).


Then enter your account credentials and click ***SIGN IN***.


![](sign_in.png)


## Global Options


It is possible to set the general startup settings for all projects, samples, and demos run via SDK Browser.


To open the **Global Options** form, click the following tab in SDK Browser:


![](options_tab.png)


The form will open:


![](options.png)


| Download Server | Server location (*Europe* or *Asia*). |
|---|---|
| Storage Path | A path to a folder where downloaded SDKs and demos will be stored. |
| Show Welcome Screen | Show the welcome screen on SDK Browser startup. |
| Close to Tray | Minimize the window to tray when closed. |
| Interface Language | Interface language used in SDK Browser. |
| Qt Path | Path to Qt libraries. This path is used to run [projects created by using QMake](../sdk/projects/index_cpp.md#api) via UNIGINE SDK Browser. > **Notice:** This option is available on Windows only. |
| Channel Activation | Activation of [Channel USB Dongles](../sdk/licenses/index.md#channel) |
| **DEFAULT VIDEO OPTIONS:** |  |
| API | Graphics API to be used for rendering. The following values are available: - *Auto* - automatically choose the best option from the available ones. - *DirectX 12* - *Vulkan* |
| Resolution | Window resolution. |
| Fullscreen | Fullscreen mode: - Disabled - application shall run in the windowed mode - Enabled - application shall run in the fullscreen mode |
| Video Debug | Debug context for Vulkan or DirectX. |
| Offscreen | Enables the offscreen mode for the application, making it possible to run UNIGINE Engine in a cloud and use powerful servers (e.g., to generate photorealistic datasets for deep learning and verification of AI algorithms). All windows in this mode are virtual, just like the display, user input is not available. |
| Monitors | Display configuration (for single- or multi-monitor rendering). |
| Stereo 3D | Stereo mode. > **Notice:** Depending on the graphics API used for rendering, the set of available [modes](../principles/render/output/stereo/index.md) varies. |


## SDKs


To start working, you should have an **SDK** installed. In the *SDKs* tab, you can install a new version of an SDK or add an already installed one.


> **Notice:** Standalone builds are available in the *[Downloads](https://developer.unigine.com/en/downloads)* section of the Developer's portal as well.


### Installing an SDK


To install a new SDK:


1. Click the *ADD SDK* button. ![](install.png) The *Add SDK* window will open. ![](add_sdk.png)
2. Select the SDK type in the **Edition** field (*Community, Engineering, Sim* or *Editor*).
3. Select the SDK version in the **Version** field. > **Notice:** You may optionally install the samples during the initial SDK setup or later via the [Samples](#samples) tab.
4. Click **Install**. The downloading and installation progress will be shown under the menu on the left and on the SDK tab. ![](progress_bar.png) > **Notice:** You can also install the required SDK when [creating a project](../sdk/projects/index_cpp.md#creation) - the SDK Browser will download and install the specified version automatically. > > > ![](projects/download_data.png)
5. When the installation is completed, click the **Activate** button of the installed SDK. ![Activate button](licenses/sdk_activate.png)
6. In the *Activate License* window that opens, select the suitable [license activation type](../sdk/licenses/index.md), and click **Activate**.


The SDK is activated and ready for use:


![Installed SDK](sdk_installed.png)


### Adding a Previously Installed SDK


To add an already installed SDK:


1. Click the *ADD SDK* button.
2. Click the ***add the already installed*** link in the bottom of the *Add SDK* window. In the browser window that opens, specify the path to the root folder of the required SDK. It will appear in the *My Projects* list. ![Link in the bottom to add an already installed SDK](add_installed.png)
3. Specify the path to the root folder of the required SDK. The SDK will appear in the SDKs tab. > **Notice:** Only SDKs containing the `manifest` file (present from the 04/23/2015) are available for adding.


### Upgrading an SDK


If a higher edition or version is available, you can uprgade your SDK instead of downloading the whole new version:


![Upgrade button](upgrade.png)


Once the SDK is installed, you can:


- Create a new project in the *[Templates](#templates)* tab.
- Install and run demos or samples ([C++](../sdk/api_samples/cpp/index.md), [C#](../sdk/api_samples/cs/index.md), [UnigineScript](../code/uniginescript/samples/index.md) and [3rd party](../sdk/api_samples/third_party/index.md) samples).


## Templates


All new projects are created from **[templates](../sdk/templates/index.md)** - a basis that matches your project's goals.


Templates provide a ready-to-use foundation: a preconfigured scene, core systems, and commonly used objects. They also include optimal settings for rendering, camera, physics, input, and plugins, set up for specific types of tasks.


![](projects/templates_sm.png)


## My Projects


![](projects/my_projects.png)


A **project** is an independent entity that contains all data on your application content organized in a set of directories.


The *My Projects* tab displays all available projects. The projects list can be displayed using thumbnails or as a list. Toggling between these two modes is done by using the corresponding buttons in the top right corner.


There are several ways of working with [projects](../sdk/projects/index_cpp.md):


- Create a [new project](../sdk/projects/index_cpp.md#creation) (you should have an SDK installed).
- Add an [existing project](../sdk/projects/index_cpp.md#add) from your local drive (after that, it will be easily accessible from here for editing, upgrade, or other actions).


## Add-Ons


![](addons.png)


**Add-On** is anything additional to standard UNIGINE SDK that extends its capabilities and/or can be used to develop UNIGINE-based projects including 3D models, materials, textures, visual effects, logic components, Engine and Editor extensions, tutorials, project examples or templates, as well as other elements that can be used in your UNIGINE projects.


You can browse and download add-ons created by UNIGINE or other users from *[Add-On Store](https://store.unigine.com/)*.


The complete list of UNIGINE's add-ons and their usage is available [here](../sdk/addons/index.md).


## Samples


The following samples can be found in the *Samples* tab:


- *[C++ Samples](../sdk/api_samples/cpp/index.md)* - a set of C++ API demos
- *[C# Component Samples](../sdk/api_samples/cs/index.md)* - a set of C# demos
- *[Unigine Script Samples](../code/uniginescript/samples/index.md)* - a set of UnigineScript demos
- *[3rd Party](../sdk/api_samples/third_party/index.md)* - a set of demos demonstrating UNIGINE integration with applications based on 3rd party technologies.


![](samples_not_installed.png)


To download samples for specific language, click **Install** button.


![](sample_content.png)


For each sample, you can:

- View the **source code**.
- Explore the **world content** used in the sample.
- Edit and view the sample world via **UnigineEditor**.
- **Run the sample** to see it in action.


> **Notice:** Each sample pack is stored as an individual project and appears in the *My Projects* tab.


## Demos


Here you can download, explore, and even modify various ready-made scenes, including *ArchViz*, *Aviation*, *Maritime*, *Complex Vehicles* and more.


To download any Demo, click **Install** under a project in the *Demos* tab.


![](install_demo.png)


## Knowledge


Use this tab to find answers to a wide range of development questions.


- Access the **online documentation** for the most up-to-date info.
- **Download offline docs** for use without an internet connection.
- Connect with other developers [on the UNIGINE forum](https://developer.unigine.com/forum/) or in our [Discord server](https://discord.com/invite/gFN7w9b).
- For confidential topics, you can request **private support** under an NDA.


![](knowledge.png)


## Links to Social Media


There is a bunch of quick links to our accounts on social media, forum and online documentation. Feel free to join our community and follow the news.


![](social.png)


## Troubleshooting


If SDK Browser displays an error message, check the following article for a possible solution:


- [SDK Browser Issues](../troubleshooting/browser_issues.md)
