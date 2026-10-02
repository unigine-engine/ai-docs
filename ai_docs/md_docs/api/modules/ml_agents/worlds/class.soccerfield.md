# SoccerField Class

**Inherits from:** ComponentBase


SoccerField is the pitch of the Soccer world: it owns the ball, builds the scoring volume behind each goal line, and reports which team has scored.


It is also where the curriculum of that world takes effect. The goal mouth is the parameter the trainer narrows as the teams learn: a wide goal is scored by accident, a narrow one has to be aimed at, so the task grows harder exactly as fast as the players get better at it.


The component goes on the training area node itself, next to **[TrainingArea](../../../../api/modules/ml_agents/class.trainingarea.md)**, and places the ball anew on every reset.


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Field Size | *Vec2* | 14.0, 20.0 | Pitch extents (m): X is the width across a goal mouth, Y is the distance between the two goals. Blue defends -Y and attacks +Y |
| Goal Width | *Float* | 5.0 | Width (m) of the opening in each end wall. This is the one the curriculum shrinks. Note that it resizes the scoring trigger only - the end walls stay where the scene put them |
| Goal Depth | *Float* | 1.0 | How far (m) behind the goal line the scoring volume extends. Its front face sits exactly on the goal line, so the ball scores the moment it touches the line. It must reach far enough for the ball to get inside before the back of the net stops it, and the component complains at initialization if the geometry makes scoring impossible |
| Kickoff Spread | *Float* | 2.0 | The ball is dropped this far (m) from the center spot in a random direction, so the policy cannot learn one opening move |


### See Also


- **[SoccerAgent](../../../../api/modules/ml_agents/worlds/class.socceragent.md)**
- **[MLAgents::TrainingArea](../../../../api/modules/ml_agents/class.trainingarea.md)**
- **[Session::getEnvParam()](../../../../api/modules/ml_agents/class.session.md)**


## SoccerField Class

---

## getScoringTeam ( )

Returns the team that scored the goal ending the current episode.
### Return value

Team that has scored, or -1 if no goal has been scored in this episode.
## hasBall ( )

Returns a value indicating if the ball node was resolved at initialization.
### Return value

true if the pitch found its ball; otherwise, false.
## getBallBody ( )

Returns the body of the ball, which is what a kick applies its impulse to.
### Return value

Rigid body of the ball.
## getBallPosition ( )

Returns where the ball currently is.
### Return value

World position of the ball.
## getBallVelocity ( )

Returns how the ball is currently moving.
### Return value

Linear velocity of the ball.
## getGoalCentre ( )

Returns the center of the goal the given team defends.
### Arguments

### Return value

World position of the center of that goal.
## getGoalWidth ( )

Returns the goal width actually applied, which is the curriculum value when a trainer is sending one and *Goal Width* otherwise.
### Return value

Width (m) of the goal mouth currently in effect.
## getCentre ( )

Returns the center of the pitch.
### Return value

World position of the center spot.
## getHalfExtent ( )

Returns half the pitch size, which is what a player clamps its spawn position against.
### Return value

Half of the pitch extents (m).
