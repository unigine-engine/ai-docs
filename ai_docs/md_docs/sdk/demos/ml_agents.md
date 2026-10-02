# Unigine ML Integration


![](ml_main.png)


The current surge in AI has changed a lot about **machine learning** and has turned it into a process which anyone from game and simulator developers to unmanned systems or industrial robotics engineers and urban planners can benefit from. And what changed is not just the scale of it. With the soaring growth of the industry, training **machine learning agents** - the entities that autonomously interact with the environment - no longer means laying down the code they would follow, nor requires a tutor repetitively training them to figure out certain patterns. Instead, dropped into a simulated reality, an agent explores it without any preconceptions, observing the consequences of its actions, and working its way towards a strategy nobody handed it. Built on **reinforcement learning**, a method borrowed from behavioral psychology, this is a cutting-edge mechanism in its own right, and what finally **makes an agent truly autonomous**.


Every move the agent makes changes the training environment and comes back scored - *positive* for what advances the task, *negative* for what works against it. Those scores accumulate into a *policy*, where the actions that score highest become the ones the agents reach for. As a result you get a *system that builds its own understanding of the environment* around it and acts according to circumstances as they shift, improving with every iteration instead of merely following direct orders and prebuilt routes.


![](ml_principle.png)

*The reinforcement learning loop: the agent acts on the environment, the environment changes and reports back the new state along with a reward for what the action achieved*


The flexible architecture of the environment supports a wide range of interaction scenarios: agents can be set *against the training environment itself*, either pushing objects or navigating themselves between obstacles, or *against each other* - in teams that compete, cooperate or even both. Reinforcement learning also cuts the other way: point a trained agent *at your own simulation* and it will find the seams you never knew were there.


Reinforcement learning is the go-to solution anywhere the environment is too complex to plan for in advance, and it is already leveraged across many industries:


- **Autonomous systems** - from warehouse robots and robotic vacuums finding their way around obstacles to delivery rovers, autopilots, drones and large-scale industrial simulations
- **Crowds and traffic simulation** - pedestrians and vehicles that react to what is happening around them, and characters that adapt to the gameplay
- **Complex adversarial tasks** where the right move depends on what an opponent does next
- **Adaptive environments** that gradually raise the difficulty in response to the progress being made, keeping the task within reach at every stage
- **Testing** the simulation itself - finding gaps in collision, exploitable joints and states your logic never anticipated


