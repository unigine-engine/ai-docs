# Configuration Files (CPP)


All global engine-related and project-related settings are grouped and stored in separate configuration files. Each configuration file is an XML file that stores settings of a certain type. The set of configuration files is as follows:


- *`*.boot`* - this is the main [boot configuration file](#boot).
- *`*.config`* - this file stores all [custom application settings](#config).
- *`*.controls`* - this file stores [controls configuration](#controls).
- *`*.global`* - this file stores [global project settings](#global), such as custom render, surface, and material parameters.
- *`*.user`* - this file stores [various personal settings](#user), such as helpers (wireframe, profiler, etc.).


> **Notice:** The extension of each configuration file doesn't matter, however, it is recommended to use these extensions for consistency.


The settings from these files are read by the Engine on the application start-up and used for engine initialization.


By default, the set of default configuration files is created automatically on [project creation](../sdk/projects/index_cpp.md#creation) in the project's `data/configs` folder available as a separate `configs` section of the Asset Browser.


![](config_files.png)

*Configuration files in theAsset Browser*


The `*.boot` configuration file stores the information about location of other configuration files for convenience. The path to the boot configuration file is set by using the *[-boot_config](../code/command_line.md#boot_config)* command-line option on the application start-up.


The paths to the configuration files can be both absolute or relative. An absolute path is always used as is. If a relative path is specified, searching of the configuration file is performed as follows:


1. If the *[-project_name](../code/command_line.md#project_name)* CLI option is set, the project folder in the User profile will be checked first for the configuration file. At that, only the name of the specified file will be checked. For example, if you run the application as follows: ```bash bin/main_x64d.exe -project_name "my_project" -boot_config "configs/my_config.boot" ``` The engine will check the `my_config.boot` file in the following folder:

  - On Windows, `C:/Users/<username>/my_project/data/configs/`
  - On Linux, `/home/<username>/.my_project/data/configs/`
2. By default, the path to the configuration file will be checked relative to the *[-data_path](../code/command_line.md#data_path)*.
3. If the configuration file isn't found, the engine will try to create a default file relative to the `data` folder or in the project folder specified in the *-project_name*.


> **Notice:** If the configuration files are stored in a [`*.ung` package](../principles/filesystem/index_cpp.md#types), they won't be loaded and, therefore, the engine will be initialized with the default settings. However, when the file system is initialized, you can specify the path to the configuration files stored in the package via the set of corresponding console commands:
> - [`boot_config`](../code/console/index.md#boot_config)
> - [`config`](../code/console/index.md#config)
> - [`controls_config`](../code/console/index.md#controls_config)
> - [`global_config`](../code/console/index.md#global_config)
> - [`user_config`](../code/console/index.md#user_config)
>
>  Then you can load the configuration files by using the corresponding *[`*_load`](../code/console/index.md#boot_config_load)* console commands.


## Startup Configuration


This is the main configuration file containing the following Engine startup parameters:


- Paths to GUI skin, log-file, system and UnigineEditor cache files.
- [Boot and Splash screen](../code/gui/screens/index.md) settings.
- Extern defines.
- Console commands.
- [Startup command-line parameters](../code/command_line.md) and a group of world manager settings.
- Information about location of other configuration files.


Expand the following spoiler to see an example of boot configuration file:


<details>
<summary>example.boot | Close</summary>

```xml
<?xml version="1.0" encoding="utf-8"?>
<boot version="2.21.0.0" autosave="0">
	<gui_path>core/gui/</gui_path>
	<engine_log>log.txt</engine_log>
	<system_script>core/unigine.usc</system_script>
	<cache_path/>
	<system_cache>unigine.cache</system_cache>
	<editor_cache>editor.cache</editor_cache>
	<video_app>auto</video_app>
	<sound_app>auto</sound_app>
	<extern_define/>
	<console_command/>
	<window_title>Project Name</window_title>
	<plugin_paths>
		<path>plugins/</path>
		<path>../extra/plugins/</path>
	</plugin_paths>
	<extern_plugins>
		<plugin>OpenVR</plugin>
		<plugin>AdditionalPlugin</plugin>
	</extern_plugins>
	<console>

		<async_log_mode>0</async_log_mode>
		<async_log_priority>0</async_log_priority>
		<auto_dpi_scaling>1</auto_dpi_scaling>
		<auto_quit>1</auto_quit>
		<background_update>0</background_update>
		<config>configs/default.config</config>
		<console_font>core/gui/console.ttf</console_font>
		<console_limit>16384</console_limit>
		<console_size>16</console_size>
		<controls_config>configs/default.controls</controls_config>

		<d3d12_small_pool_enabled>1</d3d12_small_pool_enabled>

		<decal_pool_chunk_size>16</decal_pool_chunk_size>
		<dpi_awareness>2</dpi_awareness>
		<filesystem_cache>2</filesystem_cache>
		<filesystem_mmap>1</filesystem_mmap>
		<fsr_max_contexts>8</fsr_max_contexts>
		<log_file>1</log_file>
		<log_stdout>1</log_stdout>
		<main_window>1</main_window>
		<main_window_auto_restart>1</main_window_auto_restart>
		<main_window_borders>1</main_window_borders>
		<main_window_fullscreen>0</main_window_fullscreen>
		<main_window_fullscreen_display>0</main_window_fullscreen_display>
		<main_window_fullscreen_display_mode>0</main_window_fullscreen_display_mode>
		<main_window_resizable>1</main_window_resizable>
		<main_window_size>1920 1080</main_window_size>
		<materials_preload>1</materials_preload>
		<memory_dynamic_pool>256</memory_dynamic_pool>
		<memory_statistics_enabled>1</memory_statistics_enabled>
		<particles_memory_preload>50</particles_memory_preload>
		<process_priority>1</process_priority>
		<profiler_font>core/gui/font.ttf</profiler_font>
		<profiler_size>13</profiler_size>
		<pso_preload>0</pso_preload>
		<shader_cache_preload>0</shader_cache_preload>
		<shaders_preload>1</shaders_preload>
		<skinned_pool_chunk_size>64</skinned_pool_chunk_size>
		<splash_screen>1</splash_screen>
		<starting_world/>
		<dlss_application_id>0</dlss_application_id>
		<dlss_project_id>33ff81e1-c170-5bb9-6995-d76d2664cd27</dlss_project_id>
		<swap_delay_warning>0</swap_delay_warning>
		<swap_delay_warning_time>200</swap_delay_warning_time>
		<user_config>configs/default.user</user_config>
		<video_adapter>0</video_adapter>
		<video_debug>0</video_debug>
		<video_debug_crash_dump>0</video_debug_crash_dump>
		<video_debug_shader>0</video_debug_shader>
		<video_offscreen>0</video_offscreen>
		<video_quadro_sync>0</video_quadro_sync>
		<vr_debug_mode>0</vr_debug_mode>
		<vr_foveated_rendering_enabled>1</vr_foveated_rendering_enabled>
		<vr_hand_tracking_show_basis>0</vr_hand_tracking_show_basis>
		<vr_hand_tracking_show_bone_sizes>0</vr_hand_tracking_show_bone_sizes>
		<vr_hand_tracking_show_velocity>0</vr_hand_tracking_show_velocity>
		<vr_hand_tracking_visualizer_enabled>0</vr_hand_tracking_visualizer_enabled>
		<vr_head_tracking_position_enabled>1</vr_head_tracking_position_enabled>
		<vr_head_tracking_rotation_enabled>1</vr_head_tracking_rotation_enabled>
		<vr_mirror_mode>3</vr_mirror_mode>
		<vr_mixed_reality_alpha_blend_enabled>0</vr_mixed_reality_alpha_blend_enabled>
		<vr_mixed_reality_blend_masking_debug_enabled>0</vr_mixed_reality_blend_masking_debug_enabled>
		<vr_mixed_reality_blend_masking_mode>0</vr_mixed_reality_blend_masking_mode>
		<vr_mixed_reality_camera_exposure_time>2</vr_mixed_reality_camera_exposure_time>
		<vr_mixed_reality_camera_exposure_time_mode>1</vr_mixed_reality_camera_exposure_time_mode>
		<vr_mixed_reality_camera_flicker_compensation>1</vr_mixed_reality_camera_flicker_compensation>
		<vr_mixed_reality_camera_iso>4</vr_mixed_reality_camera_iso>
		<vr_mixed_reality_camera_iso_mode>1</vr_mixed_reality_camera_iso_mode>
		<vr_mixed_reality_camera_sharpness>0</vr_mixed_reality_camera_sharpness>
		<vr_mixed_reality_camera_vst_reprojection_distance>0</vr_mixed_reality_camera_vst_reprojection_distance>
		<vr_mixed_reality_camera_vst_reprojection_mode>0</vr_mixed_reality_camera_vst_reprojection_mode>
		<vr_mixed_reality_camera_white_balance>7</vr_mixed_reality_camera_white_balance>
		<vr_mixed_reality_camera_white_balance_mode>2</vr_mixed_reality_camera_white_balance_mode>
		<vr_mixed_reality_chroma_key_enabled>0</vr_mixed_reality_chroma_key_enabled>
		<vr_mixed_reality_cubemap_ggx_quality>1</vr_mixed_reality_cubemap_ggx_quality>
		<vr_mixed_reality_cubemap_mode>2</vr_mixed_reality_cubemap_mode>
		<vr_mixed_reality_depth_test_enabled>0</vr_mixed_reality_depth_test_enabled>
		<vr_mixed_reality_depth_test_range>0 1</vr_mixed_reality_depth_test_range>
		<vr_mixed_reality_depth_test_range_enabled>0</vr_mixed_reality_depth_test_range_enabled>
		<vr_mixed_reality_marker_tracking_enabled>0</vr_mixed_reality_marker_tracking_enabled>
		<vr_mixed_reality_marker_visualizer_enabled>0</vr_mixed_reality_marker_visualizer_enabled>
		<vr_mixed_reality_override_color_correction_mode>0</vr_mixed_reality_override_color_correction_mode>
		<vr_mixed_reality_video_enabled>0</vr_mixed_reality_video_enabled>
		<vr_mixed_reality_view_offset>0</vr_mixed_reality_view_offset>
		<vr_motion_prediction>0</vr_motion_prediction>
		<vr_motion_prediction_velocity_precision>32</vr_motion_prediction_velocity_precision>
		<vr_motion_prediction_velocity_time_delta>0.0166666675</vr_motion_prediction_velocity_time_delta>
		<vr_peripheral_rendering_mode_enabled>1</vr_peripheral_rendering_mode_enabled>
		<vr_render_enabled>1</vr_render_enabled>
		<vr_service_init_timeout>60</vr_service_init_timeout>
		<vr_tracking_space>2</vr_tracking_space>
		<vr_window_mode>1</vr_window_mode>
		<world_manager_images_memory>128</world_manager_images_memory>
		<world_manager_meshes_memory>128</world_manager_meshes_memory>
	</console>
	<screen>
		<enabled>1</enabled>
		<width>570</width>
		<height>400</height>
		<background_color>0, 0, 0, 0</background_color>
		<transform>0.5, 0.33, 0.5, 0.5</transform>
		<threshold>16</threshold>
		<texture>textures/boot_screen.png</texture>
		<font>fonts/boot_screen_font.ttf</font>
		<text>
			<![CDATA[
				<p align="center">
					<font color="#606060" size="16">
						<xy y="%100" dy="-20"/>Project Name
					</font>
				</p>
			]]>
		</text>
		<messages>
			<engine_init>Custom message for engine initialization.</engine_init>
			<file_system_init>Custom message for file system initialization.</file_system_init>
			<materials_init>Custom message for materials initialization.</materials_init>
			<materials_preloading>Custom message for materials pre-loading.</materials_preloading>
			<properties_init>Custom message for properties initialization.</properties_init>
			<static_meshes_init>Custom message for static meshes initialization.</static_meshes_init>
			<shaders_compilation>Custom message for shaders compilation.</shaders_compilation>
		</messages>
	</screen>
</boot>

```

</details>


By default, the `configs/default.boot` file is used. To run the application with another boot configuration file, specify the path to it using the *[-boot_config](../code/command_line.md#boot_config)* command-line option.


The boot configuration file has the following structure:


```xml
<boot version="2.21.0.0" autosave="0">
	<cli_option>value</cli_option>
	...
	<console>
		<console_command>value</console_command>
		...
	</console>
	<screen>
		...
	</screen>
</boot>

```


The application start-up options can be set via both the command-line and the boot configuration file.


> **Notice:** Values stored in this config file are overridden by the [command-line parameters](../code/command_line.md) specified at the Engine startup. For example, if you specify the *-video_app* command-line option on the application start-up, the corresponding setting *video_app* in the configuration file will be ignored.


The configuration file contains the following parameters:


- The **autosave** attribute enables automatic saving of start-up configuration to the file on loading, closing, and saving the world, as well as on the Engine shutdown.
- A set of start-up CLI options: | - [*gui_path*](../code/command_line.md#gui_path) - [*engine_log*](../code/command_line.md#engine_log) - [*system_script*](../code/command_line.md#system_script) | - [*cache_path*](../code/command_line.md#cache_path) - [*system_cache*](../code/command_line.md#system_cache) | - [*editor_cache*](../code/command_line.md#editor_cache) - [*video_app*](../code/command_line.md#video_app) - [*sound_app*](../code/command_line.md#sound_app) | - [*extern_define*](../code/command_line.md#extern_define) - [*console_command*](../code/command_line.md#console_command) | |---|---|---|---|
- **window_title** - title to be set for the application window.
- **plugin_paths** - a list of [paths to directories](../code/command_line.md#plugin_path) that contain plugins. ```xml <plugin_paths> <path>plugins/</path> <path>../extra/plugins/</path> </plugin_paths> ``` > **Notice:** All specified plugin paths (*plugin_path*) will be ignored, if at least one *-plugin_path* is specified in the command-line.
- **extern_plugins** - a list of [plugin libraries](../code/command_line.md#extern_plugin) to be loaded. ```xml <extern_plugins> <plugin>FBXImporter</plugin> <plugin>CADImporter</plugin> <plugin>OpenVR</plugin> </extern_plugins> ```
- The **console** section contains the console variables to be defined at the engine start-up: | - [***config***](../code/console/index.md#config) - [***controls_config***](../code/console/index.md#controls_config) - [***user_config***](../code/console/index.md#user_config) - [*async_log_mode*](../code/console/index.md#async_log_mode) - [*async_log_priority*](../code/console/index.md#async_log_priority) - [*background_update*](../code/console/index.md#background_update) - [*console_font*](../code/console/index.md#console_font) - [*console_size*](../code/console/index.md#console_size) - [*filesystem_mmap*](../code/console/index.md#filesystem_mmap) - [*dpi_awareness*](../code/console/index.md#dpi_awareness) - [*auto_dpi_scaling*](../code/console/index.md#auto_dpi_scaling) - [*mesh_procedural_path*](../code/console/index.md#mesh_procedural_path) - [*mesh_procedural_read_only*](../code/console/index.md#mesh_procedural_read_only) | - [*process_priority*](../code/console/index.md#process_priority) - [*profiler_font*](../code/console/index.md#profiler_font) - [*profiler_size*](../code/console/index.md#profiler_size) - [*splash_screen*](../code/console/index.md#splash_screen) - [*starting_world*](../code/console/index.md#starting_world) - [*swap_delay_warning*](../code/console/index.md#swap_delay_warning) - [*swap_delay_warning_time*](../code/console/index.md#swap_delay_warning_time) - [*video_adapter*](../code/console/index.md#video_adapter) - [*video_debug*](../code/console/index.md#video_debug) - [*video_debug_shader*](../code/console/index.md#video_debug_shader) - [*video_offscreen*](../code/console/index.md#video_offscreen) | - [*main_window*](../code/console/index.md#main_window) - [*main_window_fullscreen*](../code/console/index.md#main_window_fullscreen) - [*main_window_size*](../code/console/index.md#main_window_size) - [*main_window_resizable*](../code/console/index.md#main_window_resizable) - [*main_window_auto_restart*](../code/console/index.md#main_window_auto_restart) - [*main_window_borders*](../code/console/index.md#main_window_borders) - [*main_window_fullscreen_display*](../code/console/index.md#main_window_fullscreen_display) - [*main_window_fullscreen_display_mode*](../code/console/index.md#main_window_fullscreen_display_mode) - [*world_manager_images_memory*](../code/console/index.md#world_manager_images_memory) - [*world_manager_meshes_memory*](../code/console/index.md#world_manager_meshes_memory) - [*materials_preload*](../code/console/index.md#materials_preload) - [*shaders_preload*](../code/console/index.md#shaders_preload) - [*dlss_application_id*](../code/console/index.md#dlss_application_id) | |---|---|---|
- The **screen** section lists the [boot screen](../code/gui/screens/index.md#boot) parameters.


To read values from the configuration file and write them back, use functionality of the *[BootConfig](../api/library/engine/class.bootconfig_cpp.md)* class.


## Application Configuration


This file stores all custom application settings. By default, the `configs/default.config` file is used. To use another configuration file, specify the path to it in the [boot configuration file](#boot).


The configuration file has the following format:


```xml
<config version="2.21.0.0" autosave="1">
	<item name="option_name" type="option_type">option_value</item>
	...
	<item name="option_name" type="option_type">option_value</item>
</config>

```


Expand the following spoiler to see an example of application configuration file:


<details>
<summary>example.config | Close</summary>

```xml
<?xml version="1.0" encoding="utf-8"?>
<config version="2.21.0.0" autosave="1">
	<player_avatar>soldier</player_avatar>
	<skip_curscenes>1</skip_curscenes>
	<bulletshell_lifetime>100</bulletshell_lifetime>
</config>

```

</details>


The **autosave** attribute enables automatic saving of configuration settings to the file on loading, closing, and saving the world, as well as on the Engine shutdown.


Each ***item*** corresponds to one setting:


- *option_name* - a name of the engine-related and project-related setting. It is the same as a name of the corresponding [console](../code/console/index.md) variable.
- *option_type* - a type of the setting: **bool*, *int*, *float*, *string**.


To read values from the configuration file and write them back, use functionality of the *[Config](../api/library/engine/class.config_cpp.md)* class. Use the appropriate methods depending on the type of the target item.


## Controls Configuration


This file stores *keyboard control keys* and settings defining the *mouse behavior*. These settings are configured via the UnigineEditor (*[Windows -> Settings -> Runtime -> Controls](../editor2/settings/controls/index.md)*).


> **Notice:** The *[ControlsApp](../api/library/controls/class.controlsapp_cpp.md)* class used to manage this configuration is considered deprecated - for handling input in new projects, use the *[Input](../api/library/controls/class.input_cpp.md)* class instead. The `.controls` file itself remains in use.


By default, the `configs/default.controls` file is used. To use another configuration file, specify the path to it in the [boot configuration file](#boot).


The controls configuration file has the following format:


```xml
<controls version="2.21.0.0" autosave="1">
	<remove_grab_key>ESC</remove_grab_key>
	<controls_always_run>0</controls_always_run>
	<controls_mouse_handle>2</controls_mouse_handle>
	<controls_mouse_inverse>0</controls_mouse_inverse>
	<controls_mouse_raw_input>1</controls_mouse_raw_input>
	<controls_mouse_sensitivity>1</controls_mouse_sensitivity>
	<keys>
		<FORWARD>W</FORWARD>
		<BACKWARD>S</BACKWARD>
		...
	</keys>
	<mouse_buttons>
		<FIRE>LEFT</FIRE>
		...
	</mouse_buttons>
</controls>
```


Expand the following spoiler to see an example of controls configuration file:


<details>
<summary>example.controls | Close</summary>

```xml
<?xml version="1.0" encoding="utf-8"?>
<controls version="2.21.0.0" autosave="1">
	<remove_grab_key>ESC</remove_grab_key>
	<controls_always_run>0</controls_always_run>
	<controls_mouse_handle>2</controls_mouse_handle>
	<controls_mouse_inverse>0</controls_mouse_inverse>
	<controls_mouse_raw_input>1</controls_mouse_raw_input>
	<controls_mouse_sensitivity>1</controls_mouse_sensitivity>
	<keys>
		<FORWARD>W</FORWARD>
		<BACKWARD>S</BACKWARD>
		<MOVE_LEFT>A</MOVE_LEFT>
		<MOVE_RIGHT>D</MOVE_RIGHT>
		<TURN_UP>UP</TURN_UP>
		<TURN_DOWN>DOWN</TURN_DOWN>
		<TURN_LEFT>LEFT</TURN_LEFT>
		<TURN_RIGHT>RIGHT</TURN_RIGHT>
		<CROUCH>Q</CROUCH>
		<JUMP>E</JUMP>
		<RUN>LEFT_SHIFT</RUN>
		<USE>ENTER</USE>
		<FIRE>UNKNOWN</FIRE>
		<SAVE>F5</SAVE>
		<RESTORE>F6</RESTORE>
		<SCREENSHOT>F12</SCREENSHOT>
		<AUX_0>UNKNOWN</AUX_0>
		<!-- ... AUX_1 ... AUX_F ... -->
	</keys>
	<mouse_buttons>
		<FIRE>LEFT</FIRE>
		<!-- the remaining states are UNKNOWN by default -->
	</mouse_buttons>
</controls>

```

</details>


The parameters are:


- The **autosave** attribute enables automatic saving of controls configuration to the file on loading, closing, and saving the world, as well as on the Engine shutdown.
- **remove_grab_key** - the key that releases the mouse grab.
- **controls_always_run** - sets the **[Always Run](../editor2/settings/controls/index.md)** option.
- **controls_mouse_handle** - sets the **[Mouse Handle](../editor2/settings/controls/index.md)** option.
- **controls_mouse_inverse** - sets the **[Invert Mouse](../editor2/settings/controls/index.md)** option.
- **controls_mouse_raw_input** - enables raw (unaccelerated) mouse input.
- **controls_mouse_sensitivity** - sets the **[Mouse Speed](../editor2/settings/controls/index.md)** option.
- **keys** - keyboard key bindings for the *[STATE_*](../api/library/controls/class.controls_cpp.md#STATE_FORWARD)* states of the *Controls* class. Each child element is named after the state (FORWARD, BACKWARD, etc.) and contains the bound key name. Unassigned states have the UNKNOWN value.
- **mouse_buttons** - mouse button bindings for the same *[STATE_*](../api/library/controls/class.controls_cpp.md#STATE_FORWARD)* states.


To manage the controls configuration, use functionality of the *[ControlsApp](../api/library/controls/class.controlsapp_cpp.md)* class or classes derived from the *[Controls](../api/library/controls/class.controls_cpp.md)* class.


## Global Configuration


This file stores global project settings shared by everyone working on the project: declarations of [custom surface and material parameters](../content/materials/custom_parameters/index.md), and [custom render parameters](../content/materials/render_parameters.md) along with their values. By default, the `configs/default.global` file is used. To use another configuration file, specify the path to it using the *`-global_config`* command-line option.


The global configuration file has the following format:


```xml
<?xml version="1.0" encoding="utf-8"?>
<global version="2.22.0.0" autosave="0">
	<console>
		<variable>value</variable>
		...
	</console>
	<render>
		<parameters/>
		<surface_custom_parameters/>
		<material_custom_parameters/>
	</render>
</global>

```


Expand the following spoiler to see an example of global configuration file:


<details>
<summary>example.global | Close</summary>

```xml
<?xml version="1.0" encoding="utf-8"?>
<global version="2.22.0.0" autosave="0">
	<console>
		<profiling_dump_dir>profiling_dump</profiling_dump_dir>
	</console>
	<render>
		<parameters>
			<parameter name="GlobalWetness" guid="<guid>" type="float" dynamic="1">0.7</parameter>
			<parameter name="SunTint" guid="<guid>" type="float3" dynamic="1">1 0.9 0.8</parameter>
		</parameters>
		<surface_custom_parameters>
			<radar_reflectivity guid="<guid>" type="float" default="0.2" min="0" max="1"/>
			<team guid="<guid>" type="int" default="0" min="0" max="100"/>
		</surface_custom_parameters>
		<material_custom_parameters>
			<emission_boost guid="<guid>" type="float" default="0" min="0" max="1"/>
		</material_custom_parameters>
	</render>
</global>

```

</details>


The **autosave** attribute enables automatic saving of global configuration settings to the file on loading, closing, and saving the world, when the application window loses focus, as well as on the Engine shutdown. It is disabled by default, so the settings are written only on an explicit save.


> **Notice:** This file is not meant to be edited by hand. It is written by *UnigineEditor* when you press *Save* on the *Settings -> Runtime -> World -> Render -> [Custom Parameters](../editor2/settings/render_settings/custom_parameters/index.md)* page, by the *[`global_config_save`](../code/console/index.md#global_config_save)* console command, or by the *[*GlobalConfig::save()*](../api/library/engine/class.globalconfig_cpp.md#save_int)* method. If the file doesn't exist on the application start-up, it is created with the default settings.


The file has the following sections:


- The **console** section lists values of the [console](../code/console/index.md) variables saved to the `*.global` configuration file. <details> <summary>Console commands in *.global configuration file | Close</summary> - [profiling_dump_dir](../code/console/#profiling_dump_dir) </details>
- The **render** section stores the declarations of custom parameters and the values of the ones that belong to the project as a whole:

  - **parameters** - [custom render parameters](../content/materials/render_parameters.md). Each **parameter** element keeps the name, the GUID, the type, the [Dynamic](../editor2/settings/render_settings/custom_parameters/index.md#dynamic) flag, and the value of the parameter, because a render parameter is global and has a single value for the whole project.
  - **surface_custom_parameters** and **material_custom_parameters** - [declarations of custom surface and material parameters](../content/materials/custom_parameters/declaring_and_setting_cpp.md#declare_storage). Each element is named after the parameter and keeps its GUID, type, default value, and the range of values. Only the declarations are stored here: values of a surface are saved in the world, values of a material - in its `*.mat` file.


> **Notice:** Values written on a surface or a material are stored under the GUID of the parameter, so a parameter can be renamed or moved up and down the list without losing them. For the same reason the GUIDs in this file should be preserved: replacing them detaches the values already written into the assets of the project.


To control the global configuration file, use functionality of the *[GlobalConfig](../api/library/engine/class.globalconfig_cpp.md)* class.


## User Configuration


This file stores various personal settings, such as helpers (wireframe, profiler, etc.). By default, the `configs/default.user` file is used. To use another configuration file, specify the path to it in the [boot configuration file](#boot).


> **Notice:** This configuration file should be added to the *ignore* list of your [Version Control System](../editor2/assets_workflow/version_control/index.md#ignore) (VCS) as it stores preferences of a particular user.


The user configuration file has the following format:


```xml
<?xml version="1.0" encoding="utf-8"?>
<user version="2.21.0.0" autosave="1">
	<parameter>value</parameter>
	...
</user>

```


Expand the following spoiler to see an example of user configuration file:


<details>
<summary>example.user | Close</summary>

```xml
<?xml version="1.0" encoding="utf-8"?>
<user version="2.21.0.0" autosave="1">
	<console_height>75</console_height>
	<console_key>BACK_QUOTE</console_key>
	<console_key_modifier/>
	<console_onscreen>0</console_onscreen>
	<console_onscreen_font_size>14</console_onscreen_font_size>
	<console_onscreen_height>20</console_onscreen_height>
	<console_onscreen_time>2</console_onscreen_time>
	<console_wrapping>0</console_wrapping>
	<materials_reload_event>1</materials_reload_event>
	<microprofile_dump_frames>500</microprofile_dump_frames>
	<microprofile_enabled>1</microprofile_enabled>
	<microprofile_webserver_frames>200</microprofile_webserver_frames>
	<physics_show_collision_surfaces>0</physics_show_collision_surfaces>
	<physics_show_contacts>0</physics_show_contacts>
	<physics_show_joints>0</physics_show_joints>
	<physics_show_shapes>0</physics_show_shapes>
	<physics_show_shapes_distance>500</physics_show_shapes_distance>
	<render_show_alpha_test>0</render_show_alpha_test>
	<render_show_ambient>0</render_show_ambient>
	<render_show_cascades>0</render_show_cascades>
	<render_show_clusters>0</render_show_clusters>
	<render_show_collision_mask>0</render_show_collision_mask>
	<render_show_collision_mask_bits>-1</render_show_collision_mask_bits>
	<render_show_complex_shadow_shader>0</render_show_complex_shadow_shader>
	<render_show_decals>0</render_show_decals>
	<render_show_dynamic>0</render_show_dynamic>
	<render_show_emission>0</render_show_emission>
	<render_show_field_mask>0</render_show_field_mask>
	<render_show_field_mask_bits>-1</render_show_field_mask_bits>
	<render_show_geodetic_pivot>0</render_show_geodetic_pivot>
	<render_show_immovable>0</render_show_immovable>
	<render_show_intersection>0</render_show_intersection>
	<render_show_intersection_mask>0</render_show_intersection_mask>
	<render_show_intersection_mask_bits>-1</render_show_intersection_mask_bits>
	<render_show_landscape_albedo>0</render_show_landscape_albedo>
	<render_show_landscape_mask>0</render_show_landscape_mask>
	<render_show_landscape_terrain_vt_streaming>0</render_show_landscape_terrain_vt_streaming>
	<render_show_lighting_mode>0</render_show_lighting_mode>
	<render_show_lightmap_checker>0</render_show_lightmap_checker>
	<render_show_manual_materials>0</render_show_manual_materials>
	<render_show_material_mask>0</render_show_material_mask>
	<render_show_material_mask_bits>-1</render_show_material_mask_bits>
	<render_show_mesh_dynamics>0</render_show_mesh_dynamics>
	<render_show_mesh_statics>0</render_show_mesh_statics>
	<render_show_navigation_mask>0</render_show_navigation_mask>
	<render_show_navigation_mask_bits>-1</render_show_navigation_mask_bits>
	<render_show_nodes_interaction_clutter>0</render_show_nodes_interaction_clutter>
	<render_show_nodes_interaction_grass>0</render_show_nodes_interaction_grass>
	<render_show_nodes_interaction_trigger>0</render_show_nodes_interaction_trigger>
	<render_show_non_manual_materials>0</render_show_non_manual_materials>
	<render_show_obstacle_mask>0</render_show_obstacle_mask>
	<render_show_obstacle_mask_bits>-1</render_show_obstacle_mask_bits>
	<render_show_occluder>0</render_show_occluder>
	<render_show_physical_exclusion_mask>0</render_show_physical_exclusion_mask>
	<render_show_physical_exclusion_mask_bits>-1</render_show_physical_exclusion_mask_bits>
	<render_show_physical_mask>0</render_show_physical_mask>
	<render_show_physical_mask_bits>-1</render_show_physical_mask_bits>
	<render_show_physics_intersection>0</render_show_physics_intersection>
	<render_show_physics_intersection_mask>0</render_show_physics_intersection_mask>
	<render_show_physics_intersection_mask_bits>-1</render_show_physics_intersection_mask_bits>
	<render_show_queries>0</render_show_queries>
	<render_show_scissors>0</render_show_scissors>
	<render_show_shadow_mask>0</render_show_shadow_mask>
	<render_show_shadow_mask_bits>-1</render_show_shadow_mask_bits>
	<render_show_sound_occlusion_mask>0</render_show_sound_occlusion_mask>
	<render_show_sound_occlusion_mask_bits>-1</render_show_sound_occlusion_mask_bits>
	<render_show_sound_reverb_mask>0</render_show_sound_reverb_mask>
	<render_show_sound_reverb_mask_bits>-1</render_show_sound_reverb_mask_bits>
	<render_show_sound_source_mask>0</render_show_sound_source_mask>
	<render_show_sound_source_mask_bits>-1</render_show_sound_source_mask_bits>
	<render_show_surface_custom_texture>0</render_show_surface_custom_texture>
	<render_show_surface_custom_texture_not_available>0</render_show_surface_custom_texture_not_available>
	<render_show_surface_custom_texture_not_used>0</render_show_surface_custom_texture_not_used>
	<render_show_texture_resolution>0</render_show_texture_resolution>
	<render_show_textures>0</render_show_textures>
	<render_show_textures_number>7</render_show_textures_number>
	<render_show_textures_offset>0</render_show_textures_offset>
	<render_show_transparent>0</render_show_transparent>
	<render_show_triangles>0</render_show_triangles>
	<render_show_vertex_color>0</render_show_vertex_color>
	<render_show_viewport_mask>0</render_show_viewport_mask>
	<render_show_viewport_mask_bits>-1</render_show_viewport_mask_bits>
	<render_show_voxel_probe_visualizer>0</render_show_voxel_probe_visualizer>
	<render_show_world_shadow_casters>0</render_show_world_shadow_casters>
	<screenshot_extension>tga</screenshot_extension>
	<show_fps>0</show_fps>
	<show_profiler>0</show_profiler>
	<show_profiler_charts>1</show_profiler_charts>
	<show_profiler_generic>0</show_profiler_generic>
	<show_profiler_memory>0</show_profiler_memory>
	<show_profiler_physics>0</show_profiler_physics>
	<show_profiler_render>1</show_profiler_render>
	<show_profiler_thread>0</show_profiler_thread>
	<show_profiler_world>0</show_profiler_world>
	<show_visualizer>0</show_visualizer>
	<visualizer_fix_flicker>1</visualizer_fix_flicker>
	<world_handler_3d>0</world_handler_3d>
	<world_handler_distance>500</world_handler_distance>
	<world_show_handler/>
	<world_show_spatial>0</world_show_spatial>
	<world_show_visualizer/>
	<console_bindings/>
</user>

```

</details>


The **autosave** attribute enables automatic saving of user configuration settings to the file on loading, closing, and saving the world, as well as on the Engine shutdown.


This file stores personal settings such as helpers (wireframe, profiler, etc.) and various debug visualization options. In the [Console](../code/console/index.md) article, all such variables are marked as saved to the `*.user` configuration file.


<details>
<summary>Console commands in *.user configuration file | Close</summary>

- [bind](../code/console/#bind)
- [console_key](../code/console/#console_key)
- [console_key_modifier](../code/console/#console_key_modifier)
- [console_height](../code/console/#console_height)
- [console_onscreen](../code/console/#console_onscreen)
- [console_onscreen_font_size](../code/console/#console_onscreen_font_size)
- [console_onscreen_height](../code/console/#console_onscreen_height)
- [console_onscreen_time](../code/console/#console_onscreen_time)
- [console_wrapping](../code/console/#console_wrapping)
- [materials_reload_event](../code/console/#materials_reload_event)
- [show_visualizer](../code/console/#show_visualizer)
- [show_fps](../code/console/#show_fps)
- [visualizer_fix_flicker](../code/console/#visualizer_fix_flicker)
- [world_show_spatial](../code/console/#world_show_spatial)
- [world_show_visualizer](../code/console/#world_show_visualizer)
- [render_show_triangles](../code/console/#render_show_triangles)
- [render_show_voxel_probe_visualizer](../code/console/#render_show_voxel_probe_visualizer)
- [world_show_handler](../code/console/#world_show_handler)
- [world_handler_3d](../code/console/#world_handler_3d)
- [world_handler_distance](../code/console/#world_handler_distance)
- [render_show_decals](../code/console/#render_show_decals)
- [render_show_landscape_albedo](../code/console/#render_show_landscape_albedo)
- [render_show_landscape_mask](../code/console/#render_show_landscape_mask)
- [render_show_landscape_terrain_vt_streaming](../code/console/#render_show_landscape_terrain_vt_streaming)
- [physics_show_collision_surfaces](../code/console/#physics_show_collision_surfaces)
- [physics_show_contacts](../code/console/#physics_show_contacts)
- [physics_show_joints](../code/console/#physics_show_joints)
- [physics_show_shapes](../code/console/#physics_show_shapes)
- [physics_show_shapes_distance](../code/console/#physics_show_shapes_distance)
- [experimental_navigation_show_mesh](../code/console/#experimental_navigation_show_mesh)
- [experimental_navigation_show_mesh_mode](../code/console/#experimental_navigation_show_mesh_mode)
- [experimental_navigation_show_mesh_depth_test](../code/console/#experimental_navigation_show_mesh_depth_test)
- [experimental_navigation_show_mesh_tiles](../code/console/#experimental_navigation_show_mesh_tiles)
- [render_show_occluder](../code/console/#render_show_occluder)
- [render_show_queries](../code/console/#render_show_queries)
- [show_profiler](../code/console/#show_profiler)
- [show_profiler_charts](../code/console/#show_profiler_charts)
- [show_profiler_table](../code/console/#show_profiler_table)
- [show_profiler_experimental_navigation](../code/console/#show_profiler_experimental_navigation)
- [show_profiler_generic](../code/console/#show_profiler_generic)
- [show_profiler_memory](../code/console/#show_profiler_memory)
- [show_profiler_memory_object](../code/console/#show_profiler_memory_object)
- [show_profiler_physics](../code/console/#show_profiler_physics)
- [show_profiler_render](../code/console/#show_profiler_render)
- [show_profiler_thread](../code/console/#show_profiler_thread)
- [show_profiler_world](../code/console/#show_profiler_world)
- [microprofile_webserver_frames](../code/console/#microprofile_webserver_frames)
- [microprofile_dump_frames](../code/console/#microprofile_dump_frames)
- [render_show_cascades](../code/console/#render_show_cascades)
- [screenshot_extension](../code/console/#screenshot_extension)
- [render_show_queries](../code/console/#render_show_queries)
- [render_show_decals](../code/console/#render_show_decals)
- [render_show_scissors](../code/console/#render_show_scissors)
- [render_show_occluder](../code/console/#render_show_occluder)
- [render_show_cascades](../code/console/#render_show_cascades)
- [render_show_visualizer_distance](../code/console/#render_show_visualizer_distance)
- [render_show_alpha_test](../code/console/#render_show_alpha_test)
- [render_show_depth_pre_pass](../code/console/#render_show_depth_pre_pass)
- [render_show_immovable](../code/console/#render_show_immovable)
- [render_show_dynamic](../code/console/#render_show_dynamic)
- [render_show_transparent](../code/console/#render_show_transparent)
- [render_show_transparent_gbuffer](../code/console/#render_show_transparent_gbuffer)
- [render_show_transparent_lighting_ambient](../code/console/#render_show_transparent_lighting_ambient)
- [render_show_transparent_lighting_environment_probe](../code/console/#render_show_transparent_lighting_environment_probe)
- [render_show_transparent_lighting_voxel_probe](../code/console/#render_show_transparent_lighting_voxel_probe)
- [render_show_transparent_lighting_planar_probe](../code/console/#render_show_transparent_lighting_planar_probe)
- [render_show_transparent_lighting_light_omni](../code/console/#render_show_transparent_lighting_light_omni)
- [render_show_transparent_lighting_light_proj](../code/console/#render_show_transparent_lighting_light_proj)
- [render_show_transparent_lighting_light_world](../code/console/#render_show_transparent_lighting_light_world)
- [render_show_ambient](../code/console/#render_show_ambient)
- [render_show_geodetic_pivot](../code/console/#render_show_geodetic_pivot)
- [render_show_landscape_mask](../code/console/#render_show_landscape_mask)
- [render_show_landscape_albedo](../code/console/#render_show_landscape_albedo)
- [render_show_textures](../code/console/#render_show_textures)
- [render_show_textures_offset](../code/console/#render_show_textures_offset)
- [render_show_textures_number](../code/console/#render_show_textures_number)
- [render_show_triangles](../code/console/#render_show_triangles)
- [render_show_vertex_color](../code/console/#render_show_vertex_color)
- [render_show_nodes_interaction_grass](../code/console/#render_show_nodes_interaction_grass)
- [render_show_nodes_interaction_clutter](../code/console/#render_show_nodes_interaction_clutter)
- [render_show_nodes_interaction_trigger](../code/console/#render_show_nodes_interaction_trigger)

</details>


To control the user configuration file, use functionality of the *[UserConfig](../api/library/engine/class.userconfig_cpp.md)* class.
