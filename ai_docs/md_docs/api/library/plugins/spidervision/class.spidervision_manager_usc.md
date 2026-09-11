# Unigine::Plugins::SpiderVision::Manager Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


This class provides auxiliary functions for configuring the plugin, as well as access to an object of [DisplaysConfig](../../../../api/library/plugins/spidervision/class.displaysconfig_usc.md) class.


## Manager Class

### Members

## DisplaysConfig getConfig () const

Returns the current *[DisplaysConfig](../../../../api/library/plugins/spidervision/class.displaysconfig_usc.md)* class instance that stores the complete configuration data.
### Return value

Current *[DisplaysConfig](../../../../api/library/plugins/spidervision/class.displaysconfig_usc.md)* class instance that stores the complete configuration data.
## void setComputerName ( String name )

Sets a new name of the computer on which the viewport is to be displayed. If this parameter is not set, the viewport can be displayed on any PC. If set, the viewport is only displayed on the PC that has a matching name.
### Arguments

- *String* **name** - The name of the computer on which the viewport is to be displayed.

## String getComputerName () const

Returns the current name of the computer on which the viewport is to be displayed. If this parameter is not set, the viewport can be displayed on any PC. If set, the viewport is only displayed on the PC that has a matching name.
### Return value

Current name of the computer on which the viewport is to be displayed.
## void setConfiguratorEnabled ( int enabled )

Sets a new value indicating if the configurator window is open.
### Arguments

- *int* **enabled** - The the configurator interface

## int isConfiguratorEnabled () const

Returns the current value indicating if the configurator window is open.
### Return value

Current the configurator interface
## static getEventComputerNameChanged () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
---

## int findViewportID ( )

Returns the of the viewport window with the specified name.
### Arguments

### Return value

ID of the viewport window with the specified name if it exists, otherwise -1.
## int findGroupID ( )

Returns the of the viewport group with the specified name.
### Arguments

### Return value

ID of the viewport group with the specified name if it exists, otherwise -1.
## void setProjectionEnabled ( int viewport_id , bool enabled )

Sets a value indicating if the projection for the specified viewport (correction of the image according to projection) is enabled. If disabled, the image is rendered as seen from the point of view without any distortions (i.e. regardless of the viewport plane position in the configuration space). If enabled, the image takes into account the projection angle (i.e. the viewport plane position relative to the point of view in the configuration space) and distorts the rendered image accordingly.
### Arguments

- *int* **viewport_id** - ID of the viewport window.
- *bool* **enabled** - true to enable [projection for the specified viewport](../../../../ig/index.md#interpolation); false - to disable.

## void setViewportCustomPlayer ( int viewport_id , Player player )

Assigns a player to the specified viewport.
### Arguments

- *int* **viewport_id** - ID of the viewport window.
- *[Player](../../../../api/library/players/class.player_usc.md)* **player** - The player camera.

## void setGroupCustomPlayer ( int group_id , Player player )

Assigns a player to the specified group of viewports.
### Arguments

- *int* **group_id** - ID of the viewport group.
- *[Player](../../../../api/library/players/class.player_usc.md)* **player** - The player camera.

## EngineWindowViewport getEngineWindow ( int viewport_id )

Returns the engine window viewport for the specified viewport.
### Arguments

- *int* **viewport_id** - ID of the viewport window.

### Return value

The engine window viewport.
## Player getViewportCustomPlayer ( int viewport_id )

Returns the custom player previously assigned to the given viewport's window via **[setViewportCustomPlayer()()](../../../...md#setViewportCustomPlayer_int_Player_void)**.
### Arguments

- *int* **viewport_id** - ID of the viewport.

### Return value

Custom player assigned to the viewport's window, or null if the viewport does not exist or no custom player is set (rendering then falls back to the game player).
