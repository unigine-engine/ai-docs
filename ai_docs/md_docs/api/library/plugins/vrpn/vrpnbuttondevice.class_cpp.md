# Unigine::Plugins::VrpnButtonDevice Class (CPP)

**Header:** #include <plugins/Unigine/VrpnClient/UnigineVrpnClient.h>


A class for the [VRPN Plugin](../../../../code/plugins/vrpn/index_cpp.md) that allows receiving data about states of input device buttons.


### See Also


- Article on [VRPN Plugin](../../../../code/plugins/vrpn/index_cpp.md)
- UnigineScript samples:

  -
  -


## VrpnButtonDevice Class

### Members

## int getNumButtons () const

Returns the current Total number of buttons of the input device.
### Return value

Current
---

## void setButtonCallback ( const char * name )


Sets the world script callback function that receives data about input device buttons.


> **Notice:** The callback function should be defined in the world script and receive **2** arguments - a button number and state.
> ```cpp
> void callback_func(int button,int state) {
>     // function logic
> }
>
> ```


### Arguments

- *const char ** **name** - Callback function name.

### Examples


```cpp
VrpnButtonDevice vrpn_button;

int init() {
	// create an instance of VrpnButtonDevice
    vrpn_button = new VrpnButtonDevice("device_name@server_addr");
	// set a callback
    vrpn_button.setButtonCallback("button_callback");
    return 1;
}

int shutdown() {
    delete vrpn_button;
    return 1;
}

int update() {
    vrpn_button.update();
    return 1;
}

// a callback function
void button_callback(int button,int state) {
    log.message("Device button %d: %d\n",button,state);
}

```


## const char * getButtonCallback ( )


Returns a name of the world script callback function that receives data about input device buttons. The callback function should be defined in the world script and receive **2** arguments - a button number and state.


```cpp
void callback_func(int button,int state) {
    // function logic
}

```


### Return value

Callback function name.
## void update ( )


Updates the internal state of the device and receives input data.


> **Notice:** This function should be called each frame.


## int getButtonState ( int num ) const

Returns the current state for a button with the specified index.
### Arguments

- *int* **num** - Button index.

### Return value

Button state.
## VrpnButtonDevice ( const char * name )

Constructor.
### Arguments

- *const char ** **name** - Path to the device in the format *device_name@server_address*.
