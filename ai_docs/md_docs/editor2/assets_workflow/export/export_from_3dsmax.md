# Exporting 3D Models From Autodesk 3ds Max


This article describes how to export your 3D Model from *Autodesk 3ds Max* so that it would have proper scaling, position, and orientation when imported to UnigineEditor.


## See Also


> **Warning:** The tutorial is created using **SDK version 2.11**. The general workflow demonstrated in the tutorial is applicable for versions **up to 2.21**. However, specific details such as UI may differ across various versions.


## Pre-Export Arrangement


Before the export, do the following:


- Select *Customize -> Units Setup* and check that **Centimeters** are set as System Units. ![](3dsmax_units.png) For convenience, you can set the grid cell size equal to 1 meter: Go to *Tools -> Grids and Snaps -> Grid and Snap Settings -> Home Grid*. ![](3dsmax_grid.png)
- Orient the model towards the negative direction of the Y axis, which is the front direction in *Autodesk 3ds Max*. ![](3dsmax_axis.png)
- Set the actual model size.
- Reset all transforms (*Utilities -> Reset XForm*). ![](3dsmax_reset_transform.png)
- Check that materials are ready for export.


## Export Settings


As soon as your model is ready for export, click *File -> Export*. Save as type: *Autodesk (*.FBX)*, click *Save*.


In *FBX Export* window, select *Geometry* and enable *Smoothing Groups* and *Triangulate*.


![](3dsmax_export_settings.png)


In the *Advanced Options*, enable **Automatic** scale factor and select **Z-up** as the *Up Axis*.


![](3dsmax_export_settings_advanced.png)
