# LineFollowerAgent Class

**Inherits from:** MLAgents::Agent


LineFollowerAgent is the agent of the Line Follow world: a car that has to stay on a painted line and keep driving along it. It is the demo's example of a camera-only task - the line has no physical body, so rays would pass straight through it and a **[CameraSensor](../../../../api/modules/ml_agents/class.camerasensor.md)** is the only sensor that perceives it. The policy steers from raw pixels, with no numbers describing where the line is.


The reward has two halves working against each other. Progress along the track pays per meter, so standing still earns nothing; drifting off the line costs per second, so a lost car cannot dodge the charge by crawling. Between the two, the car learns to steer back towards the paint.


The actions are two continuous values, throttle and steering. The car never stops completely: *Min Speed Fraction* keeps it rolling even at zero throttle, which removes "stand still and never leave the line" as a solution.


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Max Speed | *Float* | 2.5 | Top forward speed (m/s) |
| Min Speed Fraction | *Float* | 0.25 | Fraction of *Max Speed* the car keeps even at zero throttle. Stops the policy from finding "stand still and never leave the line" as a solution |
| Turn Rate | *Float* | 150.0 | Steering authority in degrees per second at full lock |
| Progress Reward | *Float* | 1.0 | Paid per meter advanced along the track. The main signal: it pays for driving, not for sitting on the line |
| Lane Half Width | *Float* | 0.35 | The offset (m) at which the reward crosses zero: on the line the car earns *Progress Reward* per meter, at this offset a car at full speed breaks even, and past it every second costs more than driving pays. Make it a bit wider than the painted line |
| Lateral Penalty | *Float* | 1.0 | Steepness of that slope, in units of the full-speed progress rate reached at one *Lane Half Width*. Charged per second rather than per meter driven, so a lost car cannot dodge it by crawling |
| Off Track Distance | *Float* | 1.5 | Leaving the center line by more than this (m) ends the episode. This is the "lost for good" radius rather than the width of the lane: by here the line is out of the camera frame and there is nothing left to learn from |
| Off Track Penalty | *Float* | 1.0 | Terminal penalty for getting lost, in the same units as the progress reward. Deliberately small: the real cost of ending the episode is the reward the car no longer collects |
| Debug Draw | *Toggle* | 1 | Include this car in the session 3D overlay: how far off the line it is, and the throttle and steering it is holding |
| Debug Vector Scale | *Float* | 1.0 | Length (m) of the throttle arrow at *Max Speed*, and of the steering arrow at full lock |


### See Also


- **[MLAgents::Agent](../../../../api/modules/ml_agents/class.agent.md)**
- **[LineTrack](../../../../api/modules/ml_agents/worlds/class.linetrack.md)**
- **[MLAgents::CameraSensor](../../../../api/modules/ml_agents/class.camerasensor.md)**


## LineFollowerAgent Class

---

## protected virtual void configure ( )

Declares two continuous actions: throttle and steering.
### Arguments

## protected virtual void onEpisodeBegin ( )

Puts the car back on the start of the track and clears the progress accumulated over the previous episode.
## protected virtual void observe ( )

Writes the car's own state: its normalized forward speed, its yaw rate, and how much of the episode is left. What the line looks like comes from the camera sensor instead, as a visual observation.
### Arguments

## protected virtual void act ( )

Applies the throttle and the steering, pays the progress reward for the distance covered along the track, charges the lateral penalty for the offset from it, and ends the episode once the car is further off than *Off Track Distance*.
### Arguments

## protected virtual void heuristic ( )

Drives the car along the track using the geometry directly, which is the reference the trained policy has to reach while seeing only the camera.
### Arguments

## protected virtual void onDebugDraw ( )

Draws the offset from the line and the applied throttle and steering.
