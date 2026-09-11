# Unigine::EngineWindowGroup Class (CS)

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
- You can stack windows using *[WindowManager](../../../api/library/gui/class.windowmanager_cs.md)* class functionality.


In this article, we will consider only the first one.


The following examples demonstrate how to create groups of different types using the *EngineWindowGroup* class and add nested windows to them:


<details>
<summary>Horizontal Group</summary>

```csharp
// create separate windows that will be grouped
EngineWindowViewport horizontal_1 = new EngineWindowViewport("Horizontal 1", 512, 256);
EngineWindowViewport horizontal_2 = new EngineWindowViewport("Horizontal 2", 512, 256);
EngineWindowViewport horizontal_3 = new EngineWindowViewport("Horizontal 3", 512, 256);

// create a horizontal group
EngineWindowGroup horizontal_group = new EngineWindowGroup(EngineWindowGroup.GROUP_TYPE.HORIZONTAL, "Horizontal Group", 565, 310);
// add windows to the group
horizontal_group.Add(horizontal_1);
horizontal_group.Add(horizontal_2);
horizontal_group.Add(horizontal_3);
// set a position of the group
horizontal_group.Position = new ivec2(50, 60);

// render the group
horizontal_group.Show();


```

</details>


<details>
<summary>Vertical Group</summary>

```csharp
// create separate windows that will be grouped
EngineWindowViewport vertical_1 = new EngineWindowViewport("Vertical 1", 512, 256);
EngineWindowViewport vertical_2 = new EngineWindowViewport("Vertical 1", 512, 256);
EngineWindowViewport vertical_3 = new EngineWindowViewport("Vertical 1", 512, 256);

// create a vertical group
EngineWindowGroup vertical_group = new EngineWindowGroup(EngineWindowGroup.GROUP_TYPE.VERTICAL, "Vertical Group", 305, 670);
// add windows to the group
vertical_group.Add(vertical_1);
vertical_group.Add(vertical_2);
vertical_group.Add(vertical_3);
// set a position of the group
vertical_group.Position = new ivec2(665, 60);
// render the group
vertical_group.Show();


```

</details>


<details>
<summary>Group of Tabs</summary>

```csharp
// create separate windows that will be grouped
EngineWindowViewport tab_1 = new EngineWindowViewport("Tab 1", 512, 256);
EngineWindowViewport tab_2 = new EngineWindowViewport("Tab 2", 512, 256);
EngineWindowViewport tab_3 = new EngineWindowViewport("Tab 3", 512, 256);

// create a group of tabs
EngineWindowGroup tab_group = new EngineWindowGroup(EngineWindowGroup.GROUP_TYPE.TAB, "Tab Group", 565, 310);
tab_group.Add(tab_1);
tab_group.Add(tab_2);
tab_group.Add(tab_3);
// set a position of the group
tab_group.Position = new ivec2(50, 420);
// render the group
tab_group.Show();


```

</details>


### Editing a Window Group


Editing a window group involves modifying its elements such as tabs and separators, adding or removing nested windows, specifying an automatic deletion mode, and so on.


