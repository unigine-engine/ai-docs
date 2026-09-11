# Unigine::EngineWindowGroup Class (CPP)

**Header:** #include <UnigineWindowManager.h>

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
- You can stack windows using *[WindowManager](../../../api/library/gui/class.windowmanager_cpp.md)* class functionality.


In this article, we will consider only the first one.


The following examples demonstrate how to create groups of different types using the *EngineWindowGroup* class and add nested windows to them:


<details>
<summary>Horizontal Group</summary>

```cpp
// create separate windows that will be grouped
EngineWindowViewportPtr horizontal_1 = EngineWindowViewport::create("Horizontal 1", 512, 256);
EngineWindowViewportPtr horizontal_2 = EngineWindowViewport::create("Horizontal 2", 512, 256);
EngineWindowViewportPtr horizontal_3 = EngineWindowViewport::create("Horizontal 3", 512, 256);

// create a horizontal group
auto horizontal_group = EngineWindowGroup::create(EngineWindowGroup::GROUP_TYPE_HORIZONTAL, "Horizontal Group", 565, 310);
// add windows to the group
horizontal_group->add(horizontal_1);
horizontal_group->add(horizontal_2);
horizontal_group->add(horizontal_3);
// set a position of the group
horizontal_group->setPosition(Math::ivec2(50, 60));

// render the group
horizontal_group->show();


```

</details>


<details>
<summary>Vertical Group</summary>

```cpp
// create separate windows that will be grouped
EngineWindowViewportPtr vertical_1 = EngineWindowViewport::create("Vertical 1", 512, 256);
EngineWindowViewportPtr vertical_2 = EngineWindowViewport::create("Vertical 2", 512, 256);
EngineWindowViewportPtr vertical_3 = EngineWindowViewport::create("Vertical 3", 512, 256);

// create a vertical group
auto vertical_group = EngineWindowGroup::create(EngineWindowGroup::GROUP_TYPE_VERTICAL, "Vertical Group", 305, 670);
// add windows to the group
vertical_group->add(vertical_1);
vertical_group->add(vertical_2);
vertical_group->add(vertical_3);
// set a position of the group
vertical_group->setPosition(Math::ivec2(665, 60));
// render the group
vertical_group->show();


```

</details>


<details>
<summary>Group of Tabs</summary>

```cpp
// create separate windows that will be grouped
EngineWindowViewportPtr tab_1 = EngineWindowViewport::create("Tab 1", 512, 256);
EngineWindowViewportPtr tab_2 = EngineWindowViewport::create("Tab 2", 512, 256);
EngineWindowViewportPtr tab_3 = EngineWindowViewport::create("Tab 3", 512, 256);

// create a group of tabs
auto tab_group = EngineWindowGroup::create(EngineWindowGroup::GROUP_TYPE_TAB, "Tab Group", 565, 310);
tab_group->add(tab_1);
tab_group->add(tab_2);
tab_group->add(tab_3);
// set a position of the group
tab_group->setPosition(Math::ivec2(50, 420));
// render the group
tab_group->show();


```

</details>


### Editing a Window Group


Editing a window group involves modifying its elements such as tabs and separators, adding or removing nested windows, specifying an automatic deletion mode, and so on.


