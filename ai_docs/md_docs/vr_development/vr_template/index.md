# Getting Started with the VR Template


The **VR Template** is a ready-made starting point for building VR projects in UNIGINE. Instead of wiring up controllers, teleportation, and object interaction from scratch, you get all of that out of the box - so you can jump straight into creating your experience.


This series of articles walks you through everything inside the template: how it's organized, what each part does, and how to extend it for your own project. We'll look at the demo scene, explore the systems behind it, and try some hands-on modifications along the way.


![](../../content/vr/vr_template.jpg)


The template supports a wide range of VR devices through a unified interface. It handles controller model loading automatically depending on your runtime and hardware, so you don't have to worry about device differences.


Here's what you get out of the box:


- Grabbing, holding, and throwing physical objects
- Pressing buttons and flipping switches
- Operating handles, levers, and rotary controls
- Opening drawers and sliding mechanisms
- Shooting with a physics-based firearm
- Connecting plugs and physical cables
- Storing items in a grid-based inventory
- In-world menus, tooltips, and object highlighting


Each of these mechanics is built as a modular [component](../../principles/component_system/index.md) - use them as-is, customize them, or create your own to add entirely new behaviors.


> **Notice:** The world in the VR Template has its settings optimized for the best performance in VR and includes the `*.render` asset that can be loaded at any time by simply double-clicking on it in the [Asset Browser](../../editor2/assets_workflow/index.md#asset_browser) to reset any changes you made to default optimized values.


## Articles in This Section

- [1. Project Setup (CS)](../../vr_development/vr_template/vr_template_project_setup/index_cs.md)

- [1. Project Setup (CPP)](../../vr_development/vr_template/vr_template_project_setup/index_cpp.md)

- [2. Controls and Movement (CS)](../../vr_development/vr_template/vr_template_player/index_cs.md)

- [2. Controls and Movement (CPP)](../../vr_development/vr_template/vr_template_player/index_cpp.md)

- [3. What's in the Scene (CS)](../../vr_development/vr_template/vr_template_interactions/index_cs.md)

- [3. What's in the Scene (CPP)](../../vr_development/vr_template/vr_template_interactions/index_cpp.md)

- [4. Adding a New Interaction (CS)](../../vr_development/vr_template/vr_template_new_interaction/index_cs.md)

- [4. Adding a New Interaction (CPP)](../../vr_development/vr_template/vr_template_new_interaction/index_cpp.md)

- [5. Adding a New Interactable Object (CS)](../../vr_development/vr_template/vr_template_new_interactable/index_cs.md)

- [5. Adding a New Interactable Object (CPP)](../../vr_development/vr_template/vr_template_new_interactable/index_cpp.md)

- [6. In-World UI (CS)](../../vr_development/vr_template/vr_template_gui/index_cs.md)

- [6. In-World UI (CPP)](../../vr_development/vr_template/vr_template_gui/index_cpp.md)

- [7. Mixed Reality Support](../../vr_development/vr_template/vr_template_mixed_reality/index.md)

- [8. Eye Tracking Support (CPP)](../../vr_development/vr_template/vr_template_eye_tracking/index_cpp.md)

- [Classes and Components Overview (CS)](../../vr_development/vr_template/vr_template_classes_and_components/index_cs.md)

- [Classes and Components Overview (CPP)](../../vr_development/vr_template/vr_template_classes_and_components/index_cpp.md)
