# Billboards


The *Billboards* object consists of a number of billboard elements. A **billboard** is a rectangular flat object that always faces the camera. The *Billboards* is used instead of fully functional objects that are barely seen from far off and slightly change their position when the camera moves around them (e.g. clouds, stars, far away forests). Using *Billboards* helps to simplify and speed up rendering.


For example, when you are adding a tree that is hardly seen from a distance, instead of creating a complex tree mesh, just put an appropriate texture onto the alpha-tested *Billboards* and it will make no visual difference at such a range.


![Billboards](billboards.jpg)

*Billboards*


In the *Create* menu you will see three options each creating a *Billboards* object used for a specific purpose and having a specific material assigned:


- **Base** - used for groups of billboards (*[billboards_base](../../../content/materials/library/billboards_base/index.md)* material)
- **Impostor** - used as an optimization for [impostors](../../../editor2/tools/impostors_creator/index.md) to be rendered, for example, instead of a *[Cluster](../../../objects/objects/mesh_cluster/index.md)* object at large distances (*Billboards* are simpler and less performance-consuming). In this case the *[billboards_impostor_base](../../../content/materials/library/billboards_impostor_base/index.md)* material is assigned, it is a base material for impostors, that supports sampling different regions of textures based on viewing angle.
- **Cloud** - intended to simulate simple shaded clouds (*[billboards_cloud_base](../../../content/materials/library/billboards_cloud_base/index.md)* material)


These materials have different parameters and are rendered differently based on their applications, you can find more details in the articles listed below, and check out the **[Billboards](../../../content/samples/main_samples/billboards.md)** sample from the **[Art Samples](../../../content/samples/index.md)** suite included in the SDK.


### See Also


- The article on the *[billboards_base](../../../content/materials/library/billboards_base/index.md)* material.
- The article on the *[material_billboards_impostor_base](../../../content/materials/library/billboards_impostor_base/index.md)* material.
- The article on the *[billboards_cloud_base](../../../content/materials/library/billboards_cloud_base/index.md)* material.


## Creating Billboards


To create *Billboards*, perform the following steps:


1. On the Menu bar, click *Create -> Billboards -> Base*. ![](billboards_create.png)
2. Place the *Billboards* object somewhere in the world.
3. Specify the [*Billboards* parameters](#billboards_param).


## Billboards Parameters


![](params_tab.png)


| Depth Sort | Indicates that billboards should be sorted in back-to-front order according to their position. This option should be enabled, if [alpha blending](../../../principles/render/blending/index.md) is used for the billboard material (except for the additive blending). |
|---|---|


## Billboards Options


In the *Billboards* section of the *Node* tab, you can create new billboards and tweak their settings.


![](billboards_tab_header.png)


| Add from Children | Adds all billboards from identical children objects to the list in the parent billboard and removes the added children from the *World Nodes* hierarchy. |
|---|---|
| Add | Adds a new billboard. After a new billboard is created, it can be selected in the list of billboards in the *Node* tab and repositioned using a standard manipulator. ![Repositioning a separate billboard](reposition.jpg) |
| Remove | Removes a billboard selected in the list. |
| Clear | Removes all billboards from the list. |


![](billboards_tab.png)


| Position | Moves the billboard along X, Y and Z axes, respectively. |
|---|---|
| Normal | Sets the X, Y and Z coordinates of the billboard's normal vector. Is used to orient the billboard. Works only with the *[billboards_impostor_base](../../../content/materials/library/billboards_impostor_base/index.md)* material. |
| ScaleX ScaleY | Scale values scale the texture on the selected billboard along X and Y axes, for example: - If *ScaleX* is set to 2, there will be two texture tiles widthways. |
| TranslateX TranslateY | Translate values offset the texture on the selected billboard along X and Y. With these parameters, an arbitrary point of the texture can be set as the top left corner of the billboard, for example: - If *TranslateX* is set to 0.5, the texture is repositioned to the left (so that the edge of the texture is rendered in the center of the billboard). |
| Width | Width of the rectangle for the selected billboard. |
| Height | Height of the rectangle for the selected billboard. |
| Angle | Angle to orientate the selected billboard. ![Angle](angle.jpg) |


![](axis.png)


| Axis | Sets the basis for the *Billboards* object's Z axis: - World Z - the *Billboards* object uses a world space orientation. - Local Z - the *Billboards* object uses a local space orientation. |
|---|---|
| Drop All to the Ground | Positions all billboards to the surface below them. |


## Generator


Generator allows you to automatically create a specified number of billboards and randomly scatter them within an arbitrary mesh volume. After that, they will appear in the list in the *Billboards* section of the *Node* tab and can be repositioned, if necessary. If a texture atlas is used, each of the created billboards will be randomly assigned one of texture slots.


![](generator_tab.png)


| Count | The number of billboards to create and scatter. |
|---|---|
| Width | If a texture atlas is used, *Width* specifies the number of slots horizontally. If a simple texture is used, this value should be 1. |
| Height | If a texture atlas is used, *Height* specifies the number of slots vertically. If a simple texture is used, this value should be 1. |
| Radius Spread | The size of the square billboards to be created. *Spread* value defines the range for possible variation of the Radius: - The higher the value, the more varying size the created billboards will have. (See how it is calculated in detail [here](../../../objects/objects/grass/index.md#spread).) - If set to 0, all billboards will be of equal size. |
| Aspect Spread | The ratio of width to height. This option is used to create rectangular billboards. - If *Aspect* is set to 0.5, the width of the billboards will be twice their height. - If *Aspect* is set to 2, the height of the billboards will be twice their width. *Spread* value defines the range for possible variation of the *Aspect*: - The higher the value, the more varying aspects the created billboards will have. (See how it is calculated in detail [here](../../../objects/objects/grass/index.md#spread).) - If set to 0, all billboards will be of equal (square) size. |
| Angle Spread | Angle of orientation. *Spread* value defines the range for possible variation of the *Angle*: - The higher the value, the more differently the created billboards will be oriented. (See how it is calculated in detail [here](../../../objects/objects/grass/index.md#spread).) - If set to 0, all billboards will stand straight. |
| Bound | A mesh that determines the volume within which billboards will be generated. The mesh itself is not rendered. |
| Generate | Create new billboards and scatter them within the mesh volume. If a texture atlas is used, each of the created billboards will be randomly assigned one of the texture slots. |
