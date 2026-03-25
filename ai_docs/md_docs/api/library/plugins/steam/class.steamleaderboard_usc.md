# Unigine::Plugins::SteamLeaderboard Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


## SteamLeaderboard Class

### Members

---

## int getID ( )

Returns the leaderboard ID.
### Return value

Leaderboard ID.
## string getName ( )

Returns the leaderboard name.
### Return value

Leaderboard name.
## int isFound ( )

Returns the value stating if the leaderboard was found.
### Return value

**1** if the leaderboard is found, otherwise **0**.
## bool find ( )

Returns the value stating if the leaderboard was created.
### Return value

true if a leaderboard is created, otherwise false.
## bool findOrCreate ( int sort_method , int display_type )

Checks if a leaderboard is created, it will create it if it's not yet created.
### Arguments

- *int* **sort_method** - The sort order of the new leaderboard if it's created.
- *int* **display_type** - The display type (used by the Steam Community web site) of the new leaderboard if it's created.

### Return value

true if a leaderboard is created, otherwise false.
## bool uploadScore ( int score , bool forced = false )

Uploads the user score to the current leaderboard.
### Arguments

- *int* **score** - The value to store in the current leaderboard.
- *bool* **forced** - If set to true, the leaderboard will always replace score with specified; if set to false, the leaderboard will keep user's best score.

### Return value

true if , otherwise false.
## bool downloadScores ( int request , int num_before , int num_after )

Downloads a set of entries from the current leaderboard.
### Arguments

- *int* **request** - Type of requested data, one of the [DATA_REQUEST](#DATA_REQUEST_GLOBAL) values.
- *int* **num_before** - Number of entries before the current user.
- *int* **num_after** - Number of entries after the current user.

### Return value

false if a leaderboard has not been selected yet, otherwise true.
## int isUploading ( )

Checks the leaderboard uploading status.
### Return value

true if the leaderboard is uploading, otherwise false.
## int isDownloading ( )

Checks the leaderboard downloading status.
### Return value

true if the leaderboard is downloading, otherwise false.
## int isLastUploadFailed ( )

Checks the leaderboard upload result.
### Return value

true if the leaderboard upload has failed, otherwise false.
## int isLastDownloadFailed ( )

Checks the leaderboard download result.
### Return value

true if the leaderboard download has failed, otherwise false.
## int getLastDataRequest ( )

Returns the type of requested data in the most recent leaderbord download.
### Return value

Type of requested data, one of the [DATA_REQUEST](#DATA_REQUEST_GLOBAL) values.
## int getEntryCount ( )

Returns the total number of entries in the leaderboard.
### Return value

Number of entries in the leaderboard. Returns 0, if the leaderboard handle is invalid.
## int getSortMethod ( )

Returns the order for the leaderboard sorting.
### Return value

Order for the leaderboard sorting, one of the values.
## int getDisplayType ( )

Returns the type of data to be displayed with the leaderboard.
### Return value

Type of data to be displayed with the leaderboard, one of the values.
## int getNumEntries ( )

Returns the existing number of entries.
### Return value

Number of entries.
## long getEntryUserID ( int num )

Returns the ID of the user who this entry belongs to.
### Arguments

- *int* **num** - Number of an entry in a leaderboard.

### Return value

The globally unique identifier for all Steam accounts.
## int getEntryRank ( int num )

Returns the global rank of the entry.
### Arguments

- *int* **num** - Number of an entry in a leaderboard.

### Return value

The global rank of this entry ranging from [1..N], where N is the number of users with an entry in the leaderboard.
## int getEntryScore ( int num )

Returns the raw score of the entry as set in the leaderboard.
### Arguments

- *int* **num** - Number of an entry in a leaderboard.

### Return value

The raw score as set in the leaderboard.