> **Notice:** You may need to call [*updateGuiHierarchy()*](../../../api/library/gui/class.enginewindow_cpp.md#updateGuiHierarchy_void) first, if you have added a new window to the group and want to access its settings immediately. Otherwise, you may get incorrect results.


<details>
<summary>AppSystemLogic.cpp</summary>

```cpp
// create separate windows that will be grouped
EngineWindowViewportPtr horizontal_1 = EngineWindowViewport::create("Horizontal 1", 512, 256);
EngineWindowViewportPtr horizontal_2 = EngineWindowViewport::create("Horizontal 2", 512, 256);
EngineWindowViewportPtr horizontal_3 = EngineWindowViewport::create("Horizontal 3", 512, 256);

// create a horizontal group
auto horizontal_group = EngineWindowGroup::create(EngineWindowGroup::GROUP_TYPE_HORIZONTAL, "Horizontal Group", 565, 310);
// add windows to the group
horizontal_group->add(horizontal_1);
horizontal_group->add(horizontal_2);
horizontal_group->add(horizontal_3);
// set a position of the group
horizontal_group->setPosition(Math::ivec2(50, 60));

// update a hierarchy in self gui of the group
horizontal_group->updateGuiHierarchy();

int position_offset = 100;
float value_offset = 0.2f;

for (int i = 0; i < horizontal_group->getNumNestedWindows(); i++)
{
	// change a tab
	horizontal_group->setTabTitle(i, "New name " + String::itoa(i));
	if (i == 0) horizontal_group->setHorizontalTabWidth(i, position_offset);

	// change a separator
	horizontal_group->setSeparatorValue(i, horizontal_group->getSeparatorValue(i) + value_offset);
}

// render the group
horizontal_group->show();


```

</details>


### Managing Groups


The *EngineWindowGroup* and base *EngineWindow* classes offer a range of functions that allow implementing custom logic for grouping and ungrouping windows. For example, you can do the following:


- Control [whether the group can be modified](#isFixed_int) (i.e. whether new windows can be added and the nested windows can be removed).
- Check if a window can be [added to the group](../../../api/library/gui/class.enginewindow_cpp.md#isCanBeNested_int)
- [Access](#getNestedWindow_int_EngineWindow) the nested windows
- Specify the [automatic deletion mode](#setAutoDeleteMode_int_void)


And more, providing you with flexible control over the grouping logic.


### See Also


- A set of `SDK samples` demonstrating various usage aspects, including:

  -
  -


## EngineWindowGroup Class

### Enums

## GROUP_TYPE

| Name | Description |
|---|---|
| **GROUP_TYPE_NONE** = 0 | A separate window inside the group. |
| **GROUP_TYPE_TAB** = 1 | Windows are arranged into a group of tabs with a selected window displayed atop the others in the group. |
| **GROUP_TYPE_HORIZONTAL** = 2 | Windows are arranged into a horizontally displayed group. |
| **GROUP_TYPE_VERTICAL** = 3 | Windows are arranged into a vertically displayed group. |

## AUTO_DELETE_MODE

| Name | Description |
|---|---|
| **AUTO_DELETE_MODE_NONE** = 0 | Automatic deletion of the window is disabled. |
| **AUTO_DELETE_MODE_EMPTY** = 1 | A window group is deleted automatically if it doesn't contain any nested windows. |
| **AUTO_DELETE_MODE_SINGLE_WINDOW** = 2 | A group is deleted automatically, if only one window is left. If this was a child group, it is automatically transformed to a child window. |

### Members

## EngineWindowGroup::GROUP_TYPE getGroupType () const

Returns the current type of the window group set in the constructor.
### Return value

Current type of the window group set in the constructor
## void setFixed ( bool fixed )

Sets a new value indicating if this group is protected from adding/removing windows.
### Arguments

- *bool* **fixed** - Set **true** to enable protection of the group from modification (adding or removing windows); **false** - to disable it.

## bool isFixed () const

Returns the current value indicating if this group is protected from adding/removing windows.
### Return value

**true** if protection of the group from modification (adding or removing windows) is enabled ; otherwise **false**.
## void setAutoDeleteMode ( EngineWindowGroup::AUTO_DELETE_MODE mode )

Sets a new automatic window deletion mode.
### Arguments

- *[EngineWindowGroup::AUTO_DELETE_MODE](../../../api/library/gui/class.enginewindowgroup_cpp.md#AUTO_DELETE_MODE)* **mode** - The automatic window deletion mode

## EngineWindowGroup::AUTO_DELETE_MODE getAutoDeleteMode () const

Returns the current automatic window deletion mode.
### Return value

Current automatic window deletion mode
## int getNumNestedWindows () const

Returns the current total number of nested windows in the group.
### Return value

Current total number of nested windows in the group
## void setCurrentTab ( int tab )

Sets a new index of the currently active tab in a tab group.
### Arguments

- *int* **tab** - The index of the currently active tab in a tab group

## int getCurrentTab () const

Returns the current index of the currently active tab in a tab group.
### Return value

Current index of the currently active tab in a tab group
## int getSeparatorWidth () const

Returns the current width of the vertical line separating a tab group from the rest of the area, in pixels.
> **Notice:** You may need to call [*updateGuiHierarchy()*](../../../api/library/gui/class.enginewindow_cpp.md#updateGuiHierarchy_void) first, if you have added a new window to the group and want to access its separator immediately. Otherwise, you may get incorrect results.


### Return value

Current width of the vertical line separating a tab group from the rest of the area, in pixels
## int getSeparatorHeight () const

Returns the current height of the horizontal line separating a tab group from the rest of the area, in pixels.
> **Notice:** You may need to call [*updateGuiHierarchy()*](../../../api/library/gui/class.enginewindow_cpp.md#updateGuiHierarchy_void) first, if you have added a new window to the group and want to access its separator immediately. Otherwise, you may get incorrect results.


### Return value

Current height of the horizontal line separating a tab group from the rest of the area, in pixels
## Math:: ivec2 getIntersectedItemPosition () const

Returns the current position of the left top corner of the intersected group item, in screen coordinates. In case of several displays, the position is relative to the main display.
### Return value

Current position of the left top corner of the intersected group item, in screen coordinates
## Math:: ivec2 getIntersectedItemSize () const

Returns the current size of the intersected group item, in pixels.
### Return value

Current size of the intersected group item, in pixels
---

## EngineWindowGroup ( EngineWindowGroup::GROUP_TYPE group_type , const Math:: ivec2 & size , int flags = 0 )

Constructor. Creates the window group of the specified type and size with the specified flags.
### Arguments

- *[EngineWindowGroup::GROUP_TYPE](../../../api/library/gui/class.enginewindowgroup_cpp.md#GROUP_TYPE)* **group_type** - The type of the group.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **size** - The size of the window group.
- *int* **flags** - Mask containing window [flags](../../../api/library/gui/class.enginewindow_cpp.md#FLAGS_MAIN).

## EngineWindowGroup ( EngineWindowGroup::GROUP_TYPE group_type , int width , int height , int flags = 0 )

Constructor. Creates the window group of the specified type and size with the specified flags.
### Arguments

- *[EngineWindowGroup::GROUP_TYPE](../../../api/library/gui/class.enginewindowgroup_cpp.md#GROUP_TYPE)* **group_type** - The type of the group.
- *int* **width** - Window width.
- *int* **height** - Window height.
- *int* **flags** - Mask containing window [flags](../../../api/library/gui/class.enginewindow_cpp.md#FLAGS_MAIN).

## EngineWindowGroup ( EngineWindowGroup::GROUP_TYPE group_type , const char * window_title , int width , int height , int flags = 0 )

Constructor. Creates the window group of the specified type and size with the specified title and flags.
### Arguments

- *[EngineWindowGroup::GROUP_TYPE](../../../api/library/gui/class.enginewindowgroup_cpp.md#GROUP_TYPE)* **group_type** - The type of the group.
- *const char ** **window_title** - The title of the window, in UTF-8 encoding.
- *int* **width** - Window width.
- *int* **height** - Window height.
- *int* **flags** - Mask containing window [flags](../../../api/library/gui/class.enginewindow_cpp.md#FLAGS_MAIN).

## void add ( const Ptr < EngineWindow > & window , int target_index = -1 )

Adds a window at a specified index. The window becomes nested (i.e. its borders, style, title bar, etc. are disabled).
> **Notice:** If the group is [fixed](#isFixed_int), a window won't be added to the group and the console will display a corresponding warning.


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[EngineWindow](../../../api/library/gui/class.enginewindow_cpp.md)> &* **window** - Window to be added.
- *int* **target_index** - The window order. If no index is set, the window is added as the last one.

## void remove ( const Ptr < EngineWindow > & window )

Removes the specified window from the group. The window's settings are the same as before adding it to the group.
> **Notice:** If the group is [fixed](#isFixed_int), a window won't be removed from the group and the console will display a corresponding warning.


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[EngineWindow](../../../api/library/gui/class.enginewindow_cpp.md)> &* **window** - Window to be removed.

## void removeByIndex ( int index )

Removes the window at a specified index from the group. The window's settings are the same as before adding it to the group.
> **Notice:** If the group is [fixed](#isFixed_int), a window won't be removed from the group and the console will display a corresponding warning.


### Arguments

- *int* **index** - The index of the window to be removed.

## Ptr < EngineWindow > getNestedWindow ( int index ) const

Returns the nested engine window by its index.
### Arguments

- *int* **index** - Index of the nested window.

### Return value

Nested engine window.
## int getNestedWindowIndex ( const Ptr < EngineWindow > & window )

Returns the index of the specified nested engine window.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[EngineWindow](../../../api/library/gui/class.enginewindow_cpp.md)> &* **window** - Nested engine window.

### Return value

Index of the nested window.
## bool containsNestedWindow ( const Ptr < EngineWindow > & window ) const

Returns the value indicating if the specified window is a direct child of the current group.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[EngineWindow](../../../api/library/gui/class.enginewindow_cpp.md)> &* **window** - Window to be checked.

### Return value

true if the specified window is a direct child of the current one, otherwise false.
## bool containsNestedWindowInHierarchy ( const Ptr < EngineWindow > & window ) const

Returns the value indicating if the specified window is a child of the current group or any of its children.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[EngineWindow](../../../api/library/gui/class.enginewindow_cpp.md)> &* **window** - Window to be checked.

### Return value

true if the specified window is a child of the current one, otherwise false.
## void setTabTitle ( int index , const char * title )

Adds the title to the specified tab and the window itself.
### Arguments

- *int* **index** - Index of the tab.
- *const char ** **title** - Title to be added.

## void setTabIcon ( int index , const Ptr < Image > & image )

Adds the image to the specified tab and the window itself.
### Arguments

- *int* **index** - Index of the tab.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Image to be added.

## int getTabWidth ( int index ) const

Returns the width of the tab. Available for [horizontal](#GROUP_TYPE_HORIZONTAL) groups only.
### Arguments

- *int* **index** - The index of the tab.

### Return value

The width of the tab.
## int getTabHeight ( int index ) const

Returns the height of the tab. Available for [vertical](#GROUP_TYPE_VERTICAL) groups only.
### Arguments

- *int* **index** - The index of the tab.

### Return value

The height of the tab.
## int getTabBarWidth ( int index ) const

Returns the width of the tab bar.
### Arguments

- *int* **index** - The index of the tab.

### Return value

The width of the tab bar.
## int getTabBarHeight ( int index ) const

Returns the height of the tab bar.
### Arguments

- *int* **index** - The index of the tab.

### Return value

The height of the tab bar.
## Math:: ivec2 getTabLocalPosition ( int index ) const

Returns the screen position of the tab relatively to the parent group (global window). The coordinates represent the displacement from the top left corner of the parent group (global window).
### Arguments

- *int* **index** - The index of the tab.

### Return value

The screen position of the tab relatively to the parent group (global window).
## Math:: ivec2 getTabBarLocalPosition ( int index ) const

Returns the screen position of the tab bar relatively to the parent group (global window). The coordinates represent the displacement from the top left corner of the parent group (global window).
### Arguments

- *int* **index** - The index of the tab.

### Return value

The screen position of the tab bar relatively to the parent group (global window).
## void setHorizontalTabWidth ( int index , int width )

Sets the width of the tab in the group of tabs arranged horizontally.
> **Notice:** You may need to call [*updateGuiHierarchy()*](../../../api/library/gui/class.enginewindow_cpp.md#updateGuiHierarchy_void) first, if you have added a new window to the group and want to change its tab width immediately. Otherwise, you may get incorrect results.


### Arguments

- *int* **index** - The index of the tab.
- *int* **width** - The width of the tab in the group of tabs arranged horizontally.

## void setVerticalTabHeight ( int index , int height )

Sets the height of the tab in the group of tabs arranged vertically.
> **Notice:** You may need to call [*updateGuiHierarchy()*](../../../api/library/gui/class.enginewindow_cpp.md#updateGuiHierarchy_void) first, if you have added a new window to the group and want to change its tab height immediately. Otherwise, you may get incorrect results.


### Arguments

- *int* **index** - The index of the tab.
- *int* **height** - The height of the tab in the group of tabs arranged vertically.

## void setSeparatorPosition ( int index , int pos )

Sets the position of the line separating a tab group from the rest of the area. The separator line can be horizontal or vertical depending on the [group type](#getGroupType_int).
> **Notice:** You may need to call [*updateGuiHierarchy()*](../../../api/library/gui/class.enginewindow_cpp.md#updateGuiHierarchy_void) first, if you have added a new window to the group and want to change its separator immediately. Otherwise, you may get incorrect results.


### Arguments

- *int* **index** - Index of the tab.
- *int* **pos** - Position of the separation line, in pixels, from the top-left corner of the window.

## int getSeparatorPosition ( int index ) const

Returns the position of the line separating a tab group from the rest of the area. The separator line can be horizontal or vertical depending on the [group type](#getGroupType_int).
> **Notice:** You may need to call [*updateGuiHierarchy()*](../../../api/library/gui/class.enginewindow_cpp.md#updateGuiHierarchy_void) first, if you have added a new window to the group and want to access its separator immediately. Otherwise, you may get incorrect results.


### Arguments

- *int* **index** - Index of the tab.

### Return value

Position of the separation line, in pixels, from the top-left corner of the window.
## void setSeparatorValue ( int index , float value )

Sets the relative position of the tab separator.
> **Notice:** You may need to call [*updateGuiHierarchy()*](../../../api/library/gui/class.enginewindow_cpp.md#updateGuiHierarchy_void) first, if you have added a new window to the group and want to change its separator immediately. Otherwise, you may get incorrect results.


### Arguments

- *int* **index** - Index of the tab.
- *float* **value** - Position of the tab separator, the value from 0 to 1 that is recalculated to pixels.

## float getSeparatorValue ( int index ) const

Returns the relative position of the tab separator.
> **Notice:** You may need to call [*updateGuiHierarchy()*](../../../api/library/gui/class.enginewindow_cpp.md#updateGuiHierarchy_void) first, if you have added a new window to the group and want to access its separator immediately. Otherwise, you may get incorrect results.


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

## int getIntersectionTabBar ( const Math:: ivec2 & global_mouse_pos )

Returns the value indicating if the mouse is hovering over the window tab bar.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **global_mouse_pos** - Global screen coordinates of the mouse relative to the main display.

### Return value

1 if the mouse hovers over the window tab bar, otherwise 0.
## int getIntersectionTabBarArea ( const Math:: ivec2 & global_mouse_pos )

Returns the value indicating if the mouse is hovering over the window tab bar area.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **global_mouse_pos** - Global screen coordinates of the mouse relative to the main display.

### Return value

1 if the mouse hovers over the window tab bar area, otherwise 0.
