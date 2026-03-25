# SkeletonRetargeterEquals Class (CPP)

**Header:** #include <UnigineSkeleton.h>

**Inherits from:** SkeletonRetargeter


This class implements retargeting between two skeletons that have identical joint hierarchies (same number of joints, same parent-child relationships). It is the simplest and most efficient retargeting strategy - joint transforms are transferred directly by index without any remapping.


## SkeletonRetargeterEquals Class

---

## static SkeletonRetargeterEqualsPtr create ( const UGUID & first_file_guid , const UGUID & second_file_guid )

Creates a retargeter for two skeletons with identical hierarchies, identified by their file GUIDs.
### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **first_file_guid** - File GUID of the first skeleton.
- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **second_file_guid** - File GUID of the second skeleton.

## static SkeletonRetargeterEqualsPtr create ( const char * first_file , const char * second_file )

Creates a retargeter for two skeletons with identical hierarchies, identified by their file paths.
### Arguments

- *const char ** **first_file** - File path of the first skeleton.
- *const char ** **second_file** - File path of the second skeleton.
