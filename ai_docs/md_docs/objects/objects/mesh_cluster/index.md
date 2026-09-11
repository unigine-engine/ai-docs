# Mesh Cluster


**Mesh Cluster** is an object that can contain a great number of identical meshes with the same material, which are managed as one object. Cluster meshes can be scattered either automatically, or each mesh can be positioned, rotated, and scaled manually.


The *Mesh Cluster* is usually used for objects of the same type, for example, houses in neighborhoods.


Meshes of the *Mesh Cluster* object that are visible in the viewing frustum are loaded, meshes outside the frustum are culled. Using the *Mesh Cluster* is very efficient performance-wise: it substantially speeds up rendering and allows handling a lot of objects without any performance drop.


Storing the *Mesh Cluster* data in the [binary format](#data_storage) adds to boosting performance and reducing both memory and disk space usage.


[![](cluster_2_sm.png)](cluster_2.png)


> **Notice:** The *Mesh Cluster* can contain only identical static meshes with the same material assigned to each of their surfaces.


There are two ways to create a *Mesh Cluster* in UnigineEditor:


- [Collect](#collecting) a *Mesh Cluster* by baking all identical meshes in node's hierarchy or in the world.
- [Create](#creating) a *Mesh Cluster* manually by baking all its identical child meshes.


> **Notice:** *Mesh Cluster* is always culled by the [Occlusion Query](../../../content/optimization/geometry/culling/index.md) and not rendered when outside the viewing frustum.


### See also


- The *[ObjectMeshCluster](../../../api/library/objects/class.objectmeshcluster_cpp.md)* class to edit clusters via API
- A set of samples located in the `<UnigineSDK>/data/samples/objects/` directory:

  - [`cluster_00`](../../../code/uniginescript/samples/objects/cluster_00.md)
  - [`cluster_01`](../../../code/uniginescript/samples/objects/cluster_01.md)
- A set of C++ and C# Component Samples demonstrating how to add and delete *Mesh Cluster* elements ( C++ sample and C# sample) and convert *Mesh Clutter* to *Mesh Cluster* ( C++ sample and C# sample)


## Collecting a Cluster


A *Mesh Cluster* can be collected from all identical meshes that were added in the world or from all identical child meshes of a certain node.


### Baking Identical Meshes of a Node Hierarchy


To create a *Mesh Cluster* by baking all identical meshes in the hierarchy, right-click the parent node of the hierarchy in the *World Hierarchy* window and select **Create Mesh Clusters From Hierarchy** in the context menu.


![](cluster_create_2.png)


Applying this operation creates a *dummy node* with the **_clustered** postfix added to the parent node name. This dummy node contains two child nodes:


- Node that is a parent of all *Mesh Clusters*. This node is named by adding the **_mesh_clusters** postfix to the source parent node name. *Mesh cluster* names are formed using the mesh name and the **_cluster** postfix.
- Node that is a parent of all other child nodes of the source parent node. This node is named by adding the **_other_nodes** postfix to the source parent node name.


The created clusters contain all identical meshes of the source node including meshes that are referenced by *Node References*. Other nodes are added as a linear list. The source node is disabled.


![](hierarchy_cluster_create.png)

*Creation of a clustered node: nodes that are not in clusters are added as a linear list*


> **Notice:** A *Mesh Cluster* is created only if a hierarchy contains at least 8 identical meshes.


### Baking Identical Meshes in the World


To create a cluster by baking all identical meshes in the world, do the following:


1. On the Menu bar, click *Create -> Cluster -> Mesh*. ![](cluster_create.png)
2. In the dialog window that opens, choose the path to the `.mesh` file. This mesh would be used as the source one for the *Mesh Cluster*.
3. Place the *Mesh Cluster* somewhere in the world. By default, is shall contain 4 instances of the selected mesh (you can remove them). Meshes to be baked should have the same `.mesh` file as the one selected for the Mesh Cluster.
4. Specify the same material that is assigned to meshes going to be baked to the cluster in the *Node* tab of the *[Parameters](../../../editor2/node_parameters/index.md)* window (the *Surfaces* section).
5. Click **Collect Similar** in the *Node* tab, *Mesh Cluster* section. All meshes having the same mesh and material assigned will be baked to the cluster. Baked meshes are no longer seen in the nodes hierarchy. ![](collect_cluster.png) *Parameterswindow,Nodetab* To change all child meshes at once, just select a required asset in the *Mesh* field of the *Mesh Cluster* section.


### Creating Mesh Clusters from Mesh Clutters


To create a *Mesh Cluster* from a *[Mesh Clutter](../../../objects/objects/mesh_clutter/index.md)*, use the following context-menu option:


![](cluster_from_clutter.png)


Using this option disables the *Mesh Clutter* and creates and enables a *Mesh Cluster* with the same name and postfix *_Cluster* added.


## Creating a Cluster Manually


To create a *Mesh Cluster* by baking its child meshes, do the following:


1. On the Menu bar, click *Create -> Cluster -> Mesh*. ![](cluster_create.png)
2. In the dialog window that opens, choose a `*.mesh` asset to be used as the source mesh for the cluster.
3. Place the cluster somewhere in the world. By default is shall contain 4 instances of the selected mesh (you can remove them).
4. Manually position identical meshes in the world and make them children of the created cluster. > **Notice:** To make a node a child of another node, drag it under the parent node in the *World Hierarchy* window.
5. To bake the child meshes to the cluster, click **Apply** in the *Mesh Cluster* section of the *Node* tab. The baked child meshes are no longer seen in the nodes hierarchy. ![](create_cluster.png) *Parameterswindow,Nodetab* > **Notice:** Only enabled meshes are baked to a cluster. Disabled meshes are left as child nodes. To add more meshes to the same cluster, simply click **Edit** make them its children and then click **Apply** to rebake the cluster. To change all child meshes at once just change the mesh asset in the *Mesh* field of the *Mesh Cluster* section.


## Editing a Cluster


To edit a *Mesh Cluster* (either [created](#creating) or [collected](#collecting)), for example, to reposition or remove some meshes, click **Edit** in the *Mesh Cluster* section of the *Node* tab.


> **Notice:** Meshes that were collected would become *Mesh Cluster* children.


## Clearing a Cluster


To delete all meshes baked to a *Mesh Cluster*, click **Clear**. Make sure that the meshes are [created](#creating) or [collected](#collecting), as the operation won't be performed if they are rebaked.


## Mesh Cluster Parameters


The following parameters are available for a cluster in the *Mesh Cluster* section of the *Node* tab:


![](parameters.png)

*Parameterswindow,Nodetab,Mesh Clustersection*


| Mesh | Change the source cluster mesh thus changing all children meshes. |
|---|---|
| Visibility Distance | The distance up to which all cluster meshes are visible. - If set to infinity (*inf*), the **[Fade](#fade_distance)** parameter will be ignored. - The real range of cluster visibility directly depends on the object (surface) [maximum visibility distance](../../../principles/world_management/index.md#visible) and also on its [fade out distance](../../../principles/world_management/index.md#fading). In case meshes disappear at a closer distance, further increase of the visibility distance won't affect the performance in any way. > **Notice:** To avoid flickering of cluster meshes, the object [maximum visibility distance](../../../principles/world_management/index.md#visible) should be greater than the sum of [minimum visibility distance](../../../principles/world_management/index.md#visible) and [minimum fade out distance](../../../principles/world_management/index.md#fading): > *Max Visibility > Min Visibility + Min Fade* |
| Fade Distance | The distance up to which the number of rendered cluster meshes gradually decreases, as they disappear randomly one by one. The fade distance follows the [visibility distance](#visible_distance). Without the fade distance set meshes disappear sharply, as a clearly seen line. Using fade distance allows the objects to disappear one by one until up to the fade distance only a few left. It makes the disappearing smooth and much less noticeable. For the best result, it is also recommended to combine this effect with [objects fade-out](../../../principles/world_management/index.md#fading). |


## Data Storage


Mesh cluster data is stored in a binary format and is not represented as standard asset files within the project.


All cluster-related data is written to a dedicated directory:


- `<project_folder>/data/.binary_nodes_data/<node_or_world_guid>/clusters`
- `mount://.binary_nodes_data/<node_or_world_guid>/clusters`


This directory is intentionally ignored by the Editor. As a result, no `.meta` files are generated for cluster data, which prevents the creation unnecessary metadata and keeps the repository clean.


Binary files associated with Mesh Clusters do not have persistent identifiers. Instead, the identifier is reassigned to match the node that was most recently created from the cluster data.


**For example:** when a *Node Reference* containing a *Node Cluster* is used to produce a *Node Layer*, the resulting binary adopts the identifier of that *Node Layer*.


This behavior ensures that the binary data always reflects the latest state of the cluster hierarchy and remains consistent with the most recent processing step.
