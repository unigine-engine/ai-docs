# Unigine::WidgetSpriteVideo Class (CS)

**Inherits from:** WidgetSprite


This class is used to create a virtual monitor that plays a video file (currently only *.OGV files are supported). It can be synchrozied with playback of the ambient sound or the directional sound source.


The following example illustrates how to play a video-file on the system GUI or a [GUI object](../../../api/library/objects/class.objectgui_cs.md) using the *WidgetSpriteVideo* class.


[Create a new C# component](../../../principles/component_system/component_system_cs/index.md#create) named `VideoSprite` and copy the code below:


<details>
<summary>VideoSprite.cs | Close</summary>

```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class VideoSprite : Component
{
	// path to the video file to play (only *.OGV type is supported)
	[ParameterFile(Filter =(".ogv"))]
	public String file_name;

	// sprite video widgets
	WidgetSpriteVideo TVscreen;
	WidgetSpriteVideo MAINscreen;

	private void Init()
	{
		// creating the first sprite video widget that plays a file_name video file on the system GUI
		MAINscreen = new WidgetSpriteVideo(Gui.GetCurrent(), file_name, 1);

		// setting size and position of the second sprite video widget on the screen
		MAINscreen.SetPosition(100, 100);
		MAINscreen.Width = 400;
		MAINscreen.Height = 225;
		MAINscreen.Arrange();

		// adding the sprite video widge to the system GUI
		Gui.GetCurrent().AddChild(MAINscreen, Gui.ALIGN_OVERLAP | Gui.ALIGN_BACKGROUND);

		// setting looped playback mode
		MAINscreen.Loop = 1;

		// launching playback
		MAINscreen.Play();

		// checking if the node to which the component is assigned is a GUI Object
		if(node.Type != Node.TYPE.OBJECT_GUI)
		{
			Log.Message("Node is not a GUI Object!\n");
			return;
		}
		ObjectGui GUIObject = node as ObjectGui;

		// creating the second sprite video widget that plays a file_name video file on the GUI object
		TVscreen = new WidgetSpriteVideo(GUIObject.GetGui(), file_name, 1);

		// adjusting the size of the widget to fit the size of the GUI object
		TVscreen.Width = GUIObject.ScreenWidth;
		TVscreen.Height = GUIObject.ScreenHeight;

		// adding the sprite video widget to the GUI object
		GUIObject.GetGui().AddChild(TVscreen, Gui.ALIGN_OVERLAP | Gui.ALIGN_BACKGROUND);

		// setting looped playback mode
		TVscreen.Loop = 1;

		// launching playback
		TVscreen.Play();
	}

	private void Update()
	{
		// write here code to be called before updating each render frame

	}
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

### Properties

## 🔒︎ bool IsStopped

The value indicating if the video is stopped at the moment.
## 🔒︎ bool IsPlaying

The value indicating if the video is being played at the moment.
## AmbientSource AmbientSource

The ambient sound source according to which video playback is synchronized.
## SoundSource SoundSource

The sound source according to which video playback is synchronized.
## float VideoTime

The time of the currently played frame, in seconds. Setting this value rewinds or fast-forwards the video to a given time.
## int YUV

The flag for YUV conversion.
## int Loop

The value indicating if the video is looped.
### Members

---

## WidgetSpriteVideo ( Gui gui , string name = 0 , int mode = 1 )

Constructor. Creates a new sprite that plays video and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - [GUI](../../../api/library/gui/class.gui_cs.md), to which the new sprite will belong.
- *string* **name** - Path to a video file.
- *int* **mode** - YUV flag: **1** if conversion to RGB should be performed by the GPU, **0** - if by the CPU.

## WidgetSpriteVideo ( string name = 0 , int mode = 1 )

Constructor. Creates a new sprite that plays video and adds it to the Engine GUI.
### Arguments

- *string* **name** - Path to a video file.
- *int* **mode** - YUV flag: **1** if conversion to RGB should be performed by the GPU, **0** - if by the CPU.

## void Play ( )

Starts playing video.
## void Stop ( )

Stops playing video. This function saves the playback position so that playing of the file can be resumed from the same point.
