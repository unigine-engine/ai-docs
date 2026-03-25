# VRPN Plugin

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


This section contains functions available when the [VRPN Plugin](../../../../code/plugins/vrpn/index_cpp.md) is loaded.


If the plugin is loaded together with the engine, the `HAS_VRPN_CLIENT` definition is set. This definition can be used, for example, to avoid errors if the plugin is not loaded: the code in which the plugin functions are executed can be wrapped around as follows:

```cpp
#ifdef HAS_VRPN_CLIENT
	// VRPN plugin functions
#endif

```


### See Also


- Article on [VRPN Plugin](../../../../code/plugins/vrpn/index_cpp.md)
- UnigineScript samples:

  -
  -


## Articles in This Section

- [VrpnClient Class (USC)](../../../../api/library/plugins/vrpn/class.vrpnclient_usc.md)

- [VrpnClient Class (CS)](../../../../api/library/plugins/vrpn/class.vrpnclient_cs.md)

- [VrpnClient Class (CPP)](../../../../api/library/plugins/vrpn/class.vrpnclient_cpp.md)

- [VrpnAnalogDevice Class (USC)](../../../../api/library/plugins/vrpn/vrpnanalogdevice.class_usc.md)

- [VrpnAnalogDevice Class (CS)](../../../../api/library/plugins/vrpn/vrpnanalogdevice.class_cs.md)

- [VrpnAnalogDevice Class (CPP)](../../../../api/library/plugins/vrpn/vrpnanalogdevice.class_cpp.md)

- [VrpnButtonDevice Class (USC)](../../../../api/library/plugins/vrpn/vrpnbuttondevice.class_usc.md)

- [VrpnButtonDevice Class (CS)](../../../../api/library/plugins/vrpn/vrpnbuttondevice.class_cs.md)

- [VrpnButtonDevice Class (CPP)](../../../../api/library/plugins/vrpn/vrpnbuttondevice.class_cpp.md)

- [VrpnTrackerDevice Class (USC)](../../../../api/library/plugins/vrpn/vrpntrackerdevice.class_usc.md)

- [VrpnTrackerDevice Class (CS)](../../../../api/library/plugins/vrpn/vrpntrackerdevice.class_cs.md)

- [VrpnTrackerDevice Class (CPP)](../../../../api/library/plugins/vrpn/vrpntrackerdevice.class_cpp.md)
