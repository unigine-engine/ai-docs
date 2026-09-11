# Simulation

**Inherits from:** SystemLogic


Simulation is a singleton system logic class that manages the UAV simulation environment. It handles drone lifecycle (creation, activation, respawning), drone presets, and spawn points. The simulation supports multiple drones with different presets (drone models with specific flight model configurations).


### See Also


- **[Drone](../../../../api/templates/template_aviation_uav/drone/class.drone.md)**
- **[SpawnPoint](../../../../api/templates/template_aviation_uav/simulation/class.spawnpoint.md)**
- **[Simulation::DronePreset](../../../../api/templates/template_aviation_uav/simulation/class.dronepreset.md)**
- **[FlightModelBase](../../../../api/templates/template_aviation_uav/drone/flightmodel/class.flightmodelbase.md)**


## Simulation Class

---

## static get ( )

Returns the singleton simulation instance.
### Return value

Singleton instance.
## addDrone ( )

Creates a new drone from a preset at the specified spawn point.
### Arguments

### Return value

Created drone pointer.
## getActiveDrone ( )

Returns the currently active drone.
### Return value

Active drone or nullptr.
## getDrone ( )

Returns the drone at the specified index.
### Arguments

### Return value

Drone pointer or nullptr.
## getActiveDroneIdx ( )

Returns the index of the active drone.
### Return value

Active drone index.
## getNumDrones ( )

Returns the total number of drones in the simulation.
### Return value

Number of drones.
## void setActiveDrone ( )

Sets the active drone by index.
### Arguments

## void respawnActiveDrone ( )

Respawns the active drone at the specified spawn point.
### Arguments

## void respawnDrone ( )

Respawns the specified drone at a spawn point.
### Arguments

## getActiveDronePreset ( )

Returns the preset of the active drone.
### Return value

Active drone preset.
## getDronePreset ( )

Returns the drone preset at the specified index.
### Arguments

### Return value

Drone preset or nullptr.
## getNumDronePresets ( )

Returns the total number of drone presets.
### Return value

Number of presets.
## void setActiveDronePreset ( )

Changes the active drone to use a different preset.
### Arguments

## getNumSpawns ( )

Returns the number of available spawn points.
### Return value

Number of spawn points.
## getSelectedSpawn ( )

Returns the currently selected spawn point.
### Return value

Selected spawn point or nullptr.
## getSpawn ( )

Returns the spawn point at the specified index.
### Arguments

### Return value

Spawn point or nullptr.
## getSelectedSpawnIdx ( )

Returns the index of the currently selected spawn point.
### Return value

Selected spawn index.
## getActiveDronePresetIdx ( )

Returns the index of the active drone's preset.
### Return value

Active preset index or -1.
## getEventActiveDroneChanged ( )

Returns the event triggered when the active drone changes.
### Return value

Drone changed event.
## getEventActiveDroneReset ( )

Returns the event triggered when the active drone is reset.
### Return value

Drone reset event.
