# LineTrack Class

**Inherits from:** ComponentBase


LineTrack generates the closed loop the Line Follow world is built around: it rolls a new shape on every episode, lays the painted strip along it, and answers where a car is relative to the center line.


The loop is a circle whose radius is modulated by a few harmonics, so it grows corners of varying tightness instead of being one constant turn. That variety is the point: a plain circle is solved by holding one steering angle, and a policy trained on it learns nothing about following a line.


The component goes on the training area node itself, next to **[TrainingArea](../../../../api/modules/ml_agents/class.trainingarea.md)**, and regenerates the track on every reset.


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Radius | *Float* | 6.0 | Mean radius (m) of the loop. Keep the loop plus *Wobble* inside the floor |
| Wobble | *Float* | 0.25 | Total amplitude of the radius harmonics as a fraction of *Radius*, so the loop stays within *Radius* * (1 +- *Wobble*). 0 gives a plain circle, which a policy solves by turning at one constant rate and learns nothing else. It has to stay below 1, or the radius reaches zero and the loop pinches at the center |
| Height | *Float* | 0.02 | How far above the floor the paint sits (m). Just enough to avoid z-fighting |
| Strip Source | *File* |  | Node asset laid along the spline to paint the line. Its mesh sets the painted width. Empty lays no paint, leaving only the reward geometry |
| Forward Axis | *Switch* | Y | Which axis of the source mesh runs along the track. Get this wrong and every copy is laid across the path instead of along it |
| Segment Mode | *Switch* | TILING | How the source is fitted along a segment. *TILING* repeats it, which is what a continuous line wants; *STRETCH* deforms one copy across the whole segment |


### See Also


- **[LineFollowerAgent](../../../../api/modules/ml_agents/worlds/class.linefolloweragent.md)**
- **[MLAgents::TrainingArea](../../../../api/modules/ml_agents/class.trainingarea.md)**


## LineTrack Class

---

## isValid ( )

Returns a value indicating if the track holds enough points to be followed.
### Return value

true if a usable track has been generated; otherwise, false.
## getLength ( )

Returns the total length of the generated loop.
### Return value

Length of the loop in meters.
## project ( )

Projects a world position onto the center line. This is what turns a car position into the two numbers the reward is built from: how far it has driven, and how far off the line it is.
### Arguments

### Return value

true if the position could be projected; otherwise, false.
## getStartPose ( )

Returns where a car starts an episode: a point on the loop, facing the direction of travel.
### Arguments

### Return value

true if a start pose is available; otherwise, false.
