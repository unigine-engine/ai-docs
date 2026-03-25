# VideoSourceComponent


**VideoSourceComponent** is a [property](../../../../principles/properties/index.md) that provides a no-code way to add video playback to objects in the UNIGINE Editor. It automatically loads media, applies the video texture to a specified surface, and manages the player lifecycle.


> **Notice:** This property is automatically added when the plugin is loaded. Once the plugin is active, **VideoSourceComponent** becomes available in the Editor and can be added to any object in your scene.


The property supports two modes of operation:


- **Unique mode** (unique = true): The component creates its own media player instance and loads media from a file or URL.
- **Shared mode** (unique = false): The component reuses a texture from another VideoSourceComponent, allowing multiple objects to display the same video, optimizing performance and removing additional decoding overhead.


To use the component:


1. Add the component to an Object (e.g., a plane [ObjectMeshStatic](../../../../api/library/objects/class.objectmeshstatic_cpp.md)).
2. Set *surface_name* to the name of the surface where the video should be displayed.
3. Set *texture_name* to the material texture slot name (e.g., *"albedo"*).
4. Configure the media source (file path or URL) and playback options.


### Component Parameters


| Parameter | Type | Default | Description |
|---|---|---|---|
| unique | bool | true | Component mode. If true, creates its own media player. If false, reuses texture from specified *source* parameter. |
| file | bool | true | Media source type. If true, loads from *file_path*. If false, loads from *url*. |
| file_path | String | "" | Path to a local media file. Used when *file = true*. |
| url | String | "" | URL for network media stream (*http://*, *https://*, *rtsp://*, and other protocols supported by [libVLC](https://wiki.videolan.org/Documentation:Streaming_HowTo_New/#Streaming)). Used when *file = false*. |
| sound | bool | false | Enables audio playback. |
| start_from | float | 0.0 | Initial playback position in range [0.0; 1.0]. |
| rate | float | 1.0 | Playback speed multiplier. |
| loop | bool | false | Enables looping playback. |
| texture_filter | int | 0 | Texture filtering mode: [POINT](../../../../api/library/rendering/class.texture_cpp.md#SAMPLER_FILTER_POINT), [LINEAR](../../../../api/library/rendering/class.texture_cpp.md#SAMPLER_FILTER_LINEAR), [BILINEAR](../../../../api/library/rendering/class.texture_cpp.md#SAMPLER_FILTER_BILINEAR), [TRILINEAR](../../../../api/library/rendering/class.texture_cpp.md#SAMPLER_FILTER_TRILINEAR). |
| source | Node | null | Reference to node with **VideoSourceComponent** to share texture (shared mode only). |
| surface_name | String | "" | Name of the object surface for video texture. |
| texture_name | String | "" | Material texture slot name (e.g., "albedo"). |


### See Also


- **[MediaPlayer::Manager](../../../../api/library/plugins/mediaplayer/class.mediaplayer_manager_cpp.md)**
- **[MediaPlayer::VideoSource](../../../../api/library/plugins/mediaplayer/class.mediaplayer_videosource_cpp.md)**
