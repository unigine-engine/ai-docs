# Stereo Rendering


UNIGINE supports "easy on the eye" stereo 3D rendering out-of-the box for all supported video cards. UNIGINE-powered 3D stereoscopic visualization provides the truly immersive experience even at the large field of view or across three monitors. It is a completely native solution for both DirectX and Vulkan APIs and does not require installing any special drivers. Depending on the set stereo mode, the only hardware requirements are the equipment necessary for stereoscopic viewing (for example, active shutter glasses, passive polarized or anaglyph ones) or a dedicated output device.


> **Notice:** You may notice a drop in performance when using stereo rendering. This happens because all viewports are effectively rendered twice each frame.


## Stereo Modes


There are several modes of stereo rendering available for a UNIGINE-powered application. Anaglyph, interlaced, and split (horizontal and vertical) stereo are [viewport rendering modes](../../../../api/library/rendering/class.render_cpp.md#setViewportMode_int_void): no special steps or modifications are required, just switch the viewport to the corresponding mode and your application is stereo-ready!


A stereo mode can be set in one of the following ways:


- Via the *[Viewport Mode](../../../../editor2/settings/render_settings/screen/index.md#stereo_panorama)* parameter in the *Screen* render settings
- By running the [`render_viewport_mode`](../../../../code/console/index.md#render_viewport_mode) console command
- Via API, by using the *[setViewportMode()](../../../../api/library/rendering/class.render_cpp.md#setViewportMode_int_void)* method


Separate images output is the only stereo mode that requires loading a plugin: the `bin/plugins/Unigine/Separate/UnigineSeparate_*` library of the UNIGINE SDK.


To check if a certain mode is a stereo one, use the *[isViewportModeStereo()](../../../../api/library/rendering/class.render_cpp.md#isViewportModeStereo_int_int)* method. To check if stereo rendering is enabled for a viewport, use the *[isStereo()](../../../../api/library/rendering/class.viewport_cpp.md#isStereo_int)* method.


### Separate Images


This mode serves to output two separate images for each of the eye. It can be used with any VR/AR output devices that support separate images output, e.g. for 3D video glasses or helmets (HMD). See further details on rendering [below](#separate_rendering).


To launch Separate images stereo mode, load the [Separate plugin](../../../../principles/render/output/stereo/appseparate/index.md).


![Separate images stereo mode](separate_images.jpg)

*Separate images stereo mode*


### Anaglyph Mode


Anaglyph stereo is viewed with red-cyan anaglyph glasses. See further details on rendering [below](#anaglyph_rendering).


To launch Anaglyph stereo mode, run the [`render_viewport_mode`](../../../../code/console/index.md#render_viewport_mode) console command with the corresponding mode (10):


```text
render_viewport_mode 10
```


![Anaglyph stereo mode](anaglyph.jpg)

*Anaglyph stereo mode*


### Interlaced Lines


Interlaced stereo mode is used with interlaced stereo monitors and polarized 3D glasses. See further details on rendering [below](#interlaced_rendering).


> **Notice:** In this mode, the vertical resolution of the image is dropped in half.


To launch the interlaced lines stereo mode, run the [`render_viewport_mode`](../../../../code/console/index.md#render_viewport_mode) console command with the corresponding mode (11):


```text
render_viewport_mode 11
```


![Interlaced lines stereo mode](stereo_interlaced.png)

*Interlaced lines stereo mode*


### Split Stereo


Horizontal and Vertical stereo modes split the frame into two halves � side-by-side and top-and-bottom respectively � containing the images for the left and the right eye. Such a frame is then handled by a display supporting this format, for example, by a glass-free 3D display. The same mode (a horizontal or a vertical one) is selected in the graphics chip driver settings. See further details on rendering [below](#mobile_rendering).


To launch Horizontal stereo mode, run the [`render_viewport_mode`](../../../../code/console/index.md#render_viewport_mode) console command with the corresponding mode (12):


```text
render_viewport_mode 12
```


![Horizontal stereo mode](stereo_horizontal.jpg)

*Horizontal stereo mode*


To launch Vertical stereo mode, run the [`render_viewport_mode`](../../../../code/console/index.md#render_viewport_mode) console command with the corresponding mode (13):


```text
render_viewport_mode 13
```


![Vertical stereo mode](stereo_vertical.jpg)

*Vertical stereo mode*


## Stereo Rendering Model


The stereo rendering model uses asymmetric frustum parallel axis projection (called *off-axis*) to create optimal stereo pairs without vertical parallax (vertical shift towards the corners).
  It means, two cameras with parallel lines of sight are created, one for each eye. They are separated horizontally relative to the central position (this distance is called the eye separation distance and can be adjusted to avoid eyestrain from stereoscopic viewing). Both cameras use asymmetric frustum, when the far plane is parallel to the near plane, yet they are not symmetrical about the view axis. It enables to correctly align projection planes of two cameras to the zero parallax plane (i.e. the screen). Asymmetric frustum parallel axis projection produces no distortions in the corners making the stereoscopic image completely comfortable to the eye.


When rendered, objects that get in front of the camera's focal distance (that is, its projection plane) are perceived as popping out of the screen; objects that are behind it appear to be behind the screen and convey the impression of scene depth.


### UNIGINE Stereo Rendering Pipeline


UNIGINE engine calculates the images for both eyes using the appropriate postprocess shader. Which shader is applied depends on the chosen stereo mode.


- *[Anaglyph](#stereo_anaglyph)* mode uses the *post_stereo_anaglyph* postprocess material and only one render target.  Two images are filtered by the red and the cyan (green and blue) channels respectively, superimposed and output onto the screen to be viewed through colored glasses.
- *[Separate images](#stereo_separate)* mode uses the *post_stereo_separate* postprocess material. It creates two render targets and outputs left and right eye images that are offset relative to each other onto the two separate monitors.
- *[Interlaced lines](#stereo_interlaced)* mode uses the *post_stereo_interlaced* postprocess material.  This mode is based on the interlaced coding. For example, the image for the left eye can be displayed on the odd rows of pixels with one polarization and the image for the right eye - on the even rows with other polarization.
- *[Horizontal and Vertical](#stereo_mobile)* stereo modes use only one render target.  After that, the graphics chip driver handles it as two images aligned horizontally or vertically (depending on the set mode) and stretches them onto the screen to create a stereo effect. If the **horizontal** stereo mode is used, the *post_stereo_horizontal* postprocess material is applied. In case of the **vertical** stereo mode, the *post_stereo_vertical* postprocess material is used.


The *post_stereo_replicate* material is used by the **Replicate** mode, which outputs the same mono image to both eyes instead of a stereo pair. Take note that the scene is still rendered twice in this mode.


> **Notice:** The **Replicate** and the **Separate images** modes are intended for VR output and cannot be set via the console. Set them for a viewport via the [API](../../../../api/library/rendering/class.viewport_cpp.md#setMode_int_void).


Stereo rendering is optimized to be performance friendly while not compromising the visual quality. For example, shadow maps are only rendered once and used for both eyes; geometry culling is also performed only once. Most of the [rendering passes](../../../../principles/render/sequence/index.md) are still doubled, that is why it might make sense to turn off unnecessary passes or set a global shader quality to lower level to minimize the performance drop.


## Customizing Stereo


The way a stereo pair is created is defined by the following parameters:


- **Distance** � focal distance for stereo rendering: the distance in world units to the zero parallax plane, i.e. to the point where the two views line up. The higher the value, the further from the viewer the rendered scene is and the weaker the stereo effect is.
- **Radius** � half of the eye separation distance, i.e. of the interaxial distance between the two cameras used to create a stereo pair. The higher the value, the stronger the stereo effect is.
- **Offset** � virtual camera offset applied after the perspective projection.


All the three parameters are available via the [Render](../../../../api/library/rendering/class.render_cpp.md#setStereoDistance_float_void) class and are applied to the main application viewport:


```cpp
// set the distance to the zero parallax plane to 4 units
Render::setStereoDistance(4.0f);

// set the eye separation distance to 64 mm
Render::setStereoRadius(0.032f);

```


Each [viewport](../../../../api/library/rendering/class.viewport_cpp.md#setStereoDistance_float_void) has its own set of these parameters as well, but it is the global values that are to be used: for the main application viewport the per-viewport ones are overridden by the global values each frame.


The same parameters are available via the [console](../../../../vr_development/vr_console.md#vr_stereo_rendering).


## Hidden Area


Some pixels are not visible in VR. You can optimize rendering performance by skipping them. Such culling is disabled by default (0), the following culling modes are available for such pixels:


- **Runtime-based** culling mode (1) - culling is performed using meshes returned by the VR runtime (OpenXR, OpenVR, or Varjo). Take note, that culling result depends on HMD used.
- **Custom** culling mode (2) - culling is performed using meshes returned by the VR runtime and an oval or circular mesh determined by custom adjustable parameters.


You can specify a [custom mesh](../../../../api/library/rendering/class.viewport_cpp.md#setStereoHiddenAreaMesh_Mesh_Mesh_void) representing such hidden area, adjust its [transformation](../../../../api/library/rendering/class.render_cpp.md#setStereoHiddenAreaTransform_vec4_void) and assign it to a viewport.


Culled pixels are excluded from the image, but they still would be taken into account when calculating exposure, which results in visual artefacts. To avoid them, adjust the area used for [exposure calculation](../../../../api/library/rendering/class.render_cpp.md#setStereoHiddenAreaExposureTransform_vec4_void).


To set the culling mode via the console, use the *[render_stereo_hidden_area](../../../../vr_development/vr_console.md#render_stereo_hidden_area)* console command.


Support of the hidden area in shaders is enabled by default and is controlled by the *[render_stereo_hidden_area_enabled](../../../../vr_development/vr_console.md#render_stereo_hidden_area_enabled)* console command.


The whole set of stereo commands is listed in the [VR Console Commands and Variables](../../../../vr_development/vr_console.md#vr_stereo_rendering) article.


## Articles in This Section

- [Separate Images Output with Separate Plugin](../../../../principles/render/output/stereo/appseparate/index.md)
