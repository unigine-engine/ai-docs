# JSBSim::GroundCallback Class

**Inherits from:** JSBSim::FGGroundCallback


GroundCallback provides ground contact information to the **JSBSim** **FDM** by implementing **JSBSim**'s FGGroundCallback interface. It uses Unigine's intersection system to detect terrain and return contact points, normals, and height above ground.


The callback is automatically used by **[FDMJSBSim](../../../api/modules/jsbsim/class.fdmjsbsim.md)** to provide accurate ground contact for landing gear simulation, including terrain following and surface normal calculation for realistic gear compression and ground handling.


A caching system is used to improve performance by avoiding redundant intersection queries for nearby positions within the same frame.


### See Also


- **[JSBSim::FDMJSBSim](../../../api/modules/jsbsim/class.fdmjsbsim.md)**


## GroundCallback Class

---

## GroundCallback ( )

Constructs a ground callback with the specified Earth ellipsoid parameters.
### Arguments

## static void clearCache ( )

Clears the cached intersection results. Call at the start of each frame.
## GetAGLevel ( )

Returns the height above ground level at the specified location. This is the main callback method called by JSBSim during gear contact calculations.
### Arguments

### Return value

Height above ground level.
## static getData ( )

Queries ground data at the specified geodetic position.
### Arguments

### Return value

Status code.
