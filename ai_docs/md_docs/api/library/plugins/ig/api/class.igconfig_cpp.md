# Unigine::Plugins::IG::IGConfig Class (CPP)

**Header:** #include <plugins/Unigine/IG/UnigineIG.h>


This class is used to manage the [IG configuration](../../../../../ig/config.md) via API.


> **Notice:** IG plugin must be loaded.


The **CloudTypeDef** structure represents the [cloud type](../../../../../ig/weather/config_cpp.md#config_cloud_types) definitions. It is declared as follows:


```cpp
struct CloudTypeDef
{
	int type = 0;
	Unigine::String name;
	Unigine::String material;
};

```


The **PrecipitationTypeDef** structure represents the [precipitation type](../../../../../ig/weather/config_cpp.md#config_precipitation_types) definitions. It is declared as follows:


```cpp
struct PrecipitationTypeDef
{
	int type = 0;
	Unigine::String name;
	Unigine::String far_node_path;
	Unigine::String near_node_path;
};

```


The **SynckerChannelDef** structure represents the Syncker channel definitions. It is declared as follows:


```cpp
struct SynckerChannelDef
{
	Unigine::String slave_name;
	int view_id = 0;
	bool use_projection = false;
};

```


The **DatabaseDef** structure represents the [database](../../../../../ig/config.md#config_databases) definitions. It is declared as follows:


```cpp
struct DatabaseDef
{
	int database_id = 0;
	Unigine::String world_name;
	Unigine::Math::Vec3 geodetic_origin;
};

```


The **ViewTypeDef** structure represents the [view type](../../../../../ig/config.md#config_view_types) definitions. It is declared as follows:


```cpp
struct ViewTypeDef
{
	int view_type_id = 0;
	Unigine::String post_material;
};

```


The **EntityTypeDef** structure represents the [entity type](../../../../../ig/config.md#config_entities) definitions with the components, articulated parts, and volumes. It is declared as follows:


```cpp
struct EntityTypeDef
{
	int64_t id = 0;
	Unigine::String name;
	Unigine::String path;
	int64_t inherit_id = 0;

	struct ComponentDef
	{
		struct ComponentParameterDef
		{
			ITEM_TYPE type = ITEM_TYPE::UNKNOWN;
			Unigine::String name;
			Unigine::String parameter_name;
		};
		bool inherited = false;
		int id = 0;
		Unigine::String name;
		Unigine::String node_path;
		Unigine::String property_name;
		Unigine::Vector<ComponentParameterDef> parameters;
	};
	Unigine::Map<int, ComponentDef> components;

	struct ArticulatedPartDef
	{
		bool inherited = false;
		int id = 0;
		Unigine::String name;
		Unigine::Vector<Unigine::String> node_path;
		Unigine::Vector<Unigine::Math::ivec3> is_inverted;
	};
	Unigine::Map<int, ArticulatedPartDef> articulated_parts;

	struct VolumeDef
	{
		bool inherited = false;
		int id = 0;
		int shape_id = 0;
		Unigine::String node_path;
		Unigine::String name;
	};
	Unigine::Map<int, VolumeDef> volume_definitions;
};

```


## IGConfig Class

### Enums

## ITEM_TYPE

| Name | Description |
|---|---|
| **ITEM_TYPE_UNKNOWN** = 0 | The parameter type has not been defined. |
| **ITEM_TYPE_INT** = 1 | The parameter type is an integer. |
| **ITEM_TYPE_FLOAT** = 2 | The parameter type is a float. |
| **ITEM_TYPE_DOUBLE** = 3 | The parameter type is a double. |
| **ITEM_TYPE_STRING** = 4 | The parameter type is a string. |

### Members

---

## void setValue ( const char * name , int value )

Sets the value for the specified parameter.
### Arguments

- *const char ** **name** - Parameter name.
- *int* **value** - Integer value to be set.

## void setValue ( const char * name , float value )

Sets the value for the specified parameter.
### Arguments

- *const char ** **name** - Parameter name.
- *float* **value** - Float value to be set.

## void setValue ( const char * name , const char * value )

Sets the value for the specified parameter.
### Arguments

- *const char ** **name** - Parameter name.
- *const char ** **value** - String value to be set.

## void setValue ( const char * name , double value )

Sets the value for the specified parameter.
### Arguments

- *const char ** **name** - Parameter name.
- *double* **value** - Parameter value.

## int getValue ( const char * name , int default_value ) const

Returns the value of the specified parameter. If this parameter has not been specified in the [ig_config.xml](../../../../../ig/config.md) file, default_value is set for this parameter.
### Arguments

- *const char ** **name** - Parameter name.
- *int* **default_value** - A value to be set if the parameter is not specified in the [ig_config.xml](../../../../../ig/config.md) file.

### Return value

Parameter value.
## float getValue ( const char * name , float default_value ) const

Returns the value of the specified parameter. If this parameter has not been specified in the [ig_config.xml](../../../../../ig/config.md) file, default_value is set for this parameter.
### Arguments

- *const char ** **name** - Parameter name.
- *float* **default_value** - A value to be set if the parameter is not specified in the [ig_config.xml](../../../../../ig/config.md) file.

### Return value

Parameter value.
## String getValue ( const char * name , const char * default_value ) const

Returns the value of the specified parameter. If this parameter has not been specified in the [ig_config.xml](../../../../../ig/config.md) file, default_value is set for this parameter.
### Arguments

- *const char ** **name** - Parameter name.
- *const char ** **default_value** - A value to be set if the parameter is not specified in the [ig_config.xml](../../../../../ig/config.md) file.

### Return value

Parameter value.
## double getValue ( const char * name , double default_value ) const

Returns the value for the specified parameter. If this parameter has not been specified in the [ig_config.xml](../../../../../ig/config.md) file, default_value is set for this parameter.
### Arguments

- *const char ** **name** - Parameter name.
- *double* **default_value** - A value to be set if the parameter is not specified in the [ig_config.xml](../../../../../ig/config.md) file.

### Return value

Parameter value.
## const String & getPath ( ) const

Returns the path to the current [ig_config.xml](../../../../../ig/config.md) file.
### Return value

Path to the [ig_config.xml](../../../../../ig/config.md) file.
## bool load ( const char * filename = "ig_config.xml" )

Loads IG configuration from a file with the specified name.
### Arguments

- *const char ** **filename** - Path to the [IG configuration file](../../../../../ig/config.md).

### Return value

**true** if the IG configuration is successfully loaded from the specified file; otherwise, **false**.
## bool save ( const char * filename )

Saves the IG configuration to the specified file.
### Arguments

- *const char ** **filename** - Path to a file to save the IG configuration to.

### Return value

**true** if the IG configuration is successfully saved to the specified file; otherwise, **false**.
## bool save ( )

Saves the IG configuration to the current file.
### Return value

**true** if the IG configuration is successfully saved; otherwise, **false**.
## bool reload ( )

Reloads the IG configuration.
### Return value

**true** if the IG configuration is successfully reloaded; otherwise, **false**.
## void removeVariable ( const char * name )

Removes the specified variable from the configuration file.
### Arguments

- *const char ** **name** - Name of the variable to be removed.

## bool isVariableExist ( const char * name ) const

Returns a value indicating if a variable with the specified name exists.
### Arguments

- *const char ** **name** - Name of the variable.

### Return value

**true** if a variable with the specified name exists; otherwise, **false**.
## const Unigine:: HashMap < Unigine:: String , int64_t> & getEntityTypeNames ( ) const

Returns the list of available type names (type_name -> type_id).
### Return value

List of available type names (type_name -> type_id).
## Unigine:: HashMap <int64_t, EntityTypeDef> & getEntityTypes ( )

Returns the list of available types (type_id -> EntityTypeDef).
### Return value

List of available types (type_id -> EntityTypeDef).
## Unigine:: HashMap <int, DatabaseDef> & getDatabases ( )

Returns the list of available worlds (id -> DatabaseDef).
### Return value

List of available worlds (id -> DatabaseDef).
## Unigine:: HashMap <int, ViewTypeDef> & getViewTypes ( )

Returns the list of available camera post effects (id -> ViewTypeDef).
### Return value

List of available camera post effects (id -> ViewTypeDef).
## Unigine:: HashMap <int, CloudTypeDef> & getCloudTypes ( )

Returns the list of available cloud types (id -> CloudTypeDef).
### Return value

List of available cloud types (id -> CloudTypeDef).
## Unigine:: HashMap <int, SynckerChannelDef> & getSynckerChannels ( )

Returns the list of available Syncker channels (id -> SynckerChannelDef).
### Return value

List of available Syncker channels (id -> SynckerChannelDef).
## Unigine:: HashMap <int, PrecipitationTypeDef> & getPrecipitationTypes ( )

Returns the list of available precipitation types (id -> PrecipitationTypeDef).
### Return value

List of available precipitation types (id -> PrecipitationTypeDef).
