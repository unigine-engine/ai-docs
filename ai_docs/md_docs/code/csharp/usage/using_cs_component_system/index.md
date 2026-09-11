# Using C# Component System


The **[C# Component System](../../../../principles/component_system/component_system_cs/index.md)** enables you to implement your application's logic via a set of building blocks � **components**, and assign these blocks to nodes. A logic component integrates a node and a C# class containing logic implementation.


This example demonstrates how to:


- Decompose application logic into building blocks.
- Create your own logic components.
- Implement interaction between your components.
- Apply logic implementation to game objects.


Let's make a simple game to demonstrate how the whole system works.


### Game Description


In the center of the play area, we are going to have an object (*Pawn*) controlled by the player via the keyboard. It has certain amount of HP and movement parameters (movement and rotation speed).


Four corners of the play area are occupied by rotating objects (*Spinner*) that throw other small objects (*Projectile*) in all directions while rotating.


Each *Projectile* moves along a straight line in the directon it has been initially thrown by *Spinner*. If a *Projectile* hits *Pawn*, *Pawn* takes damage according to the value set for the hitting *Projectile* (each of them has a random speed and damage value). *Pawn* is destroyed if the amount of HP drops below zero.


![](game.gif)


We use boxes for simplicity, but you can easily replace them with any other objects.


The basic workflow for implementing application logic using the Component System is given below.


## Prepare a Project


Before we can start creating components and implementing our game logic, we should create a project.


1. [Create](../../../../sdk/projects/index_cpp.md#creation) a new empty C# project. Open the **SDK Browser**, go to *Templates* tab and click the *Create Project* button on the *C# Empty* template card. In the new window, click *Create New Project*. ![](../../../../sdk/projects/create_project_cs.png)
2. After the project is created it will be added to the *My Projects* tab. Run the Editor by clicking **[Open Editor](../../../../editor2/index.md#run)**. ![](../../../../start/quick_start/setup_project/projects_cs.png)
3. Prepare the world: delete or disable unnecessary objects, such as *static_content, dynamic_content*, etc.


## Decompose Application Logic into Building Blocks


First of all, we should decompose our application logic in terms of building blocks � components. So, we should define parameters for each component (all these parameters will be described in a corresponding `.cs` file) and decide in which functions of the [execution sequence](../../../../code/fundamentals/execution_sequence/index.md) the component's logic will be implemented.


For our small game, we are going to use one component for each type of object. Thus, we need **3** components:


- **Pawn** with the following parameters: We are going to initialize *Pawn*, do something with it each frame, and report a message, when *Pawn* dies. Therefore, this logic will be implemented inside the *Init()*, *Update()*, and *Shutdown()* methods.

  - *name* � name of *Pawn*
  - *moving speed* � how fast *Pawn* moves
  - *rotation speed* � how fast *Pawn* rotates
  - *health* � HP count for *Pawn*
- **Spinner** with the following parameters: We are going to initialize *Spinner* and do something with it each frame. Therefore, this logic will go to the *Init()* and *Update()*.

  - *rotation speed* � how fast *Spinner* rotates
  - *acceleration* � how fast *Spinner*'s rotation rate increases
  - *node* to be used as *Projectile*
  - *minimum spawn delay*
  - *maximum spawn delay*
- **Projectile** with the following parameters: As for *Projectile*, it will be spawned and initialized by *Spinner*. The only thing we are going to do with it, is checking for a hit and controlling the life time left every frame. All this goes to *Update()*.

  - *speed* � how fast *Projectile* moves
  - *life time* � how long *Projectile* lives
  - *damage* � how much damage *Projectile* causes to *Pawn* it hits


## Create a C# Component for Each Object


For each of our objects, we should describe logic in a separate C# component. Therefore, we should do the following:


- [Create a C# component](../../../../principles/component_system/component_system_cs/index.md#create) for each game entity. ![](../../../../principles/component_system/component_system_cs/create_component.gif)
- Open the source code in the default IDE by double clicking any `*.cs` asset.
- Declare all parameters defined above with their default values (if any).
- Declare which methods we are going to use to implement our logic, and during which stages of the [execution sequence](../../../../code/fundamentals/execution_sequence/index.md) to call them. ```csharp void Init() { } void Update() { } void Shutdown() { } ```
- Declare all necessary auxiliary parameters and functions.


Thus, for our *Pawn, Spinner*, and *Projectile* components, we will have the following classes:


> **Notice:** You can copy this sample code and paste it to your source files, however, be careful not to change the values of the ***[Component(PropertyGuid = "")]*** attributes.


<details>
<summary>Pawn.cs | Close</summary>

**Pawn.cs**


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;
#if UNIGINE_DOUBLE
using Vec3 = Unigine.dvec3;
using Vec4 = Unigine.dvec4;
using Mat4 = Unigine.dmat4;
#else
	using Vec3 = Unigine.vec3;
	using Vec4 = Unigine.vec4;
	using Mat4 = Unigine.mat4;
#endif

public partial class Pawn : Component
{
	// parameters
	public String name = "Pawn1";		// Pawn's name
	public int health = 200;			// health points
	public float move_speed = 4.0f;		// move speed (meters/s)
	public float turn_speed = 90.0f;	// turn speed (deg/s)

	// auxiliary parameters
	private Controls controls;
	private Player player;

	private float damage_effect_timer = 0.0f;
	private Mat4 default_model_view;

	private void Init()
	{
	}

	private void Update()
	{
	}

	private void Shutdown()
	{
	}

	// method to be called when the Pawn is hit by a Projectile
	public void hit(int damage)
	{
	}
	// a method for damage visualization
	private void show_damage_effect()
	{
	}
}

```

</details>


<details>
<summary>Spinner.cs | Close</summary>

**Spinner.cs**


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class Spinner : Component
{
	// parameters
	public float turn_speed = 30.0f;
	public float acceleration = 5.0f;

	public Node spawn_node;
	public float min_spawn_delay = 1.0f;
	public float max_spawn_delay = 4.0f;

	private float start_turn_speed = 0.0f;
	private float color_offset = 0.0f;
	private float time_to_spawn = 0.0f;
	private Material material;

	private void Init()
	{
	}

	private void Update()
	{
	}

	// an auxiliary method for color conversion H - [0, 360), S,V - [0, 1]
	private vec3 hsv2rgb(float h, float s, float v)
	{
	}
}

```

</details>


<details>
<summary>Projectile.cs | Close</summary>

**Projectile.cs**


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class Projectile : Component
{
	// parameters
	public float speed = 5.0f;
	public float lifetime = 5.0f;	// life time of the projectile (declaration with a default value)
	public int damage;				// damage caused by the projectile (declaration with no default value)

	void Init()
	{
		// write here code to be called on component initialization

	}
}

```

</details>


All saved changes of the components source code make the components update with no compilation required when the Editor window gets focus.


## Implement Each Component's Logic


After making necessary declarations, we should implement logic for all our components.


### Pawn's Logic


The *Pawn*'s logic is divided into the following elements:


- **Initialization** � here we set necessary parameters, and *Pawn* reports its name: ```csharp Log.Message("PAWN: INIT \"{0}\"\n", name); ```
- **Main loop** � here we implement the player's keyboard control using methods of the [Input](../../../../api/library/controls/class.input_cpp.md) class. > **Notice:** To access the node from the component, we can simply use **node**, e.g. to get the current [node's direction](../../../../api/library/nodes/class.node_cpp.md#getWorldDirection_int_vec3) we can write: > > > ```csharp > vec3 direction = node.GetWorldDirection(MathLib.AXIS.Y); > ```
- **Shutdown** � here we implement actions to be performed when *Pawn* dies. We'll just print a message to the console.
- **Auxiliary** � a method to be called when *Pawn* is hit, and some visual effects.


Implementation of the *Pawn*'s logic is given below:


<details>
<summary>Pawn.cs | Close</summary>

**Pawn.cs**


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;
#if UNIGINE_DOUBLE
using Vec3 = Unigine.dvec3;
using Vec4 = Unigine.dvec4;
using Mat4 = Unigine.dmat4;
#else
	using Vec3 = Unigine.vec3;
	using Vec4 = Unigine.vec4;
	using Mat4 = Unigine.mat4;
#endif

public partial class Pawn : Component
{
	// parameters
	public String name = "Pawn1";		// Pawn's name
	public int health = 200;			// health points
	public float move_speed = 4.0f;		// move speed (meters/s)
	public float turn_speed = 90.0f;	// turn speed (deg/s)

	// auxiliary parameters
	private Controls controls;
	private Player player;

	private float damage_effect_timer = 0.0f;
	private Mat4 default_model_view;

	private const float DAMAGE_EFFECT_TIME = 0.5f;
[Method(Order=0)]
	private void Init()
	{
		player = Game.Player;
		controls = player.Controls;

		default_model_view = (Mat4) player.Camera.Modelview;
		damage_effect_timer = 0.0f;
		show_damage_effect();

		Log.Message("PAWN: INIT \"{0}\"\n", name);
	}

	private void Update()
	{
		// get delta time between frames
		float ifps = Game.IFps;

		// show damage effect
		if (damage_effect_timer > 0)
		{
			damage_effect_timer = Math.Clamp(damage_effect_timer - ifps, 0.0f, DAMAGE_EFFECT_TIME);
			show_damage_effect();
		}

		// if console is opened we disable any controls
		if (Unigine.Console.Active)
			return;

		// get the forward direction vector of the node
		vec3 direction = node.GetWorldDirection(MathLib.AXIS.Y);

		// checking controls states and changing pawn position and rotation
		if (Input.IsKeyPressed(Input.KEY.UP) || Input.IsKeyPressed(Input.KEY.W))
		{
			node.WorldPosition += direction * move_speed * ifps;
		}

		if (Input.IsKeyPressed(Input.KEY.DOWN) || Input.IsKeyPressed(Input.KEY.S))
		{
			node.WorldPosition -= direction * move_speed * ifps;
		}

		if (Input.IsKeyPressed(Input.KEY.LEFT) || Input.IsKeyPressed(Input.KEY.A))
		{
			node.Rotate(0.0f, 0.0f, turn_speed * ifps);
		}

		if (Input.IsKeyPressed(Input.KEY.RIGHT) || Input.IsKeyPressed(Input.KEY.D))
		{
			node.Rotate(0.0f, 0.0f, -turn_speed * ifps);
		}
	}

	private void Shutdown()
	{
		Log.Message("PAWN: DEAD!\n");
	}

	// method to be called when the Pawn is hit by a Projectile
	public void hit(int damage)
	{
		// take damage
		health = health - damage;

		// show effect
		damage_effect_timer = DAMAGE_EFFECT_TIME;
		show_damage_effect();

		Log.Message("PAWN: damage taken ({0}) - HP left ({1})\n", damage, health);

		// destroy
		if (health <= 0)
		{
			health = 0;
			node.DeleteLater();
		}

	}
	// a method for damage visualization
	private void show_damage_effect()
	{
		float strength = damage_effect_timer / DAMAGE_EFFECT_TIME;
		Render.FadeColor = new vec4(0.5f, 0, 0, MathLib.Saturate(strength - 0.5f));
		player.Camera.Modelview = default_model_view * new Mat4(
			MathLib.RotateX(Game.GetRandomFloat(-5, 5) * strength) *
			MathLib.RotateY(Game.GetRandomFloat(-5, 5) * strength));
	}
}

```

</details>


### Projectile's Logic


The *Projectile*'s logic is simpler � we just have to perform a check each frame whether we hit *Pawn* or not. This means that we have to access the *Pawn* component from the *Projectile* component.


> **Notice:** To access certain component on a certain node (e.g. the one that was intersected in our case) we can use the ComponentSystem's *[GetComponent<T>()](../../../../api/library/common/logic/component_system/cs/class.componentsystem.md#getComponent_Node_bool_T)* or the Node's *[GetComponent<T>()](../../../../api/library/nodes/class.node_cpp.md)* functions:
>
>
> ```csharp
> // get the component assigned to a node by type "MyComponent"
> MyComponent my_component = GetComponent<MyComponent>(some_node);
>
> // do the same by using the function of node
> my_component = some_node.GetComponent<MyComponent>();
>
> // access some method of MyComponent
> my_component.SomeMyComponentMethod();
>
> ```


*Projectile* has a limited life time, so we should destroy the node when its life time is expired. Use the *DeleteLater()* method for this purpose.


```csharp
node.DeleteLater();
```


Implementation of the *Projectile*'s logic is given below:


<details>
<summary>Projectile.cs | Close</summary>

**Projectile.cs**


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class Projectile : Component
{
	// parameters
	public float speed = 5.0f;
	public float lifetime = 5.0f;	// life time of the projectile (declaration with a default value)
	public int damage;				// damage caused by the projectile (declaration with no default value)

	private void Update()
	{
		// get delta time between frames
		float ifps = Game.IFps;

		// get the forward direction vector of the node
		vec3 direction = node.GetWorldDirection(MathLib.AXIS.Y);

		// move forward
		node.WorldPosition +=  direction * speed * ifps;

		// lifetime
		lifetime = lifetime - ifps;
		if (lifetime < 0)
		{
			// destroy current node with its properties and components
			node.DeleteLater();
			return;
		}

		// finding nodes intersecting a bounding box and listing them if any
		List<Node> nodes = new List<Node>();
		World.GetIntersection(node.WorldBoundBox, nodes);
		if (nodes.Count > 1) // (because the current node is also in this list)
		{
			foreach (Node n in nodes)
			{
				Pawn pawn = n.GetComponent<Pawn>();

				if (pawn != null)
				{
					// hit the player!
					pawn.hit(damage);

					// ...and destroy the current node
					node.DeleteLater();
					return;
				}
			}
		}
	}

	public void setMaterial(Material mat)
	{
		(node as Unigine.Object).SetMaterial(mat, "*");
	}

}

```

</details>


### Spinner's Logic


The *Spinner*'s logic is divided into the following elements:


- **Initialization** � here we set necessary parameters to be used in the main loop.
- **Main loop** � here we rotate our *Spinner* and spawn nodes with *Projectile* components. We also set some parameters of *Projectile*. You can change variables of another component directly: ```csharp component.int_parameter += 1; ```
- **Auxiliary** � color conversion function.


Implementation of the *Spinner*'s logic is given below:


<details>
<summary>Spinner.cs | Close</summary>

**Spinner.cs**


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class Spinner : Component
{
	// parameters
	public float turn_speed = 30.0f;
	public float acceleration = 5.0f;

	public Node spawn_node;
	public float min_spawn_delay = 1.0f;
	public float max_spawn_delay = 4.0f;

	private float start_turn_speed = 0.0f;
	private float color_offset = 0.0f;
	private float time_to_spawn = 0.0f;
	private Material material;

	private void Init()
	{
		 // get current material (from the first surface)
		Unigine.Object obj = node as Unigine.Object;
		if (obj != null && obj.NumSurfaces > 0)
			material = obj.GetMaterialInherit(0);

		// init randoms
		time_to_spawn = Game.GetRandomFloat(min_spawn_delay, max_spawn_delay);
		color_offset = Game.GetRandomFloat(0, 360.0f);
		start_turn_speed = turn_speed;
	}

	private void Update()
	{
		// rotate spinner
		float ifps = Game.IFps;
		turn_speed = turn_speed + acceleration * ifps;
		node.Rotate(0.0f, 0.0f, turn_speed * ifps);

		// change color
		int id = material.FindParameter("albedo_color");
		if (id != -1)
		{
			float hue = MathLib.Mod(Game.Time * 60.0f + color_offset, 360.0f);
			material.SetParameterFloat4(id, new vec4(hsv2rgb(hue, 1, 1), 1.0f));
		}

		// spawn projectiles
		time_to_spawn -= ifps;
		if (time_to_spawn < 0 && spawn_node != null)
		{
			// reset timer and increase difficulty
			time_to_spawn = Game.GetRandomFloat(min_spawn_delay, max_spawn_delay) / (turn_speed / start_turn_speed);

			// create node
			Node spawned = spawn_node.Clone();
			spawned.Enabled = true;
			spawned.WorldTransform = node.WorldTransform;

			// create component
			Projectile proj_component = AddComponent<Projectile>(spawned);

			// change variables inside another component
			proj_component.speed = Game.GetRandomFloat(proj_component.speed * 0.5f, proj_component.speed * 1.5f);
			proj_component.damage = Game.GetRandomInt(75, 100);
			proj_component.lifetime = Game.GetRandomInt(75, 100);

			// call public method of another component
			proj_component.setMaterial(material);
		}

	}

	// an auxiliary method for color conversion H - [0, 360), S,V - [0, 1]
	private vec3 hsv2rgb(float h, float s, float v)
	{
		float p, q, t, fract;

		h /= 60.0f;
		fract = h - MathLib.Floor(h);

		p = v * (1.0f - s);
		q = v * (1.0f - s * fract);
		t = v * (1.0f - s * (1.0f - fract));

		if (0.0f <= h && h < 1.0f) return new vec3(v, t, p);
		else if (1.0f <= h && h < 2.0f) return new vec3(q, v, p);
		else if (2.0f <= h && h < 3.0f) return new vec3(p, v, t);
		else if (3.0f <= h && h < 4.0f) return new vec3(p, q, v);
		else if (4.0f <= h && h < 5.0f) return new vec3(t, p, v);
		else if (5.0f <= h && h < 6.0f) return new vec3(v, p, q);
		else return new vec3(0, 0, 0);
	}
}

```

</details>


## Add Components to Nodes


As we implemented our game logic in the components, we can actually start using them. But first, we should create game objects. It is possible both via *[UnigineEditor](../../../../editor2/index.md)* and code.


### Creating a Scene via Editor


1. Create a [World](../../../../objects/lights/world/index.md) light source to illuminate the whole scene.
2. Add a [new camera](../../../../editor2/camera_settings/index.md#add_custom_camera) to the world and [adjust its position](../../../../editor2/navigation/index.md). This will be our default camera, so check on its [**Main Player**](../../../../objects/players/index.md#main_player) flag.
3. Create a [Box](../../../../editor2/create_import_nodes/index.md#box) primitive to represent *Pawn*. Assign the **Pawn** component by clicking **Add New Component or Property** and dragging the asset to the corresponding field. You can also drag the component from the Asset Browser to the node in the Editor Viewport. Adjust the parameters of the player. ![](assign.png)
4. Create another smaller box � a template for projectiles. We can disable it since its clones will be used.
5. Create the required number of objects for *Spinner*s at the same height as *Pawn*, assign the corresponding component to them and adjust the parameters. Specify the spawn node by dragging the *Projectile* node to the field. ![](projectile.png) On this step the scene looks as follows: ![](sample_scene.png)


### Creating a Scene via Code


All the same is available via API. We can describe logic to be executed on world loading (create game objects and assign components to them) in the *GameManager* component assigned to *Node Dummy*.


There are two ways to add a logic component to a node:


- By calling the corresponding method of the *[Node](../../../../api/library/nodes/class.node_cpp.md)* class: ```csharp object.AddComponent<MyComponent>(); ```
- By calling the corresponding method of the [Component System](../../../../api/library/common/logic/component_system/cs/class.componentsystem.md#addComponent_Node_T): ```csharp ComponentSystem.AddComponent<MyComponent>(object); ```


Here is the resulting code for our game including creation of entities and adding components to them:


<details>
<summary>GameManager.cs | Close</summary>

**GameManager.cs**


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;
#if UNIGINE_DOUBLE
using Vec3 = Unigine.dvec3;
using Vec4 = Unigine.dvec4;
using Mat4 = Unigine.dmat4;
#else
	using Vec3 = Unigine.vec3;
	using Vec4 = Unigine.vec4;
	using Mat4 = Unigine.mat4;
#endif
public partial class GameManager : Component
{
	 Pawn my_pawn;	// Pawn player
	float time = 0;
	WidgetLabel label;
	PlayerDummy player;
	LightWorld sun;

	// method creating a box
	ObjectMeshDynamic create_box(Mat4 transform, vec3 size)
	{
		Mesh mesh = new Mesh();
		mesh.AddBoxSurface("box", size);
		ObjectMeshDynamic obj = new ObjectMeshDynamic(1);
		obj.SetMesh(mesh);
		obj.WorldTransform = transform;
		obj.SetMaterial(Materials.FindManualMaterial("Unigine::mesh_base"), "*");

		return obj;
	}
	[Method(Order=0)]
	private void Init()
	{
		// create static camera
		player = new PlayerDummy();
		player.Position = new Vec3(17.0f);
		player.SetDirection(new vec3(-1.0f), new vec3(0.0f, 0.0f, 1.0f));
		player.Controlled = true;
		Game.Player = player;

		// create light
		sun = new LightWorld(vec4.ONE);
		sun.Name = "Sun";
		sun.SetWorldRotation(new quat(45.0f, 30.0f, 300.0f));

		// create objects
		ObjectMeshDynamic[] obj = new ObjectMeshDynamic[4];
		obj[0] = create_box(MathLib.Translate(new Vec3(-16.0f, 0.0f, 0.0f)), new vec3(1.0f));
		obj[1] = create_box(MathLib.Translate(new Vec3(16.0f, 0.0f, 0.0f)), new vec3(1.0f));
		obj[2] = create_box(MathLib.Translate(new Vec3(0.0f, -16.0f, 0.0f)), new vec3(1.0f));
		obj[3] = create_box(MathLib.Translate(new Vec3(0.0f, 16.0f, 0.0f)), new vec3(1.0f));

		// there are two ways to create components on nodes:
		ComponentSystem.AddComponent<Spinner>(obj[0]);
		ComponentSystem.AddComponent<Spinner>(obj[1]);
		obj[2].AddComponent<Spinner>();
		obj[3].AddComponent<Spinner>();

		// set up spinners (set "spawn_node" variable)
		ObjectMeshDynamic projectile_obj = create_box(Mat4.IDENTITY, new vec3(0.15f));
		projectile_obj.Enabled = false;
		for (int i = 0; i < 4; i++)
			obj[i].GetComponent<Spinner>().spawn_node = projectile_obj;

		// create player
		ObjectMeshDynamic my_pawn_object = create_box(MathLib.Translate(new Vec3(1.0f, 1.0f, 0.0f)), new vec3(1.3f, 1.3f, 0.3f));
		my_pawn = my_pawn_object.AddComponent<Pawn>();

		time = 0;

		// create info label
		label = new WidgetLabel(Gui.GetCurrent());
		label.SetPosition(10, 10);
		label.FontSize = 24;
		label.FontOutline = 1;
		Gui.GetCurrent().AddChild(label, Gui.ALIGN_OVERLAP);
	}

	private void Update()
	{
		// increase time while player is alive
			if (my_pawn != null)
				time += Game.IFps;
			// show game info
			label.Text =
				"Player:\n" +
				"Health Points: " +
				(my_pawn != null ? my_pawn.health : 0) + "\n" +
				"Time: " + time + " sec\n";
	}
}

```

</details>


Return to the Editor.


### Running the Project


Select a desired [play preset](../../../../principles/component_system/component_system_cs/index.md#run) on the toolbar and click the **Play** button to run an instance of the application.


![](run.png)


### Debugging Your C# Components


You can inspect the source code of your C# components while your application is running regardless of whether the application is launched via the **Play** button right in the UnigineEditor, or built and launched from an IDE.


See the [Debugging C# Components](../../../../code/csharp/debug_components.md) article for details.
