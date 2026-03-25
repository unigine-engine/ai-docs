# SkeletonRetargeterNamesMatching Class (CPP)

**Header:** #include <UnigineSkeleton.h>

**Inherits from:** SkeletonRetargeter


This class implements retargeting between two skeletons by matching joints by their names. It is useful when the two skeletons have different hierarchies but share the same or similar joint naming conventions. Joints are mapped by finding matching name pairs between the two skeletons.


Matching can be configured manually via [setNamesMatching()](#setNamesMatching_VECString_VECString_int) or detected automatically via [setAutoMatching()](#setAutoMatching_int).


## SkeletonRetargeterNamesMatching Class

---

## static SkeletonRetargeterNamesMatchingPtr create ( const UGUID & first_file_guid , const UGUID & second_file_guid )

Creates a name-matching retargeter for two skeletons identified by their file GUIDs.
### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **first_file_guid** - File GUID of the first skeleton.
- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **second_file_guid** - File GUID of the second skeleton.

## static SkeletonRetargeterNamesMatchingPtr create ( const char * first_file , const char * second_file )

Creates a name-matching retargeter for two skeletons identified by their file paths.
### Arguments

- *const char ** **first_file** - File path of the first skeleton.
- *const char ** **second_file** - File path of the second skeleton.

## bool setNamesMatching ( const Vector < String > & first_names , const Vector < String > & second_names )

Manually sets the joint name mapping between two skeletons. Each entry at the same index in both lists defines a matching pair.
### Arguments

- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../../api/library/common/class.string_cpp.md)> &* **first_names** - List of joint names from the first skeleton.
- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../../api/library/common/class.string_cpp.md)> &* **second_names** - List of corresponding joint names from the second skeleton. Must have the same length as first_names.

### Return value

true if matching was set successfully; false otherwise.
## bool setAutoMatching ( )

Automatically detects joint name matches between the two skeletons using the skeleton files specified at construction.
### Return value

true if auto-matching was successful; false otherwise.
## bool setAutoMatching ( const Ptr <ConstSkeleton> & first_skeleton , const Ptr <ConstSkeleton> & second_skeleton )

Automatically detects joint name matches between two explicitly provided skeleton instances.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<ConstSkeleton> &* **first_skeleton** - First skeleton instance to match against.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<ConstSkeleton> &* **second_skeleton** - Second skeleton instance to match against.

### Return value

true if auto-matching was successful; false otherwise.
