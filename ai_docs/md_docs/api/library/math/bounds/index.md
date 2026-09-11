# Bounds-Related Classes


A **bound object** represents a spherical or cubical volume enclosing the whole node, used for describing node's size and location. In UNIGINE, this can be an axis-aligned bounding box (AABB) or a sphere. The size of this box or sphere is defined as the minimum one that can contain the object.


Bounds are defined only for the nodes that have visual representation or their own size. The following "abstract" objects **do not have bounds** at all and therefore are excluded from the [spatial tree](../../../../principles/world_management/index.md#bsp):


- [Dummy Node](../../../../objects/nodes/dummy/index.md)
- [Node Reference](../../../../objects/nodes/reference/index.md)
- [Node Layer](../../../../objects/nodes/layer/index.md)
- [World Switcher](../../../../objects/worlds/world_switcher/index.md)
- [World Transform Path](../../../../objects/worlds/world_transforms/transform_path/index.md)
- [World Transform Bone](../../../../objects/worlds/world_transforms/transform_bone/index.md)
- [World Expression](../../../../objects/worlds/world_expression/index.md)
- *[Dummy Object](../../../../objects/objects/dummy/index.md)* (if it has no [body](../../../../principles/physics/bodies/index.md) assigned)


This approach significantly reduces the size of the tree and improves performance due to saving time on bound recalculation when transforming such nodes. Moreover, AABBs ensure very fast checks due to simplified operations, and to define such bounding box just two points are required � *(Xmin, Ymin, Zmin)* and *(Xmax, Ymax, Zmax)*.


However, bound checks may be inaccurate as the bound doesn't follow the object contours precisely. In addition to that, the bounding box is axis-aligned (i.e., its edges are parallel to the coordinate axes) and when the object is rotated the bound changes. Therefore, bounds are used just to quick check if objects might be colliding. If yes, then a more accurate check should be performed.


![](../../../../principles/world_management/bounds.gif)


The following types of bounds are used:


- **Local Bounds** � bound objects with local coordinates which do not take into account physics and children. Obtained via the following methods of the *Node* class: *[getBoundBox()](../../../../api/library/nodes/class.node_cpp.md#getBoundBox_BoundBox)* and *[getBoundSphere()](../../../../api/library/nodes/class.node_cpp.md#getBoundSphere_BoundSphere)*.
- **World Bounds** � same as local ones, but with world coordinates. Obtained via the following methods of the *Node* class: *[getWorldBoundBox()](../../../../api/library/nodes/class.node_cpp.md#getWorldBoundBox_WorldBoundBox)* and *[getWorldBoundSphere()](../../../../api/library/nodes/class.node_cpp.md#getWorldBoundSphere_WorldBoundSphere)*.
- **Spatial Bounds** � bound objects with world coordinates used by the spatial tree, and therefore taking physics into account (shape bounds, etc.). Obtained via the following methods of the *Node* class: *[getSpatialBoundBox()](../../../../api/library/nodes/class.node_cpp.md#getSpatialBoundBox_WorldBoundBox)* and *[getSpatialBoundSphere()](../../../../api/library/nodes/class.node_cpp.md#getSpatialBoundSphere_WorldBoundSphere)*.


> **Notice:** *Spatial* bounds are calculated faster than *World* ones.


And their hierarchical analogues (taking into account all children) to be used where hierarchical bounds are required (they are slow, but offer correct calculations):


- **Local Hierarchical Bounds** � bound objects with local coordinates taking bounds of all node's children into account. Obtained via the following methods of the *Node* class: *[getHierarchyBoundBox()](../../../../api/library/nodes/class.node_cpp.md#getHierarchyBoundBox_int_WorldBoundBox)* and *[getHierarchyBoundSphere()](../../../../api/library/nodes/class.node_cpp.md#getHierarchyBoundSphere_int_WorldBoundSphere)*.
- **World Hierarchical Bounds** � same as local ones, but with world coordinates. Obtained via the following methods of the *Node* class: *[getHierarchyWorldBoundBox()](../../../../api/library/nodes/class.node_cpp.md#getHierarchyWorldBoundBox_int_WorldBoundBox)* and *[getHierarchyWorldBoundSphere()](../../../../api/library/nodes/class.node_cpp.md#getHierarchyWorldBoundSphere_int_WorldBoundSphere)*.
- **Spatial Hierarchical Bounds** � hierarchical bound objects used by the spatial tree, and therefore taking physics into account (shape bounds, etc.). Obtained via the following methods of the *Node* class: *[getHierarchySpatialBoundBox()](../../../../api/library/nodes/class.node_cpp.md#getHierarchySpatialBoundBox_int_WorldBoundBox)* and *[getHierarchySpatialBoundSphere()](../../../../api/library/nodes/class.node_cpp.md#getHierarchySpatialBoundSphere_int_WorldBoundSphere)*.


## Articles in This Section

- [BoundBox Struct (CPP)](../../../../api/library/math/bounds/class.boundbox_cpp.md)

- [BoundFrustum Struct (CPP)](../../../../api/library/math/bounds/class.boundfrustum_cpp.md)

- [BoundSphere Struct (CPP)](../../../../api/library/math/bounds/class.boundsphere_cpp.md)

- [WorldBoundBox Struct (CPP)](../../../../api/library/math/bounds/class.worldboundbox_cpp.md)

- [WorldBoundFrustum Struct (CPP)](../../../../api/library/math/bounds/class.worldboundfrustum_cpp.md)

- [WorldBoundSphere Struct (CPP)](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md)
