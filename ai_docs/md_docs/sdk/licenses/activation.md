# License Activation


SDK Browser manages licenses for each SDK installed on the current PC: in order to use UnigineEditor or debug builds of the engine, **it is required to keep SDK Browser launched on the currently used computer**.


Having just [installed SDK](../../sdk/index.md#sdks), you should activate your [license](../../sdk/licenses/index.md) with one of the following license activation types:


- [Floating License](#floating)
- [Fixed License](#fixed)
- [USB Key (HASP) Activation](#usb)


> **Notice:** Alternatively, a license can be served to all machines on your local network from a single machine by the console-based [Offline Licensing Server](../../sdk/licenses/licensing_server.md).


Licenses are assigned to user accounts via [License Manager](../../sdk/licenses/admin_panel.md).


Release builds of the engine do not require connection to SDK Browser. Release builds based on the [**SIM Per Channel**](../../sdk/licenses/index.md#channel) SDK edition may require [Channel USB License Dongle (HASP)](#usb).


> **Notice:** For **evaluation kits**: SDK Browser should always be launched irrespective of the build version, as in this case broadcasting over LAN isn't supported.


## License Activation


After you have [installed an SDK](../../sdk/index.md#sdks), the **Activate License** window opens:


![](license_activation_types_1.png)


License activation types are available depending on your license. If a certain license activation type is not available as supposed, contact the person who is assigned the role of *[Company Admin](../../sdk/licenses/admin_panel.md#roles)* for assistance.


> **Notice:** If you have any questions or technical issues, don't hesitate to send us an email to ***licensing@unigine.com***. You can also check out the [Troubleshooting](../../troubleshooting/browser_issues.md#licensing) section for possible solutions.


If you do not have stable Internet connection, SDK Browser can work in the offline mode. However, in this case, it is required to activate your [offline license](#fixed_offline).


Having activated a license for SDK, you can see the info about it by using the **License Info** button.


![](sdk_activated_license_info.png)


In the window that opens, the information on the current license is available:


- License type
- Account
- Expiration date of runtime and updates


![](sdk_license_info.png)


## Floating License


This type of license activation is **account**-locked.


If you have a stable Internet connection, your licenses are retrieved automatically from your *[developer.unigine.com](https://developer.unigine.com)* account. That means you can switch between PCs.


> **Notice:** A seat can't be used by several computers at the same time. If you sign in on a computer, you will be logged off on the one, where you've been signed in before.


To activate a product with this type of activation, select the **Floating License** type in the **Activate License** window that appears immediately after the product has been installed:


![](license_activation_floating.png)


If the product has already been installed, but is not activated, do the following:


1. Run SDK Browser and sign in with your credentials. ![](sign_in.png)
2. Go to the **Products** tab of the *SDK Browser*.
3. Click **Activate** on the *SDK* panel. ![](sdk_activate.png)
4. In the window that opens, choose **Floating License** and click *Activate*. SDK will be activated and locked to the current account. ![](sdk_activated.png)


You can [switch](#switch_to_offline) from *Floating License* to *[Fixed](#fixed)* anytime.


## Fixed License


This type of license activation is **node**-locked. That means SDK is locked to the current PC and will not be available on other machines.


Internet connection is not required for work with this type of license. However, it is required for activation: you can activate Fixed license in the two following ways:


- [Online activation](#fixed_online)
- [Offline activation](#fixed_offline)


> **Warning:** Switching to Fixed License **cannot be reverted**.


### Online Activation


If you can provide a stable internet connection for one-time activation, this type of license activation is your choice. Your licenses are retrieved automatically from your *[developer.unigine.com](https://developer.unigine.com)* account.


To activate a product with this type of activation, select the **Fixed License (Online Activation)** type in the **Activate License** window that appears immediately after the product has been installed:


![](license_activation_fixed_online.png)


If the product has already been installed, but is not activated, do the following:


1. Run SDK Browser and sign in with your credentials. ![](sign_in.png)
2. Go to the **Products** tab of the SDK Browser.
3. Click **Activate** on the SDK panel. ![](sdk_activate.png)
4. In the window that opens, choose **Fixed License (Online Activation)** and click *Activate*. SDK will be activated and locked to the current PC.


### Offline Activation


If you do not have a stable internet connection, you can perform offline activation of the *Fixed* License.


> **Notice:** Keep in mind that the SDK that you are going to use under this license should be [downloaded and installed on your PC](../../sdk/index.md#sdks) before you go offline.


To activate your offline license:


1. Run SDK Browser and click **Go Offline**. ![](go_offline.png)
2. Go to the **Products** tab of UNIGINE SDK Browser.
3. Click **Activate** on the SDK panel. ![](sdk_activate.png)
4. In the window that opens choose **Fixed License (Offline Activation)**. ![](license_activation_types.png) The *Offline Activation* form will open: ![](offline_activation_instructions.png)
5. Copy the request code to the clipboard or write it down. ![](copy_request_code.png)
6. Provide the request code to the [Company Admin](../../sdk/licenses/admin_panel.md#roles) to [generate the activation code](../../sdk/licenses/admin_panel.md#offline_code). > **Warning:** The **Request code** is PC-dependent, so it can be used to generate the activation code for one PC and in its current configuration only. If the PC hardware has been modified, a new activation code is required for activation of a modified PC.
7. After receiving the activation code, enter it to the activation code line. If the Company Admin provided the `*.key` file with the activation code, click **Open Key File**, choose the provided file in the file dialog window that opens, and click **Open**. ![](open_key_file.png)
8. Click **Activate**.
9. SDK will be locked to the current PC. ![](sdk_activated_fixed.png)


Done! Your offline license has been activated.


### Switching to Offline License


You can switch from *[Floating](#floating)* License to *Fixed* anytime. To do that, perform the following steps:


1. Click **License Info** on the *Products* panel. ![](sdk_activated_license_info.png)
2. Click **Change to Fixed** to change the license activation type to *[Fixed](#fixed_online)*. ![](sdk_license_change_to_fixed.png)


Then follow the guidelines for the preferred activation method:


- [Online activation](#fixed_online)
- [Offline activation](#fixed_offline)


## USB License Dongle (HASP)


A USB license dongle (HASP) is the license activation method that holds licenses under hardware control thus allowing you to run SDK Browser without Internet access.


> **Notice:** Keep in mind that the SDK that you are going to use under this license should be [downloaded and installed on your PC](../../sdk/index.md#sdks) before you go offline.


The HASP license activation method is available for all [types of licenses](../../sdk/licenses/index.md): *Seat, Editor Seat*, and *Channel*.


HASP may be used for both Windows and Linux.


### Activation On Windows


1. Insert the USB license dongle into the USB port.
2. Run SDK Browser and click **Go Offline**. ![](go_offline.png) If you are already logged in, sign out to access this option. ![](sign_out.png)
3. The authorization process will be done automatically. Don't eject the dongle while working. ![SDK activated with a USB key](usb_key_activation.png) *SDK activated with a USB key*


> **Warning:** In order for your keys to work as expected, please disable the *USB selective suspend* feature. Follow [this link](https://www.windowscentral.com/how-prevent-windows-10-turning-usb-devices) to learn more.


### Activation On Linux


1. Check if your operating system contains the *[udev](https://www.freedesktop.org/software/systemd/man/udev.html)* subsystem.
2. Run the `SDK_Browser/bin/install_grdnt_udev_rules.sh` script (the root user's rights are required).
3. Insert the USB license dongle into the USB port.
4. Run SDK Browser. Authorization process will be done automatically (the sign-in form will be skipped). Don't eject the dongle while working.


### License Broadcasting with HASP


If you have a HASP with **multiple seats** (more than one *Seat* license on one and the same USB), insert a dongle into any PC in the local network. Other licenses are retrieved automatically in the same way as for online licenses.


> **Notice:** License broadcasting over the local network is not available for *IG Channel* and *VR Channel* USB Dongles.


In case of **multiple dongles** used in one local network:


1. Insert a dongle into any PC in the local network. This PC is going to be the licensing host.
2. Run SDK Browser on the licensing host.
3. On the PC that is going to work under the license, Run UNIGINE Editor with the argument containing the parameters of the licensing host (either via *[Customize Unigine Editor Options](../../sdk/projects/index_cpp.md#customize_edit)*, or directly on starting the Editor). For example: ```bash -licensing_host 192.168.1.1 ```


On the PC that has a dongle inserted (licensing host), SDK Browser shall be running. Other PCs that retrieve the license can do without SDK Browser and open the Editor or build directly.
