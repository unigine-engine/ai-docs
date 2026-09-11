# AssetLinkNode Class (CS)

**Inherits from:** AssetLink


The *AssetLinkNode* class is used in C# components ([*Component* Class](../../../../../../api/library/common/logic/component_system/cs/class.component_cs.md)) to link node assets with the application logic.


### See Also


- The [video tutorial](https://youtu.be/ti2JEdfD3v8) that illustrates the usage of the *AssetLinkNode* class.


## AssetLinkNode Class

### Members

---

## Node Load ( )

Loads a node using the referenced asset, if it exists in the project. The content of the `.node` asset will be [cached](../../../../../../principles/world_management/index.md#node_cache) on the first loading, making the further loadings faster.
### Return value

Node, if it exists in the project; otherwise, **null**.
## Node Load ( mat4 transform )

Loads and [caches](../../../../../../principles/world_management/index.md#node_cache) a node using the referenced asset, if it exists in the project, and applies the transformation matrix to it.
### Arguments

- *mat4* **transform** - Transformation matrix of the node.

### Return value

Node, if it exists in the project; otherwise, null.
## Node Load ( vec3 position , quat rotation )

Loads and [caches](../../../../../../principles/world_management/index.md#node_cache) a node using the referenced asset, if it exists in the project, and applies the specified position and rotation to it.
### Arguments

- *vec3* **position** - Position of the node.
- *quat* **rotation** - Rotation of the node.

### Return value

Node, if it exists in the project; otherwise, **null**.
