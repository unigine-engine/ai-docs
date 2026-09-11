# Mesh Transparent


Implements the basic render functionality for a transparent mesh. Can be used for the following objects (inherited from parent abstract material � *[Mesh](../../../code/materials_shaders/abstract_materials/mesh.md)*):


- [ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_cpp.md)
- [ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)
- [ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cpp.md)
- [ObjectMeshCluster](../../../api/library/objects/class.objectmeshcluster_cpp.md)
- [ObjectMeshClutter](../../../api/library/objects/class.objectmeshclutter_cpp.md)
- [ObjectMeshSplineCluster](../../../api/library/objects/class.objectmeshsplinecluster_cpp.md)


> **Notice:** *Mesh Transparent* has the same [states](../../../code/materials_shaders/abstract_materials/mesh.md#features) and [shaders](../../../code/materials_shaders/abstract_materials/mesh.md#shaders) available as the parent *Mesh* abstract material.


You can find the source code for this abstract material here: `<SDK>/data/core/materials/abstract/mesh/mesh_transparent.abstmat`


## Features


The *Mesh Transparent* abstract material has features implemented as internal states that can be enabled on demand in the child material:


| State Name | Default | Conditions | Description |
|---|---|---|---|
| transparent_blur | false | (none) | Enables rendering of transparent blur effect. |
| refraction | false | (none) | Enables rendering of post-processing refraction. |
| refraction_information_lost_fix | false | refraction | Enables correction of refraction for �information lost� areas using information from areas beyond the object's internal volume. |
| refraction_front_side | false | refraction && refraction_information_lost_fix | Renders refraction only for front faces. This option can be used for glass objects with no cavities inside. When enabled, the surface shall overlap all transparent objects located behind it. |
| planar_reflection | false | (none) | Enables rendering of dynamic reflections. Using this option you can create realistic flat mirrors and flat reflective surfaces (parquet, flat varnished surfaces, etc.) |
| reflection_size | 7 | planar_reflection | Reflection map size, in pixels. Possible values: [128, 256, 512, 1024, 2048, 4096, quart_height, half_height, height] |
| reflection_two_sided | false | (none) | Use Two Sided option for reflections |
| reflection_show_pivot | false | (none) | Enable two-sided planar reflection mode. |
| reflection_blur | true | (none) | Show the reflection pivot point. |
| ambient_light | true | (none) | Enables the support for two and more [World Lights](../../../objects/lights/world/index.md). |
| ambient | true | (none) | Enable rendering of the material illuminated by an environment probe light source. |
| environment_probe | true | ambient | Enable rendering of the material illuminated by an environment probe light source. |
| voxel_probe | true | ambient | Enable rendering of the material illuminated by a voxel probe light source. |
| planar_probe | true | ambient | Enable rendering of the material illuminated by a planar probe light source. |
| light_omni | true | (none) | Enable rendering of the material illuminated by an omni light source. |
| light_proj | true | (none) | Enable rendering of the material illuminated by a projected light source. |
| light_world | true | (none) | Enable rendering of the material illuminated by a world light source. |
| multiple_environment_probes | false | environment_probe | Illuminate a transparent object with several environment probes and map their cubemaps to this object. |
| lerp_cascades | false | (none) | Lerp Cascades |
| shadow_filter_mode | 2 | (none) | Filter Mode. Possible values: [none, low, medium, high ultra] |
| shadow_penumbra_mode | 0 | (none) | Penumbra Mode. Possible values: [none, low, medium, high ultra] |
| shadow_filter_noise | true | (none) | Filter Noise |
| shadow_penumbra_noise | true | (none) | Penumbra Noise |


## Shaders


### fragment


For every type of light the right PASS is called based on which one can choose the right shading logic:


- transparent_blur
- refraction
- ambient
- light_omni
- light_proj
- light_world
- light_environment_probe
- light_voxel_probe
- light_planar_probe


Fragment shader has the following output values:


#### Output Data


| Name | Type | Description |
|---|---|---|
| OUT_FRAG_TRANSPARENT_REFRACTION | float2 | UV offset for transparent refraction (requires enabled transparent_blur and refraction) |
| OUT_FRAG_TRANSPARENT_BLUR | float | transparent blur radius |


#### Textures


Here�s the list of available textures that are pre-defined and used in fragment shader:


| Texture name | Texture type | State | Pass | Description |
|---|---|---|---|---|
| TEX_REFLECTION_CUBE | Cube | ambient | ambient | Reflection cubemap |
| TEX_REFLECTION_2D | 2D | ambient && planar_reflection | ambient | Reflection texture |
| [TEX_TRANSPARENT_ENVIRONMENT_PROBE](../../../code/formats/materials_formats/base_material_format.md#element_texture) | 2D | ambient && multiple_environment_probes | ambient | Environment probes rendered on transparent objects |
| [TEX_SKY_LUT](../../../principles/render/sequence/index.md#common_pass) | 2D Array | ambient && ambient_light | ambient | An array of sky lookup tables |
| [TEX_REFLECT](../../../principles/render/sequence/index.md#dynamic_reflections) | 2D | ambient | light_planar_probe | Planar reflection texture |
| [TEX_REFLECT](../../../principles/render/sequence/index.md#dynamic_reflections) | Cube | ambient | light_environment_probe | Cube reflection texture |
| TEX_LIGHTMAP | 2D | lightmap | ambient, deferred | Baked lightmap texture |


## Usage Example


<details>
<summary>Transparent Mesh | Close</summary>

```xml
BaseMaterial <parent=Unigine::mesh_transparent>
{
    Texture2D albedo = "core/textures/common/checker_d.dds"
    Color albedo = [1 1 1 0.5]

    // optimization
    State static_shadow = true
    State vertex_velocity = false

    Shader vertex_struct =
    #{
        INIT_BASE_DATA
    #}

    Shader common =
    #{
        float4 sample_color(float2 uv)
        {
            return TEXTURE(tex_albedo, uv) * var_albedo;
        }
    #}

    Shader fragment =
    #{
        float4 color = sample_color(DATA_UV.xy);

        OUT_FRAG_ALBEDO = color.rgb;
        OUT_FRAG_SPECULAR = 0.5f;
        OUT_FRAG_ROUGHNESS = 1.0f;
        OUT_FRAG_METALNESS = 0.0f;

        OUT_FRAG_OPACITY = color.a;
    #}
}

```

</details>
