# Gaussian Splatting


The ***Gaussian Splatting*** demo showcases the usage of the [GaussianSplatting Plugin](../../code/plugins/gaussian/index.md) for rendering of Gaussian splat captures and **automatic collider generation** for them, turning a photorealistic scan into a walkable and interactive environment.


A splat capture is a purely visual asset: a cloud of semi-transparent kernels with no surfaces and no topology, so you cannot walk on it, throw a ball at it, or place an object on it. The [collision geometry generator](../../code/plugins/gaussian/index.md#collision_generator) closes this gap - a collision shell is reconstructed directly from the splat cloud and attached to the splat node as invisible static geometry, so physics, character controllers, ray casts, and any other collision-based systems work with splat-based content out of the box.


Along with two pre-baked scenes, the demo includes a runtime workflow: load an arbitrary **.ply* capture and generate collision for it on the fly. It serves as a practical reference for integrating Gaussian Splats into games, simulations, digital twins, and VR experiences.


The splat captures shipped with the demo are courtesy of **[Splatica](https://app.splatica.com/)**.


## Scenes


The following scenes are available with the demo:


- *Eagle Statue* - a compact object-centric capture (~8.4 million splats): a coarse global region combined with a high-resolution one driven by a [World Trigger](../../objects/worlds/world_trigger/index.md) node, so colliders follow fine sculpted detail
- *Dalyan* - a large outdoor capture of Dalyan, Turkey (~7.2 million splats) demonstrating region-based generation on a big scene: a coarse base region plus a narrow high-resolution one for a detailed walkway
- *Runtime Generation* - load any Gaussian splat **.ply* file and build collision for it in memory, with no pre-baked cache.


## Features


- Direct rendering of Gaussian splat **.ply* captures - no conversion to meshes or point clouds required
- Spherical harmonics up to order 3 with optional compression, configurable depth-sorting interval, and per-eye sorting for VR
- Automatic reconstruction of a watertight triangle collision surface from splat occupancy
- Colliders emitted as tiled static meshes, invisible and physics-only, with distance-based culling of tiles
- Two output modes: *Bake to Disk* stores the meshes in a per-scene cache for instant loading, *Runtime Only* rebuilds them in memory; one-click regeneration after any parameter change
- Oriented box regions setting voxel resolution per area - fine detail where the user interacts, coarse geometry elsewhere - with a smooth transition between neighboring regions and an automatic region covering the whole capture when none are defined
- Clean-up controls for real-world scan data: opacity and surface thresholds, filtering of sky and background blobs, denoising, thickening of thin walls, hole filling, and smoothing
- Three players switchable at runtime: a physical character controller, a spectator respecting the generated collision, and a free-flight spectator ignoring it
- A projectile launcher spawning rigid-body spheres that bounce off the reconstructed surfaces
- Debug visualization: collision wireframe drawn over the splats and generation region boxes drawn in the viewport
- Runtime UI for loading a **.ply* file and tuning voxel density, bounds, and thickness before generating collision
- Since the output is ordinary static geometry, ray casts, navigation, triggers, and vehicles work with no splat-specific code


## System Requirements


To run this demo, the following is required:


- Video memory: **minimum** 8 GB
- System memory: **minimum** 16 GB, 32 GB recommended - splat captures are loaded in full, and a single file reaches 3.2 GB
- Disk space: 21 GB
- Graphics API: Vulkan or DirectX 12


Note that the multi-million splat captures require a high-end GPU.


## Limitations


Keep the following in mind when using your own captures:


- Voxel resolution is a direct trade-off: halving the voxel size multiplies both generation time and output mesh size. This is exactly what regions are for - spend resolution only where the user actually interacts
- Thin, transparent, and wiry structures (glass, railings, cables, foliage) voxelize poorly: thickening makes them watertight at the price of geometry slightly thicker than the visual splats, and dense foliage becomes a solid blob rather than passable vegetation
- Sky, background, and floating capture artifacts have to be filtered out explicitly; otherwise they produce stray colliders in mid-air
- Reconstruction is approximate by design: around fine detail the collision surface is an offset shell rather than an exact match to the splats
- The result is static geometry with no semantics: it is not destructible, has to be regenerated when the capture or the region setup changes, and per-surface physical properties (friction, footstep sounds) have to be authored on top of it
- Splats are rendered as a sorted semi-transparent pass and do not participate in the deferred pipeline the way opaque meshes do; sorting is amortized over several frames, which may cause transient popping during fast camera motion
- Memory consumption scales with the splat count and the spherical harmonics order - reducing the SH order or enabling compression is the primary lever for large captures
- The demo runs in desktop mode only and is a reference for the workflow rather than a game: it contains no gameplay logic and does not include a pipeline for producing new splat captures


**SDK Path:***<SAMPLES_PROJECT_PATH>/demos\gaussian_splat_2.21*
## Accessing Demo Source Code

You can study and modify the source code of this demo to create your own projects. To access the source code do the following:

1. Find the **Gaussian Splatting** demo in the *Demos* section and click **[Install](/sdk/#samples)** (if you haven't installed it yet).
2. After successful installation the demo will appear in the *Installed* section, and you can click **Copy as Project** to create a project based on this demo. ![](../../sdk/demos/copy_as_project_gen.png)
3. In the **Create New Project** window, that opens, enter the name for your new project in the corresponding field and click **Create New Project**. ![](../../sdk/projects/create_project_cpp.png)
4. Now you can click **Open Code IDE** to check and modify source code in your default IDE, or click **Open Editor** to open the project in the [UnigineEditor](/editor2/). ![](../../sdk/projects/edit_code.png)
