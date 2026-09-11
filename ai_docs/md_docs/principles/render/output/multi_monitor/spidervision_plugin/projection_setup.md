# Configuring Projections


To set up projections, select *Tools -> Projection Setup* in the *SpiderVision Setup* window menu:


![](open_projection_setup.png)


The *Projection Setup* window will open. This window makes it possible to:


- [Rotate and flip](#canvas) projections.
- Control [warping](#warp) for each projection.
- Set up [edge blending](#blend) and masks for each projection.
- Correct [color intensity](#color) for each projection.


## Common Settings


These settings are common for most tabs of *Projection Setup*:


| Current Viewport | Select a projection in the drop-down list to set up its parameters. You can also use ***Page Up*** and ***Page Down*** buttons to switch between projections. |
|---|---|
| Apply | Enables or disables application of the selected projection setting to the rendered image in the [current viewport](#current_viewport). |
| Help | Displays the window with the information on controls that may be used in the grid area: - **Left-click** a point on the grid to select it. Hold **Ctrl** for multiple selection. - **Click and drag** to select several points - points inside the frame will be selected. - **Drag** selected points (or their handles) with **LMB** to modify the grid. - Hold **MMB** and move the mouse for panning in the Warp viewport. - Scrolling by the **Mouse wheel** allows zooming in the Warp viewport. - **Arrow keys**: navigate between points. - **Shift + Arrow keys**: select multiple neighboring points in a chain-like way. - **Ctrl + Arrow keys**: move the selected points. - **+** / **-** : increase/decrease the movement step when point(s) are moved using arrows. |
| ![](fit_btn.png) | The button to undo all panning and zooming actions and make the grid fit the window. |
| Shift Step | Step to shift the selected points with arrow keys. Use **+** to increase the value, or **-** to decrease it. |
| Resolution | The number of control points along the horizontal and vertical axes of the grid. A 2 x 2 grid is used by default. ![](control_points.png) > **Notice:** The maximum grid size is 32 x 32. For *[Blend Zones](#blend)*, this setting controls the number of horizontal lines only. |
| Point | Index of the selected control point. In case of [Warp Grid](#warp), the control point has the horizontal and the vertical index values. Enumeration starts from the bottom left corner. In case of multiselection, typing the point index deselects all other points. If the value is outside the limits, the point with the closest index remains selected. |
| Position | Coordinates of the selected control point along the X and Y axes. ![Coordinates for points and handles](points.png) *Coordinates for control points* In case of multiselection: - If selected points have the same X or Y coordinate, it is displayed in the corresponding position box. In case of different values, **-** is displayed. - Typing in the coordinate value sets this value for all selected points. |
| Type | Type of line curving for the selected control point: - ![](auto_linear.png) � non-controllable linear handles with the offset equal to 0 - ![](manual_symmetric.png) � controllable smooth handles with transversely aligned offsets - ![](manual_asymmetric.png) � controllable break handles with individually configurable offsets - ![](auto_curve.png) � non-controllable handles with the automatically calculated offsets |


## Warping


![Interface](projection_setup_interface.png)

*Interface*


The ***Warp*** tab allows you to set up geometry correction for your projections. Areas where geometry correction is required include:


- Advanced off-axis correction where projector placement is awkward and needs an advanced mapping over the keystone function in a projector
- Non-planar screens such a curved screens and hemispherical domes
- Projecting one image from one projector onto more than one surface
- Unusual projection applications onto custom designed screens


Warping is performed by modifying the displayed grid in the visual editor. Set up warping for the [selected projection](#current_viewport) using control points and yellow handles. These handles are displayed for each selected control point depending on its [type](#type).


> **Notice:** Points are always moved in the screen-space coordinates regardless of image orientation (whether it is flipped or not), this means if you press left arrow, the point always goes left.


The possible ways of controlling the point positions are listed [here](#help).


![](grid_edit.gif)


You can see an example of a warped grid and a corresponding projection image below.


![Warped grid](curve.png)

*Warped grid*


![Warped image](curved.jpg)

*Warped image*


In addition to the [common settings](#common_settings), the following options specific for the *Warp* tab are available:


| Reset Warp Grid | Resets the warp grid to the default state. |
|---|---|
| Canvas | Configure the canvas for the selected projection: enable vertical and horizontal flipping. ![](setup_canvas.png) |


## Color and Brightness Correction


The **Color Correction** tab allows you to correct color intensity, as well as to adjust color balance for the selected projection.


![](setup_color.png)


| Brightness | Per-channel color multiplier to control the intensity of: - Red - Green - Blue - RGB at once ![Red channel scale](red_scale.jpg) *Brightness for the red channel = 2* |
|---|---|
| Contrast | Settings that allow you to adjust the color balance per channel (as well as for all channels at once): - Positive values are added to the color values on the screen. - Negative values are subtracted from color values on the screen. ![Red channel bias](red_bias.jpg) *Contrast for the red channel = -0.1* |
| Brightness (corners) | Settings to adjust brightness compensation for each of the projection's corners individually. |


> **Notice:** All *Color Balance* parameters can be reset to defaults by clicking the corresponding parameter name (by line or by column).
>
>
> ![Clickable setting names](clicable_color_balance_settings.gif)


## Blending


The **Blend Zones** tab allows you to configure blending in the selected area.


The screen-space blend area is not affected by warping.


![](blend_zone.jpg)


To start creating the blending area, click the *[Add](#blend_add)* button, and in the grid, click to define one side of the area, then click to define the other side � the green line will appear. The third click shows the blending direction.


![](setup_blend.gif)

*Defining a screen-space blending area*


![](ssblend_result.png)

*The blended area*


The area of the screen-space blend area is divided into two parts: the part between the blue and green lines is a solid-black area (i.e. the projected image is not displayed at all), and the part between the green and red lines is a gradient area (i.e. the projected image gradually becomes transparent).


In plain words, if you have two projectors, the green line of the blend zone in one projection should coincide with the red line of the blend zone in the other projection. For more than two projectors, the area between blue and green lines is used.


By default, each of these lines has two points marking the line limits. Using [Resolution](#resolution), you can increase the number of points along each line to adjust it as required by moving the points. Multi-selection of points is available.


In addition to the [common settings](#common_settings), the following options specific for the *Blend Zones* tab are available:


| Add | Adds a blend zone |
|---|---|
| Remove | Deletes the selected blend zone. |
| Apply | Enables or disables application of the selected blend zone to the rendered image. |
| Link to Projection | Allows adjusting ***Alpha**, **Contrast***, and ***Gamma*** for two blends simultaneously for better neighboring of two projections. If toggled on, select the projection and the blend area from the drop-down lists and adjust the necessary parameters. |
| Name | Blend area name in the *Screen-Space Blending* list. |
| Alpha | Transparency of the whole blended area. |
| Contrast | Contrast of the gradient part of the blended area. |
| Gamma | Gamma correction value for the blend zone. |


## Masking


The **Masks** tab allows using masks to cut out certain areas of the selected projection.


To **create a mask**, click **Add** and ensure that the **Creation Mode** button is enabled. Then create at least three points on the grid by clicking in the required place. The corresponding area of the projection will be cut out. The list of masks for the current projection is displayed under the grid. You can add new masks and remove existing ones using the corresponding buttons.


To **add new points** to the mask selected in the list, ensure that the **Creation Mode** button is enabled. Then you can add new points by clicking within the grid area. To insert a new point into an existing mask, select the point next to which a new point is to be added, and click to insert a new one. You can drag an existing point to move it. To **remove a point**, right-click it.


![](mask_edit.gif)


As you select a mask in the list, its parameters are displayed on the panel next to it:


![](setup_masks.png)


| Apply | Enables or disables display of the selected mask. Can be used for convenience when configuring overlapping regions, when there are a lot of masks. |
|---|---|
| Name | Mask name, can be edited. |
| Smooth | Smoothing value, the number of additional points to be inserted between the control points of the mask. |


## Render


![](render.png)


The *Render* block of settings is located at the bottom of the *Projection Setup* window. These settings are designed to facilitate fine-tuning of the projection by displaying the auxiliary elements on the actual projection.


| Debug Color | Temporarily set individual colors for different projections. This helps to visualize overlapping regions. |
|---|---|
| Debug Stereo | Tints the projection to verify the stereo output: the left eye is shown in green, the right eye in red. Applies to viewports rendered in the *[Stereo](../../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#render_mode)* mode. |
| Show Grid | Display the warp grid in the viewport. |
| Show Warp Points | Display the selected warp points and auxiliary lines showing the point location (useful if the point is outside the projection boundaries). |
| Show Blend Points | Display blend zones with selected points and auxiliary lines showing the point location (useful if the point is outside the projection boundaries). The red and green lines marking the blend zone are used for correct mapping of overlapping projections. |
