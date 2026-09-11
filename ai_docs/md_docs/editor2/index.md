# UnigineEditor


**UnigineEditor** provides the core functionality for creation and editing of virtual worlds for UNIGINE-based applications based on the [assets workflow](../editor2/assets_workflow/index.md). It allows you to easily view and modify virtual worlds by adding, transforming and editing the [nodes](../start/index.md#node).


In addition, UnigineEditor also provides:


- Customizable UI layout with dockable panels
- Integration with the [Asset Browser](../editor2/assets_workflow/index.md#asset_browser)


## Editor Running


> **Notice:** You should keep UNIGINE SDK Browser [launched](../sdk/licenses/index.md) to use UnigineEditor.


To launch UnigineEditor for your project, click *Open Editor* in the SDK Browser:


![](../sdk/projects/run_editor.png)


## Articles in This Section

- [Interface Overview](../editor2/interface/index.md)

  - [Layout Customization](../editor2/interface/customize/index.md)
  - [Context Menus](../editor2/interface/context/index.md)

- [Assets Workflow](../editor2/assets_workflow/index.md)

  - [Asset Types](../editor2/assets_workflow/asset_types.md)
  - [Assets and Runtime Files](../editor2/assets_workflow/assets_runtimes.md)

    - [Runtime Files in Detail](../editor2/assets_workflow/runtimes_in_depth.md)
  - [Creating and Importing Assets](../editor2/assets_workflow/assets_create_import.md)

    - [FBX Import Guide](../editor2/fbx/index.md)
    - [CAD Import Guide](../editor2/cad/index.md)
    - [Texture Import Guide](../editor2/assets_workflow/texture_import.md)
    - [Exporting 3D Models From Blender](../editor2/assets_workflow/export/export_from_blender.md)
    - [Exporting 3D Models From Autodesk Maya](../editor2/assets_workflow/export/export_from_maya.md)
    - [Exporting 3D Models From Autodesk 3ds Max](../editor2/assets_workflow/export/export_from_3dsmax.md)
    - [Exporting 3D Models From Maxon Cinema 4D](../editor2/assets_workflow/export/export_from_cinema4d.md)
    - [Exporting Animated Models From Blender](../editor2/assets_workflow/export/export_animations_from_blender.md)
    - [Exporting Animated Models From Autodesk Maya](../editor2/assets_workflow/export/export_animations_from_maya.md)
    - [Exporting Animated Models From Autodesk 3ds Max](../editor2/assets_workflow/export/export_animations_from_3dsmax.md)
    - [Exporting Animated Models From Character Creator](../editor2/assets_workflow/export/export_animations_from_character_creator.md)
    - [Exporting Animated Models From Mixamo](../editor2/assets_workflow/export/export_animations_from_mixamo.md)
  - [Organizing Assets](../editor2/assets_workflow/assets_organize.md)
  - [Copying Assets From Other Projects](../editor2/assets_workflow/assets_migration.md)
  - [Optimizing Assets](../editor2/assets_optimize/index.md)

    - [Content Profiler](../editor2/assets_optimize/content_profiler/index.md)

      - [Profiling Textures](../editor2/assets_optimize/content_profiler/texture_profiler.md)
      - [Profiling Surfaces](../editor2/assets_optimize/content_profiler/surface_profiler.md)
    - [Cleaner](../editor2/cleaner/index.md)
    - [Connections Between Assets](../editor2/assets_optimize/asset_connections.md)
    - [Detecting Unique Assets](../editor2/assets_optimize/unique_assets.md)
  - [Upgrading Assets](../editor2/assets_upgrade/index.md)
  - [Project Files](../editor2/assets_workflow/project_files.md)

- [Version Control](../editor2/assets_workflow/version_control/index.md)

  - [VCSIntegration Plugin](../editor2/assets_workflow/version_control/vcs_plugin/index.md)

    - [Git](../editor2/assets_workflow/version_control/vcs_plugin/git.md)
    - [Subversion](../editor2/assets_workflow/version_control/vcs_plugin/svn.md)

- [Built-In Search](../editor2/search/index.md)

- [Managing Packages](../editor2/managing_packages/index.md)

- [Settings and Preferences](../editor2/settings/index.md)

  - [Editor Settings and Hotkeys](../editor2/settings/hotkeys/index.md)
  - [World Settings](../editor2/settings/world/index.md)
  - [Render Settings](../editor2/settings/render_settings/index.md)

    - [Screen](../editor2/settings/render_settings/screen/index.md)
    - [Upscalers](../editor2/settings/render_settings/upscalers/index.md)
    - [Visibility Distances](../editor2/settings/render_settings/visibility_distances/index.md)
    - [Textures](../editor2/settings/render_settings/textures/index.md)
    - [Lights](../editor2/settings/render_settings/lights/index.md)
    - [Transparent](../editor2/settings/render_settings/transparent/index.md)
    - [Shadows](../editor2/settings/render_settings/shadows/index.md)
    - [Tessellation](../editor2/settings/render_settings/tessellation/index.md)
    - [Global Illumination Settings](../editor2/settings/render_settings/global_illumination/index.md)

      - [Indirect Diffuse](../editor2/settings/render_settings/global_illumination/indirect_diffuse/index.md)

        - [SSAO](../editor2/settings/render_settings/global_illumination/indirect_diffuse/ssao/index.md)
        - [SSGI](../editor2/settings/render_settings/global_illumination/indirect_diffuse/ssgi/index.md)
        - [Bent Normal](../editor2/settings/render_settings/global_illumination/indirect_diffuse/bent_normal/index.md)
      - [Indirect Specular](../editor2/settings/render_settings/ssr/index.md)
      - [Denoise](../editor2/settings/render_settings/global_illumination/denoise/index.md)
    - [Subsurface Scattering](../editor2/settings/render_settings/sss/index.md)
    - [Dynamic Reflections](../editor2/settings/render_settings/dynamic_reflections/index.md)
    - [Decals](../editor2/settings/render_settings/decals/index.md)
    - [SSBevel](../editor2/settings/render_settings/ssbevel/index.md)
    - [SSDirt](../editor2/settings/render_settings/ssdirt/index.md)
    - [Landscape](../editor2/settings/render_settings/landscape/index.md)
    - [Terrain](../editor2/settings/render_settings/terrain/index.md)
    - [Water](../editor2/settings/render_settings/water_ssr/index.md)
    - [Clouds](../editor2/settings/render_settings/clouds/index.md)
    - [Vegetation](../editor2/settings/render_settings/vegetation/index.md)
    - [Environment](../editor2/settings/render_settings/environment/index.md)
    - [Occlusion Culling](../editor2/settings/render_settings/occlusion_culling/index.md)
    - [Camera Effects](../editor2/settings/render_settings/camera_effects/index.md)
    - [Color Correction](../editor2/settings/render_settings/color/index.md)
    - [Buffers](../editor2/settings/render_settings/buffers/index.md)
    - [Streaming](../editor2/settings/render_settings/streaming/index.md)
    - [Materials Quality](../editor2/settings/render_settings/materials_quality/index.md)
    - [Shading Quality](../editor2/settings/render_settings/shading_quality/index.md)
    - [Custom Post Materials](../editor2/settings/render_settings/custom_post/index.md)
    - [Custom Parameters](../editor2/settings/render_settings/custom_parameters/index.md)
    - [Debug Materials](../editor2/settings/render_settings/debug/index.md)
    - [Custom Composite Materials](../editor2/settings/render_settings/custom_composite/index.md)
    - [Wireframe Color](../editor2/settings/render_settings/wireframe_color/index.md)
  - [Global Physics Settings](../editor2/settings/physics_global/index.md)
  - [Global Sound Settings](../editor2/settings/sound_global/index.md)
  - [Navigation Settings (Experimental)](../editor2/settings/navigation/index.md)
  - [Controls Settings](../editor2/settings/controls/index.md)

- [Working With Projects (CS)](../editor2/projects/index_cs.md)

- [Working With Projects (CPP)](../editor2/projects/index_cpp.md)

- [Managing Worlds](../editor2/worlds/index.md)

- [Scene Navigation](../editor2/navigation/index.md)

- [Creating Nodes](../editor2/create_import_nodes/index.md)

- [Selecting and Positioning Nodes](../editor2/select_position_nodes/index.md)

- [Organizing Nodes](../editor2/organizing_nodes/index.md)

- [Node Dependencies](../editor2/organizing_nodes/node_dependencies.md)

- [Exporting Nodes](../editor2/exporting_nodes/index.md)

- [Instancing Nodes](../editor2/instancing_nodes/index.md)

- [Adjusting Node Parameters](../editor2/node_parameters/index.md)

  - [Transformation and Common Parameters](../editor2/node_parameters/transformation_common/index.md)
  - [Visual Representation](../editor2/node_parameters/visual_representation/index.md)
  - [Properties](../editor2/node_parameters/properties/index.md)
  - [Physics and Sound](../editor2/node_parameters/physics/index.md)
  - [Geo Coordinates](../editor2/node_parameters/geo/index.md)

- [Setting Up Materials](../editor2/materials_settings/index.md)

  - [Organizing Materials](../editor2/materials_settings/organizing_materials/index.md)

- [Pre-Compiling Shaders](../editor2/shaders_precompile/index.md)

- [Setting Up Properties](../editor2/properties_settings/index.md)

  - [Organizing Properties](../editor2/properties_settings/organizing_properties/index.md)

- [Lighting](../editor2/lighting/index.md)

  - [Environment](../editor2/lighting/environment.md)
  - [Light Sources](../editor2/lighting/lights/index.md)

    - [Shadows](../editor2/lighting/lights/shadows.md)
  - [Global Illumination](../editor2/lighting/gi/index.md)

    - [Bake Lighting Window](../editor2/lighting/gi/bake_lighting/index.md)
    - [Lightmapping](../editor2/lighting/gi/lightmaps.md)
    - [Voxel-Based GI](../editor2/lighting/gi/voxel_probes.md)
    - [Environment Probes](../editor2/lighting/gi/env_probes.md)
  - [Light Meter](../editor2/lighting/light_meter.md)
  - [Reflections](../editor2/lighting/reflections.md)

- [Baking Navigation Meshes](../editor2/navigation_baking/index.md)

- [Setting Up Cameras](../editor2/camera_settings/index.md)

- [Using Visual Debugging](../editor2/rendering_debug/index.md)

- [Using Visual Helpers](../editor2/using_visual_helpers/index.md)

- [Editing Curves](../editor2/curve_editor/index.md)

- [Sandworm](../editor2/sandworm/index.md)

  - [Interface Overview](../editor2/sandworm/interface/index.md)
  - [Starting with Sandworm](../editor2/sandworm/workflow/index.md)

    - [Creating Landscape](../editor2/sandworm/workflow/landscape/index.md)
    - [Adding a Mask](../editor2/sandworm/workflow/mask/index.md)
    - [Adding Vegetation](../editor2/sandworm/workflow/vegetation/index.md)
    - [Adding Roads](../editor2/sandworm/workflow/roads/index.md)
    - [Adding Point Objects](../editor2/sandworm/workflow/points/index.md)
    - [Adding Pipelines, Fences, Powerlines](../editor2/sandworm/workflow/lines/index.md)
    - [Adding Buildings](../editor2/sandworm/workflow/buildings/index.md)
    - [Generating the Terrain and Objects](../editor2/sandworm/workflow/generate/index.md)
  - [Sources and Their Parameters](../editor2/sandworm/sources/index.md)

    - [Elevation and Imagery](../editor2/sandworm/sources/elevation_imagery/index.md)
    - [Mask Parameters](../editor2/sandworm/sources/mask/index.md)
    - [Buildings Customization and Parameters](../editor2/sandworm/sources/buildings/index.md)
    - [Vegetation Parameters](../editor2/sandworm/sources/vegetation/index.md)
    - [Point Object Parameters](../editor2/sandworm/sources/points/index.md)
    - [Spline Object Parameters](../editor2/sandworm/sources/splines/index.md)
    - [River Object Parameters](../editor2/sandworm/sources/rivers/index.md)
    - [Roads](../editor2/sandworm/sources/roads/index.md)
  - [Generation Settings](../editor2/sandworm/generation/index.md)

    - [Export Area](../editor2/sandworm/generation/export_area/index.md)
    - [Data Types](../editor2/sandworm/generation/data_types/index.md)
    - [Projection](../editor2/sandworm/generation/projection/index.md)
    - [Quality](../editor2/sandworm/generation/quality/index.md)
    - [NoData](../editor2/sandworm/generation/nodata/index.md)
    - [Distributed Generation and Headless Mode](../editor2/sandworm/generation/distributed_computing/index.md)
    - [Output Directories and Files](../editor2/sandworm/generation/output_dir_files/index.md)
  - [Questions and Answers](../editor2/sandworm/faq/index.md)

- [Using Editor Tools for Specific Tasks](../editor2/tools/index.md)

  - [Keyframe Animation and Cutscenes with Sequencer](../editor2/tools/sequencer/index.md)

    - [Sequencer Editor](../editor2/tools/sequencer/editor/index.md)
    - [Sequence Channels](../editor2/tools/sequencer/channels/index.md)

      - [Targets and Bindings](../editor2/tools/sequencer/targets/index.md)
      - [Keys and Curves](../editor2/tools/sequencer/keys/index.md)
      - [Clips](../editor2/tools/sequencer/clips/index.md)
    - [Channel Reference](../editor2/tools/sequencer/channel_reference/index.md)

      - [Cinematic Channels](../editor2/tools/sequencer/channel_reference/cinematic/index.md)

        - [Camera Cuts](../editor2/tools/sequencer/channel_reference/camera_cuts/index.md)
        - [Skeletal Animation](../editor2/tools/sequencer/channel_reference/skeletal_animation/index.md)
        - [Sound Channel](../editor2/tools/sequencer/channel_reference/sound/index.md)
        - [Music Channel](../editor2/tools/sequencer/channel_reference/music/index.md)
        - [Sub-Sequence](../editor2/tools/sequencer/channel_reference/sub_sequence/index.md)
        - [Follow Path](../editor2/tools/sequencer/channel_reference/follow_path/index.md)
        - [Events Channel (CS)](../editor2/tools/sequencer/channel_reference/events/index_cs.md)
        - [Events Channel (CPP)](../editor2/tools/sequencer/channel_reference/events/index_cpp.md)
        - [Material Channel](../editor2/tools/sequencer/channel_reference/material/index.md)
        - [Component Channel](../editor2/tools/sequencer/channel_reference/component/index.md)
        - [Console Command Channel](../editor2/tools/sequencer/channel_reference/console/index.md)
      - [Specific Engine Channels](../editor2/tools/sequencer/channel_reference/engine/index.md)

        - [Property](../editor2/tools/sequencer/channel_reference/property/index.md)
        - [Render Parameters](../editor2/tools/sequencer/channel_reference/render_parameters/index.md)
        - [Animation Graph Parameters](../editor2/tools/sequencer/channel_reference/anim_graph_parameters/index.md)
    - [Runtime Playback (CS)](../editor2/tools/sequencer/runtime/index_cs.md)
    - [Runtime Playback (CPP)](../editor2/tools/sequencer/runtime/index_cpp.md)
    - [Converting Legacy Tracks](../editor2/tools/sequencer/track_import/index.md)
  - [Capturing Screenshots and Frame Sequences](../editor2/tools/video_grabber/index.md)
  - [Adding Variations for a More Realistic Environment](../editor2/tools/randomizer/index.md)
  - [Generating Impostors with Impostors Creator](../editor2/tools/impostors_creator/index.md)

    - [impostor_material](../editor2/tools/impostors_creator/impostor_material.md)
  - [Converting Landscape Terrain to Geometry with Landscape Exporter](../editor2/landscape_export/index.md)
  - [Editing Global Terrain](../editor2/terrain_editor/index.md)
  - [Editing Landscape Terrain](../editor2/brush_editor/index.md)
  - [Batch Rename](../editor2/tools/batch_rename/index.md)
  - [Mask Editor for Grass and Clutters](../editor2/mask_editor/index.md)
  - [Cluster Editor](../editor2/cluster_editor/index.md)
  - [Texture Editor](../editor2/texture_editor/index.md)

    - [Brush Tool](../editor2/texture_editor/brush_tool/index.md)
    - [Pencil Tool](../editor2/texture_editor/pencil_tool/index.md)
    - [Eraser Tool](../editor2/texture_editor/eraser_tool/index.md)
    - [Smooth Tool](../editor2/texture_editor/smooth_tool/index.md)
    - [Smudge Tool](../editor2/texture_editor/smudge_tool/index.md)
    - [Contrast Tool](../editor2/texture_editor/contrast_tool/index.md)
    - [Brightness Tool](../editor2/texture_editor/brightness_tool/index.md)
    - [Saturation Tool](../editor2/texture_editor/saturation_tool/index.md)
    - [Replace Color Tool](../editor2/texture_editor/replace_color_tool/index.md)
    - [Invert Tool](../editor2/texture_editor/invert_tool/index.md)
    - [Flow Map Tool](../editor2/texture_editor/flowmap_tool/index.md)
    - [Draw Mesh Data Tool](../editor2/texture_editor/mesh_data_tool/index.md)
    - [Ambient Occlusion Tool](../editor2/texture_editor/ambient_occlusion_tool/index.md)
    - [Curvature Tool](../editor2/texture_editor/curvature_tool/index.md)
    - [Leaks Tool](../editor2/texture_editor/leaks_tool/index.md)
    - [Color Picker Tool](../editor2/texture_editor/color_picker_tool/index.md)
  - [Tracker: Legacy Animation Tool](../editor2/tools/tracker/index.md)

    - [Basic Operations in Tracker](../editor2/tools/tracker/basics/index.md)
    - [Creating Type-Specific Tracks](../editor2/tools/tracker/parameters/index.md)
    - [Usage Example](../editor2/tools/tracker/usage/index.md)
    - [Running Tracks in Application](../editor2/tools/tracker/run/index.md)

- [Extending Editor Functionality](../editor2/extensions/index.md)

  - [Setting Up Environment](../editor2/extensions/environment.md)
  - [Creating Your First Editor Plugin](../editor2/extensions/custom_plugin.md)
  - [Managing Assets in Editor Plugins](../editor2/extensions/manage_assets.md)

- [UnigineEditor API](../api/editor/index.html.md)

- [ImGuiSamples Plugin](../editor2/imgui_samples_plugin/index.md)
