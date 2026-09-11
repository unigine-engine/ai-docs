# Unigine::Plugins::FMOD::Bus Class (CS)


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


Represents a global mixer bus.


## Bus Class

### Enums

## PORT_INDEX

Output-port index values used for routing the bus signal on platforms with auxiliary audio ports.
| Name | Description |
|---|---|
| **NONE** = 0xffffffffffffffff | The bus is not routed to any specific auxiliary output port and outputs normally. |

### Properties

## bool Paused

The pause state for the bus.
## float Volume

The volume level in range [-inf; inf].
## bool Muted

The mute state for the bus.
## 🔒︎ bool IsValid

The value indicating if the bus reference is valid.
## Bus.PORT_INDEX PortIndex

The output-port index the signal of the underlying *FMOD Studio* bus is routed to, used on platforms with auxiliary audio ports (for example, controller speakers). The *PORT_INDEX_NONE* value routes the bus normally.
### Members

---

## void StopAllEvents ( )

Stops all event instances that are routed into the bus.
## void Release ( )

Releases the bus object.
## string GetPath ( )

Returns the bus object's path.
### Return value

Object's path.
## ChannelGroup GetChannelGroup ( )

Returns the core [ChannelGroup](../../../../api/library/plugins/fmod/class.channelgroup_cs.md). By default the ChannelGroup will only exist when it is needed. If the ChannelGroup does not exist, this function will return [ERR_STUDIO_NOT_LOADED](../../../../api/library/plugins/fmod/class.fmodenums_cs.md#ERR_STUDIO_NOT_LOADED).
### Return value

The core ChannelGroup.
## void LockChannelGroup ( )

Locks the core [ChannelGroup](../../../../api/library/plugins/fmod/class.channelgroup_cs.md). This function forces the system to create the ChannelGroup and keep it available until [unlockChannelGroup](#unlockChannelGroup_void) is called.
## void UnlockChannelGroup ( )

Unlocks the core [ChannelGroup](../../../../api/library/plugins/fmod/class.channelgroup_cs.md). This function allows the system to destroy the ChannelGroup when it is not needed.
