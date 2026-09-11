# MediaPlayer Plugin (CS)

       Sorry, your browser does not support embedded videos.
**MediaPlayer** is a UNIGINE plugin that enables in-game playback of video content using the *[libVLC](https://images.videolan.org/vlc/libvlc.html)* library. The plugin supports video formats compatible with VLC Media Player, including local files and network streams. The plugin works by **rendering video frames into a texture** that can be set to desired texture slots of materials (albedo, emission, etc.), applied to object surfaces in your UNIGINE 3D scenes. When using the programmatic approach (managing the process via *[API](../../../api/library/plugins/mediaplayer/index.md)* manually at runtime), you can use textures produced by the Media Player virtually anywhere a normal texture can be used (in sprites, decal projections, etc.).


> **Warning:** The *MediaPlayer* plugin offers a limited *libVLC* functionality out of the box. Check the [Functionality](#functionality) section for more details.


![](mediaPlayer_plugin.jpg)


## Use Cases


This plugin is suitable for a wide range of applications:


- In-game TV screens and monitors
- Billboards and information panels
- 3D simulations of surveillance camera monitors and control rooms
- In-vehicle dashboards and HMI systems
- Industrial or training simulators where live or prerecorded video needs to be integrated into the scene
- Conference setups, virtual presentations, and educational or training applications where video content is displayed as part of a 3D environment


## Using MediaPlayer Plugin


Playback can be configured right in UnigineEditor via the ***VideoSourceComponent*** property assigned to the target object. It can be used to control video source type, switching audio on and off, setting the start position, playback speed, and looping - **without writing code**. Using this information, the component automatically loads video content, applies the video texture to a specified surface, and manages the player lifecycle.


***VideoSourceComponent*** supports **two modes** of operation:


- **Unique** - the video content is loaded directly from a file or URL.
- **Shared** (*Unique* mode disabled) - the component reuses a texture from another *VideoSourceComponent*, allowing multiple objects in the scene to display the same video, optimizing performance and removing additional decoding overhead.


![](modes.png)

*VideoSourceComponent property in Unique mode (on the left) and Shared mode (on the right)*


In the picture below, *Monitor_1* (left) uses the *VideoSourceComponent* in ***Unique*** mode, receiving video content on *Surface_1* directly from the video content source. *Monitor_2* (right) uses the same component in ***Shared*** mode, reusing *Monitor_1*'s texture on its own *Surface_2*.


[![](scheme_sm.png)](scheme.png)


### Launching MediaPlayer Plugin


> **Warning:** MediaPlayer is an Engine plugin designed for runtime use. It is **not intended for playback within the Editor**, as this may lead to unexpected behavior or system instability.


To use MediaPlayer plugin at runtime, specify the `extern_plugin` command line option on the application start-up:


```bash
main_x64d -extern_plugin "UnigineMediaPlayer"
```


Alternatively use the `plugin_loadUnigineMediaPlayer` console command at runtime.


### VideoSourceComponent Property Parameters


![](prop_param.png)

*Property parameter UI changes based on the selected mode (Unique/Shared) and file type (local/URL), revealing relevant input fields for each configuration.*


| Parameter | Description |
|---|---|
| **Unique** | Component mode. - If **enabled**, the object becomes the main video player, directly receiving video content from VLC. - If **disabled**, the object reuses the texture from the specified *[Source](#source)* parameter. |
| **Source** | Specifies the reference object with the *VideoSourceComponent* property assigned, whose texture (VLC-generated) will be reused. Available only when *[Unique](#unique)* is disabled (*Shared* mode). |
| **File** | Selects the video content source type: - If **enabled**, activates the *[File Path](#file_path)* field to specify a local video file. - If **disabled**, activates the *[URL](#url)* address field. |
| **File Path** | Path to a local video file. Available only when *[File](#file)* is enabled. |
| **URL** | Network or stream address (*http://, https://, rtsp://, file:///*). Available only when *[File](#file)* is disabled. > **Notice:** The MediaPlayer plugin handles streaming using its own protocols and formats. Refer to *[VLC documentation](https://wiki.videolan.org/Documentation:Streaming_HowTo_New/#Streaming)* for supported streaming methods and URL formats. > > > <details> > <summary>Common VLC URL examples</summary> > > - **HTTP Stream** (from another VLC instance) > >   - `http://192.168.1.100:8080` >   - `http://localhost:8080/` (if playing on the same machine) > - **RTSP** (IP Cameras/Security Feeds) > >   - `rtsp://192.168.1.200:554/live` (no login) >   - `rtsp://admin:password@192.168.1.200:554/stream` (with credentials) > - **IPTV / M3U Playlists** > >   - `http://example.com/path/to/playlist.m3u` (direct file URL) >   - `http://example.com/path/to/stream.m3u8` (HLS stream) > - **Local Files / Network Shares** > >   - `file:///C:/Users/YourName/Videos/movie.mp4` (local file) >   - `smb://server/share/video.mp4` (network share) > > </details> |
| **Sound** | Enables/disables audio playback. |
| **Start From** | Playback start position. 0.0 is the start of the video, 1.0 is the end. |
| **Rate** | Playback speed. 1.0 - normal speed (default). Values between 0.0 and 1.0 decrese speed, above 1 increase it. |
| **Loop** | If **enabled**, the video plays repeatedly from start to finish. |
| **Texture Filter** | Preferred texture filtering mode: - [POINT](../../../api/library/rendering/class.texture_cs.md#SAMPLER_FILTER_POINT) - [LINEAR](../../../api/library/rendering/class.texture_cs.md#SAMPLER_FILTER_LINEAR) - [BILINEAR](../../../api/library/rendering/class.texture_cs.md#SAMPLER_FILTER_BILINEAR) - [TRILINEAR](../../../api/library/rendering/class.texture_cs.md#SAMPLER_FILTER_TRILINEAR) |
| **Target Surface Name** | Name of the target object surface **as defined on the object** where the video content material will be applied. |
| **Texture Slot** | Name of the **existing material texture slot** (e.g., albedo) where the video texture will be applied at runtime. |


### Using MediaPlayer Playback


#### Add Plugin to Your Project


To use the plugin **in an existing project**, in the SDK Browser, click the three dots icon next to the project's name.


![](../../../sdk/projects/other_actions.png)


Select *[Configure](../../../sdk/projects/index_cs.md#configure) -> Plugins*. Find ***MediaPlayer plugin***, click *Add*, then *Configure Project*.


To use the plugin **in a [new project](../../../sdk/projects/index_cs.md#creation)**, press *Plugins (0)* in the project creation interface. Find ***MediaPlayer plugin*** in the list, click *Add*, then *Create New Project*.


![](add_plugin.png)


Once the plugin is added to your project, the ***VideoSourceComponent*** property will appear in the Editor's *Properties* window.


![](prop.png)


#### Set Up Your Scene


1. Select the target object that will be used for video content playback and click *Add New Component or Property* in the *Parameters* window. Assign the *VideoSourceComponent* property to the object (or multiple objects, if needed).
2. The **first** object with the *VideoSourceComponent* property will likely use the **Unique** (default) mode making it the primary media player, receiving video content directly from the source. For *Unique* objects, you can adjust *[playback settings](#component_param)* such as **Start From**, **Rate**, **Loop**, and **Sound** as required.
3. Specify the object's **Target Surface Name** and the existing material **Texture Slot** (e.g., albedo) where the video will be rendered at runtime. If the object has multiple surfaces, make sure to specify the correct one. ![](target.png) *Right-click on the target surface and texture slot to copy their names.*
4. For any **additional** objects (if any):

  - Choose **Unique** mode to play separate files or for desynchronized playback.
  - Switch to **Shared** mode (*Unique* disabled) to synchronize the same video content across multiple surfaces and avoid duplicate loading. Reference the primary node with the *VideoSourceComponent* property and the *Unique* attribute enabled - simply drag that node into the **Source** field. This copies the video content texture, and all instances will play back in sync, frame-by-frame.


### Logging


The optional `-vlc_log_level` [startup argument](../../../code/command_line.md) sets the logging level for the plugin. The available levels are inherited from libVLC:


| Value | Description | libVLC Option |
|---|---|---|
| 0 | Log output disabled. No messages are printed. | --quiet |
| 1 | Basic logging, including errors and standard messages. | --verbose=0 |
| 2 | Extended logging, including errors, standard messages, and warnings. | --verbose=1 |
| 3 | Full logging, including errors, standard messages, warnings, and debug information. | --verbose=2 |


By default (when the argument is not specified), the logging level depends on the [build configuration](../../../sdk/projects/index_cs.md#engine_build): in *Release* builds logging is disabled, while in *Development* and *Debug* builds the plugin outputs errors and standard messages (level 1).


If the argument is specified, its value always overrides the build-dependent default. Values outside the 0-3 range are clamped to the nearest valid one. The level is applied once, when the plugin initializes libVLC, and cannot be changed at run time.


```bash
-vlc_log_level 2
```


## Accessing Plugin Methods


**MediaPlayer** can also be used through the *[plugin API](../../../api/library/plugins/mediaplayer/index.md)* at runtime offering you even more flexibility. This approach enables you to use textures produced by the Video Source virtually anywhere a normal texture can be used (in sprites, decal projections, etc.), manage multiple sources, and control playback.


The plugin provides two main classes:


- *[Manager](../../../api/library/plugins/mediaplayer/class.mediaplayer_manager_cs.md)*
- *[VideoSource](../../../api/library/plugins/mediaplayer/class.mediaplayer_videosource_cs.md)*


```csharp
VideoSource video_source = Manager.Load(manager.GetFileURL("video.mp4"));
video_source.Play();

// Apply texture to a material
material.SetTexture("albedo", video_source.Texture);

// Control playback
video_source.Volume = 80;
video_source.Loop = true;

// Seek to 50% of the video
video_source.Position = 0.5f;

```


*Loading and controlling video playback via the MediaPlayer plugin API.*


```csharp
//-------------------------------------------------------------
// 1.  Using the VLC-generated texture for a Decal
//-------------------------------------------------------------
// Creating an Orthographic Decal, setting its parameters and position

DecalOrtho decal = new DecalOrtho();
decal.Radius = 10.0f;
decal.Width = 2.0f;
decal.Height = 2.0f;
decal.WorldPosition = new vec3(0.0f, 0.0f, 5.0f);

// Convert a local file path to a file URL to be loaded by the manager
string url =  Unigine.Plugins.MediaPlayer.Manager.GetFileURL("video.mp4");

// Creating a new Video Source and loading the file using the URL
VideoSource video_source = Unigine.Plugins.MediaPlayer.Manager.Load(url);

// Launching the playback
video_source.Play();

// Creating a decal material instance to tweak it
Material material = decal.MaterialInherit;

// Setting the texture produced by the Video Source as an albedo texture
material.SetTexture("albedo", video_source.Texture);

//-------------------------------------------------------------
// 2. Using the same VLC-generated texture for a Sprite Widget
//-------------------------------------------------------------
// Getting the system GUI
Gui gui = Gui.GetCurrent();

// Creating a Sprite widget
WidgetSprite sprite = new WidgetSprite();

// Setting the texture produced by the Video Source to be used by the sprite
sprite.SetRender(video_source.Texture);

// Adding the Sprite widget to the system GUI
gui.AddChild(sprite, Gui.ALIGN_OVERLAP | Gui.ALIGN_FIXED);

```


*Applying a video texture from the MediaPlayer plugin to anOrthographic Decaland aSprite Widget.*


## Functionality


The *MediaPlayer* plugin offers a limited *libVLC* functionality out of the box, supporting the most common video formats and codecs.


- Supported formats: mov, avi, mp4, ogg, webm, wmv, MJPEG, FLV, SWF, F4V, MKV, M4V.
- Supported codecs: MJPEG, H.264, H.265, AV1, VP9


To enable the full range of *libVLC* functionality, including support for all available formats, add the required libraries manually. Copy the following files and folder from `VideoLAN/VLC/` to `<ProjectName>/bin/plugins/Unigine/MediaPlayer`:


- `libvlc.dll`
- `libvlccore.dll`
- `plugins` folder


For more information and library downloads, refer to the [official VideoLAN website](https://www.videolan.org/vlc/).


## License


You may not use the *MediaPlayer* plugin (including as part of a final application), nor permit its use, in combination with Third-Party Components distributed under terms that directly or indirectly require the *MediaPlayer* plugin to be licensed under terms different from those of your license.


In particular, you may not use the *MediaPlayer* plugin in combination with components licensed under:


- the GNU General Public License (GPL)
- the GNU Lesser General Public License (LGPL), except where used solely through dynamic linking to a shared library
- the Creative Commons Attribution-ShareAlike license (CC BY-SA)


For the purposes of this clause, "Third-Party Components" means software (including libraries) and other intellectual property created by third parties.


## See Also


- *MediaPlayer* plugin [classes](../../../api/library/plugins/mediaplayer/index.md)
- Samples in **C# SIM Samples** set:

  -
  -
