# Project Workflow


The article provides key information on the workflow stages for developing a project with UNIGINE.


## Creating a Project


A new project is [created](../sdk/projects/index_cpp.md#creation) via UNIGINE SDK Browser using [templates](../sdk/templates/index.md). You can choose a template whose predefined settings match your project's needs.


The created project will have the default [file structure](../editor2/assets_workflow/project_files.md) that will be changed in the development stage.


## Developing a Project


Once the project has been created, you can start developing it. It is the most important stage as it includes working with content and implementing the application logic.


### Working with Content


> **Notice:** All your project's content must be stored in the `data` directory.


Working with the project content is performed via UnigineEditor and includes:


1. Placing your assets in the [supported formats](../editor2/assets_workflow/asset_types.md) inside the `data` folder of your project or [creating/importing](../editor2/assets_workflow/assets_create_import.md) them via the *[Asset Browser](../editor2/assets_workflow/index.md#asset_browser)*. > **Notice:** In the `data/.runtimes` directory, [UNIGINE native runtime formats](../editor2/assets_workflow/assets_runtimes.md) generated for the corresponding non-native assets (such as `.fbx`, `.hdr`, etc.) will be stored.
2. Assembling [the scene](../principles/world_structure/index.md) via [UnigineEditor](../editor2/index.md), namely: placing [objects](../objects/index.md), setting up [materials](../editor2/materials_settings/index.md), [properties](../editor2/node_parameters/properties/index.md), [physics](../editor2/node_parameters/physics/index.md) of the objects, setting up [lighting](../objects/lights/index.md), adjusting global settings ([environment](../editor2/settings/render_settings/environment/index.md), [global illumination](../editor2/settings/render_settings/global_illumination/index.md) and other [render settings](../editor2/settings/render_settings/index.md)). > **Notice:** Unlike the other engines, UNIGINE provides its own material system with a rich set of [built-in base materials](../content/materials/library/index.md) using predefined shaders. You can [adjust settings](../editor2/materials_settings/index.md) of the built-in base materials via UnigineEditor to get the desired result. You can also extend the set of available materials by adding [custom ones](../content/materials/custom.md) utilizing [custom shaders](../code/materials_shaders/abstract_materials/index.md). See also the article on [*World Management*](../principles/world_management/index.md).


### Implementing Logic


UNIGINE provides the following APIs for implementing the application logic:


- [**C# API**](../code/csharp/index.md) for a good balance between speed and ease of use. It allows using [C# Component System](../principles/component_system/component_system_cs/index.md) enabled by default and integrated into the UnigineEditor. It is the easiest way to implement your application logic in components and assign them to any node to be executed.
- [**C++ API**](../code/cpp/index.md) for maximum performance of the application and seamless integration with the existing code base.
- [**UnigineScript API**](../code/uniginescript/index.md) for fast iterative scripting language featuring instant compilation and thousands of useful functions.


You can stick to a single language: C++ if maximum performance is a key factor, or C# for optimum balance. In case of C# (.NET), UNIGINE provides the [C# Component System](../principles/component_system/component_system_cs/index.md) integrated into UnigineEditor. This approach is deemed to be the most convenient and ensuring good performance for complex applications with elaborate logic.


Alternatively, you can have different programming languages (C++, C#, and UnigineScript) for different pieces of your project: for example, you can use C++ for base classes and performance consuming operations; and implement some simple application logic in UnigineScript. You can also call methods from one API when using another, and manually expand API functionality.


> **Notice:** The scripts (both `*.h` and `*.usc`) written in UnigineScript are stored in the `data` directory. The C++/C# source code is stored in the `source` directory of the project folder.


### Tracking Changes


Tracking changes to files of the project by Version Control System is performed according to the specific [rules](../editor2/assets_workflow/version_control/index.md).


### See Also


- Articles in the section [*Programming Overview*](../code/fundamentals/programming_overview/index.md)
- Article on [*Execution Sequence*](../code/fundamentals/execution_sequence/index.md)


## Packing a Final Build for Publishing


Packing a final build is required when you need the final release version of the application for publishing. It can be done via [UnigineEditor](../editor2/projects/build_project.md).
