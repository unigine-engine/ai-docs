# Subgraphs the SDK Ships

60 ready-made node groups under `data/core/subgraphs/` in the SDK. They are part of core, so every project has them - nothing to install and nothing to copy.

**Check this list before building an effect out of raw math nodes.** Fresnel, blend by height, flipbook animation, grass animation, blackbody radiation, depth fade and triplanar projection are all here already, and using one is a single node instead of a dozen.

This is a lookup table, not documentation: 56 of the 60 are already described in the SDK's own node library pages, linked from the name column. The two columns beside it are the ones nothing else carries.

## How to use one

A subgraph is a `SubGraph` node whose single prop names the asset:

```json
"SubGraph": {
  "label": "Fresnel",
  "guid": "<fresh 40 hex, unique in your file>",
  "x": 400, "y": 200,
  "props": {
    "prop": {
      "label": "",
      "widget": "SubGraph",
      "asset": "3c754d9912973dd2c9dce4d48a9d3f51312071d6"
    }
  }
}
```

The `asset` guid is the one in the table below. It comes from the asset's `.meta` in the SDK core, ships with the SDK and is the same in every project, so write it verbatim - this is the one guid in a graph you copy rather than invent.

Link to it by the pin labels in the table: `"input_label": "Power"`, `"output_label": "Fresnel"`. A `SubGraph` node takes its pins from the asset, so those labels are the whole interface.

## Reading one

Every file here is a `.msubgraph`, the same JSON as a `.mgraph`. Open it to see how the effect is built - that is often the fastest way to learn a technique, and you can copy the internals into your own graph instead of instantiating the subgraph if you need to change them.

**The files are in the SDK, at `<sdk>/data/core/subgraphs/<name>.msubgraph`.** A project has no `data/core/subgraphs/` folder - it has the packed `core.ung` instead - so read the SDK copy.

Reading one is also the only way to settle what a pin means when the label is not enough. `depth to position` takes a pin called `Depth`, and nothing says whether that is native or linear; open the file and the answer is there, a `SampleTexture` whose `texture_data` is `Native Depth`. Take the same route for any pin you are unsure of.

## The subgraphs

The **name** links the page the SDK documentation already has for that subgraph - that is where to read what it does and see a picture of it. What those pages do not carry is either column next to it: the asset guid lives in the `.meta` beside the asset, and the pins are buried in the `Inputs` and `Outputs` nodes inside the `.msubgraph` itself. Both are things a hand-written `SubGraph` node cannot be written without, which is all this table is for.

