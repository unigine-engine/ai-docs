# Setting Up the Project (CPP)


Let's create a new **project** for our game and set up a *level* world with a camera view.


## Step 1. Download Assets and Create the Project


1. [Create](../../../sdk/projects/index_cpp.md#creation) a new empty C++ project. Open the **SDK Browser**, go to *Templates* tab and click the *Create Project* button on the *C++ Empty* template card. ![](template_cpp.png)
2. Make sure to select **C++ (Visual Studio 2022)** in the *API + IDE* list of the project settings section and click *Create New Project*. ![](create_new.png)
3. After the new project is created it will be added to the *My Projects* tab. Click *Open Editor* under the created project to open it in the [UnigineEditor](../../../editor2/index.md). ![](projects.png)
4. Download the *[Docs Sample Content](../../../sdk/addons/content/index.md)* add-on from Add-On Store at [https://store.unigine.com/](https://store.unigine.com/) and add it to the project by dragging into the project `data/` folder in the Asset Browser. In the *Import Package* window that opens, click the *Import Package* button and wait until the add-on contents are imported.


#### See Also


For more details refer to the following topics:


- [Project Workflow](../../../start/workflow.md) article to learn key information on the workflow stages for developing a project with UNIGINE.
- [Programming Overview](../../../code/fundamentals/programming_overview/index.md) article to learn about the execution sequence and the ways of creating projects in Unigine.
- [Creating C++ Application](../../../code/cpp/application.md) article to learn about creating a C++ project in Unigine.


## Step 2. Set Up the Scene


All objects added to the scene are called nodes. Each node has a position, a rotation, and a scale and some basic functionality, which can be extended with components. There are a variety of [built-in nodes](../../../objects/index.md) in UNIGINE.


The Play Area in the game will be laid out with a lot of identical floor tiles. [Visual representation](../../../editor2/node_parameters/visual_representation/index.md) of the floor tile is defined by a plane *[Static Mesh](../../../objects/objects/mesh/index.md)* with a gray [material](../../../content/materials/index.md) assigned.

 Best PracticeEach of these objects is represented by a *[NodeReference](../../../editor2/instancing_nodes/index.md)*, they all refer to a single `*.node` file on a disk. Later, if you decide to make any changes (e.g., change material), you can modify any instance (others will be updated automatically). In case of using multiple separate copies, you'll have to change each of them manually.
Before setting up the scene, let's remove the default content from the world. We will only need the ***ground_plane*** node in the *static_content* group for the test ground surface and ***sun*** node in the *lighting* group for the lighting source, all the other nodes can be removed.


![](delete.png)


So, we make floor tiles as *Node References* all referring to the single `*.node` file on a disk.


Now, we will create a template for the floor tile and save it as a *Node Reference*:


1. In the *Asset Browser* search for `plane.mesh` via the *Search*field and drag it to the [Editor Viewport](../../../editor2/instancing_nodes/index.md) to create a new node in the world. ![](search.png)
2. Select the newly created node in the *World Nodes* window and rename (**F2** hotkey) it to `floor`.
3. Choose the `data` folder and search for the `floor_gray_mat.mat` material in the *Asset Browser*. Then drag it over the **floor** node in the Editor Viewport to assign the material.
4. In the *Editor Viewport* use the manipulator to [adjust](../../../editor2/navigation/index.md) the position of the default **ground** node, moving it slightly below the floor node to avoid z-fighting artifacts. ![](tile.png)
5. Select the **floor** node in the *World Nodes* window and then select the `floor_0_mat` surface in the *Surfaces* section of the *[Parameters](../../../editor2/node_parameters/index.md)* window.
6. Check the *Collision* option for the **floor_0_mat** surface to enable [collision detection](../../../principles/physics/collision/index.md). ![](collision_cs.png)
7. [Convert](../../../editor2/instancing_nodes/index.md#save) the **floor** node to *Node Reference* and save it as an asset on a disk: right-click on the floor node in the *World Nodes* window and select *Create a Node Reference*.


### See Also


For more details refer to the following topics:


- [Creating and Deleting Nodes at Runtime](../../../start/quick_start/pqr/index_cpp.md#creating_nodes) article to learn how to manage nodes via the code.


## Step 3. Instantiate Nodes to Finalize the Play Area


Let's create a grid of floor tiles for the Play Area by instancing *Node References*. For walls we will use box primitives with the default [base material](../../../content/materials/library/mesh_base/index.md) and [surface collision](../../../principles/physics/collision/index.md) enabled to stop the character from going through them.


1. Let's instantiate more of the **floor** tiles by duplicating the *Node Reference* via **Ctrl + D** hotkeys. > **Notice:** You can activate snapping by bound box via **Shift + Z** hotkeys. Click on the arrow next to the *Snap by Grid* icon on the *[Toolbar](../../../editor2/interface/index.md)* and choose the *By Bound Box* option. Select the **floor** node reference and clone it by holding the **Shift** key and moving the translate manipulator in the required direction. ![](cloning.png) > **Notice:** Alternatively, you can hold the **Ctrl** key to snap a node to the grid.
2. You can also select multiple nodes in the *Viewport* or *World Nodes* window while holding the **Shift** key and then clone them all at the same time in a group. ![](floor.png)
3. Create a wall by choosing *Create->Primitive->Box* and then specify the size in all dimensions. Make sure it resembles a wall and place it on the border of the Play Area.
4. To make the wall a collider, select it in the *World Nodes* window. Then, go to the *Parameters* window and find the *Surfaces* section in the *Node* tab. Select the **box** surface of the mesh and check the **Collision** option.
5. Duplicate the primitive with **Ctrl + D** hotkeys and set up the opposite wall. Create the rest of the walls along the borders of the Play Area the same way. ![](walls.png)


A *[World Light](../../../objects/lights/world/index.md)* source (sun) is created for each world by default. So, the scene is lit and walls cast shadows on the ground. You can adjust rotation and other [parameters](../../../objects/lights/parameters/index.md) of the light source via the *Parameters* window.


Alternative way of creating Light Sources via the API is considered [here](../../../start/quick_start/pqr/index_cpp.md#light).


## Step 4. Create a Player Camera


In order to see the world through the application window, you need to create a [Camera](../../../editor2/camera_settings/index.md) and position it above the Play Area.


1. Add a new Camera via *Create->Camera->Dummy*, and place it in the world.
2. Adjust position (**W** hotkey) and rotation (**E** hotkey) of the *PlayerDummy* node via the manipulator in the *Viewport*. ![](adjusting.png)
3. Check the *Main Player* option in the node's *Parameters* window to make it the default camera. ![](main_player.png)


Alternative way of creating a camera via the API is considered [here](../../../start/quick_start/pqr/index_cpp.md#camera).


## Step 5. Save Changes and Run the Game


Now, you can run the game via the SDK Browser.


1. To save changes to the world, go to *File->Save World* or press **Ctrl+S** hotkey.
2. Click the **Run** button in the *SDK Browser* to run the game with the scene we've just set up. ![](run_cpp.png)
