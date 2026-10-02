# Material Graph Examples

Every graph below is a working `.mgraph` taken from the UNIGINE art samples, next to a description derived from the file itself. Copy the closest one and adapt it - see [README.md](README.md) for how the format works.

## Material examples

One graph per shading technique, from the Material Graph samples in the UNIGINE art samples. Each is a self-contained demonstration of one thing.

- [blackbody_box](examples/material_examples/blackbody/blackbody_box.md): This example demonstrates how to implement simulation of blackbody radiation for physically accurate emissive materials.
- [blackbody_rifle](examples/material_examples/blackbody/blackbody_rifle.md): This example demonstrates how to implement simulation of blackbody radiation for physically accurate emissive materials.
- [blend_by_height](examples/material_examples/blend_by_height/blend_by_height.md): This example demonstrates how to perform blending based on heightmaps when creating materials.
- [boiling](examples/material_examples/boiling/boiling.md): This example demonstrates creation of a complex effect of boiling liquid featuring tessellation and vertex offset control.
- [clear_coat_base](examples/material_examples/clear_coat/clear_coat_base.md): This example illustrates how to create materials having two physical layers such as car paint, carbon, metal, or wood covered with varnish.
- [combobox_example](examples/material_examples/combobox/combobox_example.md): This example demonstrates how to use comboboxes in your materials.
- [cube_map_texture_reflection_vector](examples/material_examples/cubemap_texture/cube_map_texture_reflection_vector.md): This example demonstrates the creation of materials applying custom cubemap textures for reflective and refractive materials.
- [cube_map_texture_refraction_vector](examples/material_examples/cubemap_texture/cube_map_texture_refraction_vector.md): This example demonstrates the creation of materials applying custom cubemap textures for reflective and refractive materials.
- [custom_code](examples/material_examples/custom_code/custom_code.md): This example demonstrates how to create and use nodes containing a custom shader code.
- [test_subgraphs](examples/material_examples/custom_subgraphs/test_subgraphs.md): This example demonstrates how to create Subgraphs and use them in your Material Graphs.
- [decal_mesh_inflation](examples/material_examples/decal_mesh_inflation/decal_mesh_inflation.md): This example demonstrates how to implement Geometry Inflation based on camera distance for Mesh Decals. The technique helps preserve visibility for very thin elements when TAA is enabled. For 3D objects (e.g., lampposts, pipes, ropes, cables, antennas, etc.), it works by offsetting vertices along their normal vectors, making them appear slightly thicker as they move farther away from the camera. For meshes see the Geometry Inflation sample.
- [material_graph_decal_base](examples/material_examples/decal_mesh_inflation/material_graph_decal_base.md): This example demonstrates how to implement Geometry Inflation based on camera distance for Mesh Decals. The technique helps preserve visibility for very thin elements when TAA is enabled. For 3D objects (e.g., lampposts, pipes, ropes, cables, antennas, etc.), it works by offsetting vertices along their normal vectors, making them appear slightly thicker as they move farther away from the camera. For meshes see the Geometry Inflation sample.
- [dissolve](examples/material_examples/dissolve/dissolve.md): This example demonstrates how to create an Alpha Test material with a dissolve effect.
- [energy_shield](examples/material_examples/energy_shield/energy_shield.md): This example demonstrates how to implement an effect of an animated energy shield.
- [base_white](examples/material_examples/fade_by_depth/base_white.md): This example demonstrates how to implement an effect of fading by depth.
- [fade_by_depth](examples/material_examples/fade_by_depth/fade_by_depth.md): This example demonstrates how to implement an effect of fading by depth.
- [lava](examples/material_examples/flowmap/lava.md): Using the Flowmap Panner node to create a lava flow.
- [flowmap_demonstration](examples/material_examples/flowmap_river_and_vortex/flowmap_demonstration.md): Using the Flowmap Panner node to create rivers, and vortexes.
- [river_water](examples/material_examples/flowmap_river_and_vortex/river_water.md): Using the Flowmap Panner node to create rivers, and vortexes.
- [fresnel_effect](examples/material_examples/fresnel_effect/fresnel_effect.md): This example demonstrates how to implement the Fresnel effect with respect to a normal map used when creating materials.
- [glass_blend_mode_add](examples/material_examples/glass/glass_blend_mode_add.md): This example demonstrates different implementations of glass materials for different needs.
- [glass_blend_mode_refraction_thick](examples/material_examples/glass/glass_blend_mode_refraction_thick.md): This example demonstrates different implementations of glass materials for different needs.
- [glass_blend_mode_refraction_thin](examples/material_examples/glass/glass_blend_mode_refraction_thin.md): This example demonstrates different implementations of glass materials for different needs.
- [glass_thick_colored_low_quality](examples/material_examples/glass/glass_thick_colored_low_quality.md): This example demonstrates different implementations of glass materials for different needs.
- [hair_base](examples/material_examples/hair_shading/hair_base.md): This sample illustrates how to create hair or fur.
- [hair_temporal_filter](examples/material_examples/hair_shading/hair_temporal_filter.md): This sample illustrates how to create hair or fur.
- [ice](examples/material_examples/ice/ice.md): This example demonstrates how to create an effect of a multi-layered ice material.
- [parallax_interior_materials](examples/material_examples/interior_mapping/parallax_interior_materials.md): This example demonstrates how to create the effect of parallax interior mapping when creating materials.
- [interior_mapping_cubemap](examples/material_examples/interior_mapping/interior_mapping_cubemap.md): This example demonstrates how to create the effect of parallax interior mapping when creating materials.
- [interior_mapping_texture2d](examples/material_examples/interior_mapping/interior_mapping_texture2d.md): This example demonstrates how to create the effect of parallax interior mapping when creating materials.
- [loop](examples/material_examples/loop/loop.md): This example demonstrates how to use loops when creating materials.
- [dragon_tesselation_quality](examples/material_examples/materials_quality/dragon_tesselation_quality.md): This example illustrates the Materials Quality feature enabling you to apply a certain set of features inside graph-based materials connected to the corresponding input of a Material Quality Switch node depending on the quality level selected globally.
- [melting_base](examples/material_examples/melting/melting_base.md): This example demonstrates how to create an effect of a melting geometry.
- [layered_material](examples/material_examples/multi_layered_material/layered_material.md): This example illustrates how to create a material combining several layers.
- [procedural_damaged_building](examples/material_examples/multi_layered_material/procedural_damaged_building.md): This example illustrates how to create a material combining several layers.
- [two-layered_material](examples/material_examples/multi_layered_material/two-layered_material.md): This example illustrates how to create a material combining several layers.
- [normal_from_height_texture](examples/material_examples/normal_from_height_texture/normal_from_height_texture.md): This example demonstrates how to convert a height value from a height texture to normals.
- [normal_from_height_value](examples/material_examples/normal_from_height_value/normal_from_height_value.md): This example demonstrates how to convert height values to normal vectors.
- [normal_map_object_space](examples/material_examples/normal_map_object_space/normal_map_object_space.md): This example demonstrates how to use object-space normal maps.
- [normal_map_tangent_space](examples/material_examples/normal_map_tangent_space/normal_map_tangent_space.md): This example demonstrates how to use tangent-space normal maps.
- [material_graph](examples/material_examples/panner/material_graph.md): This example demonstrates how to create a simple UV-panner to animate UV coordinates in a material.
- [portals](examples/material_examples/portals/portals.md): This example demonstrates how to use portals in your materials.
- [procedural_tiles_base](examples/material_examples/procedural_tiles/procedural_tiles_base.md): This example demonstrates how to create a procedurally damaged tiled material with two layers.
- [rain](examples/material_examples/rain/rain.md): This example demonstrates how to create an effect of raindrops on a surface.
- [roughness_correction_by_ramp](examples/material_examples/ramp_r_texture/roughness_correction_by_ramp.md): This example illustrates imitation of scratches and curve-based intensity adjustment for a single-channel texture using the Texture Ramp R node.
- [chameleon_paint_by_ramp](examples/material_examples/ramp_rgb_texture/chameleon_paint_by_ramp.md): This example illustrates imitation of the chameleon paint and curve-based color correction using the Texture Ramp RGB node.
- [color_correction_by_ramp](examples/material_examples/ramp_rgb_texture/color_correction_by_ramp.md): This example illustrates imitation of the chameleon paint and curve-based color correction using the Texture Ramp RGB node.
- [uv_tiling_and_offset](examples/material_examples/uv_tiling_and_offset/uv_tiling_and_offset.md): This example demonstrates how to implement UV adjustment (tiling and offset) in a material.
- [air_dencer_va_mat](examples/material_examples/vertex_animation/air_dencer_va_mat.md): This example demonstrates how to use a vertex animation texture in UNIGINE.
- [vertex_color_albedo](examples/material_examples/vertex_color/vertex_color_albedo.md): This example demonstrates how to use vertex color for texture blending when creating materials.
- [vertex_color_test](examples/material_examples/vertex_color/vertex_color_test.md): This example demonstrates how to use vertex color for texture blending when creating materials.
- [all_types_of_data](examples/material_examples/custom_subgraphs/all_types_of_data.md): This example demonstrates how to create Subgraphs and use them in your Material Graphs.
- [uv panner](<examples/material_examples/custom_subgraphs/uv panner.md>): This example demonstrates how to create Subgraphs and use them in your Material Graphs.

