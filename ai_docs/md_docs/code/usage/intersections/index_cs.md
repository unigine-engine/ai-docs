# Intersections (CS)


Unigine has different methods to detect intersections. Intersection is a shared point of the defined area (or line) and an object. This article describes different types of intersections and their usage.


There are three main types of intersections:


- **World intersection** � an intersection with [objects](../../../api/library/objects/class.object_cs.md) and [nodes](../../../api/library/nodes/class.node_cs.md).
- **Physics intersection** � an intersection with [shapes](../../../api/library/physics/class.shape_cs.md) and [collision objects](../../../principles/physics/collision/index.md).
- **Game intersection** � an intersection with pathfinding nodes such as [obstacles](../../../api/library/pathfinding/class.obstacle_cs.md).


The *[Shape](../../../api/library/physics/class.shape_cs.md)* and *[Object](../../../api/library/objects/class.object_cs.md)* classes have their own *getIntersection()* functions. These functions are used to detect intersections with a specific shape or a specific surface of the object.


### See Also


- **[C# Component Samples](../../../sdk/api_samples/cs/scene_management.md)** demonstrating the use of World Intersection
- **[C++ Samples](../../../sdk/api_samples/cpp/scene_management.md)** demonstrating different cases of intersection detection


## World Intersection


By using different overloaded *[World](../../../api/library/engine/class.world_cs.md)* class *getIntersection()* functions you can find objects and nodes that intersect bounds of the specified bounding volume or identify the first intersection of the object with the invisible tracing line.


The *World* class functions for intersection search can be divided into 3 groups:


- [Functions to find nodes](#worldintersections_nodes) within a bounding volume
- [Functions to find objects](#worldintersections_objects) within a bounding volume or intersected with a traced line
- [Functions to find first intersected object](#worldintersections_object) with a traced line


> **Notice:** The following objects have individual parameters that control the accuracy of intersection detection:
>
>
> - *[ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cs.md#setIntersectionPrecision_float_void)*
> - *[ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_cs.md#intersections)*


### Intersection with Nodes


To find the intersection of nodes with bounds of the specified volume, you should use functions that have a bounding volume and a vector of nodes in arguments:


- *[bool GetIntersection(WorldBoundBox bb, ICollection<Node> nodes)](../../../api/library/engine/class.world_cs.md#getIntersection_WorldBoundBox_VECNode_int)*
- *[bool GetIntersection(WorldBoundSphere bs, ICollection<Node> nodes)](../../../api/library/engine/class.world_cs.md#getIntersection_WorldBoundSphere_VECNode_int)*
- *[bool GetIntersection(WorldBoundBox bb, int type, ICollection<Node> nodes)](../../../api/library/engine/class.world_cs.md#getIntersection_WorldBoundBox_int_VECNode_int)*
- *[bool GetIntersection(WorldBoundSphere bs, int type, ICollection<Node> nodes)](../../../api/library/engine/class.world_cs.md#getIntersection_WorldBoundSphere_int_VECNode_int)*
- *[bool GetIntersection(WorldBoundFrustum bf, int type, ICollection<Node> nodes)](../../../api/library/engine/class.world_cs.md#getIntersection_WorldBoundFrustum_int_VECNode_int)*


![](world_nodes.png)

*Schematic visual representation of intersection with nodes in bounding volume*


These functions return the value indicating the result of the intersection search: **true** if the intersection was found; otherwise, **false**. Intersected nodes can be found in the collection that passed as an argument to the function.


To clarify the nodes search, specify the type of node to search.


#### Usage Example


In the example below, the engine checks intersections with a bounding box and shows the names of intersected objects in the console.


In the *Init()* function the bounding box is defined.


The main logic is in the *Update()* method, the engine checks the intersection and shows the message about intersection.


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
using WorldBoundBox = Unigine.BoundBox;
#endif
#endregion

public partial class Intersections : Component
{

	// define a bounding box
	WorldBoundBox boundBox;

	// create a counter to show the message once
	int counter = 1;

	private void Init()
	{

		// initialize the bounding box
		boundBox = new WorldBoundBox(new Vec3(0.0f), new Vec3(10.0f));

	}

	private void Update()
	{

		// check the intersection with the bounding box
		List<Node> nodes = new List<Node>();
		bool result = World.GetIntersection(boundBox, nodes);
		if (result && counter !=0)
		{
			foreach(Node n in nodes)
			{
				// show the name of the intersected node in the console
				Log.Message("There was an intersection with: {0} \n", n.Name);
			}
			counter--;
		}

	}

}


```


### Intersection with Objects


The following functions can be used to perform the intersection search with objects:


- *[bool GetIntersection(Vec3 p0, Vec3 p1, ICollection<Object> objects, bool check_surface_flags)](../../../api/library/engine/class.world_cs.md#getIntersection_Vec3_Vec3_VECObject_int_int)*
- *[bool GetIntersection(WorldBoundBox bb, ICollection<Object> objects)](../../../api/library/engine/class.world_cs.md#getIntersection_WorldBoundBox_VECObject_int)*
- *[bool GetIntersection(WorldBoundSphere bs, ICollection<Object> objects)](../../../api/library/engine/class.world_cs.md#getIntersection_WorldBoundSphere_VECObject_int)*
- *[bool GetIntersection(WorldBoundFrustum bf, ICollection<Object> objects)](../../../api/library/engine/class.world_cs.md#getIntersection_WorldBoundFrustum_VECObject_int)*
- *[bool GetVisibleIntersection (vec3 camera, WorldBoundFrustum bf, Object[] objects, float max_distance)](../../../api/library/engine/class.world_cs.md#getVisibleIntersection_Vec3_WorldBoundFrustum_VECObject_float_int)*
- *[int GetVisibleIntersection( vec3 camera, WorldBoundFrustum bf, Node.TYPE type, Node[] nodes, float max_distance)](../../../api/library/engine/class.world_cs.md#getVisibleIntersection_Vec3_WorldBoundFrustum_int_VECNode_float_int)*


![](world_objects.png)

*Schematic visual representation of intersection with objects in bounding volume*


These functions return the value indicating the result of the intersection search: true if the intersection was found; otherwise, false. You can pass the start (**vec3 p0**) and the end (**vec3 p1**) point of the intersecting line or pass the (*BoundBox, BoundFrustum, BoundSphere*) to get the intersection of objects with a line or with a bounding volume, respectively. Intersected nodes can be found in the collection that passed as an argument to the function.


For *WorldBoundFrustum*, there are [two modes of getting intersections](#frustrum_search):


- Intersections with the objects that are **visible** inside the frustum � *[GetVisibleIntersection()](../../../api/library/engine/class.world_cs.md#getVisibleIntersection_Vec3_WorldBoundFrustum_VECObject_float_int)*
- Intersections with all objects inside the frustum, both **visible** and **invisible** � *[GetIntersection()](../../../api/library/engine/class.world_cs.md#getIntersection_WorldBoundFrustum_VECObject_int)*


#### Finding Objects Intersected by a Bounding Box


In the example below, the engine checks intersections with a bounding box and shows the message in the console.


In the *Init()* function the bounding box is defined.


The main logic is in the *Update()* method, the engine checks the intersection and shows the message about intersection.


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
using WorldBoundBox = Unigine.BoundBox;
#endif
#endregion

public partial class Intersections : Component
{

	// define a bounding box
	WorldBoundBox boundBox;

	// create a counter to show the message once
	int counter = 1;

	private void Init()
	{

		// initialize the bounding box
		boundBox = new WorldBoundBox(new Vec3(0.0f), new Vec3(10.0f));

	}

	private void Update()
	{

		// check the intersection with the bounding box
		List<Unigine.Object> objects = new List<Unigine.Object>();
		bool result = World.GetIntersection(boundBox, objects);
		if (result && counter != 0)
		{
			foreach (Unigine.Object o in objects)
			{
				Log.Message("There was an intersection with: {0} \n", o.Name);
			}
			counter--;
		}
	}

}


```


#### Finding Objects Intersected by a Bounding Frustum


For *[WorldBoundFrustum](../../../api/library/math/bounds/class.worldboundfrustum_cs.md)*, there are two modes of getting intersections:


- Intersections with the objects that are **visible** inside the frustum (within the rendering [visibility distance](../../../editor2/settings/render_settings/visibility_distances/index.md) and the object's [LOD](../../../principles/world_management/index.md#lods) is visible by the camera) � *[GetVisibleIntersection()](../../../api/library/engine/class.world_cs.md#getVisibleIntersection_Vec3_WorldBoundFrustum_VECObject_float_int)*
- Intersections with all objects inside the frustum, both **visible** and **invisible** (either occluded by something or out of the visibility distance) � *[GetIntersection()](../../../api/library/engine/class.world_cs.md#getIntersection_WorldBoundFrustum_VECObject_int)*


In the example below, the engine checks intersections of *WorldBoundFrustum* with all objects, both visible and invisible. The frustum itself is highlighted blue, and the objects that are inside the frustum are highlighted red for 20 seconds.


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
using WorldBoundBox = Unigine.BoundBox;
#endif
#endregion

public partial class Intersections : Component
{

	private void Init()
	{

		// enable the visualizer
		Visualizer.Enabled = true;

	}

	private void Update()
	{

		if(Input.IsKeyDown(Input.KEY.SPACE))
		{
			// get a reference to the camera
			Player player = Game.Player;
			Camera camera = player.Camera;

			// get the size of the current application window
			EngineWindow main_window = WindowManager.MainWindow;
			if (!main_window)
			{
				Engine.Quit();
				return;
			}

			ivec2 main_size = main_window.Size;

			mat4 projection = camera.GetAspectCorrectedProjection(((float)(main_size.y) / ((float)main_size.x)));

			// bound frustrum for the intersection and a list to store intersected objects
			var bf = new WorldBoundFrustum(camera.Projection, camera.Modelview);
			Visualizer.RenderFrustum(projection, camera.IModelview, vec4.BLUE, 20.0f);

			List<Unigine.Object> objects = new List<Unigine.Object>();

			// perform the intersection search with the bound frustrum
			World.GetIntersection(bf, objects);

			// draw the bound spheres of all objects' surfaces found by the search
			foreach(var obj in objects)
			{
				for (int i = 0; i < obj.NumSurfaces; ++i)
					{
						var bs = obj.GetBoundSphere(i);
						Visualizer.RenderBoundSphere(bs, obj.WorldTransform, vec4.RED, 20.0f);
					}
			}

		}

	}

}


```


To search only for intersections with the objects that are within the rendering [visibility distance](../../../editor2/settings/render_settings/visibility_distances/index.md) and the [LODs](../../../principles/world_management/index.md#lods) of which are visible, use the following method instead of *getIntersection()*:


```csharp
// perform the intersection search with the bound frustrum
World.GetVisibleIntersection(player.WorldPosition, bf, objects, 100.0f);


```


> **Notice:** The current rendering *[Distance Scale](../../../editor2/settings/render_settings/visibility_distances/index.md)* is also taken into account in the distance calculation.


### First Intersected Object


The following functions are used to find the nearest intersected object with the traced line. You should specify the start point and the end point of the line, and the function detects if there are any object on the way of this line.


- *[Object GetIntersection(Vec3 p0, Vec3 p1, int mask, Vec3[] ret_point, vec3[] ret_normal, vec4[] ret_texcoord, int[] ret_index, int[] ret_surface)](../../../api/library/engine/class.world_cs.md)*
- *[Object GetIntersection(Vec3 p0, Vec3 p1, int mask, Node[] exclude, Vec3[] ret_point, vec3[] ret_normal, vec4[] ret_texcoord, int[] ret_index, int[] ret_surface)](../../../api/library/engine/class.world_cs.md)*
- *[Object GetIntersection(Vec3 p0, Vec3 p1, int mask, WorldIntersection v)](../../../api/library/engine/class.world_cs.md)*
- *[Object GetIntersection(Vec3 p0, Vec3 p1, int mask, WorldIntersectionNormal v)](../../../api/library/engine/class.world_cs.md)*
- *[Object GetIntersection(Vec3 p0, Vec3 p1, int mask, WorldIntersectionTexCoord v)](../../../api/library/engine/class.world_cs.md)*
- *[Object GetIntersection(Vec3 p0, Vec3 p1, int mask, Node[] exclude, WorldIntersection v)](../../../api/library/engine/class.world_cs.md)*
- *[Object GetIntersection(Vec3 p0, Vec3 p1, int mask, Node[] exclude, WorldIntersectionNormal v)](../../../api/library/engine/class.world_cs.md)*
- *[Object GetIntersection(Vec3 p0, Vec3 p1, int mask, Node[] exclude, WorldIntersectionTexCoord v)](../../../api/library/engine/class.world_cs.md)*


![](worldintersection.png)

*Schematic visual representation of intersection with objects and traced line*


These functions return an intersection information and a pointer to the nearest object to the start point (**p0**). Information about the intersection can be presented in standard vectors or in the following format that you pass to functions as arguments:


- *WorldIntersection **intersection*** � the *[WorldIntersection](../../../api/library/worlds/class.worldintersection_cs.md)* class instance. By using this class you can get the intersection point (coordinates), the index of the intersected triangle of the object and the index of the intersected surface.
- *WorldIntersectionNormal **normal*** � the *[WorldIntersectionNormal](../../../api/library/worlds/class.worldintersectionnormal_cs.md)* class instance. By using this class you can get only the normal of the intersection point.
- *WorldIntersectionTexCoord **texcoord*** � the *[WorldIntersectionTexCoord](../../../api/library/worlds/class.worldintersectiontexcoord_cs.md)* class instance. By using this class you can get only the texture coordinates of the intersection point.


These functions detect intersection with surfaces (polygons) of meshes. But there are some conditions to detect the intersection with the surface:


1. The surface is enabled.
2. The surface has a material assigned.
3. Per-surface **Intersection** flag is enabled. > **Notice:** You can set this flag to the object's surface by using the *[Object.SetIntersection()](../../../api/library/objects/class.object_cs.md#setIntersection_int_int_void)* function.


To clarify the object search, perform the following:


- Use an *Intersection* mask. An intersection is found only if an object is matching the *Intersection* mask.
- Specify the list of objects (nodes) to exclude and pass to the function as an argument.


#### Usage Example


In the example below, the engine checks intersections with a raytraced line and shows the message in the console.


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

public partial class Intersections : Component
{

	// define world intersection instance
	WorldIntersection wi;

	// create a counter to show the message once
	int counter = 1;

	private void Init()
	{

		// initialize the world intersection
		wi = new WorldIntersection();

	}

	private void Update()
	{

		// check the intersection with the object
		Unigine.Object o = World.GetIntersection(new Vec3(0.0f), new Vec3(1.0f), 1, wi);
		if (o != null && counter != 0)
		{
			Log.Message("The name of the obstacle is: {0} \n", o.Name);
			counter--;
		}
	}

}


```


## Physics Intersection


Physics intersection function detects intersections with a physical shape or a *Fracture Body*. If the object has no body, this function detects intersection with surfaces (polygons) of the object having the *[Physics Intersection](../../../api/library/objects/class.object_cs.md#setPhysicsIntersection_int_int_void)* flag enabled. When you need to find the intersection with the shape of the object (not with polygons), the intersection function of *[Physics](../../../api/library/physics/class.physics_cs.md)* class is the best way to get it.


![](physics_shape.png)

*The picture above shows how theGetIntersection()function detects the shape that intersects with the line*


There are 4 functions to find physics intersections:


- *[Object GetIntersection(Vec3 p0, Vec3 p1, int mask, PhysicsIntersection intersection)](../../../api/library/physics/class.physics_cs.md#getIntersection_Vec3_Vec3_int_PhysicsIntersection_Object)*
- *[Object GetIntersection(Vec3 p0, Vec3 p1, int mask, PhysicsIntersectionNormal intersection)](../../../api/library/physics/class.physics_cs.md#getIntersection_Vec3_Vec3_int_PhysicsIntersectionNormal_Object)*
- *[Object GetIntersection(Vec3 p0, Vec3 p1, int mask, Node[] exclude, PhysicsIntersection intersection)](../../../api/library/physics/class.physics_cs.md#getIntersection_Vec3_Vec3_int_VECNode_PhysicsIntersection_Object)*
- *[Object GetIntersection(Vec3 p0, Vec3 p1, int mask, Node[] exclude, PhysicsIntersectionNormal intersection)](../../../api/library/physics/class.physics_cs.md#getIntersection_Vec3_Vec3_int_VECNode_PhysicsIntersectionNormal_Object)*


These functions perform tracing from the start *p0* point to the end *p1* point to find a collision object (or a shape) located on that line. Functions use world space coordinates.


Thus, to exclude some obstacles you should use these methods:


- Use a *Physics Intersection* mask. A physics intersection is detected only if the *Physics Intersection* mask of the surface/shape/body matches the *Intersection* mask passed as a function argument, otherwise it is ignored.
- Specify the list of objects to exclude and pass to the function as an argument.


### Usage Example


The following example shows how you can get the intersection information by using the *[PhysicsIntersection](../../../api/library/physics/class.physicsintersection_cs.md)* class. In this example we specify a line from the point of the camera *(vec3 p0)* to the point of the mouse pointer *(vec3 p1)*. The executing sequence is the following:


1. Define and initialize two points (p0 and p1) by using the *[Player.GetDirectionFromScreen()](../../../api/library/players/class.player_cs.md#getDirectionFromScreen_Vec3_Vec3_int_int_int_int_int_int_void)* function.
2. Create an instance of the *PhysicsIntersection* class to get the intersection information.
3. Check if there is an intersection with an object with a shape or a collision object. The *[GetIntersection()](../../../api/library/physics/class.physics_cs.md#getIntersection_Vec3_Vec3_int_Variable)* function returns an intersected object when the object intersects with the traced line.
4. When the object intersects with the traced line, all surfaces of the intersected object change their material parameters. If the object has a shape, its information will be shown in console. The *PhysicsIntersection* class instance gets the coordinates of the intersection point and the *[Shape](../../../api/library/physics/class.shape_cs.md)* class object. You can get all these fields by using *[Shape](../../../api/library/physics/class.physicsintersection_cs.md#getShape_Shape), [Point](../../../api/library/physics/class.physicsintersection_cs.md#getPoint_Vec3)* properties.


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

public partial class PhysicsIntersectionClass : Component
{
	private void Init()
	{
		// create a mesh instance with a box surface
		Mesh mesh = new Mesh();
		mesh.AddBoxSurface("box", new vec3(2.2f));

		// create a new dynamic mesh from the Mesh instance
		ObjectMeshDynamic dynamic_mesh = new ObjectMeshDynamic(mesh);

		dynamic_mesh.WorldTransform = MathLib.Translate(new Vec3(0.0f, 0.0f, 2.0f));

		// assign a body and a shape to the dynamic mesh
		BodyRigid body = new BodyRigid(dynamic_mesh);
		ShapeBox shape = new ShapeBox(body, new vec3(2.2f));
	}
	private void Update()
	{
		// initialize points of the mouse direction
		Vec3 p0, p1;

		// get the current player (camera)
		Player player = Game.Player;

		// get the size of the current application window
		EngineWindow main_window = WindowManager.MainWindow;
		if (!main_window)
		{
			Engine.Quit();
			return;
		}

		ivec2 main_size = main_window.Size;

		// get the current X and Y coordinates of the mouse pointer
		int mouse_x = Gui.GetCurrent().MouseX;
		int mouse_y = Gui.GetCurrent().MouseY;
		// get the mouse direction from the player's position (p0) to the mouse cursor pointer (p1)
		player.GetDirectionFromScreen(out p0, out p1, mouse_x, mouse_y, 0, 0, main_size.x, main_size.y);

		// create the instance of the PhysicsIntersection object to save the information about the intersection
		PhysicsIntersection intersection = new PhysicsIntersection();
		// get an intersection
		Unigine.Object obj = Physics.GetIntersection(p0, p1, 1, intersection);

		// if the intersection has occurred, change the parameter of the object's material
		if (obj != null)
		{
			for (int i = 0; i < obj.NumSurfaces; i++)
			{
				obj.SetMaterialParameterFloat4("albedo_color", new vec4(1.0f, 1.0f, 0.0f, 1.0f), i);
			}

			// if the intersected object has a shape, show the information about the intersection
			Shape shape = intersection.Shape;
			if (shape != null)
			{
				Log.Message("physics intersection info: point: ({0} {1} {2}) shape: {3}\n", intersection.Point.x, intersection.Point.y, intersection.Point.z, shape.TypeName);
			}
		}

	}
}

```


## Game Intersection


The *GetIntersection()* functions of the *Game* class are used to check the intersection with obstacles (pathfinding nodes):


- *[Obstacle GetIntersection(Vec3 p0, Vec3 p1, float radius, int mask, Node[] exclude, Vec3[] intersection)](../../../api/library/engine/class.game_cs.md#getIntersection_Vec3_Vec3_float_int_VECNode_Vec3_Obstacle)*
- *[Obstacle GetIntersection(Vec3 p0, Vec3 p1, float radius, int mask, GameIntersection intersection)](../../../api/library/engine/class.game_cs.md#getIntersection_Vec3_Vec3_float_int_GameIntersection_Obstacle)*


The engine creates an invisible cylinder with specified radius between two points and checks if an obstacle is inside it.


![](cylinder01.png)

*Schematic visual representation of intersection with objects and cylinder volume*


These functions return an intersection information and a pointer to the nearest obstacle to the start point (**p0**). Information about the intersection will be presented in the *[GameIntersection](../../../api/library/engine/class.gameintersection_cs.md)* class instance which you pass to the function as an argument or in the vector.


Use the mask and exclude arguments of the overloaded function to specify the obstacle search.


To clarify the obstacle search, perform the following:


- Use an obstacle *Intersection* mask. An intersection is found only if an object is matching the *Intersection* mask, otherwise it is ignored.
- Specify the list of obstacles to exclude and pass to the function as an argument.


### Usage Example


The following example shows how you can get the intersection point *(vec3)* of the cylinder between two points with an obstacle. We'll do the following:


1. Create an instance of the *ObstacleBox* class on the application initialization.
2. Define two points (p1 and p2) that specify the beginning and the end of the cylinder.
3. Create an instance of the *GameIntersection* class to get the intersection point coordinates.
4. Check if there is an intersection with an obstacle. The *Game::getIntersection()* function returns an intersected obstacle when the obstacle appears in the area of the cylinder.
5. When the *GameIntersection* instance intersects with an obstacle, you can get its name using the *getName()* function or any other details using the corresponding functions.


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

public partial class Intersections : Component
{

	// define an obstacle box and game intersection instance
	ObstacleBox obstacleBox;
	GameIntersection gi;

	// parameters of the virtual cylinder defining the volume
	// inside which to check for intersections
	float radius = 1.0f;		// radius of the cylinder
	vec3 p1 = new vec3(0, -3.0f, 3.0f);	// starting point of the ray
	vec3 p2 = new vec3(0, 3.0f, 3.0f);	// ending point of the ray

	private void Init()
	{

		// initialize the obstacle box and specify the name
		obstacleBox = new ObstacleBox(new vec3(1.0f));
		obstacleBox.Name = "main_obstacle";

		// initialize the game intersection object
		gi = new GameIntersection();

		// enable the visualizer
		Visualizer.Enabled = true;

	}

	private void Update()
	{

		// make the obstacle box move inside and outside the game intersection area
		Vec3 new_pos = new Vec3(0,0,2 + MathLib.Sin(Game.Time));
		obstacleBox.WorldPosition = new_pos;
		Visualizer.RenderPoint3D(new_pos, 0.15f, vec4.MAGENTA);

		// calculate the cylinder height (equals to the distance between the starting and ending points)
		Visualizer.RenderPoint3D(p1, 0.15f, vec4.BLUE);
		Visualizer.RenderPoint3D(p2, 0.15f, vec4.YELLOW);

		// create an instance of the GameIntersection class
		Obstacle obstacle = Game.GetIntersection(p1, p2, radius, 1, gi);

		//visualize the cylinder that represents the game intersection area
		Visualizer.RenderCylinder(radius, (p2-p1).Length, MathLib.SetTo(p1 + (p2 - p1) / 2, p2, vec3.UP, MathLib.AXIS.Z), vec4.WHITE);

		// check if the intersection of the cylinder with the obstacle has occurred
		if (obstacle != null)
		{
			obstacle.RenderVisualizer();
			Log.Message("The name of the obstacle is: {0} \n", obstacle.Name);
		}
	}

}


```
