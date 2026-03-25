# Adding Variations for a More Realistic Environment


*Randomizer* is a UnigineEditor tool designed for adding variations of the scene objects in few clicks.


> **Notice:** To open the *Randomizer* tool, choose *Tools -> Randomizer* in the Menu Bar.
>  To learn how to use the tool, watch [this video tutorial](#video_tutorial).


![Randomizer Interface](randomizer.png)

*RandomizerTool*


The *Randomizer* can perform the following operations with nodes:


- Replace the selected **initial nodes** with other nodes (**replacer nodes**) taken randomly from the specified set according to the normal law of distribution.
- Change position, rotation, and scale of the **initial nodes** randomly within the range according to the normal law of distribution.


> **Notice:** You can perform all operations together. Besides, you can perform the randomization as many times as you want: every time you will get the different result.


## Randomizer Settings


The *Randomizer* tool provides the following settings:


| Offset | Defines the positional offset applied to the resulting nodes, calculated relative to the position of the corresponding [initial nodes](#initial). The offset value is taken randomly from the specified range. An offset range is specified for each axis. - **From** specifies the minimum offset of nodes in units. - **To** specifies the maximum offset of nodes in units. You can specify both negative and positive values. |
|---|---|
| Rotation | Defines the rotation applied to the resulting nodes, calculated relative to the orientation of the corresponding [initial nodes](#initial). By default, the resulting nodes inherit the *Rotation* values of the initial nodes. To randomize rotation, specify an angle range. Rotation is performed relative to the current direction of an axis. An angle range is specified for each axis. - **From** specifies the minimum angle by which nodes can be rotated. - **To** specifies the maximum angle by which nodes can be rotated. If one of the values is negative, the nodes will be rotated about the axis in both directions (clockwise and counterclockwise). |
| Scale | **Scale Mode** defines whether to consider the scale of the [replacer nodes](#replacer) during replacement: ![](scale.png) - **Absolute** - ignores the [replacer node](#nodes)'s scale and resets it to [1:1:1]. - **Relative** - multiplies the scale of the [initial nodes](#initial) by the scale of the [replacer node](#nodes). For example, if an initial node with a scale of [2, 3, 4] is replaced by a node with a scale of [0.5, 2, 1], the result node's scale will be [1, 6, 4]. The scale of the resulting nodes can be randomized within the specified range. A scale coefficient is specified for each axis. > **Notice:** If you enable the **Uniform Scale** option, you can specify the coefficient only once: the nodes will be scaled along all axes. - **From** specifies the minimum scale coefficient for nodes. - **To** specifies the maximum scale coefficient for nodes. To downscale the resulting nodes, specify values in range [0;1]. |
| Place Nodes as NodeReference | Toggles adding the [replacer nodes](#nodes) as [NodeReferences](../../../objects/nodes/reference/index.md) to the scene on and off. If the replacer `.node` file has transformations applied to its **internal** content (*Position* and/or *Rotation*), these transformations will be compensated at the *Node Reference* level to preserve the visual placement of the content. If the option is disabled, the initial nodes will change their types to the types of the replacer nodes stored in the `.node` files. > **Notice:** If a `.mesh` is used as the source asset, the initial nodes are not converted to *Node References* and remain regular scene nodes, regardless of the option state. |
| Nodes | Set of nodes (`.node`) or/and meshes (`.mesh`) that will be used for random replacing of the [initial nodes](#initial). To add a new [replacer node/mesh](#replacer), click ![](add_node.png) or drag a file from the Asset Browser. The following fields will appear: ![](node_name_probability.png) - **File Name** field displays the name of the replacing file. - **Probability** field allows specifying the probability of node/mesh occurrence. According to this value, the frequency of node/mesh occurrence is calculated as follows: the probability value of each node is divided by the sum of probabilities set for all nodes/meshes in the set. |


## Replacing Nodes


To replace initial nodes with other nodes taken randomly from the specified set, you need to do the following:


1. [Select](../../../editor2/select_position_nodes/index.md#select_nodes) the nodes that should be replaced. > **Notice:** If the initial node is a *Node Reference*, the source transformation is taken from the referenced content, not from the *Node Reference* itself.
2. Add nodes that will be used for random replacing of the initial nodes in one of the following ways:

  - In the *Nodes* section, press ![](add_node.png), then click ![](open_node.png) in the field that appears and choose a `.node` or `.mesh` file in the dialog window that opens. > **Notice:** You can specify a `.node` file stored inside the asset container.
  - Select the required nodes in the [Asset Browser](../../../editor2/assets_workflow/index.md#asset_browser) and drag them to the *Nodes* section. > **Notice:** You can also drag an `.fbx`, `.dae`, `.obj` or `.3ds` file: a `.node` file stored inside the asset container will be specified automatically.
3. Specify the [probability](#name_probability) of the node occurrence in the field to the right.
4. Toggle the *[Place Nodes as NodeReference](#place_as_reference)* option on, if required.
5. Click **Replace**.


The randomization will be performed according to the normal law of distribution.


### Usage Example


For example, we have several identical barrels:


![](barrels.jpg)


To diversify the types of barrels, do the following:


1. [Select](../../../editor2/select_position_nodes/index.md#select_nodes) all barrels in the scene. ![](selected_nodes_0.jpg)
2. Add the `.node` files with different types of barrels to the *Nodes* section by dragging them from the Asset Browser. ![](drag_nodes.gif)
3. Specify the probabilities of occurrence of each type of barrels: ![](probability.png) According to our set probabilities, the frequency of occurrence of barrels of each type will be the following:

  - 10 for red barrels
  - 5 for blue barrels
  - 2 for light brown barrels
  - 1 for brown barrels

  - 10/18 for red barrels
  - 5/18 for blue barrels
  - 2/18 for light brown barrels
  - 1/18 for brown barrels
4. Toggle the *[Place Nodes as NodeReferences](#place_as_reference)* option on, so that the replacer nodes are added to the scene as *NodeReferences*. It may be useful if you decide to change barrels of a certain type later. In this case, you will need to edit only one barrel: the others will be updated as well.
5. Click **Replace**. The initial nodes will be replaced with the node references from the list. ![](replaced_nodes.jpg)


## Transforming Nodes


To translate, rotate or scale the initial nodes randomly within the specified range, you need to do the following:


1. [Select](../../../editor2/select_position_nodes/index.md#select_nodes) the nodes that should be transformed.
2. Specify ranges for the *[Offset](#offset)*, *[Rotation](#rotation)* and *[Scale](#scale)* values. ![](transformation_settings.png)
3. Click **Replace**.


The randomization will be performed according to the normal law of distribution.


### Usage Example


1. [Select](../../../editor2/select_position_nodes/index.md#select_nodes) all barrels in the scene. ![](selected_nodes_1.jpg)
2. Specify ranges for the transformation parameters: ![](transformation_ranges.png)

  - [30;180] degree for rotation about the Z axis.
  - [0;30] for offset along the X and Y axes.
  - [1;3] for scale by the X, Y, and Z axes.
3. Click **Replace**. The initial nodes will be transformed according to the specified values. ![](transformed_nodes.jpg)


## Video Tutorial


Watch the video below to learn how to add variations with the Randomizer tool.


## See Also


- [Node References: Must-Knows](../../../videotutorials/essentials/node_reference.md) demonstrating the specifics of *Node Reference*
