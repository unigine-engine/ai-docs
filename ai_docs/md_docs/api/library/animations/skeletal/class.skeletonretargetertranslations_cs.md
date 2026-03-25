# SkeletonRetargeterTranslations Class (CS)

**Inherits from:** SkeletonRetargeter


This class implements retargeting between two skeletons by matching joints based on their bind pose translations. It is useful when skeletons have different naming conventions but similar spatial layouts - joints are paired by finding the closest positional matches in the bind pose.


Matching can be configured manually via [setMatching()](#setMatching_VECString_VECString_int) or detected automatically via [setAutoMatching()](#setAutoMatching_int).


## SkeletonRetargeterTranslations Class

### Members

---

## SkeletonRetargeterTranslations ( UGUID first_file_guid , UGUID second_file_guid )

Creates a translation-matching retargeter for two skeletons identified by their file GUIDs.
### Arguments

- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **first_file_guid** - File GUID of the first skeleton.
- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **second_file_guid** - File GUID of the second skeleton.

## SkeletonRetargeterTranslations ( string first_file , string second_file )

Creates a translation-matching retargeter for two skeletons identified by their file paths.
### Arguments

- *string* **first_file** - File path of the first skeleton.
- *string* **second_file** - File path of the second skeleton.

## bool SetMatching ( string[] first_names , string[] second_names )

Manually sets the joint mapping between two skeletons. Each entry at the same index in both lists defines a matching pair.
### Arguments

- *string[]* **first_names** - List of joint names from the first skeleton.
- *string[]* **second_names** - List of corresponding joint names from the second skeleton. Must have the same length as first_names.

### Return value

true if matching was set successfully; false otherwise.
## bool SetAutoMatching ( )

Automatically detects joint matches between the two skeletons by comparing bind pose translations, using the skeleton files specified at construction.
### Return value

true if auto-matching was successful; false otherwise.
## bool SetAutoMatching ( Skeleton first_skeleton , Skeleton second_skeleton )

Automatically detects joint matches between two explicitly provided skeleton instances by comparing bind pose translations.
### Arguments

- *[Skeleton](../../../../api/library/animations/skeletal/class.skeleton_cs.md)* **first_skeleton** - First skeleton instance to match against.
- *[Skeleton](../../../../api/library/animations/skeletal/class.skeleton_cs.md)* **second_skeleton** - Second skeleton instance to match against.

### Return value

true if auto-matching was successful; false otherwise.
