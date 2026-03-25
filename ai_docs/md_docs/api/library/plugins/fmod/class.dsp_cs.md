# Unigine::Plugins::FMOD::DSP Class (CS)


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


The Digital Signal Processor transforms input audio signals to an output stream.


## DSP Class

### Properties

## 🔒︎ bool IsIdle

The value specifying if idle state is enabled. A DSP is considered idle when it stops receiving input signal and all internal processing of stored input has been exhausted. Each DSP type has the potential to have differing idle behaviour based on the type of effect. A reverb or echo may take a longer time to go idle after it stops receiving a valid signal, compared to an effect with a shorter tail length like an EQ filter.
## bool Bypass

The processing bypass state. If bypass is set, processing of this unit is skipped but it continues to process its inputs.
## bool Active

The processing active state. If active state is disabled, processing of this unit and its inputs are stopped. When created, a DSP is inactive. If [addDSP](../../../../api/library/plugins/fmod/class.channelgroup_cs.md#addDSP_int_int_DSP) is used it will automatically be activated, otherwise it must be set to active manually.
### Members

---

## void SetParameterBool ( int index , bool value )

Sets a boolean parameter by index.
### Arguments

- *int* **index** - The parameter index in range from 0 to [getNumParameters()](#getNumParameters_int).
- *bool* **value** - The parameter value.

## void SetParameterInt ( int index , int value )


Sets an integer value for the parameter by its index.


A DSP can have several parameters that can be controlled individually. For example, ECHO DSP's parameters are: DELAY, FEEDBACK, DRYLEVEL, WETLEVEL. See the [list of available parameters](https://www.fmod.com/resources/documentation-api?version=2.02&page=core-api-common-dsp-effects.html) for various DSP types.


### Arguments

- *int* **index** - Parameter index. The parameters are numbered starting from 0 to [getNumParameters()](#getNumParameters_int).
- *int* **value** - Parameter value.

## void SetParameterFloat ( int index , float value )


Sets a floating point value for the parameter by its index.


A DSP can have several parameters that can be controlled individually. For example, ECHO DSP's parameters are: DELAY, FEEDBACK, DRYLEVEL, WETLEVEL. See the [list of available parameters](https://www.fmod.com/resources/documentation-api?version=2.02&page=core-api-common-dsp-effects.html) for various DSP types.


### Arguments

- *int* **index** - Parameter index. The parameters are numbered starting from 0 to [getNumParameters()](#getNumParameters_int).
- *float* **value** - Parameter value.

## DSPType.TYPE GetType ( )

Returns the DSP type value, one of the [TYPE](../../../../api/library/plugins/fmod/class.dsptype_cs.md) values.
### Return value

The DSP type value, one of the [TYPE](../../../../api/library/plugins/fmod/class.dsptype_cs.md) values.
## int GetNumParameters ( )

Returns the number of parameters exposed by this unit. Use this to enumerate all parameters of a DSP unit with [getParameterInfo()](#getParameterInfo_int_DSP_PARAMETER_DESC).
### Return value

The number of parameters exposed by this unit.
## void Release ( )

Frees a DSP object.
## void ReleaseFromChannel ( )

Auxiliary function, should not be used.
