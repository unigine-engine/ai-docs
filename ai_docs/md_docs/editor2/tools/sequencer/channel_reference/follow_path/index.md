# Follow Path


A **Follow Path** channel moves a node along a keyed trajectory and turns it to face the way it travels. One row carries both halves: three curves say where the node goes, and three settings say where it looks while it gets there.


It sits in the *CINEMATIC* half of the channel picker rather than among the reflected parameters. A node's position is an ordinary vector in that list, and a channel built on it would have nowhere to keep the aiming.


## What It Drives


The target is a node, picked the way it is on any other channel and described in the [Targets and Bindings](../../../../../editor2/tools/sequencer/targets/index.md) article. The channel writes that node's position and its rotation together, so a plain **Node � Position** or **Node � Rotation** channel aimed at the same node has no effect while this one runs.


> **Notice:** A Follow Path channel cannot be re-pointed at another parameter. The attempt is refused, because the forward axis, the up vector and the look-ahead have nowhere to live on a plain vector channel.


## The Trajectory


The path is three curves, one per axis, keyed and edited exactly like those of a vector channel: keys, key types, tangents and extrapolation all behave as they do elsewhere, and the [Constant Speed](../../../../../editor2/tools/sequencer/channels/index.md#constant_speed) option is available, which is usually what a glide along a path wants.


## Where the Node Looks


Three fields under **Channel** decide the rotation.


| Field | What it does |
|---|---|
| **Forward Axis** | Which of the node's own axes is turned along the direction of travel: X, Y, Z or one of the three negatives. The default is Y, the engine's forward for a node; for a camera pick -Z. |
| **Up** | The direction the node treats as up while it is aimed. The default is (0, 0, 1). |
| **Look-Ahead** | How far ahead in time, in seconds, the node reads a second point on the path to work out which way it is going. The default is 0. |


> **Notice:** A stretch of path running straight along the **Up** vector leaves no side axis to build a rotation from. There the node keeps the rotation it already had instead of taking a degenerate one, so turn **Up** if a vertical climb should still be aimed.


**Look-Ahead** of 0 is not off - it means the smallest step the curve can tell apart, so the aim follows the instant tangent and every wobble in the trajectory reaches the rotation. Raising it averages the direction over the stretch ahead: a jittery path stops shaking, at the price of cut corners, since the node begins turning into a bend before it arrives and under-turns on tight ones.

 Best PracticeRaise it only as far as the shaking needs, because the corner-cutting grows with it.
Where the node does not move at all - a flat stretch of the path, or a single key - there is no direction to face, and the rotation is left alone.


## See Also


- [Sequence Channels](../../../../../editor2/tools/sequencer/channels/index.md)
- [Keys and Curves](../../../../../editor2/tools/sequencer/keys/index.md)
- [Converting Legacy Tracks](../../../../../editor2/tools/sequencer/track_import/index.md)
