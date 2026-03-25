# Unigine::Plugins::SpiderVision::DisplaysConfig Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


The object of this class describes the current configuration, stores information about all viewports and groups of the current configuration and provides an interface to interact with them.


## DisplaysConfig Class

### Members

## String getPath () const

Returns the current path to the displays configuration file.
### Return value

Current path to the displays configuration file.
## unsigned int getNumViewports () const

Returns the current total number of viewports in the configuration.
### Return value

Current total number of viewports in the configuration.
## unsigned int getNumGroups () const

Returns the current total number of projection groups in the configuration.
### Return value

Current total number of projection groups in the configuration.
## void setShowHotkey ( int hotkey )

Sets a new hotkey that opens the displays configuration window.
### Arguments

- *int* **hotkey** - The hotkey that opens the displays configuration window.

## int getShowHotkey () const

Returns the current hotkey that opens the displays configuration window.
### Return value

Current hotkey that opens the displays configuration window.
## static getEventViewportCreated () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event reference.
## static getEventViewportRemoved () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event reference.
## static getEventLoad () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event reference.
## static getEventClear () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event reference.
## static getEventCalibrationGridChanged () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event reference.
---

## ViewportData getViewportByIndex ( int index )

### Arguments

- *int* **index** - Index of the viewport, a value from 0 to the [total number of viewports](#getNumViewports_uint). Index has a temporary correlation with the viewport ID, which may change as the number of viewports is updated. Addressing to a viewport by index implies that the index refers to the viewport ID, which in turn refers to the ViewportData corresponding to that ID.

### Return value

[ViewportData class](../../../../api/library/plugins/spidervision/class.viewportdata_usc.md) instance that stores the viewport data.
## ViewportData getViewport ( int id )

Returns the viewport by the specified ID.
### Arguments

- *int* **id** - Viewport ID.

### Return value

[ViewportData class](../../../../api/library/plugins/spidervision/class.viewportdata_usc.md) instance that stores the viewport data.
## ViewportData createViewport ( int group_id = -1 )

Creates a viewport for the specified viewport group. If no group is set, an individual viewport is created.
### Arguments

- *int* **group_id** - ID of the group. The default value of -1 means that the viewport is not related to any group.

### Return value

[ViewportData class](../../../../api/library/plugins/spidervision/class.viewportdata_usc.md) instance that stores the viewport data.
## void removeViewport ( int id )

Removes the specified viewport.
### Arguments

- *int* **id** - ID of the viewport.

## GroupData getGroupByIndex ( int index )

Returns the group with the specified index.
### Arguments

- *int* **index** - Index of the group, a value from 0 to the [total number of viewport groups](#getNumGroups_uint).

### Return value

[GroupData class](../../../../api/library/plugins/spidervision/class.groupdata_usc.md) instance that stores the group data.
## GroupData getGroup ( int id )

Returns the viewport group by the specified ID.
### Arguments

- *int* **id** - ID of the group.

### Return value

[GroupData class](../../../../api/library/plugins/spidervision/class.groupdata_usc.md) instance that stores the group data.
## GroupData createGroup ( int type )

Creates the group of the specified type.
### Arguments

- *int* **type** - Type of the group.

### Return value

[GroupData class](../../../../api/library/plugins/spidervision/class.groupdata_usc.md) instance that stores the group data.
## void removeGroup ( int id )

Removes the group with the specified ID.
### Arguments

- *int* **id** - ID of the group.

## CalibrationGridData getCalibrationGrid ( )

Returns the calibration grid for the configuration.
### Return value

[CalibrationGridData class](../../../../api/library/plugins/spidervision/class.calibrationgriddata_usc.md) instance that stores the calibration grid data.
## int hasUnsavedChanges ( )

Returns the value indicating if the displays configuration has any unsaved changes.
### Return value

**1** if the displays configuration has any unsaved changes, otherwise **0**.
## int loadConfig ( String filepath )

Loads the configuration from the specified source.
### Arguments

- *String* **filepath** - Path to the displays configuration file.

### Return value

**1** if the configuration file is loaded successfully, otherwise **0**.
## void loadConfig ( Stream stream )

Loads the configuration data from the specified source.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_usc.md)* **stream** - Stream to read data from.

## int saveConfig ( String filepath )

Saves the configuration the specified displays configuration file.
### Arguments

- *String* **filepath** - Path to the displays configuration file.

### Return value

**1** if the configuration file is saved successfully, otherwise **0**.
## void clear ( )

Clears the displays configuration.
## void saveXml ( Xml xml )

Saves the displays configuration data to the given instance of the Xml class.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_usc.md)* **xml** - [Xml class](../../../../api/library/common/class.xml_usc.md) instance into which the data will be saved.

## int restoreXml ( Xml xml )

Loads the displays configuration data from the specified instance of the Xml class.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_usc.md)* **xml** - [Xml class](../../../../api/library/common/class.xml_usc.md) instance the data from which is to be loaded.

### Return value

**1** if the data has been loaded successfully, otherwise **0**.
## void save ( Stream stream )

Saves the displays configuration data to the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_usc.md)* **stream** - Stream to which the data is to be written.

## void restore ( Stream stream )

Loads the displays configuration data from the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_usc.md)* **stream** - Stream the data from which is to be loaded.

## void loadConfig ( Xml stream )

Loads the configuration from the XML file.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_usc.md)* **stream** - [Xml class](../../../../api/library/common/class.xml_usc.md) instance the data from which is to be loaded.
