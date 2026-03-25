# Unigine::Plugins::SpiderVision::GroupData Class (CS)


This class stores the settings for the group of viewport arranged according to a predefined pattern.


The color correction data are stored in the [configuration file](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#config_file).


This object is accessible via the corresponding method of the [DisplaysConfig](../../../../api/library/plugins/spidervision/class.displaysconfig_cs.md#getGroupByIndex_int_GroupData) class.


## GroupData Class

### Enums

## GROUP_TYPE

| Name | Description |
|---|---|
| **WALL** = 0 | Wall multi-channel visualization configuration. |

### Properties

## 🔒︎ int ID

The ID of the viewport group.
## 🔒︎ GroupData.GROUP_TYPE Type

The type of the viewport group.
## string Name

The name of the viewport group.
### Members

---

## void SaveXml ( Xml xml )

Saves the viewport group data to the given instance of the Xml class.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_cs.md)* **xml** - [Xml class](../../../../api/library/common/class.xml_cs.md) instance into which the data will be saved.

## bool RestoreXml ( Xml xml )

Loads the viewport group data from the specified instance of the Xml class.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_cs.md)* **xml** - [Xml class](../../../../api/library/common/class.xml_cs.md) instance the data from which is to be loaded.

### Return value

true if the data has been loaded successfully, otherwise false.
## void Save ( Stream stream )

Saves the viewport group data to the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_cs.md)* **stream** - Stream to which the data is to be written.

## void Restore ( Stream stream )

Loads the viewport group data from the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_cs.md)* **stream** - Stream the data from which is to be loaded.
