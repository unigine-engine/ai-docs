# IG Host

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


> **Warning:** This tool is experimental, some settings and parameters are still under development.


In the simulation industry, an image generator (IG) receives data from a host via an interface (such as CIGI). For demonstration of IG features and debugging purposes, we started developing *IG Host* — a cross-platform and cross-protocol solution. Currently, IG Host is a simplified version of CIGI *[HEMU](http://cigi.sourceforge.net/product_he.php)* and includes a number of useful advantages:


- Simplified entity control
- Transparent packet transfer (requests and responses can be viewed in the console)
- CIGI Debug mode
- Improved LOS responses


It is planned to add the HLA and DIS protocols in next versions.


## Running IG Host


IG Host is a part of [CIGI demo](../sdk/demos/cigi.md). Therefore, to try out IG Host, you need to download and run CIGI demo. In the *IG Configurator* window, click the *Run IG Host* button.


![](run_host.png)


Then click *Connect*.


### Using IG Host in IG Projects


To run IG Host with your IG application, copy the `ig_host` and `libcurl` library binaries from the `demos/cigi_demo/bin/` folder to your project:


- For Windows — `ig_host_x64.pdb, ig_host_x64.exe, ig_host_x64d.exe, libcurld.dll, libcurld.pdb, libcurl.dll`
- For Linux — `ig_host_x64, ig_host_x64d, libcurld.so, libcurl.so`


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


- *Async Mode* is **enabled** by default.
- *Database Geo Origin* — the coordinates that are set for the *Geodetic Pivot* in the world you have created.
- *Connector -> CIGI* settings, if necessary.
- *Tile Source* - the source of tiles used for generated terrain. You can add your own tile sources to the `data/tile_sources.json` file and specify the path to `tile_sources.json` in the `-tile_sources` startup agrument for IG Host.


### Adding and Loading the World


To have an environment displayed in IG, you need to load a world (database).


![](load_database.png)


1. Open the *Database List* window (*Windows -> Database List*).
2. Select a database from the list.
3. Click *Load*.
4. Check if the world has been loaded in the IG window. Click *Connect/Reconnect* in the *Settings* window, if necessary.


You can add more databases to the list. The databases you want to add should be located inside the `/data` folder of the project you work with. To add another world to the database list:


![](add_database.png)


1. Click *Add*.
2. Select the `*.world` file to be loaded.
3. Specify the latitude and longitude of the geodetic pivot in that world.
4. Click *OK*.
5. Reopen IG and *IG Host*.


### Adding an Entity


The entity is added as follows:


![](entity.png)


1. Open the *Entity List* window (*Windows -> Entity List*).
2. Double-click an entity from the list to open *Entity Properties*.
3. Set the entity Type, and check its position (most importantly along the Z axis to make sure it is not under the ground).
4. Set other parameters, if necessary.


All added entities are displayed on the interactive map where you can move them changing the geoposition.


![](map.png)


### Setting the View


The view defines what actually is going to be displayed in IG.


![](view.png)


To open the view settings:


1. Open the *Views* list (*Windows -> Views List*).
2. Double-click a view from the list to open its properties.
3. Use *Position* and *Rotation* to adjust the camera relative to the entity. Both positive and negative values can be used.
4. *Parent Entity ID* — ID of the entity to which camera is attached. By changing this ID, you can switch between entities.


### Controlling the Entity


![](entity_control.png)


To move the entity around in IG:


1. Select the entity in the *Entity List*.
2. Open the *EntityControl* window (*Windows -> Entity Control*).
3. Activate the *Enabled* option.
4. Click in the black area within the IG Host window.
5. Use **WASDQE** buttons and mouse movements to control the entity. Speed is controlled by using *Shift + Mouse Scroll* button.


There are three *Motion Types* available:


- *Spectator* — camera follows the entity.
- *Airplane* — the entity moves with a predefined speed, the direction is controlled by the mouse movements.
- *Circle* — entity moves circle-wise using the entered *Radius* and *Circle Center* coordinates.


Only one entity can be controlled at a certain moment, switching to another entity stops the movement of the previous entity.


### Adjusting Weather Regions


To add or remove a weather region, open the *Weather Regions* window (*Windows -> Weather Regions Properties*):


![](regions.png)


Click *Add* and specify a new ID for the region. Then you can double-click on the created region and a new *Weather Regions Properties* window will open.


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


To control the weather, open the *Atmosphere* window (*Windows -> Atmosphere*):


![](weather.png)


Currently the weather settings are the same as in [HEMU](http://cigi.sourceforge.net/product_he.php).


### Saving and Loading IG Host Settings


In the *File* menu, the *Save State* and *Load State* options are available. You can save all *IG Host* settings and load them as needed.


## Sending CIGI Packets


To send packets, select the type of packets you want to send:


![](packets.png)


The corresponding window will open:


![](hathot.png)


You can open as many windows and send as many requests as you want.


## Logging CIGI Packets


*IG Host* allows tracing both sent and received packets.


In the *Settings* window (*File -> Settings*), click the *Packet Logger Filter* button to open the corresponding window:


![](open_filter.png)


In the window that opens, enable the CIGI option and the packets that should be logged.


![](logger_filter.png)


- Packets in the top area are the packets sent from Host to IG.
- Packets in the bottom area are the packets sent from IG to Host.


The information will be displayed in the console of the *IG Host* window (opened using the ` button).
