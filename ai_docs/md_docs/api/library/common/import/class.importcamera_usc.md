# Unigine::ImportCamera Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is an intermediate representation of a camera from a source file. The associated [ImportNode](../../../../api/library/common/import/class.importnode_usc.md) defines its position and orientation in the scene. During import, it is converted to a UNIGINE [Player](../../../../api/library/players/class.player_usc.md) by an [import processor](../../../../api/library/common/import/class.importprocessor_usc.md).


## ImportCamera Class

### Members

## void setData ( vptr data )

Sets a new metadata of the imported camera.
### Arguments

- *vptr* **data** - The camera metadata.

## vptr getData () const

Returns the current metadata of the imported camera.
### Return value

Current camera metadata.
## void setNode ( ImportNode node )

Sets a new scene node to which the camera is attached as an attribute.
### Arguments

- *[ImportNode](../../../../api/library/common/import/class.importnode_usc.md)* **node** - The scene node.

## ImportNode getNode () const

Returns the current scene node to which the camera is attached as an attribute.
### Return value

Current scene node.
---

## static ImportCamera ( )

Constructor. Creates an empty *ImportCamera* instance.
