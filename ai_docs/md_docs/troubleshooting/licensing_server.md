# Licensing Server Issues


This section provides information on typical errors related to **[UNIGINE Offline Licensing Server](../sdk/licenses/licensing_server.md)** and explains how to fix them.


## Where the Logs Are


Several problems below end with "contact support with the logs". The Licensing Server writes its logs here:


| Platform | Log location |
|---|---|
| Windows | `%LOCALAPPDATA%\unigine\LicensingServer\licensing_server_0.log` |
| Linux | `~/.config/unigine/LicensingServer/licensing_server_0.log` |


The run command prints the exact path at startup on the Log filepath: line; request-code does not print it, so use the table above.


**Collect the logs before you retry.** Three files are kept (`licensing_server_0.log` to `licensing_server_2.log`), and every start of the tool shifts them one position down and opens a fresh, empty `_0` � so after three more starts the log with the failure is gone:


![](ls_log_rotation.png)


When contacting support (*[licensing@unigine.com](mailto:licensing@unigine.com)*), attach all three files, not only `_0`. On Windows, the following command packs them into an archive on your desktop:


```bash
Compress-Archive "$env:LOCALAPPDATA\unigine\LicensingServer\licensing_server_*.log" "$env:USERPROFILE\Desktop\licensing-server-logs.zip"
```


## Messages from the Licensing Server


| Message | What Happened | What to Do |
|---|---|---|
| Cannot obtain this machine's hardware information. To fix the problem, please refer to the Troubleshooting section of the documentation: ... Error code <code>. | The tool could not read the hardware identifiers it needs. This stops both request-code and run, so it can appear when you generate the code and when you start the server. | Contact support with the error code printed in the message and the [log files](#ts_logs) � collect them before retrying. |
| Cannot read an activation code from <file>. The file must be plain text with the code on its first line. | The path was found, but the first line was empty or unreadable. | Open the file: it must contain the activation code as plain text. A wrong path also lands here � anything with a dot or a slash is treated as a path. |
| Cannot write to the installation directory <dir>. Reinstall the Licensing Server into a writable location. | The tool cannot write next to its own executable. | Move it out of `Program Files` into a writable folder. |
| Cannot use '<value>' as --licensing-host. ... | The address could not be parsed. | Use an IPv4 address or localhost, optionally with :<port>. Host names are not supported. |
| Cannot listen on <address>:<port>. The port is most likely taken ... | Another program holds the port � usually SDK Browser or a second Licensing Server. | Close the other program, or pass a different port with --licensing-host (see [Custom Address and Port](../sdk/licenses/licensing_server.md#advanced_host)). |
| Unknown --server value '<value>'. ... | Typo in --server. | Use global, china, or eastern_europe. |
| Offline activation failed for code <code>: the activation code is invalid | The code does not decode on this machine. | Most often the key was issued for a **different machine's** request code. Also check for a typo, and confirm the key has not been revoked. |
| Offline activation failed for code <code>: the activation code is already activated | The same activation code was supplied twice � for example it is still in a startup command after the first run. | Nothing to do. The license from that code is already in force, and the server carries on. Keys for one product add their places together, so an *extra* key is never rejected on these grounds � only the very same code. |
| No active license. Pass --license <code-or-file> to activate one; this is only needed the first time. | No stored license, and none supplied. | Run once with --license. |
| Another Licensing Server instance is already running on this machine. Stop it before starting a new one. | The tool is already running under your user account. | Use the existing one, or stop it first. |
| Licensing stopped: the system time is incorrect. Correct the system time or connect this machine to the internet to verify the current time. | The clock of this machine is set back more than two days from the latest date the server has seen. Licensing is suspended for the whole network, and every consumer is refused � including those that were already working. The server keeps running, and its earlier Serving licenses on ... line stays on screen, so nothing else signals the problem. | Set the clock correctly, or connect the machine to the Internet so it can verify the time. The server recovers by itself � see [System Clock](#ts_clock). |
| Licensing resumed. | The clock is trusted again after a Licensing stopped. | Nothing. Licenses are given out again from this moment; consumers that were refused have to be started again. |
| License deactivated: <product> | The license was revoked centrally, and the server saw it during a periodic check. | Contact whoever issued the key. |


## Messages on Consumer Machines


| Message | Cause |
|---|---|
| License for the current SDK version not found. | No license for that product on the server. Also what an **Editor** gets when the server holds only a [channel key](../sdk/licenses/licensing_server.md#scenario_channels). |
| Your license does not have more seats. | All seats or channels are in use. Free one, or get a larger license. There is no queue: the refused machine succeeds as soon as somebody else's application exits. |
| Your license does not cover the requested channel type. | The application requests an **IG** channel, but the key on the server holds **VR** channels only (a **Channel IG** key, by contrast, covers VR applications as well). Have a key issued with the **CHANNEL TYPE** matching the [plugins the application uses](../sdk/licenses/index.md#channel). |
| License expired. | The license's expiration date has passed. |
| Licensing is temporarily unavailable because the date and time on the machine serving the license appear to be incorrect. ... | The clock on the **server** machine is set back too far, so it has suspended licensing for everyone. Nothing is wrong with this consumer. Fix the clock on the server machine � see [System Clock](#ts_clock). |
| License broadcast over the network is forbidden. | The consumer reached a plain **SDK Browser** instead of the Licensing Server. Only the Licensing Server may serve licenses over the network (a [dongle](../sdk/licenses/activation.md#license_broadcasting) being the exception). |
| Unknown product, please update SDK-Browser. | The consumer's SDK build is newer than this Licensing Server knows about. Update the Licensing Server. |


## Nobody Finds the Server


1. Confirm the server prints Serving licenses on ... broadcasting on UDP 33334.
2. Check that inbound TCP 33333 is allowed on the server machine.
3. Confirm the consumers are on the **same subnet**. Broadcast does not cross routers or, usually, VPN links.
4. If the server is bound to one specific address, make sure that interface actually supports broadcast � point-to-point and VPN interfaces often do not, and then nothing is announced at all.


## System Clock


The server keeps track of the highest date it has ever seen, so that a license cannot be extended by setting the system clock back. Moving the clock backwards never restores an expired license.


Beyond a certain point (more than two days) the server stops trusting its own clock. If the system time is set back **more than two days** from the highest date the server has seen, it suspends licensing completely:


- Every place is released at once, so consumers that were already working lose their licenses too.
- Every new request is refused, whatever the license says.
- The server prints Licensing stopped: the system time is incorrect. ... and **keeps running**. The Serving licenses on ... line from startup stays on screen, so the console still looks healthy.
- Consumers get a message naming the *server* machine, not their own.


To recover, set the machine's clock correctly, or connect it to the Internet so it can verify the time. Nothing has to be restarted: the server rechecks about every fifteen minutes, and at once if it reaches the Internet. It then prints Licensing resumed. and serves licenses again. Programs refused in the meantime have to be started again.


> **Notice:** This is worth knowing before you put the server on a machine with no Internet and no battery-backed clock. Such a machine can come back from a reboot with a date far in the past, which suspends licensing for the whole network until somebody sets it.
