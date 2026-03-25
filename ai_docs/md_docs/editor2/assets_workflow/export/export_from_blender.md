# Exporting 3D Models From Blender


This article describes how to export your 3D Model From *Blender* so that it would have proper scaling, position, and orientation when imported to UnigineEditor.


## See Also


> **Warning:** The tutorial is created using **SDK version 2.11**. The general workflow demonstrated in the tutorial is applicable for versions **up to 2.21**. However, specific details such as UI may differ across various versions.


## Pre-Export Arrangement


Before the export, do the following:


- Check that **Meters** are set as working units. ![](blender_units.png) *Blender* scale should be: **1 unit = 1 meter**. For convenience, you can set the grid cell size equal to 1 meter: ![](blender_grid.png)
- Orient the model towards the negative direction of the Y axis, which is the front direction in *Blender*. ![](blender_axis.png)
- Set the actual model size.
- Apply all transforms (*Object -> Apply -> All Transforms*). After applying all transforms, a part of model can be misplaced due to complex parenting. In this case, first clear parent (*Object -> Parent -> Clear and Keep Transform*), then apply transforms, and finally restore parent, if necessary.
- Check that materials are ready for export.


## Export Settings


As soon as your model is ready for export, click *File -> Export -> FBX*. Check that the parameters set in the *Transform* section are as follows:


![](blender_export_settings.png)
