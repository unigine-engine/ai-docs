# IG Application Template

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


## Overview


The **Image Generator** (IG) renders scenes of the virtual world, providing an immersive view of the simulation, it can be thought of as a *viewport* into the virtual world of simulation. A simulator may have one or more IG channels rendering an "out-the-window" view and might have several additional views representing various sensors: electro-optical (EO), infrared (IR), and night vision (NV); and sometimes radar. The way these views are displayed may vary from a simple desktop monitor to a multiple projector dome display.


To synchronize the IG application and launch it across the machines of a multi-projector or **CAVE** setup, use the [IG Control Panel](../ig/ig_control_panel.md) tool.


![](displays.png)


The IG uses the [**terrain database**](#database) and a set of [**entities**](#entity) (aircrafts, vehicles, etc.) to render a scene, along with sky, weather and visual effects, from the specified perspective, and sends a video signal to the appropriate display within the user interface.


The IG receives updates and events from all the other hosts from the network, be it a vehicle/aircraft simulation host, instructor operator station (IOS), physical simulation host, etc. The IG also responds to requests from other hosts to check for intersections with the terrain to determine if the vehicle/aircraft bumps into anything or has a *line-of-sight* to another entity(ies).


The simulator and the IG can be integrated into a single application, where the simulator uses [API calls](../api/library/plugins/ig/api/index.md) to control the IG. Or, the simulator can be connected to the IG via a network connection and communicate by sending/receiving messages specified by an interface control document such as **CIGI** (Common Image Generator Interface). Or, they can be connected using the distributed simulation network and pass messages using communication protocols such as **DIS** or **HLA**.


![Communication Protocols](protocols.png)


HLA is a standard for interoperability among simulations. Rather than a networking protocol (wire standard) like DIS, HLA defines an architecture with a set of Application Programmer�s Interface (API) Standards. Simulation applications (known as federates) communicate by making calls to the HLA APIs. A piece of software known as the Runtime Infrastructure (RTI) implements the HLA API, and is responsible for transporting data from one federate to another.


An **Entity** is a static or dynamic simulation object that can be created, manipulated, and destroyed by the host. The virtual world is filled with entities, they represent certain objects of the real world (e.g. aircrafts, vehicles, ships, etc.)


A **Terrain Database** (or simply *Database*) is a virtual model of the landscape where the simulation takes place. Its character, quality, and content defines what can be done in the simulation environment. The resolution and level of detail of the terrain database content define the fidelity of interactions possible within the environment. UNIGINE supports [double-precision coordinates](../code/double_precision/index.md) enabling you to extend geographic coverage of the terrain, that defines the size of the area where the simulation can take place, up to the whole Earth's surface.


There�s more in a scene than the [terrain database](#database) and the [entities](#entity) moving around � **sky, atmosphere**, and **water**. Drawing these ethereal parts of the environment is the IG�s responsibility too. Since their appearance varies dramatically depending on the weather and the time of day, several models are implemented to simulate the environment:


- An **ephemeris model** determines the position of the sun and moon, which both cast light into the scene, depending on given coordinates and date/time.
- A **weather model**, either in the IG or supplied by an external weather simulation, provides the cloud coverage, and a global wind concept with direction and strength, affecting vegetation animation and the environment.


UNIGINE's IG is designed to be simple, easy to use and [extensible](#extension) via its plug-in based architecture. The main framework plugin, that manipulates systems, entities, articulated parts, component templates and so on, is the [IG Plugin](../api/library/plugins/ig/api/index.md), it operates in terms of the UNIGINE Engine (Nodes, NodeReferences, etc.) and is not bound to any specific communication protocol. The IG plugin has a set of additional plugins, called **connectors**, that are used to link IG terminology with that of each specific protocol (e.g. CIGI, HLA, DIS). Basically, the architecture looks as follows:


![IG](ig_structure.png)


Within the IG, all entities, lights, databases, etc. are referred to via IDs. Simple articulation of entities' parts is performed based on [XML definition](../ig/config.md) and does not require a modeler to prepare any animations.


UNIGINE IG is currently implemented as **IG Template**.


<details>
<summary>Currently supported CIGI packets | Close</summary>

**Currently supported CIGI packets**


| Type | Supported | Not Supported |
|---|---|---|
| **ig_control** | FULL |  |
| **entity_control** | Extrapolation/Interpolation Enable | Alpha |
| **entity_clamped_control** | FULL |  |
| **component_control** | Component classes: ENTITY, VIEW, GROUP | SENSOR, REG_WATER, REG_TERRAIN, REG_WEATHER, GLOBAL_WATER, GLOBAL_TERRAIN, GLOBAL_WEATHER, ATMOSPHERE, CELESTIAL, EVENT, SYSTEM, SYMBOL_SURFACE, SYMBOL |
| **component_short_control** | Component classes: ENTITY, VIEW, GROUP | SENSOR, REG_WATER, REG_TERRAIN, REG_WEATHER, GLOBAL_WATER, GLOBAL_TERRAIN, GLOBAL_WEATHER, ATMOSPHERE, CELESTIAL, EVENT, SYSTEM, SYMBOL_SURFACE, SYMBOL |
| **articulated_control** | FULL |  |
| **articulated_short_control** | FULL |  |
| **rate_control** | FULL |  |
| **celestial_control** | FULL |  |
| **atmosphere_control** | FULL |  |
| **environment_control** | FULL |  |
| **weather_control** | FULL (except for Weather Entities) |  |
| **maritime_control** | FULL |  |
| **wave_control** | **SUPPORTED:** Waveheight (Beaufort level, not in meters), Direction. > **Notice:** Other parameters such as *Wavelength, Phase Offset, Leading*, and others are automatically calculated on the basis of the current Beaufort value to ensure realistic simulation. |  |
| **terrestrial_control** | NOT SUPPORTED |  |
| **view_control** | FULL |  |
| **sensor_control** | NOT SUPPORTED |  |
| **tracker_control** | NOT SUPPORTED |  |
| **earth_model_def** | NOT SUPPORTED |  |
| **trajectory_def** | FULL |  |
| **view_def** | FULL |  |
| **segment_def** | FULL |  |
| **volume_def** | FULL |  |
| **hat_hot_request** | FULL, with Extended Response and Update Period parameter |  |
| **los_segment_request** | PARTIAL, with Extended Response and Update Period parameter | Alpha Threshold, Color |
| **los_vector_request** | PARTIAL, with Extended Response and Update Period parameter | Alpha Threshold |
| **position_request** | FULL, with Update Period parameter |  |
| **environment_request** | Weather Conditions Request: wind(sum), humidity(max), barometric(max), visibility(minimum), temperature(average) | Maritime Surface Conditions, Terrestrial Surface Conditions |
| **symbol_surface_def** | PARTIAL |  |
| **symbol_text_def** | PARTIAL |  |
| **symbol_circle_def** | PARTIAL |  |
| **symbol_line_def** | PARTIAL |  |
| **symbol_clone** | NOT SUPPORTED |  |
| **symbol_control** | PARTIAL |  |
| **symbol_short_control** | PARTIAL |  |

</details>


### Interpolation and Extrapolation


Unigine IG uses **Interpolated Snapshots** (IS) to tackle with the problem of lost packets between the IG and hosts. It works by taking two old, but known positions and interpolating the object between them. It is accomplished by having a buffer of received positions and rotations, along with the time they represent. We usually take our current local time minus some predefined amount � **interpolation period** (**40** ms by default), then go into our buffer, find the two indices that are just before and just after this time and interpolate.


If we don't have a received position and rotation for the time we're looking for, the **extrapolation** (guessing) is used. It also has a limited time � **extrapolation period** (**200** ms by default). If the extrapolation period is over but there are still no packets received, all objects will freeze.


In most cases, this method provides a very accurate representation of the world to each slave, as in general only already known positions of remote objects are rendered and in rare cases the system will try to extrapolate (guess) where an object is. This, however, comes at a cost, as we always render **40** ms (interpolation period) behind current time, so that new packets have time to arrive with data.


### Video Tutorial: Quick Start With IG Template


### See Also


- The [IG plugin API](../api/library/plugins/ig/api/index.md) section for more details on managing IG via code (C++).
- The [Setting Up Properties](../ig/properties_setup.md) article for more details on adjusting properties for new entities.
- The [IG Configuration](../ig/config.md) article for more details on setting up your IG.
- The [Weather Plugin](../ig/weather/index.md) articles for more details on configuring sky and weather parameters.


## Using the IG Template


The basic workflow is as follows:


1. Open the SDK Browser, go the the *Templates* tab, and [create a new project](../sdk/projects/index_cpp.md#creation) using the **IG** Template. ![Create a Project](sdk_bro.png) To create a VR-based project, set the required **Stereo 3D** mode in the *[Global Options](../sdk/index.md#options)* tab. The newly created project will support both VR and IG features out of the box. ![](vr_mode.png)
2. Open the world in UnigineEditor by clicking **Open Editor**. ![Open the UnigineEditor](../sdk/projects/run_editor.png)
3. Use the [Sandworm Tool](../editor2/sandworm/index.md) to [generate a terrain](../editor2/sandworm/interface/index.md).
4. Add models (as [node references](../objects/nodes/reference/index.md)) to represent entities used in your simulation (aircrafts, vehicles, etc.). [Assign properties](../ig/properties_setup.md) (lights, landing gears, wheels, controllers, effects, etc.) to the corresponding nodes and adjust their parameters as required. ![Add Models and Adjust Properties](entity_config.png)
5. Save your world and close Unigine Editor.
6. Open the [configuration file](../ig/config.md) (`ig_config.xml`) and add [definitions](../ig/config.md#config_entities) for all your entities, specify necessary system settings and connector parameters. ![Add Models and Adjust Properties](step4.jpg)
7. Launch your IG application by clicking **Run**. ![Run the Application](../sdk/projects/run_level.png) > **Notice:** By default your application will launch with **IG, CIGIConnector** plugins. If you want to change this, please modify the [startup options](../sdk/projects/index_cpp.md#customize_run) after clicking an ellipsis under the **Run** button for your project on the *Projects* tab of the SDK Browser.
8. Launch your host application or a CIGI Host Emulator to communicate with your IG. ![](step5.jpg)


## IG Synchronization System


The IG has its own synchronization system with the [Syncker plugin](../code/plugins/syncker/index.md) initialized automatically. To use a **Multi-IG** configuration, you should specify additional startup command-line arguments. There are common arguments used for both Master and Slave, and specific ones. The list of all available arguments for IG network configuration is given in the [Syncker-Specific Options](../code/plugins/syncker/options.md) article.


IG launching order does not matter (you can run the Master and then Slaves, or vice versa). What is important is that you should specify the proper number of IGs for the Master via the *-sync_count* argument. Please note, that it is the total number of IG hosts, not the number of Slaves (e.g.: if you have **1** Master and **2** Slaves, you should specify: **-sync_count 3**).


IG uses the only port (the one used by Syncker): **UDP 8890**


This means that two messages reporting successful connections must appear in the Console.


For a **Slave** it looks as follows:


```text
IG::Manager::on_ig_connected(): Connection to "IG Master" (ip:port) has been established //< - message from IG
Syncker::Slave::connect_to_master(): connection to "ip" accepted in 0.00 seconds //<- message from Syncker

```


For the **Master** it looks as follows:


```text
IG::Manager::on_ig_connected(): Connection to "IG Slave" (ip:port) has been established <- from IG
Syncker::Master::check_new_connections(): connection from "ip" "slave" accepted in 0.00 seconds <- from Syncker
IG::Manager::on_ig_connected(): all connections established. Session started <- from IG

```


The last message means that the Master has established all necessary connections and is ready to work.


If the IG is launched with a connector, the latter starts using IG API immediately, without waiting for all connections. Therefore, the Master switches to blocking mode (the window is not refreshed) with the following message printed to the Console:


```text
IG::Manager::wait_for_all_connections(): waiting for all connections within a minute�

```


Thus, you have one minute to connect all IGs. If no hosts are connected to IG during this period, the Master will shut down reporting to the [Console](../code/console/index.md) that connections were not established.


> **Notice:** To configure rendering of multiple viewports, [*SpiderVision* plugin](../principles/render/output/multi_monitor/spidervision_plugin/index.md) should also be enabled.


So, the minimum number of arguments required to launch IG on two computers looks as follows:


**Master:**

```bash
-extern_plugin "UnigineSpiderVision,UnigineIG,UnigineCIGIConnector" -sync_master 1 -sync_count 2
```


**Slave:**

```bash
-extern_plugin "UnigineSpiderVision,UnigineIG" -sync_master 0
```


Please note that if there are no explicitly specified IP addresses, IG will try to define addresses automatically.


> **Notice:** IG Master and IG Slaves must be in the same isolated subsystem. In case of several IG Masters in the network you should specify their IP addresses explicitly, as automatic detection is not available.


Here is a typical number of arguments when launching IG hosts:


**Master:**

```bash
-extern_plugin "UnigineSpiderVision,UnigineIG,UnigineCIGIConnector" -sync_master 1 -sync_count 3 -computer_name left
```


**Slave 1:**

```bash
-extern_plugin "UnigineSpiderVision,UnigineIG" -sync_master 0 -computer_name center
```


**Slave 2:**

```bash
-extern_plugin "UnigineSpiderVision,UnigineIG" -sync_master 0 -computer_name right
```


## Adaptive Quality Management


Simulations usually operate with large numbers of various entities which are often represented by complex hierarchies. To keep performance high a proper optimization is required, as transforming and rendering the whole hierarchy of an entity that is hardly visible wastes a lot of computational resources.


A special [*Simplifier*](../ig/properties_setup.md#model_simplification) component can help optimize rendering of your entities. This component, when assigned to an entity, enables you to define which parts of its model can be neglected starting at certain distance levels (e.g., hide flaps, ailerons, and rudders at 1km, engines at 5 km, etc.) and which substitutes can be used to represent an entity at a large distance (e.g., a flashing strobe light, when the plane is just a point on the screen).


The Adaptive Quality system provides automatic real-time adjustment of levels of detail depending on current performance. This system works together with entity model simplification mechanism described above and automatically drops off details as performance decreases and restores it back when the conditions get better. Parameters of the system are available in the [IG Configuration](../ig/config.md#aqs_tags).


## Extending Template's Functionality


UNIGINE's IG provides the following opportunities for customization:


- IG can be built into a Qt/WinForm/WPF application and have a custom interface (e.g., switching between cameras in the simplest case).
- A host can have several IGs connected, and each running IG can be programmed to have its own logic, if necessary.
- Secondary static objects (such as a billboard on a building or a ship following a certain route) can be animated, and their position, rotation, or other specific parameters can be requested via CIGI/HLA.
- New visual effects can be created to create a more realistic picture.
- Users can [add their own custom components](../ig/custom_component.md) and process them by modifying the [`ig_config.xml`](../ig/config.md) file.
- You can extend IG functionality to support other protocols (e.g. ALSP, TENA, CTIA, etc. ), for this purpose you'll have to write your own [connectors](#connector).


### Adding a Custom Connector


A connector is actually a custom [C++ Plugin](../code/cpp/plugin.md) used to communicate messages between the host and the IG. This plugin reads packages and calls the corresponding methods of the [IG Plugin](../api/library/plugins/ig/api/index.md) (listed in *include/plugins/Unigine/IG/UnigineIG.h*).


Files listed below can be used as a template for your custom connector:


- Plugin include file to be put to the `include/plugins` folder: <details> <summary>CUSTOMConnectorInterface.h | Close</summary> **CUSTOMConnectorInterface.h** ```cpp #ifndef __CUSTOM_CONNECTOR_INTERFACE_H__ #define __CUSTOM_CONNECTOR_INTERFACE_H__ namespace IG { namespace CUSTOM { class ConnectorInterface { public: virtual ~ConnectorInterface() {} // client initialization virtual int init(/*initialization parameters*/) = 0; // client shutdown virtual int shutdown() = 0; // other methods // ... // callbacks //virtual void setConnectCallback(Unigine::CallbackBase* func) = 0; //virtual Unigine::CallbackBase* getConnectCallback() const = 0; // ... }; } } #endif /* __CUSTOM_CONNECTOR_INTERFACE_H__ */ ``` </details>
- Plugin source files to be put to the `source/custom_connector` folder: <details> <summary>CUSTOMConnectorPlugin.cpp | Close</summary> **CUSTOMConnectorPlugin.cpp** ```cpp #include <UniginePlugin.h> #include "CUSTOMConnector.h" #include "CUSTOMConnectorInterpreter.h" using namespace Unigine; ////////////////////////////////////////////////////////////////////////// // CUSTOMConnectorPlugin ////////////////////////////////////////////////////////////////////////// class CUSTOMConnectorPlugin : public Plugin { public: CUSTOMConnectorPlugin(); virtual ~CUSTOMConnectorPlugin(); const char *get_name() override; void *get_data() override; int init() override; int shutdown() override; void update() override; private: IG::CUSTOM::Connector *connector; }; CUSTOMConnectorPlugin::CUSTOMConnectorPlugin() : connector(nullptr) { } CUSTOMConnectorPlugin::~CUSTOMConnectorPlugin() { CUSTOMConnectorInterpreterShutdown(); delete connector; } const char *CUSTOMConnectorPlugin::get_name() { return "CUSTOMConnector"; } void *CUSTOMConnectorPlugin::get_data() { return static_cast<IG::CUSTOM::ConnectorInterface *>(connector); } int CUSTOMConnectorPlugin::init() { connector = new IG::CUSTOM::Connector(); connector->init(); CUSTOMConnectorInterpreterInit(); return 1; } int CUSTOMConnectorPlugin::shutdown() { connector->shutdown(); return 1; } void CUSTOMConnectorPlugin::update() { connector->update(); } ////////////////////////////////////////////////////////////////////////// // Plugin export ////////////////////////////////////////////////////////////////////////// extern "C" UNIGINE_EXPORT void *CreatePlugin() { return new CUSTOMConnectorPlugin(); } extern "C" UNIGINE_EXPORT void ReleasePlugin(void *plugin) { delete static_cast<CUSTOMConnectorPlugin *>(plugin); } ``` </details> <details> <summary>CUSTOMConnector.h | Close</summary> **CUSTOMConnector.h** ```cpp #ifndef __CUSTOM_CONNECTOR_H__ #define __CUSTOM_CONNECTOR_H__ #include <plugins/CUSTOMConnectorInterface.h> #include <plugins/Unigine/IG/UnigineIG.h> #include <UnigineInterface.h> #include <UnigineLogic.h> namespace IG { namespace CUSTOM { class CUSTOMWorldLogic; class Connector : public ConnectorInterface { public: Connector(); virtual ~Connector() {} // singleton static Connector *get() { if (connector == nullptr) Log::fatal("%s:: CUSTOM connector is NULL\n", __FUNCTION__); return connector; }; // automatic initialization on plugin load void init(); // update/shutdown client void update(); void shutdown(); // methods to be called by the CUSTOMWorldLogic class at the corresponding stages of the execution sequence void onWorldInit(); void onWorldShutdown(); private: static Connector *connector; IG::Manager *ig_manager = nullptr; CUSTOMWorldLogic *world_logic; }; // WorldLogic class class CUSTOMWorldLogic : public Unigine::WorldLogic { public: CUSTOMWorldLogic() {} virtual ~CUSTOMWorldLogic() {} virtual UNIGINE_INLINE int init() override { Connector::get()->onWorldInit(); return 1; } virtual UNIGINE_INLINE int shutdown() override { Connector::get()->onWorldShutdown(); return 1; } }; } } #endif /* __CUSTOM_CONNECTOR_H__ */ ``` </details> <details> <summary>CUSTOMConnector.cpp | Close</summary> **CUSTOMConnector.cpp** ```cpp #include "CUSTOMConnector.h" #include <UnigineEngine.h> #include <UnigineNode.h> using namespace Unigine; using namespace Math; using namespace IG; using namespace CUSTOM; Connector::Connector() { world_logic = new CUSTOMWorldLogic(); Engine::get()->addWorldLogic(world_logic); } void Connector::init() { const auto host = "127.0.0.1"; const auto port = 3000; int ig_plugin_index = Engine::get()->findPlugin("IG"); if (ig_plugin_index == -1) { Log::error("IG::CUSTOM::Connector::init(): IG plugin isn't loaded\n"); return; } ig_manager = (IG::Manager*)Engine::get()->getPluginData(ig_plugin_index); // IG setup ig_manager->setCoordinateSystem(IG::Manager::COORDINATE_SYSTEM::NED); } void Connector::update() { // read & write packets } void Connector::shutdown() { // shutdown client shutdown(); // clear static link connector = nullptr; // ... } void Connector::onWorldInit() { // actions to be performed when a new world is loaded } void Connector::onWorldShutdown() { // actions to be performed when current world is closed } ``` </details> <details> <summary>CUSTOMConnectorInterpreter.h | Close</summary> **CUSTOMConnectorInterpreter.h** ```cpp #ifndef __CUSTOM_CONNECTOR_INTERPRETER_H__ #define __CUSTOM_CONNECTOR_INTERPRETER_H__ #include <UnigineBase.h> void CUSTOMConnectorInterpreterInit(); void CUSTOMConnectorInterpreterShutdown(); #endif /* __CUSTOM_CONNECTOR_INTERPRETER_H__ */ ``` </details> <details> <summary>CUSTOMConnectorInterpreter.cpp | Close</summary> **CUSTOMConnectorInterpreter.cpp** ```cpp #include <UnigineEngine.h> #include <UnigineInterface.h> #include <plugins/CUSTOMConnectorInterface.h> #include "CUSTOMConnector.h" using namespace Unigine; using namespace IG; void CUSTOMConnectorInterpreterInit() { int id = Interpreter::addGroup("CUSTOMConnectorInterpreter"); // defines Interpreter::addExternDefine("HAS_CUSTOM_CONNECTOR", id); // enums // Interpreter::addExternVariable("CUSTOM_VERSION_10", MakeExternConstant<int>(CUSTOM_VERSION_10), id); // functions Connector *connector = Connector::get(); Interpreter::addExternLibrary("engine.custom", id); //Interpreter::addExternFunction("engine.custom.init", MakeExternObjectFunction(connector, &Connector::init), id); //Interpreter::addExternFunction("engine.custom.shutdown", MakeExternObjectFunction(connector, &Connector::shutdown), id); } void CUSTOMConnectorInterpreterShutdown() { Interpreter::removeGroup("CUSTOMConnectorInterpreter"); } ``` </details> <details> <summary>CUSTOMConnectorWrapper.cpp | Close</summary> **CUSTOMConnectorWrapper.cpp** ```cpp //push ignore deprecated warnings #ifdef __GNUC__ #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Wdeprecated-declarations" #elif defined(_MSC_VER) #pragma warning(push) #pragma warning(disable: 4996) #endif #include <UnigineEngine.h> #include <plugins/CUSTOMConnectorInterface.h> using namespace Unigine; extern "C" { //UNIGINE_EXPORT void CUSTOMConnector_method(CUSTOMConnector *self) { if (self) self->method(); } } //pop ignore deprecated warnings #ifdef __GNUC__ #pragma GCC diagnostic pop #elif defined(_MSC_VER) #pragma warning(pop) #endif ``` </details>
