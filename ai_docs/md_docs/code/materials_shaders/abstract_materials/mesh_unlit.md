# Mesh Unlit


Implements the basic render functionality for an unlit mesh. Doesn�t cast or receive shadows, that�s why it can be the base for a custom lighting implementation (e.g., raymarching). Can be used for the following objects (inherited from parent abstract material � *[Mesh](../../../code/materials_shaders/abstract_materials/mesh.md)*):


- [ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_cpp.md)
- [ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)
- [ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cpp.md)
- [ObjectMeshCluster](../../../api/library/objects/class.objectmeshcluster_cpp.md)
- [ObjectMeshClutter](../../../api/library/objects/class.objectmeshclutter_cpp.md)
- [ObjectMeshSplineCluster](../../../api/library/objects/class.objectmeshsplinecluster_cpp.md)


> **Notice:** *Mesh Unlit* has the same [states](../../../code/materials_shaders/abstract_materials/mesh.md#features) and [shaders](../../../code/materials_shaders/abstract_materials/mesh.md#shaders) available as the parent *Mesh* abstract material.


You can find the source code for this abstract material here: `<SDK>/data/core/materials/abstract/mesh/mesh_unlit.abstmat`


### See Also


- [Unlit Materials Example](../../../content/samples/material_examples/unlit_materials.md)


## Features


The *Mesh Unlit* abstract material has features implemented as internal states that can be enabled on demand in the child material:


### States


*Mesh Unlit* contains the same states as parent abstract Mesh material but adds new or modified values of some of the existing ones.


| Name | Default | Description |
|---|---|---|
| static_shadow | true | Overrides Unigine::Mesh�s state value. |
| gbuffer | false | Enables writing of deferred buffers for the material. |
| transparent_blur | false | Enables rendering of transparent blur effect. |
| refraction | false | Enables rendering of post-processing refraction. |


## Shaders


### fragment


Input data and functions are the same as for *[Mesh](../../../code/materials_shaders/abstract_materials/mesh.md#shader_fragment)* abstract material. The *Unlit* material implements its �unlit� functionality by using the emission buffer as an output for the resulting color and skipping deferred pipeline.


#### Output Data


| Name | Type | Description |
|---|---|---|
| OUT_FRAG_COLOR | float4 | Final fragment color as emission |


## Usage Example


<details>
<summary>Unlit Mesh | Close</summary>

```xml
BaseMaterial <parent=Unigine::mesh_unlit>
{
    Texture2D albedo = "core/textures/common/checker_d.dds"
    Color albedo = [1 1 1 1]

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
        float4 color = srgbInv(sample_color(DATA_UV.xy));

        OUT_FRAG_EMISSION = color.rgb;
        OUT_FRAG_OPACITY = color.a;
    #}
}

```

</details>
