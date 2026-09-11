# Panoramic Rendering


With panoramic rendering you can get impressive 180 or even 360 degree panoramas on one monitor. To increase the total resolution of the rendered image, this viewport can be spanned across several monitors, if required.


## Panoramic Rendering Modes


The following rendering modes are supported:


- 180 or 360 degree panorama with curved edges
- 180 or 360 degree linear panorama without distortion at the edges
- Orthographic fisheye panorama with an adjustable field of view
- Equidistant (tru-theta or f-theta) fisheye panorama with an adjustable field of view
- Stereographic fisheye panorama with an adjustable field of view
- Equisolid (equal-area) fisheye panorama with an adjustable field of view


![](fisheye_modes.png)


The horizontal axis on the chart above is the angle (radians) of incident light on the lens where 0 degrees is along the lens axis. The vertical axis is proportional to the radius on the fisheye image where that light exits the lens.


### Curved Panorama


![Curved Panorama](panorama.jpg)

*180 degree panorama with curved edges on 1 monitor*


### Linear Panorama


![Linear Panorama](linear.jpg)

*180 degree linear panorama on 1 monitor*


### Fisheye


![Fisheye](fisheye.jpg)

*180 degree spherical panorama*


## How Panoramic Rendering Works


During panoramic rendering 4 viewports are seamlessly stitched into one for extra-wide field of view. Images are overlapped and blended along the border shown below.


![4 viewports of panorama](viewports.jpg)

*4 viewports used to render panorama*


## Enabling Panoramic Rendering


To enable panoramic rendering for your application, open the [console](../../../../code/console/index.md) and run the `render_viewport_mode` command with the required panoramic mode (1-9). For example, to enable 180 degree panorama with curved edges:


```text
render_viewport_mode 1
```


> **Notice:** It is impossible to use panoramic rendering with:
>
>
> - Multi-monitor plugins (*[SpiderVision](../../../../principles/render/output/multi_monitor/spidervision_plugin/index.md), [Surround](../../../../principles/render/output/multi_monitor/appsurround/index.md)*)
> - [Stereo 3D](../../../../principles/render/output/stereo/index.md)


When panoramic rendering is enabled, the camera's *[Field of View](../../../../editor2/camera_settings/index.md#fov)* option is not applicable.


![](fisheye.gif)


To adjust FOV for fisheye panoramic rendering modes, select one of the *[Fisheye](../../../../editor2/settings/render_settings/screen/index.md#stereo_panorama)* modes and set the desired *Panorama Fisheye FOV* via the *Screen Settings* or using the corresponding console commands:


```text
render_viewport_mode 7 render_panorama_fisheye_fov 30
```


> **Notice:** Available only when `render_viewport_mode` is set to one of the fisheye panorama modes (5-9).


## Multi-Monitor Mode


It is also possible to span panorama across several identical monitors (only) in the fullscreen mode without decorations. For that, you need to specify on the start-up:


- The summed resolution of two displays (for example, for two 1280x1024 displays, that would be 2560x1024)
- *video_fullscreen 2*


For example (do not forget to specify other required [start-up options](../../../../code/command_line.md)):


```bash
main_x64.exe -video_mode -1 -video_width 2560 -video_height 1024 -video_fullscreen 2
```


![Curved Panorama](fullwindow.jpg)


## Seamless Panoramic Output


Most screen-space effects and camera-based adjustments are not compatible with panoramic rendering as several independent cameras are used simultaneously. Here are the basic recommendations for creating better panoramas:


- Select the **[Static Exposure Mode](../../../../editor2/settings/render_settings/camera_effects/index.md#mode)** in the *Camera Effects* and adjust the **[Exposure](../../../../editor2/settings/render_settings/camera_effects/index.md#exposure_value)** value: ![](camera_exposure_dynamic.png) ![](camera_exposure_static.png)
- You might also need to disable **[Lens Flares](../../../../objects/lights/parameters/index.md#lens_flares_settings)** from light sources and **[Camera Glare Effects](../../../../editor2/settings/render_settings/camera_effects/index.md#glare_effects)**, such as *Bloom*;
- The **[Auto White Balance](../../../../editor2/settings/render_settings/camera_effects/index.md#white_balance)** feature can also make edges visible, so it is recommended to disable it as well;
- Screen-space post effects, like **[SSR](../../../../editor2/settings/render_settings/ssr/index.md)**, **[SSRTGI](../../../../editor2/settings/render_settings/global_illumination/index.md)**, **[SSDirt](../../../../editor2/settings/render_settings/ssdirt/index.md)**, **[SSBevel](../../../../editor2/settings/render_settings/ssbevel/index.md)**, and others, are also often a reason for noticeable artifacts. The **[Render Border](../../../../editor2/settings/render_settings/screen/index.md#border_width)** feature is capable of reducing some artifacts introduced by screen-space effects. Adjust the **Border Width** and **Height** values to enable rendering outside the screen bounds for each viewport and eliminate subtle artifacts from these effects. ![](render_border_0.png) ![](render_border_1.png)
- Shading issues are inevitable for [*Billboards*](../../../../objects/objects/billboards/index.md) and billboard-based [*Particle Systems*](../../../../objects/effects/particles/index.md).
