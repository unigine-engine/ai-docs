# Unigine::Plugins::FMOD::Bus Class (CPP)

**Header:** #include <plugins/Unigine/FMOD/UnigineFMOD.h>


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


Represents a global mixer bus.


## Bus Class

### Members

## void setPaused ( bool paused )

Sets a new pause state for the bus.
### Arguments

- *bool* **paused** - Set **true** to enable pause state for the bus; **false** - to disable it.

## bool isPaused () const

Returns the current pause state for the bus.
### Return value

**true** if pause state for the bus is enabled; otherwise **false**.
## void setVolume ( float volume )

Sets a new volume level in range [-inf; inf].
### Arguments

- *float* **volume** - The volume level in range [-inf; inf].

## float getVolume () const

Returns the current volume level in range [-inf; inf].
### Return value

Current volume level in range [-inf; inf].
## void setMuted ( bool muted )

Sets a new mute state for the bus.
### Arguments

- *bool* **muted** - Set **true** to enable mute state for the bus; **false** - to disable it.

## bool isMuted () const

Returns the current mute state for the bus.
### Return value

**true** if mute state for the bus is enabled; otherwise **false**.
## bool isValid () const

Returns the current value indicating if the bus reference is valid.
### Return value

**true** if bus reference is valid; otherwise **false**.
---

## void stopAllEvents ( )

Stops all event instances that are routed into the bus.
## void release ( )

Releases the bus object.
## String getPath ( ) const

Returns the bus object's path.
### Return value

Object's path.
## ChannelGroup * getChannelGroup ( ) const

Returns the core [ChannelGroup](../../../../api/library/plugins/fmod/class.channelgroup_cpp.md). By default the ChannelGroup will only exist when it is needed. If the ChannelGroup does not exist, this function will return [ERR_STUDIO_NOT_LOADED](../../../../api/library/plugins/fmod/class.fmodenums_cpp.md#ERR_STUDIO_NOT_LOADED).
### Return value

The core ChannelGroup.
## void lockChannelGroup ( )

Locks the core [ChannelGroup](../../../../api/library/plugins/fmod/class.channelgroup_cpp.md). This function forces the system to create the ChannelGroup and keep it available until [unlockChannelGroup](#unlockChannelGroup_void) is called.
## void unlockChannelGroup ( )

Unlocks the core [ChannelGroup](../../../../api/library/plugins/fmod/class.channelgroup_cpp.md). This function allows the system to destroy the ChannelGroup when it is not needed.
