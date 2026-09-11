# Mars Demo


![](mars_0.png)

![](mars_1.png)


***Mars*** demo project recreates one million square kilometers of the Mars surface. You can drive the rover around the planet and view the Gale Crater using a 20x scopes support!


This demo showcases features of the *[Landscape Terrain](../../objects/objects/terrain/landscape_terrain/index.md)* system. No static meshes involved, only a terrain object.


## Features


- Highest geometry and texture detailing possible (up to 1 millimeter per pixel)
- **1000 x 1000** km area size
- **8 x 8** km high-detailed zone (0.25 m / pixel mask density, 1 mm / pixel for detailed 4K textures)
- Dynamic craters (100 x 100 x 25 m) that can be placed in real-time anywhere
- Rover tracks as another demonstration of real-time modification of terrain surface
- Up to 20x scopes


## System Requirements


To run this demo, the following is required:


- Video memory: **minimum** 2 GB � this would allow running the demo with Low and Medium quality. With the memory less than this, the demo will not run.

  - **Low** � 2048 MB
  - **Medium** � 2048 MB
  - **High** � 3072 MB
  - **Ultra** � 4096 MB
- Disk space: 12 GB


We tested this with nVidia GeForce GTX 1080Ti, and it worked fine, so you can evaluate your possibilities based on this.


**SDK Path:***<SAMPLES_PROJECT_PATH>/demos\mars_2.21*
## Accessing Demo Source Code

You can study and modify the source code of this demo to create your own projects. To access the source code do the following:

1. Find the **Mars Demo** demo in the *Demos* section and click **[Install](/sdk/#samples)** (if you haven't installed it yet).
2. After successful installation the demo will appear in the *Installed* section, and you can click **Copy as Project** to create a project based on this demo. ![](../../sdk/demos/copy_as_project_gen.png)
3. In the **Create New Project** window, that opens, enter the name for your new project in the corresponding field and click **Create New Project**. ![](../../sdk/projects/create_project_cpp.png)
4. Now you can click **Open Code IDE** to check and modify source code in your default IDE, or click **Open Editor** to open the project in the [UnigineEditor](/editor2/). ![](../../sdk/projects/edit_code.png)
