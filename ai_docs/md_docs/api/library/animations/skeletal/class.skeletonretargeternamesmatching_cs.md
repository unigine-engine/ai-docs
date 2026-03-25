# SkeletonRetargeterNamesMatching Class (CS)

**Inherits from:** SkeletonRetargeter


This class implements retargeting between two skeletons by matching joints by their names. It is useful when the two skeletons have different hierarchies but share the same or similar joint naming conventions. Joints are mapped by finding matching name pairs between the two skeletons.


Matching can be configured manually via [setNamesMatching()](#setNamesMatching_VECString_VECString_int) or detected automatically via [setAutoMatching()](#setAutoMatching_int).


## SkeletonRetargeterNamesMatching Class

### Members

---

## SkeletonRetargeterNamesMatching ( UGUID first_file_guid , UGUID second_file_guid )

Creates a name-matching retargeter for two skeletons identified by their file GUIDs.
### Arguments

- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **first_file_guid** - File GUID of the first skeleton.
- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **second_file_guid** - File GUID of the second skeleton.

## SkeletonRetargeterNamesMatching ( string first_file , string second_file )

Creates a name-matching retargeter for two skeletons identified by their file paths.
### Arguments

- *string* **first_file** - File path of the first skeleton.
- *string* **second_file** - File path of the second skeleton.

## bool SetNamesMatching ( string[] first_names , string[] second_names )

Manually sets the joint name mapping between two skeletons. Each entry at the same index in both lists defines a matching pair.
### Arguments

- *string[]* **first_names** - List of joint names from the first skeleton.
- *string[]* **second_names** - List of corresponding joint names from the second skeleton. Must have the same length as first_names.

### Return value

true if matching was set successfully; false otherwise.
## bool SetAutoMatching ( )

Automatically detects joint name matches between the two skeletons using the skeleton files specified at construction.
### Return value

true if auto-matching was successful; false otherwise.
## bool SetAutoMatching ( Skeleton first_skeleton , Skeleton second_skeleton )

Automatically detects joint name matches between two explicitly provided skeleton instances.
### Arguments

- *[Skeleton](../../../../api/library/animations/skeletal/class.skeleton_cs.md)* **first_skeleton** - First skeleton instance to match against.
- *[Skeleton](../../../../api/library/animations/skeletal/class.skeleton_cs.md)* **second_skeleton** - Second skeleton instance to match against.

### Return value

true if auto-matching was successful; false otherwise.