| name | asset guid | inputs | outputs | used in examples |
|---|---|---|---|---|
| [alpha fade noise taa](../md_docs/content/materials/graph/node_library/procedural/alpha_fade_noise_taa.md) | `80d1e2b1799c2f63e18b770f792638ae0750e6d0` | Screen Coord:int2, Tile Size:int | Noise:float |  |
| [angle between vectors](../md_docs/content/materials/graph/node_library/misc/angle_between_vectors.md) | `a35a8976220e49788165b299b0afca5ee85ea429` | Vector A:float3, Vector B:float3 | Radians:float, Degrees:float |  |
| [anisotropic specular brdf](../md_docs/content/materials/graph/node_library/misc/anisotropic_specular_brdf.md) | `18b5f8415198ed2802702d311d47872df5b18eda` | Roughness:float, Anisotrophy:float, Tangent World Space:float3, Half Vector World Space:float3, Normal World Space:float3 | Anisotropic Specular:float, Anisotropic Normal World Space:float3 |  |
| [blackbody](../md_docs/content/materials/graph/node_library/misc/blackbody.md) | `274020bbc113cedf2f832046e9635aa9caaa3700` | Temperature:float | Color:float3 | 4 |
| [blend by height simple](../md_docs/content/materials/graph/node_library/misc/blend_by_height_simple.md) | `ea3e7f80a1d9e45132a2aa14811c64e7e963499a` | Blend Mask:float, Heightmap:float, Contrast:float, Width:float | Result Blend Mask:float | 2 |
| [blend by height](../md_docs/content/materials/graph/node_library/misc/blend_by_height.md) | `869b93a8c2c6c495a0f9e792425e5366e9507b9b` | Height 0 (Avarage Color Should Be Gray):float, Height 0 Scale (In Meters):float, Height 1 (Avarage Color Should Be Gray):float, Height 1 Scale (In Meters):float, Blend Mask:float, Contrast:float | Result Blend Mask:float, Result Height:float | 1 |
| blinn brdf importance sampling | `53d486d9a3aec6901e025e209e6df17f08bd37e4` | Roughness:float, Normal Tangent Space:float3, Random Value (0-1):float2, index:int, Number Of Rays:float | Light Vector World Space:float3, Half Vector World Space:float3 |  |
| [blue noise 256x256 animated](../md_docs/content/materials/graph/node_library/procedural/blue_noise_256x256_animated.md) | `8bc20908bb22dfdcf9f686f0689cb844d596ad01` | Screen Coord:int2, Number Of Frames:int | Blue Noise Animated:float3 | 1 |
| [blue noise 256x256 static](../md_docs/content/materials/graph/node_library/procedural/blue_noise_256x256_static.md) | `03f81b072757c8707e5746e307ead86a23a6f825` | Screen Coord:int2, Frame:int | Blue Noise Static:float3 |  |
| [checker noise](../md_docs/content/materials/graph/node_library/procedural/checker_noise.md) | `4fa9f65b4522b11b5f61dc818029eac4b4b54871` | Screen_Coord:int2 | Checker Noise Animated (2 Frames):float, Checker Noise Static:float |  |
| [color_correction_by_ramp](../md_docs/content/materials/graph/node_library/misc/color_correction_by_ramp.md) | `29a15ea10e200aa6fb99f7d54cdb6328595bbdc0` | Source Color:float3, Texture Ramp RGB:TextureRamp | Result Color:float3 | 1 |
| [contrast](../md_docs/content/materials/graph/node_library/misc/contrast.md) | `22306c47e7640fd970bf5be2fbbaf578527fb259` | Value:float, Contrast (From -1 to 1):float | Clamped (From 0 to 1) Result:float, Unclamped Result:float | 4 |
| [curvature](../md_docs/content/materials/graph/node_library/misc/curvature.md) | `d31519db97a4c84dedcb3803b67282efa57bc191` | Radius:float, Softness:float, Threshold:float, Noise Intensity:float | Curvature:float |  |
| decal_mesh_inflation | `8664f53f4613ecc68a4a023cb8d7053968b34532` | Inflate U(0) / V(1):int, Inflation Scale:float, Inflation Min Threshold:float, Angle Inflation:bool, Angle Inflation Intensity:float, Angle Power:float, Inflation Max Threshold:float | Vertex Offset Tangent Space:float3 | 1 |
| [depth fade](../md_docs/content/materials/graph/node_library/misc/depth_fade.md) | `ee50574468f9623f6be967ed38e55972852470d5` | Fade Distance (In Meters):float | Opacity:float | 1 |
| [depth to position](../md_docs/content/materials/graph/node_library/misc/depth_to_position.md) | `23fe8b4e7a00d2ee3916309941a079fa2668f3f1` | Depth:float | Position Object Space:float3, Position View Space:float3, Position Absolute World Space:float3, Position Camera World Space:float3 |  |
| [fibonacci hemisphere](../md_docs/content/materials/graph/node_library/procedural/fibonacci_hemisphere.md) | `a5b0512c3589b320b82204101b422cfe55b21b46` | Index:int, Samples:int, Noise Intensity:float, Noise Pattern:float | Fibonacci Hemisphere Point:float3 |  |
| [fibonacci sphere](../md_docs/content/materials/graph/node_library/procedural/fibonacci_sphere.md) | `4329ca6256943cf28679edfb89693835f92cbd25` | Index:int, Samples:int, Noise Intensity:float, Noise Pattern:float | Fibonacci Sphere Point:float3 |  |
| [flipbook](../md_docs/content/materials/graph/node_library/misc/flipbook.md) | `21318ac8c8bb82dde9e8f536f458101d09a9c1de` | X Axis Tiles:int, Y Axis Tiles:int, Tile:int, UV:float2 | UV:float2 |  |
| [float_correction_by_ramp](../md_docs/content/materials/graph/node_library/misc/float_correction_by_ramp.md) | `bbe76bc4d1499cc251724701f52323be9054faf9` | Source Float:float, Texture Ramp R:TextureRamp | Result Float:float | 1 |
| [flowmap_panner](../md_docs/content/materials/graph/node_library/misc/flowmap_panner.md) | `e7419adf7d2eaa6f406e948c2db4d724055e565d` | Source Texture:Texture2D, FlowMap Texture (0-1):Texture2D, Source UV:float2, Source Tiling:float2, FlowMap UV:float2, FlowMap Tiling:float2, Phase 2 UV Offset:float2, Speed:float, ... | Color:float4, Color Contrast Preserving:float4, Normal (Tangent Space):float3, Normal Contrast Preserving (Tangent Space):float3, Phase 1 UV:float2, Phase 2 UV:float2, Blend Coefficient:float | 3 |
| [flowmap_panner_simple](../md_docs/content/materials/graph/node_library/misc/flowmap_panner_simple.md) | `933b56a6682dab3580a9567347af85d7b2147c42` | Source Texture:Texture2D, FlowMap Texture (0-1):Texture2D, Source UV:float2, Source Tiling:float2, FlowMap UV:float2, FlowMap Tiling:float2, Phase 2 UV Offset:float2, Speed:float, ... | Color:float4, Normal (Tangent Space):float3 |  |
| [fresnel pbr](../md_docs/content/materials/graph/node_library/misc/fresnel_pbr.md) | `dc2af6b912b5fae0fa1b9676dbcf896137663281` | Roughness:float, Specular:float, Normal Tangent Space:float3 | Fresnel:float | 2 |
| [fresnel](../md_docs/content/materials/graph/node_library/misc/fresnel.md) | `3c754d9912973dd2c9dce4d48a9d3f51312071d6` | Normal Tangent Space:float3, Power:float | Fresnel:float | 11 |
| geometry_inflation | `04b8fe8558827959bd94a47adfe1de7189ffbc00` | Inflation Min Threshold:float, Inflation Scale:float, Inflation Max Threshold:float | Vertex Offset Tangent Space:float3 | 1 |
| [get vector from basis](../md_docs/content/materials/graph/node_library/misc/get_vector_from_basis.md) | `10471d3c5f3fb84426e1723cbf5de167096a2196` | Axis X:float3, Axis Y:float3, Axis Z:float3, Vector:float3 | Result Vector:float3 |  |
| [ggx brdf importance sampling](../md_docs/content/materials/graph/node_library/misc/ggx_brdf_importance_sampling.md) | `8575fba9ad172d5c7c7da6001ca1eefafea0403b` | Roughness:float, Normal Tangent Space:float3, Random Value (0-1):float2 | Light Vector World Space:float3, Half Vector World Space:float3 |  |
| [grass animation](../md_docs/content/materials/graph/node_library/misc/grass_animation.md) | `c2fcec1878f92e186555caf1ed87611787fec199` | Wind Animation Tiling:float, Wind Animation Speed:float, Wind Animation Intensity:float, Wind Direction:float2, Wind Bend Intensity:float, Normal Tangent Space:float3, Object Height (In Meters):float, Vertex Position Object Space:float3 | Position Offset Tangent Space:float3, Normal Tangent Space:float3 | 1 |
| [hair shading](../md_docs/content/materials/graph/node_library/misc/hair_shading.md) | `514cc8316a3211182193338feb93664ed29f2573` | Albedo:float3, Normal (Tangent Space):float3, Tangent (Tangent Space):float3, Diffuse Roughness:float, Diffuse Ambient Occlusion:float, Specular Roughness:float, Specular Intensity:float, Specular Ambient Occlusion:float, ... | Emission:float3 | 1 |
| [hdri raymarched](../md_docs/content/materials/graph/node_library/misc/hdri_raymarched.md) | `c854be5d6f634dfef3dc918633fca09c35fa13f8` | Cubemap:TextureCube, Step Size:float, Threshold:float, Noise Rays:float, Noise Steps:float, Normal Tangent Space:float3, Depth Buffer Mip:float, Cubemap Mip:float, ... | SSGI:float3 |  |
| [interior mapping cubemap](../md_docs/content/materials/graph/node_library/misc/interior_mapping_cubemap.md) | `5eaec176122133dee8097478223c9a344695517f` | UV:float2, Parallax Multiplier:float, Tiling:float2, Offset:float2 | Direction For Cubemap:float3 | 1 |
| [interior mapping texture2d](../md_docs/content/materials/graph/node_library/misc/interior_mapping_texture_2d.md) | `d36f96b635956154bf4dd4564a62220a0ce1c877` | UV:float2, Parallax Multiplier:float, Tiling:float2, Offset:float2, Sides Correction:float, Perspective Correction:float | Result UV:float2 | 1 |
| [lerp contrast preserving](../md_docs/content/materials/graph/node_library/math/lerp_contrast_preserving.md) | `bed21b468ab4c8594da07299b4048bee9181e510` | Color 0:float3, Color 1:float3, Color 0 Blurred:float3, Color 1 Blurred:float3, Blend (0-1):float | Result Color:float3 |  |
| [levels](../md_docs/content/materials/graph/node_library/misc/levels.md) | `44ac567c10615c1110fccbd804bc6bd4ed5cc5c4` | Value:float, Input Black Level:float, Input Gamma:float, Input White Level:float, Output Black Level:float, Output White Level:float | Result:float |  |
| [normal from height texture](../md_docs/content/materials/graph/node_library/misc/normal_from_height_texture.md) | `8a31c7e195c402c6f3f3ab811f53f8baa8617743` | Heightmap Texture:Texture2D, UV:float2, Height (Meters):float | Tangent Tangent Space:float3, Binormal Tangent Space:float3, Normal Tangent Space:float3 | 1 |
| [normal from height value](../md_docs/content/materials/graph/node_library/misc/normal_from_height_value.md) | `27e17eb1c6ce709a092e86441880eea1846c6930` | Height Value:float, Height (Meters):float, Vertex Position Object Space:float3, Normal Object Space:float3 | Normal Tangent Space:float3 | 5 |
| [object scale](../md_docs/content/materials/graph/node_library/input/object_scale.md) | `4573d2a421472bb07e56376261ea4ae017588e69` | - | Scale Absolute World Space:float3, Scale View Space:float3, Scale Camera World Space:float3 |  |
| octahedral_impostor | `417bc84eaa3badd32f20a01c13cb85b21214f8cd` | AO:bool, Shading Map:bool, Translucent Map:bool, Depth Map:bool, Depth Shadow Only:bool, Parallax Offset:bool, Vertex Interpolation:bool, Opacity Jitter:bool, ... | Opacity Threshold:float, Albedo:float4, Shading:float4, Normal:float3, Translucent:float, Ambient Occlusion:float, Depth Offset:float, Vertex Position OS:float3 |  |
| [parallax occlusion mapping](../md_docs/content/materials/graph/node_library/misc/parallax_occlusion_mapping.md) | `db833834f73846490e838d66a3bf0c79bd71fe8e` | Heightmap Texture 2D:Texture2D, Parallax Intensity (In Meters):float, Max Layers:float, Min Layers:float, Noise Intensity:float, UV Aspect:float, UV:float2, UV Tiling:float2, ... | Displaced UV:float2, Depth Offset:float, Displaced Heightmap:float | 3 |
| [parallax simple](../md_docs/content/materials/graph/node_library/misc/parallax_simple.md) | `96e0fa453eef3f115cf37a6c045a48a0d895574c` | UV:float2, Height Texture:Texture2D, Height (In Meters):float | Result UV:float2 | 1 |
| [pi05](../md_docs/content/materials/graph/node_library/math/pi05.md) | `e4e51b2eba96896821f93f3076445be513b4423a` | - | Pi / 2:float |  |
| [pi2](../md_docs/content/materials/graph/node_library/math/pi2.md) | `b48636a49bb5b4da3418ee4c1659f15034193293` | - | Pi * 2:float |  |
| [posterize](../md_docs/content/materials/graph/node_library/misc/posterize.md) | `29f554fc8f6e56dd2c5a19632a5135f743c31972` | Value:float, Steps:float | Posterized Result:float |  |
| [reflection raymarched](../md_docs/content/materials/graph/node_library/misc/reflection_raymarched.md) | `834bc0cabf082906652502db28031d8e3eebc6ad` | Step Size:float, Step Size Noise Intensity:float, Last Step Size:float, Threshold:float, Screen Perimeter Softness:float, Roughness:float, Color Buffer Mip Offset:float, Depth Buffer Mip Offset:float, ... | Emission:float3, Mask:float | 3 |
| [reflection simple](../md_docs/content/materials/graph/node_library/misc/reflection_simple.md) | `4e9d55fc4f98d8b0c69114c67d65defab0c7c1e7` | Ray Length:float, Screen Perimeter Softness:float, Color Buffer Mip Offset:float, Normal Tangent Space:float3, Position View Space:float3 | Emission:float3, Mask:float |  |
| [refraction raymarched](../md_docs/content/materials/graph/node_library/misc/refraction_raymarched.md) | `dac89e12f3f8cb4dbe68fde370dc5337df6da90a` | Step Size:float, Translucence Roughness:float, Last Step Size:float, IOR:float, Normal Tangent Space:float3, Position View Space:float3 | Emission:float3, Ray Distance:float, Intersection Screen UV:float2, Refraction Screen UV Offset:float2 | 2 |
| [refraction screen uv offset for thick objects](../md_docs/content/materials/graph/node_library/misc/refraction_screen_uv_offset_for_thick_objects.md) | `f2d97132505f37566f005346cbcdb64d26042132` | IOR:float, Ray Length:float, Normal Tangent Space:float3, Position View Space:float3 | Screen UV Offset:float2 |  |
| [refraction screen uv offset for thin objects](../md_docs/content/materials/graph/node_library/misc/refraction_screen_uv_offset_for_thin_objects.md) | `e9c472fca6f5a729c9546e1322c00550e7555fda` | Fake Refraction Intensity:float, Normal Tangent Space:float3, Position View Space:float3 | Screen UV Offset:float2 | 1 |
| [refraction simple for thick objects](../md_docs/content/materials/graph/node_library/misc/refraction_simple_for_thick_objects.md) | `cc5ad2e898951d66bae3a75972bd9d10debb060f` | Translucence Color:float3, IOR:float, Translucence Roughness:float, Ray Length:float, Normal Tangent Space:float3, Position View Space:float3 | Emission:float3 | 1 |
| [refraction simple for thin objects](../md_docs/content/materials/graph/node_library/misc/refraction_simple_for_thin_objects.md) | `c5f3bf34750c501039825894a3356cfee86ea084` | Translucence Color:float3, Fake Refraction Intensity:float, Translucence Roughness:float, Normal Tangent Space:float3, Position View Space:float3 | Emission:float3 | 1 |
| [replace color](../md_docs/content/materials/graph/node_library/misc/replace_color.md) | `99f663b541839d3b06d9ce149ad13091ba7a06f4` | Source Color:float3, Target Color:float3, Intensity:float | Result Color:float3 |  |
| [screen space subsurface scattering](../md_docs/content/materials/graph/node_library/misc/screen_space_subsurface_scattering.md) | `7616e7de81481569746d46c216ba7f607f84dcdd` | SSS Color:float3, SSS Radius:float, Threshold:float, Noise Intensity:float, Position View Space:float3 | Direct Lighting:float3, Indirect Lighting:float3 |  |
| [specular_ambient_occlusion](../md_docs/content/materials/graph/node_library/misc/specular_ambient_occlusion.md) | `b47f9f8cb0f8c9e0d04c3298d685e9e1284e50ca` | Ambient Occlusion:float, Roughness:float, Normal Tangent Space:float3 | Specular AO:float |  |
| [ssao raymarched](../md_docs/content/materials/graph/node_library/misc/ssao_raymarched.md) | `da985c4c17ed3c5e6f571ac28910a3f4589c3706` | Step Size:float, Threshold:float, Noise Rays:float, Noise Steps:float, Normal Tangent Space:float3, Depth Buffer Mip:float | SSAO:float |  |
| [ssgi raymarched](../md_docs/content/materials/graph/node_library/misc/ssgi_raymarched.md) | `3b24275e09466b9845d5bfd9073e3ea5b13c0325` | Step Size:float, Threshold:float, Noise Rays:float, Noise Steps:float, Normal Tangent Space:float3, Depth Buffer Mip:float, Color Buffer Mip:float | SSGI:float3 |  |
| [tiling and offset](../md_docs/content/materials/graph/node_library/misc/tiling_and_offset.md) | `f438039f2b5f60811c3f119ec9708ef8d5053872` | UV:float2, Tiling:float2, Offset:float2 | Result UV:float2 | 22 |
| [tree animation](../md_docs/content/materials/graph/node_library/misc/tree_animation.md) | `df61da3b8f4231569d2b5f2118e75c18f4117e2a` | Stem Speed:float, Stem Wind Offset:float, Branches Speed:float, Branches Offset:float, Leaves Tiling:float, Leaves Speed:float, Leaves Offset:float, Wind Direction:float2, ... | Vertex Offset Tangent Space:float3 | 1 |
| [triplanar color](../md_docs/content/materials/graph/node_library/misc/triplanar_color.md) | `f1b43f66ebf9e4f242c3db6896fb5268ccb7004a` | Texture2D:Texture2D, Vertex_Position:float3, Vertex_Normal:float3, Blend:float, Tiling:float3, Offset:float3 | Triplanar Color:float4 | 4 |
| [triplanar normal](../md_docs/content/materials/graph/node_library/misc/triplanar_normal.md) | `632c16d24946e42461ebb47da1f28b10b6f76e3a` | NormalMap Texture:Texture2D, Vertex Position:float3, Blend:float, Vertex Normal:float3, Tiling:float3, Offset:float3 | Triplanar Normal:float3 | 3 |
| [vertex depth](../md_docs/content/materials/graph/node_library/input/vertex_depth.md) | `b2ecd3b056018c77b39c6f55697fc7ad57e01417` | - | Vertex Depth:float | 2 |

