# Unigine::WidgetSpriteVideo Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** WidgetSprite


This class is used to create a virtual monitor that plays a video file (currently only *.OGV files are supported). It can be synchrozied with playback of the ambient sound or the directional sound source.


You can replace the current video file with another one in run-time by using one of the following methods:

- Delete the WidgetSpriteVideo node from the node hierarchy, delete the instance of the WidgetSpriteVideo and create a new instance of the WidgetSpriteVideo in the same place, but with the different path to the required video file. Then, add the new instance to the node hierarchy. > **Notice:** There can be a small pause between deletion of the old widget and creation of a new one. The following example demonstrates implementation of the described method: ```cpp #include <core/unigine.h> /* */ Gui gui; WidgetSpriteVideo sprite_video; /* */ void create_video(string file) { // create an instance of the WidgetSpriteVideo to play a given video file sprite_video = new WidgetSpriteVideo(gui,file); // add the created node to the node hierarchy gui.addChild(sprite_video,GUI_ALIGN_OVERLAP); sprite_video.setLoop(1); sprite_video.play(); } /* */ void destroy_video() { // delete the node from the node hierarchy gui.removeChild(sprite_video); // delete the instance of the WidgetSpriteVideo delete sprite_video; sprite_video = NULL; } /* */ int init() { gui = engine.getGui(); create_video("samples/widgets/videos/unigine.ogv"); thread("update_scene"); return 1; } /* */ void update_scene() { while(true) { sleep(1); // delete the video destroy_video(); // create a new video create_video("samples/widgets/videos/winter.ogv"); } } ```
- Create a new instance of the WidgetSpriteVideo on the background and disable (and then delete) the old instance of the WidgetSpriteVideo.


### See Also


- UnigineScript samples:

  -
  -
  -
  -


## WidgetSpriteVideo Class

### Members

## int isStopped () const

Returns the current value indicating if the video is stopped at the moment.
### Return value

Current the video is stopped at the moment
## int isPlaying () const

Returns the current value indicating if the video is being played at the moment.
### Return value

Current the video is being played at the moment
## void setAmbientSource ( AmbientSource source )

Sets a new ambient sound source according to which video playback is synchronized.
### Arguments

- *[AmbientSource](../../../api/library/sounds/class.ambientsource_usc.md)* **source** - The ambient sound source according to which video playback is synchronized

## AmbientSource getAmbientSource () const

Returns the current ambient sound source according to which video playback is synchronized.
### Return value

Current ambient sound source according to which video playback is synchronized
## void setSoundSource ( SoundSource source )

Sets a new sound source according to which video playback is synchronized.
### Arguments

- *[SoundSource](../../../api/library/sounds/class.soundsource_usc.md)* **source** - The sound source according to which video playback is synchronized

## SoundSource getSoundSource () const

Returns the current sound source according to which video playback is synchronized.
### Return value

Current sound source according to which video playback is synchronized
## void setVideoTime ( float time )

Sets a new time of the currently played frame, in seconds. Setting this value rewinds or fast-forwards the video to a given time.
### Arguments

- *float* **time** - The time of the currently played frame

## float getVideoTime () const

Returns the current time of the currently played frame, in seconds. Setting this value rewinds or fast-forwards the video to a given time.
### Return value

Current time of the currently played frame
## void setYUV ( int yuv )

Sets a new flag for YUV conversion.
### Arguments

- *int* **yuv** - The flag for YUV conversion

## int getYUV () const

Returns the current flag for YUV conversion.
### Return value

Current flag for YUV conversion
## void setLoop ( int loop )

Sets a new value indicating if the video is looped.
### Arguments

- *int* **loop** - The flag indicating whether the video is looped

## int getLoop () const

Returns the current value indicating if the video is looped.
### Return value

Current flag indicating whether the video is looped
---

## static WidgetSpriteVideo ( Gui gui , string name = 0 , int mode = 1 )

Constructor. Creates a new sprite that plays video and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - [GUI](../../../api/library/gui/class.gui_usc.md), to which the new sprite will belong.
- *string* **name** - Path to a video file.
- *int* **mode** - YUV flag: **1** if conversion to RGB should be performed by the GPU, **0** - if by the CPU.

## static WidgetSpriteVideo ( string name = 0 , int mode = 1 )

Constructor. Creates a new sprite that plays video and adds it to the Engine GUI.
### Arguments

- *string* **name** - Path to a video file.
- *int* **mode** - YUV flag: **1** if conversion to RGB should be performed by the GPU, **0** - if by the CPU.

## void play ( )

Starts playing video.
## void stop ( )

Stops playing video. This function saves the playback position so that playing of the file can be resumed from the same point.
