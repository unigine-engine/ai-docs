# State Machines


A state machine organizes animation logic into a set of discrete states with conditional transitions between them. At any given time, exactly one state is active (or two states are blending during a transition). Each state contains its own animation subgraph that produces the pose for that state.


State machines are the primary tool for structuring character animation behavior. For example, a character's locomotion can be modeled as a state machine with Idle, Walking, Running, and Jumping states, where transitions between them are driven by gameplay parameters such as speed and grounded status.


A state machine is created by placing a **[State Machine](../../../content/animations/graph/node_library/state_machine/index.md)** node in the animation graph. Double-click the State Machine node to enter it and view the state machine editor, where you define states and draw transitions between them.


![](state_machine_example.png)

*A locomotion state machine with four states: Idle, Walk, Run, and Jump.*


## Creating a State Machine


To create a state machine:


1. Right-click on the canvas in the animation graph and select *State Machine* from the node creation menu. ![](state_machine_creation.png)
2. The State Machine node appears with a single **Pose** output port. Connect this output to wherever you need the state machine's result (typically to the **[Output Pose](../../../content/animations/graph/node_library/output/output_pose.md)** node or to a **[Blend Poses](../../../content/animations/graph/node_library/blend/blend_poses.md)** node). Optionally, you can rename the State Machine node for easier identification in the **Graph Hierarchy** panel. ![](../graph/node_library/img/state_machine.png)
3. Double-click the State Machine node to enter it. The editor navigates inside, and the breadcrumb bar updates to show your location (e.g., *Root > Locomotion SM*).
4. Inside, you see the state machine view - a canvas where you can add states and draw transitions. ![](empty_state_machine.png)


An **Entry** node is automatically created inside every state machine. It serves as the starting point - connect it to the state that should be active first when the state machine begins playing.


## States


A state represents a single animation behavior. Each state contains its own nested graph where you build the animation logic using any combination of **[Animation Player](../../../content/animations/graph/node_library/animation/animation_player.md), [Blend Poses](../../../content/animations/graph/node_library/blend/blend_poses.md), [Blend Space](../../../content/animations/blend_spaces/index.md)**, and other nodes.


![](create_new_state.png)

*Right-click context menu inside a state machine. Available node types here: State, Condition, and State Portal.*


