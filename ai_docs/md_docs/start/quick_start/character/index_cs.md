# Creating Controllable Character (CS)


Let's create a playable robot that can move around the Play Area and [collide](../../../principles/physics/collision/index.md) with objects or wall obstacles. Our character will fly above the floor and rotate to face the cursor.


## Step 1. Engage Physics for Robot's Model


The robot with a complex [3D model](../../../content/3d_models/index.md) will represent the playable character in the game. We have already imported the *Node Reference* with the *[Skinned Mesh](../../../objects/objects/mesh_skinned_legacy/index.md)*, the flying *animation*, and *materials* for the robot.


The robot must be able to move around the Play Area and collide with static and physical objects. In order to do so, it should have a physical [body](../../../principles/physics/bodies/index.md) and a [collision shape](../../../principles/physics/shapes/index.md) approximating its volume.


1. Place the imported `programming_quick_start\character\robot\robot.node` on the floor inside the Play Area by dragging it from the *Asset Browser* directly to the *Editor Viewport*. ![](robot.jpg)
2. With the **robot** node selected click *[Edit](../../../editor2/instancing_nodes/index.md#edit)* in the *Reference* section of the *Parameters* window. The *Node Reference* shall open and the current selection shall focus on the **robot** *ObjectMeshSkinned* node. Now switch to the *[Physics](../../../editor2/node_parameters/physics/index.md)* tab of the *Parameters* window and assign a **[Rigid](../../../principles/physics/bodies/rigid/index.md)** body to the selected *ObjectMeshSkinned*. ![](rigid_body.png)
3. Set **LDamping** parameter to **5.0** to make sure that the robot will lose speed over time.
4. Scroll down to the *Shapes* section and add a **[Capsule](../../../principles/physics/shapes/index.md#capsule)** *shape* to the body. ![](capsule.png)


The capsule shape will be used as an approximation volume for collisions with other objects in the world.


## Step 2. Set Up Controls


We will apply a linear impulse to the body to move the robot with keyboard **WASD** keys. The robot's motion will be determined according to the camera's orientation. Also, let's restrict the physics-based rotation and vertical movement to avoid unwanted control behavior.


To orient the robot to face the cursor, we will use one of the [intersection types](../../../code/usage/intersections/index_cs.md) called **[World Intersection](../../../code/usage/intersections/index_cs.md#worldintersections_object)**. It will trace a line from the cursor position to the floor to get an intersection point that will be used as a reference for the robot's rotation. You can read more about managing various intersections [here](../../../start/quick_start/pqr/index_cs.md#intersection).


The best way to manage keyboard and mouse inputs, is to use the *[Input](../../../api/library/controls/class.input_cs.md)* class. It enables you to check the state of the buttons and get the current mouse coordinates. Alternative methods for input handling are described [here](../../../start/quick_start/pqr/index_cs.md#inputs).


Let's use the [C# Component System](../../../principles/component_system/component_system_cs/index.md) to implement this logic. We will [create a C# component](../../../principles/component_system/component_system_cs/index.md#create) and assign it to the robot's node in the world.


1. In the *Asset Browser* right-click and choose *Create Code->C# Component* and call it **PlayerController**. ![](../../../principles/component_system/component_system_cs/create_component.gif)
2. Select the **robot** node (*ObjectMeshSkinned*), then click *Add New Component or Property* in the *Parameters* window and assign the **PlayerController** component. > **Notice:** Make sure you assign the component to the **ObjectMeshSkinned** node inside the *NodeReference*! ![](component.png)
3. Open your IDE to edit the component by double-clicking on the created `PlayerController.cs` in the *Asset Browser* and сopy the code below. > **Notice:** It is recommended to use **VS Code** as a default IDE. <details> <summary>PlayerController.cs | Close</summary> ```csharp using System; using System.Collections; using System.Collections.Generic; using Unigine; #if UNIGINE_DOUBLE using Vec3 = Unigine.dvec3; using Mat4 = Unigine.dmat4; using Scalar = System.Double; #else using Vec3 = Unigine.vec3; using Mat4 = Unigine.mat4; using Scalar = System.Single; #endif public partial class PlayerController : Component { Player player; BodyRigid rigid; Vec3 pos; //a WorldIntersection object to store the information about the intersection WorldIntersection intersection = new WorldIntersection(); void Init() { player = Game.Player; rigid = node.ObjectBodyRigid; rigid.AngularScale = new vec3(0.0f, 0.0f, 0.0f); // restricting the rotation rigid.LinearScale = new vec3(1.0f, 1.0f, 0.0f); // restricting Z movement rigid.MaxLinearVelocity = 8.0f; // clamping the max linear velocity } void UpdatePhysics() { // forward if (Input.IsKeyPressed(Input.KEY.W)) Move(player.GetWorldDirection(MathLib.AXIS.Y)); // backward if (Input.IsKeyPressed(Input.KEY.S)) Move(player.GetWorldDirection(MathLib.AXIS.NY)); // left if (Input.IsKeyPressed(Input.KEY.A)) Move(player.GetWorldDirection(MathLib.AXIS.NX)); // right if (Input.IsKeyPressed(Input.KEY.D)) Move(player.GetWorldDirection(MathLib.AXIS.X)); // finding the positions of the cursor and the point moved 100 units away in the camera forward direction ivec2 mouse = Input.MousePosition; Vec3 p0 = player.WorldPosition; Vec3 p1 = p0 + new Vec3(player.GetDirectionFromMainWindow(mouse.x, mouse.y)) * 100; // casting a ray from p0 to p1 to find the first intersected object Unigine.Object obj = World.GetIntersection(p0, p1, 1, intersection); // the first bit of the intersection mask is set to 1, the rest are 0s // finding the intersection position, creating a transformation matrix to face this position and setting the transofrm matrix for the body preserving angular and linear velocities if (obj) { pos = intersection.Point; pos.z = rigid.Transform.Translate.z; // project the position vector to the Body Rigid pivot plane Mat4 transform = MathLib.SetTo(rigid.Transform.Translate, pos, vec3.UP, MathLib.AXIS.Y); rigid.SetPreserveTransform(transform); } } // moving the rigid body with linear impulse in the specified direction void Move(vec3 direction) { //directon is a normalized camera axis vector rigid.AddLinearImpulse(direction); } } ``` </details> > **Notice:** You can copy this sample code and paste it to your source files, however, be careful not to change the values of the default **[Component(PropertyGuid = "")]** attributes.
4. Return to the UnigineEditor. The **PlayerController** component will be automatically reimported, since it just has been changed. After the Reimport process, you will [receive a prompt message](../../../principles/component_system/component_system_cs/index.md#debug), indicating the results of the C# Component System compilation. > **Notice:** If you encounter the *red error message* in the Editor, indicating that some of the C# components were not built, check the Editor's *Console* window for details.
5. Press **Ctrl+S** to save the world and the robot's *NodeReference*.


## Step 3. Finalize and Run


1. Turn off the *[Intersection](../../../editor2/node_parameters/physics/index.md#surface_intersection)* detection for every surface of the robot node to ignore intersections with the robot's own surfaces, as we do not want it in our robot's rotation implementation.
2. For *every* wall object in the world, go to the *Parameters* window and find the *Surfaces* section in the *Node* tab. Select the **box** surface of the mesh and open an *Intersection Mask* window. Uncheck the first **Intersection Mask 0** bit to make sure that walls will not affect the player's character turning. ![](intersection_mask.png)
3. To make the cursor always visible, go to *Windows->Settings->Controls* section, change the **Mouse Handle** mode to *User*. You can also control the cursor via [API](../../../code/usage/mouse_customization/index_cs.md#defines).
4. Save changes to the world and the robot via *File->Save World* (or press **Ctrl+S** hotkey).


Now build and run the game in the *UnigineEditor* to try out the robot's controls.
