# SkeletonRetargeterNamesMatching Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** SkeletonRetargeter


This class implements retargeting between two skeletons by matching joints by their names. It is useful when the two skeletons have different hierarchies but share the same or similar joint naming conventions. Joints are mapped by finding matching name pairs between the two skeletons.


Matching can be configured manually via [setNamesMatching()](#setNamesMatching_VECString_VECString_int) or detected automatically via [setAutoMatching()](#setAutoMatching_int).


## SkeletonRetargeterNamesMatching Class

---

## static SkeletonRetargeterNamesMatching ( UGUID first_file_guid , UGUID second_file_guid )

Creates a name-matching retargeter for two skeletons identified by their file GUIDs.
### Arguments

- *[UGUID](../../../../api/library/filesystem/class.uguid_usc.md)* **first_file_guid** - File GUID of the first skeleton.
- *[UGUID](../../../../api/library/filesystem/class.uguid_usc.md)* **second_file_guid** - File GUID of the second skeleton.

## static SkeletonRetargeterNamesMatching ( string first_file , string second_file )

Creates a name-matching retargeter for two skeletons identified by their file paths.
### Arguments

- *string* **first_file** - File path of the first skeleton.
- *string* **second_file** - File path of the second skeleton.

## int setNamesMatching ( Vector<String> first_names , Vector<String> second_names )

Manually sets the joint name mapping between two skeletons. Each entry at the same index in both lists defines a matching pair.
### Arguments

- *Vector<String>* **first_names** - List of joint names from the first skeleton.
- *Vector<String>* **second_names** - List of corresponding joint names from the second skeleton. Must have the same length as first_names.

### Return value

true if matching was set successfully; false otherwise.
## int setAutoMatching ( )

Automatically detects joint name matches between the two skeletons using the skeleton files specified at construction.
### Return value

true if auto-matching was successful; false otherwise.
