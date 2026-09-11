# Unigine::Plugins::FMOD::Bus Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


Represents a global mixer bus.


## Bus Class

### Members

## void setPaused ( int paused )

Sets a new pause state for the bus.
### Arguments

- *int* **paused** - The pause state for the bus

## int isPaused () const

Returns the current pause state for the bus.
### Return value

Current pause state for the bus
## void setVolume ( float volume )

Sets a new volume level in range [-inf; inf].
### Arguments

- *float* **volume** - The volume level in range [-inf; inf].

## float getVolume () const

Returns the current volume level in range [-inf; inf].
### Return value

Current volume level in range [-inf; inf].
## void setMuted ( int muted )

Sets a new mute state for the bus.
### Arguments

- *int* **muted** - The mute state for the bus

## int isMuted () const

Returns the current mute state for the bus.
### Return value

Current mute state for the bus
## int isValid () const

Returns the current value indicating if the bus reference is valid.
### Return value

Current bus reference is valid
## void setPortIndex ( int index )

Sets a new output-port index the signal of the underlying *FMOD Studio* bus is routed to, used on platforms with auxiliary audio ports (for example, controller speakers). The *PORT_INDEX_NONE* value routes the bus normally.
### Arguments

- *int* **index** - The output-port index of the bus

## int getPortIndex () const

Returns the current output-port index the signal of the underlying *FMOD Studio* bus is routed to, used on platforms with auxiliary audio ports (for example, controller speakers). The *PORT_INDEX_NONE* value routes the bus normally.
### Return value

Current output-port index of the bus
---

## void stopAllEvents ( )

Stops all event instances that are routed into the bus.
## void release ( )

Releases the bus object.
## String getPath ( )

Returns the bus object's path.
### Return value

Object's path.
## ChannelGroup getChannelGroup ( )

Returns the core [ChannelGroup](../../../../api/library/plugins/fmod/class.channelgroup_usc.md). By default the ChannelGroup will only exist when it is needed. If the ChannelGroup does not exist, this function will return [ERR_STUDIO_NOT_LOADED](../../../../api/library/plugins/fmod/class.fmodenums_usc.md#ERR_STUDIO_NOT_LOADED).
### Return value

The core ChannelGroup.
## void lockChannelGroup ( )

Locks the core [ChannelGroup](../../../../api/library/plugins/fmod/class.channelgroup_usc.md). This function forces the system to create the ChannelGroup and keep it available until [unlockChannelGroup](#unlockChannelGroup_void) is called.
## void unlockChannelGroup ( )

Unlocks the core [ChannelGroup](../../../../api/library/plugins/fmod/class.channelgroup_usc.md). This function allows the system to destroy the ChannelGroup when it is not needed.
