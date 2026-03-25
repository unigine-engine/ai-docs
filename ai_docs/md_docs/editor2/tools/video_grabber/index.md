# Capturing Screenshots and Frame Sequences


*Video Grabber* is a UnigineEditor tool for high-quality capturing of screenshots and frame sequences. Frame sequences are captured in a special non-real-time mode, allowing to get any fixed FPS even on a low-end hardware. In comparison with traditional CPU-based offline rendering, this tool allows much faster rendering thanks to GPU acceleration.


> **Notice:** To open the Video Grabber tool, choose *Tools -> Video Grabber* in the Menu Bar.
>  To learn how to use the tool, watch [this video tutorial](#video_tutorial).


Video Grabber supports capturing of screenshots with extremely high resolution: 4K or even 8K images can be taken with a regular monitor. Also Video Grabber supports the professional EXR format in addition to the standard TGA, JPG, PNG and PSD formats.


![](video_grabber.png)

*Video Grabber Tool*


The captured screenshots can be processed by a special video utility to make a video file.


## Video Grabber Settings


The *Video Grabber* tool provides the settings described below.


### Mode Settings


![](mode_settings.png)

*Capturing Modes*


| Single shot | Take a single screenshot. |
|---|---|
| Sequence | Take a sequence of screenshots with the specified FPS according to the loaded `*.track` file. |
| FPS | The frame rate of the track animation to grab. This option is available only when the *Sequence* option is set. |
| Track | A path to a `*.track` file. This option is available only when the *Sequence* option is set. |
| Camera | [Camera](../../../editor2/camera_settings/index.md), the viewport of which should be captured. To update the list of available cameras, click ![](default_resolution.png) to the right of the *Camera* field. |
| Warmup | Warm up of the video grabber: the number of frames to skip before capturing the viewport. It is used to reduce visual artifacts. This option is available only when the *Sequence* option is set. |


### Quality Settings


![](quality_settings.png)

*Capturing Quality*


| Resolution | The output resolution. To set the output resolution to the current viewport resolution, click the ![](default_resolution.png) button to the right of the *Resolution* field. If you specify very high values, a warning may appear. |
|---|---|
| Anti-aliasing | The anti-aliasing mode for the output image: the image is captured with the output resolution multiplied by the specified value (by 2 or 4) and then it is resized to the initial output resolution. |


### Output Files Settings


![](output_settings.png)

*Settings of Output Files*


| Destination | A path to a folder, into which the screenshots will be saved. |
|---|---|
| Format | The output format: - *TGA* - *PNG* - *JPG* - *PSD* - *EXR* - *DDS (8, 10 and 16 bit)* The label under this field displays the bit depth of the chosen format. |
| Background alpha mask | Toggles capturing of the transparent [background](../../../editor2/settings/render_settings/environment/index.md#background_color) of the scene on and off: - If the option is enabled, the transparent background will be captured. - If the option is disabled, the background will be captured regardless of its transparency. > **Notice:** The option is available for all output formats except *JPG*. |


## Grabbing Viewport


To capture a screenshot with the Video Grabber tool:


1. On the Menu Bar, choose *Windows -> Video Grabber*. ![](open_grabber.png) The Video Grabber tool window will open.
2. Choose the [mode](#mode_options) of the viewport capture, choose the [camera](#camera) that will be used for capturing, specify the required [quality](#quality_options) and [output](#output_options) settings.
3. Press **Grab**.


## Video Tutorial


Watch the video below to learn how to capture video with the Video Grabber.


## See Also


- The *[ScreenshotMaker](../../../code/usage/screenshot_maker_component/index_cpp.md)* component for making snapshots at runtime with the possibility to remove Alpha channel
