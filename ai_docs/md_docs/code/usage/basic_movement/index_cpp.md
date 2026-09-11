# Moving Objects (CPP)


Every node you place in UNIGINE is defined by its position, rotation, and scale. For static objects, these properties are usually configured directly in the Editor. To move objects during runtime, you must update their transform properties dynamically through code.


This can be simple teleportation, smooth continuous motion, keyboard-driven control, or physics-based movement - the right choice depends on what you are building. In this article we will work through each of these, starting from the simplest approach and building up to the most capable one.


The **How-To: Move Objects** video, which this article is based on:


### See Also


- Article on [Matrix Transformations](../../../code/fundamentals/matrix_transformations/index_cpp.md)
- The [Node](../../../api/library/nodes/class.node_cpp.md) class API reference
- Article on [Physical Bodies](../../../principles/physics/bodies/index.md)


## Coordinate System


To move an object in a direction, you first need to know how directions are defined. UNIGINE uses a **right-handed Cartesian system** with three axes, and every movement example below refers to them:


- The **+Z axis** points **up**
- The **+Y axis** points **forward**
- The **+X axis** points **right**


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


```cpp
// Move the node to a point in space
node->setWorldPosition(Vec3(10.0f, 20.0f, 5.0f));

```

    Sorry, your browser does not support embedded videos.
*Assigning a position moves the object instantly - it appears at the new spot with no travel in between.*


