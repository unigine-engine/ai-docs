# SkeletonRetargeterEquals Class (CS)

**Inherits from:** SkeletonRetargeter


This class implements retargeting between two skeletons that have identical joint hierarchies (same number of joints, same parent-child relationships). It is the simplest and most efficient retargeting strategy - joint transforms are transferred directly by index without any remapping.


## SkeletonRetargeterEquals Class

### Members

---

## SkeletonRetargeterEquals ( UGUID first_file_guid , UGUID second_file_guid )

Creates a retargeter for two skeletons with identical hierarchies, identified by their file GUIDs.
### Arguments

- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **first_file_guid** - File GUID of the first skeleton.
- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **second_file_guid** - File GUID of the second skeleton.

## SkeletonRetargeterEquals ( string first_file , string second_file )

Creates a retargeter for two skeletons with identical hierarchies, identified by their file paths.
### Arguments

- *string* **first_file** - File path of the first skeleton.
- *string* **second_file** - File path of the second skeleton.
