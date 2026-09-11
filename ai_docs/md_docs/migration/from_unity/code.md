# Migrating to UNIGINE from Unity: Programming


Game logic in a *Unity* project is implemented via *Script components*. You got used to determine GameObject's behavior by writing event functions like ***Start(), Update()***, etc.


UNIGINE has quite a similar concept, which can be easily adopted � [C# Component System](../../principles/component_system/component_system_cs/index.md), which is safe and secure and ensures high performance. Logic is written in C# components that can be assigned to any node in the scene. Each component has a set of functions (***Init(), Update()***, etc.), that are called by the corresponding functions of the engine [main loop](../../code/fundamentals/execution_sequence/code_update.md).


**Programming in UNIGINE using C# is not much different from programming in *Unity* software.** For example, let's compare how rotation is performed in *Unity* software:


```csharp
using UnityEngine;

public partial class MyComponent : MonoBehaviour
{
    public float speed = 90.0f;

    void Update()
    {
        transform.Rotate(0, speed * Time.deltaTime, 0, Space.Self);
    }
}

```


and in UNIGINE:


```csharp
using Unigine;
/* .. */

public partial class MyComponent : Component
{

	public float speed = 90.0f;

	private void Update()
	{

		node.Rotate(0, 0, speed * Game.IFps);

	}


```


The **Run** button is available in the Editor to [run an instance of the application](../../principles/component_system/component_system_cs/index.md#run) in a separate window. Along with the button, there are settings available to fine-tune run options.


![](../../principles/component_system/component_system_cs/run.png)


That's how we'll make the wheel rotate using C# Component System and run an instance to immediately check it:


Moreover in UNIGINE, you can also implement [Application Logic](../../code/fundamentals/execution_sequence/app_logic_system.md) for the whole application by writing code in the `AppWorldLogic.cs`, `AppSystemLogic.cs` and `AppEditorLogic.cs` files stored in the `source/` project folder.


To learn more about the execution sequence and how to build components, follow the links below:


- [Execution Sequence](../../code/fundamentals/execution_sequence/code_update.md)
- [Video tutorial on C# Component System](https://youtu.be/hHcUYQUlG00)


For those who prefer C++, UNIGINE allows creating [C++ applications](../../code/cpp/application.md) using C++ API and, if required, [C++ Component System](../../principles/component_system/component_system_cpp/index.md).


## Writing Gameplay Code


### Printing to Console


| *Unity* software | UNIGINE |
|---|---|
| ```csharp Debug.Log("Text: " + text); Debug.LogFormat("Formatted text: {0}", text); ``` | ```csharp Log.Message("Debug info:" + text + "\n"); Log.Message("Debug info: {0}\n", new vec3(1, 2, 3)); ``` |


#### See Also


- More types of messages in the *[Log](../../api/library/common/class.log_cpp.md)* class API
- The [video tutorial](https://youtu.be/6MUeatvw9v0) demonstrating how to print user messages to console using C# Component System


### Accessing the GameObject / Node from Component


| *Unity* software | UNIGINE |
|---|---|
| ```csharp GameObject this_go = gameObject; string n = gameObject.name; ``` | ```csharp Node this_node = node; string n = node.Name; ``` |


#### See Also


- The [video tutorial](https://youtu.be/KjEGI311NiA) demonstrating how to access nodes from components using C# Component System


### Working with Directions


In *Unity* software to get a vector on a certain axis while also considering the rotation of a game object in world coordinates, you use the corresponding properties of the ***Transform*** component. The same vector in UNIGINE is got by using *[Node.GetWorldDirection()](../../api/library/nodes/class.node_cpp.md#getWorldDirection_int_vec3)* function:


| *Unity* software | UNIGINE |
|---|---|
| ```csharp Vector3 forward = transform.forward; Vector3 right = transform.right; Vector3 up = transform.up; transform.Translate(forward * speed * Time.deltaTime); ``` | ```csharp vec3 forward = node.GetWorldDirection(MathLib.AXIS.Y); vec3 right = node.GetWorldDirection(MathLib.AXIS.X); vec3 up = node.GetWorldDirection(MathLib.AXIS.Z); node.Translate(forward * speed * Game.IFps); ``` |


> **Notice:** Intances of the [Players-Related classes](../../api/library/players/index.md) use different direction vectors and are to be treated [correspondingly](../../code/fundamentals/matrices/index.md#get_direction).


#### See Also


- [Coordinate System](../../code/fundamentals/matrices/index.md#coordinate_system) in UNIGINE


### Smoother Gameplay with DeltaTime / IFps


In *Unity* software to ensure that certain actions are performed at the same time periods regardless of the framerate (e.g. change something once per second etc) you use a scaling multiplier **Time.deltaTime** (the time in seconds it took to complete the last frame). The same thing in UNIGINE is called **[Game.IFps](../../api/library/engine/class.game_cpp.md#getIFps_float)**:


| *Unity* software | UNIGINE |
|---|---|
| ```csharp transform.Rotate(0, speed * Time.deltaTime, 0, Space.Self); ``` | ```csharp node.Rotate(0, 0, speed * Game.IFps); ``` |


### Drawing Debug Data


*Unity* software:


```csharp
Debug.DrawLine(Vector3.zero, new Vector3(5, 0, 0), Color.white, 2.5f);

Vector3 forward = transform.TransformDirection(Vector3.forward) * 10;
Debug.DrawRay(transform.position, forward, Color.green);

```


UNIGINE:


```csharp
Visualizer.Enabled = true;

/*..*/

Visualizer.RenderLine3D(vec3.ZERO, new vec3(5, 0, 0), vec4.ONE);
Visualizer.RenderVector(node.Position, node.GetDirection(MathLib.AXIS.Y) * 10, new vec4(1, 0, 0, 1));


```


> **Notice:** The visualizer can be toggled on and off via `show_visualizer 1` console command as well.


#### See Also


- More types of visualizations in the *[Visualizer](../../api/library/engine/class.visualizer_cpp.md)* class API.


### Loading a Scene


| *Unity* software | UNIGINE |
|---|---|
| ```csharp SceneManager.LoadScene("YourSceneName",LoadSceneMode.Single); ``` | ```csharp World.LoadWorld("YourSceneName"); ``` |


### Accessing a Component from the GameObject / Node


*Unity* software:


```csharp
MyComponent my_component = gameObject.GetComponent<MyComponent>();

```


UNIGINE:


```csharp
MyComponent my_component = node.GetComponent<MyComponent>();

MyComponent my_component = GetComponent<MyComponent>(node);


```


#### Accessing Standard Components


*Unity* software provides component-based workflow so such standard entities as *MeshRenderer, Rigidbody, Collider, Transform* and other are treated as usual components.


In UNIGINE, analogs for these entities are accessed differently. For example, to access an entity of a type derived from the *Node* class (e.g. *ObjectMeshStatic*), you should [downcast the instance](#code_cast_type) to the corresponding class. Let's consider these most popular use cases:


*Unity* software:


```csharp
// accessing the transform of the game object
Transform transform_1 = gameObject.GetComponent<Transform>();
Transform transform_2 = gameObject.transform;

// accessing the Mesh Renderer component
MeshRenderer mesh_renderer = gameObject.GetComponent<MeshRenderer>();

// accessing the Rigidbody component
Rigidbody rigidbody = gameObject.GetComponent<Rigidbody>();

// accessing a collider
Collider collider = gameObject.GetComponent<Collider>();
BoxCollider boxCollider = collider as BoxCollider;

```


UNIGINE:


```csharp
// getting the transformation matrix of the node
dmat4 transform = node.WorldTransform;

// downcasting the node to the ObjectMeshStatic class
ObjectMeshStatic mesh_static = node as ObjectMeshStatic;

// accessing the rigid body assigned to the node
Body body = (node as Unigine.Object).Body;
BodyRigid rigid = body as BodyRigid;

// fetch all collision shapes of the ShapeBox type
for (int i = 0; i < body.NumShapes; i++)
{
	Shape shape = body.GetShape(i);
	if (shape is ShapeBox)
	{
		ShapeBox shape_box = shape as ShapeBox;
		/* some code */
	}
}


```


### Finding GameObjects / Nodes


*Unity* software:


```csharp
// Find a GameObject by name
GameObject myGameObj = GameObject.Find("My Game Object");

// Find the child named "ammo" of the gameobject "magazine" (magazine is a child of "gun").
Transform ammo_transform = gameObject.transform.Find("magazine/ammo");
GameObject ammo = ammo_transform.gameObject;

// Find GameObjects by the type of component assigned
MyComponent[] components = Object.FindObjectsOfType<MyComponent>();
foreach (MyComponent component in components)
{
        // ...
}

// Find GameObjects by tag
GameObject[] taggedGameObjects = GameObject.FindGameObjectsWithTag("MyTag");
foreach (GameObject gameObj in taggedGameObjects)
{
        // ...
}

```


UNIGINE:


```csharp
// Find a Node by name
Node my_node = World.GetNodeByName("my_node");

// Find all nodes having this name
List<Node> nodes = new List<Node>();
World.GetNodesByName("my_node", nodes);

// Find the index of a direct child node
int index = node.FindChild("child_node");
Node direct_child = node.GetChild(index);

// Perform a recursive descend down the hierarchy to find a child Node by name
Node child = node.FindNode("child_node", 1);

// Find Nodes by the type of component assigned
MyComponent[] my_comps = FindComponentsInWorld<MyComponent>();
foreach(MyComponent comp in my_comps)
{
	Log.Message("{0}\n",comp.node.Name);
}


```


### Casting From Type to Type


**Downcasting** (from a *pointer-to-base* to a *pointer-to-derived*) is performed similarly in both engines, by using the C# ***as*** native construction:


| *Unity* software | UNIGINE |
|---|---|
| ```csharp Collider collider = gameObject.GetComponent<Collider>; BoxCollider boxCollider = collider as BoxCollider; ``` | ```csharp Node node = World.GetNodeByName("my_mesh"); ObjectMeshStatic mesh = node as ObjectMeshStatic; ``` |


To perform **Upcasting** (from a *pointer-to-derived* to a *pointer-to-base*) you can simply use the instance itself:


| *Unity* software | UNIGINE |
|---|---|
| ```csharp Collider collider = gameObject.GetComponent<Collider>; BoxCollider boxCollider = collider as BoxCollider; Collider coll = boxCollider; ``` | ```csharp Node node = World.GetNodeByName("my_mesh"); ObjectMeshStatic mesh = node as ObjectMeshStatic; Unigine.Object obj = mesh; ``` |


### Destroy GameObject/Node


| *Unity* software | UNIGINE |
|---|---|
| ```csharp Destroy(maGameObject); // destroy the game object with 1 second delay Destroy(maGameObject, 1); ``` | ```csharp node.DeleteLater(); // recommended option //called between the current and the next frames node.DeleteForce(); // called during the same frame but unsafe ``` |


To perform deferred removal of a node in UNIGINE, you can create a component that will be responsible for the timer and deletion.


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class LifeTimeController : Component
{
	public float lifetime = 5.0f;

	void Update()
	{
		lifetime = lifetime - Game.IFps;
		if (lifetime < 0)
		{
			// destroy current node with its properties and components
			node.DeleteLater();
		}
	}
}

```


And then use it for any node in any of your other logic components.


```csharp
public partial class MyComponent : Component
{

	private void Update()
	{

		if (/a reason to die/)

		{
			LifeTimeController lc = node.AddComponent<LifeTimeController>();
			lc.lifetime = 2.0f;
		}

	}
}


```


### Instantiating Prefab / Node Reference


In *Unity* software, you instantiate a *prefab* using the *Object.Instantiate* function:


```csharp
using UnityEngine;

public partial class MyComponent : MonoBehaviour
{
public GameObject myPrefab;

void Start()
{
	Instantiate(myPrefab, new Vector3(0, 0, 0), Quaternion.identity);
}
}

```


Then, you should specify the *prefab* to be instantiated in the script component parameters:


![](unity_drag_prefab.png)


In UNIGINE, you can access any node via a [component parameter](../../api/library/common/logic/component_system/cs/class.component.md#parameters) as well, and clone it via *[Node.Clone()](../../api/library/nodes/class.node_cpp.md#clone_Node)*. However, assets are not nodes, they belong to the file system. To access assets from components use the following parameters types:


- *[AssetLink](../../api/library/common/logic/component_system/cs/class.assetlink.md)* � for assets of any type,
- *[AssetLinkNode](../../api/library/common/logic/component_system/cs/class.assetlinknode.md)* � for hierarchies saved as *[NodeReference](../../migration/from_unity/index.md#prefabs)* (`*.node` assets) exclusively.


The same way you will need to specify the asset in UnigineEditor:


![](unigine_drag_noderef.png)


You can also use *[World.LoadNode](../../api/library/engine/class.world_cpp.md#loadNode_cstr_int_Node)* to load a hierarchy of nodes from a `.node` asset manually by providing the [virtual path](../../principles/filesystem/index_cpp.md#virtual_paths) to it:


```csharp
public partial class MyComponent : Component
{

	public Node node_to_clone;
	public AssetLinkNode node_to_spawn;

	private void Init()
	{

		Node cloned = node_to_clone.Clone();

		Node spawned = node_to_spawn.Load(node.WorldPosition, quat.IDENTITY);

		Node spawned_manually = World.LoadNode("nodes/node_reference.node");

	}
}


```


You can also spawn the node reference as a single node (without extracting the content) in the world:


```csharp
public partial class MyComponent : Component
{

	private void Init()
	{

		NodeReference nodeRef = new NodeReference("nodes/node_reference_0.node");

	}
}


```


NodeReferences have a set of [peculiarities](../../api/library/nodes/class.nodereference_cpp.md) which are to be taken into account.


### Protect GameObject/Node from Destroying


In Unity, the load of a new Scene destroys all current Scene objects. Using *Object.DontDestroyOnLoad* allows for preserving an Object during scene loading.


In UNIGINE, nodes have an intrinsic [Lifetime](../../api/library/nodes/class.node_cpp.md#delete_node) property accountable for their life cycle. By default, each node is assigned the [**Node.LIFETIME.WORLD**](../../api/library/nodes/class.node_cpp.md#LIFETIME_WORLD) option, i.e. it shall be deleted when the current world is closed. But you can also switch the node's lifetime to **ENGINE** and **MANUAL** mode if necessary.


| *Unity* software | UNIGINE |
|---|---|
| ```csharp public class data_transfer : MonoBehaviour { void Awake() { DontDestroyOnLoad(transform.gameObject); } } ``` | ```csharp node.Lifetime = Node.LIFETIME.ENGINE; // This node will not be deleted when switching to another world. // It will remain in memory until the application is finished. ``` |


## Running Scripts in the Editor


You are likely to be accustomed that *Unity* software enables you to extend the Editor using C# scripts. For this purpose you can use special attributes in your scripts:


- ***[ExecuteInEditMode]*** � to execute the script logic during **Edit** mode, while your application is not running.
- ***[ExecuteAlways]*** � to execute the script logic both as part of **Play** mode and when editing.


For example, this is how you write a component that makes *GameObject* orient towards the certain point in the scene:


```csharp
//C# Example (LookAtPoint.cs)
using UnityEngine;
[ExecuteInEditMode]
public partial class LookAtPoint : MonoBehaviour
{
    public Vector3 lookAtPoint = Vector3.zero;

    void Update()
    {
        transform.LookAt(lookAtPoint);
    }
}

```


UNIGINE doesn't support executing C# logic inside the Editor. The most common way to extend functionality of UnigineEditor is [*C++ plugin*](../../editor2/extensions/index.md).


For quick tests and prototyping, you can write logic in *[UnigineScript](../../code/uniginescript/index.md)* to optimize project creation process. *UnigineScript* is available for any programming workflow you have chosen for your project including C# .NET.


There are two methods to [add a script to the project](../../code/uniginescript/add_scripts/index.md):


- **By creating a *World* script**. Perform the following steps: After that the script logic will be executed in both Editor and application.

  1. Create a `.usc` script asset. ![](unigine_usc_create_script.png)
  2. Write logic inside this script file. If necessary, add a condition checking if the Editor is loaded: ```cpp #include <core/unigine.h> vec3 lookAtPoint = vec3_zero; Node node; int init() { node = engine.world.getNodeByName("material_ball"); return 1; } int update() { if(engine.editor.isLoaded()) node.worldLookAt(lookAtPoint); return 1; } ```
  3. Select the current world and specify the world script for it. Click *Apply* and reload the world. ![](unigine_usc_apply_script.png)
  4. Check the *Console* window for errors.
- **By using *WorldExpression***. For the same purpose you can use a built-in *[WorldExpression](../../objects/worlds/world_expression/index.md)* node executing scripts when added to the world:

  1. Click *Create -> Logic -> Expression* and place the new *WorldExpression* node in the world.
  2. Write logic in *UnigineScript* in the **Source** field: ```cpp { vec3 lookAtPoint = vec3_zero; Node node = engine.world.getNodeByName("my_node"); node.worldLookAt(lookAtPoint); } ```
  3. Check the *Console* window for errors.
  4. The logic will be executed immediately.


## Triggers


In addition to collision detection, *Unity* **Collider** component is accountable for being a *Trigger* that is executed when one collider enters the space of another.


```csharp
public partial class MyComponent : MonoBehaviour
{
    void Start()
    {
        collider.isTrigger = true;
    }
    void OnTriggerEnter(Collider other)
    {
        // ...
    }
    void OnTriggerExit(Collider other)
    {
        // ...
    }
}

```


In UNIGINE, *Trigger* is a special built-in node that raises events in certain situations:


- **[NodeTrigger](../../api/library/nodes/class.nodetrigger_cpp.md)** is used to track events for a particluar node (to which the *Trigger* is attached as a child) - it executes event handlers when the *Trigger* node is [enabled](../../api/library/nodes/class.nodetrigger_cpp.md#getEventEnabled_Event) or the *Trigger* node [position](../../api/library/nodes/class.nodetrigger_cpp.md#getEventPosition_Event) has changed.
- **[WorldTrigger](../../api/library/worlds/class.worldtrigger_cpp.md)** is used to track events for any node (collider or not) that gets [inside](../../api/library/worlds/class.worldtrigger_cpp.md#getEventEnter_Event) or [outside](../../api/library/worlds/class.worldtrigger_cpp.md#getEventLeave_Event) of it.
- **[PhysicalTrigger](../../api/library/physics/class.physicaltrigger_cpp.md)** is used to track events for physical objects get [inside](../../api/library/physics/class.physicaltrigger_cpp.md#getEventEnter_Event) or [outside](../../api/library/physics/class.physicaltrigger_cpp.md#getEventLeave_Event) of it. > **Notice:** *PhysicalTrigger* does not handle collision events, for that purpose [Bodies and Joints](../../code/fundamentals/events/index_cpp.md#physics) provide their own events.


**WorldTrigger** is the most common type that can be used in gameplay. Here is an example on how to use it:


```csharp
public partial class MyComponent : Component
{

	WorldTrigger trigger;

	void enter_event_handler(Node incomer)
	{
		Log.Message("\n{0} has entered the trigger space\n", incomer.Name);
	}

	private void Init()
	{

		trigger = node as WorldTrigger;
		if(trigger != null)
		{
			trigger.EventEnter.Connect(enter_event_handler);
			trigger.EventLeave.Connect( leaver => Log.Message("{0} has left the trigger space", leaver.Name));
		}

	}
}


```


## Input


*Unity* Conventional Game Input:


```csharp
public partial class MyPlayerController : MonoBehaviour
{
    void Update()
    {
        if (Input.GetButtonDown("Fire"))
        {
            // ...
        }
        float horizontal = Input.GetAxis("Horizontal");
        float vertical = Input.GetAxis("Vertical");
        // ...
    }
}

```


UNIGINE:


```csharp
public partial class MyPlayerController : Component
{

	void Update()
	{

		if(Input.IsMouseButtonDown(Input.MOUSE_BUTTON.LEFT))
		{
			Log.Message("Left mouse button was clicked at {0}\n", Input.MousePosition);
		}

		if (Input.IsKeyDown(Input.KEY.Q) && !Unigine.Console.Active)
		{
			Log.Message("Q was pressed and the Console is not active.\n");
			Engine.Quit();
		}

	}
}


```


You can also use the **[ControlsApp](../../api/library/controls/class.controlsapp_cpp.md)** class to handle control bindings. To configure the bindings, open the *[Controls](../../editor2/settings/controls/index.md)* settings:


```csharp
public partial class MyPlayerController : Component
{

	private void Init()
	{

		// remapping states to keys and buttons
		ControlsApp.SetStateKey(Controls.STATE_FORWARD, Input.KEY.W);
		ControlsApp.SetStateKey(Controls.STATE_BACKWARD, Input.KEY.S);
		ControlsApp.SetStateKey(Controls.STATE_MOVE_LEFT, Input.KEY.A);
		ControlsApp.SetStateKey(Controls.STATE_MOVE_RIGHT, Input.KEY.D);
		ControlsApp.SetStateMouseButton(Controls.STATE_JUMP, Input.MOUSE_BUTTON.LEFT);

	}

	void Update()
	{

		if (ControlsApp.ClearState(Controls.STATE_FORWARD) != 0)
		{
			Log.Message("FORWARD key pressed\n");
		}
		else if (ControlsApp.ClearState(Controls.STATE_BACKWARD) != 0)
		{
			Log.Message("BACKWARD key pressed\n");
		}
		else if (ControlsApp.ClearState(Controls.STATE_MOVE_LEFT) != 0)
		{
			Log.Message("MOVE_LEFT key pressed\n");
		}
		else if (ControlsApp.ClearState(Controls.STATE_MOVE_RIGHT) != 0)
		{
			Log.Message("MOVE_RIGHT key pressed\n");
		}
		else if (ControlsApp.ClearState(Controls.STATE_JUMP) != 0)
		{
			Log.Message("JUMP button pressed\n");
		}

	}
}


```


## Raycasting


In *Unity* software, *Physics.Raycast* is used. *GameObject* should have a *Collider* component attached to take part in raycasting:


```csharp
using UnityEngine;
public partial class ExampleClass : MonoBehaviour
{
	public Camera camera;

    void Update()
    {
    	// ignore the 2nd layer
        int layerMask = 1 << 2;
        layerMask = ~layerMask;

        RaycastHit hit;
        Ray ray = camera.ScreenPointToRay(Input.mousePosition);
        if (Physics.Raycast(ray, out hit, Mathf.Infinity, layerMask))
        {
            Debug.DrawRay(transform.position, transform.TransformDirection(Vector3.forward) * hit.distance, Color.yellow);
            Debug.Log("Did Hit");
        }
        else
        {
            Debug.DrawRay(transform.position, transform.TransformDirection(Vector3.forward) * 1000, Color.white);
            Debug.Log("Did not Hit");
        }
    }
}

```


In UNIGINE the same is handled by [Intersections](../../code/usage/intersections/index_cpp.md):


There are several types of them in UNIGINE:


- **World Intersections** - ray intersections with object surfaces (or intersections between object bound volumes). This type can be used to select objects with the mouse cursor
- **Physics Intersections** - intersections with collider geometry or with physical objects having bodies and collider shapes assigned. *Physics Intersections* use a separate mask with the corresponding name (*[Physics Intersection Mask](../../principles/bit_masking/index.md#physics_intersection_mask)*), other than the one used for *World Intersections* (*[Intersection Mask](../../principles/bit_masking/index.md#intersection_mask)*). This offers more flexibility enabling you to control them independently. *Physics Intersections* can be used, for example, to detect collisions of spawned particles with physical shapes and bodies, or static collider surfaces to ensure proper interaction, or as a quick way to detect collisions for raycast-wheels of a simulated ground vehicle, or to check if a destructible object or a player was hit by a projectile.


The example of checking if there is an object under the mouse cursor given above for *Unity Software* is a case of using **World Intersections** in UNIGINE, and it will look like this:


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

#region Math Variables
#if UNIGINE_DOUBLE
using Scalar = System.Double;
using Vec3 = Unigine.dvec3;
#else
using Scalar = System.Single;
using Vec3 = Unigine.vec3;
#endif
#endregion

public partial class IntersectionExample : Component
{
	void Init()
	{
		Visualizer.Enabled = true;
	}
	void Update()
	{
		ivec2 mouse = Input.MousePosition;
		float length = 100.0f;
		Vec3 start = Game.Player.WorldPosition;
		Vec3 end = start + new Vec3(Game.Player.GetDirectionFromMainWindow(mouse.x, mouse.y)) * length;

		// ignore surfaces that have certain bits of the Intersection mask enabled
		int mask = ~(1 << 2 | 1 << 4);

		WorldIntersectionNormal intersection = new WorldIntersectionNormal();

		Unigine.Object obj = World.GetIntersection(start, end, mask, intersection);

		if (obj)
		{
			Vec3 point = intersection.Point;
			vec3 normal = intersection.Normal;
			Visualizer.RenderVector(point, point + normal, vec4.ONE);
			Log.Message("Hit {0} at {1}\n", obj.Name, point);
		}
	}
}

```


There are also [**Game Intersections**](../../code/usage/intersections/index_cpp.md#game_intersection) - intersections with pathfinding nodes like [obstacles](../../api/library/pathfinding/class.obstacle_cpp.md).
