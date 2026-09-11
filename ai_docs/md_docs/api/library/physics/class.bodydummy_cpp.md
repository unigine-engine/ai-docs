# Unigine::BodyDummy Class (CPP)

**Header:** #include <UniginePhysics.h>

**Inherits from:** Body


This class is used to create a dummy body that serves as unmoving, non-interacting (and often [invisible](../../../api/library/objects/class.objectdummy_cpp.md)) prop to attach other bodies with joints to.


## BodyDummy Class

---

## static BodyDummyPtr create ( )

Constructor. Creates a dummy body.
## static BodyDummyPtr create ( const Ptr < Object > & object )

Constructor. Creates a dummy body for a given object.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Object](../../../api/library/objects/class.object_cpp.md)> &* **object** - Object approximated with the new dummy body.