## Base materials

The production graphs the art sample scenes are actually built on, from `showcase_content/materials/base_materials` in the art samples repository. They are project assets of that showcase, not part of the SDK core, so a fresh project does not have them - read them as reference for how a complete PBR graph is assembled and copy from them, rather than trying to inherit from them. `pbr_base` alone is the parent of 100 of the showcase's 256 materials, so it is the closest thing here to a full, real-world graph.

- [decal_simple](examples/base_materials/decal_simple.md)
- [geometry_inflation](examples/base_materials/geometry_inflation.md)
- [grass_animation_base](examples/base_materials/grass_animation_base.md)
- [pbr_alphablend_base](examples/base_materials/pbr_alphablend_base.md)
- [pbr_alphatest_base](examples/base_materials/pbr_alphatest_base.md)
- [pbr_alphatest_spherelized_normals_base](examples/base_materials/pbr_alphatest_spherelized_normals_base.md)
- [pbr_alphatest_two_sided_base](examples/base_materials/pbr_alphatest_two_sided_base.md)
- [pbr_auxiliary_base](examples/base_materials/pbr_auxiliary_base.md)
- [pbr_base](examples/base_materials/pbr_base.md)
- [pbr_detail_alphablend_base](examples/base_materials/pbr_detail_alphablend_base.md)
- [pbr_detail_multiply_base](examples/base_materials/pbr_detail_multiply_base.md)
- [pbr_detail_overlay_base](examples/base_materials/pbr_detail_overlay_base.md)
- [pbr_emission_base](examples/base_materials/pbr_emission_base.md)
- [pbr_geometry_inflation_base](examples/base_materials/pbr_geometry_inflation_base.md)
- [pbr_microfiber_base](examples/base_materials/pbr_microfiber_base.md)
- [pbr_parallax_base](examples/base_materials/pbr_parallax_base.md)
- [pbr_parallax_depth_offset_base](examples/base_materials/pbr_parallax_depth_offset_base.md)
- [pbr_retroreflection_base](examples/base_materials/pbr_retroreflection_base.md)
- [pbr_tessellation_base](examples/base_materials/pbr_tessellation_base.md)
- [pbr_triplanar(os)_tessellation_base](<examples/base_materials/pbr_triplanar(os)_tessellation_base.md>)
- [pbr_triplanar(ws)_tessellation_base](<examples/base_materials/pbr_triplanar(ws)_tessellation_base.md>)
- [pbr_triplanar_base](examples/base_materials/pbr_triplanar_base.md)
- [pbr_two_sided_base](examples/base_materials/pbr_two_sided_base.md)
- [tree_animation_base](examples/base_materials/tree_animation_base.md)
- [ui_transparent_base](examples/base_materials/ui_transparent_base.md)
- [ui_unlit_base](examples/base_materials/ui_unlit_base.md)
- [ui_unlit_surface_custom_texture](examples/base_materials/ui_unlit_surface_custom_texture.md)
