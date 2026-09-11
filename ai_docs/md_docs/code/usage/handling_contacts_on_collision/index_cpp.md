# Handling Contacts on Collision (CPP)


Sometimes you may need to implement your own contact handler for colliding physical bodies. In this example, you will learn how to visualize contact points, display debug information, and add a hit effect (sparks) at the point of impact.


## Preparing the content


To create sparks, we are going to use the [VFX add-on](../../../sdk/addons/vfx/index.md) (you can download it on [https://store.unigine.com](https://store.unigine.com)).


Create a [new project](../../../sdk/projects/index_cpp.md#creation) in UNIGINE SDK Browser and [import](../../../editor2/managing_packages/index.md#import) the [VFX add-on](../../../sdk/addons/vfx/index.md) to it.


Open the project in the UnigineEditor and add some primitive objects to the default scene.


![](cpp_default.jpg)


Let's get some information about the contacts the blue box will have with other objects.


### Making the Objects Collidable


The objects in the scene are dynamic ones, so to be able to [collide](../../../principles/physics/collision/index.md) they need a [body](../../../principles/physics/bodies/index.md) and a [collision shape](../../../principles/physics/shapes/index.md). Add a *Rigid body* and a shape to each object via the *Physics* tab of the *Parameters* window.


Collisions are available for static objects as well (like buildings or ground) � simply enable the *[Collision](../../../editor2/node_parameters/physics/index.md#surface_collision)* option for the corresponding surface.


### Enabling High Priority Contacts


On collision, contacts are distributed randomly between the interacting bodies to optimize performance: some are handled by the first body, others by the second. For a body, contacts that it handles itself are **internal** (access to them is fast), and contacts handled by other bodies are **external**.


> **Notice:** You can iterate through all contacts for a body, but for better performance it is recommended to process only **internal** ones.


The box is a high-priority body for us and we want to track its collisions with maximum efficiency. We can make the box handle most of its contacts itself (so that most of them are internal). To do so, select the box and check ***High Priority Contacts*** in the *Physics* tab (or do it [*via code*](../../../api/library/physics/class.bodyrigid_cpp.md#setHighPriorityContacts_int_void)).


![](high_priority_contacts.png)


### Creating a Hit Effect Node


We will use a [Particle System](../../../objects/effects/particles/index.md) to create a node that simulates sparks.


1. In the UnigineEditor, click *Create -> Particle System -> Particles*. Place the object somewhere in the world, rename it to ***sparks***, and adjust its parameters:

  - *Number Per Spawn* = 10
  - *Radius* = 0.02
  - *Life Time* = 0.2
  - *Period* = inf
  - *Duration* = 0
2. In the *Surface Material* section, assign `library_spark1.mat` material (it is located in the *data -> vfx -> materials -> library_vfx* folder of your project).
3. Switch to the `data` folder in the Asset Browser. Right-click the *sparks* node and select *Create a Node Reference*. A `sparks.node` file will be generated in the `data` folder.
4. Delete the **sparks** object from the scene, we no longer need it since it will be loaded via code.


## Algorithm Description


The algorithm we are going to use can be described as follows:


1. We create three variables (*lastContactTime, lastContactPoint, lastContactInfo*) to keep the time and position of the last occurred contact and some info about it.
2. We [subscribe for an event](../../../code/fundamentals/events/index_cpp.md#physics) to perform some actions when each contact emerges. The handler function (*OnContactEnter()*) takes the body and the index of the contact.
3. If the contact is internal, we save its time and position.
4. We get both physical bodies participating in this contact (*body0*, *body1*). We check if our box has hit another physical object.

  - If any of *body0* and *body1* exists (and it is not the body of our box), then we have found this object. We get details about this body and render it in the viewport using [Visualizer](../../../api/library/engine/class.visualizer_cpp.md).
  - Otherwise, the box has hit some static object (a surface with the *Collision* option enabled). We make this surface highlighted in the viewport as well.
5. We add details we are interested in (e.g., the contact impulse).
6. We spawn a hit effect if the impulse is strong enough. Physics event handlers are called in the main thread, so it is safe to create nodes inside the *OnContactEnter()* function.
7. Finally, in the *Update()* method we display the info and create a slow motion effect for one second.


## Component Code


Let's use the [C++ Component System](../../../principles/component_system/component_system_cpp/index.md) to implement this logic. We will [create a C++ component](../../../principles/component_system/component_system_cpp/index.md#workflow) and assign it to the box node.


1. Open your project in an IDE. > **Notice:** It is recommended to use **Visual Studio** as a default IDE.
2. In the IDE create a new C++ class (`*.h` and `*.cpp` files) and call it `ContactsHandler`. Make sure it inherits from the *[Unigine::ComponentBase](../../../api/library/common/logic/component_system/cpp/class.componentbase_cpp.md)* class.
3. Copy the code below, paste it to the corresponding files in your project and save them in your IDE. <details> <summary>ContactsHandler.h | Close</summary> ```cpp #pragma once #include <UnigineComponentSystem.h> #include <UnigineGame.h> #include <time.h> class ContactsHandler : public  Unigine::ComponentBase { public: // declare constructor and destructor for our class and define a property name. COMPONENT_DEFINE(ContactsHandler, ComponentBase) // declare methods to be called at the corresponding stages of the execution sequence COMPONENT_INIT(init); COMPONENT_UPDATE(update); // A node that will be loaded on contact (a hit effect) PROP_PARAM(File, hitEffect); bool debug = true; protected: void init(); void update(); void OnContactEnter(const Unigine::BodyPtr &, int); private: // Time, position and some info of the last occurred contact time_t lastContactTime; Unigine::Math::vec3 lastContactPoint; Unigine::String lastContactInfo; }; ``` </details> <details> <summary>ContactsHandler.cpp | Close</summary> ```cpp #include "ContactsHandler.h" #include <UnigineNode.h> #include <UnigineVisualizer.h> using namespace Unigine; using namespace Math; REGISTER_COMPONENT(ContactsHandler); void ContactsHandler::init() { BodyPtr body = node->getObjectBody(); if (body) { // For debug purposes, we can render certain contacts depending on their type body->getEventContacts().connect(*this, [](const BodyPtr &b) {b->renderInternalContacts(); }); // subscription for contact event (when each contact emerges) body->getEventContactEnter().connect(this, &ContactsHandler::OnContactEnter); } } // This function takes the body and the index of the contact void ContactsHandler::OnContactEnter(const Unigine::BodyPtr &body, int num) { // Enable Visualizer to see the rendered contact points Visualizer::setEnabled(true); if (body->isContactInternal(num)) { if (debug) { // The time of the contact lastContactTime = time(NULL); // The position of the contact lastContactPoint = body->getContactPoint(num); // We get both physical bodies participating in this contact BodyPtr body0 = body->getContactBody0(num); BodyPtr body1 = body->getContactBody1(num); BodyPtr touchedBody = NULL; // We check if our object has hit another physical object. // If any of the bodies exists and it's not the body of our object // then we have found another physics-driven object that hit it if (body0 && body0 != body) touchedBody = body0; if (body1 && body1 != body) touchedBody = body1; if (touchedBody) { // Our object has touched a physics-driven object. // We save the info about the body lastContactInfo = String::format("body %s of object %s ", touchedBody->getName(), touchedBody->getObject()->getName()); // Render it in the viewport Visualizer::renderObject(touchedBody->getObject(), Math::vec4_blue, 0.5f); } else { // It has touched a surface with Collision enabled lastContactInfo = String::format("surface #%d of object %s", body->getContactSurface(num), body->getContactObject(num)->getName()); // Highlighting the surface Visualizer::renderObjectSurface(body->getContactObject(num), body->getContactSurface(num), Math::vec4_blue, 0.5f); } // You can add details you are interested in (e.g., the contact impulse) lastContactInfo += String::format("\nimpulse: %f", body->getContactImpulse(num)); } // We spawn a hit effect if the impulse is strong enough if (body->getContactImpulse(num) > 0.3f && hitEffect) { NodePtr Effect = World::loadNode(hitEffect); Effect->setPosition(Vec3(body->getContactPoint(num))); } } } void ContactsHandler::update() { // Here we can display the info and create a slow motion effect for one second if (debug) { if (int(time(NULL) - lastContactTime) < 1.0f) { // Slow motion effect Game::setScale(0.3f); Visualizer::renderMessage3D(lastContactPoint, Math::vec3_one, ("last contact: \n" + lastContactInfo).get(), Math::vec4_green, 2, 24); } else  // All the other time the speed will be normal { Game::setScale(1.0f); } } } ``` </details>
4. Before you can use C++ components, you should initialize the Component System. Modify the *init()* method of the *[AppSystemLogic](../../../code/fundamentals/execution_sequence/app_logic_system.md#systemlogic)* class as shown below (`AppSystemLogic.cpp` file). <details> <summary>AppSystemLogic.cpp | Close</summary> ```cpp #include <UnigineComponentSystem.h> int AppSystemLogic::init() { // initialize ComponentSystem and register all components ComponentSystem::get()->initialize(); return 1; } ``` </details>
5. Build and run the project via your IDE (press **Ctrl + F5** in Visual Studio). The Component System will generate a property file (`ContactsHandler.prop`) in the *data -> ComponentSystem* folder of your project.


## Applying Logic to the Object


Switch back to the UnigineEditor and select the **box** node. Click *Add New Property* in the *Parameters* window and assign the newly generated **ContactsHandler** property. Specify the `sparks.node` asset to be loaded and spawned on collision.


![](effect_on_collision_cpp.png)


> **Notice:** You might need to increase the physics FPS and the number of iterations for better quality during slowdown. You can do this in the *Settings* tab of the UnigineEditor.


Click **Run** to see the result. As the box is rolling around, the physics-driven objects and collidable surfaces it hits along the way are highlighted, and contact details are displayed near the contact point. Whenever a collision occurs, it triggers an asset spawning and a slow motion effect.


> **Notice:** All manipulations with physical bodies should belong to the *UpdatePhysics()* method.


This is how you can easily track collisions and run necessary logic on time: spawn particles, [play sounds](../../../code/usage/sound_source/index_cpp.md), and destroy fracture objects.
