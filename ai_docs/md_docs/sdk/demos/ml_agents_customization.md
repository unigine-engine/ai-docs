# Building Your Own ML Agent


The **[Unigine ML Integration](../../sdk/demos/ml_agents.md)** demo is a flexible framework you can utilize to build your own training environment based on reinforcement learning: agent and sensor components, a deterministic decision loop, episodes and rewards, and an open *[gRPC](https://grpc.io/)* protocol an external trainer connects to. This article covers the way from the first planning stage to an autonomous agent running on a trained model in the scene, and the steps it involves.


The four worlds of the demo reuse the same components assembled differently, so the world closest to your task is the best reference implementation to fall back on.


To begin with, create a project based on the demo: in the *SDK Browser* open the *Demos* tab and click *Copy As Project* on the **Unigine ML Integration** demo window, *[configure the project](../../sdk/projects/index_cpp.md#creation)* as needed and click *Create New Project*.


![](mlc_guide/mlc_project.png)


## Planning


The *[observation](../../sdk/demos/ml_agents.md#concept_observation)*, the *[actions](../../sdk/demos/ml_agents.md#concept_action)* and the *[reward](../../sdk/demos/ml_agents.md#concept_reward)* are worth settling before any code is written, because they are not equally revisable afterwards. Once a model is trained, **the observation and the actions are fixed**: the model accepts only the exact number of values it was trained on, so adding a sensor or a new action means retraining from scratch. The reward can be adjusted between training runs, and the environment is free to change - layouts, routes and starting positions can all differ, as the observations are relative to the agent.


### The Task and the Episode


A skill is mastered by repetition, so the task has to be restartable: every *[episode](../../sdk/demos/ml_agents.md#concept_episode)* needs both an end condition and a reset. An episode is ended in one of two ways named after the *[Gymnasium](https://gymnasium.farama.org/)* semantics:


- *endEpisode()* - **termination**: the task reached an outcome, either success or failure. The call is the same for both, the difference being in the *[reward](#planning_reward)* the agent adds before it
- *interruptEpisode()* - **truncation**: the episode was cut off by something outside the task, so the agent is not blamed for it (a time limit of your own, counted in seconds rather than in ticks, for instance). *[Max Episode Steps](#agent_max_steps)* needs no such call - the *[session](#env_session)* truncates the episode itself when the set limit is reached


Which of the two it was travels to the trainer with the episode, and the algorithm treats them differently: a truncated episode carries no terminal penalty by default, so being cut off does not teach the agent that its last action was wrong. Charging for a slow solution is the *[reward](#planning_reward)*'s job, and the agent is free to do it - spread over the episode rather than added at the end, so that the agent can tell which of its actions cost it.


### Choosing the Observation


What goes into the observation is a design decision, not a matter of feeding in everything available. Each added value enlarges the input space that the policy has to generalize over, which is paid for in training time, and the choice also decides what the agent has to learn at all: whatever it is handed outright is one skill that will not be acquired. For example, the *[Chase](../../sdk/demos/ml_agents.md#world_chase)* world keeps the exact position of the opponent out of the observation on purpose - the chaser has to spot the runner with its rays. The exact position is only used for the reward: the chaser is paid for every meter it closes the gap by, whether or not it has seen where the runner is.


An observation is assembled from the following sources, and an agent is free to combine them:


| Source | When to use it | Implementation |  |
|---|---|---|---|
| Code | The agent's own data: its velocity, its progress along the route, its offset to a target it tracks | *obs.write()* calls in the *[observe()](#agent_observe)* of your agent class |  |
| Sensors | *[RaySensor](#sensor_ray)* | The surroundings are detected by rays - obstacles, or a target that can break the line of sight | The *RaySensor* property assigned to a *[child node](#env_sensors)* of the agent, which aims it |
| *[CameraSensor](#sensor_camera)* | The task is only present in the rendered image: markings, colors, surfaces with no physical body | The *CameraSensor* property assigned to a *[child node](#env_sensors)* of the agent, which aims it. The trainer switches to a convolutional policy (*CNN*) by itself |  |


> **Notice:** A visual observation is the most expensive one available: it needs a larger network and a rendered frame per decision, so the training runs only as fast as the renderer. This rules out the *[headless mode](../../sdk/demos/ml_agents.md#run_headless)*. Use a camera only where the task cannot be expressed as numbers or raycasts, as in the *[Line Follow](../../sdk/demos/ml_agents.md#world_line)* world, where the line has no physical body for rays to hit.


To implement your own observation logic, you can create a **[custom sensor](#sensor_custom)** - a separate reusable component to be used with multiple agents, for example one that reports the direction towards a target node and the distance to it:


```cpp
int getObservationSize() const override { return 3; }  // dir.x, dir.y, distance

void write(MLAgents::ObservationWriter &obs) override
{
	// the vector from the agent to the target, and how long it is - the distance
	Vec3 to = target->getWorldPosition() - getOwner()->getNode()->getWorldPosition();
	const float dist = float(length(to));

	// the same vector shortened to length 1: the direction alone, XY because the agent moves on a plane
	const vec2  dir  = vec2(float(to.x), float(to.y)) / dist;

	obs.write(dir);								 // 2 values, each already within [-1, 1]
	// the distance as a fraction of the range the sensor reports, so it arrives within [0, 1]
	obs.write(clamp(dist / max_range, 0.0f, 1.0f)); // 1 value -> 3 in total
}
```


> **Notice:** **Normalize the observation**: every value should reach the network within [-1, 1], or [0, 1] for values without a sign, which is done by dividing it by the largest it can take (a limit you set yourself, like a top speed or a sensor range, or one the scene gives you, like the size of the arena). Values left on their own scales arrive as numbers of very different size, and the network gives the large ones more weight than the small ones regardless of how much each actually matters for the task, so the training is slower.


### Choosing the Actions


On a decision tick the policy turns the observation into an action - the numbers the agent applies to the world, changing the environment. Actions are **the policy's only output**, so whatever the agent is meant to control lives here.


Actions come in two kinds:


- **Continuous** actions are a vector of floats the policy samples from a Gaussian distribution, which suits anything that pushes, drives or steers by an amount
- **Discrete** actions are branches, each a categorical choice. They are easier to learn where the options are naturally separate, at the cost of not being able to express a partial input


```cpp
// continuous: two thrust components, each within [-1, 1]
setup.actions = MLAgents::ActionSpec::continuous(2);
// read in act() as actions.continuous(0) and actions.continuous(1)

// discrete: three independent branches of three choices each - driving
// (forward, backward or neither), turning (left, right or neither) and strafing
setup.actions = MLAgents::ActionSpec::discrete({3, 3, 3});
// read as actions.discrete(0), actions.discrete(1), actions.discrete(2),
// each returning the index of the option chosen in that branch: 0, 1 or 2
```


Although the Engine supports both kinds of actions within a single behavior, the bundled trainer rejects a specification containing both, as *Stable-Baselines3* offers no hybrid space. If it is necessary for your project, you can use a different trainer that fits the needs.


When planning this stage, avoid adding redundant steps that need no action of their own: the *[Soccer](../../sdk/demos/ml_agents.md#world_soccer)* players drive, turn and strafe, and a player kicks the ball by driving into it. A separate kick action would only repeat what the movement already implies, and the policy would have to learn it as well.


### Designing the Reward


The reward is the only signal the training algorithm has for shaping the policy, so it decides **what the agent will actually learn**. A working reward function usually has two parts - a *dense term* that reports progress every step, and *sparse terms* for the outcomes. The example below is the reward function of the *[Route Follow](../../sdk/demos/ml_agents.md#world_route)* world:


```cpp
// dense: reward the approach, every step, proportionally
float distance = length(getWaypointOffset());
// the progress since the last step: positive when closing in, negative when drifting away
addReward((prev_distance - distance) * progress_reward);
prev_distance = distance;

// sparse: the outcomes
if (distance < reach_distance)
{
	addReward(0.5f);				  // subgoal reached
	current_waypoint++;
	if (current_waypoint >= getNumWaypoints())
	{
		addReward(1.0f);			  // task complete
		endEpisode();
		return;
	}
	// the next waypoint is a different distance away, so the progress is measured anew
	prev_distance = length(getWaypointOffset());
	requestDecision();				// the target jumped, decide now
}

if (float(node->getWorldPosition().z) < start_z - fall_depth)
{
	addReward(-1.0f);				 // failure: fell off the platform
	endEpisode();
}
```


It illustrates the rules that hold for any task:


- **The dense term carries the learning.** A reward that only arrives on completion is too rare to learn from - the agent has to stumble on the entire solution by chance before receiving any signal. Rewarding the delta towards the goal gives a gradient on every step.
- **Score how the agent works, not only what it achieves.** Paying for the outcome and the overall progress alone leaves standing still and working towards the goal worth the same. The *[Chase](../../sdk/demos/ml_agents.md#world_chase)* world pays the chaser for keeping the runner in sight and charges it for idling, and those two terms are what stop it from parking.
- **A penalty only teaches what the agent can see coming.** The reward for falling off the platform works as far as the observation lets the agent tell it is near the edge, e.g. when given its position within the arena.
- **Expect shortcuts.** If unintended behavior scores higher than the intended solution, the policy will find it and keep it. The *[Soccer](../../sdk/demos/ml_agents.md#world_soccer)* world charges a penalty for a slow episode, and it is kept well below the goal reward on purpose. Raise it too high, and ending the episode pays more than winning it: the team starts conceding goals, or scoring into its own net.


## Preparing the Environment


A training environment splits in two:


- The *[training area](#env_area)* with everything one episode involves - the floor, the props, the *[agents](#env_agent)* and their *[sensors](#env_sensors)*. Duplicating it is what lets multiple episodes run at once
- The global components that run the process - *[Session](#env_session)* for the world and *[BehaviorConfig](#env_behavior)* per behavior


### Setting Up the Agents


The *Agent* component is where the observation, the actions and the reward are defined. All worlds of the demo carry agents of their own, solving their tasks by moving themselves along a route, towards an opponent or away from it, along a line seen with a camera, or into a ball to send it towards a goal. Each of them is driven by a component inherited from *[MLAgents::Agent](../../api/modules/ml_agents/class.agent.md)*, the base class declared in `source/ml_agents/Agent.h`, and you write an agent of your own from the same base.


The base class provides the methods an agent fills in and the ones it calls in return:


| Method | Description |  |
|---|---|---|
| Overridden | *configure()* | Declares the action spec and caches whatever the agent needs. Called once, at initialization |
| *onEpisodeBegin()* | Resets the agent's own state and randomizes the task. The *[TrainingArea](#env_area)* has already moved the nodes back to their starting transforms, so this method only adds what it cannot do - a new target spot, a fresh route, the agent's own counters |  |
| *observe()* | Writes the values the agent reads by itself. They form the *vector* block, which comes first in the observation, before the blocks the sensors add - the layout is printed to the console at startup. The number of values written here is fixed at the first call and must not change, and the Engine reports an error if it does |  |
| *act()* | Applies the action, scores the result and ends the episode. Called on **every tick of the decision loop**, not only on a fresh decision, so the same action arrives again and again until the next decision is taken |  |
| *heuristic()* | Produces an action in the agent's own code, used whenever the behavior has no other brain - no trainer connected and no model assigned. Optional, but the fastest way to verify that the actions and the scene work before any training |  |
| Called | *addReward()* | Adds a value to the reward collected since the last decision |
| *setReward()* | Replaces the reward collected since the last decision instead of adding to it |  |
| *endEpisode()*, *interruptEpisode()* | End the episode as a *[termination or a truncation](#planning_task)* |  |
| *actions.isNewDecision()* | Tells a fresh decision from a repeat in *[act()](#agent_act)*, so anything that must happen once - a reward, an episode end - is guarded by this call |  |


The base *[MLAgents::Agent](../../api/modules/ml_agents/class.agent.md)* class also offers the debug drawing hooks and a way to ask for a decision between the scheduled ones, or instead of them.


Here is how the methods of the class come together in a working component - the snippet below demonstrates a custom agent that steers towards a target, gets paid for closing the distance, charged for running into an obstacle and for falling off the platform, and ends the episode on arrival:


```cpp
class MyAgent: public MLAgents::Agent
{
	// ...

	void act(const MLAgents::Actions &actions) override
	{
		// steer: apply the action as a thrust
		vec2 a = vec2(actions.continuous(0), actions.continuous(1));
		body->addForce(vec3(a, 0.0f) * max_force);

		// dense: pay for every meter closed since the last tick
		float distance = length(vec3(target->getWorldPosition() - node->getWorldPosition()));
		addReward((prev_distance - distance) * 0.05f);
		prev_distance = distance;

		// dense: charge for running into an obstacle, without ending the episode.
		// guarded by isNewDecision(), or the charge would repeat on every tick in between
		if (actions.isNewDecision())
		{
			for (int i = 0; i < body->getNumContacts(); ++i)
			{
				BodyPtr hit = body->getContactBody0(i) == body
					? body->getContactBody1(i)
					: body->getContactBody0(i);
				if (hit && Utils::checkTag(hit->getObject(), "obstacle"))
				{
					addReward(-0.02f);
					break;
				}
			}
		}

		// sparse: fell off the platform
		if (float(node->getWorldPosition().z) < start_z - fall_depth)
		{
			addReward(-1.0f);
			endEpisode();
			return;
		}

		// sparse: the outcome, once the agent is close enough to count as arrived
		if (distance < 1.2f)
		{
			addReward(1.0f);
			endEpisode();
		}
	}

	// ...
};
```


The property of every agent component inherits the base parameters below, set per instance in *UnigineEditor*, along with the custom parameters of your own declared in your component (such as a top speed, a reward coefficient, a target node, etc.):


![The property of the Line Follow agent: the base parameters above, and everything the component declares itself - the Drive and Reward groups, and its own debug switch and vector scale](mlc_guide/mlc_ag_line.png)


| Parameter | Description |
|---|---|
| *Behavior Name* | The behavior this agent belongs to. Agents sharing a name share one brain and must declare an identical spec - the Engine validates this and reports a mismatch. An empty value means the component **class** name |
| *Max Episode Steps* | Physics ticks before the episode is truncated. The default of 0 means an episode that never ends on its own, so always set it - from 1800 to 3600 as a starting range |
| *Decision Interval* | Ask the brain for an action every N ticks: 5 trains faster, 1 moves smoother. 0 - decide only on *requestDecision()* |
| *Between Decisions* | What *[act()](#agent_act)* receives on the ticks in between: *REPEAT_LAST_ACTION* keeps the motion smooth, *ZERO_ACTIONS* zeroes the values instead |
| *Decision Offset* | Shifts this agent's decision ticks to spread the load across agents |
| *Debug Label Height*, *Debug Vector Height* | How far (m) above the agent the reward label floats and its action arrows start - drawn from the origin, the arrows would end up inside the body whenever they point along it, so they are lifted clear instead. The drawing itself is switched on by the debug parameters of the *[Session](#env_session)*, and by the agent's own *[isDebugDrawEnabled()](../../api/modules/ml_agents/class.agent.md)* |


Let's **add an agent component** to the project: open it in your preferred IDE (*Visual Studio 2022* recommended), create a file in the `source` folder, name it `MyAgent.cpp` and copy the following code into it:


[![](mlc_guide/mlc_ide_sm.png)](mlc_guide/mlc_ide.png)


<details>
<summary>MyAgent.cpp | Close</summary>

```cpp
#include <ml_agents/Agent.h>
#include <ml_agents/TrainingArea.h>
#include "common/Tag.h"

#include <UnigineObjects.h>
#include <UniginePhysics.h>

using namespace Unigine;
using namespace Unigine::Math;

class MyAgent: public MLAgents::Agent
{
public:
COMPONENT_DEFINE(MyAgent, MLAgents::Agent);
PROP_PARAM(Node, target);
PROP_PARAM(Float, max_force, 40.0f, "Max Force", "Thrust scale (N).", "Agent");
PROP_PARAM(Float, max_speed, 4.0f, "Max Speed", "Top speed cap (m/s).", "Agent");
PROP_PARAM(Float, fall_depth, 2.0f, "Fall Depth", "Meters below the start height that end the episode.", "Agent");
PROP_PARAM(Float, area_half_size, 10.0f, "Area Half Size", "Half the size of the arena (m).", "Agent");

protected:
void configure(MLAgents::AgentSetup &setup) override
{
	setup.actions = MLAgents::ActionSpec::continuous(2);

	ObjectPtr object = checked_ptr_cast<Object>(node);
	body = object ? checked_ptr_cast<BodyRigid>(object->getBody()) : BodyRigidPtr();
	if (body)
		body->setFreezable(0); // an agent standing still must not be frozen by the physics
	start_z = float(node->getWorldPosition().z);

	// the training area node is the middle of the ground the agent moves on
	if (MLAgents::TrainingArea *area = getTrainingArea())
		area_center = area->getNode()->getWorldPosition();
}

void observe(MLAgents::ObservationWriter &obs) override
{
	// what the agent knows about itself; the target and the obstacles
	// are reported by the sensors on its child nodes.
	// divided by the cap act() holds the speed to, so the values stay within [-1, 1]
	obs.write(body->getLinearVelocity().xy / max_speed);

	// where it stands within the area: 0 in the middle, +-1 at the edge,
	// so the agent can tell the brink from safe ground and learn to avoid falling
	vec2 offset = vec2((node->getWorldPosition() - area_center).xy) / max(float(area_half_size), 0.01f);
	obs.write(clamp(offset, -vec2_one, vec2_one));
}

void act(const MLAgents::Actions &actions) override
{
	vec2 a = vec2(actions.continuous(0), actions.continuous(1));
	body->addForce(vec3(a, 0.0f) * max_force);

	// keep the agent from accelerating without limit
	vec3 v = body->getLinearVelocity();
	if (length(v.xy) > max_speed)
		body->setLinearVelocity(vec3(normalize(v.xy) * max_speed, v.z));

	// dense: pay for every meter closed since the last tick
	float distance = length(vec3(target->getWorldPosition() - node->getWorldPosition()));
	addReward((prev_distance - distance) * 0.05f);
	prev_distance = distance;

	// dense: charge for running into an obstacle, without ending the episode.
	// guarded by isNewDecision(), or the charge would repeat on every tick in between
	if (actions.isNewDecision())
	{
		for (int i = 0; i < body->getNumContacts(); ++i)
		{
			BodyPtr hit = body->getContactBody0(i) == body
				? body->getContactBody1(i)
				: body->getContactBody0(i);
			if (hit && Utils::checkTag(hit->getObject(), "obstacle"))
			{
				addReward(-0.02f);
				break;
			}
		}
	}

	// sparse: fell off the platform
	if (float(node->getWorldPosition().z) < start_z - fall_depth)
	{
		addReward(-1.0f);
		endEpisode();
		return;
	}

	// sparse: the outcome
	if (distance < 1.2f)
	{
		addReward(1.0f);
		endEpisode();
	}
}

void onEpisodeBegin() override
{
	prev_distance = length(vec3(target->getWorldPosition() - node->getWorldPosition()));
}

// a scripted fallback: drive straight at the target, ignoring obstacles
void heuristic(MLAgents::Actions &actions) override
{
	vec2 to = vec2((target->getWorldPosition() - node->getWorldPosition()).xy);
	vec2 dir = length(to) > 1e-4f ? normalize(to) : vec2_zero;
	actions.setContinuous(0, dir.x);
	actions.setContinuous(1, dir.y);
}

private:
BodyRigidPtr body;
float prev_distance = 0.0f;
float start_z = 0.0f;
Vec3 area_center = Vec3_zero;
};

REGISTER_COMPONENT(MyAgent);
```

</details>


Then build the project and generate the property:


1. Add the file to *add_executable* in `source/CMakeLists.txt`: ```text ${CMAKE_CURRENT_LIST_DIR}/MyAgent.cpp ```
2. Select your project in the *Startup Item* list and build it (*Ctrl+B*). ![](mlc_guide/mlc_build.png)
3. Start the application once: the property is generated at startup and becomes available in the Editor.


Now let's **create a new world** and set it up:


1. In the *SDK Browser* open the *My Projects* tab and click *Open Editor* on the project card. ![](mlc_guide/mlc_editor.png)
2. Open the *worlds* folder in the *Asset Browser* and *[create a new world](../../editor2/worlds/index.md#create_world)*. Double-click the world to open it.
3. Add a target for the agent to pursue: click *Create -> Primitive -> Box* on the menu bar, place the created node in the scene and name it `target`. ![](mlc_guide/mlc_addbox.png)
4. Add another *Box* to the scene - the `agent` node for the agent component to drive. Switch the *Mobility* of the node to *Dynamic*, then in the *Physics* tab add a *Rigid Body* with a *Box* shape for collision detection. ![](mlc_guide/mlc_agent_set.png)
5. Assign the generated property `MyAgent.prop` from `data/ComponentSystem` to the `agent` node. Drag the `target` node from the *World Nodes* hierarchy into the *Target* parameter of the component, name the behavior `cube_agent` and set the other parameters as follows: ![](mlc_guide/mlc_agent_prop.png)


An agent does not have to be physical. With no body on the agent's node, *[act()](#agent_act)* drives the transform directly, and a world made of such agents runs on the frame clock rather than the physics one - the *[Stepping](#session_stepping)* parameter of the *Session* switches between the two.


#### Sensor Components


Besides reading its own state in *[observe()](#agent_observe)*, an agent can be given sensors that scan the environment, and what they read is added to the observation. Each sensor forms a block of its own in the observation, named after the sensor and shaped by the data it produces, alongside the block *observe()* writes. The trainer receives every block separately, so it can treat them differently - an image goes through a convolutional encoder, while plain numbers are fed into the network as they are.


The binding between an agent and its sensors is the node hierarchy: a sensor component is placed on a child node of the agent, with **nothing to assign in code**. Both bundled sensors measure along the **+Y** axis of that node, with **+Z** up, so the node is what aims them.


![](mlc_guide/mlc_sensor_hier.png)


Two parameters come from *[MLAgents::Sensor](../../api/modules/ml_agents/class.sensor.md)*, the base class declared in `source/ml_agents/Sensor.h`, so every sensor inherits them:


| Parameter | Description |
|---|---|
| *Sensor Name* | The name under which this sensor's values are logged and reported to the trainer, unique among the sensors of one agent. Left empty, the node name is used |
| *Order* | The position of this sensor's values in the observation: the lower the number, the earlier they come. Equal numbers are resolved by node name, so renaming a node can shuffle the inputs a trained model expects - give the sensors distinct numbers to pin the layout down. It is printed to the console at startup |


##### RaySensor


The *[RaySensor](../../api/modules/ml_agents/class.raysensor.md)* component casts a fan of rays in the plane of the node, telling the agent the distance to what each ray hit and the tag it carries.


![](mlc_guide/mlc_raysens.png)

*The property of the RaySensor used by the Chase agents*


| Parameter | Description |
|---|---|
| *Ray Count* | The number of rays in the fan. Every ray writes what it hit as one value per *[Detectable Tag](#sensor_detectable_tags)*, plus whether it hit anything at all and how far away - 12 rays with one tag come to 36 values. Keep the count no higher than the task requires |
| *Fan Angle* | The total spread of the fan in degrees, centered on the node's **+Y** axis. 360 gives all-round vision |
| *Ray Length* | How far the rays reach, in meters |
| *Intersection Mask* | The *[bit mask](../../principles/bit_masking/index.md#intersection_mask)* the rays test against, which decides the surfaces they can hit at all |
| *Detectable Tags* | The list of *[tags](#sensor_tag)* the sensor distinguishes. Each ray reports which of the tags it hit, in the order listed, so adding one more tag grows the observation by a value per ray and the model has to be trained anew |
| *Debug Draw* | Draw the rays of the last step, green where they hit and grey where they miss. Works only when debug drawing is enabled for the agent and on the *[Session](#env_session)* property |


The demo uses the auxiliary *[Tag](../../api/modules/common/class.tag.md)* component for labeling nodes: put it on every node the sensor is meant to distinguish and use its *Value* parameter to match the tag names listed in *Detectable Tags*. The sensor checks the node a ray hits and its parent.


![](mlc_guide/mlc_tag.png)


##### CameraSensor


The *[CameraSensor](../../api/modules/ml_agents/class.camerasensor.md)* component renders a camera from the node, capturing the surroundings of the agent as an image.


![](mlc_guide/mlc_camsens.png)

*The property of the CameraSensor of the Line Follow car*


| Parameter | Description |
|---|---|
| *Width*, *Height* | The size of the captured image in pixels, at least 36 each, as the trainer's convolutional encoder takes nothing smaller. The cost of a capture depends on their number rather than on the resolution |
| *Grayscale* | One luma channel instead of three, which thirds the observation and costs the same to render. Keep it off wherever color carries the meaning of the task |
| *Field Of View* | The vertical field of view in degrees |
| *Near Clipping*, *Far Clipping* | The clipping planes in meters. Keep the far one as tight as the task allows |
| *Viewport Mask* | What the camera is able to see. For example, you can assign a unique bit to every *[training area](#env_area)* to prevent the agents from seeing the neighboring copies |
| *Debug Save Path* | The path to the `.png` file a single capture is saved as at *[Debug Save At](#sensor_debug_save_at)* - the quickest way to check what the camera sees before looking for the problem in the training. Empty means no saving |
| *Debug Save At* | The number of the capture to save, counted from the world load. The default of 120 skips the first captures, taken before the episode has been rolled |


##### Custom Sensors


The two bundled sensors cover rays and images, and a measurement of your own becomes a sensor the same way: a component inherited from *[MLAgents::Sensor](../../api/modules/ml_agents/class.sensor.md)*, placed on a child node of the agent and writing its own block into the observation. It is worth the separate component whenever the same measurement is needed by more than one agent, or when *[observe()](#agent_observe)* would grow unwieldy.


The base class gives every method a working default, so a sensor overrides only what its own measurement needs. A numeric sensor needs two of them: *getObservationSize()*, reporting how many values it writes, and *write()*, writing exactly that many. The count is fixed for the lifetime of a model, so it must not depend on anything that changes at run time.


An **image sensor** writes bytes instead of floats, which takes three more overrides:


- *writeVisual()* in place of *write()*
- *getDataType()* reporting *UINT8* instead of the default *FLOAT32*
- *getObservationShape()* reporting the dimensions behind the flat value count, which a convolutional encoder needs. *CameraSensor* returns the height, the width and the number of channels - 64x64x1 for the grayscale camera of the line follower, whose observation is 4096 values


Two more are worth knowing about:


- *onEpisodeBegin()* clears whatever state the sensor carries between episodes. *CameraSensor* drops the flag saying it holds a rendered frame, which is what keeps the car of the *[Line Follow](../../sdk/demos/ml_agents.md#world_line)* world from starting an episode steering by the last frame of the one before
- *isOperational()* excludes the sensor from the observation layout when it cannot work at all. *CameraSensor* returns *false* when the Engine runs with no renderer to capture from, which is why a camera rules out the *[headless mode](../../sdk/demos/ml_agents.md#run_headless)*


Both bundled sensors sit next to the base class, in `source/ml_agents/RaySensor.cpp` and `source/ml_agents/CameraSensor.cpp`, and are worth reading as the reference implementations of these methods.


To **add your own sensor** to the project, create one more file in the `source` folder, name it `TargetSensor.cpp` after the class and paste the code into it:


<details>
<summary>TargetSensor.cpp | Close</summary>

```cpp
#include <ml_agents/Agent.h>
#include <ml_agents/Sensor.h>

// The observation: the direction (XY) and the normalized distance to a target node.
// The size is constant and declared in getObservationSize(); write() writes exactly that many.
class TargetSensor : public MLAgents::Sensor
{
public:
	COMPONENT_DEFINE(TargetSensor, MLAgents::Sensor);
	PROP_PARAM(Node, target, "Target", "Node the agent tracks.", "Target");
	PROP_PARAM(Float, max_range, 20.0f, "Max Range", "Distance mapped to 1.0.", "Target");

	int getObservationSize() const override { return 3; } // dir.x, dir.y, distance

	void write(MLAgents::ObservationWriter &obs) override
	{
		using namespace Unigine::Math;
		Vec3 to = Vec3_zero;
		if (target) // getOwner() - the agent that owns this sensor
			to = target->getWorldPosition() - getOwner()->getNode()->getWorldPosition();

		const float dist  = float(length(to));
		const float range = max_range > 0.01f ? max_range.get() : 0.01f;
		const vec2  dir   = dist > 1e-4f ? vec2(float(to.x), float(to.y)) / dist : vec2_zero;

		obs.write(dir);							 // 2 values
		obs.write(clamp(dist / range, 0.0f, 1.0f)); // 1 value -> 3 in total
	}
};
REGISTER_COMPONENT(TargetSensor);
```

</details>


Add it to *source/CMakeLists.txt* as `${CMAKE_CURRENT_LIST_DIR}/TargetSensor.cpp` too, then build and start the application once again to generate the property.


Our agent gets two sensors: the `TargetSensor`, which points it at the target, and a `RaySensor` scanning around for the obstacles in the way. Let's **add both sensors to the scene**:


1. In the Editor, right-click the `agent` node in the *World Nodes* hierarchy and select *Create -> Node -> Dummy*. Place the node anywhere in the scene, name it `target_sensor`, and reset its local transformations.
2. Assign the *data\ComponentSystem\TargetSensor.prop* property to it, drag the `target` node into its *Target* parameter and set *Max Range* to the distance taken as 1.0 when the distance to the target is normalized: ![](mlc_guide/mlc_targ_sens.png)
3. Add one more child *Node Dummy* to the `agent` node the same way, name it `ray_sensor` and reset its transformations too. ![](mlc_guide/mlc_ray_sens.png)
4. Assign the *data\showcase_content\components\ml_agents\RaySensor.prop* property to it and set *Fan Angle* to 360 with *Ray Count* at 12: the all-round fan spots an obstacle behind the agent as well as one in front of it, and 12 rays are enough to tell a gap from a wall without enlarging the observation more than the task needs. Set its *Order* to 1 to have its values follow the `target_sensor` in the observation.
5. Select the `agent` node and set its *[Intersection Mask](../../principles/bit_masking/index.md#intersection_mask)* in the *Surfaces* section to a bit the `ray_sensor` does not use, so that the rays do not hit the body of the agent itself. ![](mlc_guide/mlc_mask.png)


Here's how your *World Nodes* hierarchy should look at this point:


![](mlc_guide/mlc_agent_hier.png)


### Setting Up the Scene


Once the agents are configured, the scene needs three more components: one *[Session](#env_session)* for the whole world, a *[TrainingArea](#env_area)* around each arena, and one *[BehaviorConfig](#env_behavior)* per behavior.


![](mlc_guide/mlc_hier.png)

*The three components in the World Nodes hierarchy*


#### Session Component


Every world has exactly one *[Session](../../api/modules/ml_agents/class.session.md)* component, and it is mandatory: without it the agents switch themselves off and log an error. It drives the *[decision loop](../../sdk/demos/ml_agents.md#concept_loop)*, keeps the behavior registry, owns the trainer connection, and its parameters apply to all the agents at once. The node holding the component can sit anywhere in the hierarchy, under any name.


![](mlc_guide/mlc_session.png)


| Parameter | Description |
|---|---|
| *Seed* | The number the random generation starts from, which makes the runs repeatable: the same seed produces the same routes, layouts and starting positions. 0 - keep the default of the Engine |
| *Time Scale* | How much faster than the real time the simulation runs. A connected trainer may override it with the value from its *[configuration file](#training_config)* > **Notice:** With *[Stepping](#session_stepping)* set to *UPDATE* the decisions come with the rendered frames, and speeding up the time does not add any - the agent simply moves farther between two of them, far enough that it can no longer steer. The Engine clamps the value to 1 here and says so in the console. |
| *Stepping* | The clock the decisions are taken on: - *PHYSICS_TICK* - the fixed physics rate, for the agents that move physically (default) - *UPDATE* - once per rendered frame, for the worlds whose agents move their transforms directly instead of being driven by physics, and for those observing through a camera, where a decision should not act on a stale frame. Set *Fixed Frame Time* alongside it to keep the step constant |
| *Fixed Frame Time* | How much simulation time a single rendered frame covers, for *Stepping* set to *UPDATE*. Without it a decision advances the world by however long the frame happened to take, so the same model behaves differently on another computer. 0.0166667 (1/60 of a second) by default, 0 - use the real frame time |
| *Trainer Port* | The port to connect to when the world is started with the `--trainer-port` argument without a value. 5004 by default |


The component also carries a group of *[debug parameters](../../api/modules/ml_agents/class.session.md)* controlling the on-screen overlay around the agents. You can set them according to your project needs.


In the Editor, add the `session` *Node Dummy* anywhere in the world and assign the `data\showcase_content\components\ml_agents\Session.prop` property to it.


#### BehaviorConfig Component


The *[BehaviorConfig](../../api/modules/ml_agents/class.behaviorconfig.md)* component sets what drives a behavior. It is used for the following:


- Assigning a trained *ONNX* model, which drives the behavior whenever no trainer is connected - this is how a finished agent runs in a game
- Hiding the behavior from the trainer, leaving it on the agents' script
- Marking the behavior with a *Team ID* for a trainer that supports self-play


One component per behavior, and its node can also sit anywhere in the hierarchy. A second one for the same behavior is ignored by the Engine with a warning in the console. Without the `BehaviorConfig` component in the world the agents send their observations to the trainer if one is connected, and act on what it returns. Otherwise, they act on their own *heuristic()*.


![](mlc_guide/mlc_beh.png)

*The two configs of the Chase world, one per behavior, each pointing at the model of its own*


| Parameter | Description |
|---|---|
| *Behavior Name* | The behavior this component applies to, matched against the *[Behavior Name](#agent_behavior)* of the agents. An empty value means the name of the **node** the component sits on |
| *Team ID* | The team of this behavior in adversarial setups. A self-play trainer uses it to tell the opposing sides apart and match a behavior against a pool of its earlier versions. The bundled trainer ignores it |
| *Policy* | What drives the behavior: - *AUTO* - the trainer when one is connected, otherwise the model if assigned, otherwise the agents' *heuristic()* - *HEURISTIC* - always the script, and the behavior is hidden from the trainer. This is how one behavior is trained against another kept fixed |
| *ONNX Model* | The trained model driving this behavior when no trainer is connected |


We have only one behavior type in our project, so let's **add one more *Node Dummy*** in the Editor and name it `behavior_config`. Assign the *data\showcase_content\components\ml_agents\BehaviorConfig.prop* property to the node and set its *Behavior Name* parameter to the same value as the one on the agent - `cube_agent`:


![](mlc_guide/mlc_beh_prop.png)


#### TrainingArea Component


The *[TrainingArea](../../api/modules/ml_agents/class.trainingarea.md)* component goes on the node parenting each arena in the scene. After an episode ends, it restores the nodes below itself to the transforms they had at world initialization, and brings the physical bodies among them to a stop, skipping the nodes with *Mobility* set to *Immovable* (e.g., the ground and the walls) while still going through their children. A prop left immovable by mistake is never restored to its place.


Let's **assemble the training area** around the agent:


1. Select the default `ground` node in the *World Nodes* hierarchy and delete it.
2. Create a `training_area` *Node Dummy* and assign the *data\showcase_content\components\ml_agents\TrainingArea.prop* property to it.
3. Drag *data\showcase_content\meshes\floor.mesh* into the scene and add a *Dummy Body* with a *Box* shape to it in the *Physics* tab. ![](mlc_guide/mlc_floor_body.png)
4. In the *World Nodes* hierarchy drag the nodes `floor, agent` and `target` onto `training_area` to make them its children. ![](mlc_guide/mlc_area_hier.png)
5. Reset the local position of the `floor` node to 0 - the area node sets the height at which it places things, so the floor needs to be aligned with it, and the agent measures its own place in the arena from the `training_area` node as well. The bundled floor is 20 by 20 meters, which is where the *Area Half Size* of 10 *[set on the agent's node](#agent_setup)* comes from. ![](mlc_guide/mlc_floor_transf.png)
6. Adjust the position of the `agent` and `target` boxes if necessary. ![](mlc_guide/mlc_scene.png)


Anything an episode needs to do beyond restoring objects and bringing them to a stop requires a component of your own, subscribed to *getEventReset()* of the *[MLAgents::TrainingArea](../../api/modules/ml_agents/class.trainingarea.md)* class. The example below shows how to move a target to a random spot every time the episode restarts:


```cpp
void MyRandomizer::init()
{
	if (auto *area = ComponentSystem::get()->getComponent<MLAgents::TrainingArea>(node))
		area->getEventReset().connect(this, &MyRandomizer::onReset);
}

// called after the area has restored the transforms and before the agents start
// the episode; driven by the session seed, so the same seed lays out the same episodes
void MyRandomizer::onReset()
{
	target->setWorldPosition(target->getWorldPosition() + vec3(Game::getRandomFloat(-3, 3), 0, 0));
}
```


In our scene we're going to reuse the existing component from the *[Chase](../../sdk/demos/ml_agents.md#world_chase)* world to **randomize the placement of the obstacles**:


1. Assign *data\showcase_content\components\ChaseArenaBlocks.prop* to the `training_area` node alongside the *TrainingArea* property to scatter obstacles anew for every episode. Use its *Min Active* and *Max Active* parameters to set how crowded the arena gets, and *Block Gap* to set how far apart the blocks are placed.
2. Add obstacle nodes to the *Block Assets* array of the `ChaseArenaBlocks` property. The assets that come with the demo are ready to use - each carries a **collision shape** the rays and the agent can hit, and the `Tag` component with its *Value* set to obstacle. Your own obstacles will need the same two things.
3. Select the `ray_sensor` node, set the size of its *Detectable Tags* array to 1 and type obstacle into the field that appears, so that the rays tell the them apart from everything else they hit. ![](mlc_guide/mlc_obstacle.png)


With the scene assembled, **run the world and check the contract line in the console** against what you intended: the number of agents, the size of the observation and the action spec - anything that does not match points to a misconfigured scene.


```text
[ml_agents] behavior "cube_agent?team=0": 16 agent(s), obs 43 = vector(4) + target_sensor(3) + ray_sensor(36), actions = continuous(2), policy = heuristic
```


Where *cube_agent?team=0* is the behavior name with its *[Team ID](#behavior_team_id)* appended, and *obs 43 = vector(4) + target_sensor(3) + ray_sensor(36)* is the size of the observation, followed by the observation blocks it is made of.


Now the agent drives straight at the target on its *heuristic()*, ignoring the obstacles - going around them is what the training teaches it. Close the app and go back to the Editor to **duplicate one area into a grid** as all the copies feed one brain, and the training speeds up almost linearly.


1. Right-click `training_area` in the *World Nodes* hierarchy and select *[Create a Node Reference](../../editor2/exporting_nodes/index.md#export_to_noderef)* - the node will be saved as a `.node` file in the Asset Browser and replaced with a reference to it in the scene. ![](mlc_guide/mlc_ref.png)
2. Copy the reference and place the copies in a grid, leaving enough space between the arenas. Only what sits under the training area node is copied with it, and anything left outside (the `session` and `behavior_config` nodes here) stays single and is shared by every copy. Start with 16 to 32 copies: beyond that the gain depends on the hardware, and a drop in performance can cost more than the extra episodes bring. ![](mlc_guide/mlc_duplicate.png)


#### Curriculum Parameters


> **Notice:** This feature requires a trainer with support for sending curriculum parameters to the Engine. The bundled trainer has no such functionality, so a world reading one keeps running on its default - the feature becomes available with a trainer that implements it.


The Engine also accepts *curriculum* parameters - named values a trainer sets and the scene reads, which is how a task changes its difficulty while the training runs. A task that is too hard from the start produces no successful episode at all, and an agent that never succeeds has nothing to learn from. A value sent by the trainer stays in the session until the trainer replaces it, and the scene reads it by name:


```cpp
void MyField::onReset() // subscribed to getEventReset() of the area
{
	MLAgents::Session *session = MLAgents::Session::get(); // null in a world without one
	float width = session ? session->getEnvParam("goal_width", goal_width) : float(goal_width);
	// ... resize the goal to the new width
}
```


The second argument of *[getEnvParam()](../../api/modules/ml_agents/class.session.md)* is the value to fall back on while nothing has set the parameter, which keeps the scene runnable even without a trainer. Read the parameters on the *[episode reset](#area_reset)* rather than every tick: a value that changes mid-episode moves the task while the agent is still solving it. The *[Soccer](../../sdk/demos/ml_agents.md#world_soccer)* world reads *goal_width* this way and resizes the goal triggers with it.


## Training Your Agent


The bundled trainer is a *Python* script on *[Stable-Baselines3](https://github.com/DLR-RM/stable-baselines3)*, and it covers most tasks unchanged. It offers two algorithms: *PPO* for continuous and discrete action spaces, and *SAC* for continuous ones only - both take vector and visual observations. The script trains any number of behaviors at once, each in its own thread with its own model, which is what makes two behaviors co-trained against each other possible. It has one structural requirement: **every agent of a behavior must be identical** - the same observation shape, the same action spec - and their number must not change while the run lasts, as the trainer feeds a behavior to its model as one batch.


The Engine talks to the trainer over an open *[gRPC](https://grpc.io/)* protocol, sending the observations and rewards of every agent due for a decision and getting the actions back, once per decision tick.


How fast a run goes is decided by three things, in this order:


- The number of *[training areas](#env_area)*
- Running the *Release* build of the project
- The *[time scale](#session_time)* the simulation runs at (on the *[physics clock](#session_stepping)* only)


### The Configuration File


The trainer comes with the `trainer/config.yaml` configuration file, which sets the parameters of a training run and its behaviors. In the example below, the results folder, the port, the seed, the simulation speed and the checkpoint interval are set for the whole run, and the *route_follow* section holds everything that belongs to one behavior:


```text
run_id: my_run
port: 5004
seed: 42
time_scale: 32
checkpoint_freq: 100000

behaviors:
  route_follow:
    algo: ppo
    total_steps: 30000000
    network: { hidden_units: 128, num_layers: 2 }
    ppo:
      learning_rate: 0.0003
      n_steps: 2048
      batch_size: 256
      gamma: 0.99
      ent_coef: 0.005
```


> **Notice:** The *time_scale* parameter of the configuration file is what the simulation runs at while the trainer is connected, and the *[Time Scale](#session_time)* of the *Session* component applies when it is not. You can set it to 1 here to watch the agents at normal speed during the training.


The *route_follow* section holds every field a behavior takes:


- *algo* - the algorithm, *ppo* or *sac*
- *total_steps* - how long to train: the total step count of all the agents of the behavior
- *network* - the size of the network
- a block named after the algorithm - the hyperparameters handed to it


A field you leave out is filled in from elsewhere. The settings shared by the run come from the first source that has one: the command line, then the configuration file, then a default. The command line takes the following arguments:


- `--config` - the configuration file to read
- `--run-id` - the name of the results folder
- `--port` - the port to listen on
- `--seed` - the seed of the run
- `--time-scale` - the simulation speed to ask the Engine for
- `--behavior` - train this behavior alone, out of everything the scene offers


The behavior sections have no command-line equivalent: what is not written there falls back to a default. For *algo* it is *ppo* and for *total_steps* one million, both set by the trainer, while a hyperparameter you leave out keeps its *Stable-Baselines3* default.


Listing several behaviors trains them at once: the trainer runs one model per behavior side by side, as the *[Chase](../../sdk/demos/ml_agents.md#world_chase)* and *[Soccer](../../sdk/demos/ml_agents.md#world_soccer)* worlds do. One file can therefore cover several worlds, as the demo's own does: it lists the behaviors of all four, and every run trains only those the loaded world actually has, the rest being reported in the console and skipped. The reverse does not hold: **a behavior is trained only if the configuration file lists it under the name its agents use**, so any behavior you add needs a section of its own. A behavior with no section is still offered to the trainer and still waits for decisions that never come, so the run ends on the Engine's exchange timeout (60 seconds by default) with nothing trained. To keep a behavior out, set its *[Policy](#behavior_policy)* to *HEURISTIC*.


To start training our agent, let's **add its behavior section to the file**:


```text
behaviors:
  cube_agent:
    algo: ppo
    total_steps: 3000000
```


> **Notice:** The file is sensitive to indentation, which is what sets the nesting: keep the existing alignment as it is and add new sections with the same offsets - the behavior name two spaces in, its fields four.


The rest of the fields - the size of the network and the hyperparameters of the algorithm - are left out, so they keep their defaults.


### Running the Training


Your world is launched for training *[the same way](../../sdk/demos/ml_agents.md#python_env)* as the worlds of the demo. If this is the first time you're running the training, prepare and activate the Python environment first:


```bash
py -3.12 -m venv .venv                  # Linux: python3.12 -m venv .venv
.venv\Scripts\activate                  # Linux: source .venv/bin/activate
pip install -r trainer/requirements.txt
```


The installation is only done once, so later you will only have to activate it with `.venv\Scripts\activate` (`source .venv/bin/activate` on Linux) every time before running the trainer.


1. In the terminal with the Python environment activated, run the following command and wait until the trainer prints the port it is listening on (5004 by default): ```bash python trainer/train.py ```
2. Run the project with the `--trainer-port 5004` startup argument. The port must match the one the trainer reported. Without the argument the Engine never connects, and the trainer keeps waiting. Add `-video_app null` to it to train in the faster *[headless mode](../../sdk/demos/ml_agents.md#run_headless)* when the world allows it.


![](mlc_guide/mlc_run_train.png)


Once the world starts, the Engine console reports the result of the connection and the contract of every behavior it announced, with *policy = remote* now, which is what confirms the trainer took over.


### Following the Progress


The number to watch is the average reward an agent collects per episode: the trainer prints it, the *[statistics window](../../sdk/demos/ml_agents.md#stats)* shows it per behavior over the last 50 episodes, and *[TensorBoard](../../sdk/demos/ml_agents.md#tensorboard)* draws it as a curve over the whole run.


The trainer prints a table every few updates, and three of its rows tell how the run is going:


- `rollout/ep_rew_mean` - the mean reward over the recent episodes, the number that has to grow
- `rollout/ep_len_mean` - how long an episode lasts. Falling while the reward holds means the agent solves the task faster
- `time/total_timesteps` - the steps done so far, against the *total_steps* of the behavior


Read the trend over several updates rather than the change between two: the mean swings because every episode starts from a new random layout and the policy is still exploring. The number rises while the policy improves and goes flat when learning stops because the task is solved or the reward has nothing left to differentiate. A number that keeps rising while the agents misbehave means the reward has a shortcut in it, and with two behaviors trained against each other it can fall simply because the opponent improved faster.


The run ends when a behavior reaches its *[total_steps](#config_total_steps)*, or as soon as the trainer or the world is closed - close the world to stop the training once the reward stops improving, and leave the trainer running until it reports the export. The trainer writes checkpoints along the way to `results/<run-id>/checkpoints`, at the *checkpoint_freq* interval set in the configuration file and counted in the steps of one agent (the default 100,000 creates a checkpoint every 1,600,000 steps with 16 areas), and saves the model with its *ONNX* export however the run ended.


### Running the Trained Model


The exported model is saved as `results/<run-id>/<behavior>.onnx`. To run it in the scene, copy the file into the data of the project and point the *[ONNX Model](#behavior_onnx)* parameter of the behavior's *BehaviorConfig* at it. Started without a trainer, the Engine runs inference itself, with no *Python* involved.


![](mlc_guide/mlc_anim.gif)


> **Notice:** A model trained on a different set of actions than the behavior declares is rejected with an explicit error, and the behavior falls back to its *heuristic()*.


The scene is now yours to build as the project needs it, the model being tied to the observation rather than to the layout it was trained in: the grid of training areas can come down to a single one as the copies only served the speed of training, and the arena can be replaced with the actual level geometry, materials and lighting, with the model driving the agent through it. What has to survive the rebuild is everything the observation is made of: the same sensors with the same settings and the same ranges their values were normalized by, and a scene that stays readable to them - whatever the new props look like, they have to carry what the sensors find them by and tell them apart.


Use this guide to build agents of your own, and tune the reward to the task each of them has. What its terms are worth relative to each other decides the behavior the policy settles on, and every task balances them differently. Train, watch what the agent does, and adjust the terms until the behavior you want is the one that scores highest.


## Accessing Demo Source Code

You can study and modify the source code of this demo to create your own projects. To access the source code do the following:

1. Find the **Building Your Own ML Agent** demo in the *Demos* section and click **[Install](/sdk/#samples)** (if you haven't installed it yet).
2. After successful installation the demo will appear in the *Installed* section, and you can click **Copy as Project** to create a project based on this demo. ![](../../sdk/demos/copy_as_project_gen.png)
3. In the **Create New Project** window, that opens, enter the name for your new project in the corresponding field and click **Create New Project**. ![](../../sdk/projects/create_project_cpp.png)
4. Now you can click **Open Code IDE** to check and modify source code in your default IDE, or click **Open Editor** to open the project in the [UnigineEditor](/editor2/). ![](../../sdk/projects/edit_code.png)
