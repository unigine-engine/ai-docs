# Procedural Skeleton Control


Some animation graph nodes change the skeleton directly. Unlike nodes that play or blend animation clips and pass the result down as a finished pose, these nodes **read and write individual joints** according to rules you set, computing the change each frame from the current state of the scene rather than from a clip.


The most common example is placing a foot on uneven ground. The walking clip plays the same step every time, but a raycast finds the real ground height each frame and the leg is bent to match it. The foot then lands on the surface instead of hovering above it or sinking into it.


You build these adjustments with dedicated nodes in the graph, and the same operations are available from application code through the [NodeSkeletonPose](../../../api/library/nodes/class.nodeskeletonpose_cpp.md) class and its parameter classes. For the full list of inputs and properties of a node, follow the links to the [Animation Graph Nodes](../../../content/animations/graph/node_library/index.md) reference.


> **Notice:** In earlier versions, **Inverse Kinematics** and **Look-At Chains** were available only on the legacy **[ObjectMeshSkinnedLegacy](../../../api/library/objects/class.objectmeshskinnedlegacy_cpp.md#ik_chains)** object, driven completely from code. The graph nodes described here are the new, visual way to set them up on **[ObjectMeshSkinned](../../../objects/objects/mesh_skinned/index.md)** with a **[NodeSkeletonPose](../../../objects/animations/nodeskeletonpose/index.md)**.


## Inverse Kinematics


Inverse kinematics rotates a **chain of joints** so the end of a limb reaches a given position. You provide the target point, and the solver works out the joint angles that put the limb there. This is the reverse of ordinary animation, where the joint angles are set in the clip and the end of the limb ends up wherever they place it.


IK is useful whenever the target is not known until runtime: planting a foot on ground whose height changes, keeping a hand on a door handle as the character shifts, or aiming a limb at a moving object.


### Two Bone IK and IK Chain


Two nodes perform inverse kinematics. Which one to use depends on the limb.


**[Two Bone IK](../../../content/animations/graph/node_library/skeleton/two_bone_ik.md)** is for a limb with a single obvious joint in the middle, such as an arm (shoulder, elbow, wrist) or a leg (hip, knee, ankle). A limb like this bends in one plane, so there is exactly one correct pose for a given target. The node computes that pose in a single step, without repeated tries.

   Sorry, your browser does not support embedded videos.
**[IK Chain](../../../content/animations/graph/node_library/skeleton/ik_chain.md)** is for a chain of many joints, such as a spine, a tail, or a finger. A long chain can bend into many shapes that all reach the target, so the node picks one by adjusting the joints over repeated passes until the end is close enough.

   Sorry, your browser does not support embedded videos.
### Controlling the Bend Direction


A bent limb has a choice the target alone does not settle: it can swing around the straight line between the limb's base and its end while still reaching the same point. A knee, for example, can point forward or off to the side and the foot lands in the same place either way. Left unmanaged, the limb keeps whatever direction the animation gave it, which can look wrong when the target moves.

   Sorry, your browser does not support embedded videos.
The **Pole** input removes the guesswork. It marks a position that the middle joint turns to face, and the limb always bends toward it. Place the pole in front of a knee or ahead of an elbow to fix which way each one bends. The pole is only used when it is switched on: **[Two Bone IK](../../../content/animations/graph/node_library/skeleton/two_bone_ik.md)** has a **Use Pole** input for that, while **[IK Chain](../../../content/animations/graph/node_library/skeleton/ik_chain.md)** reads the pole when its **Limit Source** property is set to Pole. With the pole off, the limb keeps the bend direction of the incoming animation.


> **Notice:** **[IK Chain](../../../content/animations/graph/node_library/skeleton/ik_chain.md)** can also constrain the bend with joint limits, see [Joint Limits](#limits) below.


### Reaching Distant Targets


When the target is within reach, the limb simply bends to meet it. When the target moves farther away than the limb can stretch, the limb has to straighten out, and the **Solver Mode** decides how it does so:


- **Hard** - the limb straightens completely and stops at full length. The moment it runs out of reach is visible as a small snap.
- **Soft** - the limb eases toward full length instead of locking, trading an exact reach near the limit for a smooth motion with no snap. Use this for hands and feet, where the snap would be noticeable.
- **Stretching** - the bones lengthen so the end stays on the target even past normal reach, up to a limit you set.


![Solver Mode Settings](solver_mode_settings.png)


Because **[IK Chain](../../../content/animations/graph/node_library/skeleton/ik_chain.md)** works over several passes, it has extra settings that control how it converges and how smooth the result is. See its [node description](../../../content/animations/graph/node_library/skeleton/ik_chain.md) for the full list.


![IK Chain Advanced Settings](ik_chain_advanced_settings.png)


## Look At


**Look At** points a joint's forward axis in the direction of a target. Unlike IK, which reaches a target **position**, it aims in a target **direction** and affects only rotation. A common use is making a character follow the player or a nearby enemy with its head and eyes as they move around the scene, on top of whatever body animation is already playing. Two nodes cover this:


- **[Joint Look At](../../../content/animations/graph/node_library/skeleton/joint_look_at.md)** - aims a single joint of a skeleton.
- **[Look At Chain](../../../content/animations/graph/node_library/skeleton/look_at_chain.md)** - distributes the aiming rotation across a chain, so the tip aims while the other joints contribute a share (controlled by per-joint weights).

   Sorry, your browser does not support embedded videos.
The main setting is the **Forward Axis**: the joint's local axis that should end up pointing at the target. Which one it is depends on how the skeleton was built, so it is easiest to enable the preview, select the node, and read the local axes drawn on the joint.


As with IK, a **Pole** keeps the joint from rolling around its aim direction as the target moves. A **Max Angle** caps how far the joint may turn away from the animation, which keeps the result plausible, such as a head that should not turn too far from the spine. The remaining settings are described in the node descriptions.


## Joint Limits


When you build a chain of joints with an **[IK Chain](#ik)** or a **[Look At Chain](#look_at)**, the solver can reach the target with a pose no real joint could strike, such as an elbow bent the wrong way or a knee turned inside out. Joint limits restrict the local rotation of a joint to an anatomically valid range. The solver then keeps its result within poses the body could actually hold.


![Joint Limits Example](limits_example.png)


Four **basic limit nodes** each restrict one kind of motion:


| Basic limits |  |
|---|---|
| [Joint Hinge Limit](../../../content/animations/graph/node_library/skeleton/joint_hinge_limit.md) | A hinge around one axis. May be used for a knee, an elbow, or a finger. |
| [Joint Cone Limit](../../../content/animations/graph/node_library/skeleton/joint_cone_limit.md) | Swing kept inside a cone. May be used for a joint that tilts the same amount in every direction. |
| [Joint Cone Asym Limit](../../../content/animations/graph/node_library/skeleton/joint_cone_asym_limit.md) | Swing kept inside a lopsided cone, with different angles each way. May be used for a shoulder. |
| [Joint Twist Limit](../../../content/animations/graph/node_library/skeleton/joint_twist_limit.md) | Twist around the bone kept in range, with the swing left free. May be used for a forearm. |


The other three **combine a swing limit with a twist limit**, for joints that need both at once:


| Combined limits |  |
|---|---|
| [Joint Hinge Twist Limit](../../../content/animations/graph/node_library/skeleton/joint_hinge_twist_limit.md) | A hinge and a twist combined together. |
| [Joint Cone Twist Limit](../../../content/animations/graph/node_library/skeleton/joint_cone_twist_limit.md) | A cone swing and a twist combined together. |
| [Joint Cone Asym Twist Limit](../../../content/animations/graph/node_library/skeleton/joint_cone_asym_twist_limit.md) | A lopsided cone swing and a twist combined together. The most complete limit, for a full anatomical joint. |


Every limit node shares the same core settings:


- **Mode**:

  - **Free** - the joint moves without restriction. Use it to turn the limit off without removing the node.
  - **Limited** - the joint is kept within the range you set. This is the working mode.
  - **Locked** - the joint is held fixed and does not move at all.
- **Preferred Rotation** and **Preferred Strength** - an optional soft attractor that nudges the joint toward a resting pose after clamping.


> **Notice:** The preferred rotation is a quaternion. To set it in degrees, drive it from an **[Euler to Quat](../../../content/animations/graph/node_library/math/euler_to_quat.md)** node.


A limit node works in one of two ways, depending on which output you connect. Connect its **Pose** output to clamp the pose in place. Connect its **Limit** output instead, leaving the pose output free, and the node becomes a constraint you feed into the **Limits** input of an [IK Chain](#ik) or a [Look At Chain](#look_at). On an IK Chain, wiring a limit in also switches its **Limit Source** to Joint Limits, so the limit takes effect at once instead of sitting there inert.

 Best Practice
To apply several limits to one chain, connect each limit's **Limit** output to a **[Joint Limit Set](../../../content/animations/graph/node_library/skeleton/joint_limit_set.md)** and feed the set into the chain's **Limits** input. The set bundles the limits into one connection, and each limit keeps its own settings and its own preview.


![Joint Limit Set Usage](joint_limit_set_usage.png)


## Direct Joint Access


The **Joint Transform Nodes** read and write a single joint directly. **[Get Joint Transform](../../../content/animations/graph/node_library/transform/get_joint_transform.md)** reads a joint's **position**, **rotation**, and **scale** from the pose, and **[Set Joint Transform](../../../content/animations/graph/node_library/transform/set_joint_transform.md)** writes them back. A **Space** property selects local (relative to the parent) or object space.


| ![](../graph/node_library/img/get_joint_transform.png) | ![](../graph/node_library/img/set_joint_transform.png) |
|---|---|


They are often used together with the other procedural nodes: for example, adding a **Set Joint Transform** after an IK node to orient a foot to the ground surface, or using **Get Joint Transform** to read where a hand ended up so gameplay logic can attach an object to it.


Values often have to cross a space boundary on the way in or out - a target arrives in world space while a solver expects object space, or a rotation read in object space has to be written back into the local frame of another joint. Three nodes do that conversion: **[Position Space](../../../content/animations/graph/node_library/transform/position_space.md)** for points, **[Direction Space](../../../content/animations/graph/node_library/transform/direction_space.md)** for directions, and **[Rotation Space](../../../content/animations/graph/node_library/transform/rotation_space.md)** for rotations.


## Visualizing in the Preview


Every solver and every joint limit draws a **debug overlay** in the preview viewport that shows what it is doing to the skeleton. The overlay appears when the node's **preview eye icon** is enabled in its header and a preview mesh is assigned. Enable it on the node whose behavior you want to inspect. The [Joint Transform](#transforms) nodes draw no overlay of their own.


![Preview Eye](two_bone_ik_preview_eye.png)


Each node type draws its own shapes:


- **[Two Bone IK](../../../content/animations/graph/node_library/skeleton/two_bone_ik.md)** and **[IK Chain](../../../content/animations/graph/node_library/skeleton/ik_chain.md)** draw a marker on every joint of the chain joined by lines, a target marker with a line from the last joint to it that shows how far the chain falls short, and, when a pole is used, a filled triangle for the bend plane with the pole point marked. ![IK debug overlay](ik_preview.png)
- **[Joint Look At](../../../content/animations/graph/node_library/skeleton/joint_look_at.md)** and **[Look At Chain](../../../content/animations/graph/node_library/skeleton/look_at_chain.md)** draw a line from the joint to the target with a target marker, plus arrows for the **Forward Axis** and **Up Axis** so you can confirm which way the joint is pointing. ![Look At debug overlay](look_at_preview.png)
- The **[Joint Limit Set](../../../content/animations/graph/node_library/skeleton/joint_limit_set.md)** node draws every limit it holds at once, which is the quickest way to check a whole chain.
- **[Joint Limit Nodes](#limits)** draw the allowed range as a shape at the joint: an arc for a hinge, a cone for a cone or asymmetric cone, and a wedge for a twist. The limit axes are drawn as arrows, which is the fastest way to check that an axis points along the joint you intended. When **Preferred Strength** is greater than zero, the attractor is marked as well - a preferred rotation on its own draws nothing, because a zero strength means the attractor is off. ![Joint limit debug overlay](limits_preview.png)


> **Notice:** Axes are set in the joint's local frame. If you are not sure which one to pick, enable the preview and read the arrows drawn on the joint.
