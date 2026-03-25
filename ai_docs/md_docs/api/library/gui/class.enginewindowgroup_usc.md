# Unigine::EngineWindowGroup Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** EngineWindow


The class to create and manage window groups. It allows arranging of multiple windows of a group into tabs, defining parameters of window group elements (such as tabs and window separators), and detecting intersections with nested windows. The picture below shows the elements of the window group:


![Window group elements](tab_bar_area.png)


There are three types of the window groups:


- Vertical
- Horizontal
- Group of tabs


Within the group, all windows are stacked according to one of these types.


### Creating a Window Group


A window group can be created in one of the following ways:


- You can create an empty group using one of the *EngineWindowGroup* class constructors and then add windows or other groups to it.
- You can stack windows using *[WindowManager](../../../api/library/gui/class.windowmanager_usc.md)* class functionality.


In this article, we will consider only the first one.


The following examples demonstrate how to create groups of different types using the *EngineWindowGroup* class and add nested windows to them:


### Editing a Window Group


Editing a window group involves modifying its elements such as tabs and separators, adding or removing nested windows, specifying an automatic deletion mode, and so on.


### Managing Groups


The *EngineWindowGroup* and base *EngineWindow* classes offer a range of functions that allow implementing custom logic for grouping and ungrouping windows. For example, you can do the following:


## EngineWindowGroup Class

### Members

---

## EngineWindowGroup ( int group_type , ivec2 size , int flags = 0 )

Constructor. Creates the window group of the specified type and size with the specified flags.
### Arguments

