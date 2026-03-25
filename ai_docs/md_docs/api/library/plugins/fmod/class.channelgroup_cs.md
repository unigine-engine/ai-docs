# Unigine::Plugins::FMOD::ChannelGroup Class (CS)


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


A submix in the mixing hierarchy that can contain both Channel and ChannelGroup objects.


## ChannelGroup Class

### Members

---

## Channel GetChannel ( int id )

Returns the channel at the specified index.
### Arguments

- *int* **id** - Index of the channel.

### Return value

Channel at the specified index.
## int GetChannelCount ( )

Returns the number of channels that feed into this group.
### Return value

Number of channels.
## void SetVolume ( float volume )

Sets a volume level for the group.
### Arguments

- *float* **volume** - Volume level.

## void AddChannel ( Channel [] OUT_channel )

Adds a channel to the group.
### Arguments

- *[Channel](../../../../api/library/plugins/fmod/class.channel_cs.md)[]* **OUT_channel** - Channel to be added. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## DSP AddDSP ( int index , DSPType.TYPE dsp_type )

Adds a DSP unit to the specified index in the DSP chain.
### Arguments

- *int* **index** - Offset into the DSP chain.
- *[DSPType.TYPE](../../../../api/library/plugins/fmod/class.dsptype_cs.md#TYPE)* **dsp_type** - [Type](../../../../api/library/plugins/fmod/class.dsptype_cs.md) of DSP unit to be added.

### Return value

The added DSP unit.
## void RemoveDSP ( int index )

Removes the specified DSP unit from the DSP chain.
### Arguments

- *int* **index** - Index of the DSP unit to be removed.

## DSP GetDSP ( int index )

Returns the DSP unit at the specified index in the DSP chain.
### Arguments

- *int* **index** - Offset into the DSP chain.

### Return value

DSP unit at the specified index.
## int GetNumDSPs ( )

Returns the number of DSP units in the DSP chain.
### Return value

The number of DSP units in the DSP chain.
## void Release ( )

Shut down and free the object.
