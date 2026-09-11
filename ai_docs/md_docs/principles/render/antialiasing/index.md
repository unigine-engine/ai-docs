# Anti-Aliasing


Aliasing is a gradation of inclined lines of the image. This effect prevents the player from perceiving visual information as something continuous, and can be expressed in a sharp transition between the pixels, groups of pixels, or frames.


Usually, the problem of aliasing is considered as a problem of edges. For instance:


![](aa_off.png) ![](aa_on.png)


In a static picture, aliasing is visible at the boundaries of objects and polygons � anywhere, where there is a sharp contour. If a screen has a high resolution, then in statics, aliasing does not bring much discomfort. But in dynamics, the situation is quite different, as the picture starts to flicker. This is especially noticeable in VR, where the area of active vision is even smaller, and in this case, even the smallest pixels are very important. Moreover, the helmet itself does not remain in a static position, but in micro-motions, and when camera movements are overlapped on objects with sharp contours or fine details in the textures (specular aliasing, transparency aliasing, normals aliasing), the picture starts to flicker even more.


When a player looks at such a picture in the helmet, it causes discomfort because almost all the pixels in the image receive high-frequency noise (looks like fast flickering).


To fight the problems of aliasing, different smoothing algorithms are used. Basically the term "anti-aliasing" refers to any technology that eliminates the staircase effect (or "jaggies") on inclined (neither strictly vertical nor horizontal) edges of objects and lines including details in textures etc.


![](antialiasing.png)

*Antialiasing Settings*


| Preset | The antialiasing quality preset: - *Sharpest* � the sharpest quality - *Sharp* � sharp quality - *Smooth* � smooth quality - *Smooth + SRAA* � smooth quality with SRAA enabled - *Smoothest* � the smoothest quality - *Smoothest + SRAA* � the smoothest quality with SRAA enabled - *Vr mode* � quality preset for the VR mode - *Custom* � adjust the quality manually |
|---|---|


## Articles in This Section

- [Fast approXimate Anti-Aliasing (FXAA)](../../../principles/render/antialiasing/fxaa.md)

- [Temporal Anti-Aliasing (TAA)](../../../principles/render/antialiasing/taa.md)

- [Subpixel Reconstruction Anti-Aliasing (SRAA)](../../../principles/render/antialiasing/sraa.md)

- [Supersampling](../../../principles/render/antialiasing/supersampling.md)