The two properties differ only when the node has a parent. With no parent, they return the same value. But once the node is a child of another node, *[getPosition()](../../../api/library/nodes/class.node_cpp.md#getPosition_Vec3)* is measured relative to that parent, while *[getWorldPosition()](../../../api/library/nodes/class.node_cpp.md#getWorldPosition_Vec3)* always stays in world space.


> **Notice:** "Local" here means **relative to the parent** - not relative to the node's own orientation. Those are two different ideas; the orientation-based one belongs to *[translate()](../../../api/library/nodes/class.node_cpp.md#translate_Vec3_void)*, covered below.

   Sorry, your browser does not support embedded videos.
*The robot has a parent (the flag). Setting itsPositionplaces it relative to that parent, so it follows the flag rather than landing at fixed world coordinates.*


## Translate Methods


Instead of computing new positions by hand, the *[Node](../../../api/library/nodes/class.node_cpp.md)* class gives us two helper methods that move a node by an offset:


- **Translate()** - moves the node along its own axes, in the direction it is facing
- **WorldTranslate()** - moves the node along the world axes, ignoring its orientation


What sets them apart is whether the node's **orientation** is taken into account - not the parent hierarchy. Both end up changing the world position, as the clip below shows:

   Sorry, your browser does not support embedded videos.
*First the robot moves along the world Y axis (green) withWorldTranslate(), then along its own forward axis withTranslate(). Either way the parent flag makes no difference - the distinction is the robot's orientation, not the hierarchy.*


### WorldTranslate


*[worldTranslate()](../../../api/library/nodes/class.node_cpp.md#worldTranslate_Vec3_void)* moves a node along the world axes, regardless of its orientation. Here we move it 1 unit along world Y:


```cpp
// Move 1 unit along world Y axis
node->worldTranslate(Vec3(0.0f, 1.0f, 0.0f));

```


### Translate


*[translate()](../../../api/library/nodes/class.node_cpp.md#translate_Vec3_void)*, on the other hand, uses the node's own local coordinate system. The vector we pass is read in local space, so *[translate()](../../../api/library/nodes/class.node_cpp.md#translate_Vec3_void)* already accounts for the node's orientation - we do not rotate the vector ourselves. Passing the local forward axis (0, 1, 0) moves the node forward, whichever way it faces:


```cpp
// Move 1 unit forward along the node's local +Y axis
node->translate(Vec3(0.0f, 1.0f, 0.0f));

```


- The C++ sample compares *translate()*, *position*, and *transform* and shows they reach the same result.


## Per-Frame Movement


So far each call moves the node by a set amount. But to keep an object moving - say, forward while a key is held - we call *[translate()](../../../api/library/nodes/class.node_cpp.md#translate_Vec3_void)* on **every frame**, and a problem appears: a fast computer draws more frames per second than a slow one, so a fixed step per frame would travel faster on better hardware.

   Sorry, your browser does not support embedded videos.
*Without frame-rate scaling, the same per-frame step travels faster at 144 FPS than at 60 FPS - the object's speed depends on the hardware.*


To avoid that, we scale each step by how long the frame took. **[Game::getIFps()](../../../api/library/engine/class.game_cpp.md#IFps)* (Inverse Frames Per Second)* gives the time since the last frame, in seconds; multiplying by it turns a per-frame step into a per-second speed, so movement stays consistent regardless of frame rate. Here speed is in units per second - this is the pattern we use throughout the rest of the article:


```cpp
float ifps = Game::getIFps();
// move at "speed" units per second, not per frame
node->translate(Vec3(0.0f, 1.0f, 0.0f) * speed * ifps);

```


## Smooth Movement


The methods so far move the node in fixed steps that we choose. That is fine for input or teleports, but a camera or a pickup should settle onto a target on its own rather than advance in equal jumps. This time, instead of jumping to a fixed point, let's move the node **toward a target**, computing each step from how far it still has to go. UNIGINE's *MathLib* has several functions for this; we will use the two most common ones, *MoveTowards()* and *Lerp()*, which give the motion a noticeably different feel.


### MoveTowards


Often we want an object to approach a target at a **constant speed** and stop cleanly without overshooting. In C#, *MoveTowards()* does exactly this: it advances a value toward a target by at most a given step. C++ has no built-in equivalent, but we get the same result in a few lines - step toward the target by step, and snap to it once we are within one step. In both examples, speed is in units per second:


```cpp
// Move toward target position at constant speed (no MoveTowards in C++)
Vec3 currentPos = node->getWorldPosition();
Vec3 targetPos = Vec3(10.0f, 20.0f, 0.0f);
float step = speed * Game::getIFps();

Vec3 delta = targetPos - currentPos;
double dist = length(delta);
Vec3 newPos = (dist > step) ? currentPos + delta / dist * step : targetPos;
node->setWorldPosition(newPos);

```


Wrapped as a ready-to-use component, **MoveTowardsMover** drives the node toward a target node at a constant speed and stops when it arrives. We just assign the target node to the *Target* field in the Editor:


In the clip below we pick the target interactively instead: a click casts a ray into the scene, drops a marker where it hits, and the object moves to that marker (it also turns to face it with *[worldLookAt()](../../../api/library/nodes/class.node_cpp.md#worldLookAt_Vec3_void)*, covered under [Rotation](#rotation)).

   Sorry, your browser does not support embedded videos.
*Clicking in the scene drops a target marker, and the object travels to it at a steady, constant speed - watch the pace stay even all the way until it stops.*


<details>
<summary>MoveTowardsMover.h | Close</summary>

```cpp
#pragma once
#include <UnigineComponentSystem.h>

class MoveTowardsMover : public Unigine::ComponentBase
{
public:
	COMPONENT_DEFINE(MoveTowardsMover, ComponentBase);

	// node to move toward
	PROP_PARAM(Node, target);
	// movement speed, in units per second
	PROP_PARAM(Float, speed, 5.0f);

	COMPONENT_UPDATE(update);

protected:
	void update();
};

```

</details>


<details>
<summary>MoveTowardsMover.cpp | Close</summary>

```cpp
#include "MoveTowardsMover.h"

#include <UnigineGame.h>

REGISTER_COMPONENT(MoveTowardsMover);

using namespace Unigine;
using namespace Math;

void MoveTowardsMover::update()
{
	if (target.isEmpty())
		return;

	Vec3 currentPos = node->getWorldPosition();
	Vec3 targetPos = target->getWorldPosition();
	float step = speed * Game::getIFps();

	// step toward the target, snapping to it when within one step
	Vec3 delta = targetPos - currentPos;
	double dist = length(delta);
	Vec3 newPos = (dist > step) ? currentPos + delta / dist * step : targetPos;
	node->setWorldPosition(newPos);
}

```

</details>


### Lerp


If we replace *MoveTowards()* with *Lerp()*, the motion becomes smoother: it starts fast and softly slows down as it arrives, the natural way a camera settles onto its target. We get this by calling *Lerp()* **every frame** toward the target with a small factor t - each frame the node covers a fraction of the distance that remains, so its step shrinks as it gets closer.


A note on the name: *Lerp()* (linear interpolation) itself is not eased - a single call just returns a point a fraction t of the way from a to b (a + (b - a) * t). The slowdown comes from repeating it toward a fixed target each frame, not from the function.


```cpp
// Call every frame to ease toward the target
Vec3 currentPos = node->getWorldPosition();
Vec3 targetPos = Vec3(10.0f, 20.0f, 0.0f);
float t = 0.1f; // interpolation factor (0 to 1)

Vec3 newPos = Math::lerp(currentPos, targetPos, t);
node->setWorldPosition(newPos);

```


Wrapped as a component, **LerpMover** eases the node toward a target node every frame. The *Smoothness* field is the per-frame interpolation factor: smaller values give slower, softer motion. As before, we assign the target node to the *Target* field in the Editor:

   Sorry, your browser does not support embedded videos.
*The same click-to-move setup, now with Lerp: the object starts fast and visibly slows down as it nears the marker - compare this eased finish with the even pace ofMoveTowards()above.*


<details>
<summary>LerpMover.h | Close</summary>

```cpp
#pragma once
#include <UnigineComponentSystem.h>

class LerpMover : public Unigine::ComponentBase
{
public:
	COMPONENT_DEFINE(LerpMover, ComponentBase);

	// node to ease toward
	PROP_PARAM(Node, target);
	// per-frame interpolation factor (0 to 1)
	PROP_PARAM(Float, smoothness, 0.1f);

	COMPONENT_UPDATE(update);

protected:
	void update();
};

```

</details>


<details>
<summary>LerpMover.cpp | Close</summary>

```cpp
#include "LerpMover.h"

REGISTER_COMPONENT(LerpMover);

using namespace Unigine;
using namespace Math;

void LerpMover::update()
{
	if (target.isEmpty())
		return;

	Vec3 currentPos = node->getWorldPosition();
	Vec3 targetPos = target->getWorldPosition();

	// each frame, close a fraction of the remaining distance
	node->setWorldPosition(lerp(currentPos, targetPos, smoothness));
}

```

</details>


Which to use? Reach for *MoveTowards()* when you want a predictable, **constant speed** and a clean stop - good for an object travelling to a waypoint. Reach for *Lerp()* when you want a soft, **eased** finish - good for a camera or UI element that should glide into place.


### Putting It Together: Click to Move


The clips above come from a single component that ties these pieces together: it casts a ray from the camera through the mouse cursor, drops a marker where the ray hits the scene, then turns the node toward that point with *[worldLookAt()](../../../api/library/nodes/class.node_cpp.md#worldLookAt_Vec3_void)* and advances it with *MoveTowards()*. Swap that one call for *Lerp()* to get the eased variant.


<details>
<summary>MoveToPoint.h | Close</summary>

```cpp
#pragma once
#include <UnigineComponentSystem.h>
#include <UnigineWorld.h>

class MoveToPoint : public Unigine::ComponentBase
{
public:
	COMPONENT_DEFINE(MoveToPoint, ComponentBase);

	// marker node showing where the ray hit
	PROP_PARAM(Node, laser);
	// movement speed, in units per second
	PROP_PARAM(Float, speed, 5.0f);

	COMPONENT_INIT(init);
	COMPONENT_UPDATE(update);

protected:
	void init();
	void update();

private:
	Unigine::WorldIntersectionPtr intersection;
};

```

</details>


<details>
<summary>MoveToPoint.cpp | Close</summary>

```cpp
#include "MoveToPoint.h"

#include <UnigineGame.h>
#include <UnigineInput.h>

REGISTER_COMPONENT(MoveToPoint);

using namespace Unigine;
using namespace Math;

void MoveToPoint::init()
{
	intersection = WorldIntersection::create();
	// let the cursor move freely so we can click anywhere
	Input::setMouseHandle(Input::MOUSE_HANDLE_SOFT);
}

void MoveToPoint::update()
{
	if (Input::isMouseButtonPressed(Input::MOUSE_BUTTON_LEFT))
	{
		// cast a ray from the camera through the mouse cursor
		ivec2 mouse = Input::getMousePosition();
		Vec3 p0 = Game::getPlayer()->getWorldPosition();
		Vec3 p1 = p0 + Vec3(Game::getPlayer()->getDirectionFromMainWindow(mouse.x, mouse.y)) * 50.0f;
		World::getIntersection(p0, p1, 1, intersection);

		// place the marker at the hit point
		laser->setWorldPosition(intersection->getPoint());
	}

	// face the marker and move toward it at a constant speed
	Vec3 target = laser->getWorldPosition();
	node->worldLookAt(target);

	Vec3 currentPos = node->getWorldPosition();
	float step = speed * Game::getIFps();
	Vec3 delta = target - currentPos;
	double dist = length(delta);
	node->setWorldPosition((dist > step) ? currentPos + delta / dist * step : target);
}

```

</details>


- The C++ sample shows the raycast-from-cursor part on its own, using *World::getIntersection()*.


- For movement along a predefined path, see the C++ sample (linear and spline interpolation).


## Rotation


Rotation mirrors translation: *[rotate()](../../../api/library/nodes/class.node_cpp.md#rotate_float_float_float_void)* spins the node in its own local space, while *[worldRotate()](../../../api/library/nodes/class.node_cpp.md#worldRotate_float_float_float_void)* spins it around the world axes. Both take Euler angles in degrees.


The three angles passed to *[rotate()](../../../api/library/nodes/class.node_cpp.md#rotate_float_float_float_void)* map directly to the axes: (X, Y, Z). With UNIGINE's axes (+X right, +Y forward, +Z up) this corresponds to **pitch** (tilt up and down, around X), **roll** (bank sideways, around Y), and **yaw** (turn left and right, around Z). So to turn an object left or right, we change the third angle, as below:


```cpp
// Rotate around Z axis (yaw) by angle per frame
float turnSpeed = 90.0f; // degrees per second
node->rotate(0.0f, 0.0f, turnSpeed * Game::getIFps());

```


When we just need a node to face something, there is no need to work out the angles ourselves: *[worldLookAt()](../../../api/library/nodes/class.node_cpp.md#worldLookAt_Vec3_void)* aims the node's forward axis (+Y) at a target position and fills in the rest of the orientation, keeping the node upright (its up axis stays aligned with world up). The turn is applied instantly, in a single frame. The click-to-move examples above use exactly this to keep the object facing the point it travels toward. To turn smoothly instead of snapping, interpolate the rotation toward the target with *Slerp()* each frame - the same idea as *Lerp()*, but for orientations.


```cpp
// Rotate to face the target
node->worldLookAt(targetPos);

```


## Keyboard Control


Let's put this together into one of the most common patterns in games: free-form movement driven by the keyboard. The result is a [component](../../../principles/component_system/index.md) - a reusable script we attach to a node in the Editor - whose logic runs every frame, reads the keyboard, and moves the node it is attached to. We expose *moveSpeed* and *turnSpeed* as public parameters so they can be tuned in the Editor; the arrow keys or WASD drive the node:


<details>
<summary>SimpleMovement.h | Close</summary>

```cpp
#pragma once
#include <UnigineComponentSystem.h>

class SimpleMovement : public Unigine::ComponentBase
{
public:
	COMPONENT_DEFINE(SimpleMovement, ComponentBase);

	// movement speed, in units per second
	PROP_PARAM(Float, moveSpeed, 5.0f);
	// rotation speed, in degrees per second
	PROP_PARAM(Float, turnSpeed, 90.0f);

	COMPONENT_UPDATE(update);

protected:
	void update();
};

```

</details>


<details>
<summary>SimpleMovement.cpp | Close</summary>

```cpp
#include "SimpleMovement.h"

#include <UnigineGame.h>
#include <UnigineInput.h>

REGISTER_COMPONENT(SimpleMovement);

using namespace Unigine;
using namespace Math;

void SimpleMovement::update()
{
	float ifps = Game::getIFps();

	// forward/backward movement along the node's local axis
	if (Input::isKeyPressed(Input::KEY_W) || Input::isKeyPressed(Input::KEY_UP))
		node->translate(Vec3(0.0f, 1.0f, 0.0f) * moveSpeed * ifps);
	if (Input::isKeyPressed(Input::KEY_S) || Input::isKeyPressed(Input::KEY_DOWN))
		node->translate(Vec3(0.0f, -1.0f, 0.0f) * moveSpeed * ifps);

	// left/right rotation (yaw around the up axis)
	if (Input::isKeyPressed(Input::KEY_A) || Input::isKeyPressed(Input::KEY_LEFT))
		node->rotate(0.0f, 0.0f, turnSpeed * ifps);
	if (Input::isKeyPressed(Input::KEY_D) || Input::isKeyPressed(Input::KEY_RIGHT))
		node->rotate(0.0f, 0.0f, -turnSpeed * ifps);
}

```

</details>

    Sorry, your browser does not support embedded videos.
*WASD moves the object forward and back and turns it left and right. Note that it passes straight through the wall - direct transform changes do not collide with anything.*


Under the hood this is still teleportation - we update the transform directly. The difference is that the updates happen in very small steps, many times per second, which reads as smooth, continuous motion.


> **Notice:** Because the transform is set directly, the node ignores obstacles and passes straight through them. For collision-aware movement, use physics instead.


## Physics-Based Movement


To make movement respect collisions, we drive the object through the physics system instead of changing its transform directly. The idea is the same as before, only now the object is moved by forces. This needs a *Rigid Body* assigned to the node (a *BodyRigid* object in code), together with a collision shape.


### Physics Setup


Before using physics-based movement:


1. Set the node's *Mobility* to *Dynamic*
2. Add a *Rigid Body* in the Physics tab ![](add_rigid_body.png)
3. Add a *Shape* (e.g., Capsule, Box, or Sphere) for collision detection ![](add_physics_shape.png)
4. Configure [collision masks](../../../principles/physics/collision/index.md) on the surfaces you want to collide with


### Forces and Torques


We push the body with *[addForce()](../../../api/library/physics/class.bodyrigid_cpp.md#addForce_vec3_void)* and rotate it with *[addTorque()](../../../api/library/physics/class.bodyrigid_cpp.md#addTorque_vec3_void)*, and we call them in *UpdatePhysics()* rather than *Update()* so that physics handles the result.


To push the body in the direction it currently faces, we need that direction in world space - and it changes as the object turns. *[getWorldDirection()](../../../api/library/nodes/class.node_cpp.md#getWorldDirection_int_vec3)* gives it to us: we pass an axis and it returns that axis rotated by the node's current orientation. The component below takes the node's forward (*AXIS_Y*) for movement and its up (*AXIS_Z*) for turning:


<details>
<summary>PhysicsMovement.h | Close</summary>

```cpp
#pragma once
#include <UnigineComponentSystem.h>
#include <UniginePhysics.h>

class PhysicsMovement : public Unigine::ComponentBase
{
public:
	COMPONENT_DEFINE(PhysicsMovement, ComponentBase);

	// continuous force and torque while a key is held
	PROP_PARAM(Float, moveForce, 10.0f);
	PROP_PARAM(Float, turnTorque, 5.0f);
	// instant upward impulse on jump
	PROP_PARAM(Float, jumpImpulse, 5.0f);

	COMPONENT_INIT(init);
	COMPONENT_UPDATE(update);
	COMPONENT_UPDATE_PHYSICS(updatePhysics);

protected:
	void init();
	void update();
	void updatePhysics();

private:
	Unigine::BodyRigidPtr body;
	float moveInput = 0.0f;
	float turnInput = 0.0f;
	bool jumpRequested = false;
};

```

</details>


<details>
<summary>PhysicsMovement.cpp | Close</summary>

```cpp
#include "PhysicsMovement.h"

#include <UnigineInput.h>

REGISTER_COMPONENT(PhysicsMovement);

using namespace Unigine;
using namespace Math;

void PhysicsMovement::init()
{
	body = node->getObjectBodyRigid();
}

void PhysicsMovement::update()
{
	// read input every frame, apply it in updatePhysics()
	moveInput = 0.0f;
	turnInput = 0.0f;

	if (Input::isKeyPressed(Input::KEY_W)) moveInput = 1.0f;
	if (Input::isKeyPressed(Input::KEY_S)) moveInput = -1.0f;
	if (Input::isKeyPressed(Input::KEY_A)) turnInput = 1.0f;
	if (Input::isKeyPressed(Input::KEY_D)) turnInput = -1.0f;
	if (Input::isKeyDown(Input::KEY_SPACE)) jumpRequested = true;
}

void PhysicsMovement::updatePhysics()
{
	if (!body)
		return;

	vec3 forward = node->getWorldDirection(AXIS_Y);
	vec3 up = node->getWorldDirection(AXIS_Z);

	body->addForce(forward * moveInput * moveForce);
	body->addTorque(up * turnInput * turnTorque);

	// AddLinearImpulse applies an instant change in momentum
	if (jumpRequested)
	{
		body->addLinearImpulse(up * jumpImpulse);
		jumpRequested = false;
	}
}

```

</details>

    Sorry, your browser does not support embedded videos.
*Driven by forces, the object now collides with the wall and is stopped by it - unlike the teleportation example earlier. Pressing Space adds an upward impulse, making it jump.*


> **Notice:** Once an object is driven by physics, torque and collisions can make it topple onto its side. To keep an upright object (a character, for instance) from falling over, set its [AScale](../../../principles/physics/bodies/rigid/index.md#parameter_ascale) to 0 for the X and Y axes, leaving only rotation around the vertical axis.


### Impulse vs Force


Unlike *[addForce()](../../../api/library/physics/class.bodyrigid_cpp.md#addForce_vec3_void)*, which builds force up over time, *[addLinearImpulse()](../../../api/library/physics/class.bodyrigid_cpp.md#addLinearImpulse_vec3_void)* applies an instant change in momentum - ideal for an action like jumping. The **PhysicsMovement** component above already does this on the Space key; the call itself is a single line, where jumpImpulse is the strength of the jump:


```cpp
// Jump with instant impulse
vec3 up = node->getWorldDirection(AXIS_Z);
body->addLinearImpulse(up * jumpImpulse);

```


### Physics Tips


- **Restrict tipping** - Set the body's *[AScale](../../../principles/physics/bodies/rigid/index.md#parameter_ascale)* (angular velocity multiplier) to 0 for the X and Y axes so it can only turn around the vertical axis and will not topple over
- **Add damping** - Use linear and angular damping to smooth out movement
- **Collision masks** - Ensure shapes have matching collision masks for proper collision detection
- **Avoid scaling moving nodes** - Scaling a node that moves adds extra calculations and can accumulate error in its rotations; physics bodies ignore node scaling altogether. To change an object's size, re-import the model at the desired scale instead


- The C++ sample moves an object by force or impulse, with adjustable speed and acceleration.
