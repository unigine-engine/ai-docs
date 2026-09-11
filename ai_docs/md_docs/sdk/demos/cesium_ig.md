# Cesium Demo

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


*Cesium* demo showcases the use of a UNIGINE-based application as an *[Image Generator (IG)](../../ig/index.md)* that interacts with a host via the CIGI protocol (versions 3.0, 3.1, 3.2, and 3.3 are supported), flying over real-world planet data streamed from [Cesium ion](https://cesium.com/platform/cesium-ion/).


Global elevation and imagery are streamed on demand by the *[Cesium](../../code/plugins/cesium/index_cpp.md)* plugin, with high-detail [terrain insets](../../code/plugins/cesium/insets.md) swapped in at the places that matter, and globe-aware *[Weather](../../ig/weather/index.md)* on top.


The demo also contains *[IG Host](../../ig/ig_host.md)* - a cross-platform host emulator that can be used for debugging, and that can be [used](../../ig/ig_host.md#run_project_with_host) with any *UNIGINE IG* project.


![](cesium_ig_001.jpg)


## Features


- Two modes: driven by a CIGI host as a pure image generator, or flown by hand with no host at all
- Real-world terrain and imagery streamed from *Cesium ion*
- Support for *OSM Buildings* and *Google Photorealistic 3D Tiles*
- Floating-origin rebasing, keeping entities and cameras aligned with the terrain anywhere on the globe
- High-detail [terrain insets](../../code/plugins/cesium/insets.md) over the places that matter, swapped in over the streamed global terrain as the camera comes near
- Globe-aware weather: rounded clouds, sky and sun following the globe anchor, weather regions placed by geodetic footprint
- Cross-platform host emulator that can be used for debugging
- Entity creation/deletion and control
- Control over articulated parts of the entity
- *View/Viewgroup* control via *View Definition/Control* packets
- Changing the time of the day via *Celestial Sphere Control* packets
- Changing the weather conditions via *Weather Control* packets
- *HAT/HOT* request packets
- Runtime configuration of the streamed data sources from the [Cesium editor panel](../../code/plugins/cesium/editor_plugin.md)
- Landmarks to jump to, each with a time of day chosen to light it, and time-of-day and month scrubbing on the globe


## Requirements


Streaming requires a *Cesium ion* access token. Create a free account at [ion.cesium.com](https://ion.cesium.com) and take the default token from [ion.cesium.com/tokens](https://ion.cesium.com/tokens), or create one with the assets:read scope.


> **Notice:** The token is tied to your account and its quota. It is stored in a separate file outside the project and is never written into the plugin [configuration file](../../code/plugins/cesium/config.md), so the configuration remains safe to share.


Network access to *Cesium ion* is required for as long as the camera keeps moving: the streamed tiles are held in [memory](../../code/plugins/cesium/config.md#cache) and are not cached on disk, so an area the camera comes back to is streamed again.


## Running the Demo


As you launch the demo, you will see the start menu.


![](cesium_start_demo.png)


1. Paste the access token into the *Cesium ion access token* group and click *Save*. The status line reports whether the token was accepted and where it has been stored, and the globe starts streaming without a restart.
2. Select either of the two modes the demo offers: *[Host](#run_host)* or *[Hostless](#run_hostless)*. Either mode can be left afterwards with *Back to menu* at the bottom of the [panel](#panel), which puts the camera back over the start-menu backdrop and restores the authored weather.


### Flying It Yourself


Click ***Start in hostless mode***. Nothing has to be set up: no host is involved, the CIGI connector is not even loaded, and the camera is yours to fly with the keys listed in the [panel](#panel).


Start here if you have not used an image generator before. The *[Locations](#locations)* group lists the terrain insets and the landmarks together: click a row to select it, double-click to fly there. A landmark also brings its own time of day, chosen to light it.


### Driving It from a Host


In ***Host mode*** the application is a pure image generator: a CIGI host creates the aircraft, flies it and owns the cameras, while this window only renders. The CIGI connector is loaded at the moment the mode is picked, so nothing is connected to anything while the menu is still up.


The connection fields are filled in with the defaults of the demo's own [ig_config.xml](../../ig/config.md), and they are greyed out because the *Use the connection settings from the IG config* check box above them is on. Leave all of it as it is for a local run and click *Start in host mode*. Clear the check box to point the demo at a host elsewhere; the *View ID* this image generator renders stays editable either way.


Then click *[Run Host](#host_button)* in the *Host* group of the in-flight panel to start the bundled *[IG Host](../../ig/ig_host.md)* emulator, already pointed at the connection this application has open - or start a CIGI host of your own on the same ports. The label beside the button reports which of its states you are in, and the button stays disabled while a host is talking, since a second host would drive the same entities over the same connection.


The bundled host is launched with a start-up state file, so it comes up with its entity, its view and the demo's authored weather regions already in place. One step is still left to do in the host:


> **Warning:** Open *Windows -> Database List*, select the database and click *Load*. Until a database is loaded, the host reports the RESET mode and nothing in the simulation runs - the globe streams, and the aircraft does not move. Loading the database switches the host to OPERATE on its own, and a state file does not do it for you.


After that, check the entity in the host's *Entities* list: set its *Type* to be-200 and its *Geo Pos* to where you want to start - the coordinates of the shipped insets are listed in [Terrain Insets](../../code/plugins/cesium/insets.md#reference), *Orly* among them at 48.7378 N, 2.3573 E - and fly it from the *EntityControl* window. See [IG Host](../../ig/ig_host.md) for the full host reference.


## In-Flight Panel


The interface of the demo is its own, and what it holds depends on the mode. The panel on the left carries the groups listed below, and *Back to menu* sits at its bottom.


![](cesium_ig_002.png)


| Group | Contents |
|---|---|
| *Locations* | The places to go to, in two lists with their coordinates: the configured [terrain insets](../../code/plugins/cesium/insets.md) under *Terrain insets*, and the landmarks under *Points of interest*. Only the insets that passed the plugin's checks are listed, and the one Cesium has actually swapped in is marked. A click selects a row, and in hostless mode a double click flies the camera there; the arrow keys and *Enter* do the same from the keyboard, and *Esc* drops the selection. A middle click on an inset row switches that inset on or off |
| *Cesium Assets* | A check box per [Cesium ion asset](../../code/plugins/cesium/assets.md), with its type. Toggling one rebuilds the tilesets, so expect a re-stream; the [configuration file](../../code/plugins/cesium/config.md) is left untouched |
| *Custom location* (hostless mode) | Coordinates to fly to that are not on the list: latitude and longitude in one field, the altitude in the other, and a *Go* button. The fields come up filled with the last place entered, or with the landmark the camera is parked at |
| *Host* (host mode) | The *Run Host* button that starts the *[IG Host](../../ig/ig_host.md)* emulator and the state of the host link |
| *Scene* | - *Time*, *Month* - the time of day and the month, both UTC. Half the globe is dark at any moment, so scrubbing them shows which places are lit - *Guiding arrow* - the arrow pointing at the selected place - *Render clouds* - the clouds. Hostless mode only; in host mode they are always on - *Render debug* - the debug rendering: provides extra info on tiles streaming and visualizes tiles - *[Show help](#help)* - toggles additional information on the right |


In hostless mode the speed of the camera and its three gears are shown at the top center of the screen:


![](cesium_ig_camera_mode.jpg)


You can type in the required speed, or select one of the presets using either mouse or buttons 1-3 on the keyboard.


Help area on the right provides the following information:


![](cesium_ig_controls_panel.jpg)


- Streamer info - tiles rendered, loaded and loading, load progress and memory used. Available when *[Render debug](#scene)* is enabled, which also draws the tile bounds and the globe anchor basis in the world.
- Coordinates of the camera and its altitude, compass.
- *Controls* window with the key bindings that are available in this mode.
- *Info* window with what is going on and what to do about it - a missing token, an asset list that gives Cesium nothing to stream, a host that is not talking, or the inset currently under the camera.


## See Also


- *[Cesium Plugin](../../code/plugins/cesium/index_cpp.md)* - the streaming runtime, its concepts and API
- *[Cesium Plugin Configuration](../../code/plugins/cesium/config.md)* - the configuration file reference
- *[Terrain Insets](../../code/plugins/cesium/insets.md)* - adding high-detail ground of your own
- *[Cesium Editor Plugin](../../code/plugins/cesium/editor_plugin.md)* - configuring the plugin from UnigineEditor
- *[IG Host](../../ig/ig_host.md)* - the host emulator reference
- [Quick start with IG Template for a flight simulator](https://youtu.be/aYR_ApIBuCI?t=478)


## Accessing Demo Source Code

You can study and modify the source code of this demo to create your own projects. To access the source code do the following:

1. Find the **Cesium Demo** demo in the *Demos* section and click **[Install](/sdk/#samples)** (if you haven't installed it yet).
2. After successful installation the demo will appear in the *Installed* section, and you can click **Copy as Project** to create a project based on this demo. ![](../../sdk/demos/copy_as_project_gen.png)
3. In the **Create New Project** window, that opens, enter the name for your new project in the corresponding field and click **Create New Project**. ![](../../sdk/projects/create_project_cpp.png)
4. Now you can click **Open Code IDE** to check and modify source code in your default IDE, or click **Open Editor** to open the project in the [UnigineEditor](/editor2/). ![](../../sdk/projects/edit_code.png)
