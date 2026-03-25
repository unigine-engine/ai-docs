# Temporal Anti-Aliasing (TAA)


**Temporal anti-aliasing** (also known as **TAA**) is an anti-aliasing technique to reduce temporal aliasing (flickering or shimmering effects). This technique can be combined with [FXAA](../../../principles/render/antialiasing/fxaa.md) for better quality.


| [![](space_taa_off_sm.png)](space_taa_off.png) | [![](space_taa_on_sm.png)](space_taa_on.png) |
|---|---|
| *ISS without TAA.* | *ISS with TAA.* |


## TAA Features


Unlike **Multisample anti-aliasing** (MSAA) that performs anti-aliasing only on edges of polygons (and makes this edges smoother), Temporal anti-aliasing applies smoothing to the whole scene. In case of full deferred rendering (when the final image is composed of different texture buffers: depth, normal, etc.), MSAA will increase performance costs, because Multisample anti-aliasing should be applied to each texture buffer.


### How TAA works


The main concept of temporal anti-aliasing is to use a subpixel jitter of scene camera every frame and then combine all this frames into the final image. So, it will take time to get a smoothed picture (for example, 5-7 frames), but with the frequency of 60 frames per second it will look seamlessly.


![](camera_jitter.png)

*Simplified demonstration of the TAA camera jitter.*


During rasterization process, there is a test whether the object will get into pixel or not. And the object will not be rendered if it doesn't occupy a major part of a pixel.


![](1.png)

*Vector image before rasterization.*


And here we can get an error, when we have a sphere object before rasterization and get a square object after, because some parts of the sphere don't occupy enough pixel space.


![](2.png)

*Bitmap image after rasterization without TAA.*


Not a very good rendering, right? And temporal anti-aliasing solves this problem, because camera will have a subpixel jitter, and each part of this sphere at least once will be rendered in a frame. And after combining these frames, we will get a true sphere, not a square! Voila!


![](3.png)

*Bitmap image after rasterization with TAA.*


### Ghosting


This anti-aliasing technique works perfectly for static scenes (without any moving objects). But when objects are moving, frames will significantly differ one from another and we will see a trail of "ghosts" of the moving object. This effect is called **ghosting**.


To get rid of ghosting, there is a **velocity buffer**. Velocity buffer stores information about transformations of objects. Due to this buffer, the engine knows about the object transformation and doesn't render the "ghosts" of the moving object. Also, the engine checks the color intensity of the pixel, because of camera jitter.


### Summary


TAA has a wide scope of usage, because it improves whole image (not only the edges of the geometry, like MSAA) including geometry, shadows, etc. It greatly reduces all the problems, and does not cut the performance down, working well with both static and dynamic images. However, keep in mind that the key factor of good TAA performance is [optimized content](../../../content/optimization/index.md) of the scene: the higher FPS is, the faster temporal anti-aliasing smooths the scene. In addition to this, UNIGINE allows you to choose the type of anti-aliasing: **TAA** or **[FXAA](../../../principles/render/antialiasing/fxaa.md)**, or combine them both for better image quality (FXAA is applied before temporal summing).


## TAA Adjustment


