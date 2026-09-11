# Binds


This type of node is used to specify more objects that can use this material in addition to the main object type defined in the *[node](../../../../code/formats/materials_formats/ulon_base_material_format.md#node)* argument of the *[BaseMaterial](../../../../code/formats/materials_formats/ulon_base_material_format.md)*. To add a new type of object for the material, you must bind your new custom node to the original node this material is already bound to.


The syntax is the following:


```cpp
Bind from_node_name = to_node_name <defines=�SOME_UNIQUE_DEFINE�>

```


## Usage Examples


```cpp
BaseMaterial <node=ObjectMeshStatic> // the material is set to be used only for ObjectMeshStatic nodes
{
        Bind ObjectMeshStatic = ObjectMeshDynamic // set this material to be used by ObjectMeshDynamic as well
        Bind ObjectMeshStatic = ObjectMeshSkinned <defines="SKINNED"> // also set this material to be used by ObjectMeshSkinned with an additional define for shaders
        Bind ObjectMeshStatic = ObjectMeshCluster <defines="USE_CLUTTER_CLUSTER_PARAMETERS">
        Bind ObjectMeshStatic = ObjectMeshClutter <defines="USE_CLUTTER_CLUSTER_PARAMETERS">
        Bind ObjectMeshStatic = ObjectMeshSplineCluster <defines="USE_CLUTTER_CLUSTER_PARAMETERS,SPLINE"> // compile material's shaders with two additional defines
}

```


We have added five more types of nodes to be supported by this material, some with additional defines. The corresponding defines will be used to compile shaders for the particular node type. For instance, the material's shader for *ObjectMeshSkinned* will be compiled with the **SKINNED** define enabled.


## Arguments


### defines


Definitions separated by a comma without any space. You can also specify your own custom defines:


```cpp
Bind main_node = new_node <defines=�SOME_UNIQUE_DEFINE�>

```
