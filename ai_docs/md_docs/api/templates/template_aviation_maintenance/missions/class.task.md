# Task Component

**Inherits from:** ComponentBase


Task is an abstract base component for scenario tasks. It defines a common interface for task execution with states (NotStarted, InProgress, Success, Failure) and timing. Derived classes implement specific task logic by overriding the *startTask()* and *update()* methods.


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Task Name | *String* | � | Display name of the task. |


### See Also


- **[Tablet](../../../../api/templates/template_aviation_maintenance/missions/class.tablet.md)**
- **[FuelScenario](../../../../api/templates/template_aviation_maintenance/scenarios/fuel_scenario/class.fuelscenario.md)**


## Task Class

---

## virtual void startTask ( ) =0

Starts the task execution. Must be implemented by derived classes.
## virtual void update ( ) =0

Updates the task state. Must be implemented by derived classes.
## getState ( )

Returns the current state of the task (NotStarted, InProgress, Success, or Failure).
### Return value

Current task state.
## getName ( )

Returns the display name of the task.
### Return value

Task name string.
## getCurrentTime ( )

Returns the time elapsed since the task started.
### Return value

Elapsed time in seconds.
