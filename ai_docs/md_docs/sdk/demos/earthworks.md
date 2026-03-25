# Earthworks Demo

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


![](earthworks_001.png)


***Earthworks*** demo features a backhoe loader that can be operated to drive across the construction site, dig holes and trenches. Digging is performed via voxelization of terrain volume inside the bucket and baking of voxels back into the heightmap after dumping.


Terrain in the *Earthworks demo* resists digging, and bucket filling affects backhoe handling. With simulation of material flow and crumbling of piles while unloading a bucket the whole process looks almost real.


## Features


- Vehicle [leaving traces](../../objects/objects/terrain/landscape_terrain/index.md#modification) behind
- Switching between operator cabin view and view from outside
- Excavation activities with the soil withdrawal by the tractor digging bucket performed via voxelization of terrain volume inside the bucket and baking of voxels back into the heightmap after dumping
- Modification (build-up) of terrain using [Particle Systems](../../objects/effects/particles/index.md) and [*Landscape Terrain* brushes](../../editor2/brush_editor/index.md) to simulate soil unloaded from the bucket


**SDK Path:***<SAMPLES_PROJECT_PATH>/demos\earthworks_2.21*
## Accessing Demo Source Code

You can study and modify the source code of this demo to create your own projects. To access the source code do the following:

1. Find the **Earthworks Demo** demo in the *Demos* section and click **[Install](/sdk/#samples)** (if you haven't installed it yet).
2. After successful installation the demo will appear in the *Installed* section, and you can click **Copy as Project** to create a project based on this demo. ![](../../sdk/demos/copy_as_project_gen.png)
3. In the **Create New Project** window, that opens, enter the name for your new project in the corresponding field and click **Create New Project**. ![](../../sdk/projects/create_project_cpp.png)
4. Now you can click **Open Code IDE** to check and modify source code in your default IDE, or click **Open Editor** to open the project in the [UnigineEditor](/editor2/). ![](../../sdk/projects/edit_code.png)
