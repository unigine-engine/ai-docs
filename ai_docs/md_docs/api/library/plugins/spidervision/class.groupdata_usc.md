# Unigine::Plugins::SpiderVision::GroupData Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class stores the settings for the group of viewport arranged according to a predefined pattern.


The color correction data are stored in the [configuration file](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#config_file).


This object is accessible via the corresponding method of the [DisplaysConfig](../../../../api/library/plugins/spidervision/class.displaysconfig_usc.md#getGroupByIndex_int_GroupData) class.


## GroupData Class

### Members

## int getID () const

Returns the current ID of the viewport group.
### Return value

Current ID of the viewport group.
## int getType () const

Returns the current type of the viewport group.
### Return value

Current type of the viewport group.
## void setName ( String name )

Sets a new name of the viewport group.
### Arguments

- *String* **name** - The name of the viewport group.

## String getName () const

Returns the current name of the viewport group.
### Return value

Current name of the viewport group.
---

## void saveXml ( Xml xml )

Saves the viewport group data to the given instance of the Xml class.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_usc.md)* **xml** - [Xml class](../../../../api/library/common/class.xml_usc.md) instance into which the data will be saved.

## int restoreXml ( Xml xml )

Loads the viewport group data from the specified instance of the Xml class.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_usc.md)* **xml** - [Xml class](../../../../api/library/common/class.xml_usc.md) instance the data from which is to be loaded.

### Return value

**1** if the data has been loaded successfully, otherwise **0**.
## void save ( Stream stream )

Saves the viewport group data to the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_usc.md)* **stream** - Stream to which the data is to be written.

## void restore ( Stream stream )

Loads the viewport group data from the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_usc.md)* **stream** - Stream the data from which is to be loaded.

## void copy ( GroupData data )

Copies the name and all layout parameters from another group of the same type and resets the generated flag, so the group must be generated again.
### Arguments

- *[GroupData](../../../../api/library/plugins/spidervision/class.groupdata_usc.md)* **data** - Source group to copy the parameters from; must be of the same type as this group, otherwise the call does nothing.

## void generate ( )

Creates the group's member viewports in the displays configuration and applies the group parameters to them. Does nothing if the group has already been generated.
## void refresh ( )

Recomputes and re-applies the derived parameters (position, rotation, size, pixel density, window size and mode, render mode) of every member viewport from the current group parameters. Most parameter setters call it automatically for a generated group.
