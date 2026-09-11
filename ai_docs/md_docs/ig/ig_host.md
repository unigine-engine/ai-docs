# IG Host

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


> **Warning:** This tool is experimental, some settings and parameters are still under development.


In the simulation industry, an image generator (IG) receives data from a host via an interface (such as CIGI). For demonstration of IG features and debugging purposes, we started developing *IG Host* - a cross-platform and cross-protocol solution. Currently, IG Host is a simplified version of CIGI *[HEMU](http://cigi.sourceforge.net/product_he.php)* and includes a number of useful advantages:


- Simplified entity control
- Transparent packet transfer (requests and responses can be viewed in the console)
- CIGI Debug mode
- Improved LOS responses


Besides CIGI, a DIS connector is available: it is selected by the *Connector* setting, has its own packet windows and its own tab in the packet logger filter. Support for the HLA protocol is planned for the next versions.


## Running IG Host


IG Host is a part of the [Cesium demo](../sdk/demos/cesium_ig.md). Therefore, to try out IG Host, you need to download and run that demo. In the start menu, click *Start in host mode*: the demo becomes a pure image generator waiting for a host.


![](run_host.png)


Then click *Run Host* in the *Host* group of the in-flight panel. The bundled emulator is started as a separate process, already pointed at the connection the demo has open, and the label next to the button reports what happened to it - *Starting...*, *Host connected*, *Host is down* or *Failed, see the log*. While a host is talking, the button stays disabled, because a second host would drive the same entities over the same connection.


![](run_host_panel.png)


### Using IG Host in IG Projects


To run IG Host with your IG application, copy the `ig_host` and `libcurl` library binaries from the `bin` folder of the demo to your project:


- For Windows - `ig_host_double_x64.exe, ig_host_double_x64d.exe, ig_host_double_x64d.pdb, libcurl.dll, libcurld.dll, libcurld.pdb`
- For Linux - `ig_host_double_x64, ig_host_double_x64d, libcurl.so, libcurld.so`


> **Notice:** The emulator is built against the double-precision engine, hence the **double** in the file names. The **d** suffix marks the debug build.


The following command line options are available on the IG Host start-up:


- `-cigi_host`, `-cigi_send`, `-cigi_recv` - the address of the IG and the ports to use. The ports are crossed relative to the IG: the host sends to the port the IG receives on, and vice versa.
- `-tile_sources` - path to the [tile sources](#general) file for the interactive map.
- `-default_state` - path to a [state file](#save_load) to be loaded on start-up, so that the host comes up with its entities, views and weather already in place.


```bash
ig_host_double_x64 -cigi_host "127.0.0.1" -cigi_recv 8889 -cigi_send 8888 -tile_sources "../data/tile_sources.json" -default_state "../data/default.state"
```


## IG Host Settings and Parameters


To make things work, you need to perform the following actions:


- Connect *IG Host* with IG.
- [Open the world (database)](#load) that provides the environment.
- [Add an entity](#add_entity).
- [Create a view](#set_view) attached to the entity, which is displayed in IG.
- Enable [control of the entity](#control_entity) movements.


### General Settings


In the IG Host window, open the *Settings* window (*File -> Settings*) and set the following parameters:


![](host_settings.png)


- *Pause* - freeze the host: it stops updating its own state and stops sending packets.
- *Async Mode* is **enabled** by default: the host updates at its own pace instead of waiting for an incoming packet from IG.
- *Host Frequency* - the update rate, in frames per second, used when *Async Mode* is disabled.
- *Database Geo Origin* - the coordinates that are set for the *Geodetic Pivot* in the world you have created.
- *Connector* - the protocol to talk to IG over. The settings of the selected connector are shown below in the same window: for CIGI these are the version, the address and ports, the packet size, interpolation, the *IG Mode* readout and the *Connect/Reconnect* and *Disconnect* buttons.
- *Tile Source* - the source of tiles used for the interactive map. You can add your own tile sources to the `data/tile_sources.json` file and specify the path to `tile_sources.json` in the `-tile_sources` startup argument for IG Host.


> **Notice:** *IG Mode* is not set by hand: the host reports RESET until a [database is loaded](#load) and switches to OPERATE as soon as one is. A value typed in while no database is loaded is overwritten on the next host update.


> **Notice:** If the map stays blank or fills with error tiles, switch *Tile Source* to another entry: a public tile server can refuse the requests outright. The setting is not saved between runs, so it has to be switched again on the next start-up - change the order in `tile_sources.json` to make another source the default, since the first one in the file is the one that comes up.


### Adding and Loading the World


To have an environment displayed in IG, you need to load a world (database).


![](load_database.png)


1. Open the *Database List* window (*Windows -> Database List*).
2. Select a database from the list.
3. Click *Load*.
4. Check if the world has been loaded in the IG window. Click *Connect/Reconnect* in the *Settings* window, if necessary.


> **Warning:** This step is not optional, and it is not only about the world: until a database is loaded, the host reports the RESET mode to IG and nothing in the simulation runs, so entities do not move even if the world is already on the screen. Loading a database is what switches the host to OPERATE.
>
>
> Two things make this easy to miss:
>
>
> - *Load* does nothing at all while no row is selected in the list - select the database first.
> - A [state file](#save_load) does not restore the database. A host that comes up from a saved state, or from the `-default_state` option, still starts with no database loaded.


You can add more databases to the list. The databases you want to add should be located inside the `/data` folder of the project you work with. To add another world to the database list:


![](add_database.png)


1. Click *Add*.
2. Specify the *Database ID*. It must not collide with an existing one, and it is the number the host sends to IG.
3. Select the `*.world` file to be loaded.
4. Specify the latitude and longitude of the geodetic pivot in that world.
5. Click *Ok*.


> **Warning:** A database added this way lives for the current session only: writing the configuration file back is temporarily unavailable, so the entry is lost when *IG Host* is closed, and the list itself is only re-read when the window is created. To add a database permanently, put it into the [databases section](../ig/config.md#config_databases) of `ig_config.xml` instead.


### Adding an Entity


The entity is added as follows:


![](entity.png)


1. Open the *Entities* window (*Windows -> Entity List*).
2. Click *Add* and specify the *Entity ID*. The field is pre-filled with the first free one, and the entity appears in the list right away. A host that was started with a [state file](#save_load) already has the entities from it, so there may be nothing to add.
3. Double-click an entity from the list to open *Entity Properties*.
4. Set the entity *Type* - the list offers the types declared in the [entity types](../ig/config.md#config_entities) section of `ig_config.xml` - and check its *Geo Pos*: the latitude, the longitude, and most importantly the altitude, to make sure the entity is not under the ground. When you enter digits, press Enter to confirm changes.
5. Set other parameters, if necessary.


All added entities are displayed on the interactive map where you can move them using the mouse cursor, thus changing the geoposition.


![](map.png)


### Setting the View


The view defines what actually is going to be displayed in IG.


![](view.png)


To open the view settings:


1. Open the *Views* list (*Windows -> Views List*).
2. Double-click a view from the list to open its properties.
3. Use *Position* and *Rotation* to adjust the camera relative to the entity. Both positive and negative values can be used.
4. *Parent Entity ID* - ID of the entity to which camera is attached. By changing this ID, you can switch between entities.


### Controlling the Entity


![](entity_control.png)


To move the entity around in IG:


1. Select the entity in the *Entities* list.
2. Open the *EntityControl* window (*Windows -> Entity Control*).
3. Activate the *Enabled* option.
4. Use **WASDQE** buttons and mouse movements to control the entity. The *Speed* value can be typed in, or changed on the fly with *Shift + Mouse Scroll* in the *Spectator* motion type and with *Mouse Scroll* alone in the *Airplane* one.
5. To exit the control entity mode, press Esc.


The *HUD Enabled* option of the same window draws the flight readout of the controlled entity in the IG Host window.


There are three *Motion Type* values available:


- *Spectator* - camera follows the entity.
- *Airplane* - the entity moves with a predefined speed, the direction is controlled by the mouse movements.
- *Circle* - the entity moves along a circle of the given *Radius* around the *Circle Center* coordinates, without any input. These two fields are editable only while this motion type is selected, and greyed out in the other two.


Only one entity can be controlled at a certain moment, switching to another entity stops the movement of the previous entity.


### Adjusting Weather Regions


To add or remove a weather region, open the *Weather Regions* window (*Windows -> Weather Regions List*):


![](regions.png)


Click *Add* and specify a new *Region ID*. Then you can double-click on the created region and the *Weather Region Properties* window will open (also available as *Windows -> Weather Region Properties*).


![](region_properties.png)


Here you can specify the general properties of the region and manage its layers. You can also specify the scope, position, rotation, and size using the map manipulators:


![](manipulators.gif)


The following manipulation operations for the region are available:


- Resize (yellow handles, only for Rectangle region scope)
- Drag (click)
- Rotate (mouse wheel)
- Adding and deleting handles (double-click, only for Polygon region scope)


### Adjusting Weather Layers


To add a new layer, click *Add* and specify *Layer ID* along with *type*.


![](new_layer.png)


The layer properties are shown at the bottom of the window and they can be edited.


![](layer_properties.png)


Besides the common parameters, each specific layer type has some unique parameters:


- **Precipitation Type** - rain or snow [precipitation](../ig/weather/settings.md#weather_precipitation).
- **Particles Size** - size of [precipitation](../ig/weather/settings.md#weather_precipitation) particles.
- **Cloud Type** - one of the [cloud types](../ig/ig_plugin.md#cloud_types) (custom or default).


### Setting the Weather


To control the weather, open the *Atmosphere* window (*Windows -> Global Weather*):


![](weather.png)


Currently the weather settings are the same as in [HEMU](http://cigi.sourceforge.net/product_he.php).


### Saving and Loading IG Host Settings


In the *File* menu, the *Save State* and *Load State* options are available. You can save all *IG Host* settings and load them as needed. The state is written as a `*.state` file and holds:


- the entities, the views and the view groups, with all of their properties;
- the global atmosphere settings;
- the weather regions with their layers.


Loading a state replaces everything in the list above, so the entities and regions that were there before are destroyed rather than merged with the ones being loaded.


The same file can be loaded on start-up with the `-default_state` command line option, which is how the [Cesium demo](../sdk/demos/cesium_ig.md) brings its aircraft, its view and its authored weather up together with the host.


> **Notice:** The [loaded database](#load) is not part of a restored state, so it has to be loaded from the *Database List* after a state file, every time.


## Sending CIGI Packets


To send packets, select the type of packets you want to send:


![](packets.png)


The corresponding window will open:


![](hathot.png)


You can open as many windows and send as many requests as you want.


DIS packets are sent the same way, from the *Windows -> Packets DIS* submenu.


## Logging CIGI Packets


*IG Host* allows tracing both sent and received packets.


In the *Settings* window (*File -> Settings*), click the *Packet Logger Filter* button to open the corresponding window:


![](open_filter.png)


In the window that opens, enable the CIGI option and the packets that should be logged.


![](logger_filter.png)


- Packets in the top area are the packets sent from Host to IG.
- Packets in the bottom area are the packets sent from IG to Host.


The information will be displayed in the console of the *IG Host* window (opened using the ` button).


## See Also


- *[Cesium](../sdk/demos/cesium_ig.md)* demo - the demo IG Host is shipped with
- *[Image Generator](../ig/index.md)* - the application on the other side of the connection
- *[IG Configuration](../ig/config.md)* - the [databases](../ig/config.md#config_databases) and [entity types](../ig/config.md#config_entities) the host offers in its lists
- *[Weather Settings](../ig/weather/settings.md)* - the weather parameters the host controls
