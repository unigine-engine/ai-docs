# Content Migration


You can upgrade content of your project to UNIGINE 2.21 in the automatic or manual mode.


> **Warning:** You **cannot** correctly migrate the project that contains assets with a version higher than the project version.


If your project contains at least one file with a higher version, upgrade to this version will be skipped, as the migration script would consider that the project is already upgraded to that version. Let's review an example case:


- Your project is v. 2.14.1
- It contains a v. 2.15 node.
- You plan to upgrade the project to 2.16.


When you start the upgrade process, the following will happen:


- Upgrading to v. 2.15 is skipped as you have one v. 2.15 node, and the script assumes the whole project is already using this version.
- Upgrading to v. 2.15.1 is successful.
- Upgrading to v. 2.16 is successful.


Thus, for a correct migration, follow this recommendation: **ensure that the project does not contain assets with a version higher than the project version**. This can be done by checking the number of the target version througout all project files. In the example above, you should check if any of your project files contains the text `version="2.15"` before starting the migration process.


Another way is to keep the ***Make Backup*** option enabled. In this case the project is automatically copied for reference, and if automatic migration goes wrong (i.e. it is stopped halfway and you see a message like *"Skip migration to version "2.15" File: "D:/ProjectFolder/data/.../example_file.node* in the migration log) you can fix the problem files manually.


![Make Backup](make_backup.png)


> **Notice:** You can delete the backup folder manually after you've migrated successfully.


## Automatic Upgrade


Automatic upgrade of the project's content can be performed via [UNIGINE SDK Browser](../../sdk/projects/index_cpp.md#upgrade_project).

> **Notice:** By default, the automatic mode is used to upgrade only binary executable files and content stored in the project's `/data` folder. If you have content stored outside the `/data` folder or in the additional `/data` folders, you will have to upgrade it [manually](#manual_upgrade).


As a result, the binary executable and configuration files, meshes, terrains, worlds, nodes, splines, materials, properties, tracks, settings files will be upgraded to new formats (if any). The `<unigine_project>/migration.log.html` log file will be opened in the web browser. However, you can uncheck **Migrate Content** during automatic upgrading and perform content upgrading manually. In this case, only binary executable files will be upgraded.


> **Notice:** The migration results depend on the version of UNIGINE SDK, from which you are going to migrate.


## Manual Upgrade


> **Warning:** This mode should be used to upgrade content stored outside the project's `/data` folder (such as **[mount points](../../principles/filesystem/index_cpp.md#mount_points)**).


To upgrade the project's content in the manual mode, do the following:


1. Put the binary executable `<UnigineSDK>/bin/usc_x64.exe` to the `<UnigineSDK>/utils/upgrade` folder that contains the upgrade script. > **Notice:** Use `usc_x64.exe` from the SDK version you are migrating **to**.
2. In the command prompt, [run](../../tools/usc/index.md#run) the `upgrade.usc` with the required options: ```bash usc_x64.exe upgrade.usc path/to/additional_content_1 path/to/additional_content_2 ... ``` If you have unchecked **Migrate Content** during [automatic upgrading](#automatic_upgrade), add the path to the project's `data` folder to the list of arguments passed to the upgrade script. For example: ```bash usc_x64.exe upgrade.usc <unigine_project>/data path/to/additional_content_1 path/to/additional_content_2 ... ``` Here:

  - `path/to/additional_content_*` - paths to folders with content stored outside the `/data` folder.


As a result, you will get your meshes, terrains, worlds, nodes, splines, materials, properties, tracks, configuration and settings files upgraded.


> **Notice:** The migration results depend on the version of UNIGINE SDK, from which you are going to migrate.


As soon as migration is completed, run the Editor to have the project assets "indexed".


## Material Mask Renamed to Surface ID


The material state that enables writing the per-surface identifier has been renamed: the surface identifier and the [custom parameters](../../content/materials/custom_parameters/index.md) stored under it are now called **Surface ID** instead of **Material Mask**. The state keeps its previous behavior and still drives the classic [material mask](../../principles/bit_masking/index.md#material_mask) � only the names have changed:


| File | Was | Now |
|---|---|---|
| Materials (`*.mat`) inherited from *mesh_base* and *particles_base* | transparent_material_mask | transparent_surface_id (*Surface ID*) |
| Graph-based materials (`*.mgraph`) and subgraphs (`*.msubgraph`) | material_mask_write | surface_id_write (*Write Surface ID*) |


Both renames are performed by [automatic upgrade](#automatic_upgrade): materials, material graphs and subgraphs stored in the project's `/data` folder are updated for you, and the values of the states are preserved.


> **Notice:** Content stored outside the `/data` folder (mount points, for example) is not covered by the automatic mode � upgrade it [manually](#manual_upgrade), as usual.


What automatic upgrade cannot do for you:


- Custom base materials (`*.basemat`) that declare a state of their own with the old name, and the shaders that read it: rename the state and the corresponding define by hand.
- Application code, scripts and configuration files that refer to the state by name.


> **Warning:** Writing the Surface ID is off by default for alpha-blend materials, particles and decals, because it costs performance. A material graph created anew comes out with **Write Surface ID** enabled for mesh materials and disabled for decal ones. Check the state on the materials that a Surface ID consumer depends on � a segmentation view or a picking shader gets nothing from a surface whose material writes no ID.


## Lights Migration


The shadow pipeline has been reworked for better quality, stability, and consistency across *World*, *Omni*, and *Proj* lights. Shadow penumbra is now calculated using **PCSS** (Percentage-Closer Soft Shadows): the width of the penumbra is estimated by searching for the occluders that cast the shadow, which keeps contact shadows sharp and softens the shadow the farther it stretches away.


Whether this requires anything from you depends on how the project used penumbra:


- **Penumbra was not used** - [Penumbra Mode](../../editor2/settings/render_settings/shadows/index.md#penumbra_mode) is set to *Disabled* for the project. Such shadows require no reconfiguration, they will look better by default. Additionally try changing the [number of cascades](../../objects/lights/world/index.md#number_of_cascades) of a *World* light: their maximum has been raised to 16, and a new cascade placement mode has been added.
- **Penumbra was used and tuned**. [Automatic upgrade](#automatic_upgrade) overwrites the [Penumbra](../../objects/lights/parameters/index.md#penumbra) value of every *World*, *Omni*, and *Proj* light: 5.0 is written for *World* lights and 2.0 for *Omni* and *Proj* lights. These are the values the first version of PCSS was tuned for, and they are well above the current default of 0.5, so migrated shadows are likely to come out too soft � reduce the value for the lights where that happens. > **Warning:** PCSS penumbra is more expensive than the previous algorithm. However, the same softness is now reached with lower values. For fine-tuning, start with the [Penumbra](../../objects/lights/parameters/index.md#penumbra) value of the light itself, then adjust [World Light Blocker Search Radius](../../editor2/settings/render_settings/shadows/index.md#world_blocker_search_radius) and [Omni/Proj Light Blocker Search Radius](../../editor2/settings/render_settings/shadows/index.md#omni_proj_blocker_search_radius), which may give better penumbra for finer object shadows.
