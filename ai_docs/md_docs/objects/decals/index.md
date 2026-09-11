# Decals


A **decal** is a material projection on the surface. In fact, decals perform changing material parameters of the surface on which these decals are projected. It allows you to add a lot of additional details at basically no performance cost. Decals are rendered in buffers (they change buffer textures) and work only with deferred objects. A decal is a perfect object for bullet holes, bloodstains, ashes, etc.


Decals support two materials only: *[decal_base](../../content/materials/library/decal_base/index.md)* and *[decal_terrain_hole_base](../../content/materials/library/decal_terrain_hole_base/index.md)*. While the behavior of decals with the first material applied is similar to [detail textures](../../content/materials/library/mesh_base/index.md#option_detail) of the material, the second type of decals is intended for creating [Decal-Based Terrain Holes](../../objects/objects/terrain/terrain_global/index.md#decal_holes).


By using *[Water Decal](../../content/materials/library/decal_base/index.md#option_water_decal)* option, decals can be displayed on the top of the water surface. This option can be used to create different effects on the water surface: floating branches, leaves, etc.


![](decal_main.png)

*Projected Decal with normal map*


### Types of Decals


UNIGINE features the following types of decals:


- [![](ortho.png)](../../objects/decals/ortho/index.md) � **[Orthographic Decal](../../objects/decals/ortho/index.md)** is a decal projected onto a surface by means of orthographic projection.
- [![](proj.png)](../../objects/decals/proj/index.md) � **[Projected Decal](../../objects/decals/proj/index.md)** is a decal projected onto a surface by means of the perspective projection.
- [![](mesh.png)](../../objects/decals/mesh/index.md) � **[Mesh Decal](../../objects/decals/mesh/index.md)** is a decal based on the arbitrary `.mesh` file and projected onto a surface by means of the orthographic projection.


### See Also


- API classes to manage decals:

  - *[Decal](../../api/library/decals/class.decal_cpp.md)*
  - *[DecalMesh](../../api/library/decals/class.decalmesh_cpp.md)*
  - *[DecalOrtho](../../api/library/decals/class.decalortho_cpp.md)*
  - *[DecalProj](../../api/library/decals/class.decalproj_cpp.md)*
- The article on [Creating Decal-Based Terrain Holes](../../objects/objects/terrain/terrain_global/index.md#decal_holes)
