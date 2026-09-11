# Stereo Rendering


Unigine supports "easy on the eye" stereo 3D rendering out-of-the box for all supported video cards. Unigine-powered 3D stereoscopic visualization provides the truly immersive experience even at the large field of view or across three monitors. It is a completely native solution for both DirectX and Vulkan APIs and does not require installing any special drivers. Depending on the set stereo mode, the only hardware requirements are the equipment necessary for stereoscopic viewing (for example, active shutter glasses, passive polarized or anaglyph ones) or a dedicated output device.


> **Notice:** You may notice a drop in performance when using stereo rendering. This happens because all viewports are effectively rendered twice each frame.


## Stereo Modes


There are several modes of stereo rendering available for Unigine-powered application. To enable them, no special steps or modifications are required. Just use a ready-compiled plugin library, set the desired start-up option and you application is stereo-ready!


Stereo libraries are located in the `lib/` folder of the UNIGINE SDK.


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


Horizontal and Vertical stereo modes are supported for glass-free MasterImage 3D displays. The same mode (a horizontal or a vertical one) is selected in the graphics chip driver settings. See further details on rendering [below](#mobile_rendering).


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


### Unigine Stereo Rendering Pipeline


Unigine engine calculates the images for both eyes using the appropriate postprocess shader. Which shader is applied depends on the chosen stereo mode.


- *[Anaglyph](#stereo_anaglyph)* mode uses the *post_stereo_anaglyph* postprocess material and only one render target.  Two images are filtered by red and blue channels, superimposed and output onto the screen to be viewed through colored glasses.
- *[Separate images](#stereo_separate)* mode uses the *post_stereo_separate* postprocess material. It creates two render targets and outputs left and right eye images that are offset relative to each other onto the two separate monitors.
- *[Interlaced lines](#stereo_interlaced)* mode uses the *post_stereo_interlaced* postprocess material.  This mode is based on the interlaced coding. For example, the image for the left eye can be displayed on the odd rows of pixels with one polarization and the image for the right eye - on the even rows with other polarization.
- *[Horizontal and Vertical](#stereo_mobile)* stereo modes use only one render target.  After that, the graphics chip driver handles it as two images aligned horizontally or vertically (depending on the set mode) and stretches them onto the screen to create a stereo effect. If the **horizontal** stereo mode is used, the *post_stereo_horizontal* postprocess material is applied. In case of the **vertical** stereo mode, the *post_stereo_vertical* postprocess material is used.


If stereo rendering is disabled (for example, when 3D Vision application is switched to the windowed mode), *post_stereo_replicate* material is used and the postprocess shader creates a simple mono image (the same for all viewports, if there are many). This material allows to switch to normal rendering and avoid the black screen when the engine is not rendering stereo pairs.


Stereo rendering is optimized to be performance friendly while not compromising the visual quality. For example, shadow maps are only rendered once and used for both eyes; geometry culling is also performed only once. Most of the [rendering passes](../../../../principles/render/sequence/index.md) are still doubled, that is why it might make sense to turn off unnecessary passes or set a global shader quality to lower level to minimize the performance drop.


## Customizing Stereo


Stereo rendering can be controlled via the following code:


- Stereo script `stereo.h` (located in `data/core/scripts/system` folder). By default it is included in the system script `unigine.cpp`.  You can modify the `stereo.h` script in order to change the default camera configuration.
- If you choose not to include the stereo script into the system one, you can set the appropriate stereo mode definition and control stereo parameters directly via [*engine.render.setStereoRadius()*](../../../../api/library/rendering/class.render_cpp.md#setStereoRadius_float_void) and [*engine.render.setStereoDistance()*](../../../../api/library/rendering/class.render_cpp.md#setStereoDistance_float_void) functions. In this case, you need to implement your own camera configuration in the *render()* function of the system script: ```cpp int render() { #ifdef STEREO_MODE // implementation of a custom camera configuration #endif return 1; } ```


> **Notice:** The `STEREO_MODE` definition should be specified on the application start-up as the argument of the `-extern_define` command-line option.


## Hidden Area


Some pixels are not visible in VR. You can optimize rendering performance by skipping them. The following culling modes are available for such pixels:


- **OpenVR-based** culling mode - culling is performed using meshes returned by OpenVR. Take note, that culling result depends on HMD used.
- **Custom** culling mode - culling is performed using an oval or circular mesh determined by custom adjustable parameters.


You can specify a [custom mesh](../../../../api/library/rendering/class.viewport_cpp.md#setStereoHiddenAreaMesh_Mesh_Mesh_void) representing such hidden area, adjust its [transformation](../../../../api/library/rendering/class.render_cpp.md#setStereoHiddenAreaTransform_vec4_void) and assign it to a viewport.


To set the value via the console, use the *[render_stereo_hidden_area](../../../../code/console/index.md#render_stereo_hidden_area)* console command.


## Articles in This Section

- [Separate Images Output with Separate Plugin](../../../../principles/render/output/stereo/appseparate/index.md)
