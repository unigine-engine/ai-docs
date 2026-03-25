# Reflections


This article lists all types of rendering techniques used to simulate specular and diffuse reflections available in UNIGINE.


## Environment Reflections


This is the default type of reflections provided by the [Environment](../../editor2/lighting/environment.md) settings.


![](env/ibl_1.png)


## Environment Probe Reflections


To change reflections locally, *[Environment Probes](../../editor2/lighting/gi/env_probes.md)* are used. Both static and dynamic modes are supported.


![](environment_probes.jpg)


## Planar Reflections


*Planar Reflections* is a dynamic reflections approach available via [Planar Reflection Probes](../../objects/lights/planar/index.md).


![](planar_reflections.jpg)


## Screen-Space Reflections


*[Screen-Space Reflections](../../editor2/settings/render_settings/ssr/index.md)* is a real-time technique for calculating reflections based on screen buffers with the help of raytracing algorithms.


![](ssr.jpg)


## Diffuse Reflections from Voxel Probes


[Diffuse Reflections](../../editor2/lighting/gi/voxel_probes.md#reflections) are provided by baked voxel probes and can be used on rough surfaces.


![](gi/diff.gif)
