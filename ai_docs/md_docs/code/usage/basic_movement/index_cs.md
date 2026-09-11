# Moving Objects (CS)


Every node you place in UNIGINE is defined by its position, rotation, and scale. For static objects, these properties are usually configured directly in the Editor. To move objects during runtime, you must update their transform properties dynamically through code.


This can be simple teleportation, smooth continuous motion, keyboard-driven control, or physics-based movement - the right choice depends on what you are building. In this article we will work through each of these, starting from the simplest approach and building up to the most capable one.


The **How-To: Move Objects** video, which this article is based on:


### See Also


- Article on [Matrix Transformations](../../../code/fundamentals/matrix_transformations/index_cs.md)
- The [Node](../../../api/library/nodes/class.node_cs.md) class API reference
- Article on [Physical Bodies](../../../principles/physics/bodies/index.md)


## Coordinate System


To move an object in a direction, you first need to know how directions are defined. UNIGINE uses a **right-handed Cartesian system** with three axes, and every movement example below refers to them:


- The **+Z axis** points **up**
- The **+Y axis** points **forward**
- The **+X axis** points **right**


Because these directions come up constantly, the vector type provides named constants for them, which the C# examples below use in place of raw numbers like (0, 1, 0):


| Constant | Vector | Direction |
|---|---|---|
| *Vec3.FORWARD* | (0, 1, 0) | forward (+Y) |
| *Vec3.BACK* | (0, -1, 0) | back (-Y) |
| *Vec3.RIGHT* | (1, 0, 0) | right (+X) |
| *Vec3.LEFT* | (-1, 0, 0) | left (-X) |
| *Vec3.UP* | (0, 0, 1) | up (+Z) |
| *Vec3.DOWN* | (0, 0, -1) | down (-Z) |


### Importing Models


When importing models, keep in mind that different 3D applications use different coordinate systems. The forward direction of your mesh depends on how it was exported.


| ![](direction_maya.png) | ![](direction_unigine.png) |
|---|---|
| *A mesh in Maya* | *The same mesh in UNIGINE* |


In the images above, the model was exported with positive Y as the forward direction. If your model has a different orientation (e.g., +X as forward), you can correct this by re-importing the model with the appropriate orientation settings.


It is recommended that content creators and programmers agree on a consistent forward direction for all assets in the project.


## Direct Position Setting


> **Notice:** To be moved at runtime, a node must have its *Mobility* set to *Dynamic*.
>
>  ![](dynamic_mobility.png)


The simplest way to move a node is to set its position directly: assign a new value and the node appears there at once, with no motion in between. Every node has two position properties we can write to:


- **Position** - coordinates relative to the parent node
- **WorldPosition** - absolute world coordinates, independent of the parent hierarchy


```csharp
// Move the node to a point in space
node.WorldPosition = new Vec3(10.0f, 20.0f, 5.0f);

```

    Sorry, your browser does not support embedded videos.
*Assigning a position moves the object instantly - it appears at the new spot with no travel in between.*


