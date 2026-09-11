# Materials Conversion


## Manual Reparent from mesh_base to Graph


If you have a material inherited from the [mesh_base](../../../../content/materials/library/mesh_base/index.md) parent material and you want it to derive from a [graph-based](../../../../content/materials/graph/index.md) material, you need to make a reparenting.


> **Warning:** Before you start reparenting we strongly recommend you to make a backup of your projects or use a Version Control System.


If the names of parameters in the new base graph material are the same as in the old `mesh_base` all the previous values will be set for them automatically. Here is the list of the most common parameters that were used in the default `mesh_base` material:


> **Notice:** The parameters in your new base graph material must be named exactly like that (including the case) in order for reparent to work properly and keep parameter values.


<details>
<summary>Show the list of the most common parameters | Close</summary>

1. Common

  1. albedo
  2. albedo_color
  3. metalness
  4. roughness
  5. specular
  6. microfiber
  7. auxiliary
  8. translucent
  9. displacement
  10. tesselation_density_map
  11. ambient_occlusion
  12. diffuse_color
  13. specular_color
  14. gloss
  15. normal_scale
  16. translucent
  17. transparent
  18. transparent_pow
  19. opacity_fresnel
  20. opacity_fresnel_pow
  21. uv_transform
  22. ao_uv_transform
  23. triplanar_blend
  24. mip_bias
2. Detail

  1. detail_diffuse
  2. detail_albedo
  3. detail_normal
  4. detail_mask
  5. detail_albedo_color
  6. detail_metalness
  7. detail_roughness
  8. detail_specular
  9. detail_microfiber
  10. detail_diffuse_color
  11. detail_specular_color
  12. detail_gloss
  13. detail_uv_transform
  14. detail_triplanar_blend
  15. detail_visible
  16. detail_visible_threshold
  17. detail_albedo_color_visible
  18. detail_metalness_visible
  19. detail_roughness_visible
  20. detail_specular_visible
  21. detail_microfiber_visible
  22. detail_diffuse_color_visible
  23. detail_specular_color_visible
  24. detail_gloss_visible
  25. detail_normal_visible
  26. detail_mask_uv_transform
  27. detail_mask_triplanar_blend
  28. detail_angle_fade
  29. detail_angle_fade_threshold
3. Emission

  1. emission_color
  2. emission_scale
  3. emission_uv_transform
  4. emission_triplanar_blend
4. Bevel

  1. bevel_scale
  2. bevel_uv_transform
  3. bevel_triplanar_blend
5. Curvature

  1. curvature_scale_cavity
  2. curvature_scale_convexity
  3. curvature_uv_transform
6. Parallax

  1. parallax_scale
  2. parallax_min_layers
  3. parallax_max_layers
  4. parallax_noise
  5. parallax_cutout_uv_transform
7. Tessellation

  1. tessellation_smoothness
  2. tessellation_scale
  3. tessellation_vector_scale
  4. tessellation_mid_point
  5. tessellation_texture_exp
  6. tessellation_shadow_offset
  7. tessellation_factor
  8. tessellation_density
  9. tessellation_shadow_factor
  10. tessellation_shadow_density
  11. tessellation_distance_falloff_near
  12. tessellation_distance_falloff_far
  13. tessellation_distance_falloff_exp
  14. tessellation_distance_falloff_max_mip
  15. tessellation_culling_near
  16. tessellation_culling_back_face
  17. tessellation_culling_screen_border
  18. tessellation_shadow_culling_back_face
  19. tessellation_shadow_culling_screen_border
8. Refraction

  1. refraction_ior
  2. refraction_ray_length
  3. refraction_normal_map
9. Noise 2D

  1. noise_2d_scale
  2. noise_2d_uv_transform
10. Noise 3D

  1. noise_3d_scale
  2. noise_3d_transform
11. Planar Reflection

  1. reflection_viewport_mask
  2. reflection_distance
  3. reflection_distance_scale
  4. reflection_pivot_rotation
  5. reflection_pivot_offset

</details>


There are the following ways to manually reparent a material:


- Use the [reparent feature](../../../../editor2/materials_settings/organizing_materials/index.md#reparent_material) in the *Materials* window of *UnigineEditor*. To reparent select the material(s) inherited from the `mesh_base` in the hierarchy and drag it with the left mouse button pressed to the desired graph-based material. ![](reparent.gif)
- The alternative way to reparent materials is via the ***Ctrl + P*** hotkey (first selected materials wll be reparented to the last one selected before the hotkey was pressed).


After reparenting the old materials are deleted and the new ones are created in place of them. Now you can freely rename the parameters in the newly reparented graph materials.


## Converting to Unique Graph


If you want to make some material inherited from `mesh_base` into a unique graph material at the top level of hierarchy, you must reparent it to some graph base material and then in the context menu (available on the right mouse click) select *Convert To Unique Graph*.


![](unique.png)


> **Warning:** In this case, the material will be turned into a default template material and **won't preserve previous parameters and any logic**. We are working on a smart conversion which must be available later.
