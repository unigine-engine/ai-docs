# Implementing Color Zone (CPP)


Now we can implement the zones to throw the objects into. We will make holes in the floor, implement zone visualization, and add a [trigger](../../../objects/worlds/world_trigger/index.md) volume that will destroy objects entering it.


## Step 1. Unpack Node References to Make Holes in the Floor


To make some floor nodes invisible and non-colliding (objects will fall through them), while keeping the character's turning working smoothly, we must unpack some floor node references. The unpacking means breaking the link to the node file on disk and changing its parameters.


1. To create Color Zones select some floor tiles in a group (holding the **Shift** hotkey), right-click and choose *Unpack To Node Content*.
2. Then disable *Collisions* for these nodes but make sure that *Intersection* is enabled, so that the character's turning works correctly.
3. To make them invisible, go to *[Viewport](../../../principles/bit_masking/index.md#viewport)* Mask and click *Clear All*. This way all bits of mask are set to 0 and they will not match the Camera's *Viewport* Mask. ![](holes.png)
4. Disable *Collision* option for the **ground** node. Now, physical objects can fall through the holes and the ground.


## Step 2. Implement Zone Visualization


Let's create a plane with an emission material to represent the Color Zone.


1. Choose *Create->Mesh->Static* and search for `plane.mesh`.
2. Place it in the world via the Viewport.
3. Rename the node to `color_zone`.
4. Scale it to the size of the play area and position it between the floor and the ground, so it is visible only through the holes.
5. Create a `color_zone_mat` material inherited from `mesh_base` and assign it to the *plane* surface. ![](child_material.png)
6. In the *States* tab, check the *Emission* option. ![](emission.png) *Color Zone Visualization*


## Step 3. Make the Colors Change Over Time


The Color Zone must be easy to spot. Let's create a dynamic material that changes color emission over time using linear interpolation.


1. Create a new *C++ component* and call it **ColorChanger.**
2. The code, that changes the material *[emission](../../../content/materials/library/mesh_base/index.md#option_emission)* color for the Color Zone over time, is given below. <details> <summary>ColorChanger.h | Close</summary> ```cpp #pragma once #include <UnigineComponentSystem.h> #include <UnigineMathLib.h> #include <UnigineGame.h> class ColorChanger : public Unigine::ComponentBase { public: // declare constructor and destructor for our class and define a property name. COMPONENT_DEFINE(ColorChanger, ComponentBase) // declare methods to be called at the corresponding stages of the execution sequence COMPONENT_INIT(init); COMPONENT_UPDATE(update); protected: void init(); void update(); private: float changeSpeed = 1.5f; Unigine::MaterialPtr color_zone_mat; }; ``` </details> <details> <summary>ColorChanger.cpp | Close</summary> ```cpp #include "ColorChanger.h" using namespace Unigine; using namespace Math; REGISTER_COMPONENT(ColorChanger); void ColorChanger::init() { ObjectMeshStaticPtr mesh = checked_ptr_cast<ObjectMeshStatic>(node); // get the color zone's material color_zone_mat = mesh->getMaterial(0); } void ColorChanger::update() { if (color_zone_mat != nullptr) { // calculate the interpolation coefficient for this frame float k = (Math::sin(Game::getTime() * changeSpeed) + 1) / 2.0f; //interpolate between two colors with given coefficient and set it to the first surface's material color_zone_mat->setParameterFloat4("emission_color", Math::lerp(vec4(1.0f, 1.0f, 0.0f, 1.0f), vec4(0.0f, 1.0f, 1.0f, 1.0f), k)); //interpolate between two values of emission intensity with given coefficient and set it to the first surface's material color_zone_mat->setParameterFloat("emission_scale", Math::lerp(1.0f, 4.0f, k)); } } ``` </details>
3. Build and run the solution to generate a property file for the component.
4. Switch back to the UnigineEditor and attach the **ColorChanger** property to the color zone visualization (`color_zone`). ![](color_changer_cpp.png)


## Step 4. Add a World Trigger


To get rid of objects that were thrown in the Color Zone, let's use a *[World Trigger](../../../objects/worlds/world_trigger/index.md)*. The trigger defines an area into which a physical object will fall and a [callback](../../../code/fundamentals/callbacks/index_cpp.md) that fires when an object gets inside.


1. Create a new **World Trigger** by choosing *Create->Logic->World Tigger* and place it in the world.
2. Check the *Touch* option in the *Parameters* window of the *World Trigger* node to make the trigger fire *callbacks* on partial contact with another node. ![](touch.png)
3. Position it beneath the ground, then set its size to cover the whole play area by going to Parameters and clicking *Edit Size* and adjusting the size of the *World Trigger* in the Viewport. ![](trigger.png)
4. Create a new C++ component in your IDE and call it **KillZone** and copy the following code to the corresponding files. The trigger *callback* will delete any entering object. Don't forget to save your code. <details> <summary>KillZone.h | Close</summary> ```cpp #pragma once #include <UnigineComponentSystem.h> #include <UnigineWorlds.h> class KillZone : public Unigine::ComponentBase { public: // declare constructor and destructor for our class and define a property name. COMPONENT_DEFINE(KillZone, ComponentBase) // declare methods to be called at the corresponding stages of the execution sequence COMPONENT_INIT(init); protected: void init(); void enterEventHandler(const Unigine::NodePtr &target); private: // the area into which an object should fall Unigine::WorldTriggerPtr trigger; }; ``` </details> <details> <summary>KillZone.cpp | Close</summary> ```cpp #include "KillZone.h" using namespace Unigine; REGISTER_COMPONENT(KillZone); void KillZone::init() { trigger = checked_ptr_cast<WorldTrigger>(node); // subscribe for the Enter event (when an object enters the area) if (trigger) trigger->getEventEnter().connect(this, &KillZone::enterEventHandler); } void KillZone::enterEventHandler(const NodePtr &target) { target.deleteLater(); } ``` </details>
5. Build and run the solution to generate a property file for the component.
6. Switch back to UnigineEditor and add the **KillZone** component to the previously created World Trigger. ![](kill_zone_cpp.png)
7. Save changes to the world. Go to *File->Save World* or press **Ctrl+S** hotkey.
8. To run the project via the *SDK Browser*, click on the ellipsis beneath the *Run* button to open the *Customize Run Options* window. By default your IDE builds a *Debug* version of your applications, while the SDK Browser is configured to launch the *Release* one. So, before clicking *Run* you should check the **Debug** option to run the proper executable to check out your progress while developing your application. ![](debug_cpp.png)
