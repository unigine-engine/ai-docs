# Unigine::Plugins::FMOD::ChannelGroup Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


A submix in the mixing hierarchy that can contain both Channel and ChannelGroup objects.


## ChannelGroup Class

---

## Channel getChannel ( int id )

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

- *[Channel](../../../../api/library/plugins/fmod/class.channel_usc.md) ** **OUT_channel** - Channel to be added. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## DSP addDSP ( int index , int dsp_type )

Adds a DSP unit to the specified index in the DSP chain.
### Arguments

- *int* **index** - Offset into the DSP chain.
- *int* **dsp_type** - [Type](../../../../api/library/plugins/fmod/class.dsptype_usc.md) of DSP unit to be added.

### Return value

The added DSP unit.
## void removeDSP ( int index )

Removes the specified DSP unit from the DSP chain.
### Arguments

- *int* **index** - Index of the DSP unit to be removed.

## DSP getDSP ( int index )

Returns the DSP unit at the specified index in the DSP chain.
### Arguments

- *int* **index** - Offset into the DSP chain.

### Return value

DSP unit at the specified index.
## int getNumDSPs ( )

Returns the number of DSP units in the DSP chain.
### Return value

The number of DSP units in the DSP chain.
## void release ( )

Shut down and free the object.
