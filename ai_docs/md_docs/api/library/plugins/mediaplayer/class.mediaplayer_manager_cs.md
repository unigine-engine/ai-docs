# Unigine::Plugins::MediaPlayer::Manager Class (CS)

> **Notice:** This class is a singleton.


**Manager** is a singleton class that provides the main interface for the *MediaPlayer* plugin. It manages the lifecycle of video sources and provides utility functions for working with media files.


The plugin uses *libVLC*library to decode video and render frames to GPU textures that can be used in UNIGINE materials.

 Best PracticeFor simpler video playback management, use the ready-made **[VideoSourceComponent](../../../../api/library/plugins/mediaplayer/class.videosourcecomponent_cs.md)**. It allows you to add video to a scene object without writing code - just specify the file path or URL, select the object surface, and set the texture slot in the material. The component automatically loads the video, applies the texture, and starts playback on initialization.
### See Also


- **[MediaPlayer::VideoSource](../../../../api/library/plugins/mediaplayer/class.mediaplayer_videosource_cs.md)**
- **[VideoSourceComponent](../../../../api/library/plugins/mediaplayer/class.videosourcecomponent_cs.md)**


## Unigine::Plugins::MediaPlayer::Manager Class

### Members

---

## string GetFileURL ( string path )

Converts a local file path to a **file:///** URL that can be passed to the *[Load()](../../../...md#load_cstr_int_VideoSourcePtr)* method. The path is resolved to an absolute path using the [UNIGINE File System](../../../../principles/filesystem/index_cs.md).
### Arguments

- *string* **path** - Relative or absolute path to a local media file.

### Return value

File URL in the format `file:///absolute/path/to/file`.
## VideoSource Load ( string URL , int flags = Texture::SAMPLER_FILTER_POINT )

Loads media from the specified URL and creates a new VideoSource instance. The video source must be released using *[Unload()](../../../...md#unload_VideoSourcePtr_void)* when no longer needed.
### Arguments

- *string* **URL** - Media URL. Can be a **file:///** URL (use *[GetFileURL()](../../../...md#getFileURL_cstr_String)* to convert local paths), **http://**, **https://**, **rtsp://**, or any other protocol supported by [libVLC](https://wiki.videolan.org/Documentation:Streaming_HowTo_New/#Streaming). <details> <summary>Common VLC URL examples</summary> - **HTTP Stream** (from another VLC instance) - `http://192.168.1.100:8080` - `http://localhost:8080/` (if playing on the same machine) - **RTSP** (IP Cameras/Security Feeds) - `rtsp://192.168.1.200:554/live` (no login) - `rtsp://admin:password@192.168.1.200:554/stream` (with credentials) - **IPTV / M3U Playlists** - `http://example.com/path/to/playlist.m3u` (direct file URL) - `http://example.com/path/to/stream.m3u8` (HLS stream) - **Local Files / Network Shares** - `file:///C:/Users/YourName/Videos/movie.mp4` (local file) - `smb://server/share/video.mp4` (network share). </details>
- *int* **flags** - Texture sampler flags for the output texture. Default is [SAMPLER_FILTER_POINT](../../../../api/library/rendering/class.texture_cs.md#SAMPLER_FILTER_POINT).

### Return value

Pointer to the created VideoSource instance, or nullptr if loading failed.
## void Unload ( VideoSource file )

Unloads the specified video source and releases all associated resources. After calling this method, the VideoSource pointer becomes invalid and must not be used.
### Arguments

- *VideoSource* **file** - Pointer to the [VideoSource](../../../../api/library/plugins/mediaplayer/class.mediaplayer_videosource_cs.md) instance to unload.
