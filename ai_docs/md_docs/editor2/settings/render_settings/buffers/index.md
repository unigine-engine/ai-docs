# Buffers


The section describes buffer settings. These settings can also be toggled on and off via the *Rendering* menu.


![Buffers settings](buffers.png)

*Buffers settings*


| Lightmap | Toggles the G-Buffer lightmap on and off. |
|---|---|
| Auxiliary | Toggles the auxiliary rendering buffer on and off. |
| Color 16F | Toggles the use of 16F texture format for rendering buffers on and off. |
| Depth Pre Pass | Toggles the depth pre-pass rendering on and off. When enabled, an additional depth buffer rendering pass is performed in the beginning of the rendering sequence. > **Notice:** This option can be used to gain performance for well-optimized scenes using LODs and having a low-to-medium number of triangles in case of GPU bottlenecks. In other cases (heavy CAD models, large number of triangles, and CPU bottlenecks), it may reduce performance. Use [profiling tools](../../../../tools/profiling/index.md) to make sure that a positive effect is obtained. |
