# IG Control Panel

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


*IG Control Panel* is a cross-platform (Windows and Linux) system for managing projects and launching applications on a set of runtime nodes. From a single operator machine you synchronize a project to the nodes, start engine processes on them, monitor their state, stop or kill them, and power the nodes off at the end of a shift.


Typical use cases include **CAVE** systems, **Wall** (video wall) configurations, and other multi-screen installations, where each machine runs its own application instance with its own arguments.


![](ig_control_panel_scheme.gif)


The system consists of two components:


- **Operator** - the orchestrator (*IGControlPanel*) plus the CLI (`igctl`). One per cluster, installed on the operator's machine.
- **Agent** - *IGControlPanelAgent*, installed on every runtime node.


The CLI is shipped with the operator package; it does not need to be installed separately.


> **Notice:** *IG Control Panel* is a standalone tool distributed separately from the engine.


The tool is available in the *SDK Browser*, on the *Tools* tab. A single archive contains both installers - for the operator and for the agent - along with the `USER_GUIDE.md` manual covering installation, daily operation, and troubleshooting in detail.


## Quick Start


A step-by-step checklist to get the tool running. Each step links to the section with the details.


1. Download *IG Control Panel* from the *SDK Browser* (the *Tools* tab) and unpack the archive. ![](sdk_tools.png)
2. Install the operator on the operator PC and an agent on every runtime node using the provided installers, filling in the installer parameters - in particular, the operator's LAN address on each agent ([Windows](#install_windows) or [Linux](#install_linux)). Agents register with the operator automatically on start.
3. Log on at each node as the user that will run the application. The agent starts with that session - on Windows about 30 seconds after logon - and only then does the node appear on the operator PC.
4. [Verify the setup](#install_verify) - run `igctl status` and `igctl nodes status` and check that the nodes are online.
5. Add your [project](#cli_projects) with `igctl add`.
6. Set the [launch profile](#cli_launch_profile) with `igctl set` - the executable, working directory, and arguments.
7. [Synchronize](#sync) the project to the nodes with `igctl sync`.
8. [Launch](#cli_run) the application on the nodes with `igctl run`.


At the end of a shift, [power the nodes off](#cli_shutdown) with `igctl shutdown` and wake them again next time with `igctl wakeup`.


## Installation


The archive contains a ready-made package for the operator and one for the agent:


- On **Windows** - `igctl-operator-setup-<version>.exe` and `igctl-agent-setup-<version>.exe`.
- On **Linux** - `igctl-operator-linux.tar.gz` and `igctl-agent-linux.tar.gz`, each containing the install scripts.


**Runtime prerequisites:**


- **Permanent IP addresses** for the operator PC and for every node - static, or reservations on the DHCP server. Addresses are recorded during installation and are never detected again at start. > **Notice:** A changed address breaks the link until the installer is run again on the computer that changed: the agent keeps dialing the old operator address, and the orchestrator keeps dialing the old node address. If the operator PC changes its address, all nodes go *OFFLINE* at once; if a node changes its address, only that node is affected. > > > For **svn** projects the operator address is also stored in the repository URLs, which the installer does not rewrite. Correct *svnBaseUrl* and the *repositoryUrl* of every project in the [orchestrator config](#install_files), then restart the service.
- **svn** sync mode requires the Subversion CLI in `PATH`: on the operator PC - *svn + svnadmin + svnserve*; on a node - only *svn*. SVN is not bundled. The **manual** mode does not need SVN at all.
- **Windows:** administrator rights for installation (service / scheduled task / firewall). The agent runs in the user session so the engine can open a GUI window; that user should also be a local administrator, otherwise the agent writes no log.
- **Linux:** *root* for installation; *systemd*; a graphical session for the runtime user; *polkit* (poweroff without root); *ufw* or *firewalld*.
- **Wake-on-LAN** (optional, for `igctl wakeup`): WoL enabled in BIOS/UEFI and in the NIC settings (wired Ethernet).


### Network Ports


The installers open the ports below and restrict the rules to the local subnet:


| Port | Open on | Used for | Needed |
|---|---|---|---|
| 5100 TCP | Operator PC | Agents and `igctl` connect to the orchestrator: registration, status and commands. | Always |
| 3690 TCP | Operator PC | Nodes download project files from *svnserve*. | **svn** sync mode only |
| 5200 TCP | Every node | The orchestrator sends commands to the agent. | Always |
| 9 UDP | Every node | Wake-on-LAN magic packet. | `igctl wakeup` only |


The HTTP ports (5100 and 5200) are set in the installer. The *svnserve* port is changed in the orchestrator configuration, not in the wizard, and UDP 9 is fixed by the Wake-on-LAN standard.


> **Notice:** There is no authentication and no user accounts: any computer that can reach these ports can send commands, including `shutdown`. Keep the cluster in a separate, trusted network segment.


### Windows (MSI)


Run `igctl-operator-setup-<version>.exe` on the operator PC and `igctl-agent-setup-<version>.exe` on each node. The operator is installed as a **Windows Service**, the agent as a **scheduled task on user logon** (so the engine window starts in the user session).


> **Notice:** A node with nobody logged on runs no agent: the computer is on, but the node reports *OFFLINE* and accepts no commands.
>
>
> Set up **automatic logon** for the user that runs the application. It is required for `igctl wakeup`; without it, somebody has to log on at every node at the start of a shift.


Key operator parameters:


| Parameter | Default | Purpose |
|---|---|---|
| HTTP port | 5100 | Orchestrator HTTP listen port (bind is always *0.0.0.0*). |
| SVN repository root | D:\IGControlPanel\Repositories | Folder for bare SVN repositories (must differ from project working folders). |


Key agent parameters:


| Parameter | Default | Purpose |
|---|---|---|
| Node name | computer name | Name the node is registered under. |
| Role | unspecified | Node role, e.g. *left/center/right*. |
| Agent HTTP port | 5200 | Agent HTTP listen port. |
| Orchestrator IP | � | **Required**: the LAN address of the operator PC. The agent cannot guess where the operator is. |
| Project root | D:\IGControlPanel\Projects | Local folder for project copies on the node. |


> **Notice:** Enter the operator's LAN IPv4, never a loopback address. Addresses are scheme-less *host:port*; the scheme is added automatically.


### Linux (portable + systemd)


On Linux the operator is a systemd **system** service and the agent is a systemd **--user** unit of the runtime user. Install as *root*:


```bash
sudo ./install-operator.sh \
    --orchestrator-port 5100 \
    --svn-repository-root /var/lib/igcontrolpanel/repositories \
    --firewall-remote-address 192.168.0.0/24

sudo ./install-agent.sh \
    --node-name cave-left --role left \
    --orchestrator-url 192.168.0.10:5100 \
    --project-root /var/lib/igcontrolpanel/projects \
    --run-as-user caveuser --firewall-remote-address 192.168.0.0/24

```


> **Notice:** The addresses above are an example: put in the real LAN address of your operator PC and your own subnet. For a headless install over SSH, set `--run-as-user` explicitly.


The agent unit starts with the graphical session of the `--run-as-user` user, so the session rule is the same as on Windows: a node with no open session runs no agent and stays *OFFLINE*. Automatic logon is needed here as well, and is required for `igctl wakeup`.


### Verifying the Installation


```bash
igctl status         # the orchestrator responds, shows config/counters
igctl nodes status   # nodes online/offline, engine state

```


A node is missing from the list when it has never reached the orchestrator, and *OFFLINE* when the orchestrator cannot reach it back. Both cases are covered in [Troubleshooting](#troubleshooting).


### File Locations


Configuration and logs live next to the executables, under the installation root:


| File | Path |
|---|---|
| Installation root | `C:\Program Files\IGControlPanel` / `/opt/igcontrolpanel` |
| Orchestrator config | `<root>/IGControlPanel/config/igcontrolpanel.json` |
| Agent config | `<root>/IGControlPanelAgent/config/igcontrolpanel-agent.json` |
| Orchestrator log | `<root>/IGControlPanel/logs/operator-<date>.log` |
| Agent log | `<root>/IGControlPanelAgent/logs/agent-<date>.log` |
| CLI config | `%LOCALAPPDATA%\IGControlPanel\igctl-cli.json` / `~/.local/share/IGControlPanel/igctl-cli.json` |


There is one log file per day, and files older than about two weeks are deleted automatically. Edit a configuration file only where this article says so - use the commands and the installers instead - and restart the orchestrator service after every manual change to its config.


### Updating an Installation


Installing over an existing installation always performs a **merge**: only explicitly provided values are applied, auto-detected and built-in defaults never overwrite the live config, and nodes/projects/launch profiles are preserved. A timestamped backup is made before each merge.


Stop the application before an update, and update the operator PC first, then the nodes. The wizard and the install scripts start from the values of the previous installation, so an update usually means confirming them.


Uninstalling removes the service or the scheduled task, the firewall rules and the program files. Your project folders, the SVN repositories on the operator PC and the project copies on the nodes stay on disk - delete them by hand if you no longer need them.


## Using the igctl CLI


The CLI is a thin client: it parses arguments, calls the orchestrator HTTP API, and formats the response. The orchestrator address is taken from the per-user [CLI config](#install_files): key *orchestratorUrl*, default *127.0.0.1:5100*. The path can be overridden via the `IGCONTROLPANEL_CLI_CONFIG` environment variable. There is no dedicated command to set the address - edit the config file or use the environment override.


Common flags and exit codes:


- `--node <name>` - limit the command to the named nodes; repeat the flag for several. Works with `sync`, `run`, `stop` and `kill`. Without it every registered node is targeted, and an unknown name refuses the whole command without touching anything.
- `--json` - print raw JSON instead of the human-readable summary (for scripts/CI; disables the progress spinner).
- `<command> --help / -h` - usage of a specific command; `igctl` with no arguments prints general help.
- **Exit codes:** *0* - success; *1* - the command was refused or failed on at least one node; *2* - the orchestrator could not be reached.


### State and Inventory


```bash
igctl status        # orchestrator status: svnserve state, config, counters, syncs in progress with phase and counters
igctl nodes         # list of nodes (alias: nodes list)
igctl nodes status  # per node: online/offline, engine running/idle/exited (PID, uptime, last exit), host, projectRoot
igctl projects      # list of projects: syncMode, sourcePath, repositoryUrl, launch profiles

```


### Nodes


```bash
igctl nodes add cave-left 192.168.0.21:5200 --role left   # only needed if the node does not self-register
igctl nodes role cave-left front                          # change the role
igctl nodes remove cave-left                              # unregister the node

```


`nodes remove` deletes the registration only. An agent that is still running registers itself again within a short time, so stop or uninstall it on the node first.


### Projects


```bash
igctl add --name Demo --sync svn                 # current folder becomes an SVN working copy
igctl add --name Demo --sync svn --path D:\Work\git\Demo --force   # folder with .git: add and auto-ignore it
igctl add --name Demo --sync manual              # files are already placed on the nodes manually
igctl remove Demo

```


- **svn**: the orchestrator creates/attaches an SVN repository and performs a checkout, keeping a public *svn://* URL for the nodes.

  - `add` does not import content - the folder becomes a working copy, and files are uploaded by the first `sync`.
  - `sync` disables Subversion's built-in default *global-ignores* so that compiled binaries are not silently skipped, while a user-defined *svn:global-ignores* (via `igctl ignore`) is respected.
  - `--force` registers a folder that contains a foreign VCS (`.git`, `.hg` or `.bzr`), auto-adding that directory to *svn:global-ignores* so `sync` never uploads it.
- **manual**: registration only - you place the files on the nodes yourself. See [Synchronization](#sync).
- `remove` for **svn** is a managed removal (node working copies + SVN repo + operator metadata; the project folder itself remains). For **manual** it only unregisters.


### Launch Profile


```bash
igctl set Demo --exe Build/Demo.exe --workdir Build --args "--fullscreen"
igctl set Demo --profile wall --exe Build/Demo.exe --workdir Build
igctl set Demo --args "--fullscreen --vsync"   # partial update: --exe/--workdir are preserved
igctl set Demo --args ""                       # explicitly clear the arguments

```


`set` updates a profile partially: omitted flags keep their previous value. `--exe` is required only when creating a new profile.


Paths are relative to the project. An absolute path, or one that leaves the project through *..*, is refused - a node may only start programs from inside its own copy of the project.


> **Notice:** A launch profile also supports per-profile environment variables applied to the engine process at start. They are currently set only by editing *launchProfiles[].environment* in the [orchestrator config](#install_files) - there is no CLI flag for them.


### Ignoring Files (svn:global-ignores)


For **svn** projects only. IG Control Panel manages *svn:global-ignores* on the root of the operator's working copy - a versioned, inheritable property that propagates to the nodes on their `svn update`. The ignore applies to unversioned files (already committed files are not removed).


```bash
igctl ignore Demo                            # show current patterns
igctl ignore Demo --add "*.log" --add Cache  # append (dedupe)
igctl ignore Demo --remove "*.log"           # remove
igctl ignore Demo --set "*.log obj"          # replace the whole list

```


Patterns use *** and *?* as wildcards; **** is not supported. Only one of `--add/--remove/--set` is allowed per call; flags are repeatable and one value may carry several space-separated patterns.


### Running the Application


```bash
igctl run Demo                  # start the launch profile; run does NOT sync - call sync explicitly
igctl stop Demo                 # graceful (CloseMainWindow + timeout)
igctl kill Demo                 # force kill the process tree
igctl check Demo                # diagnostic check, starts nothing: is the project present on the nodes
igctl check Demo --profile wall # the same, plus the exe and the working directory of that profile

```


A node runs **one application at a time**. A second `run` on a busy node fails with *Process is already running. Duplicate launch is not allowed.* - a run of a different project fails the same way, because the limit is per node, not per project. Stop the running application first.


Per-node arguments are appended to the profile arguments (not replaced):


```bash
igctl run Demo \
    --node-args cave-left="--display 1 --view left" \
    --node-args cave-center="--display 2 --view center"

```


A command that targets several nodes is not transactional: a node that is offline or fails is reported on its own line while the rest of the cluster proceeds, and the command exits with code *1*. Repeat it with `--node` for the nodes that are back. The [HTTP API](#http_api) chapter lists the status codes behind these results.


### Shutting Down and Waking Nodes


```bash
igctl shutdown cave-left
igctl shutdown --all
igctl shutdown cave-left --force --delay 60
igctl wakeup                    # power on all registered nodes (Wake-on-LAN)
igctl wakeup cave-left          # power on a single node

```


`shutdown` powers the nodes off. By default the orchestrator first polls all target nodes and **refuses the command, powering off none**, if an engine is running anywhere (to avoid a half-off cluster). `--force` skips this check; `--delay` (default 30, on Linux rounded up to whole minutes) is passed to the OS shutdown command. The CLI requires either a node name or `--all`.


`wakeup` powers the nodes on at the start of a shift: it sends a Wake-on-LAN magic packet to the MAC the agent reported at registration, so only a node that has been online at least once can be woken. A bare `wakeup` targets all nodes and is safe at any time - for a running node it does nothing. The packet is never acknowledged, so the command reports only that it was sent; the node reaches *ONLINE* two steps later, when it powers on and a user session opens. Confirm with `igctl nodes status`, and set up [automatic logon](#install_windows) so that a woken node gets there on its own.


## Synchronization


Two sync modes are supported:


- **svn** - IG Control Panel manages the repository/commit/checkout/cleanup. The source of truth is the SVN repository on the operator PC. Conflicts are resolved server-wins (`svn update --accept theirs-full`). The project working folders and the repositories must be different (*svnRepositoryRoot* must differ from *sourcePath*). The operator commits through a local *file://* path, while *svnserve* serves the nodes **read-only**: a node can only pull, and nothing on the network can commit into the repository.
- **manual** - IG Control Panel does not copy files; it checks that `<agent.projectRoot>\<projectName>` exists on the nodes.


```bash
igctl sync Demo                    # transfer the project to every node
igctl sync Demo --node cave-left   # transfer to selected nodes only

```


`sync` shows **live progress** in the spinner: *uploading to SVN* (the operator uploads changes - files + bytes), then *updating nodes* (nodes pull from SVN, with per-node progress: files done/total, current path, conflicts). The API names the same two phases *committing* and *updatingNodes*, and ends with *completed* or *failed*. The operation runs on the orchestrator **detached from the HTTP request**, so closing the CLI in the middle of a sync does not abort it. The state is kept in memory and can be polled via *GET /api/projects/{project}/sync*. Only one sync per project runs at a time; a second `sync` while one is active returns *409* with the current state.


The first sync transfers the whole project - tens of minutes for a project of several gigabytes; later syncs carry only the changed files. Per-node progress shows *checkout* for a full transfer from scratch and *update* for an incremental one. A long pause with no visible change is normal: check the counters with `igctl status` from a second prompt before assuming a sync is stuck.


> **Notice:** Stop the application before you sync. A running engine keeps its files open on the node, and an open file cannot be replaced: if one of the changed files is in use, the sync fails for that node while the others succeed. IG Control Panel does not check this - keeping the order `stop`, `sync`, `run` is up to you.


## Reload vs. Restart Classification


For every node, `sync` classifies what a running engine must do to pick up the update, based on the paths that changed. The verdict is exposed as a **SyncAction** with a **SyncActionReason** (the path that forced the verdict):


| SyncAction | Meaning |
|---|---|
| none | Nothing on the node needs to react (for example, only files the editor rewrites on its own have changed). |
| reload | A live scene reload (`world_reload`) is sufficient. |
| restart | A full engine restart is required. |


The rules are applied in this order, and the first match wins:


- Under `bin/`, only real binaries - `.exe`, `.dll`, `.so`, `.dylib` - force *restart*, so a rebuilt application always does. Everything else the engine writes there while it runs (`console_history`, `editor_log.txt`, caches) is ignored.
- Editor bookkeeping - `guids.db`, `unigine.cache`, `*.meta`, `*.cache`, `*.gpu_cache` - never escalates the verdict on its own: a real asset change is classified on its own line anyway.
- Any **add, delete or replace** forces *restart*: the GUID of a new file is missing from the `guids.db` the engine loaded at start, so a running engine cannot resolve it.
- An **in-place edit** resolves to *reload* only for scene-description files - `.world`, `.node`, `.variations`, `.visual_menus`, `.mat`. Everything else, meshes and textures included, is served from the in-memory cache after a reload, so an in-place edit of those forces *restart*.


> **Notice:** An agent released before this feature always reports *none*. The verdict is currently available only through the HTTP API and the CLI `--json` output, not in the human-readable summary.


## HTTP API


**Orchestrator:**


| Method | Route | Purpose |
|---|---|---|
| GET | /api/status | Orchestrator status + active syncs. |
| GET | /api/nodes | List of nodes. |
| GET | /api/projects | List of projects. |
| GET | /api/nodes/status | Status of every node. |
| POST | /api/nodes/add | Register a node. |
| POST | /api/nodes/role | Change the role of an existing node. |
| POST | /api/nodes/remove | Unregister a node. |
| POST | /api/projects/add | Add a project (svn/manual). |
| POST | /api/projects/{project}/set | Create/update a launch profile (partial). |
| POST | /api/projects/{project}/remove | Remove a project (managed for svn). |
| POST | /api/projects/{project}/check | Diagnostic check on all target nodes. |
| GET | /api/projects/{project}/ignores | Current *svn:global-ignores*. |
| POST | /api/projects/{project}/ignores | Change the ignore list (add/remove/set). |
| GET | /api/projects/{project}/sync | Live sync state (phase + commit files/bytes + per-node) for polling. |
| POST | /api/projects/{project}/sync | Start a sync (commit + svn update on the nodes); runs in the background. |
| POST | /api/projects/{project}/run | Start the launch profile (without sync). |
| POST | /api/projects/{project}/stop | Graceful stop. |
| POST | /api/projects/{project}/kill | Force kill. |
| POST | /api/nodes/shutdown | Shut down a node/cluster. |
| POST | /api/nodes/wake | Wake-on-LAN magic packet (one node / all). |


**Agent:**


| Method | Route | Purpose |
|---|---|---|
| GET | /api/status | Identity + engine state. |
| POST | /api/projects/check | Check the project/exe/workdir presence. |
| POST | /api/projects/delete | Delete the local copy (refuse-if-running, idempotent). |
| POST | /api/sync | svn checkout/update. |
| GET | /api/sync/progress/{project} | Live per-file progress of the current svn checkout/update. |
| POST | /api/start | Start the engine. |
| POST | /api/stop | Graceful stop. |
| POST | /api/kill | Force kill (bounded timeout). |
| POST | /api/shutdown | Power off (refuse-if-running unless forced). |


For operations that target several nodes the HTTP status code follows a convention: **200 OK** - all target nodes online and the operation succeeded on each; **409 Conflict** - at least one reachable node refused or failed (engine running, a failed check, partial success); **502 Bad Gateway** - a purely transport failure (target nodes offline). The body always carries a per-node result and a top-level success flag. The `check` operation is an exception - a diagnostic probe that always returns *200* with the result in the body.


## Troubleshooting


Start with the [service logs](#install_files): the effective config is written on startup, and the agent warns about a loopback address in *orchestratorUrl*.


On a Windows node, check the rights first: the agent writes its log into the program folder under `Program Files`, so if the user that runs it is not a local administrator, no log file appears at all. Make that user a local administrator and start the agent again.


A node that registers but still shows *OFFLINE* is usually reporting the wrong address of its own: the agent detects it at installation, and on a machine with several network adapters it may pick the one that is not on the cluster network. Compare *publicUrl* in the agent log with the address the node really uses. To stop the agent from guessing, set *publicUrl* explicitly in its [config](#install_files) and restart it.


A port may stay closed even after a correct installation. Windows creates a **blocking** rule of its own when a program opens a port before an allow rule exists and the *Windows Security Alert* dialog is dismissed. A block rule wins over an allow rule and survives an uninstall. The installers delete such rules, so look for one only if the port is still unreachable:


```bash
Get-NetFirewallRule -Direction Inbound -Action Block -Enabled True |
    Where-Object { $_ | Get-NetFirewallApplicationFilter |
        Where-Object { $_.Program -like "*IGControlPanel*" } }

```


Delete every rule it lists by its name: `Remove-NetFirewallRule -Name "<name>"`.


## See Also


- [IG Application Template](../ig/index.md)
- [CAVE configuration in the SpiderVision plugin](../principles/render/output/multi_monitor/spidervision_plugin/presets.md#cave)
