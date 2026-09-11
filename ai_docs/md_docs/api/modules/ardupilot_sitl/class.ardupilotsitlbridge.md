# ArduPilotSITLBridge Class


ArduPilotSITLBridge connects Unigine's physics simulation to **ArduPilot SITL** (Software In The Loop) through its **JSON FDM** (Flight Dynamics Model) interface. **ArduPilot SITL** runs the real autopilot firmware on the host and expects an external simulator to provide vehicle sensor data and consume the servo (PWM) outputs it produces. This bridge plays the role of that external simulator: Unigine computes the vehicle motion, and **ArduPilot** flies it.


The bridge is a plain owned C++ type, **not** a scene component. The integration code holds a single instance and drives its lifetime explicitly with **init()** and **shutdown()**. Once started, all network traffic is handled on a dedicated internal thread, so the public methods form a small thread-safe exchange of two buffers: the latest servo inputs received from **ArduPilot**, and the latest vehicle sensor state to be sent back.


Communication uses a single bidirectional UDP link (default port 9002):


- **ArduPilot to Unigine:** a binary servo packet carrying 16 PWM channels plus a frame rate and frame counter.
- **Unigine to ArduPilot:** a JSON sensor-state message with timestamp, gyro, body acceleration, position, velocity, and orientation.


The reply rate paces **ArduPilot**'s simulation clock. The network thread targets a fixed 2 kHz reply cadence while the link is active (kept above **ArduPilot**'s gyro rate floor, otherwise arming fails) and idles without pinning a CPU core when no autopilot is connected.


The bridge exchanges data in **ArduPilot** coordinate frames: **NED** for the world and **FRD** (Forward-Right-Down) for the body. Unigine works in **ENU** world and Z-up body frames. Use the free function **arduPilotSensorStateFromUnigine()** (described below) to convert a Unigine-frame snapshot into the frame the bridge expects, instead of converting axes by hand.


Typical per-tick integration:


- At startup, call **init()** with the UDP port (defaults to 9002, matching the SITL launch arguments).
- Each physics tick, build a **[UnigineSensorState](#UnigineSensorState)** from the vehicle node (world position, velocity, plain acceleration, orientation, angular velocity), convert it with **arduPilotSensorStateFromUnigine()**, and push it with **setSensorState()**.
- Read the latest servo outputs with **getInputs()** and apply the 16 PWM channels to the vehicle's actuators (motors, control surfaces).
- Optionally poll **getFrameStats()** to track link liveness (the frame counter stops advancing when SITL is not driving the sim).
- On link loss, call **clearIO()** to zero the exchanged inputs and sensor state.
- At shutdown (or on destruction), call **shutdown()** to stop the thread and close the socket.


### See Also


- **[UnigineSensorState](#UnigineSensorState)** � a physics snapshot in Unigine frames.
- **[ArduPilotSensorState](#ArduPilotSensorState)** � a sensor snapshot in ArduPilot frames.
- The **jsbsim** module's **[JSBSim::FDMJSBSim](../../../api/modules/jsbsim/class.fdmjsbsim.md)** class for an alternative, in-process flight dynamics model.


## ArduPilotSITLBridge Class

---

## void init ( )

Opens and binds a non-blocking UDP socket on the given port and starts the internal network thread. Has no effect if the bridge is already initialized. If the socket cannot be opened or bound, an error is logged and the bridge stays inactive.
### Arguments

## void shutdown ( )

Stops the network thread and closes the UDP socket. Safe to call when the bridge is not initialized. Called automatically by the destructor.
## void setInputs ( )

Stores the latest servo inputs and frame statistics. Normally called by the internal network thread when a servo packet arrives; the integration code reads them back via **getInputs()**. This function is thread-safe.
### Arguments

## void getInputs ( )

Copies the latest servo outputs from ArduPilot into the supplied array. Call once per tick to drive the vehicle's actuators. This function is thread-safe.
### Arguments

## void setSensorState ( )

Stores the sensor state that the network thread sends back to ArduPilot on its next reply. Call once per tick with the converted vehicle state. This function is thread-safe.
### Arguments

## void getSensorState ( )

Reads back the currently stored sensor state. Used internally by the network thread when assembling the reply packet. This function is thread-safe.
### Arguments

## void getFrameStats ( )

Returns the most recent frame rate and frame counter from SITL. The counter advancing indicates an active link; a stalled counter indicates SITL has stopped driving the simulation. This function is thread-safe.
### Arguments

## void clearIO ( )

Zeroes the exchanged servo inputs and sensor state on link loss. Frame statistics are left untouched so liveness tracking can still observe that the frame counter has stopped advancing. This function is thread-safe.
## struct UnigineSensorState

A physics snapshot of a vehicle in Unigine frames: **ENU** world and a body frame with X pointing right, Y forward, and Z up. This is the input to [arduPilotSensorStateFromUnigine()](#arduPilotSensorStateFromUnigine_UnigineSensorState_ArduPilotSensorState). The acceleration is plain world-frame acceleration without gravity; gravity is added during conversion, so do not pre-subtract it.
### Fields


## struct ArduPilotSensorState

A vehicle sensor snapshot in **ArduPilot** frames: **NED** world and **FRD** (Forward-Right-Down) body. This is the type exchanged through [setSensorState()](#setSensorState_ArduPilotSensorState_void) and [getSensorState()](#getSensorState_ArduPilotSensorState_void). Produce it from a [UnigineSensorState](#UnigineSensorState) with [arduPilotSensorStateFromUnigine()](#arduPilotSensorStateFromUnigine_UnigineSensorState_ArduPilotSensorState) rather than filling the fields by hand.
### Fields

- *double* **timestamp** - Simulation timestamp in seconds, set by the bridge when assembling the reply, relative to the time init() was called (default: 0.0).


## Coordinate Frame Conversion


## ArduPilotSITL Functions Class

---
