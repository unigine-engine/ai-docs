# Unigine::Plugins::MediaPlayer::VideoSource Class (CS)


**VideoSource** represents a single media playback instance. It provides full control over video playback including play/pause/stop, seeking, volume control, and access to the video texture for rendering in the scene.


VideoSource instances are created via *[MediaPlayer.Manager.Load()](../../../../api/library/plugins/mediaplayer/class.mediaplayer_manager_cs.md#load_cstr_int_VideoSourcePtr)* and must be released using *[MediaPlayer.Manager.Unload()](../../../../api/library/plugins/mediaplayer/class.mediaplayer_manager_cs.md#unload_VideoSourcePtr_void)* when no longer needed.


The video is decoded into an RGBA texture that can be applied to any material in the scene:


```csharp
VideoSource player = Manager.Load(manager.GetFileURL("video.mp4"));
player.Play();

// Apply texture to a material
material.SetTexture("albedo", player.Texture);

// Control playback
player.Volume = 80;
player.Loop = true;

// Seek to 50% of the video
player.Position = 0.5f;

```


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

 Best PracticeFor simpler video playback management, use the ready-made **[VideoSourceComponent](../../../../api/library/plugins/mediaplayer/class.videosourcecomponent_cs.md)**. It allows you to add video to a scene object without writing code - just specify the file path or URL, select the object surface, and set the texture slot in the material. The component automatically loads the video, applies the texture, and starts playback on initialization.
### See Also


- **[MediaPlayer::Manager](../../../../api/library/plugins/mediaplayer/class.mediaplayer_manager_cs.md)**
- **[VideoSourceComponent](../../../../api/library/plugins/mediaplayer/class.videosourcecomponent_cs.md)**


## Unigine::Plugins::MediaPlayer::VideoSource Class

### Properties

## 🔒︎ bool Valid

The value indicating whether the video source is valid and ready for playback.
## 🔒︎ Texture Texture

The texture containing the current video frame.
## float Rate

The playback rate (speed). 1.0 is normal speed, 0.5 is half speed, 2.0 is double speed.
## float Position

The playback position as a fraction of the total duration, in range [0.0; 1.0].
## long Time

The playback time in milliseconds.
## 🔒︎ long long Duration

The Returns the total duration of the media in milliseconds.
## int Volume

The audio volume level in range [0; 100].
## bool Muted

The value indicating whether the audio is muted.
## 🔒︎ bool IsPlaying

The value indicating whether the media is currently playing.
## 🔒︎ bool IsPaused

The value indicating whether the playback is paused.
## 🔒︎ bool IsStopped

The value indicating whether the playback is stopped.
## 🔒︎ bool IsEnded

The value indicating whether playback has reached the end.
## bool Loop

The value indicating whether looping is enabled.
## 🔒︎ int Width

The video width in pixels.
## 🔒︎ int Height

The video height in pixels.
## 🔒︎ float FPS

The video frame rate in frames per second.
### Members

---

## void Play ( )

Starts or resumes media playback.
## void Pause ( )

Pauses media playback. Use [play()](#play_void) to resume.
## void Stop ( )

Stops media playback and resets the playback position to the beginning.
