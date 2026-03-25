# SkeletonRetargeterEquals Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** SkeletonRetargeter


This class implements retargeting between two skeletons that have identical joint hierarchies (same number of joints, same parent-child relationships). It is the simplest and most efficient retargeting strategy - joint transforms are transferred directly by index without any remapping.


## SkeletonRetargeterEquals Class

---

## static SkeletonRetargeterEquals ( UGUID first_file_guid , UGUID second_file_guid )

Creates a retargeter for two skeletons with identical hierarchies, identified by their file GUIDs.
### Arguments

- *[UGUID](../../../../api/library/filesystem/class.uguid_usc.md)* **first_file_guid** - File GUID of the first skeleton.
- *[UGUID](../../../../api/library/filesystem/class.uguid_usc.md)* **second_file_guid** - File GUID of the second skeleton.

## static SkeletonRetargeterEquals ( string first_file , string second_file )

Creates a retargeter for two skeletons with identical hierarchies, identified by their file paths.
### Arguments

- *string* **first_file** - File path of the first skeleton.
- *string* **second_file** - File path of the second skeleton.
