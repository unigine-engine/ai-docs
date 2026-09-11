# Unigine::BodyDummy Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Body


This class is used to create a dummy body that serves as unmoving, non-interacting (and often [invisible](../../../api/library/objects/class.objectdummy_usc.md)) prop to attach other bodies with joints to.


## BodyDummy Class

---

## static BodyDummy ( )

Constructor. Creates a dummy body.
## static BodyDummy ( Object object )

Constructor. Creates a dummy body for a given object.
### Arguments

- *[Object](../../../api/library/objects/class.object_usc.md)* **object** - Object approximated with the new dummy body.
