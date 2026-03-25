# Postprocess Materials


UNIGINE allows creating postprocessing effects using postprocess materials: they are applied after the scene in the viewport has been rendered, but before outputting it onto the screen.


Postprocess materials can be created via the [Material Editor](../../../../content/materials/graph/index.md) or implemented as [scriptable materials](../../../../content/materials/scriptable.md). Some of the postprocessing effects, such as HDR and DOF, can be adjusted directly in the *[Render Settings](../../../../editor2/settings/render_settings/index.md)*.


![](post_disabled.png) ![](post_enabled.png)


> **Warning:** Make sure that you disable all postprocess materials on all multi-monitor configurations.


## How to Apply Postprocess Materials


The postprocess materials are assigned globally or to a specific camera and affect the whole scene rendered in the viewport. To apply postprocess materials, do the following:


1. In the [Material Settings](../../../../editor2/materials_settings/index.md), select a postprocess material. ![](materials_list.png)
2. Open *Settings -> Custom Post Materials* and click *Add New Material*. Assign the selected material by dragging it to the field or by specifying the name of the material. If you want to use **several** postprocess materials at the same time, add them one by one in the list and these materials will be rendered in the order they are positioned in the section. ![](render_mat.png)
3. Click *create a child material* to enable specifying states and parameters of the material. The new child material will be created and assigned here. ![](post_parameters.png)


You can also apply postprocess materials as scriptables to a selected **camera**.


To apply the post process effect only to a specific camera, go to the *Parameters* tab of the corresponding [Player](../../../../objects/players/index.md) node and assign the material to it.


![](../../PlayerAddNew.png)
