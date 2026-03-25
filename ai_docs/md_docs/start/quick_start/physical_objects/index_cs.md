# Generating Physical Objects (CS)


We need some geometric primitives that the player can move around the Play Area and shoot at. Let's generate them via code.


A primitive should have a [body](../../../principles/physics/bodies/index.md) and a [shape](../../../principles/physics/shapes/index.md) to collide with the Player Character and be affected by gravity. We have implemented interaction with bullets via [Intersections](../../../code/usage/intersections/index_cs.md) at the previous step, so we should set the *BulletIntersection* bit for the object's *[Intersection](../../../principles/bit_masking/index.md#intersection_mask)* mask.


When the robot moves fast and the application framerate is low, the character will be teleported each frame and may go through physical objects due to *discrete collision detection*. To avoid this we are going to use [continuous collision detection](../../../principles/physics/collision/index.md#discrete_continuous).


> **Notice:** Continuous collision detection is available for [sphere](../../../principles/physics/shapes/index.md#sphere) and [capsule](../../../principles/physics/shapes/index.md#capsule) shapes only.


1. Create a new *C# component* and call it **ObjectGenerator**. Copy the following code and save it in your IDE to ensure it's automatic compilation on switching back to UnigineEditor. This component generates the physical objects and places them in the world. <details> <summary>ObjectGenerator.cs | Close</summary> ```csharp using System; using System.Collections; using System.Collections.Generic; using Unigine; public partial class ObjectGenerator : Component { private void Init() { // cube ObjectMeshDynamic box = Primitives.CreateBox(new vec3(1.0f)); box.TriggerInteractionEnabled = true; box.SetIntersection(true, 0); box.SetIntersectionMask(0x00000080, 0); // check the BulletIntersection bit box.WorldTransform = MathLib.Translate(new vec3(0.5f, 7.5f, 1.0f)); box.SetMaterialFilePath("materials/mesh_base_0.mat", "*"); box.Name = "box"; BodyRigid bodyBox = new BodyRigid(box); ShapeBox shapeBox = new ShapeBox(bodyBox, new vec3(1.0f)); new ShapeSphere(bodyBox, 0.5f); bodyBox.ShapeBased = false; bodyBox.Mass = 2.0f; // sphere ObjectMeshDynamic sphere = Primitives.CreateSphere(0.5f, 9, 32); sphere.TriggerInteractionEnabled = true; sphere.SetIntersection(true, 0); sphere.SetIntersectionMask(0x00000080, 0); // check the BulletIntersection bit sphere.WorldTransform = MathLib.Translate(new vec3(4.5f, 5.5f, 1.0f)); sphere.SetMaterialFilePath("materials/mesh_base_1.mat", "*"); sphere.Name = "sphere"; BodyRigid bodySphere = new BodyRigid(sphere); new ShapeSphere(bodySphere, 0.5f); bodySphere.ShapeBased = false; bodySphere.Mass = 2.0f; // capsule ObjectMeshDynamic capsule = Primitives.CreateCapsule(0.5f, 1.0f, 9, 32); capsule.TriggerInteractionEnabled = true; capsule.SetIntersection(true, 0); capsule.SetIntersectionMask(0x00000080, 0); // check the BulletIntersection bit capsule.WorldTransform = MathLib.Translate(new vec3(4.5f, 0.5f, 3.0f)); capsule.SetMaterialFilePath("materials/mesh_base_2.mat", "*"); capsule.Name = "capsule"; BodyRigid bodyCapsule = new BodyRigid(capsule); new ShapeCapsule(bodyCapsule, 0.5f, 1.0f); bodyCapsule.ShapeBased = false; bodyCapsule.Mass = 2.0f; } } ``` </details>
2. Switch back to the UnigineEditor and create a new *Dummy Node*, rename it to **"object_generator"**, and place it somewhere in the world.
3. Attach the created *ObjectGenerator* component to the **"object_generator"** node to make it generate physical objects on the initialization.
4. Create **3** new materials in the UnigineEditor: in the *Materials* window, right-click the `mesh_base` material and choose *Create Child*. By default, the created materials are named as specified in the previous code snippet (`mesh_base_*`). Move the materials to the `data/materials` folder of your project (create this folder if it doesn't exist). ![](materials.png)
5. Select materials one by one in the *Materials* window and in the *Parameters* window switch to the *Parameters* tab and click on the color field near **Albedo** to choose different colors for the objects via the color picker. ![](color_picker.png)
6. Save changes to the world via **Ctrl + S**.
7. Run the project via the UnigineEditor to see the spawned physical objects in the world.
