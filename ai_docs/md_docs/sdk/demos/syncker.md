# Syncker Demo


![](syncker_001.png)


***Syncker*** demo showcases the capabilities of the UNIGINE *[Syncker](../../code/plugins/syncker/index.md)* plugin. This plugin provides robust and reliable frame synchronization for real-time content rendering in a multi-node network cluster, fully customizable via API.


## Features


- Automatic synchronization of [global water](../../objects/objects/water/water_object.md) (*[ObjectWaterGlobal](../../api/library/objects/class.objectwaterglobal_cpp.md)*), [cloud layers](../../objects/objects/cloud_layer/index.md) (*[ObjectCloudLayer](../../api/library/objects/class.objectcloudlayer_cpp.md)*), [world light sources](../../objects/lights/world/index.md) (*[LightWorld](../../api/library/lights/class.lightworld_cpp.md)*), and [particle systems](../../objects/effects/particles/index.md) (*[ObjectParticles](../../api/library/objects/class.objectparticles_cpp.md)*).
- Synchronization of dynamic objects moving along the trajectories set by splines (vessel, boats, aircrafts).
- Behavior of static nodes (buoys), that have their position determined by the ObjectWaterGlobal. These nodes are not synchronized, but their positions are adjusted indirectly via global water (*ObjectWaterGlobal*) synchronization.
- Synchronization of child nodes in the NodeReference hierarchy (helicopter rotors).
- Creation of objects and enabling physical interactions for them.
- Setting individual logic and controls for each slave.
- Setting cameras on slaves to target different objects.
- Changing a slave's logic.
- Various [addressing modes](../../code/plugins/syncker/index.md#addressing_modes): *Unicast, Multicast, Broadcast*.
- Animating objects based on the current time if their position can be pre-defined to optimize network data transfer.
- Making *Syncker* a network library.


## Running the Demo


As you run the demo, you'll see the *Syncker Configurator* window.


![](syncker_002.png)


| Addressing method | Selection of the [addressing mode](../../code/plugins/syncker/index.md#addressing_modes). |
|---|---|
| Master UDP Port | UDP port to be used for message exchange between the *Master* and *Slaves*. |
| Demo | A scene demonstrating a certain aspect of the *Syncker* Plugin. As soon as you select a scene from the dropdown list, its brief description is displayed below. |
| Peers Count | The number of instances you are going to run. For example, if you plan to run a *Master* and two *Slaves*, enter 3 in this field and run two more instances of this demo scene as *Slaves*. |
| Allow adding new slaves after the session has started | Enabling this option allows connecting slave PCs that are run after the Master instance has started. Otherwise, only the slaves that have been running prior to starting the Master would be connected. |
| Run Master | Run the current instance as *[Master](../../code/plugins/syncker/index.md#work)*. |
| Allow reconnecting slaves after the session has finished (currently doesn't work with extra slaves) | Enabling this option allows reconnecting slave PCs after a disconnection. |
| Run Slave | Run the current instance as *[Slave](../../code/plugins/syncker/index.md#work)*. |
| View | Define the position of the image rendered by the current instance in the overall panorama. |
| Swap Mode | Set the buffer [swapping method](../../code/plugins/syncker/options.md#sync_swap) to be used by Syncker: - Default - NVIDIA (available only for NVIDIA Quadro GPUs with G-SYNC support) |


When the required number of instances has been run, the scene opens and the information about the demo is displayed in the *Master* instance.


**SDK Path:***<SAMPLES_PROJECT_PATH>/demos\syncker_2.21*
## Accessing Demo Source Code

You can study and modify the source code of this demo to create your own projects. To access the source code do the following:

1. Find the **Syncker Demo** demo in the *Demos* section and click **[Install](/sdk/#samples)** (if you haven't installed it yet).
2. After successful installation the demo will appear in the *Installed* section, and you can click **Copy as Project** to create a project based on this demo. ![](../../sdk/demos/copy_as_project_gen.png)
3. In the **Create New Project** window, that opens, enter the name for your new project in the corresponding field and click **Create New Project**. ![](../../sdk/projects/create_project_cpp.png)
4. Now you can click **Open Code IDE** to check and modify source code in your default IDE, or click **Open Editor** to open the project in the [UnigineEditor](/editor2/). ![](../../sdk/projects/edit_code.png)