The two properties differ only when the node has a parent. With no parent, they return the same value. But once the node is a child of another node, *[Position](../../../api/library/nodes/class.node_cs.md#getPosition_Vec3)* is measured relative to that parent, while *[WorldPosition](../../../api/library/nodes/class.node_cs.md#getWorldPosition_Vec3)* always stays in world space.


> **Notice:** "Local" here means **relative to the parent** - not relative to the node's own orientation. Those are two different ideas; the orientation-based one belongs to *[Translate()](../../../api/library/nodes/class.node_cs.md#translate_Vec3_void)*, covered below.

   Sorry, your browser does not support embedded videos.
*The robot has a parent (the flag). Setting itsPositionplaces it relative to that parent, so it follows the flag rather than landing at fixed world coordinates.*


- The C# Component sample contrasts local and world transformations side by side.


## Translate Methods


Instead of computing new positions by hand, the *[Node](../../../api/library/nodes/class.node_cs.md)* class gives us two helper methods that move a node by an offset:


- **Translate()** - moves the node along its own axes, in the direction it is facing
- **WorldTranslate()** - moves the node along the world axes, ignoring its orientation


What sets them apart is whether the node's **orientation** is taken into account - not the parent hierarchy. Both end up changing the world position, as the clip below shows:

   Sorry, your browser does not support embedded videos.
*First the robot moves along the world Y axis (green) withWorldTranslate(), then along its own forward axis withTranslate(). Either way the parent flag makes no difference - the distinction is the robot's orientation, not the hierarchy.*


### WorldTranslate


*[WorldTranslate()](../../../api/library/nodes/class.node_cs.md#worldTranslate_Vec3_void)* moves a node along the world axes, regardless of its orientation. Here we move it 1 unit along world Y:


```csharp
// Move 1 unit along world Y axis
node.WorldTranslate(new Vec3(0.0f, 1.0f, 0.0f));

```


### Translate


*[Translate()](../../../api/library/nodes/class.node_cs.md#translate_Vec3_void)*, on the other hand, uses the node's own local coordinate system. The vector we pass is read in local space, so *[Translate()](../../../api/library/nodes/class.node_cs.md#translate_Vec3_void)* already accounts for the node's orientation - we do not rotate the vector ourselves. Passing the local forward axis (0, 1, 0) moves the node forward, whichever way it faces:


```csharp
// Move 1 unit forward along the node's local +Y axis
node.Translate(Vec3.FORWARD);

```


- The C# Component sample compares *Translate()*, *Position*, and *Transform* and shows they reach the same result.


## Per-Frame Movement


So far each call moves the node by a set amount. But to keep an object moving - say, forward while a key is held - we call *[Translate()](../../../api/library/nodes/class.node_cs.md#translate_Vec3_void)* on **every frame**, and a problem appears: a fast computer draws more frames per second than a slow one, so a fixed step per frame would travel faster on better hardware.

   Sorry, your browser does not support embedded videos.
*Without frame-rate scaling, the same per-frame step travels faster at 144 FPS than at 60 FPS - the object's speed depends on the hardware.*


To avoid that, we scale each step by how long the frame took. **[Game.IFps](../../../api/library/engine/class.game_cs.md#IFps)* (Inverse Frames Per Second)* gives the time since the last frame, in seconds; multiplying by it turns a per-frame step into a per-second speed, so movement stays consistent regardless of frame rate. Here speed is in units per second - this is the pattern we use throughout the rest of the article:


```csharp
float ifps = Game.IFps;
// move at "speed" units per second, not per frame
node.Translate(Vec3.FORWARD * speed * ifps);

```


## Smooth Movement


The methods so far move the node in fixed steps that we choose. That is fine for input or teleports, but a camera or a pickup should settle onto a target on its own rather than advance in equal jumps. This time, instead of jumping to a fixed point, let's move the node **toward a target**, computing each step from how far it still has to go. UNIGINE's *MathLib* has several functions for this; we will use the two most common ones, *MoveTowards()* and *Lerp()*, which give the motion a noticeably different feel.


### MoveTowards


Often we want an object to approach a target at a **constant speed** and stop cleanly without overshooting. In C#, *MoveTowards()* does exactly this: it advances a value toward a target by at most a given step. C++ has no built-in equivalent, but we get the same result in a few lines - step toward the target by step, and snap to it once we are within one step. In both examples, speed is in units per second:


```csharp
// Move toward target position at constant speed
Vec3 currentPos = node.WorldPosition;
Vec3 targetPos = new Vec3(10.0f, 20.0f, 0.0f);
float step = speed * Game.IFps;

Vec3 newPos = MathLib.MoveTowards(currentPos, targetPos, step);
node.WorldPosition = newPos;

```


Wrapped as a ready-to-use component, **MoveTowardsMover** drives the node toward a target node at a constant speed and stops when it arrives. We just assign the target node to the *Target* field in the Editor:


In the clip below we pick the target interactively instead: a click casts a ray into the scene, drops a marker where it hits, and the object moves to that marker (it also turns to face it with *[WorldLookAt()](../../../api/library/nodes/class.node_cs.md#worldLookAt_Vec3_void)*, covered under [Rotation](#rotation)).

   Sorry, your browser does not support embedded videos.
*Clicking in the scene drops a target marker, and the object travels to it at a steady, constant speed - watch the pace stay even all the way until it stops.*


> **Notice:** The C# components below open with a small math setup block. It defines *Vec3* as an alias for the project's coordinate type - *vec3* in float precision or *dvec3* in double precision - so the same component works either way.


<details>
<summary>MoveTowardsMover.cs | Close</summary>

```csharp
using Unigine;

#if UNIGINE_DOUBLE
using Vec3 = Unigine.dvec3;
#else
using Vec3 = Unigine.vec3;
#endif

public partial class MoveTowardsMover : Component
{
	// node to move toward
	public Node target;
	// movement speed, in units per second
	public float speed = 5.0f;

	void Update()
	{
		if (target == null)
			return;

		Vec3 currentPos = node.WorldPosition;
		Vec3 targetPos = target.WorldPosition;
		float step = speed * Game.IFps;

		node.WorldPosition = MathLib.MoveTowards(currentPos, targetPos, step);
	}
}

```

</details>


### Lerp


If we replace *MoveTowards()* with *Lerp()*, the motion becomes smoother: it starts fast and softly slows down as it arrives, the natural way a camera settles onto its target. We get this by calling *Lerp()* **every frame** toward the target with a small factor t - each frame the node covers a fraction of the distance that remains, so its step shrinks as it gets closer.


A note on the name: *Lerp()* (linear interpolation) itself is not eased - a single call just returns a point a fraction t of the way from a to b (a + (b - a) * t). The slowdown comes from repeating it toward a fixed target each frame, not from the function.


```csharp
// Call every frame to ease toward the target
Vec3 currentPos = node.WorldPosition;
Vec3 targetPos = new Vec3(10.0f, 20.0f, 0.0f);
float t = 0.1f; // interpolation factor (0 to 1)

Vec3 newPos = MathLib.Lerp(currentPos, targetPos, t);
node.WorldPosition = newPos;

```


Wrapped as a component, **LerpMover** eases the node toward a target node every frame. The *Smoothness* field is the per-frame interpolation factor: smaller values give slower, softer motion. As before, we assign the target node to the *Target* field in the Editor:

   Sorry, your browser does not support embedded videos.
*The same click-to-move setup, now with Lerp: the object starts fast and visibly slows down as it nears the marker - compare this eased finish with the even pace ofMoveTowards()above.*


<details>
<summary>LerpMover.cs | Close</summary>

```csharp
using Unigine;

#if UNIGINE_DOUBLE
using Vec3 = Unigine.dvec3;
#else
using Vec3 = Unigine.vec3;
#endif

public partial class LerpMover : Component
{
	// node to ease toward
	public Node target;
	// per-frame interpolation factor (0 to 1)
	public float smoothness = 0.1f;

	void Update()
	{
		if (target == null)
			return;

		Vec3 currentPos = node.WorldPosition;
		Vec3 targetPos = target.WorldPosition;

		node.WorldPosition = MathLib.Lerp(currentPos, targetPos, smoothness);
	}
}

```

</details>


Which to use? Reach for *MoveTowards()* when you want a predictable, **constant speed** and a clean stop - good for an object travelling to a waypoint. Reach for *Lerp()* when you want a soft, **eased** finish - good for a camera or UI element that should glide into place.


### Putting It Together: Click to Move


The clips above come from a single component that ties these pieces together: it casts a ray from the camera through the mouse cursor, drops a marker where the ray hits the scene, then turns the node toward that point with *[WorldLookAt()](../../../api/library/nodes/class.node_cs.md#worldLookAt_Vec3_void)* and advances it with *MoveTowards()*. Swap that one call for *Lerp()* to get the eased variant.


<details>
<summary>MoveToPoint.cs | Close</summary>

```csharp
using Unigine;

#if UNIGINE_DOUBLE
using Vec3 = Unigine.dvec3;
#else
using Vec3 = Unigine.vec3;
#endif

public partial class MoveToPoint : Component
{
	// marker node showing where the ray hit
	public Node laser;
	// movement speed, in units per second
	public float speed = 5.0f;

	private WorldIntersection intersection = new WorldIntersection();

	void Init()
	{
		// let the cursor move freely so we can click anywhere
		Input.MouseHandle = Input.MOUSE_HANDLE.SOFT;
	}

	void Update()
	{
		if (Input.IsMouseButtonPressed(Input.MOUSE_BUTTON.LEFT))
		{
			// cast a ray from the camera through the mouse cursor
			ivec2 mouse = Input.MousePosition;
			Vec3 p0 = Game.Player.WorldPosition;
			Vec3 p1 = p0 + new Vec3(Game.Player.GetDirectionFromMainWindow(mouse.x, mouse.y)) * 50.0f;
			World.GetIntersection(p0, p1, 1, intersection);

			// place the marker at the hit point
			laser.WorldPosition = intersection.Point;
		}

		// face the marker and move toward it
		Vec3 target = laser.WorldPosition;
		node.WorldLookAt(target);
		node.WorldPosition = MathLib.MoveTowards(node.WorldPosition, target, speed * Game.IFps);
	}
}

```

</details>


- The C# Component sample shows the raycast-from-cursor part on its own, using *World.GetIntersection()*.


- For movement along a predefined path, see the C# Component sample (linear and spline interpolation).


## Rotation


Rotation mirrors translation: *[Rotate()](../../../api/library/nodes/class.node_cs.md#rotate_float_float_float_void)* spins the node in its own local space, while *[WorldRotate()](../../../api/library/nodes/class.node_cs.md#worldRotate_float_float_float_void)* spins it around the world axes. Both take Euler angles in degrees.


The three angles passed to *[Rotate()](../../../api/library/nodes/class.node_cs.md#rotate_float_float_float_void)* map directly to the axes: (X, Y, Z). With UNIGINE's axes (+X right, +Y forward, +Z up) this corresponds to **pitch** (tilt up and down, around X), **roll** (bank sideways, around Y), and **yaw** (turn left and right, around Z). So to turn an object left or right, we change the third angle, as below:


```csharp
// Rotate around Z axis (yaw) by angle per frame
float turnSpeed = 90.0f; // degrees per second
node.Rotate(0.0f, 0.0f, turnSpeed * Game.IFps);

```


When we just need a node to face something, there is no need to work out the angles ourselves: *[WorldLookAt()](../../../api/library/nodes/class.node_cs.md#worldLookAt_Vec3_void)* aims the node's forward axis (+Y) at a target position and fills in the rest of the orientation, keeping the node upright (its up axis stays aligned with world up). The turn is applied instantly, in a single frame. The click-to-move examples above use exactly this to keep the object facing the point it travels toward. To turn smoothly instead of snapping, interpolate the rotation toward the target with *Slerp()* each frame - the same idea as *Lerp()*, but for orientations.


```csharp
// Rotate to face the target
node.WorldLookAt(targetPos);

```


## Keyboard Control


Let's put this together into one of the most common patterns in games: free-form movement driven by the keyboard. The result is a [component](../../../principles/component_system/index.md) - a reusable script we attach to a node in the Editor - whose logic runs every frame, reads the keyboard, and moves the node it is attached to. We expose *moveSpeed* and *turnSpeed* as public parameters so they can be tuned in the Editor; the arrow keys or WASD drive the node:


<details>
<summary>SimpleMovement.cs | Close</summary>

```csharp
using Unigine;

#if UNIGINE_DOUBLE
using Vec3 = Unigine.dvec3;
#else
using Vec3 = Unigine.vec3;
#endif

public partial class SimpleMovement : Component
{
	// movement speed, in units per second
	public float moveSpeed = 5.0f;
	// rotation speed, in degrees per second
	public float turnSpeed = 90.0f;

	void Update()
	{
		float ifps = Game.IFps;

		// forward/backward movement along the node's local axis
		if (Input.IsKeyPressed(Input.KEY.W) || Input.IsKeyPressed(Input.KEY.UP))
			node.Translate(Vec3.FORWARD * moveSpeed * ifps);
		if (Input.IsKeyPressed(Input.KEY.S) || Input.IsKeyPressed(Input.KEY.DOWN))
			node.Translate(-Vec3.FORWARD * moveSpeed * ifps);

		// left/right rotation (yaw around the up axis)
		if (Input.IsKeyPressed(Input.KEY.A) || Input.IsKeyPressed(Input.KEY.LEFT))
			node.Rotate(0.0f, 0.0f, turnSpeed * ifps);
		if (Input.IsKeyPressed(Input.KEY.D) || Input.IsKeyPressed(Input.KEY.RIGHT))
			node.Rotate(0.0f, 0.0f, -turnSpeed * ifps);
	}
}

```

</details>

    Sorry, your browser does not support embedded videos.
*WASD moves the object forward and back and turns it left and right. Note that it passes straight through the wall - direct transform changes do not collide with anything.*


Under the hood this is still teleportation - we update the transform directly. The difference is that the updates happen in very small steps, many times per second, which reads as smooth, continuous motion.


> **Notice:** Because the transform is set directly, the node ignores obstacles and passes straight through them. For collision-aware movement, use physics instead.


- The C# Component sample covers reading keyboard and mouse input.


## Physics-Based Movement


To make movement respect collisions, we drive the object through the physics system instead of changing its transform directly. The idea is the same as before, only now the object is moved by forces. This needs a *Rigid Body* assigned to the node (a *BodyRigid* object in code), together with a collision shape.


### Physics Setup


Before using physics-based movement:


1. Set the node's *Mobility* to *Dynamic*
2. Add a *Rigid Body* in the Physics tab ![](add_rigid_body.png)
3. Add a *Shape* (e.g., Capsule, Box, or Sphere) for collision detection ![](add_physics_shape.png)
4. Configure [collision masks](../../../principles/physics/collision/index.md) on the surfaces you want to collide with


### Forces and Torques


We push the body with *[AddForce()](../../../api/library/physics/class.bodyrigid_cs.md#addForce_vec3_void)* and rotate it with *[AddTorque()](../../../api/library/physics/class.bodyrigid_cs.md#addTorque_vec3_void)*, and we call them in *UpdatePhysics()* rather than *Update()* so that physics handles the result.


To push the body in the direction it currently faces, we need that direction in world space - and it changes as the object turns. *[GetWorldDirection()](../../../api/library/nodes/class.node_cs.md#getWorldDirection_int_vec3)* gives it to us: we pass an axis and it returns that axis rotated by the node's current orientation. The component below takes the node's forward (*AXIS_Y*) for movement and its up (*AXIS_Z*) for turning:


<details>
<summary>PhysicsMovement.cs | Close</summary>

```csharp
using Unigine;

public partial class PhysicsMovement : Component
{
	// continuous force and torque while a key is held
	public float moveForce = 10.0f;
	public float turnTorque = 5.0f;
	// instant upward impulse on jump
	public float jumpImpulse = 5.0f;

	private BodyRigid body;
	private float moveInput = 0.0f;
	private float turnInput = 0.0f;
	private bool jumpRequested = false;

	void Init()
	{
		body = node.ObjectBodyRigid;
	}

	void Update()
	{
		// read input every frame, apply it in UpdatePhysics()
		moveInput = 0.0f;
		turnInput = 0.0f;

		if (Input.IsKeyPressed(Input.KEY.W)) moveInput = 1.0f;
		if (Input.IsKeyPressed(Input.KEY.S)) moveInput = -1.0f;
		if (Input.IsKeyPressed(Input.KEY.A)) turnInput = 1.0f;
		if (Input.IsKeyPressed(Input.KEY.D)) turnInput = -1.0f;
		if (Input.IsKeyDown(Input.KEY.SPACE)) jumpRequested = true;
	}

	void UpdatePhysics()
	{
		if (body == null)
			return;

		vec3 forward = node.GetWorldDirection(MathLib.AXIS.Y);
		vec3 up = node.GetWorldDirection(MathLib.AXIS.Z);

		body.AddForce(forward * moveInput * moveForce);
		body.AddTorque(up * turnInput * turnTorque);

		// AddLinearImpulse applies an instant change in momentum
		if (jumpRequested)
		{
			body.AddLinearImpulse(up * jumpImpulse);
			jumpRequested = false;
		}
	}
}

```

</details>

    Sorry, your browser does not support embedded videos.
*Driven by forces, the object now collides with the wall and is stopped by it - unlike the teleportation example earlier. Pressing Space adds an upward impulse, making it jump.*


> **Notice:** Once an object is driven by physics, torque and collisions can make it topple onto its side. To keep an upright object (a character, for instance) from falling over, set its [AScale](../../../principles/physics/bodies/rigid/index.md#parameter_ascale) to 0 for the X and Y axes, leaving only rotation around the vertical axis.


### Impulse vs Force


Unlike *[AddForce()](../../../api/library/physics/class.bodyrigid_cs.md#addForce_vec3_void)*, which builds force up over time, *[AddLinearImpulse()](../../../api/library/physics/class.bodyrigid_cs.md#addLinearImpulse_vec3_void)* applies an instant change in momentum - ideal for an action like jumping. The **PhysicsMovement** component above already does this on the Space key; the call itself is a single line, where jumpImpulse is the strength of the jump:


```csharp
// Jump with instant impulse
vec3 up = node.GetWorldDirection(MathLib.AXIS.Z);
body.AddLinearImpulse(up * jumpImpulse);

```


### Physics Tips


- **Restrict tipping** - Set the body's *[AScale](../../../principles/physics/bodies/rigid/index.md#parameter_ascale)* (angular velocity multiplier) to 0 for the X and Y axes so it can only turn around the vertical axis and will not topple over
- **Add damping** - Use linear and angular damping to smooth out movement
- **Collision masks** - Ensure shapes have matching collision masks for proper collision detection
- **Avoid scaling moving nodes** - Scaling a node that moves adds extra calculations and can accumulate error in its rotations; physics bodies ignore node scaling altogether. To change an object's size, re-import the model at the desired scale instead


- The C# Component sample moves an object by force or impulse, with adjustable speed and acceleration.
