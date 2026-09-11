# Unigine::Plugins::SteamLeaderboard Class (CS)


## SteamLeaderboard Class

### Enums

## DATA_REQUEST

| Name | Description |
|---|---|
| **GLOBAL** = 0 | Used to query for a sequential range of leaderboard entries by leaderboard rank. The start and end parameters control the requested range. For example, you can display the top 10 on a leaderboard for your game by setting start to 1 and end to 10. |
| **GLOBAL_AROUND_USER** = 1 | Used to retrieve leaderboard entries relative a user's entry. The start parameter is the number of entries to retrieve before the current user's entry, and the end parameter is the number of entries after the current user's entry. The current user's entry is always included. For example, if the current user is #5 on the leaderboard, setting start to -2 and end to 2 will return 5 entries: ranks #3 through #7. If there are not enough entries in the leaderboard before or after the user's entry, Steam will adjust the range to try to return the number of entries requested. For example, if the user is #1 on the leaderboard and start is set to -2, end is set to 2, Steam will return the first 5 entries in the leaderboard. |
| **FRIENDS** = 2 | Used to retrieve all leaderboard entries for friends of the current user. The start and end parameters are ignored. |
| **USERS** = 3 | Used internally. |

## DISPLAY_TYPE

| Name | Description |
|---|---|
| **NONE** = 0 | This is only ever used when a leaderboard is invalid, you should never set this yourself. |
| **NUMERIC** = 1 | The score is just a simple numerical value. |
| **TIME_SECONDS** = 2 | The score represents a time, in seconds. |
| **TIME_MILLISECONDS** = 3 | The score represents a time, in milliseconds. |

## SORT_METHOD

| Name | Description |
|---|---|
| **NONE** = 0 | Only ever used when a leaderboard is invalid, you should never set this yourself. |
| **ASCENDING** = 1 | The top-score is the lowest number. |
| **DESCENDING** = 2 | The top-score is the highest number. |

### Properties

## 🔒︎ int NumEntries

The existing number of entries.
## 🔒︎ SteamLeaderboard.DISPLAY_TYPE DisplayType

The type of data to be displayed with the leaderboard. One of the [DISPLAY_TYPE_*](#DISPLAY_TYPE_NONE) values.
## 🔒︎ SteamLeaderboard.SORT_METHOD SortMethod

The order for the leaderboard sorting. One of the [SORT_METHOD_*](#SORT_METHOD_NONE) values.
## 🔒︎ int EntryCount

The total number of entries in the leaderboard. Returns 0, if the leaderboard handle is invalid.
## 🔒︎ SteamLeaderboard.DATA_REQUEST LastDataRequest

The type of requested data in the most recent leaderboard download. One of the [DATA_REQUEST_*](#DATA_REQUEST_GLOBAL) values.
## 🔒︎ bool IsLastDownloadFailed

The value indicating if the last leaderboard download has failed.
## 🔒︎ bool IsLastUploadFailed

The value indicating if the last leaderboard upload has failed.
## 🔒︎ bool IsDownloading

The value indicating if the leaderboard is downloading.
## 🔒︎ bool IsUploading

The value indicating if the leaderboard is uploading.
## 🔒︎ bool IsFound

The value indicating if the leaderboard was found.
## 🔒︎ string Name

The leaderboard name.
## 🔒︎ int ID

The leaderboard ID.
### Members

---

## bool Find ( )

Returns the value stating if the leaderboard was created.
### Return value

true if a leaderboard is created, otherwise false.
## bool FindOrCreate ( SteamLeaderboard.SORT_METHOD sort_method , SteamLeaderboard.DISPLAY_TYPE display_type )

Checks if a leaderboard is created, it will create it if it's not yet created.
### Arguments

- *[SteamLeaderboard.SORT_METHOD](../../../../api/library/plugins/steam/class.steamleaderboard_cs.md#SORT_METHOD)* **sort_method** - The sort order of the new leaderboard if it's created.
- *[SteamLeaderboard.DISPLAY_TYPE](../../../../api/library/plugins/steam/class.steamleaderboard_cs.md#DISPLAY_TYPE)* **display_type** - The display type (used by the *Steam Community* web site) of the new leaderboard if it's created.

### Return value

true if a leaderboard is created, otherwise false.
## bool UploadScore ( int score , bool forced = false )

Uploads the user score to the current leaderboard.
### Arguments

- *int* **score** - The value to store in the current leaderboard.
- *bool* **forced** - If set to true, the leaderboard will always replace score with specified; if set to false, the leaderboard will keep user's best score.

### Return value

true if , otherwise false.
## bool DownloadScores ( SteamLeaderboard.DATA_REQUEST request , int num_before , int num_after )

Downloads a set of entries from the current leaderboard.
### Arguments

- *[SteamLeaderboard.DATA_REQUEST](../../../../api/library/plugins/steam/class.steamleaderboard_cs.md#DATA_REQUEST)* **request** - Type of requested data, one of the [DATA_REQUEST](#DATA_REQUEST_GLOBAL) values.
- *int* **num_before** - Number of entries before the current user.
- *int* **num_after** - Number of entries after the current user.

### Return value

false if a leaderboard has not been selected yet, otherwise true.
## ulong GetEntryUserID ( int num )

Returns the ID of the user who this entry belongs to.
### Arguments

- *int* **num** - Number of an entry in a leaderboard.

### Return value

The globally unique identifier for all Steam accounts.
## int GetEntryRank ( int num )

Returns the global rank of the entry.
### Arguments

- *int* **num** - Number of an entry in a leaderboard.

### Return value

The global rank of this entry ranging from [1..N], where N is the number of users with an entry in the leaderboard.
## int GetEntryScore ( int num )

Returns the raw score of the entry as set in the leaderboard.
### Arguments

- *int* **num** - Number of an entry in a leaderboard.

### Return value

The raw score as set in the leaderboard.