**Unigine ML Integration** demo is a practical starting point for **training intelligent agents**: four worlds - *[Route Follow](#world_route)*, *[Chase](#world_chase)*, *[Line Follow](#world_line)* and *[Soccer](#world_soccer)* - in which an agent *independently learns* to perform a given task by trial and error. Each of them is a different way of connecting agents, perception and rewards, and together they cover the patterns most tasks are built from.


Every world comes with a neural network already trained in a certain environment, so you can observe the agents perform their task from the very first launch. The demo also ships with a complete trainer, so you can train any of them from scratch and watch a policy form as it goes - all backed by the physical accuracy, visual fidelity and scalability the Engine brings to whatever you build on it.


## Features


- Four scenes with pre-trained models for different agent interactions: agents following randomly generated waypoint routes, a chaser hunting a runner through an obstacle field, a car approximation sticking to a marked line, and two teams playing a ball game
- Autonomous agents that perceive the world through plain numbers, rays or raw images from an onboard camera
- Up to 128 agents learning at once in a grid of parallel training environments
- Headless (no-render) sped-up simulation mode for faster agent training
- Real-time statistics window with per-behavior and per-agent tables, sorting and filtering
- Agent vision, memory and reward targets drawn right in the scene
- Adversarial training of opposing agents and teams that learn from each other
- Agents that remember the last known position of a target once visual contact is lost, and head for it while the memory lasts
- Switching between a trained neural network, a live trainer and scripted control
- Your own trained model loaded into the scene as an *ONNX* file
- *PPO* and *SAC* reinforcement learning algorithms with configurable hyperparameters
- Training progress in *TensorBoard*, with model checkpoints written at a configurable interval
- An open *gRPC* protocol between the Engine and the trainer, allowing the bundled *Stable-Baselines3* trainer to be replaced with another one
- Repeatable runs - randomly generated routes, layouts and starting positions reproduced exactly on every run started from the same seed
- Support for *curriculum* parameters a trainer can send during a run to adjust the task difficulty
- World selection startup menu, and a switching UI available in every scene


## Requirements


The demo runs out of the box: the C++ dependencies, *gRPC* for the trainer connection and *ONNX Runtime* for inference, are bundled with it. The *[training mode](#run_train)* additionally needs **Python 3.10, 3.11** or **3.12** with an environment prepared for the trainer - *[Stable-Baselines3](https://github.com/DLR-RM/stable-baselines3)*, *[PyTorch](https://github.com/pytorch/pytorch)* and the rest are installed into it.


## Key Concepts


The demo is built around a few core concepts:


### Environment


A **training area** built in *UnigineEditor*, where the learning takes place. It includes the *[agent](#concept_agent)* with the node it is attached to, its sensors and everything around them. Whatever the agent *[does](#concept_action)* affects this area, and whatever it *[perceives](#concept_observation)* comes from it.


Each world holds many copies of the same environment, placed side by side in a grid. Every copy has its own agent running its own attempt, with its own layout, *[rewards](#concept_reward)* and *[episode](#concept_episode)* - so none of them interferes with the others.


### Agent


The central component of the demo: placed on a node, it defines the task that node is meant for, such as driving a certain route or chasing a specified target. Everything else is defined relative to it - its code sets the *[actions](#concept_action)* it can take, the *[rewards](#concept_reward)* it earns and the conditions that end an *[episode](#concept_episode)*, as well as the part of the *[observation](#concept_observation)* the agent reads by itself.


### Behavior


A group of *[agents](#concept_agent)* learning the same skill, defined by one *[brain](#concept_brain)* they all share. Thus the more *[environments](#concept_environment)* a world holds, the faster the brain learns: dozens of agents attempt the same task in parallel, and every one of them teaches the same brain.


A world can hold several behaviors at once, each learning its own skill, and even train them against each other. The demo also lets you implement scenarios where **one behavior keeps to its script while another learns against it**: in the Editor, set the *Policy* parameter of the behavior's *BehaviorConfig* component to *HEURISTIC*, and the whole group keeps running on its script while the rest of the scene trains. This way you can focus on one behavior at a time - in the [chase world](#world_chase), for example, the runner stays on its script while the chaser learns to catch it. A trainer has to be [started deliberately](#run_train), as the normal launch has none.


### Brain


The **intelligence** behind the agent, choosing the *[action](#concept_action)* it takes next. Three types are available, and any *[agent](#concept_agent)* can use any of them without changes to its code:


- a **script**, also called a **heuristic policy** - regular C++ code that decides what to do, used when no other option is available
- the **trainer** - a bundled *Python* script built on *Stable-Baselines3* that teaches the agent by trial and error: it returns *[actions](#concept_action)* and adjusts its neural network as the *[rewards](#concept_reward)* come in. It talks to the Engine over an open *[gRPC](https://grpc.io/)* protocol, so it can be replaced with a trainer of your own. Every agent's *[observation](#concept_observation)* goes out over that channel, and the *[action](#concept_action)* comes back the same way. This is the only option that changes as it runs - the other two always answer the same way
- a **trained model** - a neural network exported to *ONNX* after completing the training process and executed by the Engine itself, with no trainer involved. The demo uses this option by default


> **Notice:** The agent takes whichever **brain** is available in that order: a **trainer** if one is connected, otherwise a **trained model**, then the **script**.


### Observation


The information the *[agent](#concept_agent)* receives before each decision. Part of it is values the agent reads by itself - the direction to its target, its own speed, its progress along the route. The rest comes from **sensors** attached to it: a fan of rays sweeping the surroundings and measuring the distance to what they hit, or a camera capturing the scene as an image.


The agent has no other source of information about the scene: what is not included in the observation cannot affect its decisions.


### Action


What the *[agent](#concept_agent)* does in response once the *[observation](#concept_observation)* is made. Actions are either **continuous**, changing smoothly within a range, or **discrete**, picking one option from a fixed set. The agents of the *[Route Follow](#world_route)*, *[Chase](#world_chase)* and *[Line Follow](#world_line)* worlds use continuous actions - either thrust along the X/Y axes, or throttle and steering. The *[Soccer](#world_soccer)* players use discrete ones, choosing how to drive, turn and strafe from a few fixed options each.


### Reward


The point the whole **reinforcement** system is built upon - a number that scores the result of an *[action](#concept_action)*: a small reward for moving in the right direction, a large one for completing the task, a penalty for failing it. This is the only learning signal the *[agent](#concept_agent)* receives, which is why rewards require careful design. The agent does not understand the purpose of the task, only the score - so if a shortcut scores higher than the expected solution, the agent will take it every time.


### Decision Loop


Decision Loop is the cycle that repeats throughout an *[episode](#concept_episode)*: an *[observation](#concept_observation)* comes in, the *[brain](#concept_brain)* decides, the *[action](#concept_action)* is applied, and the outcome is scored with a *[reward](#concept_reward)*.


A new decision is taken every few physics ticks. Between them the agent repeats its last action, which keeps the movement smooth. Since the loop depends on ticks rather than on seconds, you can change the [simulation speed](#time_scale) to train the agents at the desired pace.


Runs are repeatable: routes, obstacles and starting positions are generated from a single starting number, unpredictable to the agent but identical on every run started from that number.


### Episode


One complete attempt at the task, from the starting state to an outcome: the route is completed, the cube falls off the platform, the runner is caught, or the time limit is reached. An episode is counted in the **steps** the agent takes and ends once it runs out of them even if nothing else has happened. The environment is then reset and the next attempt begins.


The number of episodes the agent needs to learn depends on the task - the simplest of them are trained within minutes, while more complex ones can take thousands of attempts.


![](ml_concepts.png)

*Each agent runs its own decision loop in its own environment, and all the agents of a behavior share one brain. The brain decides what every agent does next. A trainer brain also receives their observations and scores, and adjusts its network accordingly, while a scripted one only issues decisions*


## Running the Demo


On startup the demo opens a menu listing the four worlds:


- *[Route Follow](#world_route)* - an agent learning to follow a waypoint route
- *[Chase](#world_chase)* - a chaser and a runner trained against each other
- *[Line Follow](#world_line)* - a car moving along a marked line using a camera
- *[Soccer](#world_soccer)* - two teams learning to play a ball game against each other


![](ml_menu.png)


Click a world to select it and run in the *[default mode](#run_default)*, start the learning process *[with a trainer](#run_train)*, or use a pre-trained *[custom model](#run_onnx)* of your own.


Use the world navigation UI to switch between the worlds, or return to the menu with *Back to Main Menu*.


### Demo Worlds


The prototypes below are built entirely from the same components you can utilize as a starting point in your own project: train the agents on the scenario you imagine, and integrate the result into your application.


Every world is a separate task with its own *[agents](#concept_agent)*, *[rewards](#concept_reward)* and a *[pre-trained model](#brain_trained)*.


What each agent *[perceives](#concept_observation)* and *[does](#concept_action)* is *[drawn](#show_data)* next to it in the scene, together with the *[reward](#concept_reward)* it has collected so far - *green* while the total is positive, *red* once it is not. Enable the *[Agent table](#show_table)* option in the *Parameters* section to examine the same values as numbers, per behavior and per agent.


#### Route Following World


![](ml_route.gif)


This world contains 32 environments, and an *[agent](#concept_agent)* (a cube) that drives a route of waypoints in each of them. The cube earns a small *[reward](#concept_reward)* for every meter it advances towards the current waypoint, a larger one for reaching it and another for completing the whole route, and it is penalized for falling off the platform. All the cubes belong to one *[behavior](#concept_behavior)*, so they practice the same skill and teach the same *[brain](#concept_brain)*.


The *[observation](#concept_observation)* is five numbers the agent reads: the direction to the current waypoint, its own speed and its progress along the route. After processing the observation, the agent takes the following *[actions](#concept_action)*: the thrust along the X axis and the thrust along the Y axis, which together push the cube in the chosen direction.


The route is not fixed - a new one is generated for every *[episode](#concept_episode)*, with a random number of waypoints placed at random positions within a defined area, so there is no path to memorize and the cube has to learn the skill of moving towards a new target wherever it appears. The waypoints are drawn in different colors for the current target and the ones already visited, along with the path the cube is following, the bounds of its area and the force pushing it. This world trains within minutes, which makes it a good place to start.


#### Chase World


![](ml_chase.gif)


This world contains 32 arenas with a pair of *[agents](#concept_agent)* in each: a **chaser** and a **runner**, trained at the same time with opposite goals. The **chaser** is *[rewarded](#concept_reward)* for reducing the distance, for keeping the runner in view and most of all for catching it, while the **runner** is rewarded for increasing the distance and for staying free. Neither of them trains against a fixed opponent, so both improve together and every improvement makes the task harder for the other. This is **adversarial training**: two *[behaviors](#concept_behavior)*, each with its own *[brain](#concept_brain)*.


The chaser is never told where the runner is - it has to spot the runner with its **ray sensor**. Once the runner slips behind an obstacle, the chaser heads for the last place where it was spotted, and starts searching around if it finds nothing there. The *[observation](#concept_observation)* here has two parts:


1. The numbers the agent reads itself: its own speed, its position in the arena, the time left, whether the opponent is visible right now, and the direction, distance and age of the last sighting
2. The ray sensor: a fan of 32 rays covering the full 360 degrees, reporting the distance to whatever each of them hits and what kind of object it is


The *[actions](#concept_action)* are the same as in the *[Route Following world](#world_route)*. Since the chaser can act only on what it has actually observed, hiding is the runner's best strategy.


The force pushing each agent and the bounds of the arena are visualized along with a yellow line connecting the two agents - bright while they see each other, dim once they do not. The last known position of the opponent is marked with a square the moment sight is lost, colored after the agent that remembers it: **red** for the chaser's memory of the runner, **green** for the runner's memory of the chaser. Both squares fade as the memory grows older, and disappear at once if the agents see each other again.


The obstacles and the starting positions of both agents are scattered anew for every *[episode](#concept_episode)*.


#### Line Following World


![](ml_line.gif)


This world contains a grid of 32 environments with a car approximation in each, driving along a line marked on the floor - the same single-*[behavior](#concept_behavior)* pattern as the *[Route Following world](#world_route)*, learned from vision instead of numbers. Unlike the other three worlds, this *[agent](#concept_agent)* *[perceives](#concept_observation)* the scene as an **image**: a small **64x64 grayscale picture** from a camera mounted on the car and pointed forward and down, and three values it reads itself (its speed, turn rate and the time left). After processing it, the agent takes two *[actions](#concept_action)*: the throttle and the steering. The line is a surface with no physical body, so rays would pass straight through it and report an empty floor. Therefore the camera is the only sensor that perceives the task.


The agent earns a *[reward](#concept_reward)* for every meter it advances along the line, and pays a penalty for every second it spends away from the center of it, so it tries to return to the middle of the line as soon as possible to stop losing the reward. The *[episode](#concept_episode)* ends when the car leaves the line far enough to lose sight of it.


A new loop is generated for every episode, and the car starts at a random point on it, driving clockwise or counterclockwise. The corners vary in sharpness, and the tightest of them require slowing down.


Two vectors show the car's current speed and steering, and a mark beneath it reports how far it has drifted from the middle of the line: **green** while it stays in the lane, **yellow** once it leaves it and **red** when it is about to lose the line altogether.


#### Soccer World


![](ml_soccer.gif)


This world contains 32 fields with four *[agents](#concept_agent)* in each: two **blue** players and two **purple** ones, each team attacking the opposite goal. The teams are two *[behaviors](#concept_behavior)* trained against each other, the same **adversarial** setup as in the *[Chase world](#world_chase)* - except that here each behavior holds two players sharing one *[brain](#concept_brain)*, so they also have to learn to **cooperate** as a team.


The players **kick** the ball by hitting it head-on, so a straight hit sends it flying while a sideways shove only rolls it. The goal of the match is to get the ball into the opponent goal, and scoring early pays more than scoring late. A conceding team loses the full *[reward](#concept_reward)* for a goal whenever it happens, while the scoring one only collects what is left on the clock, so no team can afford to sit on a lead.


A goal alone is far too rare an event to learn from, so the players are also paid along the way - for every meter the **ball** travels towards the opponent goal, and for closing on it themselves, which is what teaches them to chase the ball in the first place. Standing around, on the contrary, costs: the slower a player moves, the more it loses as the episode runs out, so a losing team keeps attacking instead of protecting the score.


The *[observation](#concept_observation)* here has two parts:


1. The numbers the agent reads itself: its own speed forward and sideways, its turn rate and the time left
2. The ray sensor: a fan of 64 rays covering the full 360 degrees, reporting the distance to whatever each of them hits and which of the six kinds of object it is - the ball, either goal, either team's players or a wall


The *[actions](#concept_action)* are **discrete**, unlike the other worlds: three independent choices made at once - drive forward, backward or neither; turn left, right or neither; move sideways to the left, to the right or neither.


The ball is placed near the center of the field at a random spot for every *[episode](#concept_episode)*, and the players start scattered around their kickoff spots facing the goal they attack, so there is no rehearsed opening to memorize. An episode ends as soon as either team scores, or once the players run out of steps without one.


A line runs from every player to the ball, colored after its team along with the force pushing the player and the direction it is turning.


### Running Modes


Every world runs at its own speed, set by the *Time Scale* parameter of its *Session* component and adjustable in the Editor (the *[Line Follow](#world_line)* world always runs at the normal speed, as its agents depend on the rendered image). A connected *[trainer](#run_train)* replaces it with the value from its configuration file.


Any of the worlds can be run in one of the following modes.


#### Watching the Trained Agents


On an ordinary launch, the **agents run on the trained models** included in all the *[worlds of the demo](#worlds)*. Every agent performs the task on its own randomized attempt.


Use the free-flying spectator camera with the standard controls to look around.


#### Training an Agent


In this mode the agents **build the model themselves** through **reinforcement** instead of running a ready-made one. This requires **two processes** running in parallel:


- the **trainer** - decides what the agents do next, adjusts the neural network to make the actions that bring more reward more likely, and saves the result along the way
- the **demo** - runs the world and reports what the agents did and which rewards they earned for it


The trainer runs on a *Python 3.10*, *3.11* or *3.12* environment. Create it and install the dependencies, running the following from the root folder of the demo:


```bash
py -3.12 -m venv .venv                  # Linux: python3.12 -m venv .venv
.venv\Scripts\activate                  # Linux: source .venv/bin/activate
pip install -r trainer/requirements.txt
```


Keep the environment activated in the terminal you start the trainer from. The installation is only done once, so later you will only have to activate it with `.venv\Scripts\activate` (`source .venv/bin/activate` on Linux) every time before running the trainer.


The demo connects to the trainer, so the trainer has to be started first:


1. Run `train.py`. ```bash python trainer/train.py ``` The trainer prints the port it is listening on - 5004 by default - and waits for the demo to connect. The port, the behaviors to train, the algorithm and its parameters are all defined in `trainer/config.yaml`.
2. Run the demo with the following *[startup arguments](../../sdk/projects/index_cpp.md#customize_run)*: ```bash --trainer-port 5004 ``` ![](mlc_guide/mlc_run_train.png) The demo will connect to the trainer and report which behaviors the scene contains, and the trainer will create a model for each of them.


The connection status is reported in the *[statistics window](#stats)*.


> **Notice:** If the demo is started before the trainer, it runs in the *[default mode](#run_default)* with the *[pre-trained models](#brain_trained)*.


The number that tells you whether the learning is progressing is the average *[reward](#concept_reward)* an agent collects per *[episode](#concept_episode)*. It should climb as the agents get better at the task, while a long flat stretch means they have stopped learning anything new. The *[statistics window](#stats)* shows it per behavior, and the trainer prints the same value in its console.


To see the result as a curve, open the `results/tb` folder of the demo in *TensorBoard* - a separate tool installed with the trainer dependencies:


```bash
cd <path_to_the_demo>
python -m tensorboard.main --logdir results/tb
```


The command prints an address to open in a browser. It picks up every run stored in that folder and draws them on the same chart, one line per behavior, so they can be compared.


Training stops when the agents reach the number of steps set in the configuration file, or as soon as you close the trainer or the demo. Whichever way it ends, the trainer saves the model and exports it to *ONNX*, ready to be *[used in the scene](#run_onnx)*. It also writes a checkpoint to the `results` folder every 100,000 steps of one agent by default (i.e. 1,600,000 steps of a run with 16 agents) - set *checkpoint_freq* in `trainer/config.yaml` to change the interval.


##### Headless Mode


To **boost the training speed**, run the demo in the headless mode: the scene is not rendered at all, so the simulation is limited only by the processor. Use the following startup arguments:


```bash
--trainer-port 5004 -video_app null
```


> **Notice:** The headless mode is not available for agents that perceive the world through a camera, as in the *[Line Follow](#world_line)* world.


#### Running a Trained Model


A model you have trained yourself can replace the one included in the demo. Every training run writes one `.onnx` file per behavior into `results/<run_name>`. To use the saved model:


1. Copy the target `.onnx` file into the demo's `data/onnx` folder.
2. Open the world in *UnigineEditor* and point the *ONNX Model* parameter of the behavior's *BehaviorConfig* component at the new file.


Started without a trainer, the demo will run the agents on that model.


A model only works with the *[observations](#concept_observation)* and *[actions](#concept_action)* it was trained on. Adding a sensor or changing either of them means the model has to be retrained. The environment is free to change: the routes, the layout and the starting positions can all be different, as the agent perceives them relative to itself.


## Interface


This chapter covers the data the demo reports on the screen and the ways to control it.


![](ml_interface.png)


### Mode Caption


The caption at the top of the screen names what is driving the agents right now:


- *TRAINING* - a *[trainer](#brain_trainer)* is connected
- *ONNX* - the agents run on a *[trained model](#brain_trained)*
- *HEURISTIC* - the agents follow *[a script](#brain_script)*
- *ONNX + HEURISTIC* - some of the behaviors run on a model and the rest on a script


The line below lists every *[behavior](#concept_behavior)* with the source of its actions, so a world running a mix of the two shows both.


### World Description Window


This window describes the world you are in and holds the switches for everything the demo draws on screen in its *Parameters* section.


| Option | Description |
|---|---|
| *Agent overlay* | The data drawn around every *[agent](#concept_agent)*: its *[reward](#concept_reward)*, its action vectors, the ray fans of its sensors and the debug geometry of the world. The same switch as *F2* |
| *Hide labels behind objects* | Hide the reward label of an agent while something stands between the agent and the camera > **Notice:** The check runs per agent every frame, so the more agents a world holds, the higher the cost |
| *Agent table* | The *[statistics window](#stats)* |
| *Mode caption* | The *[caption](#banner)* naming what drives the agents |


### Statistics Window


The statistics window reports the state of the run in a status line, a table of behaviors and a table of agents. Switch it on with the *Agent table* option of the *[world description window](#world_description)*.


[![](ml_hud.png)](ml_hud.png)


The status line describes the run as a whole: the number of ticks passed, the number of ticks per second, whether a trainer is connected and the current simulation speed.


The upper table has a row per behavior:


| Column | Description |
|---|---|
| *behavior* | The name of the behavior and its team. All agents with this name are driven by the same brain |
| *agents* | The number of agents that have this behavior |
| *obs* | How many numbers (*[observations](#concept_observation)*) the agent receives before each decision |
| *actions* | The kind and number of *[actions](#concept_action)* available to the agent |
| *brain* | What actually drives the behavior at the moment: *[a script](#brain_script)*, a *[trained model](#brain_trained)* or a *[connected trainer](#brain_trainer)* |
| *episodes*, *return* | The number of *[episodes](#concept_episode)* finished and the average *[reward](#concept_reward)* collected in the last 50 of them |


The lower table has a row per agent:


| Column | Description |
|---|---|
| *id*, *node*, *behavior* | The *[agent](#concept_agent)*, the node it is placed on and the behavior it has |
| *ep* | How many *[episodes](#concept_episode)* the agent has finished |
| *step* | The steps count for the current *[episode](#concept_episode)* |
| *reward*, *action* | The *[reward](#concept_reward)* collected in the current episode and the *[actions](#concept_action)* taken last |


By default the agents are listed in the order they were registered. The list can also be sorted by reward, step or episode, and filtered to show the agents of a single behavior only (e.g. *chaser* or *runner*).


## Third-Party Notices


This section contains licensing information about third-party components used in *Unigine ML Integration*.


### gRPC


*gRPC* library version 1.60.0, which is available under the [Apache License 2.0](https://github.com/grpc/grpc/blob/master/LICENSE).


<details>
<summary>Licensing information | Close</summary>

Apache License v2.0


This license can also be found at this permalink: [https://github.com/grpc/grpc/blob/master/LICENSE](https://github.com/grpc/grpc/blob/master/LICENSE)


Apache License


Version 2.0, January 2004


[http://www.apache.org/licenses/](http://www.apache.org/licenses/)


TERMS AND CONDITIONS FOR USE, REPRODUCTION, AND DISTRIBUTION


1. Definitions.


'License' shall mean the terms and conditions for use, reproduction, and distribution as defined by Sections 1 through 9 of this document.
'Licensor' shall mean the copyright owner or entity authorized by the copyright owner that is granting the License.
'Legal Entity' shall mean the union of the acting entity and all other entities that control, are controlled by, or are under common control with that entity. For the purposes of this definition, 'control' means (i) the power, direct or indirect, to cause the direction or management of such entity, whether by contract or otherwise, or (ii) ownership of fifty percent (50%) or more of the outstanding shares, or (iii) beneficial ownership of such entity.
'You' (or 'Your') shall mean an individual or Legal Entity exercising permissions granted by this License.
'Source' form shall mean the preferred form for making modifications, including but not limited to software source code, documentation source, and configuration files.
'Object' form shall mean any form resulting from mechanical transformation or translation of a Source form, including but not limited to compiled object code, generated documentation, and conversions to other media types.
'Work' shall mean the work of authorship, whether in Source or Object form, made available under the License, as indicated by a copyright notice that is included in or attached to the work (an example is provided in the Appendix below).
'Derivative Works' shall mean any work, whether in Source or Object form, that is based on (or derived from) the Work and for which the editorial revisions, annotations, elaborations, or other modifications represent, as a whole, an original work of authorship. For the purposes of this License, Derivative Works shall not include works that remain separable from, or merely link (or bind by name) to the interfaces of, the Work and Derivative Works thereof.
'Contribution' shall mean any work of authorship, including the original version of the Work and any modifications or additions to that Work or Derivative Works thereof, that is intentionally submitted to Licensor for inclusion in the Work by the copyright owner or by an individual or Legal Entity authorized to submit on behalf of the copyright owner. For the purposes of this definition, 'submitted' means any form of electronic, verbal, or written communication sent to the Licensor or its representatives, including but not limited to communication on electronic mailing lists, source code control systems, and issue tracking systems that are managed by, or on behalf of, the Licensor for the purpose of discussing and improving the Work, but excluding communication that is conspicuously marked or otherwise designated in writing by the copyright owner as 'Not a Contribution.'
'Contributor' shall mean Licensor and any individual or Legal Entity on behalf of whom a Contribution has been received by Licensor and subsequently incorporated within the Work.


2. Grant of Copyright License. Subject to the terms and conditions of this License, each Contributor hereby grants to You a perpetual, worldwide, non-exclusive, no-charge, royalty-free, irrevocable copyright license to reproduce, prepare Derivative Works of, publicly display, publicly perform, sublicense, and distribute the Work and such Derivative Works in Source or Object form.


3. Grant of Patent License. Subject to the terms and conditions of this License, each Contributor hereby grants to You a perpetual, worldwide, non-exclusive, no-charge, royalty-free, irrevocable (except as stated in this section) patent license to make, have made, use, offer to sell, sell, import, and otherwise transfer the Work, where such license applies only to those patent claims licensable by such Contributor that are necessarily infringed by their Contribution(s) alone or by combination of their Contribution(s) with the Work to which such Contribution(s) was submitted. If You institute patent litigation against any entity (including a cross-claim or counterclaim in a lawsuit) alleging that the Work or a Contribution incorporated within the Work constitutes direct or contributory patent infringement, then any patent licenses granted to You under this License for that Work shall terminate as of the date such litigation is filed.


4. Redistribution. You may reproduce and distribute copies of the Work or Derivative Works thereof in any medium, with or without modifications, and in Source or Object form, provided that You meet the following conditions:

- (a) You must give any other recipients of the Work or Derivative Works a copy of this License; and
- (b) You must cause any modified files to carry prominent notices stating that You changed the files; and
- (c) You must retain, in the Source form of any Derivative Works that You distribute, all copyright, patent, trademark, and attribution notices from the Source form of the Work, excluding those notices that do not pertain to any part of the Derivative Works; and
- (d) If the Work includes a 'NOTICE' text file as part of its distribution, then any Derivative Works that You distribute must include a readable copy of the attribution notices contained within such NOTICE file, excluding those notices that do not pertain to any part of the Derivative Works, in at least one of the following places: within a NOTICE text file distributed as part of the Derivative Works; within the Source form or documentation, if provided along with the Derivative Works; or, within a display generated by the Derivative Works, if and wherever such third-party notices normally appear. The contents of the NOTICE file are for informational purposes only and do not modify the License. You may add Your own attribution notices within Derivative Works that You distribute, alongside or as an addendum to the NOTICE text from the Work, provided that such additional attribution notices cannot be construed as modifying the License.

 You may add Your own copyright statement to Your modifications and may provide additional or different license terms and conditions for use, reproduction, or distribution of Your modifications, or for any such Derivative Works as a whole, provided Your use, reproduction, and distribution of the Work otherwise complies with the conditions stated in this License.
5. Submission of Contributions. Unless You explicitly state otherwise, any Contribution intentionally submitted for inclusion in the Work by You to the Licensor shall be under the terms and conditions of this License, without any additional terms or conditions. Notwithstanding the above, nothing herein shall supersede or modify the terms of any separate license agreement you may have executed with Licensor regarding such Contributions.


6. Trademarks. This License does not grant permission to use the trade names, trademarks, service marks, or product names of the Licensor, except as required for reasonable and customary use in describing the origin of the Work and reproducing the content of the NOTICE file.


7. Disclaimer of Warranty. Unless required by applicable law or agreed to in writing, Licensor provides the Work (and each Contributor provides its Contributions) on an 'AS IS' BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied, including, without limitation, any warranties or conditions of TITLE, NON-INFRINGEMENT, MERCHANTABILITY, or FITNESS FOR A PARTICULAR PURPOSE. You are solely responsible for determining the appropriateness of using or redistributing the Work and assume any risks associated with Your exercise of permissions under this License.


8. Limitation of Liability. In no event and under no legal theory, whether in tort (including negligence), contract, or otherwise, unless required by applicable law (such as deliberate and grossly negligent acts) or agreed to in writing, shall any Contributor be liable to You for damages, including any direct, indirect, special, incidental, or consequential damages of any character arising as a result of this License or out of the use or inability to use the Work (including but not limited to damages for loss of goodwill, work stoppage, computer failure or malfunction, or any and all other commercial damages or losses), even if such Contributor has been advised of the possibility of such damages.


9. Accepting Warranty or Additional Liability. While redistributing the Work or Derivative Works thereof, You may choose to offer, and charge a fee for, acceptance of support, warranty, indemnity, or other liability obligations and/or rights consistent with this License. However, in accepting such obligations, You may act only on Your own behalf and on Your sole responsibility, not on behalf of any other Contributor, and only if You agree to indemnify, defend, and hold each Contributor harmless for any liability incurred by, or claims asserted against, such Contributor by reason of your accepting any such warranty or additional liability.


END OF TERMS AND CONDITIONS


APPENDIX: How to apply the Apache License to your work.


To apply the Apache License to your work, attach the following boilerplate notice, with the fields enclosed by brackets '[]' replaced with your own identifying information. (Don�t include the brackets!) The text should be enclosed in the appropriate comment syntax for the file format. We also recommend that a file or class name and description of purpose be included on the same 'printed page' as the copyright notice for easier identification within third-party archives.


Copyright [yyyy] [name of copyright owner]


Licensed under the Apache License, Version 2.0 (the 'License'); you may not use this file except in compliance with the License. You may obtain a copy of the License at [http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)


Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an 'AS IS' BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.

</details>


### ONNX Runtime


*ONNX Runtime* library version 1.23.2, which is copyright (c) Microsoft Corporation and is available under the terms of the [MIT License](https://github.com/microsoft/onnxruntime/blob/main/LICENSE).


<details>
<summary>Licensing information | Close</summary>

MIT License


Copyright (c) Microsoft Corporation


Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the 'Software'), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:


The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.


THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

</details>


## Accessing Demo Source Code

You can study and modify the source code of this demo to create your own projects. To access the source code do the following:

1. Find the **Unigine ML Integration** demo in the *Demos* section and click **[Install](/sdk/#samples)** (if you haven't installed it yet).
2. After successful installation the demo will appear in the *Installed* section, and you can click **Copy as Project** to create a project based on this demo. ![](../../sdk/demos/copy_as_project_gen.png)
3. In the **Create New Project** window, that opens, enter the name for your new project in the corresponding field and click **Create New Project**. ![](../../sdk/projects/create_project_cpp.png)
4. Now you can click **Open Code IDE** to check and modify source code in your default IDE, or click **Open Editor** to open the project in the [UnigineEditor](/editor2/). ![](../../sdk/projects/edit_code.png)

## Articles in This Section

- [Building Your Own ML Agent](../../sdk/demos/ml_agents_customization.md)

- [Unigine ML Integration API](../../sdk/demos/ml_agents_api.md)
