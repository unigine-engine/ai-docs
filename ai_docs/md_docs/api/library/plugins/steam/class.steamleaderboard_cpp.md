# Unigine::Plugins::SteamLeaderboard Class (CPP)

**Header:** #include <plugins/Unigine/Steam/UnigineSteam.h>


## SteamLeaderboard Class

### Enums

## DATA_REQUEST

| Name | Description |
|---|---|
| **DATA_REQUEST_GLOBAL** = 0 | Used to query for a sequential range of leaderboard entries by leaderboard rank. The start and end parameters control the requested range. For example, you can display the top 10 on a leaderboard for your game by setting start to 1 and end to 10. |
| **DATA_REQUEST_GLOBAL_AROUND_USER** = 1 | Used to retrieve leaderboard entries relative a user's entry. The start parameter is the number of entries to retrieve before the current user's entry, and the end parameter is the number of entries after the current user's entry. The current user's entry is always included. For example, if the current user is #5 on the leaderboard, setting start to -2 and end to 2 will return 5 entries: ranks #3 through #7. If there are not enough entries in the leaderboard before or after the user's entry, Steam will adjust the range to try to return the number of entries requested. For example, if the user is #1 on the leaderboard and start is set to -2, end is set to 2, Steam will return the first 5 entries in the leaderboard. |
| **DATA_REQUEST_FRIENDS** = 2 | Used to retrieve all leaderboard entries for friends of the current user. The start and end parameters are ignored. |
| **DATA_REQUEST_USERS** = 3 | Used internally. |

## DISPLAY_TYPE

| Name | Description |
|---|---|
| **DISPLAY_TYPE_NONE** = 0 | This is only ever used when a leaderboard is invalid, you should never set this yourself. |
| **DISPLAY_TYPE_NUMERIC** = 1 | The score is just a simple numerical value. |
| **DISPLAY_TYPE_TIME_SECONDS** = 2 | The score represents a time, in seconds. |
| **DISPLAY_TYPE_TIME_MILLISECONDS** = 3 | The score represents a time, in milliseconds. |

## SORT_METHOD

| Name | Description |
|---|---|
| **SORT_METHOD_NONE** = 0 | Only ever used when a leaderboard is invalid, you should never set this yourself. |
| **SORT_METHOD_ASCENDING** = 1 | The top-score is the lowest number. |
| **SORT_METHOD_DESCENDING** = 2 | The top-score is the highest number. |

### Members

## int getNumEntries () const

Returns the current existing number of entries.
### Return value

Current existing number of entries
## SteamLeaderboard::DISPLAY_TYPE getDisplayType () const

Returns the current type of data to be displayed with the leaderboard. One of the [DISPLAY_TYPE_*](#DISPLAY_TYPE_NONE) values.
### Return value

Current type of data to be displayed with the leaderboard
## SteamLeaderboard::SORT_METHOD getSortMethod () const

Returns the current order for the leaderboard sorting. One of the [SORT_METHOD_*](#SORT_METHOD_NONE) values.
### Return value

Current order for the leaderboard sorting
## int getEntryCount () const

Returns the current total number of entries in the leaderboard. Returns 0, if the leaderboard handle is invalid.
### Return value

Current total number of entries in the leaderboard
## SteamLeaderboard::DATA_REQUEST getLastDataRequest () const

Returns the current type of requested data in the most recent leaderboard download. One of the [DATA_REQUEST_*](#DATA_REQUEST_GLOBAL) values.
### Return value

Current type of requested data in the most recent leaderboard download
## bool isLastDownloadFailed () const

Returns the current value indicating if the last leaderboard download has failed.
### Return value

**true** if the last leaderboard download has failed; otherwise **false**.
## bool isLastUploadFailed () const

Returns the current value indicating if the last leaderboard upload has failed.
### Return value

**true** if the last leaderboard upload has failed; otherwise **false**.
## bool isDownloading () const

Returns the current value indicating if the leaderboard is downloading.
### Return value

**true** if the leaderboard is downloading; otherwise **false**.
## bool isUploading () const

Returns the current value indicating if the leaderboard is uploading.
### Return value

**true** if the leaderboard is uploading; otherwise **false**.
## bool isFound () const

Returns the current value indicating if the leaderboard was found.
### Return value

**true** if the leaderboard was found; otherwise **false**.
## const char * getName () const

Returns the current leaderboard name.
### Return value

Current leaderboard name
## int getID () const

Returns the current leaderboard ID.
### Return value

Current leaderboard ID
---

## bool find ( )

Returns the value stating if the leaderboard was created.
### Return value

true if a leaderboard is created, otherwise false.
## bool findOrCreate ( SteamLeaderboard::SORT_METHOD sort_method , SteamLeaderboard::DISPLAY_TYPE display_type )

Checks if a leaderboard is created, it will create it if it's not yet created.
### Arguments

- *[SteamLeaderboard::SORT_METHOD](../../../../api/library/plugins/steam/class.steamleaderboard_cpp.md#SORT_METHOD)* **sort_method** - The sort order of the new leaderboard if it's created.
- *[SteamLeaderboard::DISPLAY_TYPE](../../../../api/library/plugins/steam/class.steamleaderboard_cpp.md#DISPLAY_TYPE)* **display_type** - The display type (used by the *Steam Community* web site) of the new leaderboard if it's created.

### Return value

true if a leaderboard is created, otherwise false.
## bool uploadScore ( int score , bool forced = false )

Uploads the user score to the current leaderboard.
### Arguments

- *int* **score** - The value to store in the current leaderboard.
- *bool* **forced** - If set to true, the leaderboard will always replace score with specified; if set to false, the leaderboard will keep user's best score.

### Return value

true if , otherwise false.
## bool downloadScores ( SteamLeaderboard::DATA_REQUEST request , int num_before , int num_after )

Downloads a set of entries from the current leaderboard.
### Arguments

- *[SteamLeaderboard::DATA_REQUEST](../../../../api/library/plugins/steam/class.steamleaderboard_cpp.md#DATA_REQUEST)* **request** - Type of requested data, one of the [DATA_REQUEST](#DATA_REQUEST_GLOBAL) values.
- *int* **num_before** - Number of entries before the current user.
- *int* **num_after** - Number of entries after the current user.

### Return value

false if a leaderboard has not been selected yet, otherwise true.
## unsigned long long getEntryUserID ( int num ) const

Returns the ID of the user who this entry belongs to.
### Arguments

- *int* **num** - Number of an entry in a leaderboard.

### Return value

The globally unique identifier for all Steam accounts.
## int getEntryRank ( int num ) const

Returns the global rank of the entry.
### Arguments

- *int* **num** - Number of an entry in a leaderboard.

### Return value

The global rank of this entry ranging from [1..N], where N is the number of users with an entry in the leaderboard.
## int getEntryScore ( int num ) const

Returns the raw score of the entry as set in the leaderboard.
### Arguments

- *int* **num** - Number of an entry in a leaderboard.

### Return value

The raw score as set in the leaderboard.
