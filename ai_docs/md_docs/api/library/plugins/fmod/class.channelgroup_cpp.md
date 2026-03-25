# Unigine::Plugins::FMOD::ChannelGroup Class (CPP)

**Header:** #include <plugins/Unigine/FMOD/UnigineFMOD.h>


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


A submix in the mixing hierarchy that can contain both Channel and ChannelGroup objects.


## ChannelGroup Class

---

## Channel * getChannel ( int id )

Returns the channel at the specified index.
### Arguments

- *int* **id** - Index of the channel.

### Return value

Channel at the specified index.
## int getChannelCount ( )

Returns the number of channels that feed into this group.
### Return value

Number of channels.
## void setVolume ( float volume )

Sets a volume level for the group.
### Arguments

- *float* **volume** - Volume level.

## void addChannel ( Channel * OUT_channel )

Adds a channel to the group.
### Arguments

- *[Channel](../../../../api/library/plugins/fmod/class.channel_cpp.md) ** **OUT_channel** - Channel to be added. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## DSP * addDSP ( int index , DSPType::TYPE dsp_type )

Adds a DSP unit to the specified index in the DSP chain.
### Arguments

- *int* **index** - Offset into the DSP chain.
- *[DSPType::TYPE](../../../../api/library/plugins/fmod/class.dsptype_cpp.md#TYPE)* **dsp_type** - [Type](../../../../api/library/plugins/fmod/class.dsptype_cpp.md) of DSP unit to be added.

### Return value

The added DSP unit.
## void addDSP ( DSP * fmod_dsp )

Adds the specified DSP unit in the DSP chain.
### Arguments

- *[DSP](../../../../api/library/plugins/fmod/class.dsp_cpp.md) ** **fmod_dsp** - DSP unit to be added.

## bool containsDSP ( void * fmod_dsp )

Checks if the DSP chain contains the specified DSP unit.
### Arguments

- *void ** **fmod_dsp** - DSP unit to be checked.

## void removeDSP ( int index )

Removes the specified DSP unit from the DSP chain.
### Arguments

- *int* **index** - Index of the DSP unit to be removed.

## void unregisterDSP ( void * fmod_dsp )

Unregisters a plugin DSP.
### Arguments

- *void ** **fmod_dsp** - The plugin DSP to be unregistered.

## DSP * getDSP ( int index )

Returns the DSP unit at the specified index in the DSP chain.
### Arguments

- *int* **index** - Offset into the DSP chain.

### Return value

DSP unit at the specified index.
## DSP * getDSP ( void * fmod_dsp )

Returns the internal FMOD DSP unit by its pointer.
### Arguments

- *void ** **fmod_dsp** - The pointer to the internal FMOD DSP unit.

### Return value

DSP unit.
## int getNumDSPs ( ) const

Returns the number of DSP units in the DSP chain.
### Return value

The number of DSP units in the DSP chain.
## void release ( )

Shut down and free the object.
