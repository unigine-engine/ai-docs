# Exporting 3D Models From Autodesk Maya


This article describes how to export your 3D Model From *Autodesk Maya* so that it would have proper scaling, position, and orientation when imported to UnigineEditor.


## See Also


> **Warning:** The video tutorial is created using **SDK version 2.11**. The general workflow demonstrated in the tutorial is applicable for versions **up to 2.21**. However, specific details such as UI may differ across various versions.


## Pre-Export Arrangement


Before the export, do the following:


- Check that *World Coordinate System* and *Working Units* are set as follows: ![](maya_units.png) For convenience, you can set the grid cell size equal to 1 meter. Click *Display -> Grid* and set the following: ![](maya_grid.png)
- Orient the model towards the positive direction of the Z axis, which is the front direction in *Autodesk Maya*. ![](maya_axis.png)
- Set the actual model size.
- Freeze transformations (*Modify -> Freeze Transformations*), if needed.
- Check that materials are ready for export.


## Export Settings


As soon as your model is ready for export, click *File -> Export All...*.


Export settings should be the following:


- Files of type: FBX export
- Units: Automatic
- Up Axis: Y


![](maya_export_settings.png)
