# Stars Generator for Billboards


Stars generator allows creating a starry night sky, with stars drawn fast on *[Billboards](../../../../objects/objects/billboards/index.md)*. It is found in the *Node* tab -> *Stars* section of a *Billboards* object.


![Billboards with stars](stars.png)

*Billboards with stars*


## How to Create Stars Billboards


To create the stars billboards, follow these steps:


1. Add the *[Billboards](../../../../objects/objects/billboards/index.md#create)* node.
2. In the *Node* tab of the *[Parameters](../../../../editor2/node_parameters/index.md)* window, go to the *Stars* section and specify a FK5 stars catalog (the Fifth Fundamental Catalogue) in the [Catalog](#catalog) field. You can download, unpack, and use the following catalog file: [`catalog.zip`](https://documentation-api.unigine.com/en/docs/future/objects/objects/billboards/billboards_stars/./catalog.zip).
3. Make sure that the [Radius](#radius) of the created sphere with stars is not bigger than the camera's far clipping plane (*Camera Settings -> [Far clipping](../../../../editor2/camera_settings/index.md#far)*). Otherwise, stars will not be seen.
4. Click *[Generate](#create)* to create billboards.
5. Click *[Texture](#texture)* and choose a location to save a texture atlas with stars.
6. Create a material for billboards with stars:

  1. Inherit a material from *billboards_base_stars* and assign it to the *Billboards* object.
  2. Go to the *[Textures](../../../../editor2/materials_settings/index.md#textures_tab)* tab of the *Parameters* window and load a *diffuse* texture: select the previously saved stars texture.
7. After changing any parameter in the stars generator, click *[Generate](#create)* to reload the diffuse texture.


## Options


![](stars_tab.png)


| Count | The maximum number of billboards to create. If there are fewer stars in the loaded catalog, fewer billboards will be created. |
|---|---|
| Radius | Radius of the sphere with stars billboards. > **Notice:** - To see the stars, the *Radius* should be smaller than the camera's far clipping plane (*Camera settings -> [Far clipping](../../../../editor2/camera_settings/index.md#far)*). > - For big worlds, the stars *Billboards* object should also be attached to the camera (made a child node of the [player](../../../../api/library/players/class.player_cpp.md)) to avoid any clipping. |
| Angle | The angular diameter of stars: the higher the value, the bigger the stars. |
| Catalog | Load a FK5 stars catalog. |
|  |  |
| Latitude | Latitude of the point to view the star sky from. |
| Longitude | Longitude of the point to view the star sky from. |
| Location | Choose a city to view the star sky from. |
|  |  |
| Generate | Generate stars billboards and reload the diffuse texture, if it is set in the [Material settings](#set_texture). |
| Texture | Save an atlas texture for stars billboards based on the loaded [catalog](#catalog). |
