# Unigine::Plugins::MediaPlayer::VideoSource Class (CPP)

**Header:** #include <plugins/Unigine/MediaPlayer/UnigineMediaPlayer.h>


**VideoSource** represents a single media playback instance. It provides full control over video playback including play/pause/stop, seeking, volume control, and access to the video texture for rendering in the scene.


VideoSource instances are created via *[MediaPlayer::Manager::load()](../../../../api/library/plugins/mediaplayer/class.mediaplayer_manager_cpp.md#load_cstr_int_VideoSourcePtr)* and must be released using *[MediaPlayer::Manager::unload()](../../../../api/library/plugins/mediaplayer/class.mediaplayer_manager_cpp.md#unload_VideoSourcePtr_void)* when no longer needed.


The video is decoded into an RGBA texture that can be applied to any material in the scene:


```cpp
auto *manager = MediaPlayer::Manager::get();
auto *player = manager->load(manager->getFileURL("video.mp4"));
player->play();

// Apply texture to a material
material->setTexture("albedo", player->getTexture());

// Control playback
player->setVolume(80);
player->setLoop(true);

// Seek to 50% of the video
player->setPosition(0.5f);

```


```cpp
//-------------------------------------------------------------
// 1.  Using the VLC-generated texture for a Decal
//-------------------------------------------------------------
// Creating an Orthographic Decal, setting its parameters and position
Unigine::DecalOrthoPtr decal = Unigine::DecalOrtho::create();
decal->setRadius(10.0f);
decal->setWidth(2.0f);
decal->setHeight(2.0f);
decal->setWorldPosition(Math::Vec3(0.0f, 0.0f, 5.0f));

// Convert a local file path to a file URL to be loaded by the manager
Unigine::String url = Unigine::Plugins::MediaPlayer::Manager::get()->getFileURL("video.mp4");

// Creating a new Video Source and loading the file using the URL
Unigine::Plugins::MediaPlayer::VideoSource* video_source = Unigine::Plugins::MediaPlayer::Manager::get()->load(url);

// Launching the playback
video_source->play();

// Creating a decal material instance to tweak it
Unigine::MaterialPtr material = decal->getMaterialInherit();

// Setting the texture produced by the Video Source as an albedo texture
material->setTexture("albedo", video_source->getTexture());

//-------------------------------------------------------------
// 2. Using the same VLC-generated texture for a Sprite Widget
//-------------------------------------------------------------
// Getting a pointer to the system GUI
GuiPtr gui = Gui::get();

// Creating a Sprite widget
Unigine::WidgetSpritePtr sprite = WidgetSprite::create();

// Setting the texture produced by the Video Source to be used by the sprite
sprite->setRender(video_source->getTexture());

// Adding the Sprite widget to the system GUI
gui->addChild(sprite, Gui::ALIGN_OVERLAP | Gui::ALIGN_FIXED);

```

 Best PracticeFor simpler video playback management, use the ready-made **[VideoSourceComponent](../../../../api/library/plugins/mediaplayer/class.videosourcecomponent_cpp.md)**. It allows you to add video to a scene object without writing code - just specify the file path or URL, select the object surface, and set the texture slot in the material. The component automatically loads the video, applies the texture, and starts playback on initialization.
### See Also


- **[MediaPlayer::Manager](../../../../api/library/plugins/mediaplayer/class.mediaplayer_manager_cpp.md)**
- **[VideoSourceComponent](../../../../api/library/plugins/mediaplayer/class.videosourcecomponent_cpp.md)**


## Unigine::Plugins::MediaPlayer::VideoSource Class

### Members

## bool isValid () const

Returns the current value indicating whether the video source is valid and ready for playback.
### Return value

**true** if the video source is valid and ready for playback; otherwise **false**.
## Ptr < Texture > getTexture () const

Returns the current texture containing the current video frame.
### Return value

Current texture containing the current video frame.
## void setRate ( float rate )

Sets a new playback rate (speed). 1.0 is normal speed, 0.5 is half speed, 2.0 is double speed.
### Arguments

- *float* **rate** - The playback rate.

## float getRate () const

Returns the current playback rate (speed). 1.0 is normal speed, 0.5 is half speed, 2.0 is double speed.
### Return value

Current playback rate.
## void setPosition ( float position )

Sets a new playback position as a fraction of the total duration, in range [0.0; 1.0].
### Arguments

- *float* **position** - The the playback position in range [0.0; 1.0].

## float getPosition () const

Returns the current playback position as a fraction of the total duration, in range [0.0; 1.0].
### Return value

Current the playback position in range [0.0; 1.0].
## void setTime ( long long time )

Sets a new playback time in milliseconds.
### Arguments

- *long long* **time** - The playback time in milliseconds.

## long long getTime () const

Returns the current playback time in milliseconds.
### Return value

Current playback time in milliseconds.
## long long getDuration () const

Returns the total duration of the media in milliseconds.
### Return value

The total duration in milliseconds.
## void setVolume ( int volume )

Sets a new audio volume level in range [0; 100].
### Arguments

- *int* **volume** - The audio volume level in range [0; 100].

## int getVolume () const

Returns the current audio volume level in range [0; 100].
### Return value

Current audio volume level in range [0; 100].
## void setMuted ( bool muted )

Sets a new value indicating whether the audio is muted.
### Arguments

- *bool* **muted** - Set **true** to enable the audio is muted; **false** - to disable it.

## bool isMuted () const

Returns the current value indicating whether the audio is muted.
### Return value

**true** if the audio is muted; otherwise **false**.
## bool isPlaying () const

Returns the current value indicating whether the media is currently playing.
### Return value

**true** if the media is currently playing; otherwise **false**.
## bool isPaused () const

Returns the current value indicating whether the playback is paused.
### Return value

**true** if the playback is paused; otherwise **false**.
## bool isStopped () const

Returns the current value indicating whether the playback is stopped.
### Return value

**true** if the playback is stopped; otherwise **false**.
## bool isEnded () const

Returns the current value indicating whether playback has reached the end.
### Return value

**true** if the playback has reached the end; otherwise **false**.
## void setLoop ( bool loop )

Sets a new value indicating whether looping is enabled.
### Arguments

- *bool* **loop** - Set **true** to enable video looping; **false** - to disable it.

## bool isLoop () const

Returns the current value indicating whether looping is enabled.
### Return value

**true** if video looping is enabled ; otherwise **false**.
## int getWidth () const

Returns the current video width in pixels.
### Return value

Current video width in pixels.
## int getHeight () const

Returns the current video height in pixels.
### Return value

Current video height in pixels.
## float getFPS () const

Returns the current video frame rate in frames per second.
### Return value

Current the video frame rate.
---

## void play ( )

Starts or resumes media playback.
## void pause ( )

Pauses media playback. Use [play()](#play_void) to resume.
## void stop ( )

Stops media playback and resets the playback position to the beginning.
