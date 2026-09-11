# Unigine::Plugins::IG::ArticulatedPart Class (CS)


This class represents the *IG Articulated Part* interface.


> **Notice:** IG plugin must be loaded.


## ArticulatedPart Class

### Properties

## vec3 AngularRate

The rate of angular motion of the articulated part.
## vec3 LinearRate

The rate of linear motion of the articulated part.
## vec3 RotationEuler

The rotation of the articulated part in the submodel coordinate system (SCS).
## vec3 Position

The offset of the articulated part in the submodel coordinate system (SCS).
## bool Enabled

The value indicating if the articulated part is enabled.
## 🔒︎ int NumNodes

The total number of nodes representing the articulated part.
## 🔒︎ int ID

The ID of the articulated part.
### Members

---

## Node GetNode ( int num )

Returns the given node from the array of nodes representing the articulated part.
### Arguments

- *int* **num** - Node number.

### Return value

Node.
