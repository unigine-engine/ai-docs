# Unigine::Plugins::VrpnTrackerDevice Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


A class for the [VRPN Plugin](../../../../code/plugins/vrpn/index_usc.md) that allows receiving data about position, orientation, velocity and acceleration of tracked objects from 3D tracking sensors.


### See Also


- Article on [VRPN Plugin](../../../../code/plugins/vrpn/index_usc.md)
- UnigineScript samples:

  -
  -


## VrpnTrackerDevice Class

### Members

## int getNumSensors () const

Returns the current total number of sensors.
### Return value

Current total number of sensors.
---

## VrpnTrackerDevice ( string name )

Constructor.
### Arguments

- *string* **name** - Path to the device in the format *device_name@server_address*.

## void setAccelerationCallback ( string name )

Sets the world script callback function that receives data about acceleration of tracked objects.
### Arguments

- *string* **name** - Callback function name.

### Examples


```cpp
VrpnTrackerDevice vrpn_tracker;

int init() {
	vrpn_tracker = new VrpnTrackerDevice("device_name@server_addr");
	vrpn_tracker.setAccelerationCallback("acceleration_callback");

	return 1;
}

int shutdown() {
	delete vrpn_tracker;
	return 1;
}

int update() {
	vrpn_tracker.update();
	return 1;
}
// a callback function
void acceleration_callback(int sensor,vec3 acceleration,quat orientation,float ifps) {
	log.message("Device sensor %d: acceleration %s, orientation %s, ifps %f\n",sensor,acceleration,orientation,ifps);
}

```


## string getAccelerationCallback ( )

Returns a name of the world script callback function that receives data about acceleration of tracked objects. The callback function should be defined in the world script and receive **4** arguments:


1. Sensor number (*int*)
2. Linear acceleration (*vec3* for the float precision version, or *dvec3* for the double precision version)
3. Acceleration of orientation change (an analog of angular acceleration; *quat*)
4. Acceleration measurement time (*float* for the float precision version, or *double* for the double precision version)


```cpp
// float precision
void callback_func(int sensor,vec3 acceleration,quat acceleration_orientation,float ifps) {
	// function logic
}
// double precision
void callback_func(int sensor,dvec3 acceleration,quat acceleration_orientation,double ifps) {
	// function logic
}

```


### Return value

Callback function name.
## void setTransformCallback ( string name )

Sets the world script callback function that receives data about position and orientation of tracked objects.
### Arguments

- *string* **name** - Callback function name.

### Examples


```cpp
VrpnTrackerDevice vrpn_tracker;

int init() {
	vrpn_tracker = new VrpnTrackerDevice("device_name@server_addr");
	vrpn_tracker.setTransformCallback("transform_callback");

	return 1;
}

int shutdown() {
	delete vrpn_tracker;
	return 1;
}

int update() {
	vrpn_tracker.update();
	return 1;
}
// a callback function
void transform_callback(int sensor,vec3 position,quat orientation) {
	log.message("Device sensor %d: position %s, orientation %s\n",sensor,position,orientation);
}

```


## string getTransformCallback ( )


Returns a name of the world script callback function that receives data about position and orientation of tracked objects. The callback function should be defined in the world script and receive **3** arguments:


1. Sensor number (*int*)
2. Position (*vec3* for the float precision version, or *dvec3* for the double precision version)
3. Orientation (*quat*)


```cpp
// float precision
void callback_func(int sensor,vec3 acceleration,quat acceleration_orientation,float ifps) {
	// function logic
}
// double precision
void callback_func(int sensor,dvec3 acceleration,quat acceleration_orientation,double ifps) {
	// function logic
}

```


### Return value

Callback function name.
## void setVelocityCallback ( string name )

Sets the world script callback function that receives data about velocity of tracked objects.
### Arguments

- *string* **name** - Callback function name.

### Examples


```cpp
VrpnTrackerDevice vrpn_tracker;

int init() {
	vrpn_tracker = new VrpnTrackerDevice("device_name@server_addr");
	vrpn_tracker.setVelocityCallback("velocity_callback");

	return 1;
}

int shutdown() {
	delete vrpn_tracker;
	return 1;
}

int update() {
	vrpn_tracker.update();
	return 1;
}

// a callback function
void velocity_callback(int sensor,vec3 velocity,quat orientation,float velocity_ifps) {
	log.message("Device sensor %d: velocity %s, orientation %s, ifps %f\n",sensor,velocity,orientation,ifps);
}

```


## string getVelocityCallback ( )


Returns a name of the world script callback function that receives data about velocity of tracked objects. The callback function should be defined in the world script and receive **4** arguments:


1. Sensor number (*int*)
2. Linear velocity (*vec3* for the float precision version, or *dvec3* for the double precision version)
3. Velocity of orientation change (an analog of angular velocity; *quat*)
4. Velocity measurement time (*float* for the float precision version, or *double* for the double precision version)


```cpp
// float precision
void callback_func(int sensor,vec3 velocity,quat velocity_orientation,float ifps) {
	// function logic
}
// double precision
void callback_func(int sensor,dvec3 velocity,quat velocity_orientation,double ifps) {
	// function logic
}

```


### Return value

Callback function name.
## void update ( )


Updates the internal state of the device and receives input data.


> **Notice:** This function should be called each frame.


## Vec3 getSensorPosition ( int num )

Returns the specified sensor position.
### Arguments

- *int* **num** - Sensor index number in range [0; [NUM_SENSORS](#getNumSensors_int) - 1 ].

### Return value

Sensor position.
## quat getSensorRotation ( int num )

Returns the specified sensor rotation.
### Arguments

- *int* **num** - Sensor index number in range [0; [NUM_SENSORS](#getNumSensors_int) - 1 ].

### Return value

Sensor rotation.
## Vec3 getSensorVelocity ( int num )

Returns the current sensor velocity (m/s2).
### Arguments

- *int* **num** - Sensor index number in range [0; [NUM_SENSORS](#getNumSensors_int) - 1 ].

### Return value

Sensor velocity, in units per second.
## quat getSensorVelocityOrientation ( int num )

Returns the orientation of the specified sensor after the [delta time](#getSensorVelocityIFps_int_scalar).
### Arguments

- *int* **num** - Sensor index number in range [0; [NUM_SENSORS](#getNumSensors_int) - 1 ].

### Return value

Orientation of the sensor velocity.
## scalar getSensorVelocityIFps ( int num )

Returns the delta time (in seconds) for the sensor velocity.
### Arguments

- *int* **num** - Sensor index number in range [0; [NUM_SENSORS](#getNumSensors_int) - 1 ].

### Return value

Delta time (in seconds).
## Vec3 getSensorAcceleration ( int num )

Returns the current sensor acceleration (m/s2).
### Arguments

- *int* **num** - Sensor index number in range [0; [NUM_SENSORS](#getNumSensors_int) - 1 ].

### Return value

Sensor acceleration.
## quat getSensorAccelerationOrientation ( int num )

Returns the orientation of the specified sensor after the [delta time](#getSensorAccelerationIFps_int_scalar).
### Arguments

- *int* **num** - Sensor index number in range [0; [NUM_SENSORS](#getNumSensors_int) - 1 ].

### Return value

Orientation of the sensor acceleration.
## scalar getSensorAccelerationIFps ( int num )

Returns delta time (in seconds) for the sensor acceleration.
### Arguments

- *int* **num** - Sensor index number in range [0; [NUM_SENSORS](#getNumSensors_int) - 1 ].

### Return value

Delta time (in seconds).
