# Tablet Component

**Inherits from:** MenuBaseUI


Tablet provides an in-world UI panel for displaying and tracking scenario tasks. It renders a scrollable list of tasks with status icons, progress bars, and a restart button. The tablet attaches to a specified node and can be used in both VR and desktop modes.


Each task displays a status icon (NotStarted, InProgress, Success, Failure), name label, and optional progress bar. The restart button triggers a scenario reset when held for a configurable duration.


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Logic |  |  |  |
| Tablet Node | *Node* | � | Node to attach the tablet GUI to. |
| Common UI |  |  |  |
| Not Started Icon Path | *File* | � | Icon displayed for tasks that haven't started. |
| In Progress Icon Path | *File* | � | Icon displayed for tasks currently in progress. |
| Completed Icon Path | *File* | � | Icon displayed for successfully completed tasks. |
| Failed Icon Path | *File* | � | Icon displayed for failed tasks. |
| Background Color | *Color* | *black* | Background color of the tablet. |
| Text Color | *Color* | *white* | Color for task text. |
| Spacer Color | *Color* | *white* | Color for spacer lines. |
| Font Size | *Int* | *50* | Font size for task labels. |
| Task Progress Bar |  |  |  |
| Task Progress Bar Background Color | *Color* | *black* | Background color of progress bars. |
| Task Progress Bar Progress Color | *Color* | *red* | Fill color for progress bars. |
| Task Progress Bar Completed Color | *Color* | *green* | Fill color when task is complete. |
| Task Progress Bar Border Color | *Color* | *white* | Border color of progress bars. |
| Task Progress Bar Border Thickness | *Float* | *0.1* | Border thickness. |
| Restart Button |  |  |  |
| Restart Button Background Color | *Color* | *black* | Background color of restart button. |
| Restart Button Progress Color | *Color* | *orange* | Progress fill color when holding restart. |
| Restart Button Hovered Color | *Color* | *gray* | Button color when hovered. |
| Restart Button Border Color | *Color* | *white* | Border color of restart button. |
| Restart Button Border Thickness | *Float* | *0.1* | Restart button border thickness. |


### See Also


- **[Task](../../../../api/templates/template_aviation_maintenance/missions/class.task.md)**
- **[FuelScenario](../../../../api/templates/template_aviation_maintenance/scenarios/fuel_scenario/class.fuelscenario.md)**
- **[MenuBaseUI](../../../../api/modules/vr/components/objects/class.menubaseui.md)**


## Tablet Class

---

## createTask ( )

Creates a new task with the specified name and adds it to the tablet.
### Arguments

### Return value

Index of the created task.
## getTask ( )

Returns the task at the specified index.
### Arguments

### Return value

Pointer to the task or nullptr.
## void clearTasks ( )

Removes all tasks from the tablet.
## isExamModeSelected ( )

Returns whether exam mode is currently selected.
### Return value

true if exam mode is enabled.
## getInfoLabel ( )

Returns the info label widget for displaying additional information.
### Return value

Info label widget.
## getRestartEvent ( )

Returns the event triggered when the restart button is activated.
### Return value

Restart event reference.
