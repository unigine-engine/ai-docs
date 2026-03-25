# Loading and Splash Screens


The UNIGINE [**Initialization**](../../../code/fundamentals/execution_sequence/init.md) includes 3 types of screens shown at different steps:

- [**Boot**](#boot) screen.
- [**Splash**](#splash) screen with UNIGINE logo animation.
- [**Loading**](#loading) screens.


### See Also


- Quick Video Guide: [How To Customize Boot Screen.](../../../videotutorials/how_to/how_to_basics/boot_screen.md)
- Quick Video Guide: [How To Disable Splash Screen.](../../../videotutorials/how_to/how_to_basics/splash_screen.md)
- Quick Video Guide: [How To Customize Loading Screens.](../../../videotutorials/how_to/how_to_cs/loading_screen.md)


## Boot Screen


![](boot_screen.jpg)

*The default boot screens of UNIGINE SDK editions.*


The Boot screen comes first early in the Engine initialization. It goes through several initialization steps, showing the loading progress.


> **Notice:** Fonts, textures, or any other resources used in the boot screen **cannot be packed into an UNG archive**.


The boot screen offers you a lot of flexibility in customization by editing the **screen** section of the `default.boot` [configuration file](../../../code/configuration_file_cpp.md):


```xml

<boot version="2.19.1" autosave="0">
	<!-- ... -->
	<screen>
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
						<xy y="%100" dy="-20"/>UNIGINE_COPYRIGHT
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


The following parameters are available:


| width | Width of the boot screen window, in pixels. |
|---|---|
| height | Height of the boot screen window, in pixels. |
| background_color | Background color defined by a vector of four numbers in the **[0; 1]** range. |
| texture | Path to the boot screen [texture](../../../code/gui/skin/index.md#splash). |
| transform | Transformation of the boot screen texture defined by a vector of four numbers in the **[0; 1]** range: 1. Texture size multiplier. 2. Window size multiplier. 3. Horizontal position in the [0.0, 1.0] range. 4. Vertical position in the [0.0, 1.0] range. |
| threshold | Threshold for blending based on the alpha-channel. |
| font | Path to the font for text rendering. |
| text | Text of the boot screen. Can be either a plain or [rich text](../../../code/gui/ui/index.md#rich_text). A number of aliases is provided: - UNIGINE_COPYRIGHT — the UNIGINE copyright text. - UNIGINE_VERSION — the current UNIGINE version. - LOADING_PROGRESS — the loading progress going from 0 to 100. > **Notice:** Rich text should be enclosed in <![CDATA[]]> section. |
| messages | Custom names for the corresponding initialization stages. Can be either a plain or [rich text](../../../code/gui/ui/index.md#rich_text), for example: ```xml <engine_init> <![CDATA[ <p> <font color="#c0c6cb" size="18"> <xy x="130" y="414"/>Initializing Engine... </font> </p> ]]> </engine_init> ``` - *engine_init* — engine initialization. - *file_system_init* — file system initialization. - *materials_init* — materials initialization. - *materials_preloading* — pre-loading of materials. - *properties_init* — properties initialization. - *static_meshes_init* — initialization of static meshes. - *shaders_compilation* — shaders compilation. |


> **Notice:** Please note that if the application window is out of focus the further executon will stop, unless the [*background_update*](../../../code/console/index.md#background_update) feature in the `default.boot` [configuration file](../../../code/configuration_file_cpp.md) is enabled to engage the engine execute always regardless of whether the application window is focused or in the background.


## Splash Screen


![](splash_screen.png)

*The splash screen.*


The Splash screen demonstrates UNIGINE logo animation. It is enabled only in *Release* engine binaries and omitted for *Debug* and *Development* binaries to make the development process more solid.

> **Notice:** The Splash screen can be skipped in ***Community Pro***, ***Engineering*** and ***Sim*** SDK editions. To do that, simply set the *splash_screen* parameter of the `default.boot` [configuration file](../../../code/configuration_file_cpp.md) to 0.


## Loading Screen


![](loading_screen.png)

*The Loading screen.*


Loading screens serve for other purposes, such as world loading, shaders compilation or custom loading logic. The look of loading screens is controlled by the [LoadingScreen](../../../api/library/engine/class.loadingscreen_cpp.md) class.