Temporal Anti-Aliasing (TAA) settings are available for adjustment via the *Render -> Antialiasing* section of the *Settings* window, along with [SRAA](../../../principles/render/antialiasing/sraa.md), [Fast approXimate Anti-Aliasing (FXAA)](../../../principles/render/antialiasing/fxaa.md) and [Supersampling](../../../principles/render/antialiasing/supersampling.md) settings. The following settings are available when the [Custom](../../../principles/render/antialiasing/index.md#aa_custom) preset for Anti-Aliasing is selected.


![TAA Settings](taa_preset.png)

*Anti-Aliasing Settings*


| TAA | The value indicating if [TAA (Temporal Anti-Aliasing)](../../../principles/render/antialiasing/taa.md) is enabled. **enabled** by default. `Console access:render_taa` ([API control](../../../api/library/rendering/class.render_cpp.md#render_taa)) |
|---|---|
| Preset | The index of the AA (Anti-Aliasing) preset used at the moment. To customize Anti-Aliasing options at run time you should activate the **Custom** preset: One of the following values: - Sharpest (by default) - Sharp - Smooth - Smooth + SRAA - Smoothest - Smoothest + SRAA - VR Mode - Custom `Console access:render_aa_preset` ([API control](../../../api/library/rendering/class.render_cpp.md#render_aa_preset)) |


### Customizable Settings


The following settings are available when the [Custom](#taa_preset) preset is selected.


![TAA custom settings](taa.png)

*TAA Settings*


| Fix Flicker | The value indicating if the taa [fix flicker](../../../principles/render/antialiasing/taa.md#taa_fix_flicker) option is enabled. This option fixes flickering edges caused by TAA: it removes bright pixels by using the pixel brightness information from the previous frame. It is recommended to enable the option for bright thin ropes, wires and lines. The option is available only when TAA is enabled. > **Notice:** Enabling this option may increase performance costs. **enabled** by default. `Console access:render_taa_fix_flicker` ([API control](../../../api/library/rendering/class.render_cpp.md#render_taa_fix_flicker)) |
|---|---|
| Frames By Color | The value indicating if TAA [color clamping](../../../principles/render/antialiasing/taa.md#taa_color_clamping) option is enabled. This option clamps the color of the current and previous frame. The image becomes more sharp. TAA must be enabled. **enabled** by default. `Console access:render_taa_frames_by_color` ([API control](../../../api/library/rendering/class.render_cpp.md#render_taa_frames_by_color)) |
| Fix Blur | The value indicating if Catmull-Rom resampling is enabled. This option enables you to reduce image blurring when the camera moves forward/backward. It is recommended to disable resampling fow low-quality presets. **enabled** by default. `Console access:render_taa_catmull_resampling` ([API control](../../../api/library/rendering/class.render_cpp.md#render_taa_catmull_resampling)) ![](taa_fix_blur_off.jpg) ![](taa_fix_blur_on.jpg) |
| Fix Blur Sharpness | The sharpness value for the [Catmull-Rom resampling](#TAACatmullResampling) option. Range of values: **[0.0f, 1.0f]**. The default value is : **0.7f**. `Console access:render_taa_catmull_resampling_sharpness` ([API control](../../../api/library/rendering/class.render_cpp.md#render_taa_catmull_resampling_sharpness)) |
| Antialiasing In Motion | The value indicating if improved anti-aliasing in motion (for moving camera and objects) is enabled. TAA must be enabled. **disabled** by default. `Console access:render_taa_antialiasing_in_motion` ([API control](../../../api/library/rendering/class.render_cpp.md#render_taa_antialiasing_in_motion)) ![Antialiasing In Motion](antialiasing_in_motion.gif) |
| Diagonal Neighbors | The value indicating if diagonally neighboring pixels are to be taken into account in the process of color clamping for TAA. This mode can be used for relatively static scenes when improved antialiasing is required. In case of a dynamic scene, blurring artefacts near the screen borders may appear. **disabled** by default. `Console access:render_taa_diagonal_neighbors` ([API control](../../../api/library/rendering/class.render_cpp.md#render_taa_diagonal_neighbors)) ![](taa_diagonal_neighbors_off.png) ![](taa_diagonal_neighbors_on.png) |
| Preserve Details | The [detail level](../../../principles/render/antialiasing/taa.md#taa_preserve_details) of TAA (Temporal Anti-Aliasing). The higher the value, the more detailed the image is. Can produce additional flickering. Range of values: **[0.0f, inf]**. The default value is : **0.5f**. `Console access:render_taa_preserve_details` ([API control](../../../api/library/rendering/class.render_cpp.md#render_taa_preserve_details)) |
| Frame Count | The [frame count](../../../principles/render/antialiasing/taa.md#taa_frame_count) of TAA (Temporal Anti-Aliasing). Specifies the number of frames combined for pixels. The higher the value, the more frames are combined into the final image and the better anti-aliasing. This value is used only when the Frames By Velocity option is disabled. Range of values: **[0.0f, inf]**. The default value is : **30.0f**. `Console access:render_taa_frame_count` ([API control](../../../api/library/rendering/class.render_cpp.md#render_taa_frame_count)) |
| Pixel Offset | The size of the sample offset performed during subpixel jittering. The offset can be less than a pixel: for example, if **0.5** is set, frames will shift to half a pixel. Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**. `Console access:render_taa_pixel_offset` ([API control](../../../api/library/rendering/class.render_cpp.md#render_taa_pixel_offset)) |
| Samples | The number of the sample offsets performed during subpixel jittering. The parameter allows reducing image jittering and blurring. By the minimum value of 0 (1 sample offset), there will be no offsets, and, therefore, no anti-aliasing. TAA must be enabled. One of the following values: - 1 sample offset, no anti-aliasing - 4 offsets (by default) - 8 offsets - 16 offsets `Console access:render_taa_samples` ([API control](../../../api/library/rendering/class.render_cpp.md#render_taa_samples)) |
| Frames By Velocity | The value indicating if the TAA [velocity clamping](../../../principles/render/antialiasing/taa.md#taa_vc_enabled) option is enabled. This option controls the number of frames combined for pixels depending on the velocity in the fragment. It reduces blurring in dynamic scenes with a lot of moving objects. **enabled** by default. `Console access:render_taa_frames_by_velocity` ([API control](../../../api/library/rendering/class.render_cpp.md#render_taa_frames_by_velocity)) |
| Threshold | The [velocity threshold](../../../principles/render/antialiasing/taa.md#taa_vc_threshold) of TAA (Temporal Anti-Aliasing), at which pixels are treated as fast moving ones.This value specifies the intensity of velocity clamping. The following options must be enabled: TAA and TAA velocity clamping. Range of values: **[0.0f, inf]**. The default value is : **1.0f**. `Console access:render_taa_frames_velocity_threshold` ([API control](../../../api/library/rendering/class.render_cpp.md#render_taa_frames_velocity_threshold)) |
| Edges Frame Count Multiplier | The multiplier for the number of frames accumulated for TAA effect on the sharp edges of objects within the image. Range of values: **[1.0f, inf]**. The default value is : **1.0f**. `Console access:render_taa_edges_frame_count_multiplier` ([API control](../../../api/library/rendering/class.render_cpp.md#render_taa_edges_frame_count_multiplier)) |
| Information Lost Depth Threshold | The threshold value for the depth difference used to calculate information lost areas. "Information lost" refers to rendering of the surfaces that weren't rendered in the prevoius frame. Range of values: **[0.0f, inf]**. The default value is : **0.1f**. `Console access:render_taa_information_lost_depth_threshold` ([API control](../../../api/library/rendering/class.render_cpp.md#render_taa_information_lost_depth_threshold)) |


## Recommendations


As you can see TAA has a lot of settings enabling you to adjust it for relatively static scenes as well as for dynamically changing environments.


### Static Scenes


Below is an example of TAA settings for relatively static scenes.


![TAA Settings for Relatively Static Scenes](taa_static.png)

*Recommended Antialiasing Settings for Relatively Static Scenes*


- The *[**Diagonal Neighbors**](#diagonal_neighbors)* option should be enabled, as it provides more accurate pixel color information reducing the stair-step effect. At the same time TAA causes more blurring is case of fast camera movement, which is especially noticeable on grass and other similar high-contrast screen areas.
- *[**Preserve Detail**](#taa_preserve_details)* value is decreased to reduce flickering of small pixels.
- The number of *[**TAA Samples**](#taa_samples)* is set to 16, which increases the number of variants for subpixel camera jittering, thus making the stair-step effect even less noticeable.


### Dynamic Scenes


Below is an example of TAA settings for very dynamic scenes where trails from thin objects are especially noticeable.


![TAA Settings for Dynamic Scenes](taa_dynamic.png)

*Recommended Antialiasing Settings for Dynamic Scenes*


- The *[**Diagonal Neighbors**](#diagonal_neighbors)* option should be turned off, as it may result in significant blurring of small details in motion.
- Increase the *[**Preserve Details**](#taa_preserve_details)* value up to **1** or higher to reduce ghosting effect for moving objects.
- Set *[**TAA Samples**](#taa_samples)* value to **4** to reduce flickering of small pixels when the camera does not move.
