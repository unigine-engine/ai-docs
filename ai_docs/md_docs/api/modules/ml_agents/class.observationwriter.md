# MLAgents::ObservationWriter Class


ObservationWriter collects the values that make up an observation. It is handed to **[Agent::observe()](../../../api/modules/ml_agents/class.agent.md)** and to **[Sensor::write()](../../../api/modules/ml_agents/class.sensor.md)**, and it takes the engine math types directly, so a vector or a quaternion goes in as one call rather than component by component.


The same code runs twice for two different purposes: once at initialization against a probe writer that counts values without storing them, to measure the observation size, and then once per decision to fill the vector for real. This is why an observation has to write the same number of values in the same order every time - a branch that writes three values on one tick and four on the next breaks the layout the model was trained on.


```cpp
void MyAgent::observe(MLAgents::ObservationWriter &obs)
{
    obs.write(velocity / max_speed);        // vec3, three values
    obs.write(distance_to_target);          // one value
    obs.write(target_is_visible);           // bool, written as 0 or 1
    obs.writeOneHot(current_state, 4);      // four values
}

```


> **Notice:** Normalize what you write. A policy learns much faster from values of a comparable scale, so divide velocities by the top speed and distances by the reach of the task instead of writing raw meters.


### See Also


- **[MLAgents::Agent](../../../api/modules/ml_agents/class.agent.md)**
- **[MLAgents::Sensor](../../../api/modules/ml_agents/class.sensor.md)**
- **[MLAgents::ObservationSpec](../../../api/modules/ml_agents/struct.observationspec.md)**


## ObservationWriter Class

---

## void write ( )

Writes one value to the observation.
### Arguments

## void write ( )

Writes a flag as a single value: 1.0 for true, 0.0 for false.
### Arguments

## void write ( )

Writes a two-component vector as two values, in the X, Y order.
### Arguments

## void write ( )

Writes a three-component vector as three values, in the X, Y, Z order.
### Arguments

## void write ( )

Writes a four-component vector as four values, in the X, Y, Z, W order.
### Arguments

## void write ( )

Writes a quaternion as four values, in the X, Y, Z, W order.
### Arguments

## void write ( )

Writes a block of values at once.
### Arguments

## void writeOneHot ( )

Writes a one-hot block: **range** values, all zero except the one at **index**. This is how a category is handed to a policy - writing the index itself as a number would tell it that category 3 is somehow greater than category 1.
### Arguments

## getCount ( )

Returns how many values have been written. The measuring pass uses it to work out the observation size.
### Return value

Number of values written so far.
## isProbe ( )

Returns a value indicating if this writer only counts values instead of storing them. Use it to skip expensive work on the measuring pass - but never to write a different number of values.
### Return value

true on the measuring pass; otherwise, false.
