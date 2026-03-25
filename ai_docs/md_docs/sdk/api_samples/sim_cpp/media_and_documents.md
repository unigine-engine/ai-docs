# Media & Documents

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


## MediaPlayer: Video to Texture

This sample demonstrates a simple no-code approach of integrating video playback directly into a 3D scene using the **[UnigineMediaPlayer](../../../code/plugins/mediaplayer/index.md)** plugin via the *VideoSourceComponent*. The plugin uses the functionality of the *[libVLC](https://wiki.videolan.org/Documentation:Streaming_HowTo_New/#Streaming)* library to render video frames into a texture that can be assigned to various texture slots (albedo, emission, etc.) of materials applied to object surfaces in your UNIGINE 3D scenes. Textures rendered by the plugin can also be used in sprites, decal projections, etc (see the programming approach showcased in the **Video To Widget** sample).


Using the ready-made ***VideoSourceComponent*** allows applying video content to object surfaces and configuring playback (video source type, toggling audio, setting the start position, playback speed, and looping) right in UnigineEditor - without writing code. The component automatically loads video content, applies the video texture to a specified surface, and starts playback on initialization.


***VideoSourceComponent*** supports two modes of operation:


- **Unique** - video content is loaded directly from a file or URL and decoded.
- **Shared** - the component reuses a ready-to-use texture from another *VideoSourceComponent* (already processed), allowing multiple objects to display the same video optimizing performance.


The scene features nine *Plane* objects, each playing a specific video format (`AVI, MOV, MP4, OGG, WEBM, WMV`) and streaming sources (`HTTP` camera feed), with the component working in the *Unique* mode, and two monitors in the *Shared* mode duplicating video content from selected panels.


**Use Cases:**


- In-game TV screens and monitors
- Billboards and information panels
- 3D simulations of surveillance camera monitors and control rooms
- In-vehicle dashboards and HMI systems
- Industrial or training simulators where live or prerecorded video needs to be integrated into the scene
- Conference setups, virtual presentations, and educational or training applications where video content is displayed as part of a 3D environment.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/media_and_documents/media_player_video_to_texture*
## MediaPlayer: Video to Widget

This sample demonstrates how to integrate video playback into a 3D application using the **[UnigineMediaPlayer](../../../code/plugins/mediaplayer/index.md)** plugin. It supports loading content from both local video files and streaming URLs. The plugin works by rendering video frames into a texture that can be set to desired texture slots of materials (albedo, emission, etc.) and applied to object surfaces in your UNIGINE 3D scenes, or used in sprites, decal projections, etc.


In this sample, the video texture is rendered onto a *[WidgetSprite](../../../api/library/gui/class.widgetsprite_cpp.md)* to create a media player, including a video display, timeline with current/remaining time, play/pause/stop controls, volume and playback speed adjustment, preset speed buttons, and a loop toggle using the ***UnigineMediaPlayer*** plugin's API.


The plugin supports common video formats playable by VLC, such as `MP4, AVI, MKV, MOV`, and various streaming protocols available for use with *[libVLC](https://wiki.videolan.org/Documentation:Streaming_HowTo_New/#Streaming)* (`file:///, http://, https://, rtsp://`).


**Use Cases:**


- In-game TV screens and monitors
- Billboards and information panels
- 3D simulations of surveillance camera monitors and control rooms
- In-vehicle dashboards and HMI systems
- Industrial or training simulators where live or prerecorded video needs to be integrated into the scene
- Conference setups, virtual presentations, and educational or training applications where video content is displayed as part of a 3D environment.


In the *Parameters* section, enter a network stream or online video URL to the ***Open URL*** field and click ***Open*** to load the video into the player interface, or use ***Select File*** field to select a local video file (the file is loaded automatically after selection). After loading, press the ***Play*** button in the Media Player UI to start playback.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/media_and_documents/media_player_video_to_widget*
## PDFRender: Single Page Rendering

This sample demonstrates rendering PDF files using the [*PDFRender* plugin](../../../code/plugins/pdfrender/index.md) with extended control over output parameters. In this sample, you can load any PDF document at runtime and render its pages with custom resolution and quality settings.


- Specify the *Render size* values (use custom or the default page dimensions).
- Adjust *render flags* to control text and image output.
- Click *Render Page* to display the current page.
- Use the *Page* selector to navigate through the document.


Resources are automatically released on *Shutdown()*.


**Available render flags:**


- **Render Annotations**: show annotations
- **Render LCD Text**: optimize text for LCD displays
- **Render No Native Text**: disable native text rendering
- **Render Grayscale**: render the output in grayscale
- **Render No Smooth Text**: disable text antialiasing
- **Render No Smooth Image**: disable image antialiasing
- **Render No Smooth Path**: disable vector path antialiasing.


**Use Cases:**


- In-game documentation
- Virtual presentations
- Online meetings
- Educational or training apps.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/media_and_documents/pdfrender_single_page_rendering*
## PDFRender: Viewer Widget

This sample demonstrates PDF rendering inside a custom widget using the [*PDFRender* plugin](../../../code/plugins/pdfrender/index.md). This sample allows you to:


- Load any PDF document at runtime directly from your storage (no pre-import required).
- Scroll through pages inside the widget - pages are dynamically loaded and unloaded based on scroll position.
- Configure the grid layout by setting the number of pages displayed side-by-side (*Num Columns*).
- Adjust zoom level (*Scale*) and spacing between pages (*Space X, Space Y*).


**Use Cases**:


- In-game documentation
- Virtual presentations
- Online meetings
- Educational or training apps.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/media_and_documents/pdfrender_viewer_widget*
