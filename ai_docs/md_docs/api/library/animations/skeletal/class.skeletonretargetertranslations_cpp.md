# SkeletonRetargeterTranslations Class (CPP)

**Header:** #include <UnigineSkeleton.h>

**Inherits from:** SkeletonRetargeter


This class implements retargeting between two skeletons by matching joints based on their bind pose translations. It is useful when skeletons have different naming conventions but similar spatial layouts - joints are paired by finding the closest positional matches in the bind pose.


Matching can be configured manually via [setMatching()](#setMatching_VECString_VECString_int) or detected automatically via [setAutoMatching()](#setAutoMatching_int).


## SkeletonRetargeterTranslations Class

---

## static SkeletonRetargeterTranslationsPtr create ( const UGUID & first_file_guid , const UGUID & second_file_guid )

Creates a translation-matching retargeter for two skeletons identified by their file GUIDs.
### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **first_file_guid** - File GUID of the first skeleton.
- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **second_file_guid** - File GUID of the second skeleton.

## static SkeletonRetargeterTranslationsPtr create ( const char * first_file , const char * second_file )

Creates a translation-matching retargeter for two skeletons identified by their file paths.
### Arguments

- *const char ** **first_file** - File path of the first skeleton.
- *const char ** **second_file** - File path of the second skeleton.

## bool setMatching ( const Vector < String > & first_names , const Vector < String > & second_names )

Manually sets the joint mapping between two skeletons. Each entry at the same index in both lists defines a matching pair.
### Arguments

- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../../api/library/common/class.string_cpp.md)> &* **first_names** - List of joint names from the first skeleton.
- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../../api/library/common/class.string_cpp.md)> &* **second_names** - List of corresponding joint names from the second skeleton. Must have the same length as first_names.

### Return value

true if matching was set successfully; false otherwise.
## bool setAutoMatching ( )

Automatically detects joint matches between the two skeletons by comparing bind pose translations, using the skeleton files specified at construction.
### Return value

true if auto-matching was successful; false otherwise.
## bool setAutoMatching ( const Ptr <ConstSkeleton> & first_skeleton , const Ptr <ConstSkeleton> & second_skeleton )

Automatically detects joint matches between two explicitly provided skeleton instances by comparing bind pose translations.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<ConstSkeleton> &* **first_skeleton** - First skeleton instance to match against.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<ConstSkeleton> &* **second_skeleton** - Second skeleton instance to match against.

### Return value

true if auto-matching was successful; false otherwise.
