# Unigine::Plugins::SteamLeaderboard Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


## SteamLeaderboard Class

### Members

## int getNumEntries () const

Returns the current existing number of entries.
### Return value

Current existing number of entries
## int getDisplayType () const

Returns the current type of data to be displayed with the leaderboard. One of the [DISPLAY_TYPE_*](#DISPLAY_TYPE_NONE) values.
### Return value

Current type of data to be displayed with the leaderboard
## int getSortMethod () const

Returns the current order for the leaderboard sorting. One of the [SORT_METHOD_*](#SORT_METHOD_NONE) values.
### Return value

Current order for the leaderboard sorting
## int getEntryCount () const

Returns the current total number of entries in the leaderboard. Returns 0, if the leaderboard handle is invalid.
### Return value

Current total number of entries in the leaderboard
## int getLastDataRequest () const

Returns the current type of requested data in the most recent leaderboard download. One of the [DATA_REQUEST_*](#DATA_REQUEST_GLOBAL) values.
### Return value

Current type of requested data in the most recent leaderboard download
## int isLastDownloadFailed () const

Returns the current value indicating if the last leaderboard download has failed.
### Return value

Current the last leaderboard download has failed
## int isLastUploadFailed () const

Returns the current value indicating if the last leaderboard upload has failed.
### Return value

Current the last leaderboard upload has failed
## int isDownloading () const

Returns the current value indicating if the leaderboard is downloading.
### Return value

Current the leaderboard is downloading
## int isUploading () const

Returns the current value indicating if the leaderboard is uploading.
### Return value

Current the leaderboard is uploading
## int isFound () const

Returns the current value indicating if the leaderboard was found.
### Return value

Current the leaderboard was found
## const char * getName () const

Returns the current leaderboard name.
### Return value

Current leaderboard name
## getID () const

Returns the current leaderboard ID.
### Return value

Current leaderboard ID
---

## bool find ( )

Returns the value stating if the leaderboard was created.
### Return value

true if a leaderboard is created, otherwise false.
## bool findOrCreate ( int sort_method , int display_type )

Checks if a leaderboard is created, it will create it if it's not yet created.
### Arguments

- *int* **sort_method** - The sort order of the new leaderboard if it's created.
- *int* **display_type** - The display type (used by the *Steam Community* web site) of the new leaderboard if it's created.

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
