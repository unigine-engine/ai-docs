# Working with Large Number of Objects


When the virtual scene contains a large number of objects, both identical and unique, managing each of them is a very complicated task. Moreover, when such objects are represented in the scene as separate meshes, the performance significantly drops.


UNIGINE allows managing a great number of objects as a single object by using *clusters* (*[Mesh Cluster](../../../../objects/objects/mesh_cluster/index.md)*) and *clutters* (*[Mesh Clutter](../../../../objects/objects/mesh_clutter/index.md)*). It simplifies a spatial tree of nodes (in the World Hierarchy, there will be one or several objects instead of thousands), thus increasing the performance.


> **Notice:** Unlike a *cluster*, a *clutter* scatters objects randomly, and, therefore, meshes of the clutter cannot be managed manually. However, procedural scattering provided by the clutter is more memory-efficient.


## Using Clusters


*Clusters* allow you to manage a lot of objects as a single object, while keeping the ability to independently edit each mesh baked in the cluster.


*[Mesh Cluster](../../../../objects/objects/mesh_cluster/index.md)* contains only *identical meshes*. So, if you need to create a complex construction that contains several types of identical meshes (like the tube construction on the picture below), you will have to bake several mesh clusters:


| ![](mesh_cluster_hierarchy.png) | [![](mesh_cluster.png)](https://youtu.be/Iqsr3fEvnis?t=285) |
|---|---|
| *Mesh Clusters in World Hierarchy* | *Meshes Baked toMesh Cluster(Click to watch the video tutorial)* |


The detailed instructions on baking meshes to the cluster can be found in the corresponding article referenced above, as well as in the [Content Optimization](https://youtu.be/Iqsr3fEvnis?t=217) video tutorial.


## Using Clutters


*Clutters* are almost the same objects as *clusters*. The main difference is that *[Mesh Clutter](../../../../objects/objects/mesh_clutter/index.md)* scatters objects randomly and doesn't allow editing each object baked into the clutter individually. However, such peculiarity makes the clutter objects more preferable from the perspective of the performance.


[![](mesh_clutter.png)](https://youtu.be/Iqsr3fEvnis?t=376)


*Mesh Clutter(click to watch the video tutorial)*


The detailed instructions on baking meshes to the clutter can be found in the corresponding article referenced above, as well as in the [Content Optimization](https://youtu.be/Iqsr3fEvnis?t=343) video tutorial.
