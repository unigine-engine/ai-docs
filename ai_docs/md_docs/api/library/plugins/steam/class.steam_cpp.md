# Unigine::Plugins::Steam Class (CPP)

**Header:** #include <plugins/Unigine/Steam/UnigineSteam.h>

> **Notice:** This class is a singleton.


## Steam Class

### Enums

## CALLBACK_INDEX

| Name | Description |
|---|---|
| **CALLBACK_OVERLAY_SHOWN** = 0 | Triggered when the Steam Overlay is shown or hidden. The callback receives a flag indicating whether the overlay is now active. |
| **CALLBACK_LEADERBOARD_FOUND** = 1 | Triggered when a requested leaderboard has been found on the Steam back-end. |
| **CALLBACK_LEADERBOARD_SCORES_UPLOADED** = 2 | Triggered when a score upload to a leaderboard has finished. The callback receives whether the upload failed and whether the stored score has changed. |
| **CALLBACK_LEADERBOARD_SCORES_DOWNLOADED** = 3 | Triggered when a leaderboard entries download has finished. The callback receives whether the download failed and the type of the data request. |

## PERSONA_STATE

| Name | Description |
|---|---|
| **PERSONA_STATE_OFFLINE** = 0 | Friend is not currently logged on. |
| **PERSONA_STATE_ONLINE** = 1 | Friend is logged on. |
| **PERSONA_STATE_BUSY** = 2 | User is on, but busy. |
| **PERSONA_STATE_AWAY** = 3 | Auto-away feature. |
| **PERSONA_STATE_SNOOZE** = 4 | Auto-away for a long time. |
| **PERSONA_STATE_LOOKING_TO_TRADE** = 5 | Online, trading. |
| **PERSONA_STATE_LOOKING_TO_PLAY** = 6 | Online, wanting to play. |

## FRIEND_FLAG

| Name | Description |
|---|---|
| **FRIEND_FLAG_NONE** = 0 | None. |
| **FRIEND_FLAG_BLOCKED** = 1 | Users that the current user has blocked from contacting. |
| **FRIEND_FLAG_FRIENDSHIP_REQUESTED** = 2 | Users that have sent a friend invite to the current user. |
| **FRIEND_FLAG_IMMEDIATE** = 4 | The current user's "regular" friends. |
| **FRIEND_FLAG_CLAN_MEMBER** = 8 | Users that are in one of the same (small) Steam groups as the current user. |
| **FRIEND_FLAG_ON_GAME_SERVER** = 16 | Users that are on the same game server. |
| **FRIEND_FLAG_REQUESTING_FRIENDSHIP** = 128 | Users that the current user has sent friend invites to. |
| **FRIEND_FLAG_REQUESTING_INFO** = 256 | Users that are currently sending additional info about themselves. |
| **FRIEND_FLAG_IGNORED** = 512 | Users that the current user has ignored from contacting them. |
| **FRIEND_FLAG_IGNORED_FRIEND** = 1024 | Users that have ignored the current user; but the current user still knows about them. |
| **FRIEND_FLAG_ALL** = 65535 | All friend flags. |

## FRIEND_RELATIONSHIP

| Name | Description |
|---|---|
| **FRIEND_RELATIONSHIP_NONE** = 0 | The users have no relationship. |
| **FRIEND_RELATIONSHIP_BLOCKED** = 1 | The user has just clicked Ignore on an friendship invite. This doesn't get stored. |
| **FRIEND_RELATIONSHIP_REQUEST_RECIPIENT** = 2 | The user has requested to be friends with the current user. |
| **FRIEND_RELATIONSHIP_FRIEND** = 3 | A "regular" friend. |
| **FRIEND_RELATIONSHIP_REQUEST_INITIATOR** = 4 | The current user has sent a friend invite. |
| **FRIEND_RELATIONSHIP_IGNORED** = 5 | The current user has explicit blocked this other user from comments/chat/etc. This is stored. |
| **FRIEND_RELATIONSHIP_IGNORED_FRIEND** = 6 | The user has ignored the current user. |

## OVERLAY_TO_STORE

| Name | Description |
|---|---|
| **OVERLAY_TO_STORE_FLAG_NONE** = 0 | No. |
| **OVERLAY_TO_STORE_ADD_TO_CART** = 1 | Add the specified app ID to the user's cart. |
| **OVERLAY_TO_STORE_ADD_TO_CART_AND_SHOW** = 2 | Add the specified app ID to the user's cart and show the store page. |

