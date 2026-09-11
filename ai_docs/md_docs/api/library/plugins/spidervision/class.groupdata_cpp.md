# Unigine::Plugins::SpiderVision::GroupData Class (CPP)

**Header:** #include <plugins/Unigine/SpiderVision/UnigineSpiderVision.h>


This class stores the settings for the group of viewport arranged according to a predefined pattern.


The color correction data are stored in the [configuration file](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#config_file).


This object is accessible via the corresponding method of the [DisplaysConfig](../../../../api/library/plugins/spidervision/class.displaysconfig_cpp.md#getGroupByIndex_int_GroupData) class.


## GroupData Class

### Enums

## GROUP_TYPE

| Name | Description |
|---|---|
| **WALL** = 0 | Wall multi-channel visualization configuration. |
| **CAVE** = 1 | The group is a CAVE room group (see the CAVEGroupData class). |

### Members

## int getID () const

Returns the current ID of the viewport group.
### Return value

Current ID of the viewport group.
## GroupData::GROUP_TYPE getType () const

Returns the current type of the viewport group.
### Return value

Current type of the viewport group.
## void setName ( const char * name )

Sets a new name of the viewport group.
### Arguments

- *const char ** **name** - The name of the viewport group.

## String getName () const

Returns the current name of the viewport group.
### Return value

Current name of the viewport group.
---

## void saveXml ( const Ptr < Xml > & xml )

Saves the viewport group data to the given instance of the Xml class.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../../api/library/common/class.xml_cpp.md)> &* **xml** - [Xml class](../../../../api/library/common/class.xml_cpp.md) instance into which the data will be saved.

## bool restoreXml ( const Ptr < Xml > & xml )

Loads the viewport group data from the specified instance of the Xml class.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../../api/library/common/class.xml_cpp.md)> &* **xml** - [Xml class](../../../../api/library/common/class.xml_cpp.md) instance the data from which is to be loaded.

### Return value

true if the data has been loaded successfully, otherwise false.
## void save ( const Ptr < Stream > & stream )

Saves the viewport group data to the specified stream.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream to which the data is to be written.

## void restore ( const Ptr < Stream > & stream )

Loads the viewport group data from the specified stream.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream the data from which is to be loaded.

## void copy ( const GroupData & data )

Copies the name and all layout parameters from another group of the same type and resets the generated flag, so the group must be generated again.
### Arguments

- *const [GroupData](../../../../api/library/plugins/spidervision/class.groupdata_cpp.md) &* **data** - Source group to copy the parameters from; must be of the same type as this group, otherwise the call does nothing.

## void generate ( )

Creates the group's member viewports in the displays configuration and applies the group parameters to them. Does nothing if the group has already been generated.
## void refresh ( )

Recomputes and re-applies the derived parameters (position, rotation, size, pixel density, window size and mode, render mode) of every member viewport from the current group parameters. Most parameter setters call it automatically for a generated group.
