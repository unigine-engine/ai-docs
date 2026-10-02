# SoccerAgent Class

**Inherits from:** MLAgents::Agent


SoccerAgent is the player of the Soccer world: two teams of two, trained against each other in the same run. The *Team* parameter decides which goal a player attacks, and the two teams are separate behaviors with separate policies.


This is the demo's example of a team task with a rare outcome. A goal on its own is far too infrequent to learn from on a demo budget, so the reward pays the whole team per meter the ball moves towards the opponent goal - that shaping term is what makes the task learnable at all, and it is deliberately kept small enough that driving the ball the length of the pitch pays less than scoring does.


A player sees the pitch through a **[RaySensor](../../../../api/modules/ml_agents/class.raysensor.md)** covering the full 360 degrees, and chooses from three discrete actions: drive, turn and strafe. It kicks by driving into the ball nose first, so there is no kick action to learn separately - and charging the kick only while the forward action is held is what separates shoving the ball sideways from shooting and passing.


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Team | *Switch* | BLUE | *BLUE* defends -Y and attacks +Y, *PURPLE* the other way round. The two teams are separate behaviors with separate policies, trained against each other in the same exchange |
| Move Force | *Float* | 48.0 | Thrust (N) behind one forward or sideways step. This, rather than *Max Speed*, is what sets how fast the players actually run: the body settles where thrust balances damping |
| Max Speed | *Float* | 9.0 | Top speed cap (m/s). Keep it above what *Move Force* actually reaches, so it stays a safety net rather than the thing that limits the players. The forward and sideways velocity observations are normalized by it |
| Strafe Scale | *Float* | 0.3 | Sideways thrust as a fraction of forward thrust. Deliberately weak: a player that can strafe as fast as it runs never learns to turn, and ends up crabbing across the pitch with the ball behind it |
| Turn Torque | *Float* | 10.0 | Torque (N*m) behind a full-lock turn. Applied as a torque rather than assigned as an angular velocity, so the body spins up and down over a few ticks instead of snapping between rates |
| Max Turn Rate | *Float* | 180.0 | Yaw rate cap (degrees per second), reached by holding a turn rather than instantly |
| Kick Speed | *Float* | 13.0 | Velocity (m/s) handed to the ball when a player drives into it nose first. Charged only while the forward action is held, so shoving the ball sideways is not a kick - that distinction is what turns bumping into shooting and passing |
| Kick Cooldown | *Float* | 0.25 | Seconds before the same player may kick again. Any touch counts, not just the frame the contact begins, so a pair leaning on the ball cannot inject *Kick Speed* on every physics tick |
| Goal Reward | *Float* | 3.0 | Terminal reward for a goal. The conceding team loses all of it; the scoring team gains only the share left on the clock, so a goal in the first seconds is worth full price and one on the whistle almost nothing. That is where the pressure to finish the match lives |
| Ball Progress Reward | *Float* | 0.1 | Paid to the whole team per meter the ball moves towards the opponent goal. This is the signal that makes the task learnable on a demo budget. Keep it low enough that driving the ball the length of the pitch pays less than scoring does |
| Approach Reward | *Float* | 0.05 | Paid per meter this agent closes on the ball, and charged back per meter it drifts away. Small on purpose: it teaches the first move and then has to stop mattering, or both players just huddle around the ball |
| Approach Radius | *Float* | 3.0 | Distance to the ball (m) inside which *Approach Reward* stops being paid or charged. Without it, backing off always costs, so two players who have shoved the ball into a wall are both paid to keep leaning on it |
| Time Penalty | *Float* | 1.0 | Total charged across a whole episode, spread evenly over its decisions, which makes standing still lose. A total rather than a per-step rate on purpose: a rate silently rescales when *Max Episode Steps* or *Decision Interval* change. Ignored when *Max Episode Steps* is 0 |
| Spawn Spread | *Float* | 3.0 | How far (m) a player is dropped from its authored kickoff spot, in a random direction and clamped to stay on the pitch. Without it every episode opens from the same four positions and the policy learns one rehearsed opening |
| Spawn Yaw Jitter | *Float* | 10.0 | Random yaw (+/- degrees) added on top of facing the goal under attack. The authored rotation is ignored on purpose, so both teams always start looking the right way |
| Debug Draw | *Toggle* | 1 | Include this agent in the session 3D overlay: the line to the ball, the drive force it is applying and which way it is turning |
| Debug Force Scale | *Float* | 0.04 | Meters of arrow per newton of drive force |


### See Also


- **[MLAgents::Agent](../../../../api/modules/ml_agents/class.agent.md)**
- **[SoccerField](../../../../api/modules/ml_agents/worlds/class.soccerfield.md)**
- **[MLAgents::BehaviorConfig](../../../../api/modules/ml_agents/class.behaviorconfig.md)**


## SoccerAgent Class

---

## protected virtual void configure ( )

Declares three discrete branches of three choices each - drive, turn and strafe, every one of them backwards, still or forwards - and finds the pitch the player plays on.
### Arguments

## protected virtual void onEpisodeBegin ( )

Puts the player near its kickoff spot with a random offset and yaw, facing the goal it attacks.
## protected virtual void observe ( )

Writes the player's own state: its forward and sideways speed, its yaw rate, and how much of the episode is left. Everything about the ball, the goals and the other players reaches the policy through the ray sensor instead, so one policy serves both ends of the pitch.
### Arguments

## protected virtual void act ( )

Drives and turns the player, kicks the ball when it is driven into nose first, and pays out the ball progress, approach and time terms.
### Arguments

## protected virtual void heuristic ( )

Runs at the ball and pushes it towards the opponent goal, which keeps a match going without trained models.
### Arguments

## protected virtual void onDebugDraw ( )

Draws the line to the ball, the applied drive force and the direction the player is turning.