## OVERLAY_POSITION

| Name | Description |
|---|---|
| **OVERLAY_POSITION_TOP_LEFT** = 0 | Top left corner position of the overlay notification popup. |
| **OVERLAY_POSITION_TOP_RIGHT** = 1 | Top right corner position of the overlay notification popup. |
| **OVERLAY_POSITION_BOTTOM_LEFT** = 2 | Bottom left corner position of the overlay notification popup. |
| **OVERLAY_POSITION_BOTTOM_RIGHT** = 3 | Bottom right corner position of the overlay notification popup. |

## OVERLAY_TO_WEB_PAGE_MODE

Overlay mode to be used.
| Name | Description |
|---|---|
| **OVERLAY_TO_WEB_PAGE_MODE_DEFAULT** = 0 | The web page is opened in the standard Steam Overlay browser window. |
| **OVERLAY_TO_WEB_PAGE_MODE_MODAL** = 1 | The web page is opened in a modal Steam Overlay browser window that the user must dismiss before returning to the game. |

### Members

## Steam::PERSONA_STATE getMyState () const

Returns the current friend status of the current user. One of the [PERSONA_STATE_*](#PERSONA_STATE_OFFLINE) values.
### Return value

Current friend status of the current user
## const char * getMyName () const

Returns the current persona (display) name of the current user. This is the same name that is displayed on the user's community profile page.
### Return value

Current persona (display) name of the current user
## unsigned long long getMyUserID () const

Returns the current ID of the current user.
### Return value

Current ID of the current user
## bool isOverlayShown () const

Returns the current value indicating if the Steam Overlay is running and the user can access it.
### Return value

**true** if the Steam Overlay is running and the user can access it; otherwise **false**.
## const char * getUserDataFolder () const

Returns the current name of the user data folder.
### Return value

Current name of the user data folder
## const char * getAvailableGameLanguages () const

Returns the current comma-separated list of languages.
### Return value

Current comma-separated list of languages
## const char * getCurrentGameLanguage () const

Returns the current language that the user has set.
### Return value

Current language that the user has set
## bool isVACBanned () const

Returns the current value indicating if the user has a VAC ban on their account.
### Return value

**true** if the user has a VAC ban on their account; otherwise **false**.
## bool isCybercafe () const

Returns the current value specifying if the current app is for cyber cafes.
### Return value

**true** if the current app is for cyber cafes; otherwise **false**.
## bool isLowViolence () const

Returns the current value indicating if the license owned by the user provides low violence depots.
### Return value

**true** if the license owned by the user provides low violence depots; otherwise **false**.
## bool isSubscribed () const

Returns the current value indicating if the user is allowed to run the current app.
### Return value

**true** if the user is allowed to run the current app; otherwise **false**.
## int getAppID () const

Returns the current Steam AppID.
### Return value

Current Steam AppID
---

## void showOverlay ( const char * dialog )

Opens the *Steam Overlay* to the specified dialog.
### Arguments

- *const char ** **dialog** - The dialog to open. Valid options are: *"friends", "community", "players", "settings", "officialgamegroup", "stats", "achievements"*.

## void showOverlayToWebPage ( const char * url , Steam::OVERLAY_TO_WEB_PAGE_MODE mode )

Activates *Steam Overlay* web browser directly to the specified URL.
### Arguments

- *const char ** **url** - The webpage to open (a fully qualified address with the protocol is required).
- *[Steam::OVERLAY_TO_WEB_PAGE_MODE](../../../../api/library/plugins/steam/class.steam_cpp.md#OVERLAY_TO_WEB_PAGE_MODE)* **mode** - Overlay mode to be set. One of the *[OVERLAY_TO_WEB_PAGE_MODE_*](#OVERLAY_TO_WEB_PAGE_MODE_DEFAULT)* values.

## void showOverlayToUser ( const char * dialog , unsigned long long steam_id )

Opens the *Steam Overlay* to the specified dialog.
### Arguments

- *const char ** **dialog** - The dialog to open. Valid options are: *"steamid", "chat", "jointrade", "stats", "achievements", "friendadd", "friendremove", "friendrequestaccept", "friendrequestignore"*.
- *unsigned long long* **steam_id** - The Steam ID of the context to open this dialog to.

## void showOverlayToStore ( int app_id , Steam::OVERLAY_TO_STORE store_flag )

Activates the *Steam Overlay* to the Steam store page for the provided app.
### Arguments

- *int* **app_id** - The app ID to show the store page of.
- *[Steam::OVERLAY_TO_STORE](../../../../api/library/plugins/steam/class.steam_cpp.md#OVERLAY_TO_STORE)* **store_flag** - Flag to modify the behavior when the page opens, one of the [OVERLAY_TO_STORE_*](#OVERLAY_TO_STORE_FLAG_NONE) values.

## void showOverlayInviteDialog ( unsigned long long steam_id_lobby )

Activates the *Steam Overlay* to open the invite dialog. Invitations sent from this dialog will be for the provided lobby.
### Arguments

- *unsigned long long* **steam_id_lobby** - The Steam ID of the lobby that selected users will be invited to.

## void setOverlayNotificationPosition ( Steam::OVERLAY_POSITION position )

Sets which corner the *Steam Overlay* notification popup should display itself in.
### Arguments

- *[Steam::OVERLAY_POSITION](../../../../api/library/plugins/steam/class.steam_cpp.md#OVERLAY_POSITION)* **position** - The overlay notification popup position, one of the [OVERLAY_POSITION_*](#OVERLAY_POSITION_TOP_LEFT) values.

## const char * getUserName ( unsigned long long steam_id_friend )

Returns the specified user's persona (display) name.
### Arguments

- *unsigned long long* **steam_id_friend** - The Steam ID of the user.

### Return value

The current users persona name in UTF-8 format. Guaranteed to not be NULL. Returns an empty string (""), or "[unknown]" if the Steam ID is invalid or not known to the caller.
## int getNumFriends ( int friend_flags )

Returns the number of users the client knows about who meet a specified criteria (friends, blocked, users on the same server, etc.).
### Arguments

- *int* **friend_flags** - A combined union (binary "or") of one or more [FRIEND_FLAG_*](#FRIEND_FLAG_NONE) values.

### Return value

The number of users that meet the specified criteria. Returns -1 if the current user is not logged on.
## unsigned long long getFriendByIndex ( int ifriend , int ifriend_flags )

Returns the Steam ID of the friend at the specified index in the list of users that meet the given criteria.
### Arguments

- *int* **ifriend** - Index of the friend, in the range from 0 to the value returned by [getNumFriends()](#getNumFriends_int_int) for the same flags.
- *int* **ifriend_flags** - A combined union (binary "or") of one or more [FRIEND_FLAG_*](#FRIEND_FLAG_NONE) values, matching the flags passed to [getNumFriends()](#getNumFriends_int_int).

### Return value

The Steam ID of the friend at the given index.
## Steam::FRIEND_RELATIONSHIP getUserRelationship ( unsigned long long steam_id_friend )

Returns a relationship to a specified user.
### Arguments

- *unsigned long long* **steam_id_friend** - The Steam ID of the other user.

### Return value

Relationship to a specified user, one of the [FRIEND_RELATIONSHIP_*](#FRIEND_RELATIONSHIP_NONE) values.
## Steam::PERSONA_STATE getUserPersonaState ( unsigned long long steam_id_friend )

Returns the status of the friend.
### Arguments

- *unsigned long long* **steam_id_friend** - Steam ID of the user.

### Return value

Status of the friend, one of the [PERSONA_STATE_*](#PERSONA_STATE_OFFLINE) values.
## Variable getUserAvatarSmall ( unsigned long long id )

Returns a handle to the small avatar for the specified user.
### Arguments

- *unsigned long long* **id** - Steam ID of the user.

### Return value

A Steam handle to the small (32*32 px) image. Returns 0 if no avatar is set for the user.
## Variable getUserAvatarMedium ( unsigned long long id )

Returns a handle to the medium avatar for the specified user.
### Arguments

- *unsigned long long* **id** - Steam ID of the user.

### Return value

A Steam handle to the small (64x64 px) image. Returns 0 if no avatar is set for the user.
## Variable getUserAvatarLarge ( unsigned long long id )

Returns a handle to the large avatar for the specified user.
### Arguments

- *unsigned long long* **id** - Steam ID of the user.

### Return value

A Steam handle to the large (128*128 px) image. Returns 0 if no avatar is set for the user.
## SteamLeaderboard * createLeaderboard ( const char * name )

Returns the leaderboard interface.
### Arguments

- *const char ** **name** - Name of the leaderboard to be created.

### Return value

Leaderboard interface.
## SteamLeaderboard * getLeaderboard ( int id )

Returns the leaderboard interface.
### Arguments

- *int* **id** - ID of the leaderboard to view.

### Return value

Leaderboard interface.
## void deleteLeaderboard ( SteamLeaderboard * OUT_leaderboard )

Deletes the leaderboard.
### Arguments

- *[SteamLeaderboard](../../../../api/library/plugins/steam/class.steamleaderboard_cpp.md) ** **OUT_leaderboard** - Leaderboard interface. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void * addCallback ( Steam::CALLBACK_INDEX callback , Unigine:: CallbackBase * func )


Adds a callback of the specified type. The signature of the callback function depends on the callback type:


- [CALLBACK_OVERLAY_SHOWN](#CALLBACK_OVERLAY_SHOWN) - **void callback(unsigned char shown)**
- [CALLBACK_LEADERBOARD_FOUND](#CALLBACK_LEADERBOARD_FOUND) - **void callback(int id)**
- [CALLBACK_LEADERBOARD_SCORES_UPLOADED](#CALLBACK_LEADERBOARD_SCORES_UPLOADED) - **void callback(int id, int failed, unsigned char score_changed)**
- [CALLBACK_LEADERBOARD_SCORES_DOWNLOADED](#CALLBACK_LEADERBOARD_SCORES_DOWNLOADED) - **void callback(int id, int failed, int data_request)**


### Arguments

- *[Steam::CALLBACK_INDEX](../../../../api/library/plugins/steam/class.steam_cpp.md#CALLBACK_INDEX)* **callback** - Callback type. One of the following values:

  - [CALLBACK_OVERLAY_SHOWN](#CALLBACK_OVERLAY_SHOWN)
  - [CALLBACK_LEADERBOARD_FOUND](#CALLBACK_LEADERBOARD_FOUND)
  - [CALLBACK_LEADERBOARD_SCORES_UPLOADED](#CALLBACK_LEADERBOARD_SCORES_UPLOADED)
  - [CALLBACK_LEADERBOARD_SCORES_DOWNLOADED](#CALLBACK_LEADERBOARD_SCORES_DOWNLOADED)
- *Unigine::[CallbackBase](../../../../api/library/common/callbacks/class.callbackbase_cpp.md) ** **func** - Callback pointer.

### Return value

ID of the added callback, if the callback was added successfully; otherwise, **-1**.
## bool removeCallback ( Steam::CALLBACK_INDEX callback , void * id )

Removes the callback with the given ID from the list of callbacks of the specified type.
### Arguments

- *[Steam::CALLBACK_INDEX](../../../../api/library/plugins/steam/class.steam_cpp.md#CALLBACK_INDEX)* **callback** - Callback type. One of the following values:

  - [CALLBACK_OVERLAY_SHOWN](#CALLBACK_OVERLAY_SHOWN)
  - [CALLBACK_LEADERBOARD_FOUND](#CALLBACK_LEADERBOARD_FOUND)
  - [CALLBACK_LEADERBOARD_SCORES_UPLOADED](#CALLBACK_LEADERBOARD_SCORES_UPLOADED)
  - [CALLBACK_LEADERBOARD_SCORES_DOWNLOADED](#CALLBACK_LEADERBOARD_SCORES_DOWNLOADED)
- *void ** **id** - ID of the callback to be removed (returned by [addCallback()](#addCallback_int_CallbackBase_ptr_void_ptr)).

### Return value

true if the callback with the given ID was removed successfully; otherwise, false.
## void clearCallbacks ( Steam::CALLBACK_INDEX callback )

Clears all added callbacks of the specified type.
### Arguments

- *[Steam::CALLBACK_INDEX](../../../../api/library/plugins/steam/class.steam_cpp.md#CALLBACK_INDEX)* **callback** - Callback type. One of the following values:

  - [CALLBACK_OVERLAY_SHOWN](#CALLBACK_OVERLAY_SHOWN)
  - [CALLBACK_LEADERBOARD_FOUND](#CALLBACK_LEADERBOARD_FOUND)
  - [CALLBACK_LEADERBOARD_SCORES_UPLOADED](#CALLBACK_LEADERBOARD_SCORES_UPLOADED)
  - [CALLBACK_LEADERBOARD_SCORES_DOWNLOADED](#CALLBACK_LEADERBOARD_SCORES_DOWNLOADED)
