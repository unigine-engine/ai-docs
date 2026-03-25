# Unigine::Plugins::IG::Component Class (CPP)

**Header:** #include <plugins/Unigine/IG/UnigineIG.h>


This class represents the IG Component interface.

> **Notice:** IG plugin must be loaded.


## Component Class

### Enums

## COMPONENT_TYPE

| Name | Description |
|---|---|
| **COMPONENT_TYPE_ENTITY** = 0 | Entity component class. |
| **COMPONENT_TYPE_VIEW** = 1 | View component class. |
| **COMPONENT_TYPE_GROUP** = 2 | View Group component class. |
| **COMPONENT_TYPE_SENSOR** = 3 | Sensor component class. |
| **COMPONENT_TYPE_REG_WATER** = 4 | Regional Water component class. |
| **COMPONENT_TYPE_REG_TERRAIN** = 5 | Regional Terrain component class. |
| **COMPONENT_TYPE_REG_WEATHER** = 6 | Regional Weather component class. |
| **COMPONENT_TYPE_GLOBAL_WATER** = 7 | Global Water component class. |
| **COMPONENT_TYPE_GLOBAL_TERRAIN** = 8 | Global Terrain component class. |
| **COMPONENT_TYPE_GLOBAL_WEATHER** = 9 | Global Weather component class. |
| **COMPONENT_TYPE_ATMOSPHERE** = 10 | Atmosphere component class. |
| **COMPONENT_TYPE_CELESTIAL** = 11 | Celestial component class. |
| **COMPONENT_TYPE_EVENT** = 12 | Event component class. |
| **COMPONENT_TYPE_SYSTEM** = 13 | System component class. |
| **COMPONENT_TYPE_SYMBOL_SURFACE** = 14 | Symbol Surface component class. |
| **COMPONENT_TYPE_SYMBOL** = 15 | Symbol component class. |

### Members

---

## int getID ( ) const

Returns the component ID.
### Return value

Component ID.
## Component::COMPONENT_TYPE getComponentType ( )

Returns the component class.
### Return value

CIGI component class.
## int64_t getInstanceID ( )

Returns the instance ID.
### Return value

Instance ID.
## Ptr < Node > getNode ( ) const

Returns the node assigned to the component.
### Return value

Node assigned to the component.
## Ptr < Property > getProperty ( ) const

Returns the node assigned to the component.
### Return value

Property assigned to the component.
## void setParameterData ( const char * name , const void * value )

Sets the data for the component parameter with the specified name.
### Arguments

- *const char ** **name** - Parameter name.
- *const void ** **value** - Pointer to a buffer with parameter data to be set.

## void setParameterInt ( const char * name , int value )

Sets the value of the component parameter with the specified name using the specified integer value.
### Arguments

- *const char ** **name** - Parameter name.
- *int* **value** - Value to be set.

## int getParameterInt ( const char * name )

Returns the current value of the parameter with the specified name.
### Arguments

- *const char ** **name** - Parameter name.

### Return value

Current value of the parameter with the specified name.
## void setParameterFloat ( const char * name , float value )

Sets the value of the float component parameter with the specified name using the specified float value.
### Arguments

- *const char ** **name** - Parameter name.
- *float* **value** - Value to be set.

## float getParameterFloat ( const char * name )

Returns the current value of the float parameter with the specified name.
### Arguments

- *const char ** **name** - Parameter name.

### Return value

Current value of the float parameter with the specified name.
## void setParameterDouble ( const char * name , double value )

Sets the value of the component parameter with the specified name using the specified double value.
### Arguments

- *const char ** **name** - Parameter name.
- *double* **value** - Value to be set.

## double getParameterDouble ( const char * name )

Returns the current value of the double parameter with the specified name.
### Arguments

- *const char ** **name** - Parameter name.

### Return value

Current value of the double parameter with the specified name.
