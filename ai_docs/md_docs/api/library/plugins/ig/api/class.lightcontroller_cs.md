# Unigine::Plugins::IG::LightController Class (CS)


## LightController Class

### Members

---

## void SetEnabled ( Node parent_node , string path , bool enable )

Enables or disables all lights of a given parent node within a specified [category](../../../../../ig/light.md#lights_hierarchy).
### Arguments

- *[Node](../../../../../api/library/nodes/class.node_cs.md)* **parent_node** - Parent node of lights to be enabled.
- *string* **path** - Category of lights in the [lights hierarchy](../../../../../ig/light.md#lights_hierarchy).
- *bool* **enable** - true to enable lights, false to disable.

## void SetEnabled ( string path , bool enable )

Enables or disables all lights within a specified [category](../../../../../ig/light.md#lights_hierarchy).
### Arguments

- *string* **path** - Category of lights in the [lights hierarchy](../../../../../ig/light.md#lights_hierarchy).
- *bool* **enable** - true to enable lights, false to disable.

## void SetStrobed ( string path , bool enable )

Enables or disables lights strobing within a specified [category](../../../../../ig/light.md#lights_hierarchy).
### Arguments

- *string* **path** - Category of lights in the [lights hierarchy](../../../../../ig/light.md#lights_hierarchy).
- *bool* **enable** - true to enable strobing, false to disable.

## void SetBright ( string path , float bright )

Sets the intensity of lights within a specified [category](../../../../../ig/light.md#lights_hierarchy).
### Arguments

- *string* **path** - Category of lights in the [lights hierarchy](../../../../../ig/light.md#lights_hierarchy).
- *float* **bright** - Light intensity value within the [0.0f; 1.0f] range.
