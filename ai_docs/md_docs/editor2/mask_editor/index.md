# Mask Editor


UnigineEditor provides a useful tool for painting image masks directly in the scene � *Mask Editor*. It allows editing the existing image masks and creating new ones.


### See Also


- Chapter on [Image Mask for the Grass Field](../../objects/objects/grass/index.md#mask)
- Tutorial on [Adding Grass](../../objects/objects/grass/tutorial/index.md#textures)
- Chapter on *Masking Areas with Objects* for *[Mesh Clutter](../../objects/objects/mesh_clutter/index.md#masking)* and *[World Clutter](../../objects/worlds/world_clutter/index.md#masking)*


## Creating Mask with Mask Editor


To create a new image mask by means of *Mask Editor*:


1. [Run](../../editor2/index.md#run) UnigineEditor.
2. Add *[Grass](../../objects/objects/grass/index.md), [Mesh Clutter](../../objects/objects/mesh_clutter/index.md)* or *[World Clutter](../../objects/worlds/world_clutter/index.md)* to the scene by choosing the required object via the Menu bar (the *Create* menu item).
3. Specify all required settings for the added object.
4. On the toolbar, select *Clutter Mask Paint Mode*. The *Active Tool* window will open. In the *Objects* section there will be a list of all *[Grass](../../objects/objects/grass/index.md), [Mesh Clutter](../../objects/objects/mesh_clutter/index.md)* and *[World Clutter](../../objects/worlds/world_clutter/index.md)* objects available in the world. ![](active_tool.png)
5. Select the object you want to create the mask for and click the *Create a New Mask Texture Asset* button. You can also use the ![](add.png) button next to the *Mask Texture* field in the *Parameters* window of the selected object. ![](create_empty_mask.png)
6. Specify the size and format of the mask in the window that opens and click **OK**. ![](mask_size.png)
7. In the file dialog window that opens, choose the folder within your project to save the mask and click **OK**. An empty image mask will be created.


## Editing Mask with Mask Editor


As soon as you created the mask, editing tools are available in the *Parameters* section of *Active Tool*. Select the required option and start editing the mask directly in the scene.


Available controls and hotkeys are listed at the bottom of the *Active Tool* window.


If the *Active Tool* window is closed, you can re-open it by switching to *Clutter Mask Paint Mode* or clicking the *Brush Edit* button in the *Parameters* tab of the corresponding object.


## Mask Editor Options


![](mask_editor.png)


| Mode | Available modes: - ![](mode_replace.png)**Draw** � replace pixel values of the image mask with the current values set for the brush. - ![](mode_add.png)**Add** � add pixels to the image mask (in other words, add areas to the image mask where grass or clutter objects should be placed). - ![](mode_subtract.png)**Subtract** � subtract the current values set for the brush from pixel values of the image mask. - ![](mode_smooth.png)**Smooth** � blur pixels of the image mask, making boundaries softer. - ![](mode_erase.png)**Erase** � erase pixels of the image mask. - ![](mode_select.png)**Select** � enables selection between *[Mesh Clutter](../../objects/objects/mesh_clutter/index.md#masking)* objects in *Clutter Mask Paint Mode*. |
|---|---|
| Brushes | Shape of the brush: - ![](shape_circle.png) � Circular shape. - ![](shape_square.png) � Square shape. - Custom brush. The texture is loaded using the additional button ![](shape_custom.png). |
| Size | Size of the brush. |
| Color | Color of the brush. |
| Intensity | Intensity of the color components of the brush. |
| Opacity | Transparency of the applied color. |
| Sharpness | Tip of the brush. The *lower* the value, the sharper and smaller the tip. The *higher* the value, the flatter and bigger the tip. |
| Step | The distance between the brush marks in a stroke, in pixels. |
| Refresh Rate | Frequency of updating the objects distribution following the mask changes, in seconds, if the brush is dragged continuously. |
