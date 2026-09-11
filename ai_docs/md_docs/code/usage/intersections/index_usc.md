# Intersections (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


Unigine has different methods to detect intersections. Intersection is a shared point of the defined area (or line) and an object. This article describes different types of intersections and their usage.


There are three main types of intersections:


- **World intersection** � an intersection with [objects](../../../api/library/objects/class.object_usc.md) and [nodes](../../../api/library/nodes/class.node_usc.md).
- **Physics intersection** � an intersection with [shapes](../../../api/library/physics/class.shape_usc.md) and [collision objects](../../../principles/physics/collision/index.md).
- **Game intersection** � an intersection with pathfinding nodes such as [obstacles](../../../api/library/pathfinding/class.obstacle_usc.md).


The *[Shape](../../../api/library/physics/class.shape_usc.md)* and *[Object](../../../api/library/objects/class.object_usc.md)* classes have their own *getIntersection()* functions. These functions are used to detect intersections with a specific shape or a specific surface of the object.


### See Also


- **[C# Component Samples](../../../sdk/api_samples/cs/scene_management.md)** demonstrating the use of World Intersection
- **[C++ Samples](../../../sdk/api_samples/cpp/scene_management.md)** demonstrating different cases of intersection detection


## World Intersection


By using different overloaded *[World](../../../api/library/engine/class.world_usc.md)* class *getIntersection()* functions you can find objects and nodes that intersect bounds of the specified bounding volume or identify the first intersection of the object with the invisible tracing line.


The *World* class functions for intersection search can be divided into 3 groups:


- [Functions to find nodes](#worldintersections_nodes) within a bounding volume
- [Functions to find objects](#worldintersections_objects) within a bounding volume or intersected with a traced line
- [Functions to find first intersected object](#worldintersections_object) with a traced line


> **Notice:** The following objects have individual parameters that control the accuracy of intersection detection:
>
>
> - *[ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_usc.md#setIntersectionPrecision_float_void)*
> - *[ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_usc.md#intersections)*


### Intersection with Nodes


To find the intersection of nodes with bounds of the specified volume, you should use these 2 functions:


- *[engine.world.getIntersectionNodeVariables()](../../../api/library/engine/class.world_usc.md#getIntersectionNodeVariables_Variable_int_VECint_int)* to find all the nodes (or specified type nodes) that intersect bounds of the specified volume: *BoundBox, BoundFrustum, BoundSphere*. This function finds nodes which have set user variables.
- *[engine.world.getIntersectionNodes()](../../../api/library/engine/class.world_usc.md#getIntersectionNodes_Variable_int_VECint_int)* functions to find all the nodes (or nodes of specified type) in within a given bounding volume: *BoundBox, BoundFrustum, BoundSphere*.


![](world_nodes.png)

*The picture above shows how theengine.world.getIntersection()function detects the nodes that intersect with the bounds of theBoundBoxvolume*


These functions return the amount of found nodes as an integer value and save the data in the **ret[]** array which you can pass to the function as an argument.


#### Usage Example


The following example shows how you can get the intersection nodes by using the *engine.world.getIntersectionNodes()* function. It is supposed that you already have a world containing nodes and you have the *BoundBox* instance with the specified size. This code is taken from the world script's *update()* method. In this example the function checks if there is a node of any type inside the specified *BoundBox* object. The executing sequence is the following:


1. Define an array for output values and a *BoundBox* instance.
2. Check if there is an intersection with a node. The *engine.world.getIntersectionNodes()* function returns an integer value: the amount of found nodes.
3. When the node intersects with the *BoundBox*, console shows the information about that node. If there is no intersected node, console shows another message.


```cpp
/* ... */
// It is supposed that you have these variables in your code:
// a BoundBox instance
WorldBoundBox boundBox;
// Array for the result
int resultArray[0];

/* ... */
int update() {
	boundBox = new WorldBoundBox(dvec3(0.0f, 0.0f, 0.0f), dvec3(10.0f, 10.0f, 10.0f));
	/* ... */
	/* this part is from update() method */
	// check if there is any node inside the BoundBox
	int result = engine.world.getIntersectionNodes(boundBox, -1, resultArray);

	// if there is an intersection, do the following in a loop:
	if(result != 0)
	{
		// get the size of the array and perform a for loop
		forloop(int i=0; resultArray.size())
		{
			// get the Node from the array and show its name and type in console
			Node node = resultArray[i];
			log.message("node %i is : %s %i\n", i, node.getName(), node.getType() );
		}
	}
	else
	{
		log.message("sorry, but your intersection is in another castle!\n");
	}
	return 1;
}
/* ... */

```


### Intersection with Objects


#### Finding Objects Intersected by a Bounding Box


The *engine.world* class functions have 2 overloaded functions to get objects with and without user data. Intersection is performed with surfaces (polygons):


- *[engine.world.getIntersectionObjectVariables(variable v, int ret = [])](../../../api/library/engine/class.world_usc.md#getIntersectionObjectVariables_Variable_VECint_int)*
- *[engine.world.getIntersectionObjectVariables(vec3 p0, vec3 p1, int ret = [])](../../../api/library/engine/class.world_usc.md#getIntersectionObjectVariables_vec3_vec3_VECint_int)*
- *[engine.world.getIntersectionObjects(variable v, int ret = [])](../../../api/library/engine/class.world_usc.md#getIntersectionObjects_Variable_VECint_int)*
- *[engine.world.getIntersectionObjects(vec3 p0, vec3 p1, int ret = [])](../../../api/library/engine/class.world_usc.md#getIntersectionObjects_vec3_vec3_VECint_int)*


![](world_objects.png)

*The picture above shows how theengine.world.getIntersection()function detects the objects that intersect with the bounds of theBoundBoxvolume*


All these functions return the amount of found objects as an integer value and save the data in the **ret[]** array which you can pass to the function as an argument. You can pass the start (**vec3 p0**) and the end (**vec3 p1**) point of the intersecting line or pass the **variable v** (*BoundBox, BoundFrustum, BoundSphere*) to get the intersection of objects with a line or with a bounding volume, respectively.


###### Usage Example


The following example shows how you can get the intersected objects by using the *engine.world.getIntersectionObjects()* function. It is supposed that you already have a world containing objects. This code is taken from the world script's *update()* method. In this example we specify a line from the point of the camera (vec3 p0) to the point of the mouse pointer (vec3 p1). The executing sequence is the following:


1. Define an array for output values. Also define and initialize two points (p0 and p1) by using the *Unigine::getPlayerMouseDirection()* function from `core/scripts/utils.h`.
2. Check if there is an intersection with an object. The *engine.world.getIntersectionObjects()* function returns an integer value: the amount of found nodes.
3. When the object intersects with the traced line, console shows the information about that object.


```cpp
#include <core/scripts/utils.h>

/* ... */
// it is supposed that you have this variable in your code:
// array for the result
int resultArray[0];

/* ... */
int update() {
	// define two vec3 coordinates
	vec3 p0,p1;
	// get the mouse direction from camera (p0) to the cursor pointer (p1)
	Unigine::getPlayerMouseDirection(p0,p1);

	// check if there is any node inside the BoundBox
	int result = engine.world.getIntersectionObjects(p0, p1, resultArray);

	// if there is an intersection, do the following in a loop:
	if(result != 0)
	{
		// get the size of the array
		// perform a loop from 0 up to the size of the array
		// to show the information about all objects
		forloop(int i=0; resultArray.size())
		{
			// get the Object from the array and show its material name and type in console
			Object object = resultArray[i];
			log.message("object %i is : %s %i\n", i, object.getMaterialName(0), object.getType());
		}
	}
	return 1;
}
/* ... */

```


### First Intersected Object


The *[engine.world.getIntersection()](../../../api/library/engine/class.world_usc.md#getIntersection_vec3_vec3_int_Variable_Object)* function is used to find the nearest intersected object with the traced line. You should specify the start point and the end point of the line, and the function detects if there are any object on the way of this line.


![](worldintersection.png)

*The picture above shows how theengine.world.getIntersection()function detects the object that intersects with the line*


This function detects intersection with surfaces (polygons) of mesh and terrain objects. But there are some conditions to detect the intersection with the surface:


1. The surface is enabled.
2. The surface has a material assigned.
3. Per-surface **Intersection** flag is enabled. > **Notice:** You can set this flag to the object's surface by using the *[Object.setIntersection()](../../../api/library/objects/class.object_usc.md#setIntersection_int_int_void)* function.


The *engine.world.getIntersection()* function is overloaded and receives 4 or 5 arguments:


- **vec3 p0** � the start point coordinates of the trace line.
- **vec3 p1** � the end point coordinates of the trace line.
- **int mask** � the *Intersection* mask. Use the *Intersection* mask to find object only with the specified mask.
- **int exclude[]** � the list of objects IDs to exclude.
- **variable v** � The function returns an intersected object which is the nearest to the start point (*p0*). Information about the intersection will be presented in variable which you pass to the function as an argument: > **Notice:** Passing *NULL* instead of the intersection query object will perform fast intersection algorithm without the closest intersection point searching.

  - *WorldIntersection **intersection*** � the *[WorldIntersection](../../../api/library/worlds/class.worldintersection_usc.md)* class instance. By using this class you can get the intersection point (coordinates), the index of the intersected triangle of the object and the index of the intersected surface.
  - *WorldIntersectionNormal **normal*** � the *[WorldIntersectionNormal](../../../api/library/worlds/class.worldintersectionnormal_usc.md)* class instance. By using this class you can get only the normal of the intersection point.
  - *WorldIntersectionTexCoord **texcoord*** � the *[WorldIntersectionTexCoord](../../../api/library/worlds/class.worldintersectiontexcoord_usc.md)* class instance. By using this class you can get only the texture coordinates of the intersection point.


Thus, to exclude some objects you should use these methods:


- Use an *Intersection* mask. An intersection is found only if an object is matching the *Intersection* mask.
- Specify the list of objects IDs to exclude and pass to the function as an argument.


#### Usage Example


The following example shows how you can get the intersection information by using the *WorldIntersection* class. It is supposed that you already have a world containing objects. This code is taken from the world script's *update()* method. In this example we specify a line from the point of the camera *(vec3 p0)* to the point of the mouse pointer *(vec3 p1)*. The executing sequence is the following:


1. Define and initialize two points (p0 and p1) by using the *Unigine::getPlayerMouseDirection()* function from `core/scripts/utils.h`.
2. Create an instance of the *WorldIntersection* class to get the intersection information.
3. Check if there is an intersection with an object. The *engine.world.getIntersection()* function returns an intersected object when the object intersects with the traced line.
4. When the object intersects with the traced line, all the surfaces of the intersected object change their material parameters. The *WorldIntersection* class instance gets the coordinates of the intersection point, the index of the surface and the index of the intersected triangle. You can get all these fields by using *[getIndex()](../../../api/library/worlds/class.worldintersection_usc.md#getIndex_int), [getPoint()](../../../api/library/worlds/class.worldintersection_usc.md#getPoint_Vec3)* and *[getSurface()](../../../api/library/worlds/class.worldintersection_usc.md#getSurface_int)* functions


```cpp
#include <core/scripts/utils.h>
/* ... */
int update() {
	// define two vec3 coordinates
	vec3 p0,p1;
	// get the mouse direction from camera (p0) to the cursor pointer (p1)
	Unigine::getPlayerMouseDirection(p0,p1);

	// create an instance of the WorldIntersection class to get the result
	WorldIntersection intersection = new WorldIntersection();

	// create an instance for intersected object
	Object object = engine.world.getIntersection(p0,p1,1,intersection);

	// if the intersection has occurred, change the parameter and the texture of the object's material
	if(object != NULL)
	{
	  forloop(int i=0; object.getNumSurfaces())
	  {
	    object.setMaterialParameterFloat4("diffuse_color", vec4(1.0f, 0.0f, 0.0f, 1.0f),i);
	    object.setMaterialTexture("diffuse","", i);

	    // show intersection details in console
	    log.message("point: %s index: %i surface: %i \n", typeinfo(intersection.getPoint()), intersection.getIndex(), intersection.getSurface());
	  }
	}
	return 1;
}
/* ... */

```


## Physics Intersection


Physics intersection function detects intersections with a physical shape or a *Fracture Body*. If the object has no body, this function detects intersection with surfaces (polygons) of the object having the *[Physics Intersection](../../../api/library/objects/class.object_usc.md#setPhysicsIntersection_int_int_void)* flag enabled. When you need to find the intersection with the shape of the object (not with polygons), *[engine.physics](../../../api/library/physics/class.physics_usc.md)* intersection function is the best way to get it.


![](physics_shape.png)

*The picture above shows how theengine.physics.getIntersection()function detects the shape that intersects with the line*


There are 2 *engine.physics* functions to find physics intersections:


- *[engine.physics.getIntersection (vec3 p0, vec3 p1, int mask, variable v)](../../../api/library/physics/class.physics_usc.md#getIntersection_Vec3_Vec3_int_int_Variable)*
- *[engine.physics.getIntersection (vec3 p0, vec3 p1, int mask, int exclude[] = [], variable v)](../../../api/library/physics/class.physics_usc.md#getIntersection_Vec3_Vec3_int_Variable)*


These functions perform tracing from the start *p0* point to the end *p1* point to find a collision object (or a shape) located on that line. Functions use world space coordinates.


The *engine.physics.getIntersection()* function is overloaded and receives 4 or 5 arguments:


- ***vec3 p0*** � the start point coordinates of the trace line.
- ***vec3 p1*** � the end point coordinates of the trace line.
- ***int mask*** � the *Intersection* mask. Use the *Intersection* mask to find object only with the specified mask.
- ***int exclude[]*** � the list of objects IDs to exclude, all these objects will be ignored.
- ***variable v*** � The function returns an intersected object which is the nearest to the start point (p0). Information about the intersection will be presented in variable which you pass to the function as an argument: > **Notice:** Passing *NULL* instead of the intersection query object will perform fast intersection algorithm without the closest intersection point searching.

  - *PhysicsIntersection **intersection*** � the *[PhysicsIntersection](../../../api/library/physics/class.physicsintersection_usc.md)* class instance. By using this class you can get the intersection point (coordinates), the index of the intersected surface and the intersection Shape.
  - *PhysicsIntersectionNormal **normal*** � the *[PhysicsIntersectionNormal](../../../api/library/physics/class.physicsintersectionnormal_usc.md)* class instance. By using this class you can get only the normal of the intersection point.


Thus, to exclude some obstacles you should use these methods:


- Use a *Physics Intersection* mask. A physics intersection is detected only if the *Physics Intersection* mask of the surface/shape/body matches the *Intersection* mask passed as a function argument, otherwise it is ignored.
- Specify the list of objects to exclude and pass to the function as an argument.


### Usage Example


The following example shows how you can get the intersection information by using the *[PhysicsIntersection](../../../api/library/physics/class.physicsintersection_usc.md)* class. In this example we specify a line from the point of the camera *(vec3 p0)* to the point of the mouse pointer *(vec3 p1)*. The executing sequence is the following:


1. Define and initialize two points (p0 and p1) by using the *Unigine::getPlayerMouseDirection()* function from `core/scripts/utils.h`.
2. Create an instance of the PhysicsIntersection class to get the intersection information.
3. Check if there is an intersection with an object with a shape or a collision object. The *[engine.physics.getIntersection()](../../../api/library/physics/class.physics_usc.md#getIntersection_Vec3_Vec3_int_Variable)* function returns an intersected object when the object intersects with the traced line.
4. When the object intersects with the traced line, all the surfaces of the intersected object change their material parameters. If the object has a shape, its information will be shown in console. The *PhysicsIntersection* class instance gets the coordinates of the intersection point, the index of the surface and the *[Shape](../../../api/library/physics/class.shape_usc.md)* class object. You can get all these fields by using *[getShape()](../../../api/library/physics/class.physicsintersection_usc.md#getShape_Shape), [getPoint()](../../../api/library/physics/class.physicsintersection_usc.md#getPoint_Vec3)* and *[getSurface()](../../../api/library/physics/class.physicsintersection_usc.md#getSurface_int)* functions


```cpp
#include <core/scripts/utils.h>
/* ... */
int update {
	// define two vec3 coordinates
	vec3 p0,p1;
	// get the mouse direction from camera (p0) to the cursor pointer (p1)
	Unigine::getPlayerMouseDirection(p0,p1);

	// create the instance of the PhysicsIntersection object to save the result
	PhysicsIntersection intersection = new PhysicsIntersection();
	// create an instance for intersected object and check the intersection
	Object object = engine.physics.getIntersection(p0,p1,1,intersection);

	// if the intersection has occurred, change the parameter of the object's material
	if(object != NULL)
	{
		forloop(int i=0; object.getNumSurfaces())
		{
			object.setMaterialParameterFloat4("albedo_color", vec4(1.0f, 0.0f, 0.0f, 1.0f),i);
		}

		// if the intersected object has a shape, show the information about the intersection
		Shape shape = intersection.getShape();
		if (shape != NULL)
		{
			log.message("physics intersection info: point: %s shape: %s surface: %i \n", typeinfo(intersection.getPoint()), typeinfo(shape.getType()), intersection.getSurface());
		}
	}
	return 1;
}
/* ... */

```


## Game Intersection


You can check the intersection with obstacles by using the *[engine.game.getIntersection()](../../../api/library/engine/class.game_usc.md#getIntersection_Vec3_Vec3_float_int_GameIntersection_Obstacle)* function. This function creates an invisible cylinder between two points and check if an obstacle is presented inside of it.


![](cylinder01.png)

*The picture above shows how theengine.game.getIntersection()function detects the obstacle that intersects with the cylinder*


- *[Ptr<Obstacle> getIntersection(const Math::Vec3 & p0, const Math::Vec3 & p1, float radius, int mask, const Vector< Ptr<Node> > & exclude, Math::Vec3 * intersection)](../../../api/library/engine/class.game_usc.md#getIntersection_Vec3_Vec3_float_int_VECNode_Vec3_Obstacle)*
- *[Ptr<Obstacle> getIntersection(const Math::Vec3 & p0, const Math::Vec3 & p1, float radius, int mask, const Ptr<GameIntersection> & intersection)](../../../api/library/engine/class.game_usc.md#getIntersection_Vec3_Vec3_float_int_GameIntersection_Obstacle)*


The function returns an intersected obstacle which is the nearest to the start point *(p0)*. Information about the intersection will be presented in the *[GameIntersection](../../../api/library/engine/class.gameintersection_usc.md)* class instance which you pass to the function as an argument. The *GameIntersection* class instance saves the intersection point which is the nearest to the start *(p0)* point.


The *engine.game.getIntersection()* function is overloaded and receives 5 or 6 arguments:


- ***vec3 p0*** � the start point coordinates.
- ***vec3 p1*** � the end point coordinates.
- ***float radius*** � the end point coordinates.
- ***int mask*** � the obstacle *Intersection* mask. Use the *Intersection* mask to find object only with the specified mask.
- ***int exclude[]*** � the list of obstacles to exclude.
- ***GameIntersection intersection*** � The function returns an intersected obstacle which is the nearest to the start point *(p0)*. Information about the intersection will be presented in the *GameIntersection* class instance which you pass to the function as an argument. > **Notice:** Passing *NULL* instead of the intersection query object will perform fast intersection algorithm without the closest intersection point searching.


Thus, to exclude some obstacles you should use these methods:


- Use an obstacle *Intersection* mask. An intersection is found only if an object is matching the *Intersection* mask, otherwise it is ignored.
- Specify the list of obstacles to exclude and pass to the function as an argument.


### Usage Example


The following example shows how you can get the intersection point *(vec3)* of the cylinder between two points with an obstacle. In this example we specify a cylinder from the point of the camera *(vec3 p0)* to the point of the mouse pointer *(vec3 p1)* with the specified radius. The executing sequence is the following:


1. Define and initialize two points (p0 and p1) by using the *Unigine::getPlayerMouseDirection()* function from `core/scripts/utils.h`.
2. Create an instance of the *GameIntersection* class to get the intersection point coordinates.
3. Check if there is an intersection with an obstacle. The *engine.game.getIntersection()* function returns an intersected obstacle when the obstacle appears in the area of the cylinder.
4. After that *GameIntersection* instance gets the point of the nearest intersection point and you can get it by using the *getPoint()* function.


```cpp
#include <core/scripts/utils.h>

/* ... */
int update {
	/* ... */
	// define two vec3 coordinates
	vec3 p0,p1;
	// get the mouse direction from camera (p0) to the cursor pointer (p1)
	Unigine::getPlayerMouseDirection(p0,p1);

	// create an instance of the GameIntersection class
	GameIntersection intersection = new GameIntersection();

	// try to get the intersection with an obstacle.
	// cylinder has radius 0.1f, intersection mask equals to 1
	Obstacle obstacle = engine.game.getIntersection(p0,p1,0.1f, 1, intersection);

	// check if the intersection of mouse direction with any obstacle has occurred;
	if(obstacle !=NULL)
	{
		// show the coordinates of the intersection in console
		log.message("The intersection with obstacle was here: %s\n", typeinfo(intersection.getPoint()));
	}
	return 1;
}
/* ... */

```
