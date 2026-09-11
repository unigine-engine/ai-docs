# Unigine::Plugins::IG::IGConfig Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to manage the [IG configuration](../../../../../ig/config.md) via API.


> **Notice:** IG plugin must be loaded.


The **CloudTypeDef** structure represents the [cloud type](../../../../../ig/weather/config.md#config_cloud_types) definitions. It is declared as follows:


```cpp
struct CloudTypeDef
{
	int type = 0;
	Unigine::String name;
	Unigine::String material;
};

```


The **PrecipitationTypeDef** structure represents the [precipitation type](../../../../../ig/weather/config.md#config_precipitation_types) definitions. It is declared as follows:


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

### Members

---
