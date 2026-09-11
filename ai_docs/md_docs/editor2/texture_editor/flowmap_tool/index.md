# Flow Map Tool


![](../draw_flowmap.png) **Flow Map** tool allows painting a flow map that stores direction vectors: a brush stroke changes its color depending on the direction of drawing. The flow map is used to specify the direction of a panner for textures. For example, you can simulate the flow of a river.


## Settings


![](flow_map.png)


| Flowmap Space | Specifies the coordinate space of the flow map: Tangent Space or Object Space. For example, if you set the *Flowmap Range* to From negative to positive in the Object Space, the brush stroke color will correspond to the color of the axis along which it is drawn. ![](object_space.png) *Flow Map in Object Space* |  |  |  |  |
|---|---|---|---|---|---|
| Flowmap Range | Specifies the range of values for direction vectors: - From zero to positive � the flow map stores direction vectors in range [0, 1]. It is a remapped range. When it is used, the flow map has rainbow-colored appearance. - From negative to positive � the flow map stores direction vectors in range [-1, 1]. It is a native range. \| ![](range_0.png) \| ![](range_1.png) \| \|---\|---\| \| *From zero to positive* \| *From negative to positive* \| | ![](range_0.png) | ![](range_1.png) | *From zero to positive* | *From negative to positive* |
| ![](range_0.png) | ![](range_1.png) |  |  |  |  |
| *From zero to positive* | *From negative to positive* |  |  |  |  |
