# Settings and Preferences


The *Settings* window provides quick access to general editor and run-time settings, including hotkeys and controls, general physics, sound, render and video settings.


To open the window, choose *Window -> Settings* in the main menu:


![](settings_open.png)


The following window will open:


![](settings_window.png)

*Settings Window*


## Saving and Loading Settings


Via the *Settings* window, you can save and load presets for general physics, sound and render settings. The presets are stored in files with the corresponding extensions: `*.physics, *.sound, *.render`.


> **Notice:** If there is no world currently loaded you'll only be able to save a new preset via the **Save As New** button.


By using this capability, you can prepare settings presets with low, medium, high and ultra settings for different devices.


To **save** the preset to a file:


1. Go to the section with the required setting (*Physics, Sound, Render*) and click **Save** (to save changes to the current preset file) or **Save As New** (to save settings to a new file) in the upper right corner of the window. ![](settings_save.png)
2. In the file dialog window that opens, specify a folder and a name for the preset file and click **OK**.


The file with the corresponding extension will be created in the target folder and will be available in the Asset Browser immediately.


To **load** the preset from a file and apply it:


1. Go to the section with the required setting (*Physics, Sound, Render*) and simply select the desired preset from the dropdown in the upper right corner of the window. ![](settings_load.png)


The settings from the corresponding file will be loaded and applied.


> **Notice:** You can load the **render settings** via the Asset Browser. Simply double-click the required `.render` file: the settings will be applied automatically.


By default, a UNIGINE project provides settings for *low, medium, high* and *ultra* quality presets stored in the `data/template_render_settings` folder.


To **revert** your changes made to the preset simply click **Revert** after making them.


![](settings_revert.png)


The previously saved settings will be loaded from the corresponding file and applied.


For your convenience there is also a **[From World]** option enabling you to use render, sound, and physics settings stored in a `*.world` file, that is currently loaded. If you change any settings when this option is selected, you can only save your changes to a new preset asset which will be automatically selected and applied.


![](from_world.png)


You can also assign a saved preset to a world as follows: select the world in the Asset Browser and drag and drop the corresponding preset.


![Assigning presets](assign_preset.gif)


## Articles in This Section

- [Editor Settings and Hotkeys](../../editor2/settings/hotkeys/index.md)

- [World Settings](../../editor2/settings/world/index.md)

- [Render Settings](../../editor2/settings/render_settings/index.md)

  - [Screen](../../editor2/settings/render_settings/screen/index.md)
  - [Upscalers](../../editor2/settings/render_settings/upscalers/index.md)
  - [Visibility Distances](../../editor2/settings/render_settings/visibility_distances/index.md)
  - [Textures](../../editor2/settings/render_settings/textures/index.md)
  - [Lights](../../editor2/settings/render_settings/lights/index.md)
  - [Transparent](../../editor2/settings/render_settings/transparent/index.md)
  - [Shadows](../../editor2/settings/render_settings/shadows/index.md)
  - [Tessellation](../../editor2/settings/render_settings/tessellation/index.md)
  - [Global Illumination Settings](../../editor2/settings/render_settings/global_illumination/index.md)

    - [Indirect Diffuse](../../editor2/settings/render_settings/global_illumination/indirect_diffuse/index.md)

      - [SSAO](../../editor2/settings/render_settings/global_illumination/indirect_diffuse/ssao/index.md)
      - [SSGI](../../editor2/settings/render_settings/global_illumination/indirect_diffuse/ssgi/index.md)
      - [Bent Normal](../../editor2/settings/render_settings/global_illumination/indirect_diffuse/bent_normal/index.md)
    - [Indirect Specular](../../editor2/settings/render_settings/ssr/index.md)
    - [Denoise](../../editor2/settings/render_settings/global_illumination/denoise/index.md)
  - [Subsurface Scattering](../../editor2/settings/render_settings/sss/index.md)
  - [Dynamic Reflections](../../editor2/settings/render_settings/dynamic_reflections/index.md)
  - [Decals](../../editor2/settings/render_settings/decals/index.md)
  - [SSBevel](../../editor2/settings/render_settings/ssbevel/index.md)
  - [SSDirt](../../editor2/settings/render_settings/ssdirt/index.md)
  - [Landscape](../../editor2/settings/render_settings/landscape/index.md)
  - [Terrain](../../editor2/settings/render_settings/terrain/index.md)
  - [Water](../../editor2/settings/render_settings/water_ssr/index.md)
  - [Clouds](../../editor2/settings/render_settings/clouds/index.md)
  - [Vegetation](../../editor2/settings/render_settings/vegetation/index.md)
  - [Environment](../../editor2/settings/render_settings/environment/index.md)
  - [Occlusion Culling](../../editor2/settings/render_settings/occlusion_culling/index.md)
  - [Camera Effects](../../editor2/settings/render_settings/camera_effects/index.md)
  - [Color Correction](../../editor2/settings/render_settings/color/index.md)
  - [Buffers](../../editor2/settings/render_settings/buffers/index.md)
  - [Streaming](../../editor2/settings/render_settings/streaming/index.md)
  - [Materials Quality](../../editor2/settings/render_settings/materials_quality/index.md)
  - [Shading Quality](../../editor2/settings/render_settings/shading_quality/index.md)
  - [Custom Post Materials](../../editor2/settings/render_settings/custom_post/index.md)
  - [Custom Parameters](../../editor2/settings/render_settings/custom_parameters/index.md)
  - [Debug Materials](../../editor2/settings/render_settings/debug/index.md)
  - [Custom Composite Materials](../../editor2/settings/render_settings/custom_composite/index.md)
  - [Wireframe Color](../../editor2/settings/render_settings/wireframe_color/index.md)

- [Global Physics Settings](../../editor2/settings/physics_global/index.md)

- [Global Sound Settings](../../editor2/settings/sound_global/index.md)

- [Navigation Settings (Experimental)](../../editor2/settings/navigation/index.md)

- [Controls Settings](../../editor2/settings/controls/index.md)
