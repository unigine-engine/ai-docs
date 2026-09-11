# Skin Layout


## General Information


All textures must be power of two in size, rectangular textures are supported, for example, 16�16, 128�32, 8�64, etc. All files are in the RGBA format.


## Icons


![](./icon.png)

*Standard 32x32 icon*


### Layout


There are four states of an icon:


1. Not pressed, not in focus.
2. Not pressed, in focus.
3. Pressed, not in focus.
4. Pressed, in focus.


![](./layout_icon.png)


### Assembly


Parts of the texture are copied 1:1.


## Boot and Loading Screens


![](./splash.jpg)

*Texture splash screen*


### Layout


The texture is divided into two parts: the initial state (upper) and the final state (lower).


### Assembly


While a texture of a loading screen is being displayed, the initial picture (upper) is gradually replaced with the final one (lower). Pseudo-animation can be created using the alpha channel: regions of the lower half with small alpha values will be shown first, regions with larger alpha values will be shown last.


## Base Skin


### gui_background.png


![](./gui_background.png)

*Background texture*


#### Assembly


The texture is resized to fit a widget.


### gui_border.png


![](./gui_border.png)

*Frame borders*


#### Layout


![](./layout_gui_border.png)


#### Assembly


All four corners are copied 1:1 from corresponding corners of the texture:


1. The top-left corner
2. The top-right corner
3. The bottom-left corner
4. The bottom-right corner


Vertical and horizontal strips (2 pixels in width), which are located at the center of the corresponding half of the texture are used to fill in space between corners. The strips are stretched, and the resulting color bar is constructed using interpolation between colors of the pixels in the strips.


### gui_button.png


![](./gui_button.png)

*Button*


#### Layout


