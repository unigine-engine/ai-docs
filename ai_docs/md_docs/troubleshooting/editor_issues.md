# UnigineEditor Issues


This section provides information on typical errors displayed in UnigineEditor and explains how to fix them.


## Editor Errors


### License for current version is not found


![](error_1.png)


If UnigineEditor displays an error saying that the license for the current version is not found, this may be caused by either of the following reasons:


- SDK is not [activated](../sdk/index.md#activate_sdk). Go to the *SDKs* tab and click the *Activate* button for the required SDK. ![](../sdk/activate_sdk.png)
- You might be logged off. Check SDK Browser for error messages: ![](session_expired.png) Click *Ok* and sign in to continue working.
- SDK Browser is opened twice on your computer or your account is used by someone else. Close any extra running instances.


### Failed to get license information


**SDK Browser should be running**, when you work in UnigineEditor. Otherwise, you may encounter the following error: *"Failed to get license information: connection with SDK Browser was lost."*


![](error_2.png)


Re-open SDK Browser and log in to continue working.


> **Notice:** If the problem persists, **ensure that your antivirus software is not blocking the connection** between *UnigineEditor* and *SDK Browser*.


### Your license does not have more seats


All [seats](../sdk/licenses/admin_panel.md#seats) available for your company under the current license are allocated to users. Request the user with the *[Company Admin](../sdk/licenses/admin_panel.md#roles)* role to reallocate a seat for you.


![](error_seats.png)


### Failed to connect to SDK Browser


You may encounter the following error: *"Failed to connect to SDK Browser: SSL verification failed."*


![](ssl_verirfication_failed.png)


In this case the following should be checked:


- **Ports and firewall settings**. UNIGINE SDK Browser uses TCP Port **33333** by default to communicate with UNIGINE Editor, so make sure it is available. You cal also [specify a custom licensing port](../troubleshooting/browser_issues.md#licensing). > **Notice:** Host and port **must be set for both** *SDK Browser* and Editor. Sometimes TCP Port 33333 may be occupied by other software (for example, *Goodsync* server, *Yeelight* solutions, etc.), or antivirus software can block this port. To check all open TCP ports, you can use: If this is the case, close the program that uses TCP Port 33333, and start UNIGINE SDK Browser.

  - On Windows - ***Resource Monitor***, a built-in utility. You can open it via the Start menu, or from Task Manager's *Performance* tab and sort by *Port* to see if SDK Browser is the only user of this port. ![](resource_monitor.png) *Checking the port used by SDK Browser in Resource Monitor*
  - On Linux - the following command: ```text sudo netstat -nltup ```
- A certain **application may block communication between SDK Browser and Editor**. To check if this is the issue, boot into a safe mode (for example, [*Windows 10* safe mode (with Networking)](https://support.microsoft.com/en-us/help/12376/windows-10-start-your-pc-in-safe-mode)) and try to run SDK Browser and Editor. SDK Browser can load a little bit slower here, please wait. If there are no errors, that would mean that some application running in normal *Windows* boot is blocking communication between SDK Browser and Editor.


If your problem still exists, address the [support](https://developer.unigine.com/forum/).


UNIGINE logs errors to the console and the main log file (stored in `<UserProfile>/AppData/Local/Unigine_SDK_Browser` for *Windows* or `.local/share/Unigine_SDK_Browser` for **nix* systems), so you can check there for more information.


## Performance Drop


The antivirus always-on protection feature can cause a significant performance drop. There are two ways to solve this issue:


- Add the project directory as an [exclusion](../troubleshooting/antivirus/index.md#exclusion). You can make the antivirus ignore certain directories and fix the issue.
- Disable the antivirus. However, keep in mind that disabling the protection system makes your system unprotected from web threats. Therefore, ensure alternative protection.
