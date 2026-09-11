# World Expression


**World Expression** is a point object, which executes arbitrary expressions (scripts) within the specified [distance](#distance) and at a set [frame rate](#ifps). By default, expressions are executed at the same frame rate as the main application.


> **Notice:** An expression is executed only if it's within the specified [distance](#distance) from the camera.


By using *World Expression*, you can attach a script to an object in the scene. To do that, such object must be added as a child node to *World Expression*. Child nodes inherit transformations (if any) of the *World Expression* node.


> **Notice:** Child nodes are transformed relative to the pivot point of the *World Expression* node.


If there are nested *World Expression* nodes, the child node of the last *World Expression* in the hierarchy inherits transformations of all parent *World Expression* nodes.


For example, by using *World Expression*, you can transform objects in the scene, turn on and off sounds with the distance, turn on and off NPC behavior, attach objects to the camera (e.g. drops of the rain on the camera), and so on.


![](index.gif)

*Mesh Dynamicnodes added as children to the nestedWorld Expressionnodes*


### See also


- The *[WorldExpression](../../../api/library/worlds/class.worldexpression_cpp.md)* class to manage *World Expression* via API
- Tutorial on *[Adding Scripts to the Project](../../../code/uniginescript/add_scripts/index.md#world_expression)*
- Set of samples located in the `<UnigineSDK>/data/samples/worlds/` folder:

  - `expression_00` � `expression_05`


## Creating World Expression


To create *World Expression* via UnigineEditor:


1. On the [Menu bar](../../../editor2/interface/index.md#menu_bar), click *Create -> Logic -> Expression*. ![](create_expression.png)
2. Place the *World Expression* somewhere in the world.


## Attaching World Expression Script


There are two ways of attaching a *World Expression* script via UnigineEditor:


- **Directly in UnigineEditor** in the *[Source](#source)* field of the *World Expression* section in the *Parameters* window. Source code must be inside the curly braces {}, as they define the *World Expression* scope. ![](source_expression.png)
- **Attached as a script file** in the *[File](#file)* field of the *World Expression* section. The script file should be included in the *World Expression* scope in the *[Source](#source)* field using the curly braces {}: ![](file_expression.png) In this case, the `my_expression.h` file should contain the following code: ```cpp log.message("WorldExpression is updated\n"); ``` > **Notice:** In the script file, the source code **must not** be wrapped in the curly braces {}.


### Implementing Script


The script itself can be implemented as a simple sequence of functions' calls or as a set of functions and classes. See examples [here](../../../api/library/worlds/class.worldexpression_cpp.md#create).


> **Notice:** It is recommended to implement simple scripts.


### Inter-Script Communication


Such script can [communicate with the world script](../../../api/library/worlds/class.worldexpression_cpp.md#interaction) via the corresponding *[engine.world](../../../api/library/engine/class.world_cpp.md)* class functions or with *[World Trigger](../../../objects/worlds/world_trigger/index.md)* via callbacks (see the samples listed [above](#see)).


### Script Functions


Besides functions of the UnigineScript library, there is also a set of internal functions that are available within the *World Expression* script. The list of such functions with descriptions and examples can be found [here](../../../api/library/worlds/class.worldexpression_cpp.md#script_functions).


## Setting World Expression Parameters


You can adjust the following parameters of *World Expression* in the *Node* tab:


![](expression_parameters.png)


| Update Distance Limit | Distance from the camera, within which the expression is executed. |
|---|---|
| IFps | A constant frame duration (inverse FPS, 1/FPS) used to execute the expression. If 0 is set, the expression is executed at the same frame rate as the main application. |
| File | A path to a file with a *World Expression* script to be executed. The path is relative to the `data` directory. This file should be included in the *World Expression* scope in the *[Source](#source)* field. This field is optional as the *World Expression* script can be implemented directly via the UnigineEditor interface. > **Notice:** If the script file is changed, it should be refreshed via UnigineEditor: click ![](refresh_file.png) to the right of the *File* field. |
| Source | Source code of a *World Expression* script. This field can contain: - Direct implementation of the *World Expression* script - The *#include* directive that [loads the script file](#attach_script) specified in the *File* field. > **Notice:** In both cases, the curly braces {} must wrap the code in the field. |
