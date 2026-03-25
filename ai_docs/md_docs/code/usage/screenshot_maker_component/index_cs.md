# Making Screenshots at Runtime (CS)


This article provides the code sufficient to create a screenshot making component configurable via Editor and making screenshots at runtime.


## Component Code


[Create a component](../../../principles/component_system/component_system_cs/index.md#create) in the Editor and insert this code:


<details>
<summary>ScreenshotMaker.cs | close</summary>

```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class ScreenshotMaker : Component
{
	public enum Format
	{
		tga = 0,
		png,
		jpg
	}

	public enum State
	{
		STATE_START = 0,
		STATE_WARMUP,
		STATE_SAVE,
		STATE_DONE,
	};

	[ShowInEditor]
	private string namePrefix = "screenshot";

	[ShowInEditor]
	[ParameterSlider(Min = 1)]
	private int width = 640;

	[ShowInEditor]
	[ParameterSlider(Min = 1)]
	private int height = 480;

	[ShowInEditor]
	private Format format = Format.png;

	[ShowInEditor]
	private bool alphaChannel = false;

	private Texture texture = null;
	private Viewport viewport = null;
	private int count = 0;

	private State state = State.STATE_DONE;
	const int warmup_frames = 30;
	int warm_up_count = 0;

	private void Init()
	{
		texture = new Texture();
		viewport = new Viewport();
		viewport.SkipFlags = Viewport.SKIP_VISUALIZER;

		Unigine.Console.Onscreen = true;
		Unigine.Console.OnscreenMessageLine(vec4.GREEN, "Screenshot component is initialized.");
	}

	private void Update()
	{
		Player player = Game.Player;

		if (player == null)
		{
			state = State.STATE_DONE;
			Unigine.Console.OnscreenMessageLine(vec4.RED, "No active camera.");
			return;
		}

		if (state == State.STATE_DONE && Input.IsKeyDown(Input.KEY.T))
		{
			warm_up_count = 0;
			state = State.STATE_WARMUP;
			Unigine.Console.OnscreenMessageLine(vec4.GREEN, "Trying to take a screenshot...");
		}

		if (state == State.STATE_WARMUP)
		{
			viewport.Mode = Render.ViewportMode;

			if (warm_up_count == 0)
			{
				// First frame we render with velocity buffer turned off to avoid temporal effects artifacts
				viewport.AppendSkipFlags(Viewport.SKIP_VELOCITY_BUFFER);
				viewport.RenderTexture2D(player.Camera, texture, width, height);
				viewport.RemoveSkipFlags(Viewport.SKIP_VELOCITY_BUFFER);
			}
			else
			{
				// We temporarily set exposure adaptation time to 0, otherwise the image may be too dark
				float exposureAdaptation = Render.ExposureAdaptation;
				Render.ExposureAdaptation = 0.0f;
				viewport.RenderTexture2D(player.Camera, texture, width, height);
				Render.ExposureAdaptation = exposureAdaptation;
			}

			warm_up_count++;
			if (warm_up_count == warmup_frames)
				state = State.STATE_SAVE;

			if (state == State.STATE_SAVE)
			{
				Render.AsyncTransferTextureToImage(
					null,
					(Image image) =>
						{
							if (!alphaChannel || format == Format.jpg)
							{
								if (image.Format == Image.FORMAT_RGBA8)
									image.ConvertToFormat(Image.FORMAT_RGB8);
								else if (image.Format == Image.FORMAT_RGBA16F)
									image.ConvertToFormat(Image.FORMAT_RGB16F);
							}

							if (!Render.IsFlipped)
								image.FlipY();

							string fullName = $"{namePrefix}_{count}.{format}";
							image.Save(fullName);
							Unigine.Console.OnscreenMessageLine(vec4.GREEN, $"{fullName} saved.");

						},
				texture);

				count++;
				state = State.STATE_DONE;
			}
		}
	}
}

```

</details>


## Making Screenshots


Now you have a component in your project. To be able to make screenshots, you need to do the following:


1. [Assign](../../../principles/component_system/component_system_cs/index.md#apply) the ScreenshotMaker component to any node in the Editor (or create a *Node Dummy* and assign the component to it). ![Component assigned in the Editor](cs_component.png)
2. Adjust settings as necessary. | Name Prefix | The prefix used in the file name. | |---|---| | Width | Width of the saved screenshot image. | | Height | Height of the saved screenshot image. | | Format | Format of the saved screenshot image. | | Alpha Channel | If enabled, transparent areas are cut off. |
3. Run your app and take screenshots.
4. Check the `data/` folder of your project.