> **Notice:** You may need to call [*UpdateGuiHierarchy()*](../../../api/library/gui/class.enginewindow_cs.md#updateGuiHierarchy_void) first, if you have added a new window to the group and want to access its settings immediately. Otherwise, you may get incorrect results.


<details>
<summary>EngineWindowGroupClass.cs</summary>

```csharp
// create separate windows that will be grouped
EngineWindowViewport horizontal_1 = new EngineWindowViewport("Horizontal 1", 512, 256);
EngineWindowViewport horizontal_2 = new EngineWindowViewport("Horizontal 2", 512, 256);
EngineWindowViewport horizontal_3 = new EngineWindowViewport("Horizontal 3", 512, 256);

// create a horizontal group
EngineWindowGroup horizontal_group = new EngineWindowGroup(EngineWindowGroup.GROUP_TYPE.HORIZONTAL, "Horizontal Group", 565, 310);
// add windows to the group
horizontal_group.Add(horizontal_1);
horizontal_group.Add(horizontal_2);
horizontal_group.Add(horizontal_3);
// set a position of the group
horizontal_group.Position = new ivec2(50, 60);

// update a hierarchy in self gui of the group
horizontal_group.UpdateGuiHierarchy();

int position_offset = 100;
float value_offset = 0.2f;

for (int i = 0; i < horizontal_group.NumNestedWindows; i++)
{
	// change a tab
	horizontal_group.SetTabTitle(i, "New name " + i.ToString());
	if (i == 0) horizontal_group.SetHorizontalTabWidth(i, position_offset);

	// change a separator
	horizontal_group.SetSeparatorValue(i, horizontal_group.GetSeparatorValue(i) + value_offset);
}

// render the group
horizontal_group.Show();


```

</details>


### Managing Groups


The *EngineWindowGroup* and base *EngineWindow* classes offer a range of functions that allow implementing custom logic for grouping and ungrouping windows. For example, you can do the following:


- Control [whether the group can be modified](#Fixed) (i.e. whether new windows can be added and the nested windows can be removed).
- Check if a window can be [added to the group](../../../api/library/gui/class.enginewindow_cs.md#CanBeNested)
- [Access](#getNestedWindow_int_EngineWindow) the nested windows
- Specify the [automatic deletion mode](#AutoDeleteMode)


And more, providing you with flexible control over the grouping logic.


## EngineWindowGroup Class

### Enums

## GROUP_TYPE

| Name | Description |
|---|---|
| **NONE** = 0 | A separate window inside the group. |
| **TAB** = 1 | Windows are arranged into a group of tabs with a selected window displayed atop the others in the group. |
| **HORIZONTAL** = 2 | Windows are arranged into a horizontally displayed group. |
| **VERTICAL** = 3 | Windows are arranged into a vertically displayed group. |

## AUTO_DELETE_MODE

| Name | Description |
|---|---|
| **NONE** = 0 | Automatic deletion of the window is disabled. |
| **EMPTY** = 1 | A window group is deleted automatically if it doesn't contain any nested windows. |
| **SINGLE_WINDOW** = 2 | A group is deleted automatically, if only one window is left. If this was a child group, it is automatically transformed to a child window. |

### Properties

## 🔒︎ EngineWindowGroup.GROUP_TYPE GroupType

The type of the window group set in the constructor.
## bool Fixed

The value indicating if this group is protected from adding/removing windows.
## EngineWindowGroup.AUTO_DELETE_MODE AutoDeleteMode

The automatic window deletion mode.
## 🔒︎ int NumNestedWindows

The total number of nested windows in the group.
## int CurrentTab

The index of the currently active tab in a tab group.
## 🔒︎ int SeparatorWidth

The width of the vertical line separating a tab group from the rest of the area, in pixels.
> **Notice:** You may need to call [*updateGuiHierarchy()*](../../../api/library/gui/class.enginewindow_cs.md#updateGuiHierarchy_void) first, if you have added a new window to the group and want to access its separator immediately. Otherwise, you may get incorrect results.


## 🔒︎ int SeparatorHeight

The height of the horizontal line separating a tab group from the rest of the area, in pixels.
> **Notice:** You may need to call [*updateGuiHierarchy()*](../../../api/library/gui/class.enginewindow_cs.md#updateGuiHierarchy_void) first, if you have added a new window to the group and want to access its separator immediately. Otherwise, you may get incorrect results.


## 🔒︎ ivec2 IntersectedItemPosition

The position of the left top corner of the intersected group item, in screen coordinates. In case of several displays, the position is relative to the main display.
## 🔒︎ ivec2 IntersectedItemSize

The size of the intersected group item, in pixels.
### Members

---

## EngineWindowGroup ( EngineWindowGroup.GROUP_TYPE group_type , ivec2 size , int flags = 0 )

Constructor. Creates the window group of the specified type and size with the specified flags.
### Arguments

- *[EngineWindowGroup.GROUP_TYPE](../../../api/library/gui/class.enginewindowgroup_cs.md#GROUP_TYPE)* **group_type** - The type of the group.
- *ivec2* **size** - The size of the window group.
- *int* **flags** - Mask containing window [flags](../../../api/library/gui/class.enginewindow_cs.md#FLAGS).

## EngineWindowGroup ( EngineWindowGroup.GROUP_TYPE group_type , int width , int height , int flags = 0 )

Constructor. Creates the window group of the specified type and size with the specified flags.
### Arguments

- *[EngineWindowGroup.GROUP_TYPE](../../../api/library/gui/class.enginewindowgroup_cs.md#GROUP_TYPE)* **group_type** - The type of the group.
- *int* **width** - Window width.
- *int* **height** - Window height.
- *int* **flags** - Mask containing window [flags](../../../api/library/gui/class.enginewindow_cs.md#FLAGS).

## EngineWindowGroup ( EngineWindowGroup.GROUP_TYPE group_type , string window_title , int width , int height , int flags = 0 )

Constructor. Creates the window group of the specified type and size with the specified title and flags.
### Arguments

- *[EngineWindowGroup.GROUP_TYPE](../../../api/library/gui/class.enginewindowgroup_cs.md#GROUP_TYPE)* **group_type** - The type of the group.
- *string* **window_title** - The title of the window, in UTF-8 encoding.
- *int* **width** - Window width.
- *int* **height** - Window height.
- *int* **flags** - Mask containing window [flags](../../../api/library/gui/class.enginewindow_cs.md#FLAGS).

## void Add ( EngineWindow window , int target_index = -1 )

Adds a window at a specified index. The window becomes nested (i.e. its borders, style, title bar, etc. are disabled).
> **Notice:** If the group is [fixed](#isFixed_int), a window won't be added to the group and the console will display a corresponding warning.


### Arguments

- *[EngineWindow](../../../api/library/gui/class.enginewindow_cs.md)* **window** - Window to be added.
- *int* **target_index** - The window order. If no index is set, the window is added as the last one.

## void Remove ( EngineWindow window )

Removes the specified window from the group. The window's settings are the same as before adding it to the group.
> **Notice:** If the group is [fixed](#isFixed_int), a window won't be removed from the group and the console will display a corresponding warning.


### Arguments

- *[EngineWindow](../../../api/library/gui/class.enginewindow_cs.md)* **window** - Window to be removed.

## void RemoveByIndex ( int index )

Removes the window at a specified index from the group. The window's settings are the same as before adding it to the group.
> **Notice:** If the group is [fixed](#isFixed_int), a window won't be removed from the group and the console will display a corresponding warning.


### Arguments

- *int* **index** - The index of the window to be removed.

## EngineWindow GetNestedWindow ( int index )

Returns the nested engine window by its index.
### Arguments

- *int* **index** - Index of the nested window.

### Return value

Nested engine window.
## int GetNestedWindowIndex ( EngineWindow window )

Returns the index of the specified nested engine window.
### Arguments

- *[EngineWindow](../../../api/library/gui/class.enginewindow_cs.md)* **window** - Nested engine window.

### Return value

Index of the nested window.
## bool ContainsNestedWindow ( EngineWindow window )

Returns the value indicating if the specified window is a direct child of the current group.
### Arguments

- *[EngineWindow](../../../api/library/gui/class.enginewindow_cs.md)* **window** - Window to be checked.

### Return value

true if the specified window is a direct child of the current one, otherwise false.
## bool ContainsNestedWindowInHierarchy ( EngineWindow window )

Returns the value indicating if the specified window is a child of the current group or any of its children.
### Arguments

- *[EngineWindow](../../../api/library/gui/class.enginewindow_cs.md)* **window** - Window to be checked.

### Return value

true if the specified window is a child of the current one, otherwise false.
## void SetTabTitle ( int index , string title )

Adds the title to the specified tab and the window itself.
### Arguments

- *int* **index** - Index of the tab.
- *string* **title** - Title to be added.

## void SetTabIcon ( int index , Image image )

Adds the image to the specified tab and the window itself.
### Arguments

- *int* **index** - Index of the tab.
- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image to be added.

## int GetTabWidth ( int index )

Returns the width of the tab. Available for [horizontal](#GROUP_TYPE_HORIZONTAL) groups only.
### Arguments

- *int* **index** - The index of the tab.

### Return value

The width of the tab.
## int GetTabHeight ( int index )

Returns the height of the tab. Available for [vertical](#GROUP_TYPE_VERTICAL) groups only.
### Arguments

- *int* **index** - The index of the tab.

### Return value

The height of the tab.
## int GetTabBarWidth ( int index )

Returns the width of the tab bar.
### Arguments

- *int* **index** - The index of the tab.

### Return value

The width of the tab bar.
## int GetTabBarHeight ( int index )

Returns the height of the tab bar.
### Arguments

- *int* **index** - The index of the tab.

### Return value

The height of the tab bar.
## ivec2 GetTabLocalPosition ( int index )

Returns the screen position of the tab relatively to the parent group (global window). The coordinates represent the displacement from the top left corner of the parent group (global window).
### Arguments

- *int* **index** - The index of the tab.

### Return value

The screen position of the tab relatively to the parent group (global window).
## ivec2 GetTabBarLocalPosition ( int index )

Returns the screen position of the tab bar relatively to the parent group (global window). The coordinates represent the displacement from the top left corner of the parent group (global window).
### Arguments

- *int* **index** - The index of the tab.

### Return value

The screen position of the tab bar relatively to the parent group (global window).
## void SetHorizontalTabWidth ( int index , int width )

Sets the width of the tab in the group of tabs arranged horizontally.
> **Notice:** You may need to call [*updateGuiHierarchy()*](../../../api/library/gui/class.enginewindow_cs.md#updateGuiHierarchy_void) first, if you have added a new window to the group and want to change its tab width immediately. Otherwise, you may get incorrect results.


### Arguments

- *int* **index** - The index of the tab.
- *int* **width** - The width of the tab in the group of tabs arranged horizontally.

## void SetVerticalTabHeight ( int index , int height )

Sets the height of the tab in the group of tabs arranged vertically.
> **Notice:** You may need to call [*updateGuiHierarchy()*](../../../api/library/gui/class.enginewindow_cs.md#updateGuiHierarchy_void) first, if you have added a new window to the group and want to change its tab height immediately. Otherwise, you may get incorrect results.


### Arguments

- *int* **index** - The index of the tab.
- *int* **height** - The height of the tab in the group of tabs arranged vertically.

## void SetSeparatorPosition ( int index , int pos )

Sets the position of the line separating a tab group from the rest of the area. The separator line can be horizontal or vertical depending on the [group type](#getGroupType_int).
> **Notice:** You may need to call [*updateGuiHierarchy()*](../../../api/library/gui/class.enginewindow_cs.md#updateGuiHierarchy_void) first, if you have added a new window to the group and want to change its separator immediately. Otherwise, you may get incorrect results.


### Arguments

- *int* **index** - Index of the tab.
- *int* **pos** - Position of the separation line, in pixels, from the top-left corner of the window.

## int GetSeparatorPosition ( int index )

Returns the position of the line separating a tab group from the rest of the area. The separator line can be horizontal or vertical depending on the [group type](#getGroupType_int).
> **Notice:** You may need to call [*updateGuiHierarchy()*](../../../api/library/gui/class.enginewindow_cs.md#updateGuiHierarchy_void) first, if you have added a new window to the group and want to access its separator immediately. Otherwise, you may get incorrect results.


### Arguments

- *int* **index** - Index of the tab.

### Return value

Position of the separation line, in pixels, from the top-left corner of the window.
## void SetSeparatorValue ( int index , float value )

Sets the relative position of the tab separator.
> **Notice:** You may need to call [*updateGuiHierarchy()*](../../../api/library/gui/class.enginewindow_cs.md#updateGuiHierarchy_void) first, if you have added a new window to the group and want to change its separator immediately. Otherwise, you may get incorrect results.


### Arguments

- *int* **index** - Index of the tab.
- *float* **value** - Position of the tab separator, the value from 0 to 1 that is recalculated to pixels.

## float GetSeparatorValue ( int index )

Returns the relative position of the tab separator.
> **Notice:** You may need to call [*updateGuiHierarchy()*](../../../api/library/gui/class.enginewindow_cs.md#updateGuiHierarchy_void) first, if you have added a new window to the group and want to access its separator immediately. Otherwise, you may get incorrect results.


### Arguments

- *int* **index** - Index of the tab.

### Return value

Position of the tab separator, the value from 0 to 1.
## void SwapTabs ( int first , int second )

Swaps the specified tabs.
> **Notice:** If the group is [fixed](#isFixed_int), tabs won't be swapped and the console will display a corresponding warning.


### Arguments

- *int* **first** - Index of the first tab.
- *int* **second** - Index of the second tab.

## int GetIntersectionTabBar ( ivec2 global_mouse_pos )

Returns the value indicating if the mouse is hovering over the window tab bar.
### Arguments

- *ivec2* **global_mouse_pos** - Global screen coordinates of the mouse relative to the main display.

### Return value

1 if the mouse hovers over the window tab bar, otherwise 0.
## int GetIntersectionTabBarArea ( ivec2 global_mouse_pos )

Returns the value indicating if the mouse is hovering over the window tab bar area.
### Arguments

- *ivec2* **global_mouse_pos** - Global screen coordinates of the mouse relative to the main display.

### Return value

1 if the mouse hovers over the window tab bar area, otherwise 0.