To add a state, right-click inside the state machine canvas and select **State**. A new state node appears with a default name. You can rename it in the *Selected Item* panel (see [Animation Graph Editor](../../../content/animations/graph/index.md#side_panels)).


![](inside_state_machine.png)

*Inside a state machine: theEntrynode is connected to a State that contains anAnimation Playerrouted to theOutput Pose. The Graph Hierarchy on the left shows the nesting structure.*


To edit the animation logic of a state, double-click it. The editor navigates into the state's subgraph, and the breadcrumb bar updates (e.g., *Root > Locomotion SM > Walk*). Inside, you build the animation logic the same way as in the main graph - place nodes, connect them, and route the result to the **Output Pose** node.


## Transitions


Transitions define how the state machine moves from one state to another. A transition connects a source state to a target state and fires when its condition evaluates to true.


To create a transition, hover over the edge of a source state until a connection handle appears, then drag to the target state and release. The editor automatically creates a **[Condition](../../../content/animations/graph/node_library/state_machine/condition.md)** node (small circle) between the two states. The Condition node holds all transition settings and the condition logic that determines when the transition fires.


![](creating_condition.png)


The **Entry** node is the only node that connects directly to a state without a *Condition* - it always transitions to its target state immediately when the state machine starts.


You can create multiple transitions from the same state. When multiple outgoing transitions exist, they are evaluated in priority order (see [Condition Properties](#condition_properties)). The first transition whose condition is met fires, and the others are skipped.


*Condition* nodes can be chained - a *Condition* can lead to other Conditions, creating multi-level decision trees for complex transition routing.


![](condition_branching.png)

*A more complex state machine with chained Condition nodes and transitions between multiple states. Conditions can branch, share routes, and form decision trees.*


## Condition Properties


Click a **Condition** node (the small circle on a transition arrow) to view and edit its properties in the **Selected Item** panel:


![](condition_settings.png)


| Name | The display name of the transition. |
|---|---|
| Duration (sec) | How long the blend between the source and target states takes, in seconds. During this time, both states are evaluated each frame and their poses are linearly interpolated. Root motion (if enabled) is also blended proportionally. Once the blend completes, the source state is deactivated. Default: 0.2. |
| Can Be Interrupted | When enabled, this transition can be interrupted by another transition before the blend completes. If disabled, the blend must finish before any new transition can fire. When interrupted, the current blend pose is captured as a frozen snapshot, and a new blend begins from that snapshot to the new target state - so the character transitions smoothly rather than snapping back. |
| Priority | When multiple transitions from the same state have their conditions met simultaneously, the one with the highest priority fires. Always assign distinct priorities to avoid ambiguous evaluation order. |


## Condition Graphs


Every **Condition** node contains a condition graph - a small nested graph that determines when the transition should fire. The condition graph outputs a boolean value via a **[Transition Result](../../../content/animations/graph/node_library/result/transition_result.md)** node, which is created automatically inside every condition graph.


![](empty_condition_graph.png)

*Empty condition graph.*


To edit a transition's condition, double-click the **Condition** node. The Editor navigates into the condition graph. Inside, you build the condition logic using any available nodes. Route the final boolean result to the **Transition Result** node's **Can Transition** input.


![](condition_graph_example.png)

*Example condition graph for a Walk -> Run transition: the transition fires when MoveSpeed is greater than 0.7 and the current animation has less than 5% remaining.*


If the condition graph is empty (no nodes connected to the **Transition Result**), the transition always evaluates to true and fires immediately when the state becomes active.


By default, when a transition fires, the target state's animation starts from the beginning. The **Transition Result** node has an optional **Enter Time** input (shown when *Use Enter Time* is enabled in its properties) that overrides this: provide a normalized time (0.0 to 1.0) to start the target animation at a specific point. For example, 0.5 starts the animation at its halfway point.


## State Portals


A **[State Portal](../../../content/animations/graph/node_library/state_machine/state_portal.md)** reduces visual clutter by replacing multiple identical transitions with a single one. It groups several states into a single transition source - instead of drawing the same transition from each state separately, you draw one transition from the portal.


To add a state portal, right-click inside the state machine canvas and select *State Portal*. In the *Selected Item* panel, check the boxes next to the states you want the portal to represent.


The portal's transition applies to all linked states - each gets the same condition, duration, priority, and interruption settings. Self-transitions are automatically excluded: if the destination state is also listed among the portal's states, that transition is skipped for it.


![](state_portal_example.png)

*A State Portal linking Run, Idle, and Walk states. A single transition through Jump Condition leads to the Jump state - this applies to all three linked states at once. The Selected Item panel on the right shows the portal's state checkboxes.*


> **Notice:** Transitioning **into** a portal that represents multiple states does not work - a single **[Condition](../../../content/animations/graph/node_library/state_machine/condition.md)** cannot determine which of the portal's states to transition to. A portal with a single linked state can be used as a destination.


## Querying State Machine from Code


At runtime, you can query the current state, transition status, and other state machine information from application code. The **[AnimScript](../../../api/library/animations/skeletal/class.animscript_cpp.md)** class provides methods for checking which state is active, whether a transition is in progress, and more. These methods are available in both the C++ and C# APIs.


## See Also


- C++ Sample:
- [Animation Graph Editor](../../../content/animations/graph/index.md)
- [Node Library](../../../content/animations/graph/node_library/index.md)
- [Blend Spaces](../../../content/animations/blend_spaces/index.md)
- [Animation Synchronization](../../../content/animations/synchronization/index.md)