- *int* **group_type** - The type of the group.
- *ivec2* **size** - The size of the window group.
- *int* **flags** - Mask containing window [flags](../../../api/library/gui/class.enginewindow_usc.md#FLAGS_MAIN).

## EngineWindowGroup ( int group_type , int width , int height , int flags = 0 )

Constructor. Creates the window group of the specified type and size with the specified flags.
### Arguments

- *int* **group_type** - The type of the group.
- *int* **width** - Window width.
- *int* **height** - Window height.
- *int* **flags** - Mask containing window [flags](../../../api/library/gui/class.enginewindow_usc.md#FLAGS_MAIN).

## EngineWindowGroup ( int group_type , string window_title , int width , int height , int flags = 0 )

Constructor. Creates the window group of the specified type and size with the specified title and flags.
### Arguments

- *int* **group_type** - The type of the group.
- *string* **window_title** - The title of the window, in UTF-8 encoding.
- *int* **width** - Window width.
- *int* **height** - Window height.
- *int* **flags** - Mask containing window [flags](../../../api/library/gui/class.enginewindow_usc.md#FLAGS_MAIN).

## int getGroupType ( )

Returns the window group type set in the constructor — vertical, horizontal, tab arrangement of windows, or an independent window inside a group.
### Return value

The window group type.
## void setFixed ( int fixed )

Sets a value specifying if windows can be added to this group or removed from it.
### Arguments

- *int* **fixed** - **1** to disable adding or removing windows from this group, otherwise **0**.

## int isFixed ( )

Returns a value specifying if windows can be added to this group or removed from it.
### Return value

**1** if adding or removing windows from this group is disabled, otherwise **0**.
## void setAutoDeleteMode ( int mode )

Sets the automatic window deletion mode.
### Arguments

- *int* **mode** - The automatic window deletion mode.

## int getAutoDeleteMode ( )

Returns the automatic window deletion mode.
### Return value

The automatic window deletion mode.
## void add ( EngineWindow window , int target_index = -1 )

Adds a window at a specified index. The window becomes nested (i.e. its borders, style, title bar, etc. are disabled).
> **Notice:** If the group is [fixed](#isFixed_int), a window won't be added to the group and the console will display a corresponding warning.


### Arguments

- *[EngineWindow](../../../api/library/gui/class.enginewindow_usc.md)* **window** - Window to be added.
- *int* **target_index** - The window order. If no index is set, the window is added as the last one.

## void remove ( EngineWindow window )

Removes the specified window from the group. The window's settings are the same as before adding it to the group.
> **Notice:** If the group is [fixed](#isFixed_int), a window won't be removed from the group and the console will display a corresponding warning.


### Arguments

- *[EngineWindow](../../../api/library/gui/class.enginewindow_usc.md)* **window** - Window to be removed.

## void removeByIndex ( int index )

Removes the window at a specified index from the group. The window's settings are the same as before adding it to the group.
> **Notice:** If the group is [fixed](#isFixed_int), a window won't be removed from the group and the console will display a corresponding warning.


### Arguments

- *int* **index** - The index of the window to be removed.

## int getNumNestedWindows ( )

Returns the total number of nested windows in the group.
### Return value

The total number of nested windows in the group.
## EngineWindow getNestedWindow ( int index )

Returns the nested engine window by its index.
### Arguments

- *int* **index** - Index of the nested window.

### Return value

Nested engine window.
## int getNestedWindowIndex ( EngineWindow window )

Returns the index of the specified nested engine window.
### Arguments

- *[EngineWindow](../../../api/library/gui/class.enginewindow_usc.md)* **window** - Nested engine window.

### Return value

Index of the nested window.
## int containsNestedWindow ( EngineWindow window )

Returns the value indicating if the specified window is a direct child of the current group.
### Arguments

- *[EngineWindow](../../../api/library/gui/class.enginewindow_usc.md)* **window** - Window to be checked.

### Return value

**1** if the specified window is a direct child of the current one, otherwise **0**.
## int containsNestedWindowInHierarchy ( EngineWindow window )

Returns the value indicating if the specified window is a child of the current group or any of its children.
### Arguments

- *[EngineWindow](../../../api/library/gui/class.enginewindow_usc.md)* **window** - Window to be checked.

### Return value

**1** if the specified window is a child of the current one, otherwise **0**.
## void setTabTitle ( int index , string title )

Adds the title to the specified tab and the window itself.
### Arguments

- *int* **index** - Index of the tab.
- *string* **title** - Title to be added.

## void setTabIcon ( int index , Image image )

Adds the image to the specified tab and the window itself.
### Arguments

- *int* **index** - Index of the tab.
- *[Image](../../../api/library/common/class.image_usc.md)* **image** - Image to be added.

## int setCurrentTab ( )

Sets the index of the currently active tab in a tab group.
### Return value

The index of the tab to set as currently active.
## int getCurrentTab ( )

Returns the index of the currently active tab in a tab group.
### Return value

The index of the currently active tab.
## int getTabWidth ( int index )

Returns the width of the tab. Available for [horizontal](#GROUP_TYPE_HORIZONTAL) groups only.
### Arguments

- *int* **index** - The index of the tab.

### Return value

The width of the the tab.
## int getTabHeight ( int index )

Returns the height of the tab. Available for [vertical](#GROUP_TYPE_VERTICAL) groups only.
### Arguments

- *int* **index** - The index of the tab.

### Return value

The height of the tab.
## int getTabBarWidth ( int index )

Returns the width of the tab bar.
### Arguments

- *int* **index** - The index of the tab.

### Return value

The width of the tab bar.
## int getTabBarHeight ( int index )

Returns the height of the tab bar.
### Arguments

- *int* **index** - The index of the tab.

### Return value

The height of the tab bar.
## ivec2 getTabLocalPosition ( int index )

Returns the screen position of the tab relatively to the parent group (global window). The coordinates represent the displacement from the top left corner of the parent group (global window).
### Arguments

- *int* **index** - The index of the tab.

### Return value

The screen position of the tab relatively to the parent group (global window).
## ivec2 getTabBarLocalPosition ( int index )

Returns the screen position of the tab bar relatively to the parent group (global window). The coordinates represent the displacement from the top left corner of the parent group (global window).
### Arguments

- *int* **index** - The index of the tab.

### Return value

The screen position of the tab bar relatively to the parent group (global window).
## void setHorizontalTabWidth ( int index , int width )

Sets the width of the tab in the group of tabs arranged horizontally.
> **Notice:** You may need to call [*updateGuiHierarchy()*](../../../api/library/gui/class.enginewindow_usc.md#updateGuiHierarchy_void) first, if you have added a new window to the group and want to change its tab width immediately. Otherwise, you may get incorrect results.


### Arguments

- *int* **index** - The index of the tab.
- *int* **width** - The width of the tab in the group of tabs arranged horizontally.

## void setVerticalTabHeight ( int index , int height )

Sets the height of the tab in the group of tabs arranged vertically.
> **Notice:** You may need to call [*updateGuiHierarchy()*](../../../api/library/gui/class.enginewindow_usc.md#updateGuiHierarchy_void) first, if you have added a new window to the group and want to change its tab height immediately. Otherwise, you may get incorrect results.


### Arguments

- *int* **index** - The index of the tab.
- *int* **height** - The height of the tab in the group of tabs arranged vertically.

## int getSeparatorWidth ( )

Returns the width of the vertical line separating a tab group from the rest of the area.
> **Notice:** You may need to call [*updateGuiHierarchy()*](../../../api/library/gui/class.enginewindow_usc.md#updateGuiHierarchy_void) first, if you have added a new window to the group and want to access its separator immediately. Otherwise, you may get incorrect results.


### Return value

The width of the separation line, in pixels.
## int getSeparatorHeight ( )

Returns the height of the horizontal line separating a tab group from the rest of the area.
> **Notice:** You may need to call [*updateGuiHierarchy()*](../../../api/library/gui/class.enginewindow_usc.md#updateGuiHierarchy_void) first, if you have added a new window to the group and want to access its separator immediately. Otherwise, you may get incorrect results.


### Return value

The height of the separation line, in pixels.
## void setSeparatorPosition ( int index , int pos )

Sets the position of the line separating a tab group from the rest of the area. The separator line can be horizontal or vertical depending on the [group type](#getGroupType_int).
> **Notice:** You may need to call [*updateGuiHierarchy()*](../../../api/library/gui/class.enginewindow_usc.md#updateGuiHierarchy_void) first, if you have added a new window to the group and want to change its separator immediately. Otherwise, you may get incorrect results.


### Arguments

- *int* **index** - Index of the tab.
- *int* **pos** - Position of the separation line, in pixels, from the top-left corner of the window.

## int getSeparatorPosition ( int index )

Returns the position of the line separating a tab group from the rest of the area. The separator line can be horizontal or vertical depending on the [group type](#getGroupType_int).
> **Notice:** You may need to call [*updateGuiHierarchy()*](../../../api/library/gui/class.enginewindow_usc.md#updateGuiHierarchy_void) first, if you have added a new window to the group and want to access its separator immediately. Otherwise, you may get incorrect results.


### Arguments

- *int* **index** - Index of the tab.

### Return value

Position of the separation line, in pixels, from the top-left corner of the window.
## void setSeparatorValue ( int index , float value )

Sets the relative position of the tab separator.
> **Notice:** You may need to call [*updateGuiHierarchy()*](../../../api/library/gui/class.enginewindow_usc.md#updateGuiHierarchy_void) first, if you have added a new window to the group and want to change its separator immediately. Otherwise, you may get incorrect results.


### Arguments

- *int* **index** - Index of the tab.
- *float* **value** - Position of the tab separator, the value from 0 to 1 that is recalculated to pixels.

## float getSeparatorValue ( int index )

Returns the relative position of the tab separator.
> **Notice:** You may need to call [*updateGuiHierarchy()*](../../../api/library/gui/class.enginewindow_usc.md#updateGuiHierarchy_void) first, if you have added a new window to the group and want to access its separator immediately. Otherwise, you may get incorrect results.


### Arguments

- *int* **index** - Index of the tab.

### Return value

Position of the tab separator, the value from 0 to 1.
## void swapTabs ( int first , int second )

Swaps the specified tabs.
> **Notice:** If the group is [fixed](#isFixed_int), tabs won't be swapped and the console will display a corresponding warning.


### Arguments

- *int* **first** - Index of the first tab.
- *int* **second** - Index of the second tab.

## int getIntersectionTabBar ( ivec2 global_mouse_pos )

Returns the value indicating if the mouse is hovering over the window tab bar.
### Arguments

- *ivec2* **global_mouse_pos** - Global screen coordinates of the mouse relative to the main display.

### Return value

1 if the mouse hovers over the window tab bar, otherwise 0.
## int getIntersectionTabBarArea ( ivec2 global_mouse_pos )

Returns the value indicating if the mouse is hovering over the window tab bar area.
### Arguments

- *ivec2* **global_mouse_pos** - Global screen coordinates of the mouse relative to the main display.

### Return value

1 if the mouse hovers over the window tab bar area, otherwise 0.
## ivec2 getIntersectedItemPosition ( )

Returns the position of the left top corner of the intersected group item in the screen coordinates. In case of several displays, the position is relative to the main display.
### Return value

The screen position of the intersected item — coordinates of the left top corner.
## ivec2 getIntersectedItemSize ( )

Returns the size of the intersected item.
### Return value

The size of the intersected item, in pixels.
