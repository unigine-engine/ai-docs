# Unigine::Plugins::VrpnAnalogDevice Class (CPP)

**Header:** #include <plugins/Unigine/VrpnClient/UnigineVrpnClient.h>


A class for the [VRPN Plugin](../../../../code/plugins/vrpn/index_cpp.md) that allows receiving data about input devices sticks (for example, game-pad sticks).


### See Also


- Article on [VRPN Plugin](../../../../code/plugins/vrpn/index_cpp.md)
- UnigineScript samples:

  -
  -


## VrpnAnalogDevice Class

### Members

## int getNumChannels () const

Returns the current number of analog sticks that have received data.
### Return value

Current The number of analog sticks that have received data. If no sticks have received data, 0 will be returned.
---

## void setAnalogCallback ( const char * name )


Sets the world script callback function that receives data about input device sticks.


> **Notice:** The callback function should be defined in the world script and receive **1** argument - an instance of the *VrpnAnalogDevice* class.
> ```cpp
> void callback_func(VrpnAnalogDevice device) {
>     // function logic
> }
>
> ```


### Arguments

- *const char ** **name** - Callback function name.

### Examples


```cpp
VrpnAnalogDevice vrpn_analog;

int init() {
	// create an instance of VrpnAnalogDevice
    vrpn_analog = new VrpnAnalogDevice("device_name@server_addr");
	// set a callback
    vrpn_analog.setAnalogCallback("analog_callback");
}

int shutdown() {
    delete vrpn_analog;
    return 1;
}

int update() {
    vrpn_analog.update();
    return 1;
}

// a callback function
void analog_callback(VrpnAnalogDevice device) {
    forloop(int i = 0; device.getNumChannels()) {
        log.message("Device analog channel %d: %lf\n",i,device.getChannel(i));
    }
}

```


## const char * getAnalogCallback ( )

Returns a name of the world script callback function that receives data about input device sticks. The callback function should be defined in the world script and receive **1** argument - an instance of the *VrpnAnalogDevice* class.


```cpp
void callback_func(VrpnAnalogDevice device) {
    // function logic
}

```


### Return value

Callback function name.
## double getChannel ( int channel )


Returns data received by the analog stick with the given number.


> **Notice:** If the given stick haven't received data, the engine assertion will occur.


### Arguments

- *int* **channel** - Analog stick number in range [0;number_of_sticks - 1].

### Return value

Returns data received by the analog stick with the given number.
## int getNumChannels ( )

Returns the number of analog sticks that have received data.
### Return value

The number of analog sticks that have received data. If no sticks have received data, 0 will be returned.
## void update ( )


Updates the internal state of the device and receives input data.


> **Notice:** This function should be called each frame.


## bool hasChanges ( ) const

Returns a value indicating if there were any changes in analog values registered.
### Return value

true if there were any changes in analog values registered otherwise, false.
## VrpnAnalogDevice ( const char * name )

Constructor.
### Arguments

- *const char ** **name** - Path to the device in the format *device_name@server_address*.
