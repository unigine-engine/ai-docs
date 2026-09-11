# Brush Tool


![](../brush.png) **Brush** tool (**B** hotkey) is used for painting arbitrary shapes on a texture.


![](brush.png)


## Settings


All available settings are described in the [Texture Editor](../../../editor2/texture_editor/index.md#settings) article. However, there is a specific **Draw Blend Mode** parameter that sets a blending mode for the brush:


- Alpha Blend � override the existing color with the current color.
- Add � add the current color to the existing color value. This mode can be useful when painting a height map. | ![](alphablend.png) | ![](add.png) | |---|---| | *Alpha Blend Mode* | *Add Mode* |
- Minimum � override the existing color with the current color only if it has a *lower* value.
- Maximum � override the existing color with the current color only if it has a *higher* value. This mode can be used, for example, when you need to increase low values in a height map by no more than a certain value. | ![](minimum.png) | ![](maximum.png) | |---|---| | *Minimum Mode* | *Maximum Mode* |