The texture contains four variants of buttons in different states, the same as defined for [icons](#icon). Also, each button is divided into 3 parts, which are shown below.


![](./layout_gui_button.png)


#### Assembly


All four corners are copied 1:1 from corresponding corners of the texture. Vertical and horizontal strips (2 pixels in width), which are located at the center of the corresponding half of the texture and marked as 2 and 3 on the picture are used to fill in space between corners. The strips are stretched, and the resulting color bar is constructed using interpolation between colors of the pixels in the strips.


![](./layout_gui_button_assembled.png)


### gui_checkbox.png


![](./gui_checkbox.png)

*Checkboxes and radiobuttons*


#### Layout


The texture contains two variants of checkboxes (left column) and two variants of radio buttons (right column) for unchecked/unselected (top row) and checked/selected (bottom row) states.


#### Assembly


Parts of the texture are copied 1:1.


### gui_combobox.png


![](./gui_combobox.png)

*Drop-down menu*


#### Layout


The texture contains two variants of combobox icons: closed menu (upper) and opened menu (lower).


#### Assembly


Parts of the texture are copied 1:1.


### gui_editor.png


![](./gui_editor.png)

*Background foreditlineandedittextwidgets*


#### Assembly


The left half of the texture is stretched to fill a widget. When pointing a mouse, it smoothly shifts to the right half.


### gui_hpaned.png


![](./gui_hpaned.png)

*Movable separator*


#### Assembly


The texture is stretched to the given height.


### gui_hscroll.png


![](./gui_hscroll.png)

*Horizontal scroll bar*


#### Layout


The texture is divided into five zones, each of which uses the layout similar to the [icon layout](#icon). Bottom-left corner has a specific layout, since it contains unused regions (highlighted with green hatching).


![](./layout_gui_hscroll.png)


#### Assembly


The scroll bar handle is combined from the left (1), central (3) and right (2) parts; the underlying bar is stretched to the given width.


![](./layout_gui_hscroll_assembled.png)


### gui_hslider.png


![](./gui_hslider.png)

*Horizontal slider*


#### Layout


The layout is similar to the layout of a [horizontal scroll bar](#gui_hscroll.png).


### gui_hspacer.png


![](./gui_hspacer.png)

*Horizontal spacer*


#### Assembly


The texture is stretched to the given width.


### gui_mouse.png


![](./gui_mouse.png)

*Mouse pointers*


#### Layout


There is a number of slots for different pointer states:


1. Base pointer
2. Operation is not permitted
3. Drag-and-drop mode
4. Reserved slot
5. Changing size horizontally
6. Changing size vertically
7. Changing size diagonally (1)
8. Changing size diagonally (2)
9. Movement
10. Rotation
11. Scaling


Other slots are reserved.


![](./layout_gui_mouse.png)


#### Assembly


Parts of the texture are copied 1:1.


### gui_selection.png


![](./gui_selection.png)

*Selection texture*


#### Assembly


The left half of the texture is used to highlight the text and the right one is used to highlight the selected tree element.


### gui_spinbox.png


![](./gui_spinbox.png)

*Spinbox*


#### Layout


The texture is divided into two parts: the left part is for an upper arrow, the right part is for a lower arrow. The layout of each part is the same as the icon layout and contains four states:


1. Not pressed, not in focus.
2. Not pressed, in focus.
3. Pressed, not in focus.
4. Pressed, in focus.


![](./layout_gui_spinbox.png)


#### Assembly


Parts of the texture are copied 1:1.


### gui_tabbox.png


![](./gui_tabbox.png)

*Tabs of thetabboxwidget*


#### Layout


Layout is the same as for [buttons](#gui_button.png).


#### Assembly


The assembly is the same as for [buttons](#gui_button.png).


### gui_tooltip.png


![](./gui_tooltip.png)

*Tooltip background texture*


#### Layout


Layout is the same as for [borders](#gui_border.png).


#### Assembly


The assembly is the same as for [borders](#gui_border.png).


### gui_treebox.png


![](./gui_treebox.png)

*Texture for thetreeboxwidget*


#### Layout


The texture is divided into three parts:


1. The upper left part is for folded non-leaf nodes.
2. The lower left part is for folded non-leaf nodes.
3. The right part is for "branches" connecting nodes.


#### Assembly


Parts of the texture are copied 1:1.


### gui_vpaned.png


![](./gui_vpaned.png)

*Movable separator*


#### Assembly


The texture is stretched to the given width.


### gui_vscroll.png


![](./gui_vscroll.png)

*Vertical scroll bar*


#### Layout


Layout is similar to the layout of the [horizontal scroll bar](#gui_hscroll.png).


#### Assembly


Assembly is similar to the assembly of the [horizontal scroll bar](#gui_hscroll.png).


### gui_vslider.png


![](./gui_vslider.png)

*Vertical slider*


#### Layout


Layout is similar to the layout of the [horizontal slider](#gui_hslider.png).


#### Assembly


Assembly is similar to the assembly of the [horizontal slider](#gui_hslider.png).


### gui_vspacer.png


![](./gui_vspacer.png)

*Vertical spacer*


#### Assembly


The texture is stretched to the given height.


### gui_window.png


![](./gui_window.png)

*Window skin*


#### Layout


On the image below, the left half is for windows with caption and the right half is for windows without caption.


![](./layout_gui_window.png)


#### Assembly


All four corners are copied 1:1 from the corresponding corners of the texture. Vertical and horizontal strips (two pixels in width), which are located at the center of the corresponding half of the texture are used to fill in space between corners. The strips are stretched, and the resulting color bar is constructed using interpolation between colors of the pixels in the strips.


![](./layout_gui_window_assembled.png)


## Dialogs


### Base Dialog


![](./sample_base_dialog.png)

*Simple dialog*


Two files are used to create a base dialog. These files correspond to two buttons of the dialog. Images are copied 1:1.


- ![](./dialog_ok.png) - dialog_ok.png
- ![](./dialog_cancel.png) - dialog_cancel.png


### File Dialog


![](./sample_file_dialog.png)

*File selection dialog*


This dialog requires four images that use the [icon layout](#icon).


- Go to the upper directory: ![](./dialog_file_path.png) *dialog_file_path.png*
- Add a tab ![](./dialog_file_add.png) *dialog_file_add.png*
- Remove the tab ![](./dialog_file_remove.png) *dialog_file_remove.png*
- Mini-icons for different file objects; split vertically into squares: ![](./dialog_file_list.png) *dialog_file_list.png*


### Image Dialog


![](./sample_image_dialog.png)


This dialog requires four images that use the [icon layout](#icon).


- Red channel toggle: ![](./dialog_image_r.png) *dialog_image_r.png*
- Green channel toggle: ![](./dialog_image_g.png) *dialog_image_g.png*
- Blue channel toggle: ![](./dialog_image_b.png) *dialog_image_b.png*
- Alpha channel toggle: ![](./dialog_image_a.png) *dialog_image_a.png*
