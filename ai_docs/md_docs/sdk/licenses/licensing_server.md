# Licensing Server


**UNIGINE Offline Licensing Server** is a small program that runs in a console window. It lets one UNIGINE [license](../../sdk/licenses/index.md) work on all computers in your local network. You activate the license once, on one computer. That computer then gives the license out to every UNIGINE Editor, engine, or runtime application in your network. The server does not give you extra licenses: *it gives out exactly the seats and channels that are written in the license key you activate on it*.


Use the Licensing Server in these cases:


- Your project **builds the engine into your own system**, and installing and running *SDK Browser* on every computer is not realistic.
- You run [Channels](../../sdk/licenses/index.md#channel) **without USB dongles**. Here the Licensing Server takes the place of the dongle.


**Setting up takes three steps**, and you do them only once:


1. **Get the request code** of the server computer (*works only on that computer, won't activate anywhere else*).
2. **Exchange this code for a license key** on the Developer Portal.
3. **Start the server with that key.**


![](ls_first_run.png)


Before that, check the [Requirements](#requirements) and [install the tool](#where_to_get). If it is already installed and the firewall is [configured](#firewall_settings), go straight to **[Typical Set Up Scenarios](#scenarios)**.


> **Notice:** The ***My Company -> LICENSE MANAGER*** section on the Developer Portal is open only to **[Company Admin](../../sdk/licenses/admin_panel.md#roles)** users, make sure you have a proper account.


## Requirements


For a normal local network you need very little:


- **One computer to be the server** � Windows or Linux, 64-bit, and it does not need to be powerful. It has to be turned on whenever anyone needs a license, and its **clock must be correct**: set back more than two days, it stops giving out licenses to everybody at once (see [Troubleshooting: System Clock](../../troubleshooting/licensing_server.md#ts_clock)). > **Notice:** If the server computer does have the Internet, it uses it only to check from time to time whether your licenses are still valid (see [What Leaves Your Network](#network_data)). The [--server](#server_option) option chooses which UNIGINE server that check goes to; it plays no part in activation.
- **The other computers in the same subnet** as the server � workstations, render nodes, and so on. Nothing to install, activate or set up on them: they find the server by themselves. A computer that reaches your network through a router or a VPN usually cannot.
- **No Internet connection**, anywhere. The server works fully offline, and activating a key needs no Internet either: the key already carries everything the server has to know.


> **Notice:** If you are going to give out [Channels](../../sdk/licenses/index.md#channel) (e.g. you plan a stand of render nodes) for applications built on **SDK 2.21 or older**, a [special setup is required](#advanced_legacy_channels).


## Download & Install


You can get the Licensing Server in two places:


- On the **Tools** tab in *SDK Browser*. ![](sdk_tools.png)
- In the **Tools** section on the **Downloads** tab of your *[developer.unigine.com](https://developer.unigine.com)* account. ![](download_tools.png)


Choose one computer in your network to be the server (see [Requirements](#requirements)). Install the Licensing Server on that computer.


Install it into a folder **you can write to**. Do not use `C:\Program Files`. Use a folder in your user profile, or a folder you make for it, such as `C:\UNIGINE\LicensingServer`. The tool writes some of its own data next to itself while it runs, so it needs a writable folder.


> **Notice:** The Licensing Server **has to be running as long as anyone needs a license.** It is not a system service and does not start by itself after a reboot. You'll either have to restart it manually every time, or [make it start automatically](#op_autostart).


Before you start the server, let it through the firewall of that computer (see below).


### Firewall Settings


Two firewalls matter, and they need different things:


| Computer | Has to allow |
|---|---|
| **Server** | Incoming **TCP 33333** � this is how licenses are handed out. |
| **Client**-computers | Incoming **UDP 33334** � this is how it hears the server and finds it without any setup. |


If the server�s firewall blocks it, the server runs, detects this problem, and writes the corresponding messages to the console (see [Nobody Finds the Server](../../troubleshooting/licensing_server.md#ts_discovery)).


On **Windows**, the installation folder holds a script that sets up the server side for you. Run it once:


```bash
firewall_add_rule.vbs
```


It asks for administrator rights and then allows `LicensingServer.exe` to accept incoming connections, so there is nothing to enter by hand.


> **Warning:** If you dismiss the request for administrator rights, **no rule is created**. If client-computers cannot find the server afterwards, run it again and accept the request.


Next to it is a `firewall_del_rule.vbs`, which removes the rule again � for example before you move the server to another computer. Run it before uninstalling the Licensing Server: uninstalling deletes the script but leaves the firewall rule behind.


On **Linux**, or on Windows if you would rather write the rule yourself, allow incoming **TCP 33333** on the server computer. For what each port is for, see [Network Ports](#req_ports).


## Typical Set Up Scenarios


Find your case below and follow it from start to finish. If something does not work, see [Troubleshooting](../../troubleshooting/licensing_server.md). If your network is not a simple one, see [Additional Setup Instructions](#advanced).


- [Serving Seats](#scenario_seats) � your team writes and builds projects in UNIGINE and shares a set of seats.
- [Serving Channels](#scenario_channels) � a final application runs on several computers, yours or your customer's.
- [Serving Seats and Channels Together](#scenario_both) � your license has both, for example a team plus a stand of render nodes.
- [You Bought an Additional License](#scenario_new_license) � the server already works and you want to add a license to it.


### Serving Seats (Development Team)


Your team works with UNIGINE, and your license has several [Seats](../../sdk/licenses/index.md#seat). You want every developer's Editor and engine to take a seat by itself, so that you do not have to activate a license on each workstation.


1. [Install the Licensing Server](#where_to_get) on the computer you chose. On that computer, run: ```bash LicensingServer request-code ``` It prints one line that looks like ***XXXXXXXX-XXXXXXXX-XXXXXXXX-XXXXXXXX***. This is your request code.
2. Sign in to *[developer.unigine.com](https://developer.unigine.com)*. Go to *My Company -> LICENSE MANAGER* and click ***Get Code For Fixed License***: ![](license_manager_generate.jpg) Fill in the form: set **ACTIVATION TYPE** to *Licensing Server*, set **LICENSE TYPE** to *Seats*, paste your request code, choose your product and license, set how many seats to give out, and click ***Get code***: ![](get_code_ls_seats.png) Copy the code you get, or download it as a `*.key` file: ![](activation_code_for_offline.jpg)
3. Go back to the server computer and start the server with your key file: ```bash LicensingServer run --license license.key ``` A plain file name like this is looked for in the folder you run the command from. If the key is somewhere else, give the full path to it. You can pass the code itself instead of the file. The dashes inside the code do not matter: ```bash LicensingServer run --license XXXXXX-XXXXX-XXXXX-XXXXX-XXXXX ```
4. That is all. The seats are now given out over your local network. The Editors and engines in the same subnet find the server by themselves, and **you do not have to set up anything on the developers' computers**. Look at what the server prints � see [Checking That It Works](#checking). The server remembers your key, all subsequent runs after restarting it do not require [--license](#license_option).


### Serving Channels (Delivery to a Customer)


You have built an application on UNIGINE, and it has to run on several computers. This may be your own site or your customer's site. A typical case is a set of render nodes, and each of them needs a [Channel](../../sdk/licenses/index.md#channel). See also [How to Count Seats and Channels](../../sdk/licenses/channels.md).


1. [Install the Licensing Server](#where_to_get) on one computer at that site. On that computer, run: ```bash LicensingServer request-code ``` If the server stands at your customer's site, the customer sends this code to you. You then make the key for them: the channels come from **your** channel quota, under **your** portal account. Your customer needs no UNIGINE account, no access to the portal, and no Internet connection.
2. Sign in to *[developer.unigine.com](https://developer.unigine.com)*. Go to *My Company -> LICENSE MANAGER* and click ***Get Code For Fixed License***: ![](license_manager_generate.jpg) Fill in the form: set **ACTIVATION TYPE** to *Licensing Server* and **LICENSE TYPE** to *Channels*. Then choose the **CHANNEL TYPE**: *Channel IG* or *Channel VR*, depending on [which plugins your application uses](../../sdk/licenses/index.md#channel). Paste your request code, choose the product and license, set how many channels to give out, and click ***Get code***: ![](get_code_ls_channels.png) Copy the code you get, or download it as a `*.key` file: ![](activation_code_for_offline.jpg) Give the code, or the `*.key` file, to the person who runs the server.
3. On the server computer, start the server with the key file: ```bash LicensingServer run --license channels.key ``` Or with the code itself: ```bash LicensingServer run --license XXXXXX-XXXXX-XXXXX-XXXXX-XXXXX ```
4. The channels are now given out over the local network. Your application takes one channel on every computer where you start it. Look at what the server prints � see [Checking That It Works](#checking). The server remembers your key, all subsequent runs after restarting it do not require [--license](#license_option).


> **Warning:** Projects built on **SDK 2.21 or older** can take channels only on the server computer itself (see [Working With Channels for SDK 2.21 and Earlier](#advanced_legacy_channels)).


### Serving Seats and Channels Together


Your license has both [Seats](../../sdk/licenses/index.md#seat) and [Channels](../../sdk/licenses/index.md#channel), and you want one server to give out both. This is the usual case when developers and a set of render nodes work side by side: the workstations take seats, and the final application running on the nodes takes channels.


It covers two situations that look the same to the server:


- A **permanent setup of your own** � a team and a render stand that stay in place.
- A **temporary check before a delivery**, when you [test the application the way it will really run](../../sdk/licenses/channels.md#test_app) at the customer's site.


Both licenses live on the same server. You make two keys for the same request code and activate both of them at once:


![](ls_seats_and_channels.png)


1. [Install the Licensing Server](#where_to_get) on one computer and get its request code: ```bash LicensingServer request-code ```
2. On the Developer Portal (*[developer.unigine.com](https://developer.unigine.com)*), go to *My Company -> LICENSE MANAGER* and click ***Get Code For Fixed License***: ![](license_manager_generate.jpg) Set **ACTIVATION TYPE** to *Licensing Server* and **LICENSE TYPE** to *Seats*. Choose your product and license, and click ***Get code***: ![](get_code_ls_seats.png) Copy the code, or download it as a `*.key` file � for example `seats.key`. Do not activate it yet. ![](activation_code_for_offline.jpg)
3. Now make a second key for the **same** request code, this time with **LICENSE TYPE** set to *Channels*, and save it as `channels.key`: ![](get_code_ls_channels.png)
4. Go back to the server computer and activate **both keys in one command**. Repeat --license for every key: ```bash LicensingServer run --license seats.key --license channels.key ``` > **Notice:** Activate all keys in a single run, or if you do it sequentially, stop the server first (see [Stopping the Server](#op_stopping)), then run it with another key. Otherwise, all sequential runs won't work.
5. Now the server gives out both kinds of license over your local network, and it counts them separately. Workstations take seats, render nodes take channels. The server prints both numbers when it starts � see [Checking That It Works](#checking). The server remembers your keys, all subsequent runs after restarting it do not require [--license](#license_option).


> **Notice:** Which of the two a program gets is decided by **the program, not by the server**. The Editor and the engine take seats, while a final application built for channels can take a channel, or a seat (vacant only).


#### Releasing Channels


**If this was a temporary check before a delivery, give the test channels back.** The channels you used for testing come from the same quota you sell to customers from, so release them when you are done and they can go to a real customer.


> **Warning:** **You can release only one license key a day, only 5 times a year.**
>
>
> Do this only for channels you no longer need. If the stand is a permanent setup of your own, keep the channels: releasing them stops the nodes that are using them.


To release them, open the **[LICENSE MANAGER](../../sdk/licenses/admin_panel.md#license_manager)**. Find the pack of *Activated Channels*, or a single channel, in the matching section and click ***Release***:


![](release_channels.png)


After that you can issue these channels again, as described in [Serving Channels](#scenario_channels).


### You Bought an Additional License


The server already works and gives out licenses, and you have bought one more license: more seats, a pack of channels, or another product edition. To add it, you go through the same steps once more.


**Keys add up.** Every key you activate keeps its own places, and the server hands out all of them together. If a product already has a 10-seat key on the server and you activate a 5-seat key for it, you get **15** seats.


1. You need the request code of the server computer � the same one your other licenses were made for. If you did not keep it, get it again. It is always the same on the same computer: ```bash LicensingServer request-code ```
2. On the Developer Portal (*[developer.unigine.com](https://developer.unigine.com)*), go to *My Company -> LICENSE MANAGER* and click ***Get Code For Fixed License***: ![](license_manager_generate.jpg) Set **ACTIVATION TYPE** to *Licensing Server* and make a key for the new license, for that request code. Set **LICENSE TYPE** (Channels, for example), **PRODUCT** and **LICENSE** to match what you bought: ![](get_code_ls_channels.png) Copy the code, or download it as a `*.key` file: ![](activation_code_for_offline.jpg)
3. Your server is already running, and a second copy of it does not start. So **stop it first** � press **Ctrl+C** in its console window (see [Stopping the Server](#op_stopping)) � and then start it once with the new key: ```bash LicensingServer run --license new.key ``` The server keeps the new license next to the ones it already has, and prints the new numbers when it starts. From then on, plain LicensingServer run is enough again. > **Notice:** Everybody loses their license for the few seconds the server is down, and picks it up again once it is back. Do this when nobody is in the middle of something important.


## Checking That It Works


When the server starts correctly, it prints something like this:


![](license_server_check.png)


A few lines are worth reading every time.


The License: line shows what the server is going to give out: the product, the number of seats: and channels:, and the date the license expires. These numbers come from the key itself, so compare them with what you ordered.


> **Notice:** There is **one such line per key**. If you activated several keys you get several lines � including additional lines for the *same* product, if you bought more places for it (in this case the places add up, so the server hands out the total of those lines).


The Serving licenses on ... line means that the server is listening and telling the network it is there. Now the other computers can find it.


After that the server prints a line every time somebody takes a license or gives it back. Every line names the machine and the address it came from, which makes this the easiest way to see who is using your licenses right now:


```bash
[...] (info) <LicensingServer> Seat acquired: "UNIGINE 2 Sim" by machine <id> from 192.168.1.24:51314
[...] (info) <LicensingServer> Seat released: "UNIGINE 2 Sim" by machine <id> from 192.168.1.24:51314
```


Channels are logged the same way, as Channel acquired: and Channel released:.


> **Notice:** **Do not close the console window.** If you close it, the server stops, and everybody using it loses the license.


If you set the server to [start automatically](#op_autostart), there is no console window to watch. Everything described above is written to the log file just the same (see [Where the Logs Are](../../troubleshooting/licensing_server.md#ts_logs)).


If the server does not start, if it refuses a license, or if the other computers do not find it, look up the message it printed in [Licensing Server Issues](../../troubleshooting/licensing_server.md). Every message is listed there with what to do about it.


## How Licenses Are Handed Out


### How a Computer Gets a License


It happens in five steps:


![](ls_seat_lifecycle.png)


1. **The server says it is there.** While the server runs, it sends a short message to your local network about once a second (UDP port 33334). The other computers listen for this message. This is why you do not have to set up anything on them.
2. **A program asks for a license.** When a UNIGINE Editor, engine, or final application starts, it connects to the server (TCP port 33333) and asks for a license for its product.
3. **The server answers.** First it makes sure its own clock can be trusted; if it cannot, every request is refused and nothing below is even looked at (see [Troubleshooting: System Clock](../../troubleshooting/licensing_server.md#ts_clock)). Then it checks three things: that it has a license for this product, that the license has not expired, and that one place is still free. If all three are fine, it writes the computer down and answers yes. If not, it answers with the reason (see [Messages on Consumer Machines](../../troubleshooting/licensing_server.md#ts_consumer)).
4. **The license stays taken while the program runs.** The connection stays open until the program closes. **This open connection is the license.** There is nothing to renew, and no license file appears on the other computer.
5. **Closing the program gives the license back.** The connection closes, and the place becomes free at once.


Three things follow from this.


The other computers hold nothing while they are not working. Nothing is installed on them and nothing is activated on them. If you retire a workstation, there is nothing to clean up.


The server keeps the list of taken places in memory only. It never writes it to disk. That is why stopping the server takes the licenses away from everybody at once, and why starting it again frees all the places.


If a computer switches off suddenly � the power goes out, somebody pulls the cable, a virtual machine is killed � the server does not notice at once. It keeps the place as taken until the operating system reports the connection as dead, and that can take a couple of hours. To free such places right away, restart the server.


> **Notice:** A UNIGINE program running on the server computer itself also asks the server for a license and takes a place, just like any other computer.


### How Many Computers One License Serves


As many as there are **places in the keys you activated**, added up per product.


**Keys for one product share a pool**, and every product has its own. A 3-seat and a 4-seat key for Sim make a pool of 7. A 10-seat Sim license next to a 4-seat Engineering license is not a pool of 14 that anybody can draw from � it lets 10 computers work with Sim and 4 with Engineering.


What the server will really hand out is printed when it starts, on the License: lines (see [Checking That It Works](#checking)). There is one line per key, so add the lines of the same product together. For channels the type is shown in brackets after the number:


```bash
License: "UNIGINE 2 Sim" | seats: 5 | channels: 0 | expires: 2027-01-31
License: "UNIGINE 2 Sim" | seats: 0 | channels: 8 (IG) | expires: 2027-01-31

```


How many places you need in the first place, and how they are counted against your computers and applications, is explained in [How to Count Seats and Channels](../../sdk/licenses/channels.md).


### When All Seats or Channels Are Taken


If every place is taken, the next computer does not get a license. The program says that **your license does not have more**.


There is no queue and no waiting list. As soon as somebody closes their program, the place becomes free, and the next attempt succeeds. So the computer that was refused just has to start the program again.


> **Notice:** If **every** computer is refused at once, including ones that were working a minute ago, the places are probably not the reason. Check the clock of the server computer, and see other reasons in the [Troubleshooting](../../troubleshooting/licensing_server.md) section.


## Everyday Operation


**Starting the server again**, no key required, as the server remembers the ones you have activated before. Run:


```bash
LicensingServer run
```


You do this after the server computer restarts. The Licensing Server is not a service, so it does not come back by itself. Until somebody starts it, nobody in the network can get a license. To take this off your hands, set the computer to [start the server automatically](#op_autostart).


Restarting the server is also the fastest way to free places that are still held by computers that are already gone. It is not free, though: see [Stopping the Server](#op_stopping) for what happens to the people working at that moment.


**Adding another license.** See [You Bought an Additional License](#scenario_new_license).


**Moving the server to another computer.** There is no command to deactivate a license. A key belongs to the hardware it was made for. If you change the computer, or reinstall the operating system, the old key stops working there. Get a new request code on the new computer and ask for a new key for it.


**Running the server next to SDK Browser.** The Licensing Server and *SDK Browser* cannot both give out licenses on the same computer, because they use the same port. Close *SDK Browser*. If you need both, see [SDK Browser & Licensing Server in One Network](#sdk_bro_licensing_server).


**Starting from scratch.** [Stop the server](#op_stopping) and delete its configuration file (`%APPDATA%\unigine\LicensingServer.json` on Windows, or `~/.config/unigine/LicensingServer.json` on Linux). This file holds the activated licenses, so deleting it removes them. After that, activate a license again with --license, as you did the first time.


You can always look up your activation code on *[developer.unigine.com](https://developer.unigine.com)*, in *My Company -> LICENSE MANAGER*:


![](activation_code.png)


### Stopping the Server


To stop the server, press **Ctrl+C** in its console window. Closing the window does the same thing.


You need this when you [add a license](#scenario_new_license), [update the tool](#updates), or start from scratch � in all these cases the server has to be stopped and started again, because a second copy of it does not run.


> **Warning:** Stopping the server takes the license away from **everybody** at once, immediately. Stop it when nobody is in the middle of something important.


To be precise about what a restart costs:


- **All places are freed at once**, including those still held by computers that are already gone. This is why a restart is the quickest way to clean them up.
- **Programs that are running lose their license.** An Editor or an application open at that moment does not quietly wait for the server to come back � treat it as work interrupted, and expect to start it again.
- **Anything started afterwards is served normally.** Once LicensingServer run is up again, every computer takes its place as usual, with nothing to set up.


## Updates


To update the Licensing Server, [download the new version](#where_to_get) and install it over the old one. [Stop the server](#op_stopping) first � and if it runs from the [autostart](#op_autostart), stop that task too, or the files being replaced are still in use.


**You do not have to set anything up again, and all your activated licenses stay.** So after the update you simply start the server:


```bash
LicensingServer run
```


## SDK Browser & Licensing Server in One Network


In one local network, licenses can come from more than one place at the same time. There are three kinds of source:


- *SDK Browser* with an ordinary [activated license](../../sdk/licenses/activation.md). It serves **only the computer it runs on**.
- The **Licensing Server**. It serves **the whole local network**.
- *SDK Browser* with a [USB dongle (HASP) license shared over the network](../../sdk/licenses/activation.md#license_broadcasting). It also serves the whole local network. This article calls it a *broadcasting* SDK Browser.


![](ls_network_sources.png)


These sources can work in one network together, and you do not have to set up anything special. But it is recommended to follow one rule: **in one network, one product should come from one source only.**


Here is why. If two sources offer licenses for the same product, you cannot tell which one a program will use. A program may even be refused by the source it happened to reach, while the other source still has free places. If you cannot avoid having two sources for one product, tell each computer which source to use. This is done with the -licensing_host argument � see [Custom Address and Port](#advanced_host).


The sections below describe the usual combinations. But first, one thing that only happens when two programs run on **the same computer**.


> **Notice:** On the server computer it is fine to open *SDK Browser* from time to time (e.g., to download an SDK or a tool) **only when the Licensing Server is already running**, not the other way round. And do not plan to *work* on this computer under the Browser's own license.


### Local SDK Browser License Next to a Licensing Server


Your workstation runs *SDK Browser* with a license [activated for this computer only](../../sdk/licenses/activation.md). Somewhere in the same network, a Licensing Server gives out licenses to the rest of the team.


You do not have to set up anything. The two do not get in each other's way:


- Programs on **your computer** use your own license. Keep *SDK Browser* running as usual. Your computer does not take a place on the Licensing Server.
- Your license stays yours. An *SDK Browser* with an ordinary license (not a dongle one) does not tell the network it is there, and never gives licenses to other computers.
- Computers that have **no** license of their own take their places from the Licensing Server, as usual.


> **Notice:** Your own license may not cover everything. If you start a UNIGINE program for a product your license does not include, it can take a place from the Licensing Server, just like any other computer in the network. Your computer then holds that place until you close the program.


### Several Licensing Servers in One Network


You can run several Licensing Servers in one network, **each on its own computer**. Nothing special is needed: every server tells the network it is there and gives out its own licenses.


> **Notice:** Two Licensing Servers cannot run on the same computer. The second one does not start and prints Another Licensing Server instance is already running on this machine. Stop it before starting a new one.


The servers know nothing about each other, and their licenses are never added together. Ten seats on one server plus ten seats on another are two separate sets of ten, not one set of twenty.


**Give each server a different product** (e.g., one for Sim, and the other for Engineering). Then every program simply ends up on the server that has a license for its product, and the counting stays clear.


> **Warning:** Do not serve **one** product from two servers **to get more places** � pools on different servers never add up, and a computer refused by one server does not try the other. If you need more places, activate the new key on the server you already have (see [You Bought an Additional License](#scenario_new_license)). Two servers with the same product are workable only as a deliberate split, with every computer pointed at its server explicitly (see the rule above and [Custom Address and Port](#advanced_host)).


### Licensing Server and Broadcasting SDK Browser on Separate Machines


A USB dongle (HASP) license with several seats can be [shared over the network](../../sdk/licenses/activation.md#license_broadcasting). You put the dongle into one computer and run *SDK Browser* there. That *SDK Browser* then tells the network it is there and gives out the dongle license to the other computers. For them it works just like a small licensing server: they get the license by themselves, with nothing to install and nothing to set up.


> **Notice:** *IG Channel* and *VR Channel* USB dongles cannot be shared over the network. Only dongles with several seats can.


Such an *SDK Browser* and a Licensing Server can serve one network at the same time, each on its own computer. If they hold licenses for **different products**, you do not have to set up anything: the dongle seats come from the Browser computer, and everything else comes from the Licensing Server. If they hold licenses for the same product, follow the one-source-per-product rule at the top of this chapter.


> **Warning:** Never run an *SDK Browser* with a dongle on the **same computer** as the Licensing Server � the setup breaks.


## Additional Setup Instructions


This chapter is for specific setup cases: legacy channel licenses, closed networks, custom ports, computers you cannot copy text from.


### Working With Channels for SDK 2.21 and Earlier


On SDK 2.21 and older, channel licenses are given out differently: an application can take a channel **only on the server computer itself**.


You have two ways around this.


1. **[Install the Licensing Server](#where_to_get) on every computer.**
2. **Redirect the licensing port on every computer that needs a channel.** Every UNIGINE program starts by looking for a license at 127.0.0.1:33333, that is, on its own computer, and only then listens for the announcement. You make that first address lead to the server instead, and the application does not notice the difference. In the commands below, replace <server_ip> with the IP address of the computer that runs the Licensing Server. Replace <port> with the licensing port. It is 33333, unless you moved the server to a [custom port](#advanced_host). > **Notice:** While this rule is in place, licensing through *SDK Browser* on this computer **does not work**. It works again after you remove the rule. On **Windows**, open a terminal **as Administrator** and run: ```bash netsh interface portproxy add v4tov4 listenaddress=127.0.0.1 listenport=<port> connectaddress=<server_ip> connectport=<port> ``` On **Linux**, run: ```bash sudo sysctl -w net.ipv4.conf.all.route_localnet=1 sudo iptables -t nat -A OUTPUT -p tcp -d 127.0.0.1 --dport <port> -j DNAT --to-destination <server_ip>:<port> sudo iptables -t nat -A POSTROUTING -p tcp -d <server_ip> --dport <port> -j MASQUERADE ``` You can close the terminal after you enter the commands. The redirection stays. From now on, the application on this computer takes its channel from the server as if the license were its own.


### Writing the Request Code to a File


By default the request code only appears in the console. You can write it to a file instead. Add a file name to the command:


```bash
LicensingServer request-code code.txt
```


The file then holds the code on a single line. This is handy when the console is hard to copy from, or when you have to carry the code on a USB stick.


> **Notice:** If the file already exists, it is **overwritten without a question**. If you give a name without a path, the file appears in the folder you ran the command from. If the file cannot be written, the tool explains why (Cannot write the request code to ...) and stops without printing the code anywhere.


### Starting the Server Automatically


The Licensing Server is not a service and does not come back after a reboot. If the server computer restarts at night, nobody in your network can get a license in the morning until somebody logs in and starts the tool by hand. Set up the autostart once and this stops being your problem.


On **Windows**, use *Task Scheduler*. Create a task with these settings:


- **Trigger**: *At log on*.
- Select: *Specific User* and choose your user account.
- **Action**: *Start a program*, the program being your `LicensingServer.exe`, with run in the arguments field.
- **Start in**: the folder you installed the tool into. Without this the tool starts in the wrong folder.
- On the **General** tab, choose *Run whether user is logged on or not*, so that the server works when nobody is logged in. Leave the account itself as **the user who activated the license** � see the warning below.


> **Warning:** **The task must run under the same user account that activated the license.** The activated keys are kept in that account's profile, not in a shared place on the computer.
>
>
> The *Run whether user is logged on or not* setting is also where it is easy to switch the task to SYSTEM or to a separate service account. Do not. Such a task starts with an empty configuration and stops at once with:
>
>
> ```bash
> No active license. Pass --license <code-or-file> to activate one; this is only needed the first time.
> ```
>
>
> The license is fine � the task is simply looking in another profile. If you need the server to run under a different account, activate the key again while logged in as that account.


On **Linux**, make a **user** service � not a system one, and under the same user that activated the license, for the same reason. Put this into `~/.config/systemd/user/licensing-server.service`, with the path replaced by your own:


```bash
[Unit]
Description=UNIGINE Licensing Server

[Service]
ExecStart=/home/user/LicensingServer/LicensingServer run
Restart=on-failure

[Install]
WantedBy=default.target

```


Then turn it on, and allow it to work while you are logged out:


```bash
systemctl --user enable --now licensing-server
sudo loginctl enable-linger $USER

```


> **Notice:** Started this way, the server has no console window you can look at. To check that it is working, and to see who is taking licenses, read its log file instead (see [Where the Logs Are](../../troubleshooting/licensing_server.md#ts_logs)).


The autostart runs LicensingServer run without --license, which is exactly right: the licenses are already stored on the machine. When you [add a license](#scenario_new_license) later, stop the task, activate the new key by hand once, and start the task again � or simply add another --license to the task's arguments, since a code that is already activated is passed over on every later start.


### Custom Address and Port


By default the server listens on 0.0.0.0:33333. You can bind it to one network interface, or move it to another port. For example, do this when *SDK Browser* already holds the default port:


```bash
LicensingServer run --licensing-host 0.0.0.0:33400
```


Use an IP address or localhost. Host names do not work here.


> **Notice:** Moving the server to another port does **not** mean you have to visit every computer. Whatever port the server listens on, it always announces itself on **UDP 33334**, and the announcement carries that port. The other computers read it and connect to the right place by themselves.


**Telling a computer which server to use.** You name the address yourself in two cases: when you started the server with --no-broadcast, because then nothing is announced, and when there are several sources and you want one particular computer to use one particular source.


This is the -licensing_host startup argument. It works the same way for *UnigineEditor*, for the engine, and for your final application � so a render node is pointed at the server exactly like a workstation:


```bash
MyApplication.exe -licensing_host 192.168.1.10:33400
```


The port is optional. -licensing_host 192.168.1.10 means that computer on the default port.


> **Notice:** The two names look alike, and they are not the same thing. --licensing-host, with two dashes, is an option of the **server** and says where to listen. -licensing_host, with one dash and an underscore, is a startup argument of a **consumer** program and says where to look.


A computer that was given this argument tries that address **first**, and only falls back to the announcement if nothing answers there. Note that it does not fall back to a server it has already failed to reach: if you name an address where no server is running, and the announcement points at that same address, the computer stops and reports that it has no license.


When a computer finds its server through the announcement, the engine writes this line in its own log:


```bash
Engine connects to 192.168.1.10:33400 licensing server
```


That is the way to see which server a particular computer actually reached.


See also [SDK Browser Issues](../../troubleshooting/browser_issues.md#licensing).


You can also stop the server from telling the network it is there. Add --no-broadcast, for example in networks where such messages are not welcome. Use it only when every computer already knows the server's address.


## Command Reference


The Licensing Server has two commands:


- LicensingServer request-code [file] � print the request code of this computer and exit. If you name a **file**, the code is saved to that file instead.
- LicensingServer run [options] � give out the activated licenses over the local network.


The options below work with run only. The request-code command takes an optional file name and nothing else.


| Option | Description |
|---|---|
| --license <code-or-file> | An activation code, or a path to a license file. The file is plain text with the code on the first line, usually `*.key`. A plain file name is looked for in the folder you run the command from; give a full path if the key is elsewhere. Dashes inside the code do not matter. Repeat the option to activate several licenses in one run. Needed only the first time. |
| --server <server> | Which UNIGINE server to contact for the periodic check that your licenses are still valid: global, china, eastern_europe. Choose the one nearest to you. Activation itself is done offline and does not use this option. ***Default:*** global |
| --licensing-host <address[:port]> | The address and port to listen on. An IP address or localhost; host names do not work. ***Default:*** 0.0.0.0:33333 |
| --no-broadcast | Stop telling the network that the server is here (UDP 33334). By default the server does tell. Use this option only when every computer already knows the server's address. |
| -h, --help | Show help. |
| -v, --version | Show the version. |


## What Leaves Your Network


The Licensing Server works fully offline. If it can reach the Internet, it contacts the [UNIGINE server](#server_option) from time to time to check whether your licenses are still valid. It sends three things:


- the request code of the computer, which describes its hardware,
- the version of the tool,
- the list of activated license codes.


Nothing else is sent: no project data, no file names, no personal information.


If the computer has no Internet access, this check simply fails and is repeated later. Your licenses keep working until the date written inside the key.


## Network Ports


The Licensing Server uses three network ports. These are the default values; you can change the address and the port it listens on � see [Custom Address and Port](#advanced_host). What each computer has to allow through its firewall is in [Firewall Settings](#firewall_settings).


| Port | Direction | What it is for |
|---|---|---|
| 33333 (TCP) | Client-computers -> Server | The licenses are handed out over this port. |
| 33334 (UDP) | Server -> your LAN | The server announces itself, so the other computers find it without any setup. |
| 443 (HTTPS) | Server -> `sdk-browser-api*.unigine.com` | Optional. Used only to check whether your licenses are still valid (see [What Leaves Your Network](#network_data)). |


> **Notice:** The server and client-computers must stay connected all the time they work. If the connection breaks, the license goes back to the server and can be taken by somebody else.
