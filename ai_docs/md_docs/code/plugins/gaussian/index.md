# GaussianSplatting Plugin

       Sorry, your browser does not support embedded videos.
The *GaussianSplatting* plugin allows importing 3D Gaussian Splatting (`*.ply`) files into a UNIGINE application and rendering them in real time.


Apart from rendering, the plugin can [generate collision geometry](#collision_generator) for a 3DGS object. It makes splat-based content available to physics, character controllers, intersections, and any other systems that rely on collision.


*3D Gaussian Splatting (3DGS)* primarily uses the *PLY (Polygon File Format)* to store the parameters of millions of Gaussians that define a 3D scene. Because raw *PLY* files are often very large, specialized compressed formats have been developed to reduce file sizes for web and mobile viewing.


**Primary 3DGS File Formats**:


1. **PLY (.ply)**: The standard format for 3D Gaussian Splat data. It stores vertex data, including:

  - Position: 3D coordinates.
  - Scale: Size of the Gaussian along each axis.
  - Rotation: Quaternion for orientation.
  - Opacity: Transparency value.
  - Spherical Harmonics (SH): Color encoding.
2. **SPLAT (.splat)**: A highly efficient, compressed binary format specifically optimized for web-based rendering and real-time viewing.
3. **SPZ (.spz)**: An open-source format developed by Niantic (Scaniverse) designed to act like a "JPG for Gaussian Splatting", offering ~90% compression (10x smaller) compared to standard PLY files, with minimal quality loss.
4. **SOG (Self-Organizing Gaussians)**: Developed by PlayCanvas, this format compresses gaussian PLY files by over 90% by optimizing the data structure.
5. **LCC (.lcc)**: An open-source format by XGRIDS focusing on high-density scene compression and Level-of-Detail (LOD) streaming.
6. **KSPLAT (.ksplat**): A custom, highly compressed format used in *Three.js* implementations for optimized loading.


> **Notice:** Currently, only `.ply` files are supported for Gaussian Splatting assets in UNIGINE. If your data is stored in a different format, you can convert it to `.ply` using third-party tools, for example *[3dgsconverter](https://github.com/francescofugazzi/3dgsconverter)*.


### See Also


- sample in *C++ SIM Samples*
- ***[Gaussian Splatting](../../../sdk/demos/gaussian_splat.md)*** demo


## Launching GaussianSplatting Plugin


To use the *GaussianSplatting* plugin, load it via the `plugin_load` console command or specify the `extern_plugin` command line option on the application start-up:


```bash
-extern_plugin "UnigineGaussianSplatting"
```


## Using GaussianSplatting Plugin


To add a Gaussian Splatting file to the scene, do the following:


1. Open the *Templates* tab in the SDK browser and choose a template that meets your needs. Click *Create Project*. ![](../../../sdk/projects/create_project_cpp.png)
2. In the project creation window that opens, click *Advanced Settings > Plugins*.
3. Enable the `Gaussian Splatting plugin`, click *Add* and *CREATE NEW PROJECT*. The project will appear in the *My Projects* tab list. ![](gaussian_add.png)
4. When the project is created, click the *Customize Unigine Editor Options* button on the projects card, and add the additional argument `-extern_plugin "UnigineGaussianSplatting"`. ![](customize_editor.png)
5. Open UnigineEditor.
6. Create a *Node Dummy* and assign the ***gaussian*** property to it (this property is available in the project as a part of the plugin).
7. In the property parameter ***Gaussian Ply File***, assign the `*.ply` file that you want to render.
8. Adjust other parameters, if necessary.
9. If the splats should participate in physics, be intersected, or cast shadows, assign the ***GaussianCollisionGenerator*** property to the same node and [generate collision geometry](#collision_generator) for it.


![](gaussian_prop_settings.png)


### Gaussian Property Parameters


The *Gaussian* property contains the following parameters available for adjustment:


| Gaussian Ply File | The `*.ply` file containing 3D Gaussian splatting [3DGS] scene. |
|---|---|
| Render Order | The order of rendering the 3DGS object. The object with the highest render order will be rendered last (on top of all other 3DGS objects). The default value is 0. |
| Render Sequence Order | Specifies at which stage of the rendering pipeline the splats are rendered: - **Transparent** � splats are rendered together with other transparent objects. - **After Tonemapping** � splats are rendered after the tonemapping stage, avoiding tonemapping influence. Set by default. - **After Post Effects** � splats are rendered after all post-processing effects are applied. |
| Gaussian Render Material | The material used for rendering the gaussians. It has a set of [parameters](#mat_parameters) that can be changed to adjust the look of the 3DGS render. |
| Gaussian Utils Material | Utility material used to initialize Gaussian data and calculate distance from camera for each Gaussian splat. |
| Sorting Material | Material used for Gaussian sorting based on their distance from the camera. |
| SH Order | The spherical harmonics order used for rendering the gaussians, which determines the visual fidelity of the gaussians. The SH order equal to zero represents only the perspective-indepent base color, while higher orders encode more persective-dependent details, such as shininess, reflections, etc. The value ranges from 0 to 3, the default one is 0. |
| SH Compression | Compressing the spherical harmonics data to improve VRAM usage efficiency. Enabled by default. |
| Sort Interval | Frame interval between sorting gaussian splats. Higher values can be set for a relatively static camera to save performance. The minimum and the default value is 1, i.e. sorting on every frame. |
| Sort VR Per Eye | Enabling sorting for each eye in VR. If disabled, the Gaussian data will be sorted once and reused for the other eye. Disabled by default. |


### Gaussian Material Parameters


The `gaussian_render` material contains the following parameters available for adjustment:


![](gaussian_material_settings.png)


| Sh Only | Using only the spherical harmonics components with the order > 0, i.e. without the base color, to see how they affect the final color. Disabled by default. |
|---|---|
| Debug Cubes | Rendering primitive quads instead of guassians. Intended for debugging purposes. Disabled by default. |
| Mip Splatting Paper |  |
| Use 2D Mip Filter | Enables the experimental 2D mip filter. The filter compensates for the alpha falloff of Gaussians at distance and applies screen-space blur depending on their projected size. This helps reduce aliasing and shimmering compared to the standard constant Gaussian size. Enabled by default. |
| Mip Filter Scale | Controls the strength of the 2D mip filter. Lower values reduce the amount of blur applied to distant Gaussians, while higher values increase smoothing. This parameter can be used to fine-tune the visual sharpness. Available only when *[Use 2D Mip Filter](#use_2d_map_filter)* is enabled. The value ranges from 0.1 to 3.0, the default one is 1.0. |
| Use Adaptive 3D Filter | Enables an experimental 3D smoothing filter for Gaussians. The filter adapts Gaussian scaling based on camera parameters used during training. It helps preserve small details such as grass, wires, and thin structures when viewed up close. Disabled by default. |
| Training Minimum Depth | Specifies the minimum distance from the camera to Gaussians used during training. This value is required for the adaptive 3D filter to correctly scale Gaussians at close range. The value can be estimated from the dataset or adjusted manually for better visual results. Available only when *[Use Adaptive 3D Filter](#use_adaptive_3d_filter)* is enabled. The default value is 5.0. |
| Training Maximum Focal Length | Specifies the maximum camera focal length used during training. This parameter is used by the adaptive 3D filter to reconstruct the appropriate Gaussian scale relative to the original capture cameras. Available only when *[Use Adaptive 3D Filter](#use_adaptive_3d_filter)* is enabled. The value can be approximated if the exact training parameters are unknown: ```text focal = viewport_width / (2.0 * tan(fov_x / 2.0)) ``` The default value is 1663, which corresponds to a camera 1920 pixels wide with a horizontal field of view of 60 degrees. |
| Splat Adjustments |  |
| Culling Frustum Dilation | The scalar factor controlling how much the view frustum is expanded to include 3D Gaussians whose centers lie outside the original frustum but remain visible due to their large covariance. The value ranges from 0 to 1, the default one is 0.1. |
| Culling Alpha Threshold | The alpha threshold for culling gaussians. Gaussians with alpha lower than this value will not be drawn. The value ranges from 0 to 1, the default one is 0.004. |
| Splat Opacity Scale | The gaussian splat opacity (alpha) scale factor. Adjust this value to make the gaussians more/less opaque. The value ranges from 0.2 to 3.0, the default one is 1.0. |
| Splat Size Scale | The gaussian splat size scale. Adjust this value to make the gaussians larger/smaller. The value ranges from 0.2 to 3.0, the default one is 1.0. |
| Low Pass Filter Strength | Controls the strength of the low-pass filter applied to Gaussians. Increasing this value increases blur and reduces high-frequency detail. This parameter is available only when *[Use 2D Mip Filter](#use_2d_map_filter)* is disabled and provides a simpler way to smooth distant splats and reduce aliasing. The value ranges from 0 to 1, the default one is 0.3. |
| Color Adjustments |  |
| Tint Color | Applies a color tint to all splats. This parameter can be used to globally shift the color balance of the rendered Gaussians. White by default, i.e. the colors are left as they are. |
| Temperature | Adjusts the color temperature of splats, shifting colors toward warmer (yellow/orange) or cooler (blue) tones. The value ranges from -1 to 1, the default one is 0. |
| Saturation | Controls the color saturation of splats. Higher values increase color intensity, while lower values move colors toward grayscale. The value ranges from 0 to 2, the default one is 1. |
| Brightness | Adjusts the overall brightness of splats. The value ranges from -1 to 1, the default one is 0. |
| Black Point | Defines the black level of the splat colors. Increasing this value darkens shadows and increases contrast. The value ranges from 0 to 1, the default one is 0. |
| White Point | Defines the white level of the splat colors. Adjusting this value changes the intensity of highlights. The value ranges from 0 to 1, the default one is 1. |


### Generating Collision Geometry


3DGS data describes a cloud of gaussians and contains no surface geometry, therefore splats cannot be collided with, intersected, or used for shadow casting on their own. The *GaussianCollisionGenerator* property generates a polygonal proxy mesh for a 3DGS object: gaussians are rasterized into a voxel grid, the resulting volume is cleaned up and polygonized, and the mesh is added to the scene as a *gaussian_collision* child node containing one *Object Mesh Static* per tile.


To generate collision geometry for a 3DGS object, do the following:


1. Assign the ***GaussianCollisionGenerator*** property to the same *Node Dummy* that has the [*Gaussian* property](#prop_parameters) assigned.
2. Add one or more elements to the *Regions* array to specify which parts of the splat cloud are meshed and at what resolution. Each region is an oriented box that is either read from a *World Trigger* node or specified manually. ![](collision_generator_regions.png)
3. Adjust the generation parameters, if necessary.
4. Enable the *[Regenerate](#regenerate)* toggle to build the mesh. The toggle is switched off automatically as soon as generation is finished. ![](regenerate_toggle.png)


> **Notice:** If the *Regions* array is left empty, a single region covering the whole object is used instead, controlled by the *Global Voxel Size*, *Global Tile Size*, and *Ceiling Cut* parameters.


#### Generation Parameters


The *GaussianCollisionGenerator* property contains the following parameters available for adjustment:


##### Mode


| Mode | Specifies how the generated geometry is stored: - **Bake to Disk** � the generated `*.mesh` tiles are kept on disk and the mesh is saved into the world. Set by default. - **Runtime Only** � the mesh is rebuilt in memory on every start and nothing is stored. |
|---|---|


##### Regions


| Regions | An array of boxes defining what is meshed and at what resolution. Each element has the following fields: - **Trigger** � the *World Trigger* node marking the region. Available for the *Trigger* source. - **Source** � the way the box is defined: *Trigger* to read it from a *World Trigger* node, or *Manual* to specify the position, rotation, and size directly. - **Position** � the center of the box in world coordinates. Available for the *Manual* source. - **Rotation** � the rotation of the box (Euler angles, in degrees) in world coordinates. Available for the *Manual* source. - **Size** � the size of the box, in units. Available for the *Manual* source. - **Voxel Size** � the size of a single voxel inside this region. It defines the level of detail of the generated geometry. The minimum value is 0.01, the default one is 0.1. - **Tile Size** � the size of a chunk (in units) the region geometry is split into. Tiles are used for physics-distance culling. The minimum value is 0.1, the default one is 16. |
|---|---|
| Transition | The distance (in units) over which the resolution ramps between neighboring regions. The default value is 4. |
| Draw Regions | Enabling debug visualization of all region boxes in the viewport. Disabled by default. |
| Global Voxel Size | The voxel size of the automatically created region used when the *Regions* array is empty. The minimum value is 0.01, the default one is 0.1. |
| Global Tile Size | The tile size of the automatically created region used when the *Regions* array is empty. The minimum value is 0.1, the default one is 16. |
| Ceiling Cut | The number of units trimmed off the top of the automatically created region, which allows dropping roofs and the sky. The **0** value disables trimming and is set by default. Used only when the *Regions* array is empty. |


##### Settings


| Opacity Threshold | Gaussians that are more transparent than this value are ignored during generation. The value ranges from 0 to 1, the default one is 0.1. |
|---|---|
| Surface Threshold | The occupancy level in the [0;1] range at which the surface is placed. While the gaussians are rasterized, each voxel accumulates an occupancy value from all the kernels overlapping it; polygonization then treats the voxels with occupancy above this level as solid and the rest as empty, and builds the surface along the border between them. Lower values place the surface in the faint outer falloff of the gaussians, which produces bulkier geometry that captures weak structures along with more noise. Higher values make the surface hug only the dense cores of the gaussians, which gives tighter geometry but may thin out faint structures or leave holes in them. The minimum value is 0.01, the default one is 0.25. |
| Max Sigma (voxels) | The upper limit for the sigma (standard deviation) of a gaussian, measured in voxels. The sigma defines how far a gaussian spreads in space, and the sigma of every gaussian is clamped to this value before rasterization. As the limit is expressed in voxels, it scales together with the *Voxel Size* of the region. Clamping keeps oversized gaussians, such as huge background splats or strongly stretched ones, from smearing occupancy across a large volume and bounds the amount of work spent on a single gaussian. Lower values make big gaussians contribute locally, so the geometry follows small details, but large smooth surfaces assembled from big gaussians may break up into separate blobs. Higher values spread occupancy wider, which yields smoother yet coarser geometry and slows generation down. The minimum value is 0.5, the default one is 3. |
| Support Sigma | The number of sigmas the gaussian kernel is rasterized out to. The density of a gaussian never falls to zero, so the kernel has to be truncated somewhere: this value sets the truncation radius as a number of standard deviations from the center of the gaussian, and everything beyond it is ignored. Together with *[Max Sigma](#max_sigma)* it defines the maximum voxel neighborhood a single gaussian can affect. Higher values take more of the faint outer tail of the gaussians into account, which fills the gaps between neighboring gaussians more reliably and smooths the result, but the number of voxels each gaussian writes to grows roughly cubically, so generation becomes noticeably slower. Lower values are faster, however the falloff is cut off more abruptly, which may leave gaps in sparsely covered areas. The value ranges from 1 to 5, the default one is 2. |
| Max Splat Size | Splats larger than this size (in units) are skipped, which allows removing sky and background blobs. The **0** value disables the check and is set by default. |


##### Robustness


| Close Radius | The radius (in voxels) of the closing operation applied to the voxel volume before it is polygonized: the solid is first expanded by this number of voxels in all directions and then shrunk back by the same amount. Gaps and holes that are narrower than approximately twice this radius are closed up during the expansion and do not reopen when the volume is shrunk back, while the overall thickness of the geometry remains the same. Higher values seal larger holes, but also smooth out small details. The **0** value disables the operation. The default value is 1. |
|---|---|
| Denoise Min Cluster | The minimum size (in voxels) of a connected voxel cluster to be kept. After the gaussians are rasterized, the filled voxels are grouped into clusters of neighboring voxels, and every cluster that contains fewer voxels than this value is discarded before polygonization. This removes small isolated blobs produced by stray semi-transparent gaussians, which would otherwise become invisible obstacles floating in the air. Excessively high values may also discard small standalone objects that are meant to be collidable. The **0** value disables the check. The default value is 16. |
| Denoise Min Fraction | The minimum size of a connected voxel cluster to be kept, specified as a fraction of the largest cluster in the [0;1] range. For example, the **0.02** value keeps only the clusters that contain at least 2% of the voxels of the biggest one. Unlike the absolute *Denoise Min Cluster* threshold, this criterion scales automatically with the size of the object and the chosen *Voxel Size*, so noise keeps being filtered out consistently when the resolution is changed. The **0** value disables the check. The default value is 0.02. |
| Thicken | The number of voxels the solid is expanded by in all directions before the volume is polygonized. Unlike *[Close Radius](#close_radius)*, the volume is not shrunk back afterwards, so the resulting geometry becomes thicker than the original surface. Gaussian surfaces are often reconstructed as a shell only one voxel thick, which polygonizes into geometry that physical bodies and traced rays can slip through. Thickening such a shell makes it watertight. Keep the value as low as possible: the collision surface is offset outwards from the visible splats by roughly this number of voxels. The **0** value disables thickening. The default value is 1. |
| Fill Holes Max Edges | The maximum length of a hole boundary, in edges, for the hole to be sewn up. This operation is performed on the polygonal mesh rather than on the voxel volume: every open boundary loop (a chain of edges that belong to a single triangle each) consisting of no more than this number of edges is triangulated and closed. It cleans up the small openings that survive voxel filtering. The limit keeps large legitimate openings, such as doorways, windows, or the sides of the region box where the geometry is cut off, from being covered with a false surface. Higher values close bigger holes, but increase the risk of such artifacts. The **0** value disables sewing. The default value is 20. |
| Smooth Iterations | The number of Laplacian smoothing passes applied to the polygonal mesh. On each pass, every vertex is moved towards the average position of the vertices it is connected to by edges. Smoothing evens out the stair-step faceting that the mesh inherits from the voxel grid. Note that each pass also slightly shrinks the geometry and rounds sharp features off, so high values may round the corners of buildings and pull the collision surface away from the visible splats. The **0** value disables smoothing. The default value is 2. |


##### Output


| Collision | The generated mesh participates in physics, i.e. it can be walked on and collided with. Enabled by default. |
|---|---|
| Cast Shadows | The generated mesh casts and receives shadows. Enabled by default. |
| Visible | Rendering the generated mesh in the viewport. Disabled by default, so that the mesh serves as an invisible collision or shadow proxy - enable it to inspect the geometry that has been built. |
| Cache Dir | The folder (relative to the `data` folder) storing the generated `*.mesh` files. Used in the *Bake to Disk* mode only. The default value is `gaussian_collision_cache`. |
| Surface Material | The material assigned to the surfaces of the generated mesh. |
| Regenerate | Rebuilding the mesh with the current settings. The toggle is switched off automatically when generation is finished. |
