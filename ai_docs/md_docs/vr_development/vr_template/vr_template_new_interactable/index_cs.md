# Adding a New Interactable Object (CS)


The demo scene comes with several ready-made interactable objects, but real projects usually need custom ones -a tool that triggers an animation, a container that plays a sound when opened, or anything else specific to your scenario. Creating one is straightforward: you write a small component that reacts to grab, hold, or throw events, and attach it to any object alongside the existing ones.


Let's try it -we'll make an object that shows a visual effect (e.g. smoke) when grabbed and hides it when released. As a bonus, it can also log a message to the console.


![Object with Visual Effect](../../../learn/13_vr_app/visual_effect_smoke.png)


We're going to use two components together on the same object:


- A **movable component** (e.g. [VRPhysicMovableObject](../../../api/templates/template_vr_csharp/interactions/class.vrphysicmovableobject.md)) -to enable basic grabbing and throwing
- new **VRObjectVFX** -to show/hide a visual effect on grab/release


The movable component handles grabbing and throwing, *VRObjectVFX* handles the visual feedback -each component does one thing, and they work together on the same object.


Here's how to set it up:


1. Create a new **VRObjectVFX** class inherited from *[VRBaseInteractable](../../../api/templates/template_vr_csharp/base/class.vrbaseinteractable.md)*. Add a new file to the *vr_template/components/interactions/interactable/* folder of your project: <details> <summary>VRObjectVFX.cs | Close</summary> `VRObjectVFX.cs` ```csharp using System; using System.Collections; using System.Collections.Generic; using Unigine; public partial class VRObjectVFX : VRBaseInteractable { [ShowInEditor] [Parameter(Title = "VFX Node", Group = "VR Object VFX")] private Node vfxNode = null; [ShowInEditor] [Parameter(Title = "Show Text", Group = "VR Object VFX")] private bool showText = true; [ShowInEditor] [Parameter(Title = "Text", Group = "VR Object VFX")] private string text = "VFX activated!"; protected override void OnReady() { // hide the effect initially if (vfxNode != null) vfxNode.Enabled = false; } public override void OnGrabBegin(VRBaseInteraction interaction, VRBaseController controller) { // show the effect when the object is grabbed if (vfxNode != null) { vfxNode.Enabled = true; if (showText) Log.Message("\n{0}\n", text); } } private void Update() { // keep the effect following the object while held if (vfxNode != null && vfxNode.Enabled) vfxNode.WorldTransform = node.WorldTransform; } public override void OnGrabEnd(VRBaseInteraction interaction, VRBaseController controller) { // hide the effect when the object is released if (vfxNode != null) vfxNode.Enabled = false; } } ``` </details>
2. Build your application to register the new component in the Component System.
3. Open the world in the [UnigineEditor](../../../editor2/index.md) and select one of the movable objects on the table (e.g. the cylinder).
4. Make sure the object already has a movable component assigned (the cylinder uses *[VRPhysicMovableObject](../../../api/templates/template_vr_csharp/interactions/class.vrphysicmovableobject.md)* by default). Then click **Add New Component** and find *VRObjectVFX* in the list. Drag the `vr/particles/smoke.node` asset to the **VFX Node** field -this node stores the particle system representing the smoke effect. It is available in the `vr/particles/` folder of the [UNIGINE Starter Course Projects](../../../sdk/addons/content/index.md) add-on. ![VRObjectVFX Component](../../../learn/13_vr_app/Vfx_Node_field.png)
5. Save your world and close the UnigineEditor.
6. Launch your application. Now if you grab the cylinder, the visual effect will appear: ![Visual Effect Smoke](../../../learn/13_vr_app/visual_effect_smoke.png)
