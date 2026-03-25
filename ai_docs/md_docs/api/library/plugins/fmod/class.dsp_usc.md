# Unigine::Plugins::FMOD::DSP Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


The Digital Signal Processor transforms input audio signals to an output stream.


## DSP Class

### Members

## int isIdle () const

Returns the current value specifying if idle state is enabled. A DSP is considered idle when it stops receiving input signal and all internal processing of stored input has been exhausted. Each DSP type has the potential to have differing idle behaviour based on the type of effect. A reverb or echo may take a longer time to go idle after it stops receiving a valid signal, compared to an effect with a shorter tail length like an EQ filter.
### Return value

Current idle state
## void setBypass ( int bypass )

Sets a new processing bypass state. If bypass is set, processing of this unit is skipped but it continues to process its inputs.
### Arguments

- *int* **bypass** - The processing bypass

## int isBypass () const

Returns the current processing bypass state. If bypass is set, processing of this unit is skipped but it continues to process its inputs.
### Return value

Current processing bypass
## void setActive ( int active )

Sets a new processing active state. If active state is disabled, processing of this unit and its inputs are stopped. When created, a DSP is inactive. If [addDSP](../../../../api/library/plugins/fmod/class.channelgroup_usc.md#addDSP_int_int_DSP) is used it will automatically be activated, otherwise it must be set to active manually.
### Arguments

- *int* **active** - The active state

## int isActive () const

Returns the current processing active state. If active state is disabled, processing of this unit and its inputs are stopped. When created, a DSP is inactive. If [addDSP](../../../../api/library/plugins/fmod/class.channelgroup_usc.md#addDSP_int_int_DSP) is used it will automatically be activated, otherwise it must be set to active manually.
### Return value

Current active state
---

## void setParameterBool ( int index , bool value )

Sets a boolean parameter by index.
### Arguments

- *int* **index** - The parameter index in range from 0 to [getNumParameters()](#getNumParameters_int).
- *bool* **value** - The parameter value.

## void setParameterInt ( int index , int value )


Sets an integer value for the parameter by its index.


A DSP can have several parameters that can be controlled individually. For example, ECHO DSP's parameters are: DELAY, FEEDBACK, DRYLEVEL, WETLEVEL. See the [list of available parameters](https://www.fmod.com/resources/documentation-api?version=2.02&page=core-api-common-dsp-effects.html) for various DSP types.


### Arguments

- *int* **index** - Parameter index. The parameters are numbered starting from 0 to [getNumParameters()](#getNumParameters_int).
- *int* **value** - Parameter value.

## void setParameterFloat ( int index , float value )


Sets a floating point value for the parameter by its index.


A DSP can have several parameters that can be controlled individually. For example, ECHO DSP's parameters are: DELAY, FEEDBACK, DRYLEVEL, WETLEVEL. See the [list of available parameters](https://www.fmod.com/resources/documentation-api?version=2.02&page=core-api-common-dsp-effects.html) for various DSP types.


### Arguments

- *int* **index** - Parameter index. The parameters are numbered starting from 0 to [getNumParameters()](#getNumParameters_int).
- *float* **value** - Parameter value.

## int getType ( )

Returns the DSP type value, one of the [TYPE](../../../../api/library/plugins/fmod/class.dsptype_usc.md) values.
### Return value

The DSP type value, one of the [TYPE](../../../../api/library/plugins/fmod/class.dsptype_usc.md) values.
## int getNumParameters ( )

Returns the number of parameters exposed by this unit. Use this to enumerate all parameters of a DSP unit with [getParameterInfo()](#getParameterInfo_int_DSP_PARAMETER_DESC).
### Return value

The number of parameters exposed by this unit.
## void release ( )

Frees a DSP object.
## void releaseFromChannel ( )

Auxiliary function, should not be used.
