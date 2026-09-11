# Unigine::Plugins::FMOD::DSP Class (CPP)

**Header:** #include <plugins/Unigine/FMOD/UnigineFMOD.h>


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


The Digital Signal Processor transforms input audio signals to an output stream.


## DSP Class

### Members

## bool isIdle () const

Returns the current value specifying if idle state is enabled. A DSP is considered idle when it stops receiving input signal and all internal processing of stored input has been exhausted. Each DSP type has the potential to have differing idle behaviour based on the type of effect. A reverb or echo may take a longer time to go idle after it stops receiving a valid signal, compared to an effect with a shorter tail length like an EQ filter.
### Return value

**true** if idle state is enabled ; otherwise **false**.
## void setBypass ( bool bypass )

Sets a new processing bypass state. If bypass is set, processing of this unit is skipped but it continues to process its inputs.
### Arguments

- *bool* **bypass** - Set **true** to enable processing bypass; **false** - to disable it.

## bool isBypass () const

Returns the current processing bypass state. If bypass is set, processing of this unit is skipped but it continues to process its inputs.
### Return value

**true** if processing bypass is enabled ; otherwise **false**.
## void setActive ( bool active )

Sets a new processing active state. If active state is disabled, processing of this unit and its inputs are stopped. When created, a DSP is inactive. If [addDSP](../../../../api/library/plugins/fmod/class.channelgroup_cpp.md#addDSP_int_int_DSP) is used it will automatically be activated, otherwise it must be set to active manually.
### Arguments

- *bool* **active** - Set **true** to enable active state; **false** - to disable it.

## bool isActive () const

Returns the current processing active state. If active state is disabled, processing of this unit and its inputs are stopped. When created, a DSP is inactive. If [addDSP](../../../../api/library/plugins/fmod/class.channelgroup_cpp.md#addDSP_int_int_DSP) is used it will automatically be activated, otherwise it must be set to active manually.
### Return value

**true** if active state is enabled ; otherwise **false**.
---

## void getInfo ( char * name , unsigned int * version , int * channels , int * configwidth , int * configheight )

Retrieves information about this DSP unit.
### Arguments

- *char ** **name** - The name of this unit will be written (null terminated) to the provided 32 byte buffer. (UTF-8 string).
- *unsigned int ** **version** - Version number of this unit, usually formated as hex AAAABBBB where the AAAA is the major version number and the BBBB is the minor version number.
- *int ** **channels** - Number of channels this unit processes where 0 represents "any".
- *int ** **configwidth** - Configuration dialog box width where 0 represents "no dialog box".
- *int ** **configheight** - Configuration dialog box height where 0 represents "no dialog box".

## FMODStructs::DSP_PARAMETER_DESC getParameterInfo ( int index )

Returns the information about a specified parameter.
### Arguments

- *int* **index** - The parameter index.

### Return value

The parameter description at the specified index.
## void getParameterData ( int index , void * data , int size )

Sets a binary data parameter by index.
### Arguments

- *int* **index** - The parameter index.
- *void ** **data** - The parameter binary data.
- *int* **size** - The size of data.

## void getParameterData ( int index , void ** data , unsigned int * size , char * value_strlen , int value_strlen )

Retrieves a binary data parameter by index.
### Arguments

- *int* **index** - The parameter index.
- *void *** **data** - The parameter binary data.
- *unsigned int ** **size** - The size of data.
- *char ** **value_strlen** - String representation data (UTF-8 string).
- *int* **value_strlen** - Length of data.

## void setParameterBool ( int index , bool value )

Sets a boolean parameter by index.
### Arguments

- *int* **index** - The parameter index in range from 0 to [getNumParameters()](#getNumParameters_int).
- *bool* **value** - The parameter value.

## int getParameterBool ( int index , char * value_strlen , int value_strlen )

Returns a boolean parameter by index.
### Arguments

- *int* **index** - The parameter index.
- *char ** **value_strlen** - String representation value (UTF-8 string).
- *int* **value_strlen** - Length of the string representation value.

### Return value

The parameter value.
## void setParameterInt ( int index , int value )


Sets an integer value for the parameter by its index.


A DSP can have several parameters that can be controlled individually. For example, ECHO DSP's parameters are: DELAY, FEEDBACK, DRYLEVEL, WETLEVEL. See the [list of available parameters](https://www.fmod.com/resources/documentation-api?version=2.02&page=core-api-common-dsp-effects.html) for various DSP types.


### Arguments

- *int* **index** - Parameter index. The parameters are numbered starting from 0 to [getNumParameters()](#getNumParameters_int).
- *int* **value** - Parameter value.

## int getParameterInt ( int index , char * value_strlen , int value_strlen )

Retrieves an integer parameter by index.
### Arguments

- *int* **index** - Parameter index. The parameters are numbered starting from 0 to [getNumParameters()](#getNumParameters_int).
- *char ** **value_strlen** - String representation value (UTF-8 string).
- *int* **value_strlen** - Length of the string representation value.

### Return value

The parameter value.
## void setParameterFloat ( int index , float value )


Sets a floating point value for the parameter by its index.


A DSP can have several parameters that can be controlled individually. For example, ECHO DSP's parameters are: DELAY, FEEDBACK, DRYLEVEL, WETLEVEL. See the [list of available parameters](https://www.fmod.com/resources/documentation-api?version=2.02&page=core-api-common-dsp-effects.html) for various DSP types.


### Arguments

- *int* **index** - Parameter index. The parameters are numbered starting from 0 to [getNumParameters()](#getNumParameters_int).
- *float* **value** - Parameter value.

## float getParameterFloat ( int index , char * value_strlen , int value_strlen )

Retrieves a floating point parameter by index.
### Arguments

- *int* **index** - Parameter index in range from 0 to [getNumParameters()](#getNumParameters_int).
- *char ** **value_strlen** - String representation value (UTF-8 string).
- *int* **value_strlen** - Length of the string representation value.

### Return value

The parameter value.
## DSPType::TYPE getType ( ) const

Returns the DSP type value, one of the [TYPE](../../../../api/library/plugins/fmod/class.dsptype_cpp.md) values.
### Return value

The DSP type value, one of the [TYPE](../../../../api/library/plugins/fmod/class.dsptype_cpp.md) values.
## int getNumParameters ( ) const

Returns the number of parameters exposed by this unit. Use this to enumerate all parameters of a DSP unit with [getParameterInfo()](#getParameterInfo_int_DSP_PARAMETER_DESC).
### Return value

The number of parameters exposed by this unit.
## void setWetDryMix ( float prewet = 1 , float postwet = 1 , float dry = 1 )

Sets the scale of the wet and dry signal components.
### Arguments

- *float* **prewet** - Level of the 'Dry' (pre-processed signal) mix that is processed by the DSP. 0 = silent, 1 = full. Negative level inverts the signal. Values larger than 1 amplify the signal.
- *float* **postwet** - Level of the 'Wet' (post-processed signal) mix that is output. 0 = silent, 1 = full. Negative level inverts the signal. Values larger than 1 amplify the signal.
- *float* **dry** - Level of the 'Dry' (pre-processed signal) mix that is output. 0 = silent, 1 = full. Negative level inverts the signal. Values larger than 1 amplify the signal.

## void getWetDryMix ( float prewet = 1 , float postwet = 1 , float dry = 1 )

Returns the scale of the wet and dry signal components.
### Arguments

- *float* **prewet** - Level of the 'Dry' (pre-processed signal) mix that is processed by the DSP. 0 = silent, 1 = full. Negative level inverts the signal. Values larger than 1 amplify the signal.
- *float* **postwet** - Level of the 'Wet' (post-processed signal) mix that is output. 0 = silent, 1 = full. Negative level inverts the signal. Values larger than 1 amplify the signal.
- *float* **dry** - Level of the 'Dry' (pre-processed signal) mix that is output. 0 = silent, 1 = full. Negative level inverts the signal. Values larger than 1 amplify the signal.

## void release ( )

Frees a DSP object.
## void releaseFromChannel ( )

Auxiliary function, should not be used.
