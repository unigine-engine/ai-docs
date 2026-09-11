# SDK Browser Issues


This section provides information on typical errors displayed in SDK Browser and explains how to fix them.


## Activation Issues


After registering on the *UNIGINE Developer* portal, you receive an email with a link to verify your email. As soon as you confirm your email address, your account is created � you can sign in to the Developer portal and SDK Browser. **Without confirming your email address you won't be able to sign in.**


If you can't find the confirmation letter, please check the spam folder. The letter subject is: *[UNIGINE] Email confirmation*.


## Licensing Issues


Verification of your license may fail in case the default **port of the licensing host** that is used for incoming connections is occupied. You can solve this issue by setting a custom port and ip-address using the special startup command-line argument: **--licensing-host ip:port**


For example, you can launch SDK Browser on Windows like this:


```bash
SdkBrowser.exe --licensing-host 0.0.0.0:11223
```


The same settings **must** be passed as a startup argument for UnigineEditor as well:
 `-licensing_host 0.0.0.0:11223`


![](custom_port.png)


If licenses are served over the local network by the [Licensing Server](../sdk/licenses/licensing_server.md), see its [Troubleshooting](../troubleshooting/licensing_server.md) section for the licensing messages and discovery issues.


## Evaluation Kit Limitations


Applications built with the **Evaluation kit** require SDK Browser installation and SDK activation on each PC. This limitation is only valid for the Evaluation kits.


Please, use an individual account per person to avoid the warning.


## Browser Errors


Settings and issues that may cause errors:


- Unstable **internet connection**. This may cause repeated logging off. However, if you are in the middle of downloading something via SDK Browser, it will be paused and continue downloading as soon as internet connection is resumed. ![](connection_problem_1.png) or ![](connection_problem_2.png) If you have continuous problems with the internet connection, you may consider using a [*fixed* license](../sdk/licenses/activation.md#fixed).
- The connection error may also be caused by **wrong date and time** settings. Check that you have actual date and time set.
- A certain **application may block communication between SDK Browser and Editor**. To check if this is the issue, boot into a safe mode (for example, [*Windows 10* safe mode (with Networking)](https://support.microsoft.com/en-us/help/12376/windows-10-start-your-pc-in-safe-mode)) and try to run SDK Browser and Editor. SDK Browser can load a little bit slower here, please wait. If there are no errors, that would mean that some application running in normal Windows boot is blocking communication between SDK Browser and Editor.
- You may encounter a **License Activation Error** due to missing *WMI* classes. ![](licensing_wmi.png) To restore the required classes open the Command Prompt (`cmd.exe`) as an Administrator and type: `MOFComp <WindowsDirectory>\system32\wbem\CIMWIN32.MOF` If the problem persists, simply reboot your computer.


UNIGINE logs errors to the console and the main log file (stored in `<UserProfile>/AppData/Local/Unigine_SDK_Browser` for *Windows* or `.local/share/Unigine_SDK_Browser` for a **nix* systems), so you can check there for more information.


If your problem still exists, address the [support](https://developer.unigine.com/forum/).
