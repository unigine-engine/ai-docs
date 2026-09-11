# Unigine::WidgetSpriteVideo Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** WidgetSprite


This class is used to create a virtual monitor that plays a video file (currently only *.OGV files are supported). It can be synchrozied with playback of the ambient sound or the directional sound source.


The following example illustrates how to play a video-file on the system GUI or a [GUI object](../../../api/library/objects/class.objectgui_cpp.md) using the *WidgetSpriteVideo* class.


[Create a C++ component](../../../principles/component_system/component_system_cpp/index.md#workflow) named `VideoSprite` and copy the code below to the corresponding files:


<details>
<summary>VideoSprite.h | Close</summary>

```cpp
#pragma once
#include <UnigineComponentSystem.h>
class VideoSprite :
	public Unigine::ComponentBase
{
public:
	COMPONENT_DEFINE(VideoSprite, Unigine::ComponentBase);
	COMPONENT_INIT(init);
	// path to the video file to play (only *.OGV type is supported)
	PROP_PARAM(File, file_name, "");

private:
	// sprite video widgets
	Unigine::WidgetSpriteVideoPtr TVscreen;
	Unigine::WidgetSpriteVideoPtr MAINscreen;
	void init();

};


```

</details>


<details>
<summary>VideoSprite.cpp | Close</summary>

```cpp
#include "VideoSprite.h"
#include <UnigineGui.h>
REGISTER_COMPONENT(VideoSprite);

using namespace Unigine;

void VideoSprite::init()
{
	// creating the first sprite video widget that plays a file_name video file on the system GUI
	MAINscreen = WidgetSpriteVideo::create(Gui::getCurrent(), file_name, 1);

	// setting size and position of the second sprite video widget on the screen
	MAINscreen->setPosition(100, 100);
	MAINscreen->setWidth(400);
	MAINscreen->setHeight(225);
	MAINscreen->arrange();

	// adding the sprite video widge to the system GUI
	Gui::getCurrent()->addChild(MAINscreen, Gui::ALIGN_OVERLAP | Gui::ALIGN_BACKGROUND);

	// setting looped playback mode
	MAINscreen->setLoop(1);

	// launching playback
	MAINscreen->play();

	// checking if the node to which the component is assigned is a GUI Object
	if (node->getType() != Node::OBJECT_GUI)
	{
		Log::message("Node is not a GUI Object!\n");
		return;
	}
	ObjectGuiPtr GUIObject = checked_ptr_cast<ObjectGui>(node);

	// creating the second sprite video widget that plays a file_name video file on the GUI object
	TVscreen = WidgetSpriteVideo::create(GUIObject->getGui(), file_name, 1);

	// adjusting the size of the widget to fit the size of the GUI object
	TVscreen->setWidth(GUIObject->getScreenWidth());
	TVscreen->setHeight(GUIObject->getScreenHeight());

	// adding the sprite video widget to the GUI object
	GUIObject->getGui()->addChild(TVscreen, Gui::ALIGN_OVERLAP | Gui::ALIGN_BACKGROUND);

	// setting looped playback mode
	TVscreen->setLoop(1);

	// launching playback
	TVscreen->play();
}

```

</details>


### See Also


- UnigineScript samples:

  -
  -
  -
  -


## WidgetSpriteVideo Class

### Members

## bool isStopped () const

Returns the current value indicating if the video is stopped at the moment.
### Return value

**true** if the video is stopped at the moment; otherwise **false**.
## bool isPlaying () const

Returns the current value indicating if the video is being played at the moment.
### Return value

**true** if the video is being played at the moment; otherwise **false**.
## void setAmbientSource ( const Ptr < AmbientSource >& source )

Sets a new ambient sound source according to which video playback is synchronized.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[AmbientSource](../../../api/library/sounds/class.ambientsource_cpp.md)>&* **source** - The ambient sound source according to which video playback is synchronized

## Ptr < AmbientSource > getAmbientSource () const

Returns the current ambient sound source according to which video playback is synchronized.
### Return value

Current ambient sound source according to which video playback is synchronized
## void setSoundSource ( const Ptr < SoundSource >& source )

Sets a new sound source according to which video playback is synchronized.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[SoundSource](../../../api/library/sounds/class.soundsource_cpp.md)>&* **source** - The sound source according to which video playback is synchronized

## Ptr < SoundSource > getSoundSource () const

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

## static WidgetSpriteVideoPtr create ( const Ptr < Gui > & gui , const char * name = 0 , int mode = 1 )

Constructor. Creates a new sprite that plays video and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the new sprite will belong.
- *const char ** **name** - Path to a video file.
- *int* **mode** - YUV flag: **1** if conversion to RGB should be performed by the GPU, **0** - if by the CPU.

## static WidgetSpriteVideoPtr create ( const char * name = 0 , int mode = 1 )

Constructor. Creates a new sprite that plays video and adds it to the Engine GUI.
### Arguments

- *const char ** **name** - Path to a video file.
- *int* **mode** - YUV flag: **1** if conversion to RGB should be performed by the GPU, **0** - if by the CPU.

## void play ( )

Starts playing video.
## void stop ( )

Stops playing video. This function saves the playback position so that playing of the file can be resumed from the same point.
