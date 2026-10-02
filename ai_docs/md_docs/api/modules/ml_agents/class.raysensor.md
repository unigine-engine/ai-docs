# MLAgents::RaySensor Class

**Inherits from:** Sensor


RaySensor casts a fan of rays and reports what they hit. It is the cheapest way to give an agent a sense of its surroundings, and the one to reach for before a camera: a handful of rays costs a few physics intersections per decision, where a visual observation costs a rendered frame.


The fan is centered on the node's +Y axis and spread evenly across *Fan Angle*. Each ray contributes a one-hot block over *Detectable Tags*, a flag saying whether it hit anything at all, and the hit distance as a fraction of *Ray Length* - so the observation size is *Ray Count* * (number of tags + 2).


Tags are matched through the **[Tag](../../../api/modules/common/class.tag.md)** component: put it on every node the sensor is meant to tell apart and set its *Value* to one of the names listed in *Detectable Tags*. The sensor checks the node a ray hits and its parent.


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Ray Count | *Int* | 7 | Number of rays in the fan |
| Fan Angle | *Float* | 90.0 | Total fan spread in degrees, centered on the node's +Y axis |
| Ray Length | *Float* | 10.0 | Ray reach in meters |
| Intersection Mask | *Mask* | physics_intersection | The [bit mask](../../../principles/bit_masking/index.md#intersection_mask) the rays test against, which decides the surfaces they can hit at all |
| Detectable Tags | *String* array |  | **[Tag](../../../api/modules/common/class.tag.md)** values encoded as one-hot per ray, in this order |
| Debug Draw | *Toggle* | 0 | Draw the last ray results with the Visualizer (green for a hit, grey for a miss). Drawn by the owning agent, so the session overlay switch and the agent's own debug draw flag turn these off along with everything else |


### See Also


- **[MLAgents::Sensor](../../../api/modules/ml_agents/class.sensor.md)**
- **[MLAgents::CameraSensor](../../../api/modules/ml_agents/class.camerasensor.md)**
- **[Tag](../../../api/modules/common/class.tag.md)**


## RaySensor Class

---

## virtual getObservationSize ( )

Returns the size of the observation block produced by the ray fan.
### Return value

Number of values the sensor writes: *Ray Count* * (number of detectable tags + 2).
## virtual void write ( )

Casts the fan and writes what it found: per ray, the one-hot encoding of the tag carried by the node that was hit, a hit flag, and the hit distance as a fraction of *Ray Length*.
### Arguments

## virtual void onDebugDraw ( )

Draws the rays of the last cast when *Debug Draw* is on.
