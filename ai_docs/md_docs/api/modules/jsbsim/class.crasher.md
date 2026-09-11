# JSBSim::Crasher Component

**Inherits from:** ComponentBase


Crasher is a component that handles aircraft crash detection and post-crash physics. When an aircraft crashes (e.g., hard landing, collision), this component takes over control from the flight model and applies Unigine physics to simulate the wreckage behavior.


The component monitors collision shapes attached to the aircraft. When a contact exceeds the maximum depth threshold, the aircraft is considered crashed. After a crash, the component transfers the current velocity to the physics body, enables ragdoll-style physics simulation, and detects water contact for water crashes.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Settings Group |  |  |
| Max Contact Depth | *Float* | Maximum allowed contact penetration before triggering a crash (*default: 0.3*). |


### See Also


- **[JSBSim::FDMJSBSim](../../../api/modules/jsbsim/class.fdmjsbsim.md)**


## Crasher Class

---

## void push ( )

Initiates the crash simulation with the specified velocities.
### Arguments

## void reset ( )

Resets the crasher state, allowing the aircraft to fly again.
## isCrashed ( )

Returns whether the aircraft is in a crashed state.
### Return value

True if the aircraft has crashed.
