# Adding a New Interactable Object (CPP)


The demo scene comes with several ready-made interactable objects, but real projects usually need custom ones -a tool that triggers an animation, a container that plays a sound when opened, or anything else specific to your scenario. Creating one is straightforward: you write a small property that reacts to grab, hold, or throw events, and attach it to any object alongside the existing ones.


Let's try it -we'll make an object that shows a visual effect (e.g. smoke) when grabbed and hides it when released. As a bonus, it can also log a message to the console.


![Object with Visual Effect](../../../learn/13_vr_app/visual_effect_smoke.png)


We're going to use two properties together on the same object:


- **[ObjMovable](../../../api/modules/vr/components/objects/class.objmovable.md)** -to enable basic grabbing and throwing
- new **ObjVFX** -to show/hide a visual effect on grab/release


*[ObjMovable](../../../api/modules/vr/components/objects/class.objmovable.md)* handles grabbing and throwing, *ObjVFX* handles the visual feedback -each property does one thing, and they work together on the same object.


Here's how to set it up:


1. Create a new **ObjVFX** class inherited from *[VRInteractable](../../../api/modules/vr/components/class.vrinteractable.md)*. Add two new files to your project -a header and a source file: <details> <summary>ObjVFX.h | Close</summary> `ObjVFX.h` ```cpp #pragma once #include <UnigineNode.h> #include "vr/Components/VRInteractable.h" #include "vr/Components/Players/VRPlayer.h" class ObjVFX : public VRInteractable , public Unigine::ComponentBase { public: COMPONENT_DEFINE(ObjVFX, Unigine::ComponentBase); COMPONENT_INIT(init); PROP_NAME("ObjVFX"); // node with the visual effect (e.g. a particle system) PROP_PARAM(Node, vfx_node); PROP_PARAM(Toggle, show_text, 1); PROP_PARAM(String, text, "VFX activated!"); // interact methods void grabIt(VRPlayer *player, VRController::Side side) override; void holdIt(VRPlayer *player, VRController::Side side) override; void throwIt(VRPlayer *player, VRController::Side side) override; protected: void init(); }; ``` </details> <details> <summary>ObjVFX.cpp | Close</summary> `ObjVFX.cpp` ```cpp #include "ObjVFX.h" REGISTER_COMPONENT(ObjVFX); using namespace Unigine; void ObjVFX::init() { // hide the effect initially if (vfx_node) vfx_node->setEnabled(false); } void ObjVFX::grabIt(VRPlayer *player, VRController::Side side) { // show the effect when the object is grabbed if (vfx_node) { vfx_node->setEnabled(true); if (show_text) Log::message("\n%s\n", text.get()); } } void ObjVFX::holdIt(VRPlayer *player, VRController::Side side) { // keep the effect following the object if (vfx_node) vfx_node->setWorldTransform(node->getWorldTransform()); } void ObjVFX::throwIt(VRPlayer *player, VRController::Side side) { // hide the effect when the object is released if (vfx_node) vfx_node->setEnabled(false); } ``` </details>
2. Build your application and launch it as we did [earlier](../../../vr_development/vr_template/vr_template_project_setup/index_cpp.md#open_source), a new property file (`ObjVFX.prop`) will be generated for our new component.
3. Open the world in the [UnigineEditor](../../../editor2/index.md) and select one of the movable objects on the table (e.g. the cylinder).
4. Make sure the object already has the `ObjMovable.prop` property assigned. Then click **Add New Property** in the *Node Properties* section, drag the `ObjVFX.prop` property to the new empty field. Drag the `vr/particles/smoke.node` asset to the **Vfx Node** field -this node stores the particle system representing the smoke effect. It is available in the `vr/particles/` folder of the [UNIGINE Starter Course Projects](../../../sdk/addons/content/index.md) add-on. ![ObjVFX Property](../../../learn/13_vr_app/vfx_node_cpp.png)
5. Save your world and close the UnigineEditor.
6. Launch your application. Now if you grab and hold the cylinder, it will emit smoke: ![Visual Effect Smoke](../../../learn/13_vr_app/visual_effect_smoke.png)
