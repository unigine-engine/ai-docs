# Volumetric Objects


Volumetric objects are used to simulate different kinds of volumes depending on their materials:


- Visible light volumes (they are not light sources, therefore, they don't illuminate the scene):

  - [Spheres](../../../content/materials/library/volume_light_base/index.md) of light around omnidirectional light sources
  - [Beams](../../../content/materials/library/volume_proj_base/index.md) from directional light sources
  - [Light volumes](../../../content/materials/library/volume_omni_base/index.md) around flat light emitters
  - [Sun beams](../../../content/materials/library/volume_shaft_base/index.md) falling into a room through openings
- [Fog](../../../content/materials/library/volume_fog_base/index.md) that obscures objects inside its volume
- [Clouds](../../../content/materials/library/volume_cloud_base/index.md) or shaped fog


## Types of Volumetric Objects


There are four possible shapes for volumetric objects:


- [Box](../../../objects/effects/volumetrics/volume_box.md)
- [Sphere](../../../objects/effects/volumetrics/volume_sphere.md)
- [Omni](../../../objects/effects/volumetrics/volume_omni.md)
- [Proj](../../../objects/effects/volumetrics/volume_proj.md) (Projected)


To create various effects described above, you need to assign them different materials. Some materials can be assigned only to one type of volumetric objects.


![Volumetric objects](volumetrics.jpg)

*Volumetric lights, fog and shafts*


## See also


- *[volume_cloud_base](../../../content/materials/library/volume_cloud_base/index.md)* material
- *[volume_fog_base](../../../content/materials/library/volume_fog_base/index.md)* material
- *[volume_light_base](../../../content/materials/library/volume_light_base/index.md)* material
- *[volume_omni_base](../../../content/materials/library/volume_omni_base/index.md)* material
- *[volume_proj_base](../../../content/materials/library/volume_proj_base/index.md)* material
- *[volume_shaft_base](../../../content/materials/library/volume_shaft_base/index.md)* material
