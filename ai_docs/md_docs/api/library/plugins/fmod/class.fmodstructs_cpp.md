# Unigine::Plugins::FMOD::FMODStructs Class (CPP)

**Header:** #include <plugins/Unigine/FMOD/UnigineFMOD.h>


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


Structures used in FMOD Plugin API.


## struct DSP_PARAMETER_FLOAT_MAPPING_PIECEWISE_LINEAR

### Fields

- *int* **numpoints** - Number of pairs in the piecewise mapping (at least 2).
- *float** **pointparamvalues** - Values in the parameter's units for each point.
- *float** **pointpositions** - Positions along the control's scale (e.g. dial angle) corresponding to each parameter value. The range of the scale is arbitrary. All positions will be relative to the minimum and maximum values. If this array is empty, *pointparamvalues* will be distributed with equal spacing.


## struct DSP_PARAMETER_FLOAT_MAPPING

### Fields

- *[FMODEnums::DSP_PARAMETER_FLOAT_MAPPING_TYPE](../../../../api/library/plugins/fmod/class.fmodenums_cpp.md#DSP_PARAMETER_FLOAT_MAPPING_TYPE)* **type** - Mapping type.
- *[FMODStructs::DSP_PARAMETER_FLOAT_MAPPING_PIECEWISE_LINEAR](../../../../api/library/plugins/fmod/class.fmodstructs_cpp.md#DSP_PARAMETER_FLOAT_MAPPING_PIECEWISE_LINEAR)* **piecewiselinearmapping** - Piecewise linear mapping type.


## struct DSP_PARAMETER_DESC_FLOAT

### Fields

- *float* **min** - Minimum value.
- *float* **max** - Maximum value.
- *float* **defaultval** - Default value.
- *[FMODStructs::DSP_PARAMETER_FLOAT_MAPPING](../../../../api/library/plugins/fmod/class.fmodstructs_cpp.md#DSP_PARAMETER_FLOAT_MAPPING)* **mapping** - Mapping and piecewise linear mapping types that define how the values are distributed across dials and automation curves.


## struct DSP_PARAMETER_DESC_INT

### Fields

- *float* **min** - Minimum value.
- *float* **max** - Maximum value.
- *float* **defaultval** - Default value.
- *bool* **goestoinf** - Value indicating whether the last value represents infinity.
- *const char* const** **valuenames** - Names of values (UTF-8 string). The number of strings should correspond to the number of possible values (max - min + 1).


## struct DSP_PARAMETER_DESC_BOOL

### Fields

- *bool* **defaultval** - Default parameter value.
- *const char* const** **valuenames** - Names of values (for false and true, respectively), UTF-8 string. There should be two strings.


## struct DSP_PARAMETER_DESC_DATA

### Fields

- *int* **datatype** - Data type.


## struct DSP_PARAMETER_DESC

### Fields

- *[FMODEnums::DSP_PARAMETER_TYPE](../../../../api/library/plugins/fmod/class.fmodenums_cpp.md#DSP_PARAMETER_TYPE)* **type** - Parameter type.
- *char[]* **name** - Parameter name.
- *char[]* **label** - Unit type label.
- *const char** **description** - Parameter description.
- *union*  -

  - *[FMODStructs::DSP_PARAMETER_DESC_FLOAT](#DSP_PARAMETER_DESC_FLOAT)* **floatdesc** - Floating point format description used when the type is *FMOD_DSP_PARAMETER_TYPE_FLOAT*.
  - *[FMODStructs::DSP_PARAMETER_DESC_INT](#DSP_PARAMETER_DESC_INT)* **intdesc** - Integer format description used when the type is *FMOD_DSP_PARAMETER_TYPE_INT*.
  - *[FMODStructs::DSP_PARAMETER_DESC_BOOL](#DSP_PARAMETER_DESC_BOOL)* **booldesc** - Boolean format description used when the type is *FMOD_DSP_PARAMETER_TYPE_BOOL*.
  - *[FMODStructs::DSP_PARAMETER_DESC_DATA](#DSP_PARAMETER_DESC_DATA)* **datadesc** - Data format description used when the type is *FMOD_DSP_PARAMETER_TYPE_DATA*.
