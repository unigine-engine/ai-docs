# UAV Template - Autopilot Simulation


**ArduPilot SITL (Software in the Loop)** is the real *[ArduPilot](https://ardupilot.org/)* firmware compiled as a native PC binary.


![](../modules/sitl/img/sitl.png)


ArduPilot, an open source **autopilot system** supporting various vehicle types, runs on a wide variety of platforms, and SITL allows you to execute it directly on your PC, with no special hardware required.


When launched with the JSON option, ArduPilot skips its built-in physics and instead talks to an external simulator over User Datagram Protocol (UDP): it sends raw servo Pulse Width Modulation (PWM) values out and expects simulated sensor data (IMU, position, velocity, orientation) back. The UAV template plays the role of that external simulator - **ArduPilot runs the full control stack**, while the **template provides the airframe, the world, and the sensors**.


Using a real autopilot instead of the template's built-in flight model gives you ArduPilot's actual feature set: guided flight, waypoint missions, auto takeoff and landing, return-to-launch, failsafes, the complete parameter system.


Any MAVLink ground station (MAVProxy, Mission Planner, QGroundControl) works with the simulated vehicle **exactly as it would with a real drone**. If you are building a UAV application on the template, you develop and test against the same autopilot stack your hardware will run - the behavior in simulation matches the behavior of the physical drone.


## Architecture


ArduPilot SITL integration in the template includes:


[![](../modules/sitl/img/sitl_scheme.png)](../modules/sitl/img/sitl_scheme.png)


1. `ardupilot_sitl` module (*modules/ardupilot_sitl*, class *[ArduPilotSITLBridge](../../../api/modules/ardupilot_sitl/class.ardupilotsitlbridge.md)*) is a reusable transport **bridge** which handles the communication between your application and ArduPilot, and makes the application act as an ArduPilot JSON physics backend. The module serves as:

  - *A UDP socket* serviced by its own network thread
  - *A wire-format handler* (a small binary PWM packet in, one JSON sensor line out - the protocol is documented at *[https://ardupilot.org/dev/docs/sitl-with-JSON.html](https://ardupilot.org/dev/docs/sitl-with-JSON.html)*)
  - *A helper that [converts coordinates](../../../sdk/templates/uav/custom.md#sitl_custom_helper)*: Unigine state (ENU, body Z-up) into ArduPilot conventions (NED, body forward-right-down).
2. `SITL_Integration` (*template/SITL/SITL_Integration.{h,cpp}* in the template sources) is an example integration layer between ArduPilot SITL and the UAV template. It is a *[WorldLogic](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic)* that owns the bridge and, each physics tick, pushes the incoming PWM channels into the active drone and sends derived sensor data back to ArduPilot. The interpretation of the servo PWM values depends on which ArduPilot firmware is running, not on any aspect of the template. Each vehicle type is implemented as a small, self-contained struct inside `SITL_Integration`: The **active vehicle** is selected by a dedicated *[launch flag](#sitl_mission_planner_launch)*. ArduPilot's **tunable parameters** are defined in the *[parameter file](#sitl_mp_param_file)*, applied at SITL launch. Firmware defaults combined with the file data, provide the complete, reproducible parameter state of the demo setup. `SITL_Integration` also tracks **link liveness**: The **HUD** on the right edge of the screen shows the link state, frame rate, the first PWM inputs, and the sensor reply. A **debug** visualizer draws the flight trail and per-rotor thrust vectors.

  - `CopterIntegration (ArduCopter)`: every PWM channel is a motor throttle. A channel map names which rotor of the drone each channel drives.
  - `PlaneIntegration (ArduPlane)`: the PWM values represent control surfaces and throttle, pushed into the fixed-wing flight model as one input struct.

  - While SITL is connected, the drone is under external control (ArduPilot flies it)
  - When the link drops, it returns to its internal flight model, so manual flight works as usual.


The integration is deliberately thin and one-way in its dependencies: the template's flight models know nothing about ArduPilot (the same flight model can be used with any autopilot or none at all), and the reusable transport layer - *ardupilot_sitl module* - knows nothing about drones (UDP, JSON, and coordinate conversion only, with no drone-specific logic).


To use ArduPilot SITL **[in your own project](../../../sdk/templates/uav/custom.md#sitl_custom)**, copy `SITL_Integration.{h,cpp}` to the corresponding folder in your project.


## Running The Template With ArduPilot SITL


ArduPilot SITL is a native PC program that can be launched using different Ground Control Stations (GCS). In this template, two of them are available out of the box:


- `Mission Planner` (recommended, Windows OS only) - the standard ArduPilot ground control station (map, live telemetry, mission editor, full parameter tree). Mission Planner runs natively on Windows OS, offers a single-click SITL firmware binary download, and doesn't require source compilation or WSL.
- `sim_vehicle.py + MAVProxy` (Windows WSL or Linux OS) - a minimalist, command-line based, portable and extendable GCS. With this approach, SITL is built from the ArduPilot source tree and driven from the WSL console. It's the standard ArduPilot developer tooling, which runs natively on Linux and via WSL on Windows.


Regardless of the selected launch method, the template runs directly on the host OS and binds UDP port 9002. SITL then connects to this port and is controlled from the selected ground station.


> **Notice:** Start the template before SITL: ArduPilot blocks on startup waiting for sensor data.


### Mission Planner (Windows OS)


![](../modules/sitl/img/sitl_mission_planner.png)


#### Prerequisite Setup


1. **Install Mission Planner**: download the installer from *[https://ardupilot.org/planner/docs/mission-planner-installation.html](https://ardupilot.org/planner/docs/mission-planner-installation.html)* and run it.
2. **Obtain the SITL firmware binary**:

  1. Open *Mission Planner*, go to the *Simulation* tab on the top toolbar ![](../modules/sitl/img/sitl_mission_planner_setup.png)
  2. Click the desired vehicle (*Multirotor* or *Plane*). The first click downloads the current stable build to `%USERPROFILE%\Documents\Mission Planner\sitl`, specifically `ArduCopter.exe` or `ArduPlane.exe` along with their `cyg*.dll` runtime. ![](../modules/sitl/img/sitl_mission_planner_setup_v.png)
  3. Once the download completes, close the SITL console window.


#### Launching


1. Launch the template with the corresponding flag: `-sitl copter` for a multirotor, or `-sitl plane` for a fixed-wing drone. ![](../modules/sitl/img/sitl_mission_planner_flag.png) The console log confirms the selection: ![](../modules/sitl/img/sitl_fpv_bound.png) The SITL integration is always compiled into the template, but stays dormant unless this flag is present. With the flag, the template listens on UDP port 9002 and the HUD shows an amber `"SITL LINK DOWN - Waiting for ArduPilot..."` message. ![](../modules/sitl/img/sitl_amber.png) The bare `-sitl` flag defaults to `-sitl copter`. A plain launch without the flag runs the template as usual with no SITL code active.
2. **Run the SITL binary** Create a parameter file matching your vehicle type and copy the code given below. Save it as `copter.parm` or `plane.parm` in a convenient location. <details> <summary>copter.parm</summary> ```text # ArduCopter parameters for the UAV template SITL setup. # Applied at SITL launch: sim_vehicle.py --add-param-file=<this file>, # or the raw binary -w --defaults <this file>. # quad frame, X motor layout - must match the integration's channel map # (FRAME_CLASS firmware default is 0 = undefined, nothing flies) FRAME_CLASS 1 FRAME_TYPE 1 # the demo scene is fictional terrain: don't compare EKF altitude against # the real-world elevation database TERRAIN_ENABLE 0 # optional, uncomment as needed: #CRASH_CHECK_ANGLE_DEG 60   # tolerate strong scene wind banking the drone #MOT_THST_HOVER 0.3         # hover throttle of the demo airframe (T/W ~ 3.3) #WPNAV_SPEED 300            # gentler waypoint approach ``` </details> > **Notice:** With a JSON frame, ArduPilot loads only the firmware defaults and the `.parm` file settings. Therefore, for ***ArduCopter*** the parameter file must **explicitly define the frame configuration** (*FRAME_CLASS* and *FRAME_TYPE*). Without these, the copter will not know its motor layout and will not fly. <details> <summary>plane.parm</summary> ```text # ArduPlane parameters for the UAV template SITL setup. # Applied at SITL launch: sim_vehicle.py --add-param-file=<this file>, # or the raw binary -w --defaults <this file>. # the demo scene is fictional terrain: don't compare EKF altitude against # the real-world elevation database TERRAIN_ENABLE 0 # the first turn after takeoff happens at this altitude: keep a margin TKOFF_ALT 80 # the steepest bank the demo airframe holds in turns without sinking ROLL_LIMIT_DEG 30 # damp the altitude oscillation (phugoid) of the demo airframe TECS_THR_DAMP 1.5 TECS_PTCH_DAMP 0.5 TECS_TIME_CONST 7 # optional, uncomment for tighter navigation: #WP_LOITER_RAD 40 #NAV_L1_PERIOD 15 ``` </details> > **Notice:** The vehicle parameter file must match the *[launch flag](#sitl_mission_planner_launch)* used with the template. Open a Command Prompt and launch the SITL binary from the `sitl\` folder (this ensures that the `eeprom.bin` is created there): ```text cd %USERPROFILE%\Documents\Mission Planner\sitl ArduCopter.exe -w --model json:127.0.0.1 --home 57.196976,-170.244540,-245,132 --defaults <path>\copter.parm --serial0 udpclient:127.0.0.1:14550 ``` > **Notice:** Replace `<path>` with the actual path to your `.parm` file. The command line options are: Once connected, the HUD switches to green *"SITL LINK UP"*, and ArduPilot takes control of the drone. Manual controls are inactive while the link is up. ![](../modules/sitl/img/sitl_green.png)

  - **`--model json:127.0.0.1`** selects the external JSON simulator - the UAV template, running at this address - instead of SITL's built-in physics. The port is fixed at 9002.
  - **`-w`** wipes the stored parameters and **`--defaults <file>`** loads the demo parameter file instead, so every run starts from the same reproducible state.
  - **`--home lat,lon,alt,heading`** (no spaces; N/E positive, S/W negative) tells ArduPilot where the Unigine world origin is located on Earth, so the map shows the drone over the terrain matching your scene. The example coordinates correspond to St. Paul Island (Bering Sea), which roughly matches the location of the demo scene. Note that the parameter georeferences the **world origin, not the drone position**. The drone appears on the map offset from this origin by its in-world position. Omitting `--home` places the map at a default location in Australia.
  - **`--serial0 udpclient:127.0.0.1:14550`** streams MAVLink telemetry to UDP port 14550, where Mission Planner receives it.
3. In Mission Planner, set the connection type (top-right of the window) to *UDP*, click *Connect*, and accept the default port 14550. Once connected, the vehicle appears on the map. Mission Planner remembers the connection, so subsequent runs reconnect automatically. ![](../modules/sitl/img/sitl_mission_planner_connect.png)


#### Flying


Use the *Data* screen (the map) for control and monitoring. The HUD displays mode, arm state, and ArduPilot messages. The *Actions* tab in the bottom-left panel provides the mode dropdown and *Arm/Disarm* button.


[![](../modules/sitl/img/sitl_mission_planner_ui_sm.png)](../modules/sitl/img/sitl_mission_planner_ui.png)


##### Copter


1. In the *Actions* tab, set mode to *Guided*, then click *Arm/Disarm*. Arming takes a few seconds - ArduPilot waits for the position estimate to settle.
2. Right-click on the map, select *Takeoff*, and enter an altitude. The copter climbs straight up and holds position.
3. Right-click on the map again and select *Fly To Here* to send the copter to a chosen point. Alternatively, build a mission on the *Plan* screen and switch to *Auto* mode.
4. To land, select *Land* or *RTL (Return To Launch)*.


##### Plane


1. Press `U` to select the airplane preset as the active drone. The template console prints: `plane bound to drone "..."`, when the correct preset is active.
2. In the *Actions* tab, set mode to *TAKEOFF*, then click *Arm/Disarm*. The plane rolls down the runway, rotates, climbs to the takeoff altitude (80 m, according to the *[parameter file](#sitl_mp_param_file)*), and loiters there.
3. Landing requires a mission. By design, a plane in RTL mode returns home but does not land automatically, instead - it circles above waiting for further commands. To perform an actual landing: The plane flies the approach, flares, and rolls out. You can click *Disarm* to end the ground rollout immediately after touchdown.

  1. On the *Plan* screen, add waypoints and a *LAND* item
  2. Click *Write* to write the mission
  3. Switch to *Auto* mode.


### sim_vehicle.py + MAVProxy (WSL or Linux)


![](../modules/sitl/img/sitl_mavproxy.png)


#### Prerequisite Setup


> **Notice:** If you are using Mission Planner exclusively, you can skip this section entirely.


While the template runs directly on the host OS (Windows or Linux), SITL and its MAVProxy console live in an ***Ubuntu shell*** - a WSL terminal on Windows, a regular terminal on Linux.


For the first run, complete the initial one-time setup by following these steps:


1. (Windows only) In an admin PowerShell, run `wsl --install -d Ubuntu`, and then reboot your computer.
2. Open Ubuntu and run the following commands to install ArduPilot and its prerequisites: ```text git clone --recurse-submodules https://github.com/ArduPilot/ardupilot.git cd ardupilot Tools/environment_install/install-prereqs-ubuntu.sh -y . ~/.profile ```
3. (Windows only) Enable mirrored networking so WSL shares localhost with Windows: create `C:\Users\<user>\.wslconfig` with the following content: ```text [wsl2] networkingMode=mirrored ```
4. Run `wsl --shutdown` in PowerShell and restart Ubuntu. Without this step, 127.0.0.1 inside WSL does **not** point to the Windows host, and the connection between SITL and the template will silently hang.


For more details, refer to the official ArduPilot SITL documentation:


- *[https://ardupilot.org/dev/docs/sitl-on-windows-wsl.html](https://ardupilot.org/dev/docs/sitl-on-windows-wsl.html)*
- *[https://ardupilot.org/dev/docs/setting-up-sitl-on-linux.html](https://ardupilot.org/dev/docs/setting-up-sitl-on-linux.html)*


#### Launching


1. Launch the template with the corresponding flag: `-sitl copter` for a multirotor, or `-sitl plane` for a fixed-wing drone. ![](../modules/sitl/img/sitl_mission_planner_flag.png) The console log confirms the selection: ![](../modules/sitl/img/sitl_fpv_bound.png) The SITL integration is always compiled into the template, but stays dormant unless this flag is present. With the flag, the template listens on UDP port 9002 and the HUD shows an amber `"SITL LINK DOWN - Waiting for ArduPilot..."` message. ![](../modules/sitl/img/sitl_amber.png) The bare `-sitl` flag defaults to `-sitl copter`. A plain launch without the flag runs the template as usual with no SITL code active.
2. **Run the SITL binary** Create a parameter file matching your vehicle type and copy the code given below. Save it as `copter.parm` or `plane.parm` in a convenient location. <details> <summary>copter.parm</summary> ```text # ArduCopter parameters for the UAV template SITL setup. # Applied at SITL launch: sim_vehicle.py --add-param-file=<this file>, # or the raw binary -w --defaults <this file>. # quad frame, X motor layout - must match the integration's channel map # (FRAME_CLASS firmware default is 0 = undefined, nothing flies) FRAME_CLASS 1 FRAME_TYPE 1 # the demo scene is fictional terrain: don't compare EKF altitude against # the real-world elevation database TERRAIN_ENABLE 0 # optional, uncomment as needed: #CRASH_CHECK_ANGLE_DEG 60   # tolerate strong scene wind banking the drone #MOT_THST_HOVER 0.3         # hover throttle of the demo airframe (T/W ~ 3.3) #WPNAV_SPEED 300            # gentler waypoint approach ``` </details> > **Notice:** With a JSON frame, ArduPilot loads only the firmware defaults and the `.parm` file settings. Therefore, for ArduCopter the `.parm` file must explicitly define the frame configuration (*FRAME_CLASS* and *FRAME_TYPE*). Without these, the copter will not know its motor layout and will not fly. <details> <summary>plane.parm</summary> ```text # ArduPlane parameters for the UAV template SITL setup. # Applied at SITL launch: sim_vehicle.py --add-param-file=<this file>, # or the raw binary -w --defaults <this file>. # the demo scene is fictional terrain: don't compare EKF altitude against # the real-world elevation database TERRAIN_ENABLE 0 # the first turn after takeoff happens at this altitude: keep a margin TKOFF_ALT 80 # the steepest bank the demo airframe holds in turns without sinking ROLL_LIMIT_DEG 30 # damp the altitude oscillation (phugoid) of the demo airframe TECS_THR_DAMP 1.5 TECS_PTCH_DAMP 0.5 TECS_TIME_CONST 7 # optional, uncomment for tighter navigation: #WP_LOITER_RAD 40 #NAV_L1_PERIOD 15 ``` </details>
3. In Ubuntu shell (WSL or native), launch SITL with the matching vehicle firmware and its parameter file: ```text cd ardupilot # For multirotor: sim_vehicle.py -v ArduCopter -f JSON:127.0.0.1 --console --map --add-param-file=$HOME/copter.parm # For plane: sim_vehicle.py -v ArduPlane  -f JSON:127.0.0.1 --console --map -l 57.196976,-170.244540,-245,132 --add-param-file=$HOME/plane.parm ``` The command line options are: Once connected, the HUD switches to green *"SITL LINK UP"*, and ArduPilot takes control of the drone. Manual controls are inactive while the link is up. ![](../modules/sitl/img/sitl_green.png)

  - **`-v`** selects which vehicle firmware to build and run: *ArduCopter* for multirotor, *ArduPlane* for fixed-wing. > **Notice:** The vehicle *[parameter file](#sitl_proxy_param_file)* and firmware must match the *[launch flag](#sitl_mavproxy_launch)* used with the template, as the two interpret the incoming servo channels differently.
  - **`-f JSON:127.0.0.1`** selects the external JSON simulator - the UAV template - instead of SITL's built-in physics. The address points to the machine running the template (127.0.0.1 works from WSL via mirrored networking, and natively on Linux). The port is fixed at 9002.
  - **`--add-param-file`** applies the known-good ArduPilot parameters at every launch, so the setup is reproducible with no console typing. > **Notice:** From WSL, a Windows path is reachable as `/mnt/c/...`, `/mnt/d/...`.
  - **`-l lat,lon,alt,heading`** (no spaces; N/E positive, S/W negative) tells ArduPilot where the Unigine world origin is located on Earth, so the map shows the drone over the terrain matching your scene. The example coordinates correspond to St. Paul Island (Bering Sea), which roughly matches the location of the demo scene. Note that the parameter georeferences the **world origin, not the drone position**. The drone appears on the map offset from this origin by its in-world position. Omitting `-l` places the map at a default location in Australia.


#### Flying


Use the *Map* window for control and monitoring, and the Ubuntu shell to enter MAVProxy commands. The MAVProxy Console displays ArduPilot messages.


![](../modules/sitl/img/sitl_mavproxy_console.png)


##### Copter


1. Enter the following commands into the terminal: ```text mode GUIDED arm throttle takeoff 10 ```
2. Once airborne, right-click in the map window and select the *Fly To* option to send the copter to a chosen location. ![](../modules/sitl/img/sitl_mavproxy_map.png)
3. To return home and land, enter the `mode RTL` (Return To Launch) command.


##### Plane


1. Press `U` to select the airplane preset as the active drone. The template console prints `plane bound to drone "..."` when the correct preset is active.
2. Enter the following commands into the Ubuntu command line: ```text mode TAKEOFF arm throttle ``` The plane rolls down the runway, rotates, climbs to the takeoff altitude (80 m, according to the *[parameter file](#sitl_proxy_param_file)*), and loiters there.
3. To land, add a landing point in the map's mission editor (this inserts a *NAV_LAND* sequence), then use the `mode AUTO` command. The plane will execute the landing approach, flare, and roll out.


More on MAVProxy controls: *[https://ardupilot.org/dev/docs/copter-sitl-mavproxy-tutorial.html](https://ardupilot.org/dev/docs/copter-sitl-mavproxy-tutorial.html)*.


**Mission Planner** can also run alongside **MAVProxy** - MAVProxy forwards MAVLink to UDP 14550 by default, and any GCS listening on that port will detect the vehicle automatically. This is useful, for example, when you want to send quick MAVProxy commands via console while monitoring the drone's position on Mission Planner's map.


## Troubleshooting


1. **No SITL HUD:** the template was launched without the `-sitl` flag. *[Add the flag](#sitl_mission_planner_launch)* and restart.
2. **(Mission Planner) No vehicle on the map:** confirm Mission Planner's connection is set to **UDP** on port 14550, and the SITL binary is actually running - it is the process that feeds data to port 14550. If you clicked a vehicle on the *Simulation* tab, that launches SITL with its own built-in physics, not the template, close it and launch the binary *[manually](#sitl_mp_bin)* with `--model json:127.0.0.1`.
3. **(WSL) SITL link never comes up:** - mirrored networking is not active. Check your `.wslconfig` and run `wsl --shutdown` to restart WSL. On both Windows (WSL) and Linux, make sure the template is started **before** SITL.
4. **(WSL) Batches of "`Warning, time moved backwards. Restarting timer.`" in the console:** The Ubuntu clock is being stepped backwards by its own NTP service conflicting with WSL's host time sync. Fix once with **`sudo systemctl disable --now systemd-timesyncd`** in Ubuntu, then restart SITL. Do not ignore this warning as an autopilot running on a jumping clock will misbehave in flight.
5. **Drone refuses to arm:** The "Need Position Estimate" warning is normal. Wait a few seconds for the EKF (estimation filter) to settle.
6. **Disarms mid-air in strong wind:** this is ArduPilot's crash check working as intended. To allow steeper banking in windy conditions, set `CRASH_CHECK_ANGLE_DEG 60` in the [`.parm`](#sitl_mp_param_file) file.
7. **Copter circles or wobbles instead of holding position:** the parameter file was not applied, or extra parameters leaked in on top of it. The setup expects exactly firmware defaults + the parameter file. Do **not** layer ArduPilot's **stock SITL calibration file** (*Tools/autotest/default_params/copter.parm*) on top. That file sets a plus-frame motor layout (*FRAME_TYPE 0*) and non-zero compass offsets - both are incorrect for this integration.
8. **"`Terrain: clamping offset ...`"** followed by erratic behavior after takeoff (thrust loss warnings, EKF failsafe): ArduPilot is comparing its altitude against the real-world elevation database, which has nothing to do with your simulated scene's terrain. The provided [`.parm`](#sitl_mp_param_file) files disable this with *TERRAIN_ENABLE 0*. If you launch without those files, set this parameter manually.
9. **`-sitl plane` works but the plane does not respond:** "`has no fixed wing flight model, inputs ignored`" warning means that the active drone in the scene is not the airplane preset. Cycle presets with the *U* key until the template console prints `plane bound to drone "airplane"`.


## ArduPilot SITL API


*[ArduPilotSITLBridge Class](../../../api/modules/ardupilot_sitl/class.ardupilotsitlbridge.md)*
