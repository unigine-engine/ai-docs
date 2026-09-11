# Organizing Materials


UNIGINE [materials](../../../content/materials/index.md) are organized in a hierarchy and managed via the *Materials Hierarchy* window.


![](materials_hierarchy_detailed.png)

*Materials Hierarchy Window*


The Materials Hierarchy window provides access to all materials of the project and allows filtering them, collapsing materials hierarchy (i.e., showing only the [base](../../../content/materials/index.md#base_materials) materials and hiding the [user](../../../content/materials/index.md#user_materials) ones), [inheriting](#materials_hierarchy), [cloning](#clone_material), [renaming](#rename_material), and [deleting](#delete_material) materials.


All materials in the hierarchy are linked to the `.basemat`, `.mat` and `.mgraph` material files stored in the `assets` folder of the project and available via the [Asset Browser](../../../editor2/assets_workflow/index.md#asset_browser). So, any operation on a material via the UnigineEditor interface updates the corresponding asset.


To open the Materials Hierarchy window, choose *Windows -> Toggle Materials Hierarchy* in the [Menu Bar](../../../editor2/interface/index.md#menu_bar) or press **M**.


### See Also


- *[Materials](../../../content/materials/index.md)* article to know basics of the material system used in UNIGINE
- *[Hierarchy and Inheritance](../../../content/materials/inheritance.md)* article to know more about how materials are organized
- *[Materials Files](../../../code/formats/materials_formats/index.md)* section to know more about the base and user material files


## Creating a Material


A material can be created via UnigineEditor in one of the following ways:


- By [inheriting](#materials_hierarchy) or [cloning](#clone_material) the existing material via the Materials Hierarchy window.
- By [creating](../../../editor2/assets_workflow/assets_create_import.md#create) or [importing](../../../editor2/fbx/index.md#materials) a material via the Asset Browser. Usually, materials are imported together with a [3D model or a scene of one of the supported formats](../../../editor2/assets_workflow/asset_types.md#geometry).


The new material is automatically added to the materials hierarchy and displayed in the Materials Hierarchy window. The asset, to which the new material links, is also created and becomes available via the Asset Browser.


> **Notice:** Materials in the hierarchy are sorted alphabetically by names, so you cannot rearrange them.


## Basic Operations on a Material


The Materials Hierarchy window allows the following basic operations on a material.


### Renaming a Material


To rename a material, right-click it and choose *Rename* in the drop-down list.


![](rename_material.gif)

*Renaming a Material*


You can also rename a material via the *Parameters* window by editing the *[Name](../../../editor2/materials_settings/index.md#material_preview)* field.


> **Notice:** Only the [user materials](../../../content/materials/index.md#user_materials) can be renamed. Renaming a material leads to renaming the asset file it is linked to.


If you rename a material asset via the [Asset Browser](../../../editor2/assets_workflow/assets_organize.md#rename), the material that links to it will be renamed as well.


### Cloning a Material


To clone a material, right-click it and choose *Clone* in the drop-down list.


![](clone_material.gif)

*Cloning a Material*


Another way to clone a material is to select it and click ![](clone.png) to the left of the material name filter.


> **Notice:** Only the [user materials](../../../content/materials/index.md#user_materials) can be cloned. Cloning a material leads creating an asset file, to which the new material links.


The new material will be created at the same hierarchy level as the original one. Note that the child materials won't be cloned.


If you copy a material file via the [Asset Browser](../../../editor2/assets_workflow/assets_organize.md#copy), the material that links to it will be cloned.


### Deleting a Material


To delete a material, right-click it, choose *Delete* in the drop-down list and confirm deletion in the dialog window that opens:


![](delete_material.gif)

*Deleting a Material*


Another way to delete a material is to select it and click ![](delete.png) to the left of the material name filter. If you delete a parent material, all its child materials will be deleted as well.


> **Notice:** Deleting a material leads deleting the asset file it is linked. You cannot undo material's deletion.


If you delete a material file via the [Asset Browser](../../../editor2/assets_workflow/assets_organize.md#remove), the material that links to it will be deleted as well.


## Setting Up Materials Inheritance


In UNIGINE, materials are organized in a [hierarchy](../../../content/materials/inheritance.md), like [nodes](../../../editor2/organizing_nodes/index.md#reparent_node), but are completely independent of the nodes hierarchy. Each material (*parent material*) can have multiple children (*child materials*). The parent material can be both the [base](../../../content/materials/index.md#base_materials) or [user material](../../../content/materials/index.md#user_materials); the child material is always a user material.


To collapse or expand the list of child materials, click the *arrow* to the left of the parent material. You can also collapse all child materials in the Materials Hierarchy window by clicking ![](collapse.png).


### Inheriting a Material


Inheriting one material from another allows forming the materials hierarchy. To inherit a new material from the existing one, right-click the desired parent material and choose *Create Child* in the drop-down list.


![](inherit_material.gif)

*Inheriting a Material*


Another way to inherit a material is to select a material and click ![](inherit.png) to the right of the material name filter.


> **Notice:** Inheriting a material leads to creating a new asset file.


You can also inherit a new material via the *Parameters* window: select a surface, go to the [Material](../../../editor2/node_parameters/visual_representation/index.md#surface_material) section and click ![](inherit.png) right to the field with the material name. The inherited material will be assigned to the currently selected surface automatically.


> **Notice:** The child material asset is created in the same folder as the parent material asset. If the material is inherited from the base material, the asset will be created in the root of the `asset` folder.


#### Inheriting via Asset Browser


To inherit a material via the Asset Browser, select the material asset, right-click it and choose *Create Child* in the drop-down list. The new material will be added to the Materials Hierarchy window and linked to the created asset.


![](inherit_asset.gif)

*Inheriting a Material via Asset Browser*


### Reparenting a Material


To change the parent material (reparent), select the target material in the hierarchy and drag it with the **left mouse button** pressed to the desired parent.


![](reparent_material.gif)

*Reparenting a Material*


The parent material, to which the child material will be added, is highlighted with the *white frame*:


![](move_to_parent.png)

*Highlighted Parent Material*


You can also move the material to a position alongside the child materials of the desired parent: the material will be added as a child to this parent material in alphabetical order. The position in the hierarchy is highlighted with the *white line* during moving.


![](move_alongside_children.png)

*Reparenting a Material*


## Assigning a Material


A material can be assigned to the entire node (i.e., to all its surfaces), several surfaces or a single surface of the node.


To assign a material to a surface (or surfaces) of a node, select the node, select the [target surface](../../../editor2/node_parameters/visual_representation/index.md) (surfaces) and perform one of the following:


> **Notice:** To assign a material to the entire node, selecting the node will be enough: the material will be assigned to all its surfaces.


- Drag the material from the Materials Hierarchy window or the icon of the material asset from the Asset Browser to the [field with the material asset name](../../../editor2/node_parameters/visual_representation/index.md#surface_material) in the *[Parameters](../../../editor2/node_parameters/index.md)* window. ![](drag_to_material_field.png)
- Drag the material from the Materials Hierarchy window or the icon of the material asset from the Asset Browser to the target surface in the Editor Viewport. ![](drag_to_surface.png)
- Use the button next to the [field with the material asset name](../../../editor2/node_parameters/visual_representation/index.md#surface_material) in the *[Parameters](../../../editor2/node_parameters/index.md)* window (the *Node* tab) to choose the desired material asset. ![](set_material_button.png)
- Type the name of the material asset to the [field with the material asset name](../../../editor2/node_parameters/visual_representation/index.md#surface_material) in the *[Parameters](../../../editor2/node_parameters/index.md)* window (the *Node* tab) manually. If an asset with the specified name exists in the project, it will be shown in the drop-down list while typing. ![](set_material_manually.gif)


## Filtering Materials


Filtering helps to reduce the number of materials viewed in the hierarchy, and, therefore, simplifies its management.


To filter materials *by name*, start typing a material name in the corresponding field of the Materials Hierarchy window:


![](filter_by_name.gif)


Materials in the hierarchy can also be displayed depending on the specified filters: click ![](filter_icon.png) in the *Materials Hierarchy* window and choose the required filters. By default, all materials are shown (*Enable All* is toggled on).


![](filters.png)

*Available Filters*


The filters are divided into several groups, so you can:


- Filter the materials *by types of objects*, to which they can be applied. For example, you can toggle on the *Grass* filter to show materials that can cover the Grass object.
- Display or hide the materials implemented programmatically (the *Code-Based* filter) and/or created via [Materials Editor](../../../content/materials/graph/index.md) (the *Material Graph* filter).
- Display or hide the *Built-In Engine Base Materials* and/or *Users Created Base Materials*.
- Filter the materials *by their properties*. For example, you can show all materials with *Emission*.
- Filter by *Detail* rendering parameters.
- Filter by *UV mapping* parameters.


To filter the materials, toggle checkboxes in the *Visibility* column. Each filter can have one of the following values:


- enabled - all materials that match the filter are displayed in the hierarchy.
- NOT enabled - all materials that don't match the filter are displayed.
- disabled - the filter isn't taken into account.


Filters can be combined using *logical OR* or *logical AND* operations. For example, to display the opaque materials with detail rendering disabled that can be applied to a mesh, you should use the following combination of filters with logical AND:


![](filter_example.png)


You can also display filter states in the materials hierarchy: toggle on the corresponding checkboxes in the *States* column. The materials hierarchy will switch to a table view. If the displayed material matches the filter, it will have a mark in the corresponding column.


![](filter_states.png)


You can sort the materials by state by clicking the column header.
